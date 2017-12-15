---
title: "nuget.org プロトコル |Microsoft ドキュメント"
author: anangaur
ms.author: anangaur
manager: unniravindranathan
ms.date: 10/30/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: ba1d9742-9f1c-42ff-8c30-8e953e23c501
description: "NuGet のクライアントと対話する継続的に進化 nuget.org プロトコル。"
ms.reviewer:
- kraigb
- karann-msft
ms.openlocfilehash: 097b7a86d056b692c52d6de76bc2fb99d1b58c6f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="a3cac-103">nuget.org プロトコル</span><span class="sxs-lookup"><span data-stu-id="a3cac-103">nuget.org Protocols</span></span>

<span data-ttu-id="a3cac-104">Nuget.org をやり取りするには、クライアントは特定のプロトコルに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="a3cac-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="a3cac-105">これらのプロトコルが進化を保持するため、クライアントは、特定 nuget.org Api を呼び出すときに使用するプロトコルのバージョンを識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a3cac-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="a3cac-106">これにより、古いクライアントの重要ではない方法で変更を nuget.org できます。</span><span class="sxs-lookup"><span data-stu-id="a3cac-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="a3cac-107">このページに記載されている Api は、nuget.org に固有とその他の NuGet サーバー実装をこれらの Api を導入することを見込んではありません。</span><span class="sxs-lookup"><span data-stu-id="a3cac-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="a3cac-108">NuGet のエコシステムで広範に実装されている NuGet API については、次を参照してください。、 [API の概要](overview.md)です。</span><span class="sxs-lookup"><span data-stu-id="a3cac-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="a3cac-109">このトピックでは、さまざまなプロトコルと存在するきたときを示します。</span><span class="sxs-lookup"><span data-stu-id="a3cac-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="a3cac-110">NuGet プロトコル バージョン 4.1.0</span><span class="sxs-lookup"><span data-stu-id="a3cac-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="a3cac-111">4.1.0 プロトコル nuget.org アカウントに対してパッケージを検証する、nuget.org 以外のサービスと対話することを確認スコープ キーの使用法を指定します。</span><span class="sxs-lookup"><span data-stu-id="a3cac-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="a3cac-112">なお、`4.1.0`バージョン番号は不透明な文字列がこのプロトコルはサポートされている公式 NuGet クライアントの最初のバージョンと一致するように動作します。</span><span class="sxs-lookup"><span data-stu-id="a3cac-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="a3cac-113">検証はにより、ユーザーが作成した API キーは nuget.org でのみ使用されますされ、その他の検証またはサード パーティのサービスからの検証が 1 回限り使用することを確認スコープ キーによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="a3cac-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="a3cac-114">これらのことを確認スコープ キーを使用して、パッケージが nuget.org の特定のユーザー (アカウント) に所属するを検証することです。</span><span class="sxs-lookup"><span data-stu-id="a3cac-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="a3cac-115">クライアントの要件</span><span class="sxs-lookup"><span data-stu-id="a3cac-115">Client requirement</span></span>

<span data-ttu-id="a3cac-116">クライアントは、API の呼び出しを行うときは、次のヘッダーを渡す必要**プッシュ**nuget.org をパッケージ。</span><span class="sxs-lookup"><span data-stu-id="a3cac-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="a3cac-117">なお、既存の`X-NuGet-Client-Version`ヘッダー同じ目的が使用されなくなりましたがあり、使用できなくする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a3cac-117">Note that the pre-existing `X-NuGet-Client-Version` header has the same purpose but is now deprecated and should no longer be used.</span></span>

<span data-ttu-id="a3cac-118">**プッシュ**プロトコル自体がのドキュメントに記載されている、 [ `PackagePublish`リソース](package-publish-resource.md)です。</span><span class="sxs-lookup"><span data-stu-id="a3cac-118">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="a3cac-119">クライアントは、外部サービスおよびパッケージは、特定のユーザー (アカウント) に属しているかどうかを検証する必要がありますと対話するを次のプロトコルを使用し、スコープを確認してくださいキーや nuget.org から API キーではないを使用します。</span><span class="sxs-lookup"><span data-stu-id="a3cac-119">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="a3cac-120">スコープを確認してくださいキーを要求する API</span><span class="sxs-lookup"><span data-stu-id="a3cac-120">API to request a verify-scope key</span></span>

