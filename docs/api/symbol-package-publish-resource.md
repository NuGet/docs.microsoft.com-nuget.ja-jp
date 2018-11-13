---
title: シンボル パッケージを NuGet API をプッシュ |Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 発行サービスは、新しいシンボル パッケージを公開するクライアントを使用します。
keywords: NuGet API プッシュ シンボル パッケージ
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580415"
---
# <a name="push-symbol-packages"></a><span data-ttu-id="8066c-104">シンボル パッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="8066c-104">Push Symbol Packages</span></span>

<span data-ttu-id="8066c-105">シンボル パッケージをプッシュすることができます ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) NuGet V3 API を使用します。</span><span class="sxs-lookup"><span data-stu-id="8066c-105">It is possible to push symbols packages ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the NuGet V3 API.</span></span>
<span data-ttu-id="8066c-106">これらの操作は無効の基づいて、`SymbolPackagePublish`リソースで見つかった、[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="8066c-106">These operations are based off of the `SymbolPackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8066c-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="8066c-107">Versioning</span></span>

<span data-ttu-id="8066c-108">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="8066c-108">The following `@type` value is used:</span></span>

<span data-ttu-id="8066c-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="8066c-109">@type value</span></span>                 | <span data-ttu-id="8066c-110">メモ</span><span class="sxs-lookup"><span data-stu-id="8066c-110">Notes</span></span>
--------------------        | -----
<span data-ttu-id="8066c-111">SymbolPackagePublish/4.9.0</span><span class="sxs-lookup"><span data-stu-id="8066c-111">SymbolPackagePublish/4.9.0</span></span>  | <span data-ttu-id="8066c-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="8066c-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="8066c-113">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="8066c-113">Base URL</span></span>

<span data-ttu-id="8066c-114">次の Api のベース URL の値は、`@id`のプロパティ、`SymbolPackagePublish/4.9.0`パッケージ ソースのリソース[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="8066c-114">The base URL for the following APIs is the value of the `@id` property of the `SymbolPackagePublish/4.9.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="8066c-115">次のドキュメントでは、nuget.org の URL を使用します。</span><span class="sxs-lookup"><span data-stu-id="8066c-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="8066c-116">検討`https://www.nuget.org/api/v2/symbolpackage`のプレース ホルダーとして、`@id`サービス インデックスにある値。</span><span class="sxs-lookup"><span data-stu-id="8066c-116">Consider `https://www.nuget.org/api/v2/symbolpackage` as a placeholder for the `@id` value found in the service index.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8066c-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="8066c-117">HTTP methods</span></span>

<span data-ttu-id="8066c-118">`PUT` HTTP メソッドがこのリソースでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8066c-118">The `PUT` HTTP method is supported by this resource.</span></span> 

## <a name="push-a-symbol-package"></a><span data-ttu-id="8066c-119">シンボル パッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="8066c-119">Push a symbol package</span></span>

<span data-ttu-id="8066c-120">nuget.org にプッシュの新しいシンボル パッケージ形式がサポートしています ([snupkg](../create-packages/Symbol-Packages-snupkg.md))、次の API を使用します。</span><span class="sxs-lookup"><span data-stu-id="8066c-120">nuget.org supports pushing new symbol packages format ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) using the following API.</span></span> 

    PUT https://www.nuget.org/api/v2/symbolpackage

<span data-ttu-id="8066c-121">シンボル パッケージ ID とバージョンが同じでは、複数回送信できます。</span><span class="sxs-lookup"><span data-stu-id="8066c-121">Symbol packages with the same ID and version can be submitted multiple times.</span></span> <span data-ttu-id="8066c-122">シンボル パッケージは、次の場合に拒否されます。</span><span class="sxs-lookup"><span data-stu-id="8066c-122">A symbol package will be rejected in the following cases.</span></span>
- <span data-ttu-id="8066c-123">同じ ID とバージョンを使用してパッケージが存在しません。</span><span class="sxs-lookup"><span data-stu-id="8066c-123">A package with the same ID and version does not exist.</span></span>
- <span data-ttu-id="8066c-124">シンボル パッケージ ID とバージョンが同じでは、プッシュされたが、まだ公開されていません。</span><span class="sxs-lookup"><span data-stu-id="8066c-124">A symbol package with the same ID and version was pushed but is not yet published.</span></span>
- <span data-ttu-id="8066c-125">シンボル パッケージ ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) が無効です (を参照してください[シンボル パッケージ制約](../create-packages/Symbol-Packages-snupkg.md))。</span><span class="sxs-lookup"><span data-stu-id="8066c-125">The symbol package ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) is invalid (see [symbol package constraints](../create-packages/Symbol-Packages-snupkg.md)).</span></span>

### <a name="request-parameters"></a><span data-ttu-id="8066c-126">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="8066c-126">Request parameters</span></span>

