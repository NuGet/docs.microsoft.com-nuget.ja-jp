---
title: 転送率の制限を NuGet API
description: NuGet Api によって、不正使用を防ぐために転送率の制限が適用されたされます。
author: cmanu
ms.author: cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: c5d3cf68ac6a96a6c14eb5e652bcf72698b6a8e8
ms.sourcegitcommit: 8f0bb8bb9cb91d27d660963ed9b0f32642f420fe
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/17/2018
---
# <a name="rate-limits"></a><span data-ttu-id="b2932-103">速度の制限</span><span class="sxs-lookup"><span data-stu-id="b2932-103">Rate Limits</span></span>

<span data-ttu-id="b2932-104">NuGet.org API は、不正使用を防ぐためのレート制限を強制します。</span><span class="sxs-lookup"><span data-stu-id="b2932-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="b2932-105">レート制限を超える要求は、次のエラーを返します。</span><span class="sxs-lookup"><span data-stu-id="b2932-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="b2932-106">次の表では、NuGet.org API の転送率の制限が一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b2932-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="b2932-107">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="b2932-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="b2932-108">NuGet.org の使用をお勧め[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)現在検索パフォーマンスの高いは、いずれかがないことを制限します。</span><span class="sxs-lookup"><span data-stu-id="b2932-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="b2932-109">V1 と V2 の検索 Api、followins 制限を適用します。</span><span class="sxs-lookup"><span data-stu-id="b2932-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="b2932-110">API</span><span class="sxs-lookup"><span data-stu-id="b2932-110">API</span></span> | <span data-ttu-id="b2932-111">制限の種類</span><span class="sxs-lookup"><span data-stu-id="b2932-111">Limit Type</span></span> | <span data-ttu-id="b2932-112">制限値</span><span class="sxs-lookup"><span data-stu-id="b2932-112">Limit Value</span></span> | <span data-ttu-id="b2932-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="b2932-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="b2932-114">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="b2932-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="b2932-115">IP</span><span class="sxs-lookup"><span data-stu-id="b2932-115">IP</span></span> | <span data-ttu-id="b2932-116">1000/分</span><span class="sxs-lookup"><span data-stu-id="b2932-116">1000 / minute</span></span> | <span data-ttu-id="b2932-117">V1 の OData を使用して NuGet パッケージのメタデータを照会する`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="b2932-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="b2932-118">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="b2932-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="b2932-119">IP</span><span class="sxs-lookup"><span data-stu-id="b2932-119">IP</span></span> | <span data-ttu-id="b2932-120">3000/分</span><span class="sxs-lookup"><span data-stu-id="b2932-120">3000 / minute</span></span> | <span data-ttu-id="b2932-121">V1 検索 endpoint を使用して NuGet パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="b2932-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="b2932-122">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="b2932-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="b2932-123">IP</span><span class="sxs-lookup"><span data-stu-id="b2932-123">IP</span></span> | <span data-ttu-id="b2932-124">20000/分</span><span class="sxs-lookup"><span data-stu-id="b2932-124">20000 / minute</span></span> | <span data-ttu-id="b2932-125">V2 の OData を使用して NuGet パッケージのメタデータを照会する`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="b2932-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="b2932-126">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="b2932-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="b2932-127">IP</span><span class="sxs-lookup"><span data-stu-id="b2932-127">IP</span></span> | <span data-ttu-id="b2932-128">100/分</span><span class="sxs-lookup"><span data-stu-id="b2932-128">100 / minute</span></span> | <span data-ttu-id="b2932-129">V2 の OData を使用して NuGet パッケージの数を照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="b2932-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="b2932-130">パッケージ プッシュ モードと非公開</span><span class="sxs-lookup"><span data-stu-id="b2932-130">Package Push and Unlist</span></span>

| <span data-ttu-id="b2932-131">API</span><span class="sxs-lookup"><span data-stu-id="b2932-131">API</span></span> | <span data-ttu-id="b2932-132">制限の種類</span><span class="sxs-lookup"><span data-stu-id="b2932-132">Limit Type</span></span> | <span data-ttu-id="b2932-133">制限値</span><span class="sxs-lookup"><span data-stu-id="b2932-133">Limit Value</span></span> | <span data-ttu-id="b2932-134">API usecase</span><span class="sxs-lookup"><span data-stu-id="b2932-134">API usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="b2932-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="b2932-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="b2932-136">API キー</span><span class="sxs-lookup"><span data-stu-id="b2932-136">API Key</span></span> | <span data-ttu-id="b2932-137">250/時間</span><span class="sxs-lookup"><span data-stu-id="b2932-137">250 / hour</span></span> | <span data-ttu-id="b2932-138">V2 プッシュ endpoint を使用して新しい NuGet パッケージ (バージョン) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="b2932-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="b2932-139">**削除** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="b2932-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="b2932-140">API キー</span><span class="sxs-lookup"><span data-stu-id="b2932-140">API Key</span></span> | <span data-ttu-id="b2932-141">250/時間</span><span class="sxs-lookup"><span data-stu-id="b2932-141">250 / hour</span></span> | <span data-ttu-id="b2932-142">非公開 v2 endpoint を使用して NuGet パッケージ (バージョン)</span><span class="sxs-lookup"><span data-stu-id="b2932-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
