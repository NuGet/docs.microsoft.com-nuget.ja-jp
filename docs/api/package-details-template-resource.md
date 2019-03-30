---
title: パッケージの詳細 URL テンプレートは、NuGet API
description: パッケージの詳細 URL テンプレートでは、パッケージの詳細へのリンクを web UI に表示するクライアントを使用できます。
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638075"
---
# <a name="package-details-url-template"></a><span data-ttu-id="da4ae-103">パッケージの詳細 URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="da4ae-103">Package details URL template</span></span>

<span data-ttu-id="da4ae-104">クライアント web ブラウザーでのパッケージ詳細を表示、ユーザーが使用できる URL を構築することができます。</span><span class="sxs-lookup"><span data-stu-id="da4ae-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="da4ae-105">これは、機能は、パッケージ ソースが、NuGet クライアント アプリケーションに表示される内容のスコープ内に収まらない可能性がありますパッケージに関する追加情報を表示するときに便利です。</span><span class="sxs-lookup"><span data-stu-id="da4ae-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="da4ae-106">この URL を構築するために使用されるリソースは、`PackageDetailsUriTemplate`リソースで見つかった、[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="da4ae-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="da4ae-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="da4ae-107">Versioning</span></span>

<span data-ttu-id="da4ae-108">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="da4ae-108">The following `@type` values are used:</span></span>

<span data-ttu-id="da4ae-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="da4ae-109">@type value</span></span>                     | <span data-ttu-id="da4ae-110">メモ</span><span class="sxs-lookup"><span data-stu-id="da4ae-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="da4ae-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="da4ae-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="da4ae-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="da4ae-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="da4ae-113">URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="da4ae-113">URL template</span></span>

<span data-ttu-id="da4ae-114">次の API の URL の値である、`@id`前述のリソースのいずれかに関連付けられているプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="da4ae-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="da4ae-115">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="da4ae-115">HTTP methods</span></span>

<span data-ttu-id="da4ae-116">Web ページをサポートする必要がありますが、クライアントは、ユーザーの代理として、パッケージの詳細 URL に対して要求を行うものではありません、`GET`クリックされた URL を web ブラウザーで簡単に開くことができるようにする方法。</span><span class="sxs-lookup"><span data-stu-id="da4ae-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="da4ae-117">URL を構築します。</span><span class="sxs-lookup"><span data-stu-id="da4ae-117">Construct the URL</span></span>

<span data-ttu-id="da4ae-118">既知のパッケージ ID とバージョンを指定すると、クライアントの実装は、web インターフェイスへのアクセスに使用する URL を構築できます。</span><span class="sxs-lookup"><span data-stu-id="da4ae-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="da4ae-119">クライアントの実装では、URL に web ブラウザーを開くと、パッケージの詳細についてようにユーザーにこの構築された URL (またはリンクのクリック可能な) を表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="da4ae-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="da4ae-120">パッケージ詳細ページの内容は、サーバーの実装によって決定されます。</span><span class="sxs-lookup"><span data-stu-id="da4ae-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="da4ae-121">絶対 URL である必要があります、URL と (protocol) スキームが HTTPS にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="da4ae-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="da4ae-122">値、`@id`サービス インデックスは、次のプレース ホルダーのトークンのいずれかを含む URL 文字列。</span><span class="sxs-lookup"><span data-stu-id="da4ae-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="da4ae-123">URL のプレース ホルダー</span><span class="sxs-lookup"><span data-stu-id="da4ae-123">URL placeholders</span></span>

<span data-ttu-id="da4ae-124">名前</span><span class="sxs-lookup"><span data-stu-id="da4ae-124">Name</span></span>        | <span data-ttu-id="da4ae-125">型</span><span class="sxs-lookup"><span data-stu-id="da4ae-125">Type</span></span>    | <span data-ttu-id="da4ae-126">必須</span><span class="sxs-lookup"><span data-stu-id="da4ae-126">Required</span></span> | <span data-ttu-id="da4ae-127">メモ</span><span class="sxs-lookup"><span data-stu-id="da4ae-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="da4ae-128">string</span><span class="sxs-lookup"><span data-stu-id="da4ae-128">string</span></span>  | <span data-ttu-id="da4ae-129">Ｘ</span><span class="sxs-lookup"><span data-stu-id="da4ae-129">no</span></span>       | <span data-ttu-id="da4ae-130">詳細を取得するパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="da4ae-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="da4ae-131">string</span><span class="sxs-lookup"><span data-stu-id="da4ae-131">string</span></span>  | <span data-ttu-id="da4ae-132">Ｘ</span><span class="sxs-lookup"><span data-stu-id="da4ae-132">no</span></span>       | <span data-ttu-id="da4ae-133">パッケージのバージョンの詳細を取得するには</span><span class="sxs-lookup"><span data-stu-id="da4ae-133">The package version to get details for</span></span>

<span data-ttu-id="da4ae-134">サーバーが受け入れる必要があります`{id}`と`{version}`任意の大文字と小文字の値。</span><span class="sxs-lookup"><span data-stu-id="da4ae-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="da4ae-135">さらに、サーバーすることはできません、バージョンがいるかどうかに機密性の高い[正規化された](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers)します。</span><span class="sxs-lookup"><span data-stu-id="da4ae-135">In addition, the server should not be sensitive to whether the version is [normalized](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers).</span></span> <span data-ttu-id="da4ae-136">つまり、このサーバーが受け入れる正規化されていないバージョンでも使用できます。</span><span class="sxs-lookup"><span data-stu-id="da4ae-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="da4ae-137">たとえば、nuget.org のパッケージ詳細のテンプレートは、ようになります。</span><span class="sxs-lookup"><span data-stu-id="da4ae-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="da4ae-138">クライアントの実装、パッケージの詳細を NuGet.Versioning 4.3.0 のリンクを表示する場合は、次の URL を生成し、ユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="da4ae-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
