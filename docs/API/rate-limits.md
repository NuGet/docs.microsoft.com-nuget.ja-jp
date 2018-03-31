---
title: 転送率の制限値 |Microsoft ドキュメント
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet Api によって、不正使用を防ぐために転送率の制限が適用されたされます。
keywords: NuGet API、率を制限します。
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a><span data-ttu-id="7861f-104">速度の制限</span><span class="sxs-lookup"><span data-stu-id="7861f-104">Rate Limits</span></span>

<span data-ttu-id="7861f-105">NuGet.org API は、不正使用を防ぐためのレート制限を強制します。</span><span class="sxs-lookup"><span data-stu-id="7861f-105">The NuGet.org API enforces rate limiting to prevent abuse.</span></span> <span data-ttu-id="7861f-106">レート制限を超える要求は、次のエラーを返します。</span><span class="sxs-lookup"><span data-stu-id="7861f-106">Requests that exceed the rate limit return the following error:</span></span> 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

<span data-ttu-id="7861f-107">次の表では、NuGet.org API の転送率の制限が一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="7861f-107">The following tables list the rate limits for the NuGet.org API.</span></span>

## <a name="package-search"></a><span data-ttu-id="7861f-108">パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="7861f-108">Package search</span></span>

> [!Note]
> <span data-ttu-id="7861f-109">NuGet.org の使用をお勧め[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)現在検索パフォーマンスの高いは、いずれかがないことを制限します。</span><span class="sxs-lookup"><span data-stu-id="7861f-109">We recommend using NuGet.org's [V3 APIs](https://docs.microsoft.com/nuget/api/search-query-service-resource) for search that are performant and do not have any limit currently.</span></span> <span data-ttu-id="7861f-110">V1 と V2 の検索 Api、followins 制限を適用します。</span><span class="sxs-lookup"><span data-stu-id="7861f-110">For V1 and V2 search APIs, the followins limits apply:</span></span>


| <span data-ttu-id="7861f-111">API</span><span class="sxs-lookup"><span data-stu-id="7861f-111">API</span></span> | <span data-ttu-id="7861f-112">制限の種類</span><span class="sxs-lookup"><span data-stu-id="7861f-112">Limit Type</span></span> | <span data-ttu-id="7861f-113">制限値</span><span class="sxs-lookup"><span data-stu-id="7861f-113">Limit Value</span></span> | <span data-ttu-id="7861f-114">API usecase</span><span class="sxs-lookup"><span data-stu-id="7861f-114">API usecase</span></span> |
|:---|:---|:---|:---|
<span data-ttu-id="7861f-115">**GET** `/api/v1/Packages`</span><span class="sxs-lookup"><span data-stu-id="7861f-115">**GET** `/api/v1/Packages`</span></span> | <span data-ttu-id="7861f-116">IP</span><span class="sxs-lookup"><span data-stu-id="7861f-116">IP</span></span> | <span data-ttu-id="7861f-117">1000/分</span><span class="sxs-lookup"><span data-stu-id="7861f-117">1000 / minute</span></span> | <span data-ttu-id="7861f-118">V1 の OData を使用して NuGet パッケージのメタデータを照会する`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="7861f-118">Query NuGet package metadata via v1 OData `Packages` collection</span></span> |
<span data-ttu-id="7861f-119">**GET** `/api/v1/Search()`</span><span class="sxs-lookup"><span data-stu-id="7861f-119">**GET** `/api/v1/Search()`</span></span> | <span data-ttu-id="7861f-120">IP</span><span class="sxs-lookup"><span data-stu-id="7861f-120">IP</span></span> | <span data-ttu-id="7861f-121">3000/分</span><span class="sxs-lookup"><span data-stu-id="7861f-121">3000 / minute</span></span> | <span data-ttu-id="7861f-122">V1 検索 endpoint を使用して NuGet パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="7861f-122">Search for NuGet packages via v1 Search endpoint</span></span> | 
<span data-ttu-id="7861f-123">**GET** `/api/v2/Packages`</span><span class="sxs-lookup"><span data-stu-id="7861f-123">**GET** `/api/v2/Packages`</span></span> | <span data-ttu-id="7861f-124">IP</span><span class="sxs-lookup"><span data-stu-id="7861f-124">IP</span></span> | <span data-ttu-id="7861f-125">20000/分</span><span class="sxs-lookup"><span data-stu-id="7861f-125">20000 / minute</span></span> | <span data-ttu-id="7861f-126">V2 の OData を使用して NuGet パッケージのメタデータを照会する`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="7861f-126">Query NuGet package metadata via v2 OData `Packages` collection</span></span> | 
<span data-ttu-id="7861f-127">**GET** `/api/v2/Packages/$count`</span><span class="sxs-lookup"><span data-stu-id="7861f-127">**GET** `/api/v2/Packages/$count`</span></span> | <span data-ttu-id="7861f-128">IP</span><span class="sxs-lookup"><span data-stu-id="7861f-128">IP</span></span> | <span data-ttu-id="7861f-129">100/分</span><span class="sxs-lookup"><span data-stu-id="7861f-129">100 / minute</span></span> | <span data-ttu-id="7861f-130">V2 の OData を使用して NuGet パッケージの数を照会`Packages`コレクション</span><span class="sxs-lookup"><span data-stu-id="7861f-130">Query NuGet package count via v2 OData `Packages` collection</span></span> | 

