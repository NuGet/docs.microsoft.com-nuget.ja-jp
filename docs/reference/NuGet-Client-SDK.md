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
# <a name="nuget-client-sdk"></a><span data-ttu-id="577fd-103">NuGet クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="577fd-103">NuGet Client SDK</span></span>

<span data-ttu-id="577fd-104">*Nuget クライアント SDK*は、nuget パッケージのグループを参照します。</span><span class="sxs-lookup"><span data-stu-id="577fd-104">The *NuGet Client SDK* refers to a group of NuGet packages:</span></span>

* <span data-ttu-id="577fd-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -HTTP およびファイルベースの NuGet フィードとの対話に使用されます</span><span class="sxs-lookup"><span data-stu-id="577fd-105">[`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) - Used to interact with HTTP and file-based NuGet feeds</span></span>
* <span data-ttu-id="577fd-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) -NuGet パッケージを操作するために使用します。</span><span class="sxs-lookup"><span data-stu-id="577fd-106">[`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) - Used to interact with NuGet packages.</span></span> <span data-ttu-id="577fd-107">`NuGet.Protocol` がこのパッケージに依存しています</span><span class="sxs-lookup"><span data-stu-id="577fd-107">`NuGet.Protocol` depends on this package</span></span>

<span data-ttu-id="577fd-108">これらのパッケージのソースコードは、 [nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) GitHub リポジトリで確認できます。</span><span class="sxs-lookup"><span data-stu-id="577fd-108">You can find the source code for these packages in the [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client) GitHub repository.</span></span>

> [!Note]
> <span data-ttu-id="577fd-109">NuGet サーバープロトコルに関するドキュメントについては、 [Nuget サーバー API](~/api/overview.md)に関するドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="577fd-109">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="getting-started"></a><span data-ttu-id="577fd-110">作業の開始</span><span class="sxs-lookup"><span data-stu-id="577fd-110">Getting started</span></span>

### <a name="install-the-package"></a><span data-ttu-id="577fd-111">パッケージをインストールする</span><span class="sxs-lookup"><span data-stu-id="577fd-111">Install the package</span></span>

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a><span data-ttu-id="577fd-112">例</span><span class="sxs-lookup"><span data-stu-id="577fd-112">Examples</span></span>

<span data-ttu-id="577fd-113">これらの例については、GitHub の[サンプル](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples)プロジェクトを参照してください。</span><span class="sxs-lookup"><span data-stu-id="577fd-113">You can find these examples on the [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) project on GitHub.</span></span>

### <a name="list-package-versions"></a><span data-ttu-id="577fd-114">パッケージのバージョンを一覧表示する</span><span class="sxs-lookup"><span data-stu-id="577fd-114">List package versions</span></span>

<span data-ttu-id="577fd-115">[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md#enumerate-package-versions)を使用して Newtonsoft. Json のすべてのバージョンを検索します。</span><span class="sxs-lookup"><span data-stu-id="577fd-115">Find all versions of Newtonsoft.Json using the [NuGet V3 Package Content API](../api/package-base-address-resource.md#enumerate-package-versions):</span></span>

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a><span data-ttu-id="577fd-116">パッケージをダウンロードする</span><span class="sxs-lookup"><span data-stu-id="577fd-116">Download a package</span></span>

<span data-ttu-id="577fd-117">[NuGet V3 パッケージコンテンツ API](../api/package-base-address-resource.md)を使用して Newtonsoft 12.0.1 をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="577fd-117">Download Newtonsoft.Json v12.0.1 using the [NuGet V3 Package Content API](../api/package-base-address-resource.md):</span></span>

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a><span data-ttu-id="577fd-118">パッケージメタデータを取得する</span><span class="sxs-lookup"><span data-stu-id="577fd-118">Get package metadata</span></span>

<span data-ttu-id="577fd-119">[NuGet V3 パッケージメタデータ API](../api/registration-base-url-resource.md)を使用して、"Newtonsoft. Json" パッケージのメタデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="577fd-119">Get the metadata for the "Newtonsoft.Json" package using the [NuGet V3 Package Metadata API](../api/registration-base-url-resource.md):</span></span>

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a><span data-ttu-id="577fd-120">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="577fd-120">Search packages</span></span>

<span data-ttu-id="577fd-121">[NuGet V3 SEARCH API](../api/search-query-service-resource.md)を使用して、"json" パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="577fd-121">Search for "json" packages using the [NuGet V3 Search API](../api/search-query-service-resource.md):</span></span>

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a><span data-ttu-id="577fd-122">サードパーティのドキュメント</span><span class="sxs-lookup"><span data-stu-id="577fd-122">Third-party documentation</span></span>

<span data-ttu-id="577fd-123">API の一部の例とドキュメントは、次のブログシリーズで、発行済み2016を使用して確認できます。</span><span class="sxs-lookup"><span data-stu-id="577fd-123">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="577fd-124">NuGet v3 ライブラリの調査、パート 1: 概要と概念</span><span class="sxs-lookup"><span data-stu-id="577fd-124">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="577fd-125">NuGet v3 ライブラリの調査、パート 2: パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="577fd-125">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="577fd-126">NuGet v3 ライブラリの調査、パート 3: パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="577fd-126">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="577fd-127">これらのブログ投稿は、 **3.4.3**バージョンの NUGET クライアント SDK パッケージがリリースされた直後に作成されました。</span><span class="sxs-lookup"><span data-stu-id="577fd-127">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="577fd-128">新しいバージョンのパッケージは、ブログの投稿の情報と互換性がない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="577fd-128">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="577fd-129">Martin Björkström のブログシリーズでは、NuGet クライアント SDK を使用して NuGet パッケージをインストールするためのさまざまなアプローチを紹介しています。</span><span class="sxs-lookup"><span data-stu-id="577fd-129">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK to install NuGet packages:</span></span>

- [<span data-ttu-id="577fd-130">NuGet v3 ライブラリの再度</span><span class="sxs-lookup"><span data-stu-id="577fd-130">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