<span data-ttu-id="8066c-127">名前</span><span class="sxs-lookup"><span data-stu-id="8066c-127">Name</span></span>           | <span data-ttu-id="8066c-128">イン</span><span class="sxs-lookup"><span data-stu-id="8066c-128">In</span></span>     | <span data-ttu-id="8066c-129">型</span><span class="sxs-lookup"><span data-stu-id="8066c-129">Type</span></span>   | <span data-ttu-id="8066c-130">必須</span><span class="sxs-lookup"><span data-stu-id="8066c-130">Required</span></span> | <span data-ttu-id="8066c-131">メモ</span><span class="sxs-lookup"><span data-stu-id="8066c-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="8066c-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="8066c-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="8066c-133">Header</span><span class="sxs-lookup"><span data-stu-id="8066c-133">Header</span></span> | <span data-ttu-id="8066c-134">string</span><span class="sxs-lookup"><span data-stu-id="8066c-134">string</span></span> | <span data-ttu-id="8066c-135">可</span><span class="sxs-lookup"><span data-stu-id="8066c-135">yes</span></span>      | <span data-ttu-id="8066c-136">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="8066c-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="8066c-137">API キーは、ユーザーがパッケージ ソースから取得し、クライアントに構成されている不透明な文字列です。</span><span class="sxs-lookup"><span data-stu-id="8066c-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="8066c-138">特定の文字列形式が必須でありませんが、API キーの長さは、適切な HTTP ヘッダーの値のサイズを超えない必要があります。</span><span class="sxs-lookup"><span data-stu-id="8066c-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="8066c-139">要求本文</span><span class="sxs-lookup"><span data-stu-id="8066c-139">Request body</span></span>

<span data-ttu-id="8066c-140">シンボルのプッシュの要求本文は、パッケージのプッシュ要求の要求の本体と同じ (を参照してください[プッシュをパッケージ化し、削除](package-publish-resource.md))。</span><span class="sxs-lookup"><span data-stu-id="8066c-140">The request body for the symbol push is same as with the request body of a package push request (see [package push and delete](package-publish-resource.md)).</span></span> 

### <a name="response"></a><span data-ttu-id="8066c-141">応答</span><span class="sxs-lookup"><span data-stu-id="8066c-141">Response</span></span>

<span data-ttu-id="8066c-142">状態コード</span><span class="sxs-lookup"><span data-stu-id="8066c-142">Status Code</span></span> | <span data-ttu-id="8066c-143">説明</span><span class="sxs-lookup"><span data-stu-id="8066c-143">Meaning</span></span>
----------- | -------
<span data-ttu-id="8066c-144">201</span><span class="sxs-lookup"><span data-stu-id="8066c-144">201</span></span>         | <span data-ttu-id="8066c-145">シンボル パッケージが正常にプッシュされました。</span><span class="sxs-lookup"><span data-stu-id="8066c-145">The symbol package was successfully pushed.</span></span>
<span data-ttu-id="8066c-146">400</span><span class="sxs-lookup"><span data-stu-id="8066c-146">400</span></span>         | <span data-ttu-id="8066c-147">指定されたシンボル パッケージが無効です。</span><span class="sxs-lookup"><span data-stu-id="8066c-147">The provided symbol package is invalid.</span></span>
<span data-ttu-id="8066c-148">401</span><span class="sxs-lookup"><span data-stu-id="8066c-148">401</span></span>         | <span data-ttu-id="8066c-149">ユーザーは、この操作を実行する権限がありません。</span><span class="sxs-lookup"><span data-stu-id="8066c-149">The user is not authorized to perform this action.</span></span>
<span data-ttu-id="8066c-150">404</span><span class="sxs-lookup"><span data-stu-id="8066c-150">404</span></span>         | <span data-ttu-id="8066c-151">指定された ID とバージョンを使用して対応するパッケージが存在しません。</span><span class="sxs-lookup"><span data-stu-id="8066c-151">A corresponding package with the provided ID and version does not exist.</span></span>
<span data-ttu-id="8066c-152">409</span><span class="sxs-lookup"><span data-stu-id="8066c-152">409</span></span>         | <span data-ttu-id="8066c-153">指定された ID とバージョンで、シンボル パッケージのプッシュが、これはまだ利用できません。</span><span class="sxs-lookup"><span data-stu-id="8066c-153">A symbol package with the provided ID and version was pushed but it is not available yet.</span></span>
<span data-ttu-id="8066c-154">413</span><span class="sxs-lookup"><span data-stu-id="8066c-154">413</span></span>         | <span data-ttu-id="8066c-155">パッケージが大きすぎます。</span><span class="sxs-lookup"><span data-stu-id="8066c-155">The package is too large.</span></span>

