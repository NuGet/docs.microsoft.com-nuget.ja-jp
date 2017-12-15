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
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a><span data-ttu-id="16742-104">プッシュ モードと削除</span><span class="sxs-lookup"><span data-stu-id="16742-104">Push and Delete</span></span>

<span data-ttu-id="16742-105">プッシュし削除 (またはサーバーの実装によって、非公開) することは NuGet V3 API を使用してパッケージ化します。</span><span class="sxs-lookup"><span data-stu-id="16742-105">It is possible to push and delete (or unlist, depending on the server implementation) packages using the NuGet V3 API.</span></span>
<span data-ttu-id="16742-106">両方の操作は無効の基づいて、`PackagePublish`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="16742-106">Both operations are based off of the `PackagePublish` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="16742-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="16742-107">Versioning</span></span>

<span data-ttu-id="16742-108">次`@type`値を使用します。</span><span class="sxs-lookup"><span data-stu-id="16742-108">The following `@type` value is used:</span></span>

<span data-ttu-id="16742-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="16742-109">@type value</span></span>          | <span data-ttu-id="16742-110">メモ</span><span class="sxs-lookup"><span data-stu-id="16742-110">Notes</span></span>
-------------------- | -----
<span data-ttu-id="16742-111">PackagePublish/2.0.0</span><span class="sxs-lookup"><span data-stu-id="16742-111">PackagePublish/2.0.0</span></span> | <span data-ttu-id="16742-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="16742-112">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="16742-113">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="16742-113">Base URL</span></span>

