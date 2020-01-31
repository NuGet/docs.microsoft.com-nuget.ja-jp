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
ms.openlocfilehash: 9e60c0236bd4e6f1374b50a236447faf80dddb38
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813196"
---
# <a name="rate-limits"></a><span data-ttu-id="2d46b-103">速度の制限</span><span class="sxs-lookup"><span data-stu-id="2d46b-103">Rate Limits</span></span>

<span data-ttu-id="2d46b-104">NuGet.org API は、誤用を防ぐためにレート制限を適用します。</span><span class="sxs-lookup"><span data-stu-id="2d46b-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="2d46b-105">転送率の制限を超える要求では、次のエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="2d46b-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="2d46b-106">レート制限を使用した要求の調整に加えて、一部の Api もクォータを適用します。</span><span class="sxs-lookup"><span data-stu-id="2d46b-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="2d46b-107">クォータを超える要求では、次のエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="2d46b-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="2d46b-108">次の表は、NuGet.org API のレート制限を示しています。</span><span class="sxs-lookup"><span data-stu-id="2d46b-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="2d46b-109">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="2d46b-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="2d46b-110">現在、レートが制限されていないため、NuGet の[V3 検索 api](search-query-service-resource.md)を使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2d46b-110">We recommend using NuGet.org's [V3 search APIs](search-query-service-resource.md) as it is not rate limited currently.</span></span> <span data-ttu-id="2d46b-111">V1 と V2 の検索 Api では、次の制限が適用されます。</span><span class="sxs-lookup"><span data-stu-id="2d46b-111">For V1 and V2 search APIs, the following limits apply:</span></span>

| <span data-ttu-id="2d46b-112">API</span><span class="sxs-lookup"><span data-stu-id="2d46b-112">API</span></span> | <span data-ttu-id="2d46b-113">制限の種類</span><span class="sxs-lookup"><span data-stu-id="2d46b-113">Limit Type</span></span> | <span data-ttu-id="2d46b-114">制限値</span><span class="sxs-lookup"><span data-stu-id="2d46b-114">Limit Value</span></span> | <span data-ttu-id="2d46b-115">API ユースケース</span><span class="sxs-lookup"><span data-stu-id="2d46b-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="2d46b-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="2d46b-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="2d46b-117">IP</span><span class="sxs-lookup"><span data-stu-id="2d46b-117">IP</span></span> | <span data-ttu-id="2d46b-118">1000/分</span><span class="sxs-lookup"><span data-stu-id="2d46b-118">1000 / minute</span></span> | <span data-ttu-id="2d46b-119">V1 OData `Packages` コレクションを使用した NuGet パッケージメタデータのクエリ</span><span class="sxs-lookup"><span data-stu-id="2d46b-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="2d46b-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="2d46b-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="2d46b-121">IP</span><span class="sxs-lookup"><span data-stu-id="2d46b-121">IP</span></span> | <span data-ttu-id="2d46b-122">3000/分</span><span class="sxs-lookup"><span data-stu-id="2d46b-122">3000 / minute</span></span> | <span data-ttu-id="2d46b-123">V1 検索エンドポイント経由で NuGet パッケージを検索する</span><span class="sxs-lookup"><span data-stu-id="2d46b-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="2d46b-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="2d46b-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="2d46b-125">IP</span><span class="sxs-lookup"><span data-stu-id="2d46b-125">IP</span></span> | <span data-ttu-id="2d46b-126">2万/分</span><span class="sxs-lookup"><span data-stu-id="2d46b-126">20000 / minute</span></span> | <span data-ttu-id="2d46b-127">V2 OData `Packages` コレクションを使用した NuGet パッケージメタデータのクエリ</span><span class="sxs-lookup"><span data-stu-id="2d46b-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="2d46b-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="2d46b-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="2d46b-129">IP</span><span class="sxs-lookup"><span data-stu-id="2d46b-129">IP</span></span> | <span data-ttu-id="2d46b-130">100/分</span><span class="sxs-lookup"><span data-stu-id="2d46b-130">100 / minute</span></span> | <span data-ttu-id="2d46b-131">V2 OData `Packages` コレクションを使用した NuGet パッケージ数の照会</span><span class="sxs-lookup"><span data-stu-id="2d46b-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="2d46b-132">Package Push and 一覧から削除</span><span class="sxs-lookup"><span data-stu-id="2d46b-132">Package Push and Unlist</span></span>

| <span data-ttu-id="2d46b-133">API</span><span class="sxs-lookup"><span data-stu-id="2d46b-133">API</span></span> | <span data-ttu-id="2d46b-134">制限の種類</span><span class="sxs-lookup"><span data-stu-id="2d46b-134">Limit Type</span></span> | <span data-ttu-id="2d46b-135">制限値</span><span class="sxs-lookup"><span data-stu-id="2d46b-135">Limit Value</span></span> | <span data-ttu-id="2d46b-136">API ユースケース</span><span class="sxs-lookup"><span data-stu-id="2d46b-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="2d46b-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="2d46b-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="2d46b-138">API キー</span><span class="sxs-lookup"><span data-stu-id="2d46b-138">API Key</span></span> | <span data-ttu-id="2d46b-139">350/時間</span><span class="sxs-lookup"><span data-stu-id="2d46b-139">350 / hour</span></span> | <span data-ttu-id="2d46b-140">V2 プッシュエンドポイント経由で新しい NuGet パッケージ (バージョン) をアップロードする</span><span class="sxs-lookup"><span data-stu-id="2d46b-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="2d46b-141">`/api/v2/package/{id}/{version}` の**削除**</span><span class="sxs-lookup"><span data-stu-id="2d46b-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="2d46b-142">API キー</span><span class="sxs-lookup"><span data-stu-id="2d46b-142">API Key</span></span> | <span data-ttu-id="2d46b-143">250/時間</span><span class="sxs-lookup"><span data-stu-id="2d46b-143">250 / hour</span></span> | <span data-ttu-id="2d46b-144">V2 エンドポイントを使用した NuGet パッケージ (バージョン) の一覧から削除</span><span class="sxs-lookup"><span data-stu-id="2d46b-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
