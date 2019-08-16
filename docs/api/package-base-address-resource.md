---
title: パッケージコンテンツ, NuGet API
description: パッケージのベースアドレスは、パッケージ自体をフェッチするための単純なインターフェイスです。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 5ec6c0e17a3e8b9a3f156a48685bcaafe42c744b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488220"
---
# <a name="package-content"></a><span data-ttu-id="6ffb9-103">パッケージコンテンツ</span><span class="sxs-lookup"><span data-stu-id="6ffb9-103">Package Content</span></span>

<span data-ttu-id="6ffb9-104">V3 API を使用して、任意のパッケージのコンテンツ (nupkg ファイル) を取得するための URL を生成することができます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="6ffb9-105">パッケージコンテンツのフェッチに使用されるリソース`PackageBaseAddress`は、[サービスインデックス](service-index.md)で見つかったリソースです。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="6ffb9-106">また、このリソースにより、パッケージのすべてのバージョンの検出、一覧表示、または一覧からの削除が可能になります。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="6ffb9-107">このリソースは、一般に "パッケージベースアドレス" または "フラットコンテナー" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="6ffb9-108">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="6ffb9-108">Versioning</span></span>

<span data-ttu-id="6ffb9-109">次`@type`の値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-109">The following `@type` value is used:</span></span>

<span data-ttu-id="6ffb9-110">@type の値</span><span class="sxs-lookup"><span data-stu-id="6ffb9-110">@type value</span></span>              | <span data-ttu-id="6ffb9-111">メモ</span><span class="sxs-lookup"><span data-stu-id="6ffb9-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="6ffb9-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="6ffb9-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="6ffb9-113">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="6ffb9-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="6ffb9-114">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="6ffb9-114">Base URL</span></span>

<span data-ttu-id="6ffb9-115">次の api のベース URL は、前述のリソース`@id` `@type`値に関連付けられているプロパティの値です。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="6ffb9-116">次のドキュメントでは、プレースホルダーのベース`{@id}` URL が使用されます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="6ffb9-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="6ffb9-117">HTTP methods</span></span>

<span data-ttu-id="6ffb9-118">登録リソースで見つかったすべての url は、HTTP `GET`メソッド`HEAD`とをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="6ffb9-119">パッケージバージョンの列挙</span><span class="sxs-lookup"><span data-stu-id="6ffb9-119">Enumerate package versions</span></span>

<span data-ttu-id="6ffb9-120">クライアントがパッケージ ID を認識し、パッケージソースに使用可能なパッケージバージョンを検出する必要がある場合、クライアントは、すべてのパッケージバージョンを列挙するための予測可能な URL を作成できます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="6ffb9-121">このリストは、以下で説明するパッケージコンテンツ API の "ディレクトリリスト" として使用することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="6ffb9-122">この一覧には、一覧表示され、一覧にないパッケージバージョンの両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="6ffb9-123">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="6ffb9-123">Request parameters</span></span>

<span data-ttu-id="6ffb9-124">名前</span><span class="sxs-lookup"><span data-stu-id="6ffb9-124">Name</span></span>     | <span data-ttu-id="6ffb9-125">イン</span><span class="sxs-lookup"><span data-stu-id="6ffb9-125">In</span></span>     | <span data-ttu-id="6ffb9-126">型</span><span class="sxs-lookup"><span data-stu-id="6ffb9-126">Type</span></span>    | <span data-ttu-id="6ffb9-127">必須</span><span class="sxs-lookup"><span data-stu-id="6ffb9-127">Required</span></span> | <span data-ttu-id="6ffb9-128">メモ</span><span class="sxs-lookup"><span data-stu-id="6ffb9-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="6ffb9-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6ffb9-129">LOWER_ID</span></span> | <span data-ttu-id="6ffb9-130">URL</span><span class="sxs-lookup"><span data-stu-id="6ffb9-130">URL</span></span>    | <span data-ttu-id="6ffb9-131">string</span><span class="sxs-lookup"><span data-stu-id="6ffb9-131">string</span></span>  | <span data-ttu-id="6ffb9-132">可</span><span class="sxs-lookup"><span data-stu-id="6ffb9-132">yes</span></span>      | <span data-ttu-id="6ffb9-133">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="6ffb9-133">The package ID, lowercase</span></span>

