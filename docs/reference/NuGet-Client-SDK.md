---
title: NuGet クライアント SDK
description: API は進化していますが、まだ文書化されていませんが、例については Dave Glick のブログを参照してください。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231241"
---
# <a name="nuget-client-sdk"></a>NuGet クライアント SDK

*Nuget クライアント SDK*は、nuget パッケージのグループを参照します。

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP およびファイルベースの NuGet フィードとの対話に使用されます
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet パッケージを操作するために使用します。 `NuGet.Protocol` がこのパッケージに依存しています

これらのパッケージのソースコードは、 [nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) GitHub リポジトリで確認できます。

> [!Note]
> NuGet サーバープロトコルに関するドキュメントについては、 [Nuget サーバー API](~/api/overview.md)に関するドキュメントを参照してください。

## <a name="getting-started"></a>作業の開始

### <a name="install-the-package"></a>パッケージをインストールする

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>例

これらの例については、GitHub の[サンプル](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples)プロジェクトを参照してください。

### <a name="list-package-versions"></a>パッケージのバージョンを一覧表示する

[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md#enumerate-package-versions)を使用して Newtonsoft. Json のすべてのバージョンを検索します。

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>パッケージをダウンロードする

[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md)を使用して Newtonsoft 12.0.1 をダウンロードします。

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>パッケージメタデータを取得する

[NuGet V3 パッケージメタデータ API](../api/registration-base-url-resource.md)を使用して、"Newtonsoft. Json" パッケージのメタデータを取得します。

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>パッケージの検索

[NuGet V3 SEARCH API](../api/search-query-service-resource.md)を使用して、"json" パッケージを検索します。

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a>サードパーティのドキュメント

API の一部の例とドキュメントは、次のブログシリーズで、発行済み2016を使用して確認できます。

- [NuGet v3 ライブラリの調査、パート 1: 概要と概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [NuGet v3 ライブラリの調査、パート 2: パッケージの検索](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [NuGet v3 ライブラリの調査、パート 3: パッケージのインストール](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> これらのブログ投稿は、 **3.4.3**バージョンの NUGET クライアント SDK パッケージがリリースされた直後に作成されました。
> 新しいバージョンのパッケージは、ブログの投稿の情報と互換性がない可能性があります。

Martin Björkström のブログシリーズでは、NuGet クライアント SDK を使用して NuGet パッケージをインストールするためのさまざまなアプローチを紹介しています。

- [NuGet v3 ライブラリの再度](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
