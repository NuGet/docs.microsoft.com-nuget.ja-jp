---
title: プッシュ モードと NuGet API を削除します。
description: 発行サービスは、クライアントが新しいパッケージを公開および非公開または既存のパッケージを削除できます。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 911c8238624f806b1fbb5c7938d02b6bdfbd8614
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="push-and-delete"></a><span data-ttu-id="f1f66-103">プッシュ モードと削除</span><span class="sxs-lookup"><span data-stu-id="f1f66-103">Push and Delete</span></span>

<span data-ttu-id="f1f66-104">プッシュ、削除 (またはサーバーの実装によって、非公開キーを押す)、可能であれば、NuGet V3 API を使用してパッケージを relist とします。</span><span class="sxs-lookup"><span data-stu-id="f1f66-104">It is possible to push, delete (or unlist, depending on the server implementation), and relist packages using the NuGet V3 API.</span></span> <span data-ttu-id="f1f66-105">これらの操作は無効の基づいて、`PackagePublish`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="f1f66-105">These operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="f1f66-106">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="f1f66-106">Versioning</span></span>

<span data-ttu-id="f1f66-107">次`@type`値を使用します。</span><span class="sxs-lookup"><span data-stu-id="f1f66-107">The following `@type` value is used:</span></span>

<span data-ttu-id="f1f66-108">@type の値</span><span class="sxs-lookup"><span data-stu-id="f1f66-108">@type value</span></span>          | <span data-ttu-id="f1f66-109">メモ</span><span class="sxs-lookup"><span data-stu-id="f1f66-109">Notes</span></span>
-------------------- | -----
<span data-ttu-id="f1f66-110">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="f1f66-110">PackagePublish/2.0.0</span></span> | <span data-ttu-id="f1f66-111">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="f1f66-111">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="f1f66-112">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="f1f66-112">Base URL</span></span>

