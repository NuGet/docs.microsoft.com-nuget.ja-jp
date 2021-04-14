---
title: NuGet クライアント SDK
description: API は進化していますが、まだ文書化されていませんが、例については Dave Glick のブログを参照してください。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387388"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="cf074-103">NuGet クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="cf074-103">NuGet Client SDK</span></span>

<span data-ttu-id="cf074-104">*Nuget クライアント SDK* は、nuget パッケージのグループを参照します。</span><span class="sxs-lookup"><span data-stu-id="cf074-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="cf074-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP およびファイルベースの NuGet フィードとの対話に使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf074-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="cf074-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet パッケージとの対話に使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf074-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="cf074-107">`NuGet.Protocol` このパッケージに依存</span><span class="sxs-lookup"><span data-stu-id="cf074-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="cf074-108">これらのパッケージのソースコードは、 [nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) GitHub リポジトリで確認できます。</span><span class="sxs-lookup"><span data-stu-id="cf074-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>
<span data-ttu-id="cf074-109">これらの例のソースコードについては、GitHub の [サンプル](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) プロジェクトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf074-109">You can find the source code for these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) project on GitHub.</span></span>

> [!Note]
> <span data-ttu-id="cf074-110">NuGet サーバープロトコルに関するドキュメントについては、 [Nuget サーバー API](~/api/overview.md)に関するドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf074-110">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="nugetprotocol"></a><span data-ttu-id="cf074-111">NuGet. プロトコル</span><span class="sxs-lookup"><span data-stu-id="cf074-111">NuGet.Protocol</span></span>

<span data-ttu-id="cf074-112">パッケージをインストールして、 `NuGet.Protocol` HTTP およびフォルダーベースの NuGet パッケージフィードと対話します。</span><span class="sxs-lookup"><span data-stu-id="cf074-112">Install the `NuGet.Protocol` package to interact with HTTP and folder-based NuGet package feeds:</span></span>

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> <span data-ttu-id="cf074-113">`Repository.Factory` は名前空間で定義され、 `NuGet.Protocol.Core.Types` `GetCoreV3` メソッドは名前空間で定義された拡張メソッドです `NuGet.Protocol` 。</span><span class="sxs-lookup"><span data-stu-id="cf074-113">`Repository.Factory` is defined in the `NuGet.Protocol.Core.Types` namespace, and the `GetCoreV3` method is an extension method defined in the `NuGet.Protocol` namespace.</span></span> <span data-ttu-id="cf074-114">したがって、 `using` 両方の名前空間にステートメントを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cf074-114">Therefore, you will need to add `using` statements for both namespaces.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="cf074-115">パッケージのバージョンを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="cf074-115">List package versions</span></span>

<span data-ttu-id="cf074-116">[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md#enumerate-package-versions)を使用して Newtonsoft.Jsのすべてのバージョンを検索します。</span><span class="sxs-lookup"><span data-stu-id="cf074-116">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="cf074-117">パッケージをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="cf074-117">Download a package</span></span>

<span data-ttu-id="cf074-118">[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md)を使用して、Newtonsoft.Json v 12.0.1 をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="cf074-118">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="cf074-119">パッケージメタデータを取得する</span><span class="sxs-lookup"><span data-stu-id="cf074-119">Get package metadata</span></span>

<span data-ttu-id="cf074-120">[NuGet V3 パッケージメタデータ API](../api/registration-base-url-resource.md)を使用して、"Newtonsoft.Json" パッケージのメタデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="cf074-120">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="cf074-121">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="cf074-121">Search packages</span></span>

<span data-ttu-id="cf074-122">[NuGet V3 SEARCH API](../api/search-query-service-resource.md)を使用して、"json" パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="cf074-122">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a><span data-ttu-id="cf074-123">パッケージをプッシュする</span><span class="sxs-lookup"><span data-stu-id="cf074-123">Push a package</span></span>

<span data-ttu-id="cf074-124">[NuGet V3 プッシュおよび削除 API](../api/package-publish-resource.md)を使用してパッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="cf074-124">Push a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a><span data-ttu-id="cf074-125">パッケージを削除する</span><span class="sxs-lookup"><span data-stu-id="cf074-125">Delete a package</span></span>

<span data-ttu-id="cf074-126">[NuGet V3 プッシュおよび削除 API](../api/package-publish-resource.md)を使用してパッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="cf074-126">Delete a package using the [NuGet V3 Push and Delete API](../api/package-publish-resource.md):</span></span>

> [!Note]
> <span data-ttu-id="cf074-127">NuGet サーバーは、パッケージ削除要求を "ハード削除"、"論理的な削除"、"一覧から削除" として解釈することができます。</span><span class="sxs-lookup"><span data-stu-id="cf074-127">NuGet servers are free to interpret a package delete request as a "hard delete", "soft delete", or "unlist".</span></span>
> <span data-ttu-id="cf074-128">たとえば、nuget.org は package delete 要求を "一覧から削除" と解釈します。</span><span class="sxs-lookup"><span data-stu-id="cf074-128">For example, nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="cf074-129">このプラクティスの詳細については、「 [パッケージの削除](../nuget-org/policies/deleting-packages.md) 」ポリシーを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf074-129">For more information about this practice, see the [Deleting Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span>

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a><span data-ttu-id="cf074-130">認証済みフィードの使用</span><span class="sxs-lookup"><span data-stu-id="cf074-130">Work with authenticated feeds</span></span>

<span data-ttu-id="cf074-131">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol)認証されたフィードを操作するには、を使用します。</span><span class="sxs-lookup"><span data-stu-id="cf074-131">Use [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) to work with authenticated feeds.</span></span>

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a><span data-ttu-id="cf074-132">NuGet. パッケージング</span><span class="sxs-lookup"><span data-stu-id="cf074-132">NuGet.Packaging</span></span>

