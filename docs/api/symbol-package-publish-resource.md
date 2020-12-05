---
title: プッシュシンボルパッケージ、NuGet API |Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 発行サービスにより、クライアントは新しいシンボルパッケージを発行できます。
keywords: NuGet API プッシュシンボルパッケージ
ms.reviewer: karann
ms.openlocfilehash: bd4a10cc976c9d0775a63cfe61c35327c196065c
ms.sourcegitcommit: e39e5a5ddf68bf41e816617e7f0339308523bbb3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/05/2020
ms.locfileid: "96738878"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="b3bd8-104">シンボルパッケージのプッシュ</span><span class="sxs-lookup"><span data-stu-id="b3bd8-104">Push Symbol Packages</span></span>

<span data-ttu-id="b3bd8-105">NuGet V3 API を使用してシンボルパッケージ ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) をプッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="b3bd8-106">これらの操作は、 `SymbolPackagePublish` [サービスインデックス](service-index.md)で検出されたリソースに基づいています。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b3bd8-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="b3bd8-107">Versioning</span></span>

<span data-ttu-id="b3bd8-108">次の `@type` 値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-108">The following `@type` value is used:</span></span>

<span data-ttu-id="b3bd8-109">@type 値</span><span class="sxs-lookup"><span data-stu-id="b3bd8-109">@type value</span></span>                 | <span data-ttu-id="b3bd8-110">メモ</span><span class="sxs-lookup"><span data-stu-id="b3bd8-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="b3bd8-111">シンボル Packagepublish/4.9.0-</span><span class="sxs-lookup"><span data-stu-id="b3bd8-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="b3bd8-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="b3bd8-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="b3bd8-113">ベース URL</span><span class="sxs-lookup"><span data-stu-id="b3bd8-113">Base URL</span></span>

<span data-ttu-id="b3bd8-114">次の Api のベース URL は、 `@id` `SymbolPackagePublish/4.9.0` パッケージソースの [サービスインデックス](service-index.md)に含まれるリソースのプロパティの値です。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="b3bd8-115">次のドキュメントでは、nuget の URL が使用されます。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="b3bd8-116">`https://www.nuget.org/api/v2/symbolpackage` `@id` サービスインデックスで見つかった値のプレースホルダーとして考慮します。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b3bd8-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="b3bd8-117">HTTP methods</span></span>

<span data-ttu-id="b3bd8-118">`PUT`このリソースでは、HTTP メソッドがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="b3bd8-119">シンボルパッケージをプッシュする</span><span class="sxs-lookup"><span data-stu-id="b3bd8-119">Push a symbol package</span></span>

<span data-ttu-id="b3bd8-120">nuget.org では、次の API を使用した新しいシンボルパッケージ形式 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) のプッシュがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="b3bd8-121">同じ ID とバージョンのシンボルパッケージは、複数回送信できます。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="b3bd8-122">シンボルパッケージは、次の場合には拒否されます。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="b3bd8-123">同じ ID とバージョンのパッケージが存在しません。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="b3bd8-124">同じ ID とバージョンのシンボルパッケージがプッシュされましたが、まだ発行されていません。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="b3bd8-125">シンボルパッケージ ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) が無効です (「 [シンボルパッケージの制約](../create-packages/Symbol-Packages-snupkg.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="b3bd8-126">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="b3bd8-126">Request parameters</span></span>

<span data-ttu-id="b3bd8-127">Name</span><span class="sxs-lookup"><span data-stu-id="b3bd8-127">Name</span></span>           | <span data-ttu-id="b3bd8-128">/</span><span class="sxs-lookup"><span data-stu-id="b3bd8-128">In</span></span>     | <span data-ttu-id="b3bd8-129">型</span><span class="sxs-lookup"><span data-stu-id="b3bd8-129">Type</span></span>   | <span data-ttu-id="b3bd8-130">必須</span><span class="sxs-lookup"><span data-stu-id="b3bd8-130">Required</span></span> | <span data-ttu-id="b3bd8-131">メモ</span><span class="sxs-lookup"><span data-stu-id="b3bd8-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b3bd8-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b3bd8-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b3bd8-133">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="b3bd8-133">Header</span></span> | <span data-ttu-id="b3bd8-134">string</span><span class="sxs-lookup"><span data-stu-id="b3bd8-134">string</span></span> | <span data-ttu-id="b3bd8-135">はい</span><span class="sxs-lookup"><span data-stu-id="b3bd8-135">yes</span></span>      | <span data-ttu-id="b3bd8-136">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="b3bd8-137">API キーは、ユーザーによってパッケージソースから得られた非透過文字列であり、クライアントに構成されています。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="b3bd8-138">特定の文字列形式は必須ではありませんが、API キーの長さは HTTP ヘッダー値に対して妥当なサイズを超えることはできません。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="b3bd8-139">要求本文</span><span class="sxs-lookup"><span data-stu-id="b3bd8-139">Request body</span></span>

<span data-ttu-id="b3bd8-140">シンボルプッシュの要求本文は、パッケージプッシュ要求の要求本文と同じです (「 [パッケージプッシュと削除](package-publish-resource.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="b3bd8-141">Response</span><span class="sxs-lookup"><span data-stu-id="b3bd8-141">Response</span></span>

<span data-ttu-id="b3bd8-142">状態コード</span><span class="sxs-lookup"><span data-stu-id="b3bd8-142">Status Code</span></span> | <span data-ttu-id="b3bd8-143">説明</span><span class="sxs-lookup"><span data-stu-id="b3bd8-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="b3bd8-144">201</span><span class="sxs-lookup"><span data-stu-id="b3bd8-144">201</span></span>         | <span data-ttu-id="b3bd8-145">シンボルパッケージが正常にプッシュされました。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="b3bd8-146">400</span><span class="sxs-lookup"><span data-stu-id="b3bd8-146">400</span></span>         | <span data-ttu-id="b3bd8-147">指定されたシンボルパッケージは無効です。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="b3bd8-148">401</span><span class="sxs-lookup"><span data-stu-id="b3bd8-148">401</span></span>         | <span data-ttu-id="b3bd8-149">この操作を実行する権限がユーザーにありません。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="b3bd8-150">404</span><span class="sxs-lookup"><span data-stu-id="b3bd8-150">404</span></span>         | <span data-ttu-id="b3bd8-151">指定された ID とバージョンの対応するパッケージが存在しません。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="b3bd8-152">409</span><span class="sxs-lookup"><span data-stu-id="b3bd8-152">409</span></span>         | <span data-ttu-id="b3bd8-153">指定された ID とバージョンのシンボルパッケージはプッシュされましたが、まだ使用できません。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="b3bd8-154">413</span><span class="sxs-lookup"><span data-stu-id="b3bd8-154">413</span></span>         | <span data-ttu-id="b3bd8-155">パッケージが大きすぎます。</span><span class="sxs-lookup"><span data-stu-id="b3bd8-155">The package is too large.</span></span>

