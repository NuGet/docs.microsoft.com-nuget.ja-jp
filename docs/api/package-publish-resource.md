---
title: プッシュと削除、NuGet API
description: 発行サービスを使用すると、クライアントは新しいパッケージを公開したり、既存のパッケージを一覧から削除または削除したりできます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773916"
---
# <a name="push-and-delete"></a><span data-ttu-id="23c85-103">プッシュと削除</span><span class="sxs-lookup"><span data-stu-id="23c85-103">Push and Delete</span></span>

<span data-ttu-id="23c85-104">サーバーの実装に応じてプッシュ、削除 (または一覧から削除) を実行し、NuGet V3 API を使用してパッケージの一覧を再設定することができます。</span><span class="sxs-lookup"><span data-stu-id="23c85-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="23c85-105">これらの操作は、 `PackagePublish` [サービスインデックス](service-index.md)で検出されたリソースに基づいています。</span><span class="sxs-lookup"><span data-stu-id="23c85-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="23c85-106">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="23c85-106">Versioning</span></span>

<span data-ttu-id="23c85-107">次の `@type` 値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="23c85-107">The following `@type` value is used:</span></span>

<span data-ttu-id="23c85-108">@type 値</span><span class="sxs-lookup"><span data-stu-id="23c85-108">@type value</span></span>          | <span data-ttu-id="23c85-109">Notes</span><span class="sxs-lookup"><span data-stu-id="23c85-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="23c85-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="23c85-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="23c85-111">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="23c85-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="23c85-112">ベース URL</span><span class="sxs-lookup"><span data-stu-id="23c85-112">Base URL</span></span>

<span data-ttu-id="23c85-113">次の Api のベース URL は、 `@id` `PackagePublish/2.0.0` パッケージソースの [サービスインデックス](service-index.md)に含まれるリソースのプロパティの値です。</span><span class="sxs-lookup"><span data-stu-id="23c85-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="23c85-114">次のドキュメントでは、nuget の URL が使用されます。</span><span class="sxs-lookup"><span data-stu-id="23c85-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="23c85-115">`https://www.nuget.org/api/v2/package` `@id` サービスインデックスで見つかった値のプレースホルダーとして考慮します。</span><span class="sxs-lookup"><span data-stu-id="23c85-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="23c85-116">この URL は、プロトコルが同じであるため、従来の V2 プッシュエンドポイントと同じ場所を指していることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="23c85-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="23c85-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="23c85-117">HTTP methods</span></span>

<span data-ttu-id="23c85-118">`PUT`、、 `POST` および `DELETE` HTTP メソッドは、このリソースでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="23c85-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="23c85-119">各エンドポイントでサポートされるメソッドについては、以下を参照してください。</span><span class="sxs-lookup"><span data-stu-id="23c85-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="23c85-120">パッケージをプッシュする</span><span class="sxs-lookup"><span data-stu-id="23c85-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="23c85-121">nuget.org には、プッシュエンドポイントと対話するための [追加の要件](NuGet-Protocols.md) があります。</span><span class="sxs-lookup"><span data-stu-id="23c85-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="23c85-122">nuget.org では、次の API を使用した新しいパッケージのプッシュがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="23c85-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="23c85-123">指定された ID とバージョンのパッケージが既に存在する場合、nuget.org はプッシュを拒否します。</span><span class="sxs-lookup"><span data-stu-id="23c85-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="23c85-124">他のパッケージソースでは、既存のパッケージの置換がサポートされている場合があります。</span><span class="sxs-lookup"><span data-stu-id="23c85-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="23c85-125">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="23c85-125">Request parameters</span></span>

