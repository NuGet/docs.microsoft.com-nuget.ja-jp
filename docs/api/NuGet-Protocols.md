---
title: nuget.org プロトコル
description: NuGet クライアントと対話するための進化する nuget.org プロトコル。
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773979"
---
# <a name="nugetorg-protocols"></a><span data-ttu-id="b2474-103">nuget.org プロトコル</span><span class="sxs-lookup"><span data-stu-id="b2474-103">nuget.org protocols</span></span>

<span data-ttu-id="b2474-104">Nuget.org と対話するには、クライアントは特定のプロトコルに従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2474-104">To interact with nuget.org, clients need to follow certain protocols.</span></span> <span data-ttu-id="b2474-105">これらのプロトコルは進化し続けるため、クライアントは、特定の nuget.org Api を呼び出すときに使用するプロトコルのバージョンを識別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2474-105">Because these protocols keep evolving, clients must identify the protocol version they use when calling specific nuget.org APIs.</span></span> <span data-ttu-id="b2474-106">これにより、nuget.org は古いクライアントに対して互換性のない方法で変更を加えることができます。</span><span class="sxs-lookup"><span data-stu-id="b2474-106">This allows nuget.org to introduce changes in a non-breaking way for the old clients.</span></span>

> [!Note]
> <span data-ttu-id="b2474-107">このページに記載されている Api は nuget.org に固有のものであり、他の NuGet サーバー実装でこれらの Api を導入することは期待されていません。</span><span class="sxs-lookup"><span data-stu-id="b2474-107">The APIs documented on this page are specific to nuget.org and there is no expectation for other NuGet server implementations to introduce these APIs.</span></span> 

<span data-ttu-id="b2474-108">NuGet エコシステム全体で広く実装されている NuGet API の詳細については、 [API の概要](overview.md)に関するトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2474-108">For information about the NuGet API implemented broadly across the NuGet ecosystem, see the [API overview](overview.md).</span></span>

<span data-ttu-id="b2474-109">このトピックでは、さまざまなプロトコルが存在する場合に、それらのプロトコルを示します。</span><span class="sxs-lookup"><span data-stu-id="b2474-109">This topic lists various protocols as and when they come to existence.</span></span>

## <a name="nuget-protocol-version-410"></a><span data-ttu-id="b2474-110">NuGet プロトコルバージョン4.1.0</span><span class="sxs-lookup"><span data-stu-id="b2474-110">NuGet protocol version 4.1.0</span></span>

<span data-ttu-id="b2474-111">4.1.0 プロトコルは、nuget.org 以外のサービスと対話するための検証スコープキーの使用法を指定し、nuget.org アカウントに対してパッケージを検証します。</span><span class="sxs-lookup"><span data-stu-id="b2474-111">The 4.1.0 protocol specifies usage of verify-scope keys to interact with services other than nuget.org, to validate a package against a nuget.org account.</span></span> <span data-ttu-id="b2474-112">`4.1.0`バージョン番号は不透明な文字列ですが、このプロトコルをサポートしている公式の NuGet クライアントの最初のバージョンと一致することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="b2474-112">Note that the `4.1.0` version number is an opaque string but happens to coincide with the first version of the official NuGet client that supported this protocol.</span></span>

<span data-ttu-id="b2474-113">検証によって、ユーザーが作成した API キーは nuget.org でのみ使用され、サードパーティのサービスからのその他の検証や検証は、1回限りの使用確認スコープのキーによって処理されます。</span><span class="sxs-lookup"><span data-stu-id="b2474-113">Validation ensures that the user-created API keys are used only with nuget.org, and that other verification or validation from a third-party service is handled through a one-time use verify-scope keys.</span></span> <span data-ttu-id="b2474-114">これらの検証スコープキーを使用して、パッケージが nuget.org の特定のユーザー (アカウント) に属していることを検証できます。</span><span class="sxs-lookup"><span data-stu-id="b2474-114">These verify-scope keys can be used to validate that the package belongs to a particular user (account) on nuget.org.</span></span>

### <a name="client-requirement"></a><span data-ttu-id="b2474-115">クライアントの要件</span><span class="sxs-lookup"><span data-stu-id="b2474-115">Client requirement</span></span>

<span data-ttu-id="b2474-116">クライアントは、API を呼び出して nuget.org にパッケージを **プッシュ** するときに、次のヘッダーを渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2474-116">Clients are required to pass the following header when they make API calls to **push** packages to nuget.org:</span></span>

```
X-NuGet-Protocol-Version: 4.1.0
```

