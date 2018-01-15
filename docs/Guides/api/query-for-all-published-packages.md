---
title: "nuget.org に発行されたすべてのパッケージに対するクエリの実行 | Microsoft Docs"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 11/2/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 5d017cd4-3d75-4341-ba90-3c57be093b7d
description: "NuGet API を使用して、nuget.org に発行されたすべてのパッケージに対してクエリを実行し、時間が経過しても最新の状態を把握することができます。"
keywords: "NuGet API ですべてのパッケージを列挙する, NuGet API でパッケージをレプリケートする, nuget.org に発行された最新のパッケージ"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5559a7cd104861b1a10aa8d1513696e609c51c15
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a>nuget.org に発行されたすべてのパッケージに対するクエリの実行

従来の OData V2 API に共通のクエリ パターンの 1 つは、nuget.org に発行されたすべてのパッケージを、そのパッケージの発行順に列挙するというものでした。 nuget.org に対するこの種のクエリに必要なシナリオは、次のように大きく異なります。

- nuget.org を完全にレプリケートする
- パッケージの新しいバージョンがリリースされたときに検出する
- 使用しているパッケージに依存するパッケージを検索する

これを行う従来の方法は、一般的に、タイムスタンプによる OData パッケージ エンティティの並べ替え、および `skip` と `top` (ページ サイズ) パラメーターを使用する大規模な結果セットでのページングによって異なりました。 残念ながら、この方法には次のようないくつかの欠点があります。

- 多くの場合、クエリはデータに対して変更順に実行されるため、パッケージが欠落する可能性がある
- クエリが最適化されていないため、クエリの応答時間が遅くなる (最も最適化されたクエリとは、公式の NuGet クライアントの主要なシナリオをサポートするクエリのことです)
- 使用されていない、ドキュメント化もされていない API の使用 (このようなクエリのサポートは将来的に保証されないことを意味します)
- 正確な発生順に履歴を再生できない

このような理由から、以下のガイドに従うことで、より信頼性の高い将来性のある方法で前述のシナリオに対処できます。

## <a name="overview"></a>概要

このガイドの中心となるのは、**カタログ**と呼ばれる [NuGet API](../../api/overview.md) のリソースです。 カタログは追加専用の API であり、これを使用することで、呼び出し元は nuget.org で追加、変更、および削除されたパッケージのすべての履歴を確認することができます。nuget.org に発行されたパッケージのすべて (あるいは一部でも) に関心がある場合、カタログは、時間が経過しても現在使用可能なパッケージ セットを常に把握することができる優れた方法です。

このガイドは簡単なチュートリアルであるため、カタログの詳細については、[API 参照に関するドキュメント](../../api/catalog-resource.md)を参照してください。