<span data-ttu-id="a3cac-121">この API は、' | 4 ' によって所有されているパッケージを検証する nuget.org 作成者のスコープを確認してくださいキーの取得に使用されます。</span><span class="sxs-lookup"><span data-stu-id="a3cac-121">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="a3cac-122">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="a3cac-122">Request parameters</span></span>

<span data-ttu-id="a3cac-123">名前</span><span class="sxs-lookup"><span data-stu-id="a3cac-123">Name</span></span>           | <span data-ttu-id="a3cac-124">イン</span><span class="sxs-lookup"><span data-stu-id="a3cac-124">In</span></span>     | <span data-ttu-id="a3cac-125">型</span><span class="sxs-lookup"><span data-stu-id="a3cac-125">Type</span></span>   | <span data-ttu-id="a3cac-126">必須</span><span class="sxs-lookup"><span data-stu-id="a3cac-126">Required</span></span> | <span data-ttu-id="a3cac-127">メモ</span><span class="sxs-lookup"><span data-stu-id="a3cac-127">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="a3cac-128">ID</span><span class="sxs-lookup"><span data-stu-id="a3cac-128">ID</span></span>             | <span data-ttu-id="a3cac-129">URL</span><span class="sxs-lookup"><span data-stu-id="a3cac-129">URL</span></span>    | <span data-ttu-id="a3cac-130">string</span><span class="sxs-lookup"><span data-stu-id="a3cac-130">string</span></span> | <span data-ttu-id="a3cac-131">可</span><span class="sxs-lookup"><span data-stu-id="a3cac-131">yes</span></span>      | <span data-ttu-id="a3cac-132">確認してくださいスコープ キーを要求する対象のパッケージ identidier</span><span class="sxs-lookup"><span data-stu-id="a3cac-132">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="a3cac-133">VERSION</span><span class="sxs-lookup"><span data-stu-id="a3cac-133">VERSION</span></span>        | <span data-ttu-id="a3cac-134">URL</span><span class="sxs-lookup"><span data-stu-id="a3cac-134">URL</span></span>    | <span data-ttu-id="a3cac-135">string</span><span class="sxs-lookup"><span data-stu-id="a3cac-135">string</span></span> | <span data-ttu-id="a3cac-136">Ｘ</span><span class="sxs-lookup"><span data-stu-id="a3cac-136">no</span></span>       | <span data-ttu-id="a3cac-137">パッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="a3cac-137">The package version</span></span>
<span data-ttu-id="a3cac-138">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="a3cac-138">X-NuGet-ApiKey</span></span> | <span data-ttu-id="a3cac-139">Header</span><span class="sxs-lookup"><span data-stu-id="a3cac-139">Header</span></span> | <span data-ttu-id="a3cac-140">string</span><span class="sxs-lookup"><span data-stu-id="a3cac-140">string</span></span> | <span data-ttu-id="a3cac-141">可</span><span class="sxs-lookup"><span data-stu-id="a3cac-141">yes</span></span>      | <span data-ttu-id="a3cac-142">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="a3cac-142">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="a3cac-143">応答</span><span class="sxs-lookup"><span data-stu-id="a3cac-143">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="a3cac-144">API を確認してくださいスコープ キーを確認するには</span><span class="sxs-lookup"><span data-stu-id="a3cac-144">API to verify the verify scope key</span></span>

<span data-ttu-id="a3cac-145">この API を使用すると、nuget.org の作成者によって所有されているパッケージのスコープを確認してくださいキーを検証します。</span><span class="sxs-lookup"><span data-stu-id="a3cac-145">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="a3cac-146">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="a3cac-146">Request parameters</span></span>

