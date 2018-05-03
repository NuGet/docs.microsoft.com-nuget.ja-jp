---
title: パッケージのコンテンツを NuGet API
description: パッケージのベース アドレスは、パッケージ自体をフェッチするための単純なインターフェイスです。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="package-content"></a><span data-ttu-id="50c0f-103">パッケージの内容</span><span class="sxs-lookup"><span data-stu-id="50c0f-103">Package Content</span></span>

<span data-ttu-id="50c0f-104">V3 API を使用して任意のパッケージのコンテンツ (これは .nupkg ファイル) をフェッチする URL を生成することができます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="50c0f-105">パッケージの内容をフェッチするために使用されるリソースは、`PackageBaseAddress`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="50c0f-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="50c0f-106">このリソースに表示される、パッケージのすべてのバージョンの探索を有効にも一覧にないか。</span><span class="sxs-lookup"><span data-stu-id="50c0f-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="50c0f-107">このリソースはいずれかの"パッケージ ベース アドレスとして"または「フラット コンテナー」として一般的に呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="50c0f-108">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="50c0f-108">Versioning</span></span>

<span data-ttu-id="50c0f-109">次`@type`値を使用します。</span><span class="sxs-lookup"><span data-stu-id="50c0f-109">The following `@type` value is used:</span></span>

<span data-ttu-id="50c0f-110">@type の値</span><span class="sxs-lookup"><span data-stu-id="50c0f-110">@type value</span></span>              | <span data-ttu-id="50c0f-111">メモ</span><span class="sxs-lookup"><span data-stu-id="50c0f-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="50c0f-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="50c0f-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="50c0f-113">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="50c0f-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="50c0f-114">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="50c0f-114">Base URL</span></span>

<span data-ttu-id="50c0f-115">次の Api のベース URL の値、`@id`前述のリソースに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="50c0f-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="50c0f-116">次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="50c0f-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="50c0f-117">HTTP methods</span></span>

<span data-ttu-id="50c0f-118">HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。</span><span class="sxs-lookup"><span data-stu-id="50c0f-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="50c0f-119">パッケージのバージョンを列挙します。</span><span class="sxs-lookup"><span data-stu-id="50c0f-119">Enumerate package versions</span></span>

<span data-ttu-id="50c0f-120">場合は、クライアントがパッケージ ID を知っているし、するパッケージのバージョンのパッケージを検出するソースが利用可能なクライアントは、すべてのパッケージ バージョンを列挙する予測可能な URL を構築できます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="50c0f-121">この一覧は目的として「ディレクトリの一覧」パッケージのコンテンツ api 以下に説明します。</span><span class="sxs-lookup"><span data-stu-id="50c0f-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="50c0f-122">この一覧には、両方の一覧表示され、一覧にないパッケージ バージョンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="50c0f-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="50c0f-123">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="50c0f-123">Request parameters</span></span>

<span data-ttu-id="50c0f-124">名前</span><span class="sxs-lookup"><span data-stu-id="50c0f-124">Name</span></span>     | <span data-ttu-id="50c0f-125">イン</span><span class="sxs-lookup"><span data-stu-id="50c0f-125">In</span></span>     | <span data-ttu-id="50c0f-126">型</span><span class="sxs-lookup"><span data-stu-id="50c0f-126">Type</span></span>    | <span data-ttu-id="50c0f-127">必須</span><span class="sxs-lookup"><span data-stu-id="50c0f-127">Required</span></span> | <span data-ttu-id="50c0f-128">メモ</span><span class="sxs-lookup"><span data-stu-id="50c0f-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="50c0f-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="50c0f-129">LOWER_ID</span></span> | <span data-ttu-id="50c0f-130">URL</span><span class="sxs-lookup"><span data-stu-id="50c0f-130">URL</span></span>    | <span data-ttu-id="50c0f-131">string</span><span class="sxs-lookup"><span data-stu-id="50c0f-131">string</span></span>  | <span data-ttu-id="50c0f-132">可</span><span class="sxs-lookup"><span data-stu-id="50c0f-132">yes</span></span>      | <span data-ttu-id="50c0f-133">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="50c0f-133">The package ID, lowercase</span></span>

<span data-ttu-id="50c0f-134">`LOWER_ID`値は小文字によって実装される規則を使用して、目的のパッケージ ID。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。</span><span class="sxs-lookup"><span data-stu-id="50c0f-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="50c0f-135">応答</span><span class="sxs-lookup"><span data-stu-id="50c0f-135">Response</span></span>

