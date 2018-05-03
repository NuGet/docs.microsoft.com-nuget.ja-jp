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
ms.openlocfilehash: 3aaebef8fff670759c6484a5a8f90a2f4dd58c66
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="rate-limits"></a><span data-ttu-id="cb828-103">速度の制限</span><span class="sxs-lookup"><span data-stu-id="cb828-103">Rate Limits</span></span>

<span data-ttu-id="cb828-104">NuGet.org API は、不正使用を防ぐためのレート制限を強制します。</span><span class="sxs-lookup"><span data-stu-id="cb828-104">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="cb828-105">レート制限を超える要求は、次のエラーを返します。</span><span class="sxs-lookup"><span data-stu-id="cb828-105">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="cb828-106">次の表では、NuGet.org API の転送率の制限が一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="cb828-106">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="cb828-107">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="cb828-107">Package search</span></span>

> [!Note]
> <span data-ttu-id="cb828-108">NuGet.org の使用をお勧め[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)現在検索パフォーマンスの高いは、いずれかがないことを制限します。</span><span class="sxs-lookup"><span data-stu-id="cb828-108">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="cb828-109">V1 と V2 の検索 Api、followins 制限を適用します。</span><span class="sxs-lookup"><span data-stu-id="cb828-109">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="cb828-110">API</span><span class="sxs-lookup"><span data-stu-id="cb828-110">API</span></span> | <span data-ttu-id="cb828-111">制限の種類</span><span class="sxs-lookup"><span data-stu-id="cb828-111">Limit Type</span></span> | <span data-ttu-id="cb828-112">制限値</span><span class="sxs-lookup"><span data-stu-id="cb828-112">Limit Value</span></span> | <span data-ttu-id="cb828-113">API usecase</span><span class="sxs-lookup"><span data-stu-id="cb828-113">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="cb828-114">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="cb828-114">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="cb828-115">IP</span><span class="sxs-lookup"><span data-stu-id="cb828-115">IP</span></span> | <span data-ttu-id="cb828-116">1000/分</span><span class="sxs-lookup"><span data-stu-id="cb828-116">1000 / minute</span></span> | <span data-ttu-id="cb828-117">V1 の OData を使用して NuGet パッケージのメタデータを照会する`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="cb828-117">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="cb828-118">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="cb828-118">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="cb828-119">IP</span><span class="sxs-lookup"><span data-stu-id="cb828-119">IP</span></span> | <span data-ttu-id="cb828-120">3000/分</span><span class="sxs-lookup"><span data-stu-id="cb828-120">3000 / minute</span></span> | <span data-ttu-id="cb828-121">V1 検索 endpoint を使用して NuGet パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="cb828-121">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="cb828-122">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="cb828-122">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="cb828-123">IP</span><span class="sxs-lookup"><span data-stu-id="cb828-123">IP</span></span> | <span data-ttu-id="cb828-124">20000/分</span><span class="sxs-lookup"><span data-stu-id="cb828-124">20000 / minute</span></span> | <span data-ttu-id="cb828-125">V2 の OData を使用して NuGet パッケージのメタデータを照会する`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="cb828-125">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="cb828-126">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="cb828-126">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="cb828-127">IP</span><span class="sxs-lookup"><span data-stu-id="cb828-127">IP</span></span> | <span data-ttu-id="cb828-128">100/分</span><span class="sxs-lookup"><span data-stu-id="cb828-128">100 / minute</span></span> | <span data-ttu-id="cb828-129">V2 の OData を使用して NuGet パッケージの数を照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="cb828-129">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="cb828-130">パッケージ プッシュ モードと非公開</span><span class="sxs-lookup"><span data-stu-id="cb828-130">Package Push and Unlist</span></span>

| <span data-ttu-id="cb828-131">API</span><span class="sxs-lookup"><span data-stu-id="cb828-131">API</span></span> | <span data-ttu-id="cb828-132">制限の種類</span><span class="sxs-lookup"><span data-stu-id="cb828-132">Limit Type</span></span> | <span data-ttu-id="cb828-133">制限値</span><span class="sxs-lookup"><span data-stu-id="cb828-133">Limit Value</span></span> | <span data-ttu-id="cb828-134">APU usecase</span><span class="sxs-lookup"><span data-stu-id="cb828-134">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="cb828-135">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="cb828-135">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="cb828-136">API キー</span><span class="sxs-lookup"><span data-stu-id="cb828-136">API Key</span></span> | <span data-ttu-id="cb828-137">100/分</span><span class="sxs-lookup"><span data-stu-id="cb828-137">100 / minute</span></span> | <span data-ttu-id="cb828-138">V2 プッシュ endpoint を使用して新しい NuGet パッケージ (バージョン) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="cb828-138">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="cb828-139">**削除** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="cb828-139">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="cb828-140">API キー</span><span class="sxs-lookup"><span data-stu-id="cb828-140">API Key</span></span> | <span data-ttu-id="cb828-141">100/分</span><span class="sxs-lookup"><span data-stu-id="cb828-141">100 / minute</span></span> | <span data-ttu-id="cb828-142">非公開 v2 endpoint を使用して NuGet パッケージ (バージョン)</span><span class="sxs-lookup"><span data-stu-id="cb828-142">Unlist a NuGet package (version) via v2 endpoint</span></span> 
