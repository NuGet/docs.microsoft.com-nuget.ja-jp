---
title: パッケージの詳細 URL テンプレート、NuGet API
description: パッケージの詳細の URL テンプレートを使用すると、クライアントの UI に、より多くのパッケージ詳細への web リンクを表示できます。
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 1b84c6e88a56216e5747d5bc602219af6695c305
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76812936"
---
# <a name="package-details-url-template"></a><span data-ttu-id="24bf5-103">パッケージの詳細の URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="24bf5-103">Package details URL template</span></span>

<span data-ttu-id="24bf5-104">クライアントは、web ブラウザーでより多くのパッケージの詳細を表示するためにユーザーが使用できる URL を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="24bf5-104">It is possible for a client to build a URL that can be used by the user to see more package details in their web browser.</span></span> <span data-ttu-id="24bf5-105">これは、パッケージソースが、NuGet クライアントアプリケーションで表示される内容の範囲内に含まれない可能性があるパッケージに関する追加情報を表示する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="24bf5-105">This is useful when a package source wants to show additional information about a package that may not fit within the scope of what the NuGet client application shows.</span></span>

<span data-ttu-id="24bf5-106">この URL の作成に使用されるリソースは、[サービスインデックス](service-index.md)で見つかった `PackageDetailsUriTemplate` リソースです。</span><span class="sxs-lookup"><span data-stu-id="24bf5-106">The resource used for building this URL is the `PackageDetailsUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="24bf5-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="24bf5-107">Versioning</span></span>

<span data-ttu-id="24bf5-108">次の `@type` 値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="24bf5-108">The following `@type` values are used:</span></span>

<span data-ttu-id="24bf5-109">@type 値</span><span class="sxs-lookup"><span data-stu-id="24bf5-109">@type value</span></span>                     | <span data-ttu-id="24bf5-110">メモ</span><span class="sxs-lookup"><span data-stu-id="24bf5-110">Notes</span></span>
------------------------------- | -----
<span data-ttu-id="24bf5-111">PackageDetailsUriTemplate/5.1.0</span><span class="sxs-lookup"><span data-stu-id="24bf5-111">PackageDetailsUriTemplate/5.1.0</span></span> | <span data-ttu-id="24bf5-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="24bf5-112">The initial release</span></span>

## <a name="url-template"></a><span data-ttu-id="24bf5-113">URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="24bf5-113">URL template</span></span>

<span data-ttu-id="24bf5-114">次の API の URL は、前述のリソース `@type` の値のいずれかに関連付けられている `@id` プロパティの値です。</span><span class="sxs-lookup"><span data-stu-id="24bf5-114">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="24bf5-115">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="24bf5-115">HTTP methods</span></span>

<span data-ttu-id="24bf5-116">クライアントは、ユーザーの代わりにパッケージの詳細 URL に要求を送信することを意図していませんが、web ページは、web ブラウザーでクリックした URL を簡単に開くことができるように、`GET` メソッドをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="24bf5-116">Although the client is not intended to make requests to the package details URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="24bf5-117">URL を作成する</span><span class="sxs-lookup"><span data-stu-id="24bf5-117">Construct the URL</span></span>

<span data-ttu-id="24bf5-118">既知のパッケージ ID とバージョンを指定すると、クライアント実装は、web インターフェイスにアクセスするために使用する URL を作成できます。</span><span class="sxs-lookup"><span data-stu-id="24bf5-118">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="24bf5-119">クライアントの実装では、この構築された URL (またはクリック可能なリンク) をユーザーに表示して、URL に対して web ブラウザーを開いてパッケージの詳細を確認できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="24bf5-119">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and to learn more about the package.</span></span> <span data-ttu-id="24bf5-120">パッケージの詳細ページの内容は、サーバーの実装によって決まります。</span><span class="sxs-lookup"><span data-stu-id="24bf5-120">The contents of the package details page is determined by the server implementation.</span></span>

<span data-ttu-id="24bf5-121">URL は絶対 URL にする必要があり、スキーム (プロトコル) は HTTPS である必要があります。</span><span class="sxs-lookup"><span data-stu-id="24bf5-121">The URL must be an absolute URL and the scheme (protocol) must be HTTPS.</span></span>

<span data-ttu-id="24bf5-122">サービスインデックス内の `@id` の値は、次のプレースホルダートークンのいずれかを含む URL 文字列です。</span><span class="sxs-lookup"><span data-stu-id="24bf5-122">The value of the `@id` in the service index is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="24bf5-123">URL プレースホルダー</span><span class="sxs-lookup"><span data-stu-id="24bf5-123">URL placeholders</span></span>

<span data-ttu-id="24bf5-124">[名前]</span><span class="sxs-lookup"><span data-stu-id="24bf5-124">Name</span></span>        | <span data-ttu-id="24bf5-125">の型</span><span class="sxs-lookup"><span data-stu-id="24bf5-125">Type</span></span>    | <span data-ttu-id="24bf5-126">必須</span><span class="sxs-lookup"><span data-stu-id="24bf5-126">Required</span></span> | <span data-ttu-id="24bf5-127">メモ</span><span class="sxs-lookup"><span data-stu-id="24bf5-127">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="24bf5-128">string</span><span class="sxs-lookup"><span data-stu-id="24bf5-128">string</span></span>  | <span data-ttu-id="24bf5-129">Ｘ</span><span class="sxs-lookup"><span data-stu-id="24bf5-129">no</span></span>       | <span data-ttu-id="24bf5-130">詳細を取得するパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="24bf5-130">The package ID to get details for</span></span>
`{version}` | <span data-ttu-id="24bf5-131">string</span><span class="sxs-lookup"><span data-stu-id="24bf5-131">string</span></span>  | <span data-ttu-id="24bf5-132">Ｘ</span><span class="sxs-lookup"><span data-stu-id="24bf5-132">no</span></span>       | <span data-ttu-id="24bf5-133">詳細を取得するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="24bf5-133">The package version to get details for</span></span>

<span data-ttu-id="24bf5-134">サーバーは `{id}` と `{version}` の値を大文字と小文字を区別して受け取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="24bf5-134">The server should accept `{id}` and `{version}` values with any casing.</span></span> <span data-ttu-id="24bf5-135">また、バージョンが[正規化](../concepts/package-versioning.md#normalized-version-numbers)されているかどうかはサーバーに依存しないようにしてください。</span><span class="sxs-lookup"><span data-stu-id="24bf5-135">In addition, the server should not be sensitive to whether the version is [normalized](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="24bf5-136">つまり、サーバーは、正規化されていないバージョンも受け入れる必要があります。</span><span class="sxs-lookup"><span data-stu-id="24bf5-136">In other words, the server should accept also accept non-normalized versions.</span></span>

<span data-ttu-id="24bf5-137">たとえば、nuget の [パッケージの詳細] テンプレートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="24bf5-137">For example, nuget.org's package details template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}

<span data-ttu-id="24bf5-138">クライアント実装で NuGet のパッケージ詳細へのリンクを表示する必要がある場合、バージョン4.3.0 では次の URL が生成され、ユーザーに提供されます。</span><span class="sxs-lookup"><span data-stu-id="24bf5-138">If the client implementation needs to display a link to the package details for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