## <a name="package-push-and-unlist"></a><span data-ttu-id="7861f-131">パッケージ プッシュ モードと非公開</span><span class="sxs-lookup"><span data-stu-id="7861f-131">Package Push and Unlist</span></span>

| <span data-ttu-id="7861f-132">API</span><span class="sxs-lookup"><span data-stu-id="7861f-132">API</span></span> | <span data-ttu-id="7861f-133">制限の種類</span><span class="sxs-lookup"><span data-stu-id="7861f-133">Limit Type</span></span> | <span data-ttu-id="7861f-134">制限値</span><span class="sxs-lookup"><span data-stu-id="7861f-134">Limit Value</span></span> | <span data-ttu-id="7861f-135">APU usecase</span><span class="sxs-lookup"><span data-stu-id="7861f-135">APU usecase</span></span> | 
|:---|:---|:---|:--- |
<span data-ttu-id="7861f-136">**PUT** `/api/v2/package`</span><span class="sxs-lookup"><span data-stu-id="7861f-136">**PUT** `/api/v2/package`</span></span> | <span data-ttu-id="7861f-137">API キー</span><span class="sxs-lookup"><span data-stu-id="7861f-137">API Key</span></span> | <span data-ttu-id="7861f-138">100/分</span><span class="sxs-lookup"><span data-stu-id="7861f-138">100 / minute</span></span> | <span data-ttu-id="7861f-139">V2 プッシュ endpoint を使用して新しい NuGet パッケージ (バージョン) をアップロードします。</span><span class="sxs-lookup"><span data-stu-id="7861f-139">Upload a new NuGet package (version) via v2 push endpoint</span></span> 
<span data-ttu-id="7861f-140">**DELETE** `/api/v2/package/{id}/{version}`</span><span class="sxs-lookup"><span data-stu-id="7861f-140">**DELETE** `/api/v2/package/{id}/{version}`</span></span> | <span data-ttu-id="7861f-141">API キー</span><span class="sxs-lookup"><span data-stu-id="7861f-141">API Key</span></span> | <span data-ttu-id="7861f-142">100/分</span><span class="sxs-lookup"><span data-stu-id="7861f-142">100 / minute</span></span> | <span data-ttu-id="7861f-143">非公開 v2 endpoint を使用して NuGet パッケージ (バージョン)</span><span class="sxs-lookup"><span data-stu-id="7861f-143">Unlist a NuGet package (version) via v2 endpoint</span></span> 
