---
title: レポート不正使用 URL テンプレートは、NuGet API
description: レポートの不正使用 URL テンプレートは、その UI に、不正使用のリンクを表示するクライアントを使用できます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d0ff41b08eeba5a6e4bc7c44722b6bc57f502047
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549340"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="5a793-103">レポートの不正使用の URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="5a793-103">Report abuse URL template</span></span>

<span data-ttu-id="5a793-104">クライアントが特定のパッケージに関する不正使用を報告する、ユーザーが使用できる URL を構築するために可能性があります。</span><span class="sxs-lookup"><span data-stu-id="5a793-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="5a793-105">これは、機能は、パッケージ ソースがパッケージ ソースへのレポートの不正使用を委任するすべてのクライアント エクスペリエンス (でもサード パーティ) を有効にするときに便利です。</span><span class="sxs-lookup"><span data-stu-id="5a793-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="5a793-106">この URL を構築するために使用されるリソースは、`ReportAbuseUriTemplate`リソースで見つかった、[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="5a793-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="5a793-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="5a793-107">Versioning</span></span>

<span data-ttu-id="5a793-108">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="5a793-108">The following `@type` values are used:</span></span>

<span data-ttu-id="5a793-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="5a793-109">@type value</span></span>                       | <span data-ttu-id="5a793-110">メモ</span><span class="sxs-lookup"><span data-stu-id="5a793-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="5a793-111">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="5a793-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="5a793-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="5a793-112">The initial release</span></span>
<span data-ttu-id="5a793-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="5a793-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="5a793-114">エイリアス `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="5a793-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="5a793-115">URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="5a793-115">URL template</span></span>

<span data-ttu-id="5a793-116">次の API の URL の値である、`@id`前述のリソースのいずれかに関連付けられているプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="5a793-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="5a793-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="5a793-117">HTTP methods</span></span>

<span data-ttu-id="5a793-118">Web ページをサポートする必要がありますが、クライアントは、レポートの URL の不正使用に、ユーザーに代わって要求を行うものではありません、`GET`クリックされた URL を web ブラウザーで簡単に開くことができるようにする方法。</span><span class="sxs-lookup"><span data-stu-id="5a793-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="5a793-119">URL を構築します。</span><span class="sxs-lookup"><span data-stu-id="5a793-119">Construct the URL</span></span>

<span data-ttu-id="5a793-120">既知のパッケージ ID とバージョンを指定すると、クライアントの実装は、web インターフェイスへのアクセスに使用する URL を構築できます。</span><span class="sxs-lookup"><span data-stu-id="5a793-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="5a793-121">クライアントの実装では、URL に web ブラウザーを開き、任意の不正使用を必要なレポートを作成するようにユーザーにこの構築された URL (またはリンクのクリック可能な) を表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a793-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="5a793-122">不適切な発言の報告書フォームの実装は、サーバーの実装によって決定されます。</span><span class="sxs-lookup"><span data-stu-id="5a793-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="5a793-123">値、`@id`は次のプレース ホルダーのトークンのいずれかを含む URL 文字列です。</span><span class="sxs-lookup"><span data-stu-id="5a793-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="5a793-124">URL のプレース ホルダー</span><span class="sxs-lookup"><span data-stu-id="5a793-124">URL placeholders</span></span>

<span data-ttu-id="5a793-125">名前</span><span class="sxs-lookup"><span data-stu-id="5a793-125">Name</span></span>        | <span data-ttu-id="5a793-126">種類</span><span class="sxs-lookup"><span data-stu-id="5a793-126">Type</span></span>    | <span data-ttu-id="5a793-127">必須</span><span class="sxs-lookup"><span data-stu-id="5a793-127">Required</span></span> | <span data-ttu-id="5a793-128">メモ</span><span class="sxs-lookup"><span data-stu-id="5a793-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="5a793-129">string</span><span class="sxs-lookup"><span data-stu-id="5a793-129">string</span></span>  | <span data-ttu-id="5a793-130">Ｘ</span><span class="sxs-lookup"><span data-stu-id="5a793-130">no</span></span>       | <span data-ttu-id="5a793-131">不正使用を報告するパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="5a793-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="5a793-132">string</span><span class="sxs-lookup"><span data-stu-id="5a793-132">string</span></span>  | <span data-ttu-id="5a793-133">Ｘ</span><span class="sxs-lookup"><span data-stu-id="5a793-133">no</span></span>       | <span data-ttu-id="5a793-134">パッケージのバージョンの不正使用を報告する</span><span class="sxs-lookup"><span data-stu-id="5a793-134">The package version to report abuse for</span></span>

<span data-ttu-id="5a793-135">`{id}`と`{version}`サーバーの実装によって解釈される値は、大文字と小文字を区別しないと、バージョンを正規化するかどうかに左右されないをする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5a793-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="5a793-136">たとえば、nuget.org のレポートの不正使用のテンプレートは、ようになります。</span><span class="sxs-lookup"><span data-stu-id="5a793-136">For example, nuget.org's report abuse template looks like this:</span></span>

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

<span data-ttu-id="5a793-137">クライアント実装 NuGet.Versioning 4.3.0 のレポートの不正使用をフォームにリンクを表示する場合は、次の URL を生成し、ユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="5a793-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
