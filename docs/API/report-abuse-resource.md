---
title: "レポート不正使用を URL テンプレート、NuGet API |Microsoft ドキュメント"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 148d743a-09e5-4539-8454-675be11902db
description: "レポートの不正使用を URL テンプレートは、その UI に、不正使用のリンクを表示するクライアントを使用できます。"
keywords: "NuGet API 不正使用を報告、NuGet API ファイル準拠している、NuGet.org レポート URL テンプレート"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7b3413297f5a7fcf0e2c7757036b1f240ed0058a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="report-abuse-url-template"></a><span data-ttu-id="49c39-104">レポートの不正使用を URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="49c39-104">Report Abuse URL Template</span></span>

<span data-ttu-id="49c39-105">クライアント ユーザーが特定のパッケージの不正使用を報告に使用できる URL を作成することができます。</span><span class="sxs-lookup"><span data-stu-id="49c39-105">It is possible for a client to build a URL that can be used by the user to report abuse about a specific package.</span></span> <span data-ttu-id="49c39-106">これは、機能は、パッケージ ソースがパッケージ ソースへのレポートの不正使用を委任するすべてのクライアント エクスペリエンス (でもサード パーティ) を有効にするときに便利です。</span><span class="sxs-lookup"><span data-stu-id="49c39-106">This is useful when a package source wants to enable all client experiences (even 3rd party) to delegate abuse reports to the package source.</span></span>

<span data-ttu-id="49c39-107">パッケージの内容をフェッチするために使用されるリソースは、`ReportAbuseUriTemplate`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="49c39-107">The resource used for fetching package content is the `ReportAbuseUriTemplate` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="49c39-108">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="49c39-108">Versioning</span></span>

<span data-ttu-id="49c39-109">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="49c39-109">The following `@type` values are used:</span></span>

<span data-ttu-id="49c39-110">@type の値</span><span class="sxs-lookup"><span data-stu-id="49c39-110">@type value</span></span>                       | <span data-ttu-id="49c39-111">メモ</span><span class="sxs-lookup"><span data-stu-id="49c39-111">Notes</span></span>
--------------------------------- | -----
<span data-ttu-id="49c39-112">ReportAbuseUriTemplate/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="49c39-112">ReportAbuseUriTemplate/3.0.0-beta</span></span> | <span data-ttu-id="49c39-113">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="49c39-113">The initial release</span></span>
<span data-ttu-id="49c39-114">ReportAbuseUriTemplate/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="49c39-114">ReportAbuseUriTemplate/3.0.0-rc</span></span>   | <span data-ttu-id="49c39-115">エイリアス`ReportAbuseUriTemplate/3.0.0-beta`</span><span class="sxs-lookup"><span data-stu-id="49c39-115">Alias of `ReportAbuseUriTemplate/3.0.0-beta`</span></span>

## <a name="url-template"></a><span data-ttu-id="49c39-116">URL テンプレート</span><span class="sxs-lookup"><span data-stu-id="49c39-116">URL template</span></span>

<span data-ttu-id="49c39-117">次の API の URL がの値、`@id`前述のリソースのいずれかに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="49c39-117">The URL for the following API is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span>

## <a name="http-methods"></a><span data-ttu-id="49c39-118">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="49c39-118">HTTP methods</span></span>

<span data-ttu-id="49c39-119">Web ページをサポートする必要があります、クライアントは、ユーザーの代理として、レポートの不正使用を URL に要求をするものではありません、ただし、`GET`を簡単に web ブラウザーで開くクリックされた url を入力できるようにするメソッド。</span><span class="sxs-lookup"><span data-stu-id="49c39-119">Although the client is not intended to make requests to the report abuse URL on behalf of the user, the web page should support the `GET` method to allow a clicked URL to be easily opened in a web browser.</span></span>

## <a name="construct-the-url"></a><span data-ttu-id="49c39-120">URL を構築します。</span><span class="sxs-lookup"><span data-stu-id="49c39-120">Construct the URL</span></span>

