---
title: レート制限、NuGet API
description: NuGet Api で、不正使用を防ぐために転送率の制限が適用されたされます。
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548678"
---
# <a name="rate-limits"></a><span data-ttu-id="2c688-103">速度の制限</span><span class="sxs-lookup"><span data-stu-id="2c688-103">Rate Limits</span></span>

<span data-ttu-id="2c688-104">NuGet.org の API は、不正使用を防ぐレートの制限を適用します。</span><span class="sxs-lookup"><span data-stu-id="2c688-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="2c688-105">レート制限を超える要求には、次のエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="2c688-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="2c688-106">要求の調整も、レート制限、一部の Api を使用するだけでなく、クォータを適用します。</span><span class="sxs-lookup"><span data-stu-id="2c688-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="2c688-107">クォータを超える要求には、次のエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="2c688-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="2c688-108">次の表では、NuGet.org の API のレート制限を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="2c688-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="2c688-109">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="2c688-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="2c688-110">NuGet.org の使用をお勧め[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)現在はパフォーマンスの高いを持たない検索の制限します。</span><span class="sxs-lookup"><span data-stu-id="2c688-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="2c688-111">V1 と V2 の search Api、followins 制限が適用されます。</span><span class="sxs-lookup"><span data-stu-id="2c688-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="2c688-112">API</span><span class="sxs-lookup"><span data-stu-id="2c688-112">API</span></span> | <span data-ttu-id="2c688-113">制限の種類</span><span class="sxs-lookup"><span data-stu-id="2c688-113">Limit Type</span></span> | <span data-ttu-id="2c688-114">制限値</span><span class="sxs-lookup"><span data-stu-id="2c688-114">Limit Value</span></span> | <span data-ttu-id="2c688-115">API のユースケース</span><span class="sxs-lookup"><span data-stu-id="2c688-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="2c688-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="2c688-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="2c688-117">IP</span><span class="sxs-lookup"><span data-stu-id="2c688-117">IP</span></span> | <span data-ttu-id="2c688-118">1000/分</span><span class="sxs-lookup"><span data-stu-id="2c688-118">1000 / minute</span></span> | <span data-ttu-id="2c688-119">V1 の OData を使用して NuGet パッケージのメタデータを照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="2c688-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="2c688-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="2c688-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="2c688-121">IP</span><span class="sxs-lookup"><span data-stu-id="2c688-121">IP</span></span> | <span data-ttu-id="2c688-122">3000/分</span><span class="sxs-lookup"><span data-stu-id="2c688-122">3000 / minute</span></span> | <span data-ttu-id="2c688-123">V1 Search エンドポイント経由での NuGet パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="2c688-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="2c688-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="2c688-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="2c688-125">IP</span><span class="sxs-lookup"><span data-stu-id="2c688-125">IP</span></span> | <span data-ttu-id="2c688-126">20000/分</span><span class="sxs-lookup"><span data-stu-id="2c688-126">20000 / minute</span></span> | <span data-ttu-id="2c688-127">V2 の OData を使用して NuGet パッケージのメタデータを照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="2c688-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="2c688-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="2c688-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="2c688-129">IP</span><span class="sxs-lookup"><span data-stu-id="2c688-129">IP</span></span> | <span data-ttu-id="2c688-130">100/分</span><span class="sxs-lookup"><span data-stu-id="2c688-130">100 / minute</span></span> | <span data-ttu-id="2c688-131">V2 の OData を使用して NuGet パッケージの数を照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="2c688-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="2c688-132">パッケージをプッシュし、一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="2c688-132">Package Push and Unlist</span></span>

| <span data-ttu-id="2c688-133">API</span><span class="sxs-lookup"><span data-stu-id="2c688-133">API</span></span> | <span data-ttu-id="2c688-134">制限の種類</span><span class="sxs-lookup"><span data-stu-id="2c688-134">Limit Type</span></span> | <span data-ttu-id="2c688-135">制限値</span><span class="sxs-lookup"><span data-stu-id="2c688-135">Limit Value</span></span> | <span data-ttu-id="2c688-136">API のユースケース</span><span class="sxs-lookup"><span data-stu-id="2c688-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="2c688-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="2c688-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="2c688-138">API キー</span><span class="sxs-lookup"><span data-stu-id="2c688-138">API Key</span></span> | <span data-ttu-id="2c688-139">250/時間</span><span class="sxs-lookup"><span data-stu-id="2c688-139">250 / hour</span></span> | <span data-ttu-id="2c688-140">V2 プッシュ エンドポイントを経由して、新しい NuGet パッケージ (バージョン) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="2c688-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="2c688-141">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="2c688-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="2c688-142">API キー</span><span class="sxs-lookup"><span data-stu-id="2c688-142">API Key</span></span> | <span data-ttu-id="2c688-143">250/時間</span><span class="sxs-lookup"><span data-stu-id="2c688-143">250 / hour</span></span> | <span data-ttu-id="2c688-144">V2 エンドポイントを使用して NuGet パッケージ (バージョン) を一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="2c688-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
