---
title: "パッケージのコンテンツを NuGet API |Microsoft ドキュメント"
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
description: "パッケージのベース アドレスは、パッケージ自体をフェッチするための単純なインターフェイスです。"
keywords: "NuGet は、コンテナー、NuGet パッケージのベース アドレス、NuGet nupkg API、API の NuGet パッケージのバージョンを NuGet API フラットな一覧にないパッケージでは、NuGet API ダウンロード nuspec"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: c2e631dc0bba95ac849430d77142f27ef591f741
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="package-content"></a><span data-ttu-id="aa77a-104">パッケージの内容</span><span class="sxs-lookup"><span data-stu-id="aa77a-104">Package Content</span></span>

<span data-ttu-id="aa77a-105">V3 API を使用して任意のパッケージのコンテンツ (これは .nupkg ファイル) をフェッチする URL を生成することができます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-105">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="aa77a-106">パッケージの内容をフェッチするために使用されるリソースは、`PackageBaseAddress`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="aa77a-106">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="aa77a-107">このリソースに表示される、パッケージのすべてのバージョンの探索を有効にも一覧にないか。</span><span class="sxs-lookup"><span data-stu-id="aa77a-107">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="aa77a-108">このリソースはいずれかの"パッケージ ベース アドレスとして"または「フラット コンテナー」として一般的に呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-108">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="aa77a-109">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="aa77a-109">Versioning</span></span>

<span data-ttu-id="aa77a-110">次`@type`値を使用します。</span><span class="sxs-lookup"><span data-stu-id="aa77a-110">The following `@type` value is used:</span></span>

<span data-ttu-id="aa77a-111">@type の値</span><span class="sxs-lookup"><span data-stu-id="aa77a-111">@type value</span></span>              | <span data-ttu-id="aa77a-112">メモ</span><span class="sxs-lookup"><span data-stu-id="aa77a-112">Notes</span></span>
------------------------ | -----
<span data-ttu-id="aa77a-113">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="aa77a-113">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="aa77a-114">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="aa77a-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="aa77a-115">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="aa77a-115">Base URL</span></span>

<span data-ttu-id="aa77a-116">次の Api のベース URL の値、`@id`前述のリソースに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="aa77a-116">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="aa77a-117">次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-117">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="aa77a-118">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="aa77a-118">HTTP methods</span></span>

<span data-ttu-id="aa77a-119">HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。</span><span class="sxs-lookup"><span data-stu-id="aa77a-119">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="aa77a-120">パッケージのバージョンを列挙します。</span><span class="sxs-lookup"><span data-stu-id="aa77a-120">Enumerate package versions</span></span>

<span data-ttu-id="aa77a-121">場合は、クライアントがパッケージ ID を知っているし、するパッケージのバージョンのパッケージを検出するソースが利用可能なクライアントは、すべてのパッケージ バージョンを列挙する予測可能な URL を構築できます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-121">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="aa77a-122">この一覧は目的として「ディレクトリの一覧」パッケージのコンテンツ api 以下に説明します。</span><span class="sxs-lookup"><span data-stu-id="aa77a-122">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="aa77a-123">この一覧には、両方の一覧表示され、一覧にないパッケージ バージョンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="aa77a-123">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="aa77a-124">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="aa77a-124">Request parameters</span></span>

<span data-ttu-id="aa77a-125">name</span><span class="sxs-lookup"><span data-stu-id="aa77a-125">Name</span></span>     | <span data-ttu-id="aa77a-126">イン</span><span class="sxs-lookup"><span data-stu-id="aa77a-126">In</span></span>     | <span data-ttu-id="aa77a-127">型</span><span class="sxs-lookup"><span data-stu-id="aa77a-127">Type</span></span>    | <span data-ttu-id="aa77a-128">必須</span><span class="sxs-lookup"><span data-stu-id="aa77a-128">Required</span></span> | <span data-ttu-id="aa77a-129">メモ</span><span class="sxs-lookup"><span data-stu-id="aa77a-129">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="aa77a-130">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="aa77a-130">LOWER_ID</span></span> | <span data-ttu-id="aa77a-131">URL</span><span class="sxs-lookup"><span data-stu-id="aa77a-131">URL</span></span>    | <span data-ttu-id="aa77a-132">string</span><span class="sxs-lookup"><span data-stu-id="aa77a-132">string</span></span>  | <span data-ttu-id="aa77a-133">可</span><span class="sxs-lookup"><span data-stu-id="aa77a-133">yes</span></span>      | <span data-ttu-id="aa77a-134">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="aa77a-134">The package ID, lowercase</span></span>

<span data-ttu-id="aa77a-135">`LOWER_ID`値は小文字によって実装される規則を使用して、目的のパッケージ ID。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。</span><span class="sxs-lookup"><span data-stu-id="aa77a-135">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="aa77a-136">応答</span><span class="sxs-lookup"><span data-stu-id="aa77a-136">Response</span></span>

