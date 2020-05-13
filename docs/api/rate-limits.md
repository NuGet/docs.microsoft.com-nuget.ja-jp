---
title: レート制限、NuGet API
description: NuGet Api では、誤用を防ぐためにレート制限が適用されます。
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367935"
---
# <a name="rate-limits"></a><span data-ttu-id="3c884-103">速度の制限</span><span class="sxs-lookup"><span data-stu-id="3c884-103">Rate Limits</span></span>

<span data-ttu-id="3c884-104">NuGet.org API は、誤用を防ぐためにレート制限を適用します。</span><span class="sxs-lookup"><span data-stu-id="3c884-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="3c884-105">転送率の制限を超える要求では、次のエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="3c884-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="3c884-106">レート制限を使用した要求の調整に加えて、一部の Api もクォータを適用します。</span><span class="sxs-lookup"><span data-stu-id="3c884-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="3c884-107">クォータを超える要求では、次のエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="3c884-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="3c884-108">次の表は、NuGet.org API のレート制限を示しています。</span><span class="sxs-lookup"><span data-stu-id="3c884-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="3c884-109">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="3c884-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="3c884-110">現在、レートが制限されていないため、NuGet の[V3 検索 api](search-query-service-resource.md)を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3c884-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="3c884-111">V1 と V2 の検索 Api では、次の制限が適用されます。</span><span class="sxs-lookup"><span data-stu-id="3c884-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="3c884-112">API</span><span class="sxs-lookup"><span data-stu-id="3c884-112">API</span></span> | <span data-ttu-id="3c884-113">制限の種類</span><span class="sxs-lookup"><span data-stu-id="3c884-113">Limit Type</span></span> | <span data-ttu-id="3c884-114">制限値</span><span class="sxs-lookup"><span data-stu-id="3c884-114">Limit Value</span></span> | <span data-ttu-id="3c884-115">API ユースケース</span><span class="sxs-lookup"><span data-stu-id="3c884-115">API Use Case</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="3c884-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="3c884-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="3c884-117">IP</span><span class="sxs-lookup"><span data-stu-id="3c884-117">IP</span></span> | <span data-ttu-id="3c884-118">1000/分</span><span class="sxs-lookup"><span data-stu-id="3c884-118">1000 / minute</span></span> | <span data-ttu-id="3c884-119">V1 OData コレクションを使用した NuGet パッケージメタデータのクエリ `Packages`</span><span class="sxs-lookup"><span data-stu-id="3c884-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="3c884-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="3c884-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="3c884-121">IP</span><span class="sxs-lookup"><span data-stu-id="3c884-121">IP</span></span> | <span data-ttu-id="3c884-122">3000/分</span><span class="sxs-lookup"><span data-stu-id="3c884-122">3000 / minute</span></span> | <span data-ttu-id="3c884-123">V1 検索エンドポイント経由で NuGet パッケージを検索する</span><span class="sxs-lookup"><span data-stu-id="3c884-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="3c884-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="3c884-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="3c884-125">IP</span><span class="sxs-lookup"><span data-stu-id="3c884-125">IP</span></span> | <span data-ttu-id="3c884-126">2万/分</span><span class="sxs-lookup"><span data-stu-id="3c884-126">20000 / minute</span></span> | <span data-ttu-id="3c884-127">V2 OData コレクションを使用した NuGet パッケージメタデータのクエリ `Packages`</span><span class="sxs-lookup"><span data-stu-id="3c884-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="3c884-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="3c884-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="3c884-129">IP</span><span class="sxs-lookup"><span data-stu-id="3c884-129">IP</span></span> | <span data-ttu-id="3c884-130">100/分</span><span class="sxs-lookup"><span data-stu-id="3c884-130">100 / minute</span></span> | <span data-ttu-id="3c884-131">V2 OData コレクションを使用した NuGet パッケージ数の照会 `Packages`</span><span class="sxs-lookup"><span data-stu-id="3c884-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="3c884-132">Package Push and 一覧から削除</span><span class="sxs-lookup"><span data-stu-id="3c884-132">Package Push and Unlist</span></span>

