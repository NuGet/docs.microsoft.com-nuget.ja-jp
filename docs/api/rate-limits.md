---
title: レート制限、NuGet API
description: NuGet Api で、不正使用を防ぐために転送率の制限が適用されたされます。
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: a55eb49318b766028d1579a4d33618617bbd8801
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508128"
---
# <a name="rate-limits"></a><span data-ttu-id="75b82-103">速度の制限</span><span class="sxs-lookup"><span data-stu-id="75b82-103">Rate Limits</span></span>

<span data-ttu-id="75b82-104">NuGet.org の API は、不正使用を防ぐレートの制限を適用します。</span><span class="sxs-lookup"><span data-stu-id="75b82-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="75b82-105">レート制限を超える要求には、次のエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="75b82-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="75b82-106">要求の調整も、レート制限、一部の Api を使用するだけでなく、クォータを適用します。</span><span class="sxs-lookup"><span data-stu-id="75b82-106">In addition to request throttling using rate limits, some APIs also enforce quota.</span></span> <span data-ttu-id="75b82-107">クォータを超える要求には、次のエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="75b82-107">Requests that exceed the quota return the following error:</span></span>

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

<span data-ttu-id="75b82-108">次の表では、NuGet.org の API のレート制限を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="75b82-108">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="75b82-109">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="75b82-109">Package search</span></span>

> [!Note]
> <span data-ttu-id="75b82-110">NuGet.org の使用をお勧め[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)現在はパフォーマンスの高いを持たない検索の制限します。</span><span class="sxs-lookup"><span data-stu-id="75b82-110">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="75b82-111">V1 と V2 の search Api、followins 制限が適用されます。</span><span class="sxs-lookup"><span data-stu-id="75b82-111">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="75b82-112">API</span><span class="sxs-lookup"><span data-stu-id="75b82-112">API</span></span> | <span data-ttu-id="75b82-113">制限の種類</span><span class="sxs-lookup"><span data-stu-id="75b82-113">Limit Type</span></span> | <span data-ttu-id="75b82-114">制限値</span><span class="sxs-lookup"><span data-stu-id="75b82-114">Limit Value</span></span> | <span data-ttu-id="75b82-115">API のユースケース</span><span class="sxs-lookup"><span data-stu-id="75b82-115">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="75b82-116">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="75b82-116">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="75b82-117">IP</span><span class="sxs-lookup"><span data-stu-id="75b82-117">IP</span></span> | <span data-ttu-id="75b82-118">1000/分</span><span class="sxs-lookup"><span data-stu-id="75b82-118">1000 / minute</span></span> | <span data-ttu-id="75b82-119">V1 の OData を使用して NuGet パッケージのメタデータを照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="75b82-119">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="75b82-120">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="75b82-120">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="75b82-121">IP</span><span class="sxs-lookup"><span data-stu-id="75b82-121">IP</span></span> | <span data-ttu-id="75b82-122">3000/分</span><span class="sxs-lookup"><span data-stu-id="75b82-122">3000 / minute</span></span> | <span data-ttu-id="75b82-123">V1 Search エンドポイント経由での NuGet パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="75b82-123">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="75b82-124">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="75b82-124">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="75b82-125">IP</span><span class="sxs-lookup"><span data-stu-id="75b82-125">IP</span></span> | <span data-ttu-id="75b82-126">20000/分</span><span class="sxs-lookup"><span data-stu-id="75b82-126">20000 / minute</span></span> | <span data-ttu-id="75b82-127">V2 の OData を使用して NuGet パッケージのメタデータを照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="75b82-127">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="75b82-128">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="75b82-128">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="75b82-129">IP</span><span class="sxs-lookup"><span data-stu-id="75b82-129">IP</span></span> | <span data-ttu-id="75b82-130">100/分</span><span class="sxs-lookup"><span data-stu-id="75b82-130">100 / minute</span></span> | <span data-ttu-id="75b82-131">V2 の OData を使用して NuGet パッケージの数を照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="75b82-131">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="75b82-132">パッケージをプッシュし、一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="75b82-132">Package Push and Unlist</span></span>

| <span data-ttu-id="75b82-133">API</span><span class="sxs-lookup"><span data-stu-id="75b82-133">API</span></span> | <span data-ttu-id="75b82-134">制限の種類</span><span class="sxs-lookup"><span data-stu-id="75b82-134">Limit Type</span></span> | <span data-ttu-id="75b82-135">制限値</span><span class="sxs-lookup"><span data-stu-id="75b82-135">Limit Value</span></span> | <span data-ttu-id="75b82-136">API のユースケース</span><span class="sxs-lookup"><span data-stu-id="75b82-136">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="75b82-137">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="75b82-137">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="75b82-138">API キー</span><span class="sxs-lookup"><span data-stu-id="75b82-138">API Key</span></span> | <span data-ttu-id="75b82-139">250/時間</span><span class="sxs-lookup"><span data-stu-id="75b82-139">250 / hour</span></span> | <span data-ttu-id="75b82-140">V2 プッシュ エンドポイントを経由して、新しい NuGet パッケージ (バージョン) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="75b82-140">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="75b82-141">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="75b82-141">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="75b82-142">API キー</span><span class="sxs-lookup"><span data-stu-id="75b82-142">API Key</span></span> | <span data-ttu-id="75b82-143">250/時間</span><span class="sxs-lookup"><span data-stu-id="75b82-143">250 / hour</span></span> | <span data-ttu-id="75b82-144">V2 エンドポイントを使用して NuGet パッケージ (バージョン) を一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="75b82-144">Unlist a NuGet package (version) via v2 endpoint</span></span> 
