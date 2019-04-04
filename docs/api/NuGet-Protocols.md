---
title: nuget.org プロトコル
description: NuGet クライアントと対話する進化 nuget.org プロトコル。
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547274"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="b2af5-103">nuget.org protocols</span><span class="sxs-lookup"><span data-stu-id="b2af5-103">nuget.org protocols</span></span>

<span data-ttu-id="b2af5-104">Nuget.org をやり取りするには、クライアントは特定のプロトコルに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2af5-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="b2af5-105">これらのプロトコル、進化、ために、クライアントは、特定 nuget.org の Api を呼び出すときに使用するプロトコルのバージョンを識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2af5-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="b2af5-106">これにより、古いクライアントの互換性に影響しない方法で変更を導入する nuget.org ができます。</span><span class="sxs-lookup"><span data-stu-id="b2af5-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="b2af5-107">このページに記載されている Api は nuget.org に固有と、これらの Api を導入するその他の NuGet サーバーの実装に対する期待はありません。</span><span class="sxs-lookup"><span data-stu-id="b2af5-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="b2af5-108">NuGet エコシステム全体で広く実装されている NuGet API については、、 [API の概要](overview.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2af5-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="b2af5-109">このトピックでは、としてさまざまなプロトコルと存在に来たときに一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b2af5-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="b2af5-110">プロトコルのバージョンの NuGet 4.1.0</span><span class="sxs-lookup"><span data-stu-id="b2af5-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="b2af5-111">4.1.0 プロトコルを nuget.org には、nuget.org アカウントに対して、パッケージを検証する以外のサービスと対話することを確認スコープのキーの使用量を指定します。</span><span class="sxs-lookup"><span data-stu-id="b2af5-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="b2af5-112">なお、`4.1.0`バージョン数値が不透明な文字列が、このプロトコルがサポートされている公式の NuGet クライアントの最初のバージョンと同時に発生します。</span><span class="sxs-lookup"><span data-stu-id="b2af5-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="b2af5-113">検証では、ユーザーが作成した API キーは、nuget.org でのみ使用され、その他の検証またはサード パーティのサービスからの検証は、1 回だけ使用確認スコープ キーを介して処理されことを確認します。</span><span class="sxs-lookup"><span data-stu-id="b2af5-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="b2af5-114">パッケージを nuget.org で特定のユーザー (アカウント) が属していることを検証することを確認スコープのこれらのキーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="b2af5-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="b2af5-115">クライアントの要件</span><span class="sxs-lookup"><span data-stu-id="b2af5-115">Client requirement</span></span>

<span data-ttu-id="b2af5-116">クライアントは、API の呼び出しを行ったときに、次のヘッダーを渡す必要**プッシュ**nuget.org にパッケージ。</span><span class="sxs-lookup"><span data-stu-id="b2af5-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

    X-NuGet-Protocol-Version: 4.1.0

<span data-ttu-id="b2af5-117">なお、`X-NuGet-Client-Version`ヘッダーのような意味を持ちますが、公式の NuGet クライアントでのみ使用される予約されています。</span><span class="sxs-lookup"><span data-stu-id="b2af5-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="b2af5-118">サード パーティのクライアントを使用する必要があります、`X-NuGet-Protocol-Version`ヘッダーと値。</span><span class="sxs-lookup"><span data-stu-id="b2af5-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="b2af5-119">**プッシュ**プロトコル自体がドキュメントで説明されている、 [ `PackagePublish`リソース](package-publish-resource.md)します。</span><span class="sxs-lookup"><span data-stu-id="b2af5-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="b2af5-120">クライアントは、外部のサービスおよびパッケージは、特定のユーザー (アカウント) が属しているかどうかを検証する必要があると対話するを次のプロトコルを使用し、使用して、検証スコープ キーと nuget.org から API キーではありません。</span><span class="sxs-lookup"><span data-stu-id="b2af5-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="b2af5-121">API スコープを確認してくださいキーを要求するには</span><span class="sxs-lookup"><span data-stu-id="b2af5-121">API to request a verify-scope key</span></span>

<span data-ttu-id="b2af5-122">この API を使用して、につきによって所有されているパッケージを検証する nuget.org 作成者のスコープを確認してくださいキーを取得します。</span><span class="sxs-lookup"><span data-stu-id="b2af5-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="b2af5-123">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="b2af5-123">Request parameters</span></span>

<span data-ttu-id="b2af5-124">名前</span><span class="sxs-lookup"><span data-stu-id="b2af5-124">Name</span></span>           | <span data-ttu-id="b2af5-125">イン</span><span class="sxs-lookup"><span data-stu-id="b2af5-125">In</span></span>     | <span data-ttu-id="b2af5-126">型</span><span class="sxs-lookup"><span data-stu-id="b2af5-126">Type</span></span>   | <span data-ttu-id="b2af5-127">必須</span><span class="sxs-lookup"><span data-stu-id="b2af5-127">Required</span></span> | <span data-ttu-id="b2af5-128">メモ</span><span class="sxs-lookup"><span data-stu-id="b2af5-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b2af5-129">ID</span><span class="sxs-lookup"><span data-stu-id="b2af5-129">ID</span></span>             | <span data-ttu-id="b2af5-130">URL</span><span class="sxs-lookup"><span data-stu-id="b2af5-130">URL</span></span>    | <span data-ttu-id="b2af5-131">string</span><span class="sxs-lookup"><span data-stu-id="b2af5-131">string</span></span> | <span data-ttu-id="b2af5-132">可</span><span class="sxs-lookup"><span data-stu-id="b2af5-132">yes</span></span>      | <span data-ttu-id="b2af5-133">確認のスコープのキーを要求する対象のパッケージ identidier</span><span class="sxs-lookup"><span data-stu-id="b2af5-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="b2af5-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="b2af5-134">VERSION</span></span>        | <span data-ttu-id="b2af5-135">URL</span><span class="sxs-lookup"><span data-stu-id="b2af5-135">URL</span></span>    | <span data-ttu-id="b2af5-136">string</span><span class="sxs-lookup"><span data-stu-id="b2af5-136">string</span></span> | <span data-ttu-id="b2af5-137">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b2af5-137">no</span></span>       | <span data-ttu-id="b2af5-138">パッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="b2af5-138">The package version</span></span>
<span data-ttu-id="b2af5-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b2af5-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b2af5-140">Header</span><span class="sxs-lookup"><span data-stu-id="b2af5-140">Header</span></span> | <span data-ttu-id="b2af5-141">string</span><span class="sxs-lookup"><span data-stu-id="b2af5-141">string</span></span> | <span data-ttu-id="b2af5-142">可</span><span class="sxs-lookup"><span data-stu-id="b2af5-142">yes</span></span>      | <span data-ttu-id="b2af5-143">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b2af5-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="b2af5-144">応答</span><span class="sxs-lookup"><span data-stu-id="b2af5-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="b2af5-145">API を確認のスコープのキーを確認します。</span><span class="sxs-lookup"><span data-stu-id="b2af5-145">API to verify the verify scope key</span></span>

<span data-ttu-id="b2af5-146">この API は、nuget.org の作成者によって所有されているパッケージの検証スコープ キーの検証に使用されます。</span><span class="sxs-lookup"><span data-stu-id="b2af5-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a><span data-ttu-id="b2af5-147">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="b2af5-147">Request parameters</span></span>

<span data-ttu-id="b2af5-148">名前</span><span class="sxs-lookup"><span data-stu-id="b2af5-148">Name</span></span>           | <span data-ttu-id="b2af5-149">イン</span><span class="sxs-lookup"><span data-stu-id="b2af5-149">In</span></span>     | <span data-ttu-id="b2af5-150">型</span><span class="sxs-lookup"><span data-stu-id="b2af5-150">Type</span></span>   | <span data-ttu-id="b2af5-151">必須</span><span class="sxs-lookup"><span data-stu-id="b2af5-151">Required</span></span> | <span data-ttu-id="b2af5-152">メモ</span><span class="sxs-lookup"><span data-stu-id="b2af5-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="b2af5-153">ID</span><span class="sxs-lookup"><span data-stu-id="b2af5-153">ID</span></span>             | <span data-ttu-id="b2af5-154">URL</span><span class="sxs-lookup"><span data-stu-id="b2af5-154">URL</span></span>    | <span data-ttu-id="b2af5-155">string</span><span class="sxs-lookup"><span data-stu-id="b2af5-155">string</span></span> | <span data-ttu-id="b2af5-156">可</span><span class="sxs-lookup"><span data-stu-id="b2af5-156">yes</span></span>      | <span data-ttu-id="b2af5-157">確認のスコープのキーを要求する対象のパッケージ識別子</span><span class="sxs-lookup"><span data-stu-id="b2af5-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="b2af5-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="b2af5-158">VERSION</span></span>        | <span data-ttu-id="b2af5-159">URL</span><span class="sxs-lookup"><span data-stu-id="b2af5-159">URL</span></span>    | <span data-ttu-id="b2af5-160">string</span><span class="sxs-lookup"><span data-stu-id="b2af5-160">string</span></span> | <span data-ttu-id="b2af5-161">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b2af5-161">no</span></span>       | <span data-ttu-id="b2af5-162">パッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="b2af5-162">The package version</span></span>
<span data-ttu-id="b2af5-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b2af5-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b2af5-164">Header</span><span class="sxs-lookup"><span data-stu-id="b2af5-164">Header</span></span> | <span data-ttu-id="b2af5-165">string</span><span class="sxs-lookup"><span data-stu-id="b2af5-165">string</span></span> | <span data-ttu-id="b2af5-166">可</span><span class="sxs-lookup"><span data-stu-id="b2af5-166">yes</span></span>      | <span data-ttu-id="b2af5-167">たとえば、`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span><span class="sxs-lookup"><span data-stu-id="b2af5-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="b2af5-168">この確認スコープ API キーの有効期限は 1 日の時間または初めて使用する、どちらかに最初に発生します。</span><span class="sxs-lookup"><span data-stu-id="b2af5-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="b2af5-169">応答</span><span class="sxs-lookup"><span data-stu-id="b2af5-169">Response</span></span>

<span data-ttu-id="b2af5-170">状態コード</span><span class="sxs-lookup"><span data-stu-id="b2af5-170">Status Code</span></span> | <span data-ttu-id="b2af5-171">説明</span><span class="sxs-lookup"><span data-stu-id="b2af5-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="b2af5-172">200</span><span class="sxs-lookup"><span data-stu-id="b2af5-172">200</span></span>         | <span data-ttu-id="b2af5-173">API キーは無効です。</span><span class="sxs-lookup"><span data-stu-id="b2af5-173">The API key is valid</span></span>
<span data-ttu-id="b2af5-174">403</span><span class="sxs-lookup"><span data-stu-id="b2af5-174">403</span></span>         | <span data-ttu-id="b2af5-175">API キーが無効であるか、パッケージをプッシュする権限がありません。</span><span class="sxs-lookup"><span data-stu-id="b2af5-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="b2af5-176">404</span><span class="sxs-lookup"><span data-stu-id="b2af5-176">404</span></span>         | <span data-ttu-id="b2af5-177">によって参照されるパッケージ`ID`と`VERSION`(省略可能) は存在しません</span><span class="sxs-lookup"><span data-stu-id="b2af5-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