<span data-ttu-id="b2474-117">ヘッダーのセマンティクスは似てい `X-NuGet-Client-Version` ますが、公式の NuGet クライアントでのみ使用されるように予約されています。</span><span class="sxs-lookup"><span data-stu-id="b2474-117">Note that the `X-NuGet-Client-Version` header has similar semantics but is reserved to only be used by the official NuGet client.</span></span> <span data-ttu-id="b2474-118">サードパーティのクライアントは、ヘッダーと値を使用する必要があり `X-NuGet-Protocol-Version` ます。</span><span class="sxs-lookup"><span data-stu-id="b2474-118">Third party clients should use the `X-NuGet-Protocol-Version` header and value.</span></span>

<span data-ttu-id="b2474-119">**プッシュ** プロトコル自体については、 [ `PackagePublish` リソース](package-publish-resource.md)のドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b2474-119">The **push** protocol itself is described in the documentation for the [`PackagePublish` resource](package-publish-resource.md).</span></span>

<span data-ttu-id="b2474-120">クライアントが外部サービスとやり取りし、パッケージが特定のユーザー (アカウント) に属しているかどうかを検証する必要がある場合、次のプロトコルを使用し、nuget.org からの API キーではなく、検証スコープのキーを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b2474-120">If a client interacts with external services and needs to validate whether a package belongs to a particular user (account), it should use the following protocol and use the verify-scope keys and not the API keys from nuget.org.</span></span>

### <a name="api-to-request-a-verify-scope-key"></a><span data-ttu-id="b2474-121">検証スコープキーを要求する API</span><span class="sxs-lookup"><span data-stu-id="b2474-121">API to request a verify-scope key</span></span>

<span data-ttu-id="b2474-122">この API は、nuget.org の作成者が所有しているパッケージを検証するための検証スコープキーを取得するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b2474-122">This API is used to get a verify-scope key for a nuget.org author to validate a package owned by him/her.</span></span>

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="b2474-123">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="b2474-123">Request parameters</span></span>

<span data-ttu-id="b2474-124">名前</span><span class="sxs-lookup"><span data-stu-id="b2474-124">Name</span></span>           | <span data-ttu-id="b2474-125">/</span><span class="sxs-lookup"><span data-stu-id="b2474-125">In</span></span>     | <span data-ttu-id="b2474-126">Type</span><span class="sxs-lookup"><span data-stu-id="b2474-126">Type</span></span>   | <span data-ttu-id="b2474-127">必須</span><span class="sxs-lookup"><span data-stu-id="b2474-127">Required</span></span> | <span data-ttu-id="b2474-128">Notes</span><span class="sxs-lookup"><span data-stu-id="b2474-128">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="b2474-129">ID</span><span class="sxs-lookup"><span data-stu-id="b2474-129">ID</span></span>             | <span data-ttu-id="b2474-130">URL</span><span class="sxs-lookup"><span data-stu-id="b2474-130">URL</span></span>    | <span data-ttu-id="b2474-131">string</span><span class="sxs-lookup"><span data-stu-id="b2474-131">string</span></span> | <span data-ttu-id="b2474-132">はい</span><span class="sxs-lookup"><span data-stu-id="b2474-132">yes</span></span>      | <span data-ttu-id="b2474-133">検証スコープキーが要求されているパッケージの識別子</span><span class="sxs-lookup"><span data-stu-id="b2474-133">The package identidier for which the verify scope key is requested</span></span>
<span data-ttu-id="b2474-134">VERSION</span><span class="sxs-lookup"><span data-stu-id="b2474-134">VERSION</span></span>        | <span data-ttu-id="b2474-135">URL</span><span class="sxs-lookup"><span data-stu-id="b2474-135">URL</span></span>    | <span data-ttu-id="b2474-136">string</span><span class="sxs-lookup"><span data-stu-id="b2474-136">string</span></span> | <span data-ttu-id="b2474-137">no</span><span class="sxs-lookup"><span data-stu-id="b2474-137">no</span></span>       | <span data-ttu-id="b2474-138">パッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="b2474-138">The package version</span></span>
<span data-ttu-id="b2474-139">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b2474-139">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b2474-140">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="b2474-140">Header</span></span> | <span data-ttu-id="b2474-141">string</span><span class="sxs-lookup"><span data-stu-id="b2474-141">string</span></span> | <span data-ttu-id="b2474-142">はい</span><span class="sxs-lookup"><span data-stu-id="b2474-142">yes</span></span>      | <span data-ttu-id="b2474-143">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。</span><span class="sxs-lookup"><span data-stu-id="b2474-143">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

#### <a name="response"></a><span data-ttu-id="b2474-144">応答</span><span class="sxs-lookup"><span data-stu-id="b2474-144">Response</span></span>

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a><span data-ttu-id="b2474-145">検証スコープキーを検証する API</span><span class="sxs-lookup"><span data-stu-id="b2474-145">API to verify the verify scope key</span></span>

<span data-ttu-id="b2474-146">この API は、nuget.org の作成者が所有するパッケージの検証スコープキーを検証するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b2474-146">This API is used to validate a verify-scope key for package owned by the nuget.org author.</span></span>

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a><span data-ttu-id="b2474-147">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="b2474-147">Request parameters</span></span>

