---
title: NuGet クライアント SDK
description: API は進化していますが、まだ文書化されていませんが、例については Dave Glick のブログを参照してください。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: f9e08d37b30dfea83fd9b61f168c1e20f530ff9f
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859409"
---
# <a name="nuget-client-sdk"></a>NuGet クライアント SDK

*Nuget クライアント SDK* は、nuget パッケージのグループを参照します。

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP およびファイルベースの NuGet フィードとの対話に使用されます。
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet パッケージとの対話に使用されます。 `NuGet.Protocol` このパッケージに依存

これらのパッケージのソースコードは、 [nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) GitHub リポジトリで確認できます。
これらの例のソースコードについては、GitHub の [サンプル](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) プロジェクトを参照してください。

> [!Note]
> NuGet サーバープロトコルに関するドキュメントについては、 [Nuget サーバー API](~/api/overview.md)に関するドキュメントを参照してください。

## <a name="nugetprotocol"></a>NuGet. プロトコル

パッケージをインストールして、 `NuGet.Protocol` HTTP およびフォルダーベースの NuGet パッケージフィードと対話します。

```ps1
dotnet add package NuGet.Protocol
```

### <a name="list-package-versions"></a>パッケージのバージョンを一覧表示する

[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md#enumerate-package-versions)を使用して Newtonsoft.Jsのすべてのバージョンを検索します。

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>パッケージをダウンロードする

[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md)を使用して、Newtonsoft.Json v 12.0.1 をダウンロードします。

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>パッケージメタデータを取得する

[NuGet V3 パッケージメタデータ API](../api/registration-base-url-resource.md)を使用して、"Newtonsoft.Json" パッケージのメタデータを取得します。

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>パッケージの検索

[NuGet V3 SEARCH API](../api/search-query-service-resource.md)を使用して、"json" パッケージを検索します。

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>パッケージをプッシュする

[NuGet V3 プッシュおよび削除 API](../api/package-publish-resource.md)を使用してパッケージをプッシュします。

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>パッケージを削除する

[NuGet V3 プッシュおよび削除 API](../api/package-publish-resource.md)を使用してパッケージを削除します。

> [!Note]
> NuGet サーバーは、パッケージ削除要求を "ハード削除"、"論理的な削除"、"一覧から削除" として解釈することができます。
> たとえば、nuget.org は package delete 要求を "一覧から削除" と解釈します。 このプラクティスの詳細については、「 [パッケージの削除](../nuget-org/policies/deleting-packages.md) 」ポリシーを参照してください。

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>認証済みフィードの使用

[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol)認証されたフィードを操作するには、を使用します。

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet. パッケージング

`NuGet.Packaging`ストリームからとのファイルを操作するパッケージをインストールし `.nupkg` `.nuspec` ます。

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>パッケージを作成する

を使用してパッケージを作成し、メタデータを設定し、依存関係を追加し [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) ます。

> [!IMPORTANT]
> NuGet パッケージは、公式の NuGet ツールを使用して作成することを強くお勧めします。この低レベルの API は使用し **ません** 。 適切な形式のパッケージに重要な特性がいくつかあり、最新バージョンのツールを使用すると、これらのベストプラクティスを組み込むことができます。
> 
> NuGet パッケージの作成の詳細については、「 [パッケージ作成ワークフロー](../create-packages/overview-and-workflow.md) の概要」および公式パックツール (たとえば、 [dotnet CLI の使用](../create-packages/creating-a-package-dotnet-cli.md)) のドキュメントを参照してください。

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>パッケージの読み取り

を使用してファイルストリームからパッケージを読み取り [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) ます。

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>サードパーティのドキュメント

API の一部の例とドキュメントは、次のブログシリーズで、発行済み2016を使用して確認できます。

- [NuGet v3 ライブラリの調査、パート 1: 概要と概念](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [NuGet v3 ライブラリの調査、パート 2: パッケージの検索](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [NuGet v3 ライブラリの調査、パート 3: パッケージのインストール](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> これらのブログ投稿は、 **3.4.3** バージョンの NUGET クライアント SDK パッケージがリリースされた直後に作成されました。
> 新しいバージョンのパッケージは、ブログの投稿の情報と互換性がない可能性があります。

Martin Björkström のブログシリーズでは、NuGet クライアント SDK を使用して NuGet パッケージをインストールするためのさまざまなアプローチを紹介しています。

- [NuGet v3 ライブラリの再度](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