<span data-ttu-id="50c0f-136">指定されたパッケージ ID のバージョンのパッケージ ソースがない場合は、状態コード 404 が返されます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="50c0f-137">パッケージ ソースに 1 つまたは複数のバージョンがある場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="50c0f-138">応答本文は、次のプロパティを使用して、JSON オブジェクトを示します。</span><span class="sxs-lookup"><span data-stu-id="50c0f-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="50c0f-139">名前</span><span class="sxs-lookup"><span data-stu-id="50c0f-139">Name</span></span>     | <span data-ttu-id="50c0f-140">種類</span><span class="sxs-lookup"><span data-stu-id="50c0f-140">Type</span></span>             | <span data-ttu-id="50c0f-141">必須</span><span class="sxs-lookup"><span data-stu-id="50c0f-141">Required</span></span> | <span data-ttu-id="50c0f-142">メモ</span><span class="sxs-lookup"><span data-stu-id="50c0f-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="50c0f-143">バージョン</span><span class="sxs-lookup"><span data-stu-id="50c0f-143">versions</span></span> | <span data-ttu-id="50c0f-144">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="50c0f-144">array of strings</span></span> | <span data-ttu-id="50c0f-145">可</span><span class="sxs-lookup"><span data-stu-id="50c0f-145">yes</span></span>      | <span data-ttu-id="50c0f-146">パッケージに使用できる Id</span><span class="sxs-lookup"><span data-stu-id="50c0f-146">The package IDs available</span></span>