<span data-ttu-id="aa77a-137">指定されたパッケージ ID のバージョンのパッケージ ソースがない場合は、状態コード 404 が返されます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-137">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="aa77a-138">パッケージ ソースに 1 つまたは複数のバージョンがある場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-138">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="aa77a-139">応答本文は、次のプロパティを使用して、JSON オブジェクトを示します。</span><span class="sxs-lookup"><span data-stu-id="aa77a-139">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="aa77a-140">name</span><span class="sxs-lookup"><span data-stu-id="aa77a-140">Name</span></span>     | <span data-ttu-id="aa77a-141">種類</span><span class="sxs-lookup"><span data-stu-id="aa77a-141">Type</span></span>             | <span data-ttu-id="aa77a-142">必須</span><span class="sxs-lookup"><span data-stu-id="aa77a-142">Required</span></span> | <span data-ttu-id="aa77a-143">メモ</span><span class="sxs-lookup"><span data-stu-id="aa77a-143">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="aa77a-144">バージョン</span><span class="sxs-lookup"><span data-stu-id="aa77a-144">versions</span></span> | <span data-ttu-id="aa77a-145">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="aa77a-145">array of strings</span></span> | <span data-ttu-id="aa77a-146">可</span><span class="sxs-lookup"><span data-stu-id="aa77a-146">yes</span></span>      | <span data-ttu-id="aa77a-147">パッケージに使用できる Id</span><span class="sxs-lookup"><span data-stu-id="aa77a-147">The package IDs available</span></span>