<span data-ttu-id="f1f66-113">次の Api のベース URL の値、`@id`のプロパティ、`PackagePublish/2.0.0`パッケージ ソースのリソース[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="f1f66-113">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="f1f66-114">次のドキュメントでは、nuget.org の URL が使用されます。</span><span class="sxs-lookup"><span data-stu-id="f1f66-114">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="f1f66-115">検討`https://www.nuget.org/api/v2/package`のプレース ホルダーとして、`@id`サービス インデックス内の値で見つかった。</span><span class="sxs-lookup"><span data-stu-id="f1f66-115">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="f1f66-116">プロトコルが同じであるために、この URL がレガシ V2 プッシュ エンドポイントと同じ場所を指していることを注意してください。</span><span class="sxs-lookup"><span data-stu-id="f1f66-116">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f1f66-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="f1f66-117">HTTP methods</span></span>

<span data-ttu-id="f1f66-118">`PUT`、`POST`と`DELETE`HTTP メソッドは、このリソースでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f1f66-118">The `PUT`, `POST` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="f1f66-119">各エンドポイントでは、どのメソッドがサポートされている、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f1f66-119">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="f1f66-120">パッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="f1f66-120">Push a package</span></span>

> [!Note]
> <span data-ttu-id="f1f66-121">nuget.org が[追加要件](NuGet-Protocols.md)プッシュ エンドポイントと対話するためです。</span><span class="sxs-lookup"><span data-stu-id="f1f66-121">nuget.org has [additional requirements](NuGet-Protocols.md) for interacting with the push endpoint.</span></span>

<span data-ttu-id="f1f66-122">nuget.org には、次の API を使用してプッシュの新しいパッケージがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f1f66-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="f1f66-123">指定された ID とバージョンのパッケージが既に存在する場合、nuget.org は、プッシュを拒否します。</span><span class="sxs-lookup"><span data-stu-id="f1f66-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="f1f66-124">他のパッケージ ソースでは、既存のパッケージの交換をサポートできます。</span><span class="sxs-lookup"><span data-stu-id="f1f66-124">Other package sources may support replacing an existing package.</span></span>

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a><span data-ttu-id="f1f66-125">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="f1f66-125">Request parameters</span></span>

<span data-ttu-id="f1f66-126">名前</span><span class="sxs-lookup"><span data-stu-id="f1f66-126">Name</span></span>           | <span data-ttu-id="f1f66-127">イン</span><span class="sxs-lookup"><span data-stu-id="f1f66-127">In</span></span>     | <span data-ttu-id="f1f66-128">型</span><span class="sxs-lookup"><span data-stu-id="f1f66-128">Type</span></span>   | <span data-ttu-id="f1f66-129">必須</span><span class="sxs-lookup"><span data-stu-id="f1f66-129">Required</span></span> | <span data-ttu-id="f1f66-130">メモ</span><span class="sxs-lookup"><span data-stu-id="f1f66-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="f1f66-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="f1f66-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="f1f66-132">Header</span><span class="sxs-lookup"><span data-stu-id="f1f66-132">Header</span></span> | <span data-ttu-id="f1f66-133">string</span><span class="sxs-lookup"><span data-stu-id="f1f66-133">string</span></span> | <span data-ttu-id="f1f66-134">可</span><span class="sxs-lookup"><span data-stu-id="f1f66-134">yes</span></span>      | <span data-ttu-id="f1f66-135">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="f1f66-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="f1f66-136">API キーは、ユーザーがパッケージ ソースから取得し、クライアントに構成されている非透過の文字列です。</span><span class="sxs-lookup"><span data-stu-id="f1f66-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="f1f66-137">特定の文字列形式が必須でありませんが、API キーの長さは、適切な HTTP ヘッダーの値のサイズを超えない必要があります。</span><span class="sxs-lookup"><span data-stu-id="f1f66-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="f1f66-138">要求本文</span><span class="sxs-lookup"><span data-stu-id="f1f66-138">Request body</span></span>

<span data-ttu-id="f1f66-139">要求本文で、次の形式でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="f1f66-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="f1f66-140">マルチパート フォーム データ</span><span class="sxs-lookup"><span data-stu-id="f1f66-140">Multipart form data</span></span>

<span data-ttu-id="f1f66-141">要求ヘッダー`Content-Type`は`multipart/form-data`要求本文の最初の項目は、これはプッシュされる .nupkg の生のバイトとします。</span><span class="sxs-lookup"><span data-stu-id="f1f66-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="f1f66-142">マルチパート ボディ内の後続の項目は無視されます。</span><span class="sxs-lookup"><span data-stu-id="f1f66-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="f1f66-143">ファイルの名前またはマルチパートの項目の他のヘッダーが無視されます。</span><span class="sxs-lookup"><span data-stu-id="f1f66-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="f1f66-144">応答</span><span class="sxs-lookup"><span data-stu-id="f1f66-144">Response</span></span>

<span data-ttu-id="f1f66-145">状態コード</span><span class="sxs-lookup"><span data-stu-id="f1f66-145">Status Code</span></span> | <span data-ttu-id="f1f66-146">説明</span><span class="sxs-lookup"><span data-stu-id="f1f66-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="f1f66-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="f1f66-147">201, 202</span></span>    | <span data-ttu-id="f1f66-148">パッケージが正常にプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="f1f66-148">The package was successfully pushed</span></span>
<span data-ttu-id="f1f66-149">400</span><span class="sxs-lookup"><span data-stu-id="f1f66-149">400</span></span>         | <span data-ttu-id="f1f66-150">指定したパッケージが正しくありません。</span><span class="sxs-lookup"><span data-stu-id="f1f66-150">The provided package is invalid</span></span>
<span data-ttu-id="f1f66-151">409</span><span class="sxs-lookup"><span data-stu-id="f1f66-151">409</span></span>         | <span data-ttu-id="f1f66-152">指定された ID とバージョンを使用してパッケージが既に存在します。</span><span class="sxs-lookup"><span data-stu-id="f1f66-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="f1f66-153">サーバーの実装は、パッケージが正常にプッシュされたときに返される成功ステータス コードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="f1f66-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="f1f66-154">パッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="f1f66-154">Delete a package</span></span>

<span data-ttu-id="f1f66-155">nuget.org としてパッケージの削除要求では、解釈「非公開」にします。</span><span class="sxs-lookup"><span data-stu-id="f1f66-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="f1f66-156">つまり、パッケージは、パッケージの既存のコンシューマーを引き続き使用できますが、パッケージで検索結果または web インターフェイスが表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="f1f66-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="f1f66-157">この方法の詳細については、次を参照してください。、[パッケージの削除](../policies/deleting-packages.md)ポリシー。</span><span class="sxs-lookup"><span data-stu-id="f1f66-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="f1f66-158">その他のサーバーの実装では、ハード削除としてこの信号を解釈し、論理削除、または、非公開に解放されます。</span><span class="sxs-lookup"><span data-stu-id="f1f66-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="f1f66-159">たとえば、 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (するサーバーの実装だけ古い V2 API をサポート)、unlist または構成オプションに基づくハード delete のいずれかとしてこの要求の処理をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f1f66-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="f1f66-160">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="f1f66-160">Request parameters</span></span>

<span data-ttu-id="f1f66-161">名前</span><span class="sxs-lookup"><span data-stu-id="f1f66-161">Name</span></span>           | <span data-ttu-id="f1f66-162">イン</span><span class="sxs-lookup"><span data-stu-id="f1f66-162">In</span></span>     | <span data-ttu-id="f1f66-163">型</span><span class="sxs-lookup"><span data-stu-id="f1f66-163">Type</span></span>   | <span data-ttu-id="f1f66-164">必須</span><span class="sxs-lookup"><span data-stu-id="f1f66-164">Required</span></span> | <span data-ttu-id="f1f66-165">メモ</span><span class="sxs-lookup"><span data-stu-id="f1f66-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="f1f66-166">ID</span><span class="sxs-lookup"><span data-stu-id="f1f66-166">ID</span></span>             | <span data-ttu-id="f1f66-167">URL</span><span class="sxs-lookup"><span data-stu-id="f1f66-167">URL</span></span>    | <span data-ttu-id="f1f66-168">string</span><span class="sxs-lookup"><span data-stu-id="f1f66-168">string</span></span> | <span data-ttu-id="f1f66-169">可</span><span class="sxs-lookup"><span data-stu-id="f1f66-169">yes</span></span>      | <span data-ttu-id="f1f66-170">削除するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="f1f66-170">The ID of the package to delete</span></span>
<span data-ttu-id="f1f66-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="f1f66-171">VERSION</span></span>        | <span data-ttu-id="f1f66-172">URL</span><span class="sxs-lookup"><span data-stu-id="f1f66-172">URL</span></span>    | <span data-ttu-id="f1f66-173">string</span><span class="sxs-lookup"><span data-stu-id="f1f66-173">string</span></span> | <span data-ttu-id="f1f66-174">可</span><span class="sxs-lookup"><span data-stu-id="f1f66-174">yes</span></span>      | <span data-ttu-id="f1f66-175">削除するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="f1f66-175">The version of the package to delete</span></span>
<span data-ttu-id="f1f66-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="f1f66-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="f1f66-177">Header</span><span class="sxs-lookup"><span data-stu-id="f1f66-177">Header</span></span> | <span data-ttu-id="f1f66-178">string</span><span class="sxs-lookup"><span data-stu-id="f1f66-178">string</span></span> | <span data-ttu-id="f1f66-179">可</span><span class="sxs-lookup"><span data-stu-id="f1f66-179">yes</span></span>      | <span data-ttu-id="f1f66-180">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="f1f66-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="f1f66-181">応答</span><span class="sxs-lookup"><span data-stu-id="f1f66-181">Response</span></span>

<span data-ttu-id="f1f66-182">状態コード</span><span class="sxs-lookup"><span data-stu-id="f1f66-182">Status Code</span></span> | <span data-ttu-id="f1f66-183">説明</span><span class="sxs-lookup"><span data-stu-id="f1f66-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="f1f66-184">204</span><span class="sxs-lookup"><span data-stu-id="f1f66-184">204</span></span>         | <span data-ttu-id="f1f66-185">パッケージが削除されました</span><span class="sxs-lookup"><span data-stu-id="f1f66-185">The package was deleted</span></span>
<span data-ttu-id="f1f66-186">404</span><span class="sxs-lookup"><span data-stu-id="f1f66-186">404</span></span>         | <span data-ttu-id="f1f66-187">指定されたパッケージに含まれない`ID`と`VERSION`が存在します。</span><span class="sxs-lookup"><span data-stu-id="f1f66-187">No package with the provided `ID` and `VERSION` exists</span></span>

## <a name="relist-a-package"></a><span data-ttu-id="f1f66-188">パッケージを relist します。</span><span class="sxs-lookup"><span data-stu-id="f1f66-188">Relist a package</span></span>

<span data-ttu-id="f1f66-189">パッケージが一覧にない場合は、そのパッケージを"relist"のエンドポイントを使用して検索結果にもう一度表示することができます。</span><span class="sxs-lookup"><span data-stu-id="f1f66-189">If a package is unlisted, it is possible to make that package once again visible in search results using the "relist" endpoint.</span></span> <span data-ttu-id="f1f66-190">このエンドポイントと同じ形には、[削除 (非公開) エンドポイント](#delete-a-package)が使用して、 `POST` HTTP メソッドの代わりに、`DELETE`メソッドです。</span><span class="sxs-lookup"><span data-stu-id="f1f66-190">This endpoint has the same shape as the [delete (unlist) endpoint](#delete-a-package) but uses the `POST` HTTP method instead of the `DELETE` method.</span></span>

<span data-ttu-id="f1f66-191">パッケージが既に表示されている場合でも、要求は成功します。</span><span class="sxs-lookup"><span data-stu-id="f1f66-191">If the package is already listed, the request still succeeds.</span></span>

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a><span data-ttu-id="f1f66-192">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="f1f66-192">Request parameters</span></span>

<span data-ttu-id="f1f66-193">名前</span><span class="sxs-lookup"><span data-stu-id="f1f66-193">Name</span></span>           | <span data-ttu-id="f1f66-194">イン</span><span class="sxs-lookup"><span data-stu-id="f1f66-194">In</span></span>     | <span data-ttu-id="f1f66-195">型</span><span class="sxs-lookup"><span data-stu-id="f1f66-195">Type</span></span>   | <span data-ttu-id="f1f66-196">必須</span><span class="sxs-lookup"><span data-stu-id="f1f66-196">Required</span></span> | <span data-ttu-id="f1f66-197">メモ</span><span class="sxs-lookup"><span data-stu-id="f1f66-197">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="f1f66-198">ID</span><span class="sxs-lookup"><span data-stu-id="f1f66-198">ID</span></span>             | <span data-ttu-id="f1f66-199">URL</span><span class="sxs-lookup"><span data-stu-id="f1f66-199">URL</span></span>    | <span data-ttu-id="f1f66-200">string</span><span class="sxs-lookup"><span data-stu-id="f1f66-200">string</span></span> | <span data-ttu-id="f1f66-201">可</span><span class="sxs-lookup"><span data-stu-id="f1f66-201">yes</span></span>      | <span data-ttu-id="f1f66-202">Relist するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="f1f66-202">The ID of the package to relist</span></span>
<span data-ttu-id="f1f66-203">VERSION</span><span class="sxs-lookup"><span data-stu-id="f1f66-203">VERSION</span></span>        | <span data-ttu-id="f1f66-204">URL</span><span class="sxs-lookup"><span data-stu-id="f1f66-204">URL</span></span>    | <span data-ttu-id="f1f66-205">string</span><span class="sxs-lookup"><span data-stu-id="f1f66-205">string</span></span> | <span data-ttu-id="f1f66-206">可</span><span class="sxs-lookup"><span data-stu-id="f1f66-206">yes</span></span>      | <span data-ttu-id="f1f66-207">Relist するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="f1f66-207">The version of the package to relist</span></span>
<span data-ttu-id="f1f66-208">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="f1f66-208">X-NuGet-ApiKey</span></span> | <span data-ttu-id="f1f66-209">Header</span><span class="sxs-lookup"><span data-stu-id="f1f66-209">Header</span></span> | <span data-ttu-id="f1f66-210">string</span><span class="sxs-lookup"><span data-stu-id="f1f66-210">string</span></span> | <span data-ttu-id="f1f66-211">可</span><span class="sxs-lookup"><span data-stu-id="f1f66-211">yes</span></span>      | <span data-ttu-id="f1f66-212">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="f1f66-212">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="f1f66-213">応答</span><span class="sxs-lookup"><span data-stu-id="f1f66-213">Response</span></span>

<span data-ttu-id="f1f66-214">状態コード</span><span class="sxs-lookup"><span data-stu-id="f1f66-214">Status Code</span></span> | <span data-ttu-id="f1f66-215">説明</span><span class="sxs-lookup"><span data-stu-id="f1f66-215">Meaning</span></span>
----------- | -------
<span data-ttu-id="f1f66-216">200</span><span class="sxs-lookup"><span data-stu-id="f1f66-216">200</span></span>         | <span data-ttu-id="f1f66-217">パッケージが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="f1f66-217">The package is now listed</span></span>
<span data-ttu-id="f1f66-218">404</span><span class="sxs-lookup"><span data-stu-id="f1f66-218">404</span></span>         | <span data-ttu-id="f1f66-219">指定されたパッケージに含まれない`ID`と`VERSION`が存在します。</span><span class="sxs-lookup"><span data-stu-id="f1f66-219">No package with the provided `ID` and `VERSION` exists</span></span>
