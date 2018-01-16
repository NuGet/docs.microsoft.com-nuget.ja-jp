---
title: "プッシュ モードと NuGet API を削除します |。Microsoft ドキュメント"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "発行サービスは、クライアントが新しいパッケージを公開および非公開または既存のパッケージを削除できます。"
keywords: "NuGet API プッシュ パッケージ、パッケージを削除する NuGet API、NuGet API は、パッケージ、NuGet API アップロード パッケージを非公開、API の NuGet パッケージの作成"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 5fbcd82b09ebd56ae21103640e7c39b482059525
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="9aa27-104">プッシュ モードと削除</span><span class="sxs-lookup"><span data-stu-id="9aa27-104">Push and Delete</span></span>

<span data-ttu-id="9aa27-105">プッシュ、削除 (またはサーバーの実装によって、非公開キーを押す)、可能であれば、NuGet V3 API を使用してパッケージを relist とします。</span><span class="sxs-lookup"><span data-stu-id="9aa27-105">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="9aa27-106">これらの操作は無効の基づいて、`PackagePublish`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="9aa27-106">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="9aa27-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="9aa27-107">Versioning</span></span>

<span data-ttu-id="9aa27-108">次`@type`値を使用します。</span><span class="sxs-lookup"><span data-stu-id="9aa27-108">The following `@type` value is used:</span></span>

<span data-ttu-id="9aa27-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="9aa27-109">@type value</span></span>          | <span data-ttu-id="9aa27-110">メモ</span><span class="sxs-lookup"><span data-stu-id="9aa27-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="9aa27-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="9aa27-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="9aa27-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="9aa27-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="9aa27-113">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="9aa27-113">Base URL</span></span>