| <span data-ttu-id="3c884-133">API</span><span class="sxs-lookup"><span data-stu-id="3c884-133">API</span></span> | <span data-ttu-id="3c884-134">制限の種類</span><span class="sxs-lookup"><span data-stu-id="3c884-134">Limit Type</span></span> | <span data-ttu-id="3c884-135">制限値</span><span class="sxs-lookup"><span data-stu-id="3c884-135">Limit Value</span></span> | <span data-ttu-id="3c884-136">API ユースケース</span><span class="sxs-lookup"><span data-stu-id="3c884-136">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="3c884-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="3c884-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="3c884-138">API キー</span><span class="sxs-lookup"><span data-stu-id="3c884-138">API Key</span></span> | <span data-ttu-id="3c884-139">350/時間</span><span class="sxs-lookup"><span data-stu-id="3c884-139">350 / hour</span></span> | <span data-ttu-id="3c884-140">V2 プッシュエンドポイント経由で新しい NuGet パッケージ (バージョン) をアップロードする</span><span class="sxs-lookup"><span data-stu-id="3c884-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="3c884-141">**削除**`/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="3c884-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="3c884-142">API キー</span><span class="sxs-lookup"><span data-stu-id="3c884-142">API Key</span></span> | <span data-ttu-id="3c884-143">250/時間</span><span class="sxs-lookup"><span data-stu-id="3c884-143">250 / hour</span></span> | <span data-ttu-id="3c884-144">V2 エンドポイントを使用した NuGet パッケージ (バージョン) の一覧から削除</span><span class="sxs-lookup"><span data-stu-id="3c884-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 

## <a name="nugetorg-website-page-views"></a><span data-ttu-id="3c884-145">nuget.org web サイトのページビュー</span><span class="sxs-lookup"><span data-stu-id="3c884-145">nuget.org website page views</span></span>

<span data-ttu-id="3c884-146">プログラムによって nuget.org web ページにアクセスする場合は、ドキュメント化された[V3 api](overview.md)を調査することを検討してください。</span><span class="sxs-lookup"><span data-stu-id="3c884-146">If you are accessing the nuget.org web pages programmatically, consider investigating our documented [V3 APIs](overview.md).</span></span> <span data-ttu-id="3c884-147">これらのエンドポイントを使用すると、パッケージのメタデータとコンテンツに簡単にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="3c884-147">These endpoints allow for simpler access to package metadata and content.</span></span> <span data-ttu-id="3c884-148">V3 API は可用性が向上し、web ブラウザーとの対話用に設計された NuGet ギャラリー web ページにアクセスするよりもパフォーマンスが向上しています。</span><span class="sxs-lookup"><span data-stu-id="3c884-148">The V3 API has better availability and has higher performance than accessing the NuGet Gallery web pages, which are designed for web browser interaction.</span></span>

| <span data-ttu-id="3c884-149">API</span><span class="sxs-lookup"><span data-stu-id="3c884-149">API</span></span> | <span data-ttu-id="3c884-150">制限の種類</span><span class="sxs-lookup"><span data-stu-id="3c884-150">Limit Type</span></span> | <span data-ttu-id="3c884-151">制限値</span><span class="sxs-lookup"><span data-stu-id="3c884-151">Limit Value</span></span> | <span data-ttu-id="3c884-152">API ユースケース</span><span class="sxs-lookup"><span data-stu-id="3c884-152">API Use Case</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="3c884-153">**GET** `/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="3c884-153">**GET** `/package/{id}/{version}`</span></span> | <span data-ttu-id="3c884-154">IP</span><span class="sxs-lookup"><span data-stu-id="3c884-154">IP</span></span> | <span data-ttu-id="3c884-155">50/分</span><span class="sxs-lookup"><span data-stu-id="3c884-155">50 / minute</span></span> | <span data-ttu-id="3c884-156">[パッケージ (バージョン) の詳細] ページを表示します。</span><span class="sxs-lookup"><span data-stu-id="3c884-156">Display package (version) details page.</span></span> 