<span data-ttu-id="a3cac-147">名前</span><span class="sxs-lookup"><span data-stu-id="a3cac-147">Name</span></span>           | <span data-ttu-id="a3cac-148">イン</span><span class="sxs-lookup"><span data-stu-id="a3cac-148">In</span></span>     | <span data-ttu-id="a3cac-149">型</span><span class="sxs-lookup"><span data-stu-id="a3cac-149">Type</span></span>   | <span data-ttu-id="a3cac-150">必須</span><span class="sxs-lookup"><span data-stu-id="a3cac-150">Required</span></span> | <span data-ttu-id="a3cac-151">メモ</span><span class="sxs-lookup"><span data-stu-id="a3cac-151">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="a3cac-152">ID</span><span class="sxs-lookup"><span data-stu-id="a3cac-152">ID</span></span>             | <span data-ttu-id="a3cac-153">URL</span><span class="sxs-lookup"><span data-stu-id="a3cac-153">URL</span></span>    | <span data-ttu-id="a3cac-154">string</span><span class="sxs-lookup"><span data-stu-id="a3cac-154">string</span></span> | <span data-ttu-id="a3cac-155">可</span><span class="sxs-lookup"><span data-stu-id="a3cac-155">yes</span></span>      | <span data-ttu-id="a3cac-156">確認してくださいスコープ キーを要求する対象のパッケージ識別子</span><span class="sxs-lookup"><span data-stu-id="a3cac-156">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="a3cac-157">VERSION</span><span class="sxs-lookup"><span data-stu-id="a3cac-157">VERSION</span></span>        | <span data-ttu-id="a3cac-158">URL</span><span class="sxs-lookup"><span data-stu-id="a3cac-158">URL</span></span>    | <span data-ttu-id="a3cac-159">string</span><span class="sxs-lookup"><span data-stu-id="a3cac-159">string</span></span> | <span data-ttu-id="a3cac-160">Ｘ</span><span class="sxs-lookup"><span data-stu-id="a3cac-160">no</span></span>       | <span data-ttu-id="a3cac-161">パッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="a3cac-161">The package version</span></span>
<span data-ttu-id="a3cac-162">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="a3cac-162">X-NuGet-ApiKey</span></span> | <span data-ttu-id="a3cac-163">Header</span><span class="sxs-lookup"><span data-stu-id="a3cac-163">Header</span></span> | <span data-ttu-id="a3cac-164">string</span><span class="sxs-lookup"><span data-stu-id="a3cac-164">string</span></span> | <span data-ttu-id="a3cac-165">可</span><span class="sxs-lookup"><span data-stu-id="a3cac-165">yes</span></span>      | <span data-ttu-id="a3cac-166">たとえば、`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="a3cac-166">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="a3cac-167">この確認スコープ API キーの有効期限は 1 日の時刻または初めて使用するとき、先に生じた方です。</span><span class="sxs-lookup"><span data-stu-id="a3cac-167">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="a3cac-168">応答</span><span class="sxs-lookup"><span data-stu-id="a3cac-168">Response</span></span>

<span data-ttu-id="a3cac-169">状態コード</span><span class="sxs-lookup"><span data-stu-id="a3cac-169">Status Code</span></span> | <span data-ttu-id="a3cac-170">説明</span><span class="sxs-lookup"><span data-stu-id="a3cac-170">Meaning</span></span>
----------- | -------
<span data-ttu-id="a3cac-171">200</span><span class="sxs-lookup"><span data-stu-id="a3cac-171">200</span></span>         | <span data-ttu-id="a3cac-172">API キーは無効です。</span><span class="sxs-lookup"><span data-stu-id="a3cac-172">The API key is valid</span></span>
<span data-ttu-id="a3cac-173">403</span><span class="sxs-lookup"><span data-stu-id="a3cac-173">403</span></span>         | <span data-ttu-id="a3cac-174">API キーは無効であるか、パッケージに対してをプッシュする権限がありません。</span><span class="sxs-lookup"><span data-stu-id="a3cac-174">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="a3cac-175">404</span><span class="sxs-lookup"><span data-stu-id="a3cac-175">404</span></span>         | <span data-ttu-id="a3cac-176">によって参照されるパッケージ`ID`と`VERSION`(省略可能) は存在しません</span><span class="sxs-lookup"><span data-stu-id="a3cac-176">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
