---
title: 不正行為の URL テンプレート、NuGet API
description: レポートの不正使用 URL テンプレートを使用すると、クライアントは UI に不正使用のリンクを表示できます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775228"
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="c1cd8-103">不正を報告する URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="c1cd8-103">Report abuse URL template</span></span>

<span data-ttu-id="c1cd8-104">クライアントは、特定のパッケージに関する誤用を報告するためにユーザーが使用できる URL を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-104">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="c1cd8-105">これは、パッケージソースがすべてのクライアントエクスペリエンス (サードパーティでも) を有効にして、不正使用レポートをパッケージソースに委任する場合に便利です。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-105">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="c1cd8-106">この URL の作成に使用されるリソースは、 `ReportAbuseUriTemplate` [サービスインデックス](service-index.md)で検出されたリソースです。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-106">The resource used for building this URL is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="c1cd8-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="c1cd8-107">Versioning</span></span>

<span data-ttu-id="c1cd8-108">次の `@type` 値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-108">The following `@type` values are used:</span></span>

<span data-ttu-id="c1cd8-109">@type 値</span><span class="sxs-lookup"><span data-stu-id="c1cd8-109">@type value</span></span>                       | <span data-ttu-id="c1cd8-110">Notes</span><span class="sxs-lookup"><span data-stu-id="c1cd8-110">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="c1cd8-111">ReportAbuseUriTemplate/3.0.0-ベータ</span><span class="sxs-lookup"><span data-stu-id="c1cd8-111">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="c1cd8-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="c1cd8-112">The initial release</span></span>
<span data-ttu-id="c1cd8-113">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="c1cd8-113">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="c1cd8-114">エイリアス `ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="c1cd8-114">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="c1cd8-115">URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="c1cd8-115">URL template</span></span>

<span data-ttu-id="c1cd8-116">次の API の URL は、 `@id` 前述のいずれかのリソース値に関連付けられているプロパティの値です `@type` 。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-116">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c1cd8-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="c1cd8-117">HTTP methods</span></span>

<span data-ttu-id="c1cd8-118">クライアントは、ユーザーの代わりにレポートの不正使用の URL に要求を送信することを意図していませんが、web ページでは、クリックした `GET` url を web ブラウザーで簡単に開くことができるように、メソッドをサポートする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-118">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="c1cd8-119">URL を作成する</span><span class="sxs-lookup"><span data-stu-id="c1cd8-119">Construct the URL</span></span>

<span data-ttu-id="c1cd8-120">既知のパッケージ ID とバージョンを指定すると、クライアント実装は、web インターフェイスにアクセスするために使用する URL を作成できます。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-120">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="c1cd8-121">クライアントの実装では、この構築された URL (またはクリック可能なリンク) をユーザーに表示して、ユーザーが URL に対して web ブラウザーを開いて、必要な不正使用レポートを作成できるようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-121">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="c1cd8-122">誤用レポートフォームの実装は、サーバーの実装によって決まります。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-122">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="c1cd8-123">の値は、 `@id` 次のプレースホルダートークンのいずれかを含む URL 文字列です。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-123">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="c1cd8-124">URL プレースホルダー</span><span class="sxs-lookup"><span data-stu-id="c1cd8-124">URL placeholders</span></span>

<span data-ttu-id="c1cd8-125">名前</span><span class="sxs-lookup"><span data-stu-id="c1cd8-125">Name</span></span>        | <span data-ttu-id="c1cd8-126">Type</span><span class="sxs-lookup"><span data-stu-id="c1cd8-126">Type</span></span>    | <span data-ttu-id="c1cd8-127">必須</span><span class="sxs-lookup"><span data-stu-id="c1cd8-127">Required</span></span> | <span data-ttu-id="c1cd8-128">Notes</span><span class="sxs-lookup"><span data-stu-id="c1cd8-128">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="c1cd8-129">string</span><span class="sxs-lookup"><span data-stu-id="c1cd8-129">string</span></span>  | <span data-ttu-id="c1cd8-130">no</span><span class="sxs-lookup"><span data-stu-id="c1cd8-130">no</span></span>       | <span data-ttu-id="c1cd8-131">不正使用を報告するパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="c1cd8-131">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="c1cd8-132">string</span><span class="sxs-lookup"><span data-stu-id="c1cd8-132">string</span></span>  | <span data-ttu-id="c1cd8-133">no</span><span class="sxs-lookup"><span data-stu-id="c1cd8-133">no</span></span>       | <span data-ttu-id="c1cd8-134">不正使用を報告するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="c1cd8-134">The package version to report abuse for</span></span>

<span data-ttu-id="c1cd8-135">`{id}`サーバーの `{version}` 実装で解釈されるおよび値は、バージョンが正規化されているかどうかにかかわらず、大文字と小文字が区別されないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-135">The `{id}` and `{version}` values interpreted by the server implementation must be case insensitive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="c1cd8-136">たとえば、nuget.exe のレポートの不正使用テンプレートは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-136">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="c1cd8-137">クライアントの実装で、NuGet のレポート不正使用フォームへのリンクを表示する必要がある場合、バージョン4.3.0 では次の URL が生成され、ユーザーに提供されます。</span><span class="sxs-lookup"><span data-stu-id="c1cd8-137">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