次の手順は任意のプログラミング言語で実行できます。 完全な実行サンプルが必要な場合は、以下の [C# のサンプル](#c-sample-code)を参照してください。

それ以外の場合は、以下のガイドに従って、信頼性の高いカタログ リーダーをビルドします。

## <a name="initialize-a-cursor"></a>カーソルを初期化する

信頼性の高いカタログ リーダーをビルドする最初の手順は、カーソルの実装です。 カタログ カーソルの設計の詳細については、[カタログ参照に関するドキュメント](../../api/catalog-resource.md#cursor)を参照してください。 要するに、カーソルは、カタログ内のイベントがどの時点まで処理されたかを示すものです。 カタログ内のイベントはあるパッケージの発行と他のパッケージの変更を示します。 これまでに (開始以降) NuGet に発行されたすべてのパッケージに関心がある場合は、カーソルを初期化してタイムスタンプが "最小値" (.NET の場合は `DateTime.MinValue` など) になるようにします。 これから発行されるパッケージのみに関心がある場合は、カーソル値を初期化する際に現在のタイムスタンプを使用します。

このガイドでは、タイムスタンプが 1 時間前になるようにカーソルを初期化します。 ここでは、単にそのタイムスタンプをメモリに保存します。

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a>カタログ インデックス URL を判別する

NuGet API のすべてのリソース (エンドポイント) の場所は、[サービス インデックス](../../api/service-index.md)を使用して検出する必要があります。 このガイドでは nuget.org に焦点を当てているため、nuget.org のサービス インデックスを使用します。

```
GET https://api.nuget.org/v3/index.json
```

サービス ドキュメントは、nuget.org のすべてのリソースを含む JSON ドキュメントです。`@type` プロパティの値が `Catalog/3.0.0` のリソースを見つけてください。 関連付けられている `@id`プロパティの値は、カタログ インデックス自体の URL です。

## <a name="find-new-catalog-leaves"></a>新しいカタログ リーフを見つける

前の手順で見つけた `@id` プロパティの値を使用して、カタログ インデックスをダウンロードします。

```
GET https://api.nuget.org/v3/catalog0/index.json
```

[カタログ インデックス](../../api/catalog-resource.md#catalog-index)を逆シリアル化します。 すべての[カタログ ページ オブジェクト](../../api/catalog-resource.md#catalog-page-object-in-the-index)を、現在のカーソル値以下の `commitTimeStamp` でフィルタリングします。

残りのカタログ ページごとに、`@id` プロパティを使用して完全なドキュメントをダウンロードします。

```
GET https://api.nuget.org/v3/catalog0/page2926.json
```

[カタログ ページ](../../api/catalog-resource.md#catalog-page)を逆シリアル化します。 すべての[カタログ リーフ オブジェクト](../../api/catalog-resource.md#catalog-item-object-in-a-page)を、現在のカーソル値以下の `commitTimeStamp` でフィルタリングします。

フィルタリングされなかったカタログ ページをすべてダウンロードした後、カーソルのタイムスタンプから今までに発行、リスト解除、リスト、または削除されたパッケージを表す一連のカタログ リーフ オブジェクトが示されます。

## <a name="process-catalog-leaves"></a>カタログ リーフを処理する

この時点で、カタログ項目に対して必要なカスタム処理を実行することができます。 必要なものがパッケージの ID とバージョンのみである場合は、ページで検出されたカタログ項目オブジェクトの `nuget:id` および `nuget:version` プロパティを調べることができます。 必ず、`@type` プロパティを調べ、カタログ項目が既存のパッケージと削除されたパッケージのどちらに関するものであるかを確認してください。

パッケージに関するメタデータ (説明、依存関係、.nupkg のサイズなど) に関心がある場合は、`@id` プロパティを使用して[カタログ リーフ ドキュメント](../../api/catalog-resource.md#catalog-leaf)をフェッチできます。

```
GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json
```

このドキュメントには、[パッケージ メタデータ リソース](../../api/registration-base-url-resource.md)などに含まれるすべてのメタデータが示されます。

この手順では、カスタム ロジックを実装します。 このガイドの他の手順は、カタログ リーフでの実行内容に関係なく、ほとんど同じ方法で行われます。

### <a name="downloading-the-nupkg"></a>.nupkg のダウンロード

カタログで検出されたパッケージ用の .nupkg をダウンロードしたい場合は、[パッケージ コンテンツ リソース](../../api/package-base-address-resource.md)を使用できます。 ただし、パッケージがカタログで検出されてから、パッケージ コンテンツ リソースで使用できるようになるまで短い遅延が発生することに注意してください。 したがって、カタログで検出されたパッケージの .nupkg をダウンロードしようとしたときに `404 Not Found` が発生した場合は、しばらくしてから再試行するだけです。 この遅延の修正については、GitHub の問題 [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) で追跡されています。

## <a name="move-the-cursor-forward"></a>カーソルを先に進める

カタログ項目を正しく処理したら、保存する新しいカーソル値を判別する必要があります。 これを行うには、処理したすべてのカタログ項目の最大 (最新) `commitTimeStamp` を検索します。 これが新しいカーソル値になります。 データベース、ファイル システム、または BLOB ストレージなどのいくつかの固定ストアに保存します。 カタログ項目をさらに取得する場合は、この固定ストアのカーソル値を初期化して、[最初の手順](#initialize-a-cursor)から開始するだけです。

アプリケーションが例外やフォールトをスローする場合は、カーソルを先に進めないでください。 カーソルを先に進めるということは、カーソルの前のカタログ項目を再度処理する必要がないことを意味します。

なんらかの理由で、カタログ リーフの処理方法にバグが発生した場合は、その時点までカーソルを戻すだけで、コードで以前のカタログ項目を再処理することができます。

## <a name="c-sample-code"></a>C# のサンプル コード

カタログは HTTP 経由で使用可能な一連の JSON ドキュメントであるため、HTTP クライアントと JSON デシリアライザーを持つ任意のプログラミング言語を使用して対話することができます。

C# のサンプルは、[NuGet/Sample リポジトリ](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)で入手可能です。

```
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a>カタログ SDK

カタログを使用する場合、プレリリース版の .NET カタログ SDK パッケージである [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog) を使用するのが最も簡単な方法です。
このパッケージは、`nuget-build` MyGet フィード (NuGet パッケージ ソース URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json` を使用する場合) で入手可能です。

このパッケージを、`netstandard1.3` 以上 (.NET Framework 4.6 など) と互換性のあるプロジェクトにインストールすることができます。

このパッケージを使用するサンプルは、GitHub の [NuGet.Protocol.Catalog.Sample プロジェクト](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)で入手できます。

#### <a name="sample-output"></a>出力例

```
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a>最小サンプル

カタログとの対話を詳細に示す、いくつかの依存関係を含む例については、[CatalogReaderExample サンプル プロジェクト](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)を参照してください。
プロジェクトは `netcoreapp2.0` をターゲットとし、[NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (サービス インデックスを解決する場合) および [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (JSON シリアル化解除の場合) に依存します。

コードの主なロジックは [Program.cs ファイル](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)に表示されます。

#### <a name="sample-output"></a>出力例

```
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