<span data-ttu-id="23c85-126">名前</span><span class="sxs-lookup"><span data-stu-id="23c85-126">Name</span></span>           | <span data-ttu-id="23c85-127">/</span><span class="sxs-lookup"><span data-stu-id="23c85-127">In</span></span>     | <span data-ttu-id="23c85-128">Type</span><span class="sxs-lookup"><span data-stu-id="23c85-128">Type</span></span>   | <span data-ttu-id="23c85-129">必須</span><span class="sxs-lookup"><span data-stu-id="23c85-129">Required</span></span> | <span data-ttu-id="23c85-130">Notes</span><span class="sxs-lookup"><span data-stu-id="23c85-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="23c85-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="23c85-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="23c85-132">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="23c85-132">Header</span></span> | <span data-ttu-id="23c85-133">string</span><span class="sxs-lookup"><span data-stu-id="23c85-133">string</span></span> | <span data-ttu-id="23c85-134">はい</span><span class="sxs-lookup"><span data-stu-id="23c85-134">yes</span></span>      | <span data-ttu-id="23c85-135">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。</span><span class="sxs-lookup"><span data-stu-id="23c85-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="23c85-136">API キーは、ユーザーによってパッケージソースから得られた非透過文字列であり、クライアントに構成されています。</span><span class="sxs-lookup"><span data-stu-id="23c85-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="23c85-137">特定の文字列形式は必須ではありませんが、API キーの長さは HTTP ヘッダー値に対して妥当なサイズを超えることはできません。</span><span class="sxs-lookup"><span data-stu-id="23c85-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="23c85-138">要求本文</span><span class="sxs-lookup"><span data-stu-id="23c85-138">Request body</span></span>

<span data-ttu-id="23c85-139">要求本文は次の形式にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="23c85-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="23c85-140">マルチパート フォーム データ</span><span class="sxs-lookup"><span data-stu-id="23c85-140">Multipart form data</span></span>

<span data-ttu-id="23c85-141">要求ヘッダーはで、 `Content-Type` `multipart/form-data` 要求本文の最初の項目は、の未加工のバイトです。 nupkg プッシュされます。</span><span class="sxs-lookup"><span data-stu-id="23c85-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="23c85-142">マルチパート本体の後続の項目は無視されます。</span><span class="sxs-lookup"><span data-stu-id="23c85-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="23c85-143">ファイル名またはマルチパート項目のその他のヘッダーは無視されます。</span><span class="sxs-lookup"><span data-stu-id="23c85-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="23c85-144">応答</span><span class="sxs-lookup"><span data-stu-id="23c85-144">Response</span></span>

<span data-ttu-id="23c85-145">状態コード</span><span class="sxs-lookup"><span data-stu-id="23c85-145">Status Code</span></span> | <span data-ttu-id="23c85-146">意味</span><span class="sxs-lookup"><span data-stu-id="23c85-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="23c85-147">201、202</span><span class="sxs-lookup"><span data-stu-id="23c85-147">201, 202</span></span>    | <span data-ttu-id="23c85-148">パッケージが正常にプッシュされました</span><span class="sxs-lookup"><span data-stu-id="23c85-148">The package was successfully pushed</span></span>
<span data-ttu-id="23c85-149">400</span><span class="sxs-lookup"><span data-stu-id="23c85-149">400</span></span>         | <span data-ttu-id="23c85-150">指定されたパッケージは無効です</span><span class="sxs-lookup"><span data-stu-id="23c85-150">The provided package is invalid</span></span>
<span data-ttu-id="23c85-151">409</span><span class="sxs-lookup"><span data-stu-id="23c85-151">409</span></span>         | <span data-ttu-id="23c85-152">指定された ID とバージョンのパッケージは既に存在します</span><span class="sxs-lookup"><span data-stu-id="23c85-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="23c85-153">サーバーの実装は、パッケージが正常にプッシュされたときに返される成功状態コードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="23c85-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="23c85-154">パッケージを削除する</span><span class="sxs-lookup"><span data-stu-id="23c85-154">Delete a package</span></span>