<span data-ttu-id="9aa27-114">次の Api のベース URL の値、`@id`のプロパティ、`PackagePublish/2.0.0`パッケージ ソースのリソース[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="9aa27-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="9aa27-115">次のドキュメントでは、nuget.org の URL が使用されます。</span><span class="sxs-lookup"><span data-stu-id="9aa27-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="9aa27-116">検討`https://www.nuget.org/api/v2/package`のプレース ホルダーとして、`@id`サービス インデックス内の値で見つかった。</span><span class="sxs-lookup"><span data-stu-id="9aa27-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="9aa27-117">プロトコルが同じであるために、この URL がレガシ V2 プッシュ エンドポイントと同じ場所を指していることを注意してください。</span><span class="sxs-lookup"><span data-stu-id="9aa27-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9aa27-118">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="9aa27-118">HTTP methods</span></span>

<span data-ttu-id="9aa27-119">`PUT`、`POST`と`DELETE`HTTP メソッドは、このリソースでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="9aa27-119">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="9aa27-120">各エンドポイントでは、どのメソッドがサポートされている、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="9aa27-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="9aa27-121">パッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="9aa27-121">Push a package</span></span>

> [!Note]
> <span data-ttu-id="9aa27-122">nuget.org が[追加要件](NuGet-Protocols.md)プッシュ エンドポイントと対話するためです。</span><span class="sxs-lookup"><span data-stu-id="9aa27-122">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="9aa27-123">nuget.org には、次の API を使用してプッシュの新しいパッケージがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="9aa27-123">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="9aa27-124">指定された ID とバージョンのパッケージが既に存在する場合、nuget.org は、プッシュを拒否します。</span><span class="sxs-lookup"><span data-stu-id="9aa27-124">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="9aa27-125">他のパッケージ ソースでは、既存のパッケージの交換をサポートできます。</span><span class="sxs-lookup"><span data-stu-id="9aa27-125">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="9aa27-126">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="9aa27-126">Request parameters</span></span>

<span data-ttu-id="9aa27-127">name</span><span class="sxs-lookup"><span data-stu-id="9aa27-127">Name</span></span>           | <span data-ttu-id="9aa27-128">イン</span><span class="sxs-lookup"><span data-stu-id="9aa27-128">In</span></span>     | <span data-ttu-id="9aa27-129">型</span><span class="sxs-lookup"><span data-stu-id="9aa27-129">Type</span></span>   | <span data-ttu-id="9aa27-130">必須</span><span class="sxs-lookup"><span data-stu-id="9aa27-130">Required</span></span> | <span data-ttu-id="9aa27-131">メモ</span><span class="sxs-lookup"><span data-stu-id="9aa27-131">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9aa27-132">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9aa27-132">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9aa27-133">Header</span><span class="sxs-lookup"><span data-stu-id="9aa27-133">Header</span></span> | <span data-ttu-id="9aa27-134">string</span><span class="sxs-lookup"><span data-stu-id="9aa27-134">string</span></span> | <span data-ttu-id="9aa27-135">可</span><span class="sxs-lookup"><span data-stu-id="9aa27-135">yes</span></span>      | <span data-ttu-id="9aa27-136">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9aa27-136">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="9aa27-137">API キーは、ユーザーがパッケージ ソースから取得し、クライアントに構成されている非透過の文字列です。</span><span class="sxs-lookup"><span data-stu-id="9aa27-137">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="9aa27-138">特定の文字列形式が必須でありませんが、API キーの長さは、適切な HTTP ヘッダーの値のサイズを超えない必要があります。</span><span class="sxs-lookup"><span data-stu-id="9aa27-138">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="9aa27-139">要求本文</span><span class="sxs-lookup"><span data-stu-id="9aa27-139">Request body</span></span>

<span data-ttu-id="9aa27-140">要求本文で、次の形式でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="9aa27-140">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="9aa27-141">マルチパート フォーム データ</span><span class="sxs-lookup"><span data-stu-id="9aa27-141">Multipart form data</span></span>

<span data-ttu-id="9aa27-142">要求ヘッダー`Content-Type`は`multipart/form-data`要求本文の最初の項目は、これはプッシュされる .nupkg の生のバイトとします。</span><span class="sxs-lookup"><span data-stu-id="9aa27-142">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="9aa27-143">マルチパート ボディ内の後続の項目は無視されます。</span><span class="sxs-lookup"><span data-stu-id="9aa27-143">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="9aa27-144">ファイルの名前またはマルチパートの項目の他のヘッダーが無視されます。</span><span class="sxs-lookup"><span data-stu-id="9aa27-144">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="9aa27-145">応答</span><span class="sxs-lookup"><span data-stu-id="9aa27-145">Response</span></span>

<span data-ttu-id="9aa27-146">状態コード</span><span class="sxs-lookup"><span data-stu-id="9aa27-146">Status Code</span></span> | <span data-ttu-id="9aa27-147">説明</span><span class="sxs-lookup"><span data-stu-id="9aa27-147">Meaning</span></span>
----------- | -------
<span data-ttu-id="9aa27-148">201, 202</span><span class="sxs-lookup"><span data-stu-id="9aa27-148">201, 202</span></span>    | <span data-ttu-id="9aa27-149">パッケージが正常にプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="9aa27-149">The package was successfully pushed</span></span>
<span data-ttu-id="9aa27-150">400</span><span class="sxs-lookup"><span data-stu-id="9aa27-150">400</span></span>         | <span data-ttu-id="9aa27-151">指定したパッケージが正しくありません。</span><span class="sxs-lookup"><span data-stu-id="9aa27-151">The provided package is invalid</span></span>
<span data-ttu-id="9aa27-152">409</span><span class="sxs-lookup"><span data-stu-id="9aa27-152">409</span></span>         | <span data-ttu-id="9aa27-153">指定された ID とバージョンを使用してパッケージが既に存在します。</span><span class="sxs-lookup"><span data-stu-id="9aa27-153">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="9aa27-154">サーバーの実装は、パッケージが正常にプッシュされたときに返される成功ステータス コードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="9aa27-154">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="9aa27-155">パッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="9aa27-155">Delete a package</span></span>

<span data-ttu-id="9aa27-156">nuget.org としてパッケージの削除要求では、解釈「非公開」にします。</span><span class="sxs-lookup"><span data-stu-id="9aa27-156">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="9aa27-157">つまり、パッケージは、パッケージの既存のコンシューマーを引き続き使用できますが、パッケージで検索結果または web インターフェイスが表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="9aa27-157">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="9aa27-158">この方法の詳細については、次を参照してください。、[パッケージの削除](../policies/deleting-packages.md)ポリシー。</span><span class="sxs-lookup"><span data-stu-id="9aa27-158">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="9aa27-159">その他のサーバーの実装では、ハード削除としてこの信号を解釈し、論理削除、または、非公開に解放されます。</span><span class="sxs-lookup"><span data-stu-id="9aa27-159">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="9aa27-160">たとえば、 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (するサーバーの実装だけ古い V2 API をサポート)、unlist または構成オプションに基づくハード delete のいずれかとしてこの要求の処理をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="9aa27-160">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="9aa27-161">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="9aa27-161">Request parameters</span></span>

<span data-ttu-id="9aa27-162">name</span><span class="sxs-lookup"><span data-stu-id="9aa27-162">Name</span></span>           | <span data-ttu-id="9aa27-163">イン</span><span class="sxs-lookup"><span data-stu-id="9aa27-163">In</span></span>     | <span data-ttu-id="9aa27-164">型</span><span class="sxs-lookup"><span data-stu-id="9aa27-164">Type</span></span>   | <span data-ttu-id="9aa27-165">必須</span><span class="sxs-lookup"><span data-stu-id="9aa27-165">Required</span></span> | <span data-ttu-id="9aa27-166">メモ</span><span class="sxs-lookup"><span data-stu-id="9aa27-166">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9aa27-167">ID</span><span class="sxs-lookup"><span data-stu-id="9aa27-167">ID</span></span>             | <span data-ttu-id="9aa27-168">URL</span><span class="sxs-lookup"><span data-stu-id="9aa27-168">URL</span></span>    | <span data-ttu-id="9aa27-169">string</span><span class="sxs-lookup"><span data-stu-id="9aa27-169">string</span></span> | <span data-ttu-id="9aa27-170">可</span><span class="sxs-lookup"><span data-stu-id="9aa27-170">yes</span></span>      | <span data-ttu-id="9aa27-171">削除するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="9aa27-171">The ID of the package to delete</span></span>
<span data-ttu-id="9aa27-172">VERSION</span><span class="sxs-lookup"><span data-stu-id="9aa27-172">VERSION</span></span>        | <span data-ttu-id="9aa27-173">URL</span><span class="sxs-lookup"><span data-stu-id="9aa27-173">URL</span></span>    | <span data-ttu-id="9aa27-174">string</span><span class="sxs-lookup"><span data-stu-id="9aa27-174">string</span></span> | <span data-ttu-id="9aa27-175">可</span><span class="sxs-lookup"><span data-stu-id="9aa27-175">yes</span></span>      | <span data-ttu-id="9aa27-176">削除するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="9aa27-176">The version of the package to delete</span></span>
<span data-ttu-id="9aa27-177">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9aa27-177">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9aa27-178">Header</span><span class="sxs-lookup"><span data-stu-id="9aa27-178">Header</span></span> | <span data-ttu-id="9aa27-179">string</span><span class="sxs-lookup"><span data-stu-id="9aa27-179">string</span></span> | <span data-ttu-id="9aa27-180">可</span><span class="sxs-lookup"><span data-stu-id="9aa27-180">yes</span></span>      | <span data-ttu-id="9aa27-181">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9aa27-181">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="9aa27-182">応答</span><span class="sxs-lookup"><span data-stu-id="9aa27-182">Response</span></span>

<span data-ttu-id="9aa27-183">状態コード</span><span class="sxs-lookup"><span data-stu-id="9aa27-183">Status Code</span></span> | <span data-ttu-id="9aa27-184">説明</span><span class="sxs-lookup"><span data-stu-id="9aa27-184">Meaning</span></span>
----------- | -------
<span data-ttu-id="9aa27-185">204</span><span class="sxs-lookup"><span data-stu-id="9aa27-185">204</span></span>         | <span data-ttu-id="9aa27-186">パッケージが削除されました</span><span class="sxs-lookup"><span data-stu-id="9aa27-186">The package was deleted</span></span>
<span data-ttu-id="9aa27-187">404</span><span class="sxs-lookup"><span data-stu-id="9aa27-187">404</span></span>         | <span data-ttu-id="9aa27-188">指定されたパッケージに含まれない`ID`と`VERSION`が存在します。</span><span class="sxs-lookup"><span data-stu-id="9aa27-188">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="9aa27-189">パッケージを relist します。</span><span class="sxs-lookup"><span data-stu-id="9aa27-189">Relist a package</span></span>

<span data-ttu-id="9aa27-190">パッケージが一覧にない場合は、そのパッケージを"relist"のエンドポイントを使用して検索結果にもう一度表示することができます。</span><span class="sxs-lookup"><span data-stu-id="9aa27-190">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="9aa27-191">このエンドポイントと同じ形には、[削除 (非公開) エンドポイント](#delete-a-package)が使用して、 `POST` HTTP メソッドの代わりに、`DELETE`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="9aa27-191">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="9aa27-192">パッケージが既に表示されている場合でも、要求は成功します。</span><span class="sxs-lookup"><span data-stu-id="9aa27-192">If the package is already listed, the request still succeeds.</span></span>

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="9aa27-193">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="9aa27-193">Request parameters</span></span>

<span data-ttu-id="9aa27-194">name</span><span class="sxs-lookup"><span data-stu-id="9aa27-194">Name</span></span>           | <span data-ttu-id="9aa27-195">イン</span><span class="sxs-lookup"><span data-stu-id="9aa27-195">In</span></span>     | <span data-ttu-id="9aa27-196">型</span><span class="sxs-lookup"><span data-stu-id="9aa27-196">Type</span></span>   | <span data-ttu-id="9aa27-197">必須</span><span class="sxs-lookup"><span data-stu-id="9aa27-197">Required</span></span> | <span data-ttu-id="9aa27-198">メモ</span><span class="sxs-lookup"><span data-stu-id="9aa27-198">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="9aa27-199">ID</span><span class="sxs-lookup"><span data-stu-id="9aa27-199">ID</span></span>             | <span data-ttu-id="9aa27-200">URL</span><span class="sxs-lookup"><span data-stu-id="9aa27-200">URL</span></span>    | <span data-ttu-id="9aa27-201">string</span><span class="sxs-lookup"><span data-stu-id="9aa27-201">string</span></span> | <span data-ttu-id="9aa27-202">可</span><span class="sxs-lookup"><span data-stu-id="9aa27-202">yes</span></span>      | <span data-ttu-id="9aa27-203">Relist するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="9aa27-203">The ID of the package to relist</span></span>
<span data-ttu-id="9aa27-204">VERSION</span><span class="sxs-lookup"><span data-stu-id="9aa27-204">VERSION</span></span>        | <span data-ttu-id="9aa27-205">URL</span><span class="sxs-lookup"><span data-stu-id="9aa27-205">URL</span></span>    | <span data-ttu-id="9aa27-206">string</span><span class="sxs-lookup"><span data-stu-id="9aa27-206">string</span></span> | <span data-ttu-id="9aa27-207">可</span><span class="sxs-lookup"><span data-stu-id="9aa27-207">yes</span></span>      | <span data-ttu-id="9aa27-208">Relist するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="9aa27-208">The version of the package to relist</span></span>
<span data-ttu-id="9aa27-209">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="9aa27-209">X-NuGet-ApiKey</span></span> | <span data-ttu-id="9aa27-210">Header</span><span class="sxs-lookup"><span data-stu-id="9aa27-210">Header</span></span> | <span data-ttu-id="9aa27-211">string</span><span class="sxs-lookup"><span data-stu-id="9aa27-211">string</span></span> | <span data-ttu-id="9aa27-212">可</span><span class="sxs-lookup"><span data-stu-id="9aa27-212">yes</span></span>      | <span data-ttu-id="9aa27-213">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="9aa27-213">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="9aa27-214">応答</span><span class="sxs-lookup"><span data-stu-id="9aa27-214">Response</span></span>

<span data-ttu-id="9aa27-215">状態コード</span><span class="sxs-lookup"><span data-stu-id="9aa27-215">Status Code</span></span> | <span data-ttu-id="9aa27-216">説明</span><span class="sxs-lookup"><span data-stu-id="9aa27-216">Meaning</span></span>
----------- | -------
<span data-ttu-id="9aa27-217">200</span><span class="sxs-lookup"><span data-stu-id="9aa27-217">200</span></span>         | <span data-ttu-id="9aa27-218">パッケージが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="9aa27-218">The package is now listed</span></span>
<span data-ttu-id="9aa27-219">404</span><span class="sxs-lookup"><span data-stu-id="9aa27-219">404</span></span>         | <span data-ttu-id="9aa27-220">指定されたパッケージに含まれない`ID`と`VERSION`が存在します。</span><span class="sxs-lookup"><span data-stu-id="9aa27-220">No package with the provided `ID` and `VERSION` exists</span></span>