<span data-ttu-id="50c0f-147">内の文字列、`versions`配列は、すべて小文字、 [NuGet のバージョン文字列を正規化](../reference/package-versioning.md#normalized-version-numbers)です。</span><span class="sxs-lookup"><span data-stu-id="50c0f-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="50c0f-148">バージョン文字列では、SemVer 2.0.0 ビルド メタデータは含まれません。</span><span class="sxs-lookup"><span data-stu-id="50c0f-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="50c0f-149">この配列内で見つかったバージョン文字列をそのまま使用することができますが、目的、`LOWER_VERSION`のトークンが、次のエンドポイント。</span><span class="sxs-lookup"><span data-stu-id="50c0f-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="50c0f-150">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="50c0f-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="50c0f-151">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="50c0f-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="50c0f-152">パッケージのコンテンツ (これは .nupkg) のダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50c0f-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="50c0f-153">のみ、クライアントがパッケージ ID とバージョンを把握して、パッケージ コンテンツをダウンロードする場合は、それらを次の URL を構築する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50c0f-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="50c0f-154">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="50c0f-154">Request parameters</span></span>

<span data-ttu-id="50c0f-155">名前</span><span class="sxs-lookup"><span data-stu-id="50c0f-155">Name</span></span>          | <span data-ttu-id="50c0f-156">イン</span><span class="sxs-lookup"><span data-stu-id="50c0f-156">In</span></span>     | <span data-ttu-id="50c0f-157">型</span><span class="sxs-lookup"><span data-stu-id="50c0f-157">Type</span></span>   | <span data-ttu-id="50c0f-158">必須</span><span class="sxs-lookup"><span data-stu-id="50c0f-158">Required</span></span> | <span data-ttu-id="50c0f-159">メモ</span><span class="sxs-lookup"><span data-stu-id="50c0f-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="50c0f-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="50c0f-160">LOWER_ID</span></span>      | <span data-ttu-id="50c0f-161">URL</span><span class="sxs-lookup"><span data-stu-id="50c0f-161">URL</span></span>    | <span data-ttu-id="50c0f-162">string</span><span class="sxs-lookup"><span data-stu-id="50c0f-162">string</span></span> | <span data-ttu-id="50c0f-163">可</span><span class="sxs-lookup"><span data-stu-id="50c0f-163">yes</span></span>      | <span data-ttu-id="50c0f-164">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="50c0f-164">The package ID, lowercase</span></span>
<span data-ttu-id="50c0f-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="50c0f-165">LOWER_VERSION</span></span> | <span data-ttu-id="50c0f-166">URL</span><span class="sxs-lookup"><span data-stu-id="50c0f-166">URL</span></span>    | <span data-ttu-id="50c0f-167">string</span><span class="sxs-lookup"><span data-stu-id="50c0f-167">string</span></span> | <span data-ttu-id="50c0f-168">可</span><span class="sxs-lookup"><span data-stu-id="50c0f-168">yes</span></span>      | <span data-ttu-id="50c0f-169">パッケージのバージョンが正規化され、小文字</span><span class="sxs-lookup"><span data-stu-id="50c0f-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="50c0f-170">両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用している小文字です。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。</span><span class="sxs-lookup"><span data-stu-id="50c0f-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="50c0f-171">`LOWER_VERSION`目的のパッケージのバージョンを使用して正規化 NuGet のバージョン[正規化規則](../reference/package-versioning.md#normalized-version-numbers)です。</span><span class="sxs-lookup"><span data-stu-id="50c0f-171">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="50c0f-172">つまり、SemVer 2.0.0 の仕様によって許可されているメタデータをビルドするをここでは除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50c0f-172">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="50c0f-173">応答本文</span><span class="sxs-lookup"><span data-stu-id="50c0f-173">Response body</span></span>

<span data-ttu-id="50c0f-174">パッケージがパッケージ ソースに存在する場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-174">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="50c0f-175">応答本文は、パッケージのコンテンツそのものになります。</span><span class="sxs-lookup"><span data-stu-id="50c0f-175">The response body will be the package content itself.</span></span>

<span data-ttu-id="50c0f-176">パッケージがパッケージ ソースに存在しない場合は、状態コード 404 が返されます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-176">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="50c0f-177">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="50c0f-177">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="50c0f-178">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="50c0f-178">Sample response</span></span>

<span data-ttu-id="50c0f-179">これは、Newtonsoft.Json 9.0.1 の .nupkg であるバイナリ ストリーム。</span><span class="sxs-lookup"><span data-stu-id="50c0f-179">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="50c0f-180">パッケージ マニフェスト (.nuspec) をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="50c0f-180">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="50c0f-181">のみ、クライアントがパッケージ ID とバージョンを把握して、パッケージ マニフェストをダウンロードする場合は、それらを次の URL を構築する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50c0f-181">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="50c0f-182">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="50c0f-182">Request parameters</span></span>

<span data-ttu-id="50c0f-183">名前</span><span class="sxs-lookup"><span data-stu-id="50c0f-183">Name</span></span>          | <span data-ttu-id="50c0f-184">イン</span><span class="sxs-lookup"><span data-stu-id="50c0f-184">In</span></span>     | <span data-ttu-id="50c0f-185">型</span><span class="sxs-lookup"><span data-stu-id="50c0f-185">Type</span></span>    | <span data-ttu-id="50c0f-186">必須</span><span class="sxs-lookup"><span data-stu-id="50c0f-186">Required</span></span> | <span data-ttu-id="50c0f-187">メモ</span><span class="sxs-lookup"><span data-stu-id="50c0f-187">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="50c0f-188">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="50c0f-188">LOWER_ID</span></span>      | <span data-ttu-id="50c0f-189">URL</span><span class="sxs-lookup"><span data-stu-id="50c0f-189">URL</span></span>    | <span data-ttu-id="50c0f-190">string</span><span class="sxs-lookup"><span data-stu-id="50c0f-190">string</span></span>  | <span data-ttu-id="50c0f-191">可</span><span class="sxs-lookup"><span data-stu-id="50c0f-191">yes</span></span>      | <span data-ttu-id="50c0f-192">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="50c0f-192">The package ID, lowercase</span></span>
<span data-ttu-id="50c0f-193">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="50c0f-193">LOWER_VERSION</span></span> | <span data-ttu-id="50c0f-194">URL</span><span class="sxs-lookup"><span data-stu-id="50c0f-194">URL</span></span>    | <span data-ttu-id="50c0f-195">整数</span><span class="sxs-lookup"><span data-stu-id="50c0f-195">integer</span></span> | <span data-ttu-id="50c0f-196">可</span><span class="sxs-lookup"><span data-stu-id="50c0f-196">yes</span></span>      | <span data-ttu-id="50c0f-197">パッケージのバージョンが正規化され、小文字</span><span class="sxs-lookup"><span data-stu-id="50c0f-197">The package version, normalized and lowercased</span></span>

<span data-ttu-id="50c0f-198">両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用している小文字です。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。</span><span class="sxs-lookup"><span data-stu-id="50c0f-198">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="50c0f-199">`LOWER_VERSION`目的のパッケージのバージョンを使用して正規化 NuGet のバージョン[正規化規則](../reference/package-versioning.md#normalized-version-numbers)です。</span><span class="sxs-lookup"><span data-stu-id="50c0f-199">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="50c0f-200">つまり、SemVer 2.0.0 の仕様によって許可されているメタデータをビルドするをここでは除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50c0f-200">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="50c0f-201">応答本文</span><span class="sxs-lookup"><span data-stu-id="50c0f-201">Response body</span></span>

<span data-ttu-id="50c0f-202">パッケージがパッケージ ソースに存在する場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-202">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="50c0f-203">応答本文は、パッケージ マニフェストでは、これは、対応する .nupkg に含まれている .nuspec になります。</span><span class="sxs-lookup"><span data-stu-id="50c0f-203">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="50c0f-204">.Nuspec は、XML ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="50c0f-204">The .nuspec is an XML document.</span></span>

<span data-ttu-id="50c0f-205">パッケージがパッケージ ソースに存在しない場合は、状態コード 404 が返されます。</span><span class="sxs-lookup"><span data-stu-id="50c0f-205">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="50c0f-206">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="50c0f-206">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="50c0f-207">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="50c0f-207">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