<span data-ttu-id="23c85-155">nuget.org は、"一覧から削除" としてパッケージの削除要求を解釈します。</span><span class="sxs-lookup"><span data-stu-id="23c85-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="23c85-156">つまり、パッケージの既存のコンシューマーはパッケージを引き続き使用できますが、パッケージは検索結果または web インターフェイスに表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="23c85-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="23c85-157">このプラクティスの詳細については、「 [削除されたパッケージ](../nuget-org/policies/deleting-packages.md) ポリシー」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="23c85-157">For more information about this practice, see the [Deleted Packages](../nuget-org/policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="23c85-158">その他のサーバー実装では、この信号をハード削除、論理的な削除、または一覧から削除として解釈できます。</span><span class="sxs-lookup"><span data-stu-id="23c85-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="23c85-159">たとえば、Nuget.exe (以前の V2 API のみをサポートするサーバー実装) は、この要求を構成オプションに基づいて一覧から削除またはハード削除として処理することをサポートしています[。](https://www.nuget.org/packages/NuGet.Server)</span><span class="sxs-lookup"><span data-stu-id="23c85-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="23c85-160">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="23c85-160">Request parameters</span></span>

<span data-ttu-id="23c85-161">名前</span><span class="sxs-lookup"><span data-stu-id="23c85-161">Name</span></span>           | <span data-ttu-id="23c85-162">/</span><span class="sxs-lookup"><span data-stu-id="23c85-162">In</span></span>     | <span data-ttu-id="23c85-163">Type</span><span class="sxs-lookup"><span data-stu-id="23c85-163">Type</span></span>   | <span data-ttu-id="23c85-164">必須</span><span class="sxs-lookup"><span data-stu-id="23c85-164">Required</span></span> | <span data-ttu-id="23c85-165">Notes</span><span class="sxs-lookup"><span data-stu-id="23c85-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="23c85-166">ID</span><span class="sxs-lookup"><span data-stu-id="23c85-166">ID</span></span>             | <span data-ttu-id="23c85-167">URL</span><span class="sxs-lookup"><span data-stu-id="23c85-167">URL</span></span>    | <span data-ttu-id="23c85-168">string</span><span class="sxs-lookup"><span data-stu-id="23c85-168">string</span></span> | <span data-ttu-id="23c85-169">はい</span><span class="sxs-lookup"><span data-stu-id="23c85-169">yes</span></span>      | <span data-ttu-id="23c85-170">削除するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="23c85-170">The ID of the package to delete</span></span>
<span data-ttu-id="23c85-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="23c85-171">VERSION</span></span>        | <span data-ttu-id="23c85-172">URL</span><span class="sxs-lookup"><span data-stu-id="23c85-172">URL</span></span>    | <span data-ttu-id="23c85-173">string</span><span class="sxs-lookup"><span data-stu-id="23c85-173">string</span></span> | <span data-ttu-id="23c85-174">はい</span><span class="sxs-lookup"><span data-stu-id="23c85-174">yes</span></span>      | <span data-ttu-id="23c85-175">削除するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="23c85-175">The version of the package to delete</span></span>
<span data-ttu-id="23c85-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="23c85-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="23c85-177">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="23c85-177">Header</span></span> | <span data-ttu-id="23c85-178">string</span><span class="sxs-lookup"><span data-stu-id="23c85-178">string</span></span> | <span data-ttu-id="23c85-179">はい</span><span class="sxs-lookup"><span data-stu-id="23c85-179">yes</span></span>      | <span data-ttu-id="23c85-180">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。</span><span class="sxs-lookup"><span data-stu-id="23c85-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="23c85-181">応答</span><span class="sxs-lookup"><span data-stu-id="23c85-181">Response</span></span>

<span data-ttu-id="23c85-182">状態コード</span><span class="sxs-lookup"><span data-stu-id="23c85-182">Status Code</span></span> | <span data-ttu-id="23c85-183">意味</span><span class="sxs-lookup"><span data-stu-id="23c85-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="23c85-184">204</span><span class="sxs-lookup"><span data-stu-id="23c85-184">204</span></span>         | <span data-ttu-id="23c85-185">パッケージが削除されました</span><span class="sxs-lookup"><span data-stu-id="23c85-185">The package was deleted</span></span>
<span data-ttu-id="23c85-186">404</span><span class="sxs-lookup"><span data-stu-id="23c85-186">404</span></span>         | <span data-ttu-id="23c85-187">指定された `ID` と `VERSION` 存在するパッケージはありません</span><span class="sxs-lookup"><span data-stu-id="23c85-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="23c85-188">パッケージを一覧に再記載する</span><span class="sxs-lookup"><span data-stu-id="23c85-188">Relist a package</span></span>

<span data-ttu-id="23c85-189">パッケージが一覧から削除されている場合は、"relist" エンドポイントを使用して、そのパッケージが検索結果に再び表示されるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="23c85-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="23c85-190">このエンドポイントには、 [delete (一覧から削除) エンドポイント](#delete-a-package) と同じ図形がありますが、 `POST` メソッドの代わりに HTTP メソッドが使用され `DELETE` ます。</span><span class="sxs-lookup"><span data-stu-id="23c85-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="23c85-191">パッケージが既に表示されている場合でも、要求は成功します。</span><span class="sxs-lookup"><span data-stu-id="23c85-191">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="23c85-192">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="23c85-192">Request parameters</span></span>

<span data-ttu-id="23c85-193">名前</span><span class="sxs-lookup"><span data-stu-id="23c85-193">Name</span></span>           | <span data-ttu-id="23c85-194">/</span><span class="sxs-lookup"><span data-stu-id="23c85-194">In</span></span>     | <span data-ttu-id="23c85-195">Type</span><span class="sxs-lookup"><span data-stu-id="23c85-195">Type</span></span>   | <span data-ttu-id="23c85-196">必須</span><span class="sxs-lookup"><span data-stu-id="23c85-196">Required</span></span> | <span data-ttu-id="23c85-197">Notes</span><span class="sxs-lookup"><span data-stu-id="23c85-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="23c85-198">ID</span><span class="sxs-lookup"><span data-stu-id="23c85-198">ID</span></span>             | <span data-ttu-id="23c85-199">URL</span><span class="sxs-lookup"><span data-stu-id="23c85-199">URL</span></span>    | <span data-ttu-id="23c85-200">string</span><span class="sxs-lookup"><span data-stu-id="23c85-200">string</span></span> | <span data-ttu-id="23c85-201">はい</span><span class="sxs-lookup"><span data-stu-id="23c85-201">yes</span></span>      | <span data-ttu-id="23c85-202">再一覧表示するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="23c85-202">The ID of the package to relist</span></span>
<span data-ttu-id="23c85-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="23c85-203">VERSION</span></span>        | <span data-ttu-id="23c85-204">URL</span><span class="sxs-lookup"><span data-stu-id="23c85-204">URL</span></span>    | <span data-ttu-id="23c85-205">string</span><span class="sxs-lookup"><span data-stu-id="23c85-205">string</span></span> | <span data-ttu-id="23c85-206">はい</span><span class="sxs-lookup"><span data-stu-id="23c85-206">yes</span></span>      | <span data-ttu-id="23c85-207">再一覧表示するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="23c85-207">The version of the package to relist</span></span>
<span data-ttu-id="23c85-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="23c85-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="23c85-209">ヘッダー</span><span class="sxs-lookup"><span data-stu-id="23c85-209">Header</span></span> | <span data-ttu-id="23c85-210">string</span><span class="sxs-lookup"><span data-stu-id="23c85-210">string</span></span> | <span data-ttu-id="23c85-211">はい</span><span class="sxs-lookup"><span data-stu-id="23c85-211">yes</span></span>      | <span data-ttu-id="23c85-212">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。</span><span class="sxs-lookup"><span data-stu-id="23c85-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="23c85-213">応答</span><span class="sxs-lookup"><span data-stu-id="23c85-213">Response</span></span>

<span data-ttu-id="23c85-214">状態コード</span><span class="sxs-lookup"><span data-stu-id="23c85-214">Status Code</span></span> | <span data-ttu-id="23c85-215">意味</span><span class="sxs-lookup"><span data-stu-id="23c85-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="23c85-216">200</span><span class="sxs-lookup"><span data-stu-id="23c85-216">200</span></span>         | <span data-ttu-id="23c85-217">パッケージが表示されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="23c85-217">The package is now listed</span></span>
<span data-ttu-id="23c85-218">404</span><span class="sxs-lookup"><span data-stu-id="23c85-218">404</span></span>         | <span data-ttu-id="23c85-219">指定された `ID` と `VERSION` 存在するパッケージはありません</span><span class="sxs-lookup"><span data-stu-id="23c85-219">No package with the provided `ID` and `VERSION` exists</span></span>
