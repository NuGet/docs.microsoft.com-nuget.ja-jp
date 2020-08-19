---
title: NuGet クライアント SDK
description: API は進化していますが、まだ文書化されていませんが、例については Dave Glick のブログを参照してください。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622929"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="294e8-103">NuGet クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="294e8-103">NuGet Client SDK</span></span>

<span data-ttu-id="294e8-104">*Nuget クライアント SDK*は、nuget パッケージのグループを参照します。</span><span class="sxs-lookup"><span data-stu-id="294e8-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="294e8-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP およびファイルベースの NuGet フィードとの対話に使用されます。</span><span class="sxs-lookup"><span data-stu-id="294e8-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="294e8-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet パッケージとの対話に使用されます。</span><span class="sxs-lookup"><span data-stu-id="294e8-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="294e8-107">`NuGet.Protocol` このパッケージに依存</span><span class="sxs-lookup"><span data-stu-id="294e8-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="294e8-108">これらのパッケージのソースコードは、 [nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) GitHub リポジトリで確認できます。</span><span class="sxs-lookup"><span data-stu-id="294e8-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="294e8-109">NuGet サーバープロトコルに関するドキュメントについては、 [Nuget サーバー API](~/api/overview.md)に関するドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="294e8-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="294e8-110">作業の開始</span><span class="sxs-lookup"><span data-stu-id="294e8-110">Getting started</span></span>

### <a name="install-the-packages"></a><span data-ttu-id="294e8-111">パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="294e8-111">Install the packages</span></span>

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a><span data-ttu-id="294e8-112">例</span><span class="sxs-lookup"><span data-stu-id="294e8-112">Examples</span></span>

<span data-ttu-id="294e8-113">これらの例については、GitHub の [サンプル](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) プロジェクトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="294e8-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="294e8-114">パッケージのバージョンを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="294e8-114">List package versions</span></span>

<span data-ttu-id="294e8-115">[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md#enumerate-package-versions)を使用して Newtonsoft.Jsのすべてのバージョンを検索します。</span><span class="sxs-lookup"><span data-stu-id="294e8-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="294e8-116">パッケージをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="294e8-116">Download a package</span></span>

<span data-ttu-id="294e8-117">[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md)を使用して、Newtonsoft.Json v 12.0.1 をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="294e8-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="294e8-118">パッケージメタデータを取得する</span><span class="sxs-lookup"><span data-stu-id="294e8-118">Get package metadata</span></span>

<span data-ttu-id="294e8-119">[NuGet V3 パッケージメタデータ API](../api/registration-base-url-resource.md)を使用して、"Newtonsoft.Json" パッケージのメタデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="294e8-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="294e8-120">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="294e8-120">Search packages</span></span>

<span data-ttu-id="294e8-121">[NuGet V3 SEARCH API](../api/search-query-service-resource.md)を使用して、"json" パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="294e8-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a><span data-ttu-id="294e8-122">パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="294e8-122">Create a package</span></span>

<span data-ttu-id="294e8-123">を使用してパッケージを作成し、メタデータを設定し、依存関係を追加し [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) ます。</span><span class="sxs-lookup"><span data-stu-id="294e8-123">Create a package, set metadata, and add dependencies using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="294e8-124">NuGet パッケージは、公式の NuGet ツールを使用して作成することを強くお勧めします。この低レベルの API は使用し **ません** 。</span><span class="sxs-lookup"><span data-stu-id="294e8-124">It is strongly recommended that NuGet packages are created using the official NuGet tooling and **not** using this low-level API.</span></span> <span data-ttu-id="294e8-125">適切な形式のパッケージに重要な特性がいくつかあり、最新バージョンのツールを使用すると、これらのベストプラクティスを組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="294e8-125">There are a variety of characteristics important for a well-formed package and the latest version of tooling helps incorporate these best practices.</span></span>
> 
> <span data-ttu-id="294e8-126">NuGet パッケージの作成の詳細については、「 [パッケージ作成ワークフロー](../create-packages/overview-and-workflow.md) の概要」および公式パックツール (たとえば、 [dotnet CLI の使用](../create-packages/creating-a-package-dotnet-cli.md)) のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="294e8-126">For more information about creating NuGet packages, see the overview of the [package creation workflow](../create-packages/overview-and-workflow.md) and the documentation for official pack tooling (for example, [using the dotnet CLI](../create-packages/creating-a-package-dotnet-cli.md)).</span></span>

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a><span data-ttu-id="294e8-127">パッケージの読み取り</span><span class="sxs-lookup"><span data-stu-id="294e8-127">Read a package</span></span>

<span data-ttu-id="294e8-128">を使用してファイルストリームからパッケージを読み取り [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) ます。</span><span class="sxs-lookup"><span data-stu-id="294e8-128">Read a package from a file stream using [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging).</span></span>

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a><span data-ttu-id="294e8-129">サードパーティのドキュメント</span><span class="sxs-lookup"><span data-stu-id="294e8-129">Third-party documentation</span></span>

<span data-ttu-id="294e8-130">API の一部の例とドキュメントは、次のブログシリーズで、発行済み2016を使用して確認できます。</span><span class="sxs-lookup"><span data-stu-id="294e8-130">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="294e8-131">NuGet v3 ライブラリの調査、パート 1: 概要と概念</span><span class="sxs-lookup"><span data-stu-id="294e8-131">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="294e8-132">NuGet v3 ライブラリの調査、パート 2: パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="294e8-132">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="294e8-133">NuGet v3 ライブラリの調査、パート 3: パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="294e8-133">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="294e8-134">これらのブログ投稿は、 **3.4.3** バージョンの NUGET クライアント SDK パッケージがリリースされた直後に作成されました。</span><span class="sxs-lookup"><span data-stu-id="294e8-134">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="294e8-135">新しいバージョンのパッケージは、ブログの投稿の情報と互換性がない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="294e8-135">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="294e8-136">Martin Björkström のブログシリーズでは、NuGet クライアント SDK を使用して NuGet パッケージをインストールするためのさまざまなアプローチを紹介しています。</span><span class="sxs-lookup"><span data-stu-id="294e8-136">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="294e8-137">NuGet v3 ライブラリの再度</span><span class="sxs-lookup"><span data-stu-id="294e8-137">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
