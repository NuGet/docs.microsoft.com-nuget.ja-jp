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
ms.openlocfilehash: 0bc71795d120256b9eb14ca64141f0b69f01e620
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="05b83-103">nuget.org プロトコル</span><span class="sxs-lookup"><span data-stu-id="05b83-103">nuget.org Protocols</span></span>

<span data-ttu-id="05b83-104">Nuget.org をやり取りするには、クライアントは特定のプロトコルに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="05b83-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="05b83-105">これらのプロトコルが進化を保持するため、クライアントは、特定 nuget.org Api を呼び出すときに使用するプロトコルのバージョンを識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="05b83-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="05b83-106">これにより、古いクライアントの重要ではない方法で変更を nuget.org できます。</span><span class="sxs-lookup"><span data-stu-id="05b83-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="05b83-107">このページに記載されている Api は、nuget.org に固有とその他の NuGet サーバー実装をこれらの Api を導入することを見込んではありません。</span><span class="sxs-lookup"><span data-stu-id="05b83-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="05b83-108">NuGet のエコシステムで広範に実装されている NuGet API については、次を参照してください。、 [API の概要](overview.md)です。</span><span class="sxs-lookup"><span data-stu-id="05b83-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="05b83-109">このトピックでは、さまざまなプロトコルと存在するきたときを示します。</span><span class="sxs-lookup"><span data-stu-id="05b83-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="05b83-110">NuGet プロトコル バージョン 4.1.0</span><span class="sxs-lookup"><span data-stu-id="05b83-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="05b83-111">4.1.0 プロトコル nuget.org アカウントに対してパッケージを検証する、nuget.org 以外のサービスと対話することを確認スコープ キーの使用法を指定します。</span><span class="sxs-lookup"><span data-stu-id="05b83-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="05b83-112">なお、`4.1.0`バージョン番号は不透明な文字列がこのプロトコルはサポートされている公式 NuGet クライアントの最初のバージョンと一致するように動作します。</span><span class="sxs-lookup"><span data-stu-id="05b83-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="05b83-113">検証はにより、ユーザーが作成した API キーは nuget.org でのみ使用されますされ、その他の検証またはサード パーティのサービスからの検証が 1 回限り使用することを確認スコープ キーによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="05b83-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="05b83-114">これらのことを確認スコープ キーを使用して、パッケージが nuget.org の特定のユーザー (アカウント) に所属するを検証することです。</span><span class="sxs-lookup"><span data-stu-id="05b83-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="05b83-115">クライアントの要件</span><span class="sxs-lookup"><span data-stu-id="05b83-115">Client requirement</span></span>

<span data-ttu-id="05b83-116">クライアントは、API の呼び出しを行うときは、次のヘッダーを渡す必要**プッシュ**nuget.org をパッケージ。</span><span class="sxs-lookup"><span data-stu-id="05b83-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="05b83-117">なお、`X-NuGet-Client-Version`ヘッダーによく似たセマンティクスは公式 NuGet クライアントでのみ使用される予約済みです。</span><span class="sxs-lookup"><span data-stu-id="05b83-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="05b83-118">サード パーティのクライアントを使用する必要があります、`X-NuGet-Protocol-Version`ヘッダーと値。</span><span class="sxs-lookup"><span data-stu-id="05b83-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="05b83-119">**プッシュ**プロトコル自体がのドキュメントに記載されている、 [ `PackagePublish`リソース](package-publish-resource.md)です。</span><span class="sxs-lookup"><span data-stu-id="05b83-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="05b83-120">クライアントは、外部サービスおよびパッケージは、特定のユーザー (アカウント) に属しているかどうかを検証する必要がありますと対話するを次のプロトコルを使用し、スコープを確認してくださいキーや nuget.org から API キーではないを使用します。</span><span class="sxs-lookup"><span data-stu-id="05b83-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="05b83-121">スコープを確認してくださいキーを要求する API</span><span class="sxs-lookup"><span data-stu-id="05b83-121">API to request a verify-scope key</span></span>

<span data-ttu-id="05b83-122">この API は、' | 4 ' によって所有されているパッケージを検証する nuget.org 作成者のスコープを確認してくださいキーの取得に使用されます。</span><span class="sxs-lookup"><span data-stu-id="05b83-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="05b83-123">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="05b83-123">Request parameters</span></span>

<span data-ttu-id="05b83-124">name</span><span class="sxs-lookup"><span data-stu-id="05b83-124">Name</span></span>           | <span data-ttu-id="05b83-125">イン</span><span class="sxs-lookup"><span data-stu-id="05b83-125">In</span></span>     | <span data-ttu-id="05b83-126">型</span><span class="sxs-lookup"><span data-stu-id="05b83-126">Type</span></span>   | <span data-ttu-id="05b83-127">必須</span><span class="sxs-lookup"><span data-stu-id="05b83-127">Required</span></span> | <span data-ttu-id="05b83-128">メモ</span><span class="sxs-lookup"><span data-stu-id="05b83-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="05b83-129">ID</span><span class="sxs-lookup"><span data-stu-id="05b83-129">ID</span></span>             | <span data-ttu-id="05b83-130">URL</span><span class="sxs-lookup"><span data-stu-id="05b83-130">URL</span></span>    | <span data-ttu-id="05b83-131">string</span><span class="sxs-lookup"><span data-stu-id="05b83-131">string</span></span> | <span data-ttu-id="05b83-132">可</span><span class="sxs-lookup"><span data-stu-id="05b83-132">yes</span></span>      | <span data-ttu-id="05b83-133">確認してくださいスコープ キーを要求する対象のパッケージ identidier</span><span class="sxs-lookup"><span data-stu-id="05b83-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="05b83-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="05b83-134">VERSION</span></span>        | <span data-ttu-id="05b83-135">URL</span><span class="sxs-lookup"><span data-stu-id="05b83-135">URL</span></span>    | <span data-ttu-id="05b83-136">string</span><span class="sxs-lookup"><span data-stu-id="05b83-136">string</span></span> | <span data-ttu-id="05b83-137">Ｘ</span><span class="sxs-lookup"><span data-stu-id="05b83-137">no</span></span>       | <span data-ttu-id="05b83-138">パッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="05b83-138">The package version</span></span>
<span data-ttu-id="05b83-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="05b83-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="05b83-140">Header</span><span class="sxs-lookup"><span data-stu-id="05b83-140">Header</span></span> | <span data-ttu-id="05b83-141">string</span><span class="sxs-lookup"><span data-stu-id="05b83-141">string</span></span> | <span data-ttu-id="05b83-142">可</span><span class="sxs-lookup"><span data-stu-id="05b83-142">yes</span></span>      | <span data-ttu-id="05b83-143">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="05b83-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="05b83-144">応答</span><span class="sxs-lookup"><span data-stu-id="05b83-144">Response</span></span>