<span data-ttu-id="16742-114">次の Api のベース URL の値、`@id`のプロパティ、`PackagePublish/2.0.0`パッケージ ソースのリソース[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="16742-114">The base URL for the following APIs is the value of the `@id` property of the `PackagePublish/2.0.0` resource in the package source's [service index](service-index.md).</span></span> <span data-ttu-id="16742-115">次のドキュメントでは、nuget.org の URL が使用されます。</span><span class="sxs-lookup"><span data-stu-id="16742-115">For the documentation below, nuget.org's URL is used.</span></span> <span data-ttu-id="16742-116">検討`https://www.nuget.org/api/v2/package`のプレース ホルダーとして、`@id`サービス インデックス内の値で見つかった。</span><span class="sxs-lookup"><span data-stu-id="16742-116">Consider `https://www.nuget.org/api/v2/package` as a placeholder for the `@id` value found in the service index.</span></span>

<span data-ttu-id="16742-117">プロトコルが同じであるために、この URL がレガシ V2 プッシュ エンドポイントと同じ場所を指していることを注意してください。</span><span class="sxs-lookup"><span data-stu-id="16742-117">Note that this URL points to the same location as the legacy V2 push endpoint since the protocol is the same.</span></span>

## <a name="http-methods"></a><span data-ttu-id="16742-118">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="16742-118">HTTP methods</span></span>

<span data-ttu-id="16742-119">`PUT`と`DELETE`HTTP メソッドは、このリソースでサポートされています。</span><span class="sxs-lookup"><span data-stu-id="16742-119">The `PUT` and `DELETE` HTTP methods are supported by this resource.</span></span> <span data-ttu-id="16742-120">各エンドポイントでは、どのメソッドがサポートされている、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="16742-120">For which methods are supported on each endpoint, see below.</span></span>

## <a name="push-a-package"></a><span data-ttu-id="16742-121">パッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="16742-121">Push a package</span></span>

<span data-ttu-id="16742-122">nuget.org には、次の API を使用してプッシュの新しいパッケージがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="16742-122">nuget.org supports pushing new packages using the following API.</span></span> <span data-ttu-id="16742-123">指定された ID とバージョンのパッケージが既に存在する場合、nuget.org は、プッシュを拒否します。</span><span class="sxs-lookup"><span data-stu-id="16742-123">If the package with the provided ID and version already exists, nuget.org will reject the push.</span></span> <span data-ttu-id="16742-124">他のパッケージ ソースでは、既存のパッケージの交換をサポートできます。</span><span class="sxs-lookup"><span data-stu-id="16742-124">Other package sources may support replacing an existing package.</span></span>

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a><span data-ttu-id="16742-125">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="16742-125">Request parameters</span></span>

<span data-ttu-id="16742-126">名前</span><span class="sxs-lookup"><span data-stu-id="16742-126">Name</span></span>           | <span data-ttu-id="16742-127">イン</span><span class="sxs-lookup"><span data-stu-id="16742-127">In</span></span>     | <span data-ttu-id="16742-128">型</span><span class="sxs-lookup"><span data-stu-id="16742-128">Type</span></span>   | <span data-ttu-id="16742-129">必須</span><span class="sxs-lookup"><span data-stu-id="16742-129">Required</span></span> | <span data-ttu-id="16742-130">メモ</span><span class="sxs-lookup"><span data-stu-id="16742-130">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="16742-131">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="16742-131">X-NuGet-ApiKey</span></span> | <span data-ttu-id="16742-132">Header</span><span class="sxs-lookup"><span data-stu-id="16742-132">Header</span></span> | <span data-ttu-id="16742-133">string</span><span class="sxs-lookup"><span data-stu-id="16742-133">string</span></span> | <span data-ttu-id="16742-134">可</span><span class="sxs-lookup"><span data-stu-id="16742-134">yes</span></span>      | <span data-ttu-id="16742-135">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="16742-135">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

<span data-ttu-id="16742-136">API キーは、ユーザーがパッケージ ソースから取得し、クライアントに構成されている非透過の文字列です。</span><span class="sxs-lookup"><span data-stu-id="16742-136">The API key is an opaque string gotten from the package source by the user and configured into the client.</span></span> <span data-ttu-id="16742-137">特定の文字列形式が必須でありませんが、API キーの長さは、適切な HTTP ヘッダーの値のサイズを超えない必要があります。</span><span class="sxs-lookup"><span data-stu-id="16742-137">No particular string format is mandated but the length of the API key should not exceed a reasonable size for HTTP header values.</span></span>

### <a name="request-body"></a><span data-ttu-id="16742-138">要求本文</span><span class="sxs-lookup"><span data-stu-id="16742-138">Request body</span></span>

<span data-ttu-id="16742-139">要求本文で、次の形式でなければなりません。</span><span class="sxs-lookup"><span data-stu-id="16742-139">The request body must come in the following form:</span></span>

#### <a name="multipart-form-data"></a><span data-ttu-id="16742-140">マルチパート フォーム データ</span><span class="sxs-lookup"><span data-stu-id="16742-140">Multipart form data</span></span>

<span data-ttu-id="16742-141">要求ヘッダー`Content-Type`は`multipart/form-data`要求本文の最初の項目は、これはプッシュされる .nupkg の生のバイトとします。</span><span class="sxs-lookup"><span data-stu-id="16742-141">The request header `Content-Type` is `multipart/form-data` and the first item in the request body is the raw bytes of the .nupkg being pushed.</span></span> <span data-ttu-id="16742-142">マルチパート ボディ内の後続の項目は無視されます。</span><span class="sxs-lookup"><span data-stu-id="16742-142">Subsequent items in the multipart body are ignored.</span></span> <span data-ttu-id="16742-143">ファイルの名前またはマルチパートの項目の他のヘッダーが無視されます。</span><span class="sxs-lookup"><span data-stu-id="16742-143">The file name or any other headers of the multipart items are ignored.</span></span>

### <a name="response"></a><span data-ttu-id="16742-144">応答</span><span class="sxs-lookup"><span data-stu-id="16742-144">Response</span></span>

<span data-ttu-id="16742-145">状態コード</span><span class="sxs-lookup"><span data-stu-id="16742-145">Status Code</span></span> | <span data-ttu-id="16742-146">説明</span><span class="sxs-lookup"><span data-stu-id="16742-146">Meaning</span></span>
----------- | -------
<span data-ttu-id="16742-147">201, 202</span><span class="sxs-lookup"><span data-stu-id="16742-147">201, 202</span></span>    | <span data-ttu-id="16742-148">パッケージが正常にプッシュされます。</span><span class="sxs-lookup"><span data-stu-id="16742-148">The package was successfully pushed</span></span>
<span data-ttu-id="16742-149">400</span><span class="sxs-lookup"><span data-stu-id="16742-149">400</span></span>         | <span data-ttu-id="16742-150">指定したパッケージが正しくありません。</span><span class="sxs-lookup"><span data-stu-id="16742-150">The provided package is invalid</span></span>
<span data-ttu-id="16742-151">409</span><span class="sxs-lookup"><span data-stu-id="16742-151">409</span></span>         | <span data-ttu-id="16742-152">指定された ID とバージョンを使用してパッケージが既に存在します。</span><span class="sxs-lookup"><span data-stu-id="16742-152">A package with the provided ID and version already exists</span></span>

<span data-ttu-id="16742-153">サーバーの実装は、パッケージが正常にプッシュされたときに返される成功ステータス コードによって異なります。</span><span class="sxs-lookup"><span data-stu-id="16742-153">Server implementations vary on the success status code returned when a package is successfully pushed.</span></span>

## <a name="delete-a-package"></a><span data-ttu-id="16742-154">パッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="16742-154">Delete a package</span></span>

<span data-ttu-id="16742-155">nuget.org としてパッケージの削除要求では、解釈「非公開」にします。</span><span class="sxs-lookup"><span data-stu-id="16742-155">nuget.org interprets the package delete request as an "unlist".</span></span> <span data-ttu-id="16742-156">つまり、パッケージは、パッケージの既存のコンシューマーを引き続き使用できますが、パッケージで検索結果または web インターフェイスが表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="16742-156">This means that the package is still available for existing consumers of the package but the package no longer appears in search results or in the web interface.</span></span> <span data-ttu-id="16742-157">この方法の詳細については、次を参照してください。、[パッケージの削除](../policies/deleting-packages.md)ポリシー。</span><span class="sxs-lookup"><span data-stu-id="16742-157">For more information about this practice, see the [Deleted Packages](../policies/deleting-packages.md) policy.</span></span> <span data-ttu-id="16742-158">その他のサーバーの実装では、ハード削除としてこの信号を解釈し、論理削除、または、非公開に解放されます。</span><span class="sxs-lookup"><span data-stu-id="16742-158">Other server implementations are free to interpret this signal as a hard delete, soft delete, or unlist.</span></span> <span data-ttu-id="16742-159">たとえば、 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (するサーバーの実装だけ古い V2 API をサポート)、unlist または構成オプションに基づくハード delete のいずれかとしてこの要求の処理をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="16742-159">For example, [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (a server implementation only supporting the older V2 API) supports handling this request as either an unlist or a hard delete based on a configuration option.</span></span>

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a><span data-ttu-id="16742-160">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="16742-160">Request parameters</span></span>

<span data-ttu-id="16742-161">名前</span><span class="sxs-lookup"><span data-stu-id="16742-161">Name</span></span>           | <span data-ttu-id="16742-162">イン</span><span class="sxs-lookup"><span data-stu-id="16742-162">In</span></span>     | <span data-ttu-id="16742-163">型</span><span class="sxs-lookup"><span data-stu-id="16742-163">Type</span></span>   | <span data-ttu-id="16742-164">必須</span><span class="sxs-lookup"><span data-stu-id="16742-164">Required</span></span> | <span data-ttu-id="16742-165">メモ</span><span class="sxs-lookup"><span data-stu-id="16742-165">Notes</span></span>
-------------- | ------ | ------ | -------- | -----
<span data-ttu-id="16742-166">ID</span><span class="sxs-lookup"><span data-stu-id="16742-166">ID</span></span>             | <span data-ttu-id="16742-167">URL</span><span class="sxs-lookup"><span data-stu-id="16742-167">URL</span></span>    | <span data-ttu-id="16742-168">string</span><span class="sxs-lookup"><span data-stu-id="16742-168">string</span></span> | <span data-ttu-id="16742-169">可</span><span class="sxs-lookup"><span data-stu-id="16742-169">yes</span></span>      | <span data-ttu-id="16742-170">削除するパッケージの ID</span><span class="sxs-lookup"><span data-stu-id="16742-170">The ID of the package to delete</span></span>
<span data-ttu-id="16742-171">VERSION</span><span class="sxs-lookup"><span data-stu-id="16742-171">VERSION</span></span>        | <span data-ttu-id="16742-172">URL</span><span class="sxs-lookup"><span data-stu-id="16742-172">URL</span></span>    | <span data-ttu-id="16742-173">string</span><span class="sxs-lookup"><span data-stu-id="16742-173">string</span></span> | <span data-ttu-id="16742-174">可</span><span class="sxs-lookup"><span data-stu-id="16742-174">yes</span></span>      | <span data-ttu-id="16742-175">削除するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="16742-175">The version of the package to delete</span></span>
<span data-ttu-id="16742-176">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="16742-176">X-NuGet-ApiKey</span></span> | <span data-ttu-id="16742-177">Header</span><span class="sxs-lookup"><span data-stu-id="16742-177">Header</span></span> | <span data-ttu-id="16742-178">string</span><span class="sxs-lookup"><span data-stu-id="16742-178">string</span></span> | <span data-ttu-id="16742-179">可</span><span class="sxs-lookup"><span data-stu-id="16742-179">yes</span></span>      | <span data-ttu-id="16742-180">たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`</span><span class="sxs-lookup"><span data-stu-id="16742-180">For example, `X-NuGet-ApiKey: {USER_API_KEY}`</span></span>

### <a name="response"></a><span data-ttu-id="16742-181">応答</span><span class="sxs-lookup"><span data-stu-id="16742-181">Response</span></span>

<span data-ttu-id="16742-182">状態コード</span><span class="sxs-lookup"><span data-stu-id="16742-182">Status Code</span></span> | <span data-ttu-id="16742-183">説明</span><span class="sxs-lookup"><span data-stu-id="16742-183">Meaning</span></span>
----------- | -------
<span data-ttu-id="16742-184">204</span><span class="sxs-lookup"><span data-stu-id="16742-184">204</span></span>         | <span data-ttu-id="16742-185">パッケージが削除されました</span><span class="sxs-lookup"><span data-stu-id="16742-185">The package was deleted</span></span>
<span data-ttu-id="16742-186">404</span><span class="sxs-lookup"><span data-stu-id="16742-186">404</span></span>         | <span data-ttu-id="16742-187">指定されたパッケージに含まれない`ID`と`VERSION`が存在します。</span><span class="sxs-lookup"><span data-stu-id="16742-187">No package with the provided `ID` and `VERSION` exists</span></span>