<span data-ttu-id="49c39-121">クライアントの実装は、既知のパッケージ ID とバージョンを指定するには、web インターフェイスへのアクセスに使用する URL を構築できます。</span><span class="sxs-lookup"><span data-stu-id="49c39-121">Given a known package ID and version, the client implementation can construct a URL used to access a web interface.</span></span> <span data-ttu-id="49c39-122">クライアント実装では、URL に web ブラウザーを開き、任意の不正使用を必要なレポートを作成するようにユーザーにこの構築された URL (またはクリック可能なリンク) を表示します。</span><span class="sxs-lookup"><span data-stu-id="49c39-122">The client implementation should display this constructed URL (or clickable link) to the user allowing them to open a web browser to the URL and make any necessary abuse report.</span></span> <span data-ttu-id="49c39-123">不正使用を報告書フォームの実装は、サーバーの実装によって決定されます。</span><span class="sxs-lookup"><span data-stu-id="49c39-123">The implementation of the abuse report form is determined by the server implementation.</span></span>

<span data-ttu-id="49c39-124">値、`@id`は、次のプレース ホルダーのトークンのいずれかを含む URL 文字列。</span><span class="sxs-lookup"><span data-stu-id="49c39-124">The value of the `@id` is a URL string containing any of the following placeholder tokens:</span></span>

### <a name="url-placeholders"></a><span data-ttu-id="49c39-125">URL のプレース ホルダー</span><span class="sxs-lookup"><span data-stu-id="49c39-125">URL placeholders</span></span>

<span data-ttu-id="49c39-126">名前</span><span class="sxs-lookup"><span data-stu-id="49c39-126">Name</span></span>        | <span data-ttu-id="49c39-127">種類</span><span class="sxs-lookup"><span data-stu-id="49c39-127">Type</span></span>    | <span data-ttu-id="49c39-128">必須</span><span class="sxs-lookup"><span data-stu-id="49c39-128">Required</span></span> | <span data-ttu-id="49c39-129">メモ</span><span class="sxs-lookup"><span data-stu-id="49c39-129">Notes</span></span>
----------- | ------- | -------- | -----
`{id}`      | <span data-ttu-id="49c39-130">string</span><span class="sxs-lookup"><span data-stu-id="49c39-130">string</span></span>  | <span data-ttu-id="49c39-131">Ｘ</span><span class="sxs-lookup"><span data-stu-id="49c39-131">no</span></span>       | <span data-ttu-id="49c39-132">不正使用を報告するパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="49c39-132">The package ID to report abuse for</span></span>
`{version}` | <span data-ttu-id="49c39-133">string</span><span class="sxs-lookup"><span data-stu-id="49c39-133">string</span></span>  | <span data-ttu-id="49c39-134">Ｘ</span><span class="sxs-lookup"><span data-stu-id="49c39-134">no</span></span>       | <span data-ttu-id="49c39-135">パッケージのバージョンの不正使用を報告する</span><span class="sxs-lookup"><span data-stu-id="49c39-135">The package version to report abuse for</span></span>

<span data-ttu-id="49c39-136">`{id}`と`{version}`サーバー実装により解釈される値がケース insenstive をする必要があります、バージョンを正規化するかどうかに左右されないとします。</span><span class="sxs-lookup"><span data-stu-id="49c39-136">The `{id}` and `{version}` values interpreted by the server implementation must be case insenstive and not sensitive to whether the version is normalized.</span></span>

<span data-ttu-id="49c39-137">たとえば、nuget.org のレポートの不正使用のテンプレートは、これのようになります。</span><span class="sxs-lookup"><span data-stu-id="49c39-137">For example, nuget.org's report abuse template looks like this:</span></span>

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

<span data-ttu-id="49c39-138">クライアント実装では、レポートの不正使用をフォームに NuGet.Versioning 4.3.0 のリンクを表示する場合は、次の URL を生成は、ユーザーに提供します。</span><span class="sxs-lookup"><span data-stu-id="49c39-138">If the client implementation needs to display a link to the report abuse form for NuGet.Versioning 4.3.0, it would produce the following URL and provide it to the user:</span></span>

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```