```
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="05b83-145">API を確認してくださいスコープ キーを確認するには</span><span class="sxs-lookup"><span data-stu-id="05b83-145">API to verify the verify scope key</span></span>

<span data-ttu-id="05b83-146">この API を使用すると、nuget.org の作成者によって所有されているパッケージのスコープを確認してくださいキーを検証します。</span><span class="sxs-lookup"><span data-stu-id="05b83-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="05b83-147">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="05b83-147">Request parameters</span></span>

<span data-ttu-id="05b83-148">name</span><span class="sxs-lookup"><span data-stu-id="05b83-148">Name</span></span>           | <span data-ttu-id="05b83-149">イン</span><span class="sxs-lookup"><span data-stu-id="05b83-149">In</span></span>     | <span data-ttu-id="05b83-150">型</span><span class="sxs-lookup"><span data-stu-id="05b83-150">Type</span></span>   | <span data-ttu-id="05b83-151">必須</span><span class="sxs-lookup"><span data-stu-id="05b83-151">Required</span></span> | <span data-ttu-id="05b83-152">メモ</span><span class="sxs-lookup"><span data-stu-id="05b83-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="05b83-153">ID</span><span class="sxs-lookup"><span data-stu-id="05b83-153">ID</span></span>             | <span data-ttu-id="05b83-154">URL</span><span class="sxs-lookup"><span data-stu-id="05b83-154">URL</span></span>    | <span data-ttu-id="05b83-155">string</span><span class="sxs-lookup"><span data-stu-id="05b83-155">string</span></span> | <span data-ttu-id="05b83-156">可</span><span class="sxs-lookup"><span data-stu-id="05b83-156">yes</span></span>      | <span data-ttu-id="05b83-157">確認してくださいスコープ キーを要求する対象のパッケージ識別子</span><span class="sxs-lookup"><span data-stu-id="05b83-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="05b83-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="05b83-158">VERSION</span></span>        | <span data-ttu-id="05b83-159">URL</span><span class="sxs-lookup"><span data-stu-id="05b83-159">URL</span></span>    | <span data-ttu-id="05b83-160">string</span><span class="sxs-lookup"><span data-stu-id="05b83-160">string</span></span> | <span data-ttu-id="05b83-161">Ｘ</span><span class="sxs-lookup"><span data-stu-id="05b83-161">no</span></span>       | <span data-ttu-id="05b83-162">パッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="05b83-162">The package version</span></span>
<span data-ttu-id="05b83-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="05b83-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="05b83-164">Header</span><span class="sxs-lookup"><span data-stu-id="05b83-164">Header</span></span> | <span data-ttu-id="05b83-165">string</span><span class="sxs-lookup"><span data-stu-id="05b83-165">string</span></span> | <span data-ttu-id="05b83-166">可</span><span class="sxs-lookup"><span data-stu-id="05b83-166">yes</span></span>      | <span data-ttu-id="05b83-167">たとえば、`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="05b83-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="05b83-168">この確認スコープ API キーの有効期限は 1 日の時刻または初めて使用するとき、先に生じた方です。</span><span class="sxs-lookup"><span data-stu-id="05b83-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="05b83-169">応答</span><span class="sxs-lookup"><span data-stu-id="05b83-169">Response</span></span>

<span data-ttu-id="05b83-170">状態コード</span><span class="sxs-lookup"><span data-stu-id="05b83-170">Status Code</span></span> | <span data-ttu-id="05b83-171">説明</span><span class="sxs-lookup"><span data-stu-id="05b83-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="05b83-172">200</span><span class="sxs-lookup"><span data-stu-id="05b83-172">200</span></span>         | <span data-ttu-id="05b83-173">API キーは無効です。</span><span class="sxs-lookup"><span data-stu-id="05b83-173">The API key is valid</span></span>
<span data-ttu-id="05b83-174">403</span><span class="sxs-lookup"><span data-stu-id="05b83-174">403</span></span>         | <span data-ttu-id="05b83-175">API キーは無効であるか、パッケージに対してをプッシュする権限がありません。</span><span class="sxs-lookup"><span data-stu-id="05b83-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="05b83-176">404</span><span class="sxs-lookup"><span data-stu-id="05b83-176">404</span></span>         | <span data-ttu-id="05b83-177">によって参照されるパッケージ`ID`と`VERSION`(省略可能) は存在しません</span><span class="sxs-lookup"><span data-stu-id="05b83-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