<span data-ttu-id="b2474-148">名前</span><span class="sxs-lookup"><span data-stu-id="b2474-148">Name</span></span>           | <span data-ttu-id="b2474-149">/</span><span class="sxs-lookup"><span data-stu-id="b2474-149">In</span></span>     | <span data-ttu-id="b2474-150">Type</span><span class="sxs-lookup"><span data-stu-id="b2474-150">Type</span></span>   | <span data-ttu-id="b2474-151">必須</span><span class="sxs-lookup"><span data-stu-id="b2474-151">Required</span></span> | <span data-ttu-id="b2474-152">Notes</span><span class="sxs-lookup"><span data-stu-id="b2474-152">Notes</span></span>
-------------  | ------ | ------ | -------- | -----
<span data-ttu-id="b2474-153">ID</span><span class="sxs-lookup"><span data-stu-id="b2474-153">ID</span></span>             | <span data-ttu-id="b2474-154">URL</span><span class="sxs-lookup"><span data-stu-id="b2474-154">URL</span></span>    | <span data-ttu-id="b2474-155">string</span><span class="sxs-lookup"><span data-stu-id="b2474-155">string</span></span> | <span data-ttu-id="b2474-156">はい</span><span class="sxs-lookup"><span data-stu-id="b2474-156">yes</span></span>      | <span data-ttu-id="b2474-157">スコープの検証キーが要求されたパッケージの識別子</span><span class="sxs-lookup"><span data-stu-id="b2474-157">The package identifier for which the verify scope key is requested</span></span>
<span data-ttu-id="b2474-158">VERSION</span><span class="sxs-lookup"><span data-stu-id="b2474-158">VERSION</span></span>        | <span data-ttu-id="b2474-159">URL</span><span class="sxs-lookup"><span data-stu-id="b2474-159">URL</span></span>    | <span data-ttu-id="b2474-160">string</span><span class="sxs-lookup"><span data-stu-id="b2474-160">string</span></span> | <span data-ttu-id="b2474-161">no</span><span class="sxs-lookup"><span data-stu-id="b2474-161">no</span></span>       | <span data-ttu-id="b2474-162">パッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="b2474-162">The package version</span></span>
<span data-ttu-id="b2474-163">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="b2474-163">X-NuGet-ApiKey</span></span> | <span data-ttu-id="b2474-164">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="b2474-164">Header</span></span> | <span data-ttu-id="b2474-165">string</span><span class="sxs-lookup"><span data-stu-id="b2474-165">string</span></span> | <span data-ttu-id="b2474-166">はい</span><span class="sxs-lookup"><span data-stu-id="b2474-166">yes</span></span>      | <span data-ttu-id="b2474-167">たとえば、`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}` のように指定します。</span><span class="sxs-lookup"><span data-stu-id="b2474-167">For example, `X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`</span></span>

> [!Note]
> <span data-ttu-id="b2474-168">この検証スコープ API キーは、1日の時間に有効期限が切れるか、最初の使用時に、いずれか早い方で期限切れになります。</span><span class="sxs-lookup"><span data-stu-id="b2474-168">This verify scope API key expires in a day's time or on first use, whichever occurs first.</span></span>

#### <a name="response"></a><span data-ttu-id="b2474-169">応答</span><span class="sxs-lookup"><span data-stu-id="b2474-169">Response</span></span>

<span data-ttu-id="b2474-170">状態コード</span><span class="sxs-lookup"><span data-stu-id="b2474-170">Status Code</span></span> | <span data-ttu-id="b2474-171">意味</span><span class="sxs-lookup"><span data-stu-id="b2474-171">Meaning</span></span>
----------- | -------
<span data-ttu-id="b2474-172">200</span><span class="sxs-lookup"><span data-stu-id="b2474-172">200</span></span>         | <span data-ttu-id="b2474-173">API キーが有効です</span><span class="sxs-lookup"><span data-stu-id="b2474-173">The API key is valid</span></span>
<span data-ttu-id="b2474-174">403</span><span class="sxs-lookup"><span data-stu-id="b2474-174">403</span></span>         | <span data-ttu-id="b2474-175">API キーが無効であるか、パッケージに対するプッシュが許可されていません</span><span class="sxs-lookup"><span data-stu-id="b2474-175">The API key is invalid or not authorized to push against the package</span></span>
<span data-ttu-id="b2474-176">404</span><span class="sxs-lookup"><span data-stu-id="b2474-176">404</span></span>         | <span data-ttu-id="b2474-177">とによって参照 `ID` されるパッケージ `VERSION` (省略可能) は存在しません</span><span class="sxs-lookup"><span data-stu-id="b2474-177">The package referred to by `ID` and `VERSION` (optional) does not exist</span></span>