<span data-ttu-id="6ffb9-134">この`LOWER_ID`値は、によって実装されたルールを使用して、必要なパッケージ ID を小文字にしたものです。NET の[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="6ffb9-135">応答</span><span class="sxs-lookup"><span data-stu-id="6ffb9-135">Response</span></span>

<span data-ttu-id="6ffb9-136">パッケージソースに提供されているパッケージ ID のバージョンがない場合は、404状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="6ffb9-137">パッケージソースに1つ以上のバージョンがある場合は、200状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="6ffb9-138">応答本文は、次のプロパティを持つ JSON オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="6ffb9-139">名前</span><span class="sxs-lookup"><span data-stu-id="6ffb9-139">Name</span></span>     | <span data-ttu-id="6ffb9-140">種類</span><span class="sxs-lookup"><span data-stu-id="6ffb9-140">Type</span></span>             | <span data-ttu-id="6ffb9-141">必須</span><span class="sxs-lookup"><span data-stu-id="6ffb9-141">Required</span></span> | <span data-ttu-id="6ffb9-142">メモ</span><span class="sxs-lookup"><span data-stu-id="6ffb9-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="6ffb9-143">versions</span><span class="sxs-lookup"><span data-stu-id="6ffb9-143">versions</span></span> | <span data-ttu-id="6ffb9-144">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="6ffb9-144">array of strings</span></span> | <span data-ttu-id="6ffb9-145">可</span><span class="sxs-lookup"><span data-stu-id="6ffb9-145">yes</span></span>      | <span data-ttu-id="6ffb9-146">使用可能なパッケージ Id</span><span class="sxs-lookup"><span data-stu-id="6ffb9-146">The package IDs available</span></span>

<span data-ttu-id="6ffb9-147">`versions`配列内の文字列は、すべて小文字で正規化された[NuGet バージョン文字列](../concepts/package-versioning.md#normalized-version-numbers)です。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6ffb9-148">バージョン文字列に SemVer 2.0.0 ビルドメタデータが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="6ffb9-149">目的は、この配列で見つかったバージョン文字列を、次のエンドポイントに`LOWER_VERSION`あるトークンに対して逐語的に使用できることです。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6ffb9-150">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6ffb9-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="6ffb9-151">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6ffb9-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="6ffb9-152">パッケージコンテンツのダウンロード (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="6ffb9-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="6ffb9-153">クライアントがパッケージ ID とバージョンを認識し、パッケージコンテンツをダウンロードする必要がある場合は、次の URL を構築するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="6ffb9-154">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="6ffb9-154">Request parameters</span></span>

<span data-ttu-id="6ffb9-155">名前</span><span class="sxs-lookup"><span data-stu-id="6ffb9-155">Name</span></span>          | <span data-ttu-id="6ffb9-156">イン</span><span class="sxs-lookup"><span data-stu-id="6ffb9-156">In</span></span>     | <span data-ttu-id="6ffb9-157">型</span><span class="sxs-lookup"><span data-stu-id="6ffb9-157">Type</span></span>   | <span data-ttu-id="6ffb9-158">必須</span><span class="sxs-lookup"><span data-stu-id="6ffb9-158">Required</span></span> | <span data-ttu-id="6ffb9-159">メモ</span><span class="sxs-lookup"><span data-stu-id="6ffb9-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6ffb9-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6ffb9-160">LOWER_ID</span></span>      | <span data-ttu-id="6ffb9-161">URL</span><span class="sxs-lookup"><span data-stu-id="6ffb9-161">URL</span></span>    | <span data-ttu-id="6ffb9-162">string</span><span class="sxs-lookup"><span data-stu-id="6ffb9-162">string</span></span> | <span data-ttu-id="6ffb9-163">可</span><span class="sxs-lookup"><span data-stu-id="6ffb9-163">yes</span></span>      | <span data-ttu-id="6ffb9-164">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="6ffb9-164">The package ID, lowercase</span></span>
<span data-ttu-id="6ffb9-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="6ffb9-165">LOWER_VERSION</span></span> | <span data-ttu-id="6ffb9-166">URL</span><span class="sxs-lookup"><span data-stu-id="6ffb9-166">URL</span></span>    | <span data-ttu-id="6ffb9-167">string</span><span class="sxs-lookup"><span data-stu-id="6ffb9-167">string</span></span> | <span data-ttu-id="6ffb9-168">可</span><span class="sxs-lookup"><span data-stu-id="6ffb9-168">yes</span></span>      | <span data-ttu-id="6ffb9-169">パッケージのバージョン、正規化、および小文字</span><span class="sxs-lookup"><span data-stu-id="6ffb9-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="6ffb9-170">`LOWER_ID` と`LOWER_VERSION`はどちらも、によって実装される規則を使用した小文字です。NET の[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="6ffb9-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="6ffb9-171">メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-171">method.</span></span>

<span data-ttu-id="6ffb9-172">は`LOWER_VERSION` 、NuGet のバージョン[正規化規則](../concepts/package-versioning.md#normalized-version-numbers)を使用して正規化された、必要なパッケージバージョンです。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6ffb9-173">これは、この場合、SemVer 2.0.0 仕様で許可されているビルドメタデータを除外する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="6ffb9-174">応答本文</span><span class="sxs-lookup"><span data-stu-id="6ffb9-174">Response body</span></span>

<span data-ttu-id="6ffb9-175">パッケージがパッケージソースに存在する場合は、200状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="6ffb9-176">応答本文は、パッケージコンテンツ自体になります。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="6ffb9-177">パッケージがパッケージソースに存在しない場合は、404状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6ffb9-178">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6ffb9-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="6ffb9-179">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6ffb9-179">Sample response</span></span>

<span data-ttu-id="6ffb9-180">. Nupkg (Newtonsoft. Json の 9.0.1) のバイナリストリーム。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="6ffb9-181">パッケージマニフェストのダウンロード (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="6ffb9-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="6ffb9-182">クライアントがパッケージ ID とバージョンを認識し、パッケージマニフェストをダウンロードする必要がある場合は、次の URL を構築するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="6ffb9-183">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="6ffb9-183">Request parameters</span></span>

<span data-ttu-id="6ffb9-184">名前</span><span class="sxs-lookup"><span data-stu-id="6ffb9-184">Name</span></span>          | <span data-ttu-id="6ffb9-185">イン</span><span class="sxs-lookup"><span data-stu-id="6ffb9-185">In</span></span>     | <span data-ttu-id="6ffb9-186">型</span><span class="sxs-lookup"><span data-stu-id="6ffb9-186">Type</span></span>   | <span data-ttu-id="6ffb9-187">必須</span><span class="sxs-lookup"><span data-stu-id="6ffb9-187">Required</span></span> | <span data-ttu-id="6ffb9-188">メモ</span><span class="sxs-lookup"><span data-stu-id="6ffb9-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="6ffb9-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="6ffb9-189">LOWER_ID</span></span>      | <span data-ttu-id="6ffb9-190">URL</span><span class="sxs-lookup"><span data-stu-id="6ffb9-190">URL</span></span>    | <span data-ttu-id="6ffb9-191">string</span><span class="sxs-lookup"><span data-stu-id="6ffb9-191">string</span></span> | <span data-ttu-id="6ffb9-192">可</span><span class="sxs-lookup"><span data-stu-id="6ffb9-192">yes</span></span>      | <span data-ttu-id="6ffb9-193">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="6ffb9-193">The package ID, lowercase</span></span>
<span data-ttu-id="6ffb9-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="6ffb9-194">LOWER_VERSION</span></span> | <span data-ttu-id="6ffb9-195">URL</span><span class="sxs-lookup"><span data-stu-id="6ffb9-195">URL</span></span>    | <span data-ttu-id="6ffb9-196">string</span><span class="sxs-lookup"><span data-stu-id="6ffb9-196">string</span></span> | <span data-ttu-id="6ffb9-197">可</span><span class="sxs-lookup"><span data-stu-id="6ffb9-197">yes</span></span>      | <span data-ttu-id="6ffb9-198">パッケージのバージョン、正規化、および小文字</span><span class="sxs-lookup"><span data-stu-id="6ffb9-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="6ffb9-199">`LOWER_ID` と`LOWER_VERSION`はどちらも、によって実装される規則を使用した小文字です。NET の[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="6ffb9-200">は`LOWER_VERSION` 、NuGet のバージョン[正規化規則](../concepts/package-versioning.md#normalized-version-numbers)を使用して正規化された、必要なパッケージバージョンです。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="6ffb9-201">これは、この場合、SemVer 2.0.0 仕様で許可されているビルドメタデータを除外する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="6ffb9-202">応答本文</span><span class="sxs-lookup"><span data-stu-id="6ffb9-202">Response body</span></span>

<span data-ttu-id="6ffb9-203">パッケージがパッケージソースに存在する場合は、200状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="6ffb9-204">応答本文はパッケージマニフェストになります。これは、対応する. nupkg に含まれている nuspec です。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="6ffb9-205">Nuspec は XML ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="6ffb9-206">パッケージがパッケージソースに存在しない場合は、404状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="6ffb9-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="6ffb9-207">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="6ffb9-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="6ffb9-208">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="6ffb9-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