<span data-ttu-id="aa77a-148">内の文字列、`versions`配列は、すべて小文字、 [NuGet のバージョン文字列を正規化](../reference/package-versioning.md#normalized-version-numbers)です。</span><span class="sxs-lookup"><span data-stu-id="aa77a-148">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="aa77a-149">バージョン文字列では、SemVer 2.0.0 ビルド メタデータは含まれません。</span><span class="sxs-lookup"><span data-stu-id="aa77a-149">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="aa77a-150">この配列内で見つかったバージョン文字列をそのまま使用することができますが、目的、`LOWER_VERSION`のトークンが、次のエンドポイント。</span><span class="sxs-lookup"><span data-stu-id="aa77a-150">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="aa77a-151">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="aa77a-151">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="aa77a-152">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="aa77a-152">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="aa77a-153">パッケージのコンテンツ (これは .nupkg) のダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="aa77a-153">Download package content (.nupkg)</span></span>

<span data-ttu-id="aa77a-154">のみ、クライアントがパッケージ ID とバージョンを把握して、パッケージ コンテンツをダウンロードする場合は、それらを次の URL を構築する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa77a-154">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="aa77a-155">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="aa77a-155">Request parameters</span></span>

<span data-ttu-id="aa77a-156">name</span><span class="sxs-lookup"><span data-stu-id="aa77a-156">Name</span></span>          | <span data-ttu-id="aa77a-157">イン</span><span class="sxs-lookup"><span data-stu-id="aa77a-157">In</span></span>     | <span data-ttu-id="aa77a-158">型</span><span class="sxs-lookup"><span data-stu-id="aa77a-158">Type</span></span>   | <span data-ttu-id="aa77a-159">必須</span><span class="sxs-lookup"><span data-stu-id="aa77a-159">Required</span></span> | <span data-ttu-id="aa77a-160">メモ</span><span class="sxs-lookup"><span data-stu-id="aa77a-160">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="aa77a-161">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="aa77a-161">LOWER_ID</span></span>      | <span data-ttu-id="aa77a-162">URL</span><span class="sxs-lookup"><span data-stu-id="aa77a-162">URL</span></span>    | <span data-ttu-id="aa77a-163">string</span><span class="sxs-lookup"><span data-stu-id="aa77a-163">string</span></span> | <span data-ttu-id="aa77a-164">可</span><span class="sxs-lookup"><span data-stu-id="aa77a-164">yes</span></span>      | <span data-ttu-id="aa77a-165">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="aa77a-165">The package ID, lowercase</span></span>
<span data-ttu-id="aa77a-166">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="aa77a-166">LOWER_VERSION</span></span> | <span data-ttu-id="aa77a-167">URL</span><span class="sxs-lookup"><span data-stu-id="aa77a-167">URL</span></span>    | <span data-ttu-id="aa77a-168">string</span><span class="sxs-lookup"><span data-stu-id="aa77a-168">string</span></span> | <span data-ttu-id="aa77a-169">可</span><span class="sxs-lookup"><span data-stu-id="aa77a-169">yes</span></span>      | <span data-ttu-id="aa77a-170">パッケージのバージョンが正規化され、小文字</span><span class="sxs-lookup"><span data-stu-id="aa77a-170">The package version, normalized and lowercased</span></span>

<span data-ttu-id="aa77a-171">両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用している小文字です。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。</span><span class="sxs-lookup"><span data-stu-id="aa77a-171">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="aa77a-172">`LOWER_VERSION`目的のパッケージのバージョンを使用して正規化 NuGet のバージョン[正規化規則](../reference/package-versioning.md#normalized-version-numbers)です。</span><span class="sxs-lookup"><span data-stu-id="aa77a-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="aa77a-173">つまり、SemVer 2.0.0 の仕様によって許可されているメタデータをビルドするをここでは除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa77a-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="aa77a-174">応答本文</span><span class="sxs-lookup"><span data-stu-id="aa77a-174">Response body</span></span>

<span data-ttu-id="aa77a-175">パッケージがパッケージ ソースに存在する場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="aa77a-176">応答本文は、パッケージのコンテンツそのものになります。</span><span class="sxs-lookup"><span data-stu-id="aa77a-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="aa77a-177">パッケージがパッケージ ソースに存在しない場合は、状態コード 404 が返されます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="aa77a-178">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="aa77a-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="aa77a-179">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="aa77a-179">Sample response</span></span>

<span data-ttu-id="aa77a-180">これは、Newtonsoft.Json 9.0.1 の .nupkg であるバイナリ ストリーム。</span><span class="sxs-lookup"><span data-stu-id="aa77a-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="aa77a-181">パッケージ マニフェスト (.nuspec) をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="aa77a-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="aa77a-182">のみ、クライアントがパッケージ ID とバージョンを把握して、パッケージ マニフェストをダウンロードする場合は、それらを次の URL を構築する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa77a-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="aa77a-183">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="aa77a-183">Request parameters</span></span>

<span data-ttu-id="aa77a-184">name</span><span class="sxs-lookup"><span data-stu-id="aa77a-184">Name</span></span>          | <span data-ttu-id="aa77a-185">イン</span><span class="sxs-lookup"><span data-stu-id="aa77a-185">In</span></span>     | <span data-ttu-id="aa77a-186">型</span><span class="sxs-lookup"><span data-stu-id="aa77a-186">Type</span></span>    | <span data-ttu-id="aa77a-187">必須</span><span class="sxs-lookup"><span data-stu-id="aa77a-187">Required</span></span> | <span data-ttu-id="aa77a-188">メモ</span><span class="sxs-lookup"><span data-stu-id="aa77a-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="aa77a-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="aa77a-189">LOWER_ID</span></span>      | <span data-ttu-id="aa77a-190">URL</span><span class="sxs-lookup"><span data-stu-id="aa77a-190">URL</span></span>    | <span data-ttu-id="aa77a-191">string</span><span class="sxs-lookup"><span data-stu-id="aa77a-191">string</span></span>  | <span data-ttu-id="aa77a-192">可</span><span class="sxs-lookup"><span data-stu-id="aa77a-192">yes</span></span>      | <span data-ttu-id="aa77a-193">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="aa77a-193">The package ID, lowercase</span></span>
<span data-ttu-id="aa77a-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="aa77a-194">LOWER_VERSION</span></span> | <span data-ttu-id="aa77a-195">URL</span><span class="sxs-lookup"><span data-stu-id="aa77a-195">URL</span></span>    | <span data-ttu-id="aa77a-196">整数</span><span class="sxs-lookup"><span data-stu-id="aa77a-196">integer</span></span> | <span data-ttu-id="aa77a-197">可</span><span class="sxs-lookup"><span data-stu-id="aa77a-197">yes</span></span>      | <span data-ttu-id="aa77a-198">パッケージのバージョンが正規化され、小文字</span><span class="sxs-lookup"><span data-stu-id="aa77a-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="aa77a-199">両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用している小文字です。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。</span><span class="sxs-lookup"><span data-stu-id="aa77a-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="aa77a-200">`LOWER_VERSION`目的のパッケージのバージョンを使用して正規化 NuGet のバージョン[正規化規則](../reference/package-versioning.md#normalized-version-numbers)です。</span><span class="sxs-lookup"><span data-stu-id="aa77a-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="aa77a-201">つまり、SemVer 2.0.0 の仕様によって許可されているメタデータをビルドするをここでは除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="aa77a-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="aa77a-202">応答本文</span><span class="sxs-lookup"><span data-stu-id="aa77a-202">Response body</span></span>

<span data-ttu-id="aa77a-203">パッケージがパッケージ ソースに存在する場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="aa77a-204">応答本文は、パッケージ マニフェストでは、これは、対応する .nupkg に含まれている .nuspec になります。</span><span class="sxs-lookup"><span data-stu-id="aa77a-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="aa77a-205">.Nuspec は、XML ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="aa77a-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="aa77a-206">パッケージがパッケージ ソースに存在しない場合は、状態コード 404 が返されます。</span><span class="sxs-lookup"><span data-stu-id="aa77a-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="aa77a-207">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="aa77a-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="aa77a-208">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="aa77a-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