<span data-ttu-id="cf074-133">`NuGet.Packaging`ストリームからとのファイルを操作するパッケージをインストールし `.nupkg` `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="cf074-133">Install the `NuGet.Packaging` package to interact with `.nupkg` and `.nuspec` files from a stream:</span></span>

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a><span data-ttu-id="cf074-134">パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="cf074-134">Create a package</span></span>

<span data-ttu-id="cf074-135">を使用してパッケージを作成し、メタデータを設定し、依存関係を追加し [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) ます。</span><span class="sxs-lookup"><span data-stu-id="cf074-135">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf074-136">NuGet パッケージは、公式の NuGet ツールを使用して作成することを強くお勧めします。この低レベルの API は使用し **ません** 。</span><span class="sxs-lookup"><span data-stu-id="cf074-136">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="cf074-137">適切な形式のパッケージに重要な特性がいくつかあり、最新バージョンのツールを使用すると、これらのベストプラクティスを組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="cf074-137">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="cf074-138">NuGet パッケージの作成の詳細については、「 [パッケージ作成ワークフロー](../create-packages/overview-and-workflow.md) の概要」および公式パックツール (たとえば、 [dotnet CLI の使用](../create-packages/creating-a-package-dotnet-cli.md)) のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf074-138">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="cf074-139">パッケージの読み取り</span><span class="sxs-lookup"><span data-stu-id="cf074-139">Read a package</span></span>

<span data-ttu-id="cf074-140">を使用してファイルストリームからパッケージを読み取り [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) ます。</span><span class="sxs-lookup"><span data-stu-id="cf074-140">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="cf074-141">サードパーティのドキュメント</span><span class="sxs-lookup"><span data-stu-id="cf074-141">Third-party documentation</span></span>

<span data-ttu-id="cf074-142">API の一部の例とドキュメントは、次のブログシリーズで、発行済み2016を使用して確認できます。</span><span class="sxs-lookup"><span data-stu-id="cf074-142">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="cf074-143">NuGet v3 ライブラリの調査、パート 1: 概要と概念</span><span class="sxs-lookup"><span data-stu-id="cf074-143">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="cf074-144">NuGet v3 ライブラリの調査、パート 2: パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="cf074-144">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="cf074-145">NuGet v3 ライブラリの調査、パート 3: パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="cf074-145">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="cf074-146">これらのブログ投稿は、 **3.4.3** バージョンの NUGET クライアント SDK パッケージがリリースされた直後に作成されました。</span><span class="sxs-lookup"><span data-stu-id="cf074-146">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="cf074-147">新しいバージョンのパッケージは、ブログの投稿の情報と互換性がない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="cf074-147">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="cf074-148">Martin Björkström のブログシリーズでは、NuGet クライアント SDK を使用して NuGet パッケージをインストールするためのさまざまなアプローチを紹介しています。</span><span class="sxs-lookup"><span data-stu-id="cf074-148">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="cf074-149">NuGet v3 ライブラリの再度</span><span class="sxs-lookup"><span data-stu-id="cf074-149">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
