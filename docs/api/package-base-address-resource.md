---
title: パッケージコンテンツ, NuGet API
description: パッケージのベースアドレスは、パッケージ自体をフェッチするための単純なインターフェイスです。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 8ea03ece635aa06e22032c4fb43ce932dbdf717c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773936"
---
# <a name="package-content"></a><span data-ttu-id="fe553-103">パッケージの内容</span><span class="sxs-lookup"><span data-stu-id="fe553-103">Package Content</span></span>

<span data-ttu-id="fe553-104">V3 API を使用して、任意のパッケージのコンテンツ (nupkg ファイル) を取得するための URL を生成することができます。</span><span class="sxs-lookup"><span data-stu-id="fe553-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="fe553-105">パッケージコンテンツのフェッチに使用されるリソースは、 `PackageBaseAddress` [サービスインデックス](service-index.md)で見つかったリソースです。</span><span class="sxs-lookup"><span data-stu-id="fe553-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="fe553-106">また、このリソースにより、パッケージのすべてのバージョンの検出、一覧表示、または一覧からの削除が可能になります。</span><span class="sxs-lookup"><span data-stu-id="fe553-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="fe553-107">このリソースは、一般に "パッケージベースアドレス" または "フラットコンテナー" と呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="fe553-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="fe553-108">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="fe553-108">Versioning</span></span>

<span data-ttu-id="fe553-109">次の `@type` 値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="fe553-109">The following `@type` value is used:</span></span>

<span data-ttu-id="fe553-110">@type 値</span><span class="sxs-lookup"><span data-stu-id="fe553-110">@type value</span></span>              | <span data-ttu-id="fe553-111">Notes</span><span class="sxs-lookup"><span data-stu-id="fe553-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="fe553-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="fe553-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="fe553-113">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="fe553-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="fe553-114">ベース URL</span><span class="sxs-lookup"><span data-stu-id="fe553-114">Base URL</span></span>

<span data-ttu-id="fe553-115">次の Api のベース URL は、 `@id` 前述のリソース値に関連付けられているプロパティの値です `@type` 。</span><span class="sxs-lookup"><span data-stu-id="fe553-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="fe553-116">次のドキュメントでは、プレースホルダーのベース URL `{@id}` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="fe553-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="fe553-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="fe553-117">HTTP methods</span></span>

<span data-ttu-id="fe553-118">登録リソースで見つかったすべての Url は、HTTP メソッドとをサポートして `GET` `HEAD` います。</span><span class="sxs-lookup"><span data-stu-id="fe553-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="fe553-119">パッケージバージョンの列挙</span><span class="sxs-lookup"><span data-stu-id="fe553-119">Enumerate package versions</span></span>

<span data-ttu-id="fe553-120">クライアントがパッケージ ID を認識し、パッケージソースに使用可能なパッケージバージョンを検出する必要がある場合、クライアントは、すべてのパッケージバージョンを列挙するための予測可能な URL を作成できます。</span><span class="sxs-lookup"><span data-stu-id="fe553-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="fe553-121">このリストは、以下で説明するパッケージコンテンツ API の "ディレクトリリスト" として使用することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="fe553-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="fe553-122">この一覧には、一覧表示され、一覧にないパッケージバージョンの両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="fe553-122">This list contains both listed and unlisted package versions.</span></span>

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a><span data-ttu-id="fe553-123">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="fe553-123">Request parameters</span></span>

<span data-ttu-id="fe553-124">名前</span><span class="sxs-lookup"><span data-stu-id="fe553-124">Name</span></span>     | <span data-ttu-id="fe553-125">/</span><span class="sxs-lookup"><span data-stu-id="fe553-125">In</span></span>     | <span data-ttu-id="fe553-126">Type</span><span class="sxs-lookup"><span data-stu-id="fe553-126">Type</span></span>    | <span data-ttu-id="fe553-127">必須</span><span class="sxs-lookup"><span data-stu-id="fe553-127">Required</span></span> | <span data-ttu-id="fe553-128">Notes</span><span class="sxs-lookup"><span data-stu-id="fe553-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="fe553-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="fe553-129">LOWER_ID</span></span> | <span data-ttu-id="fe553-130">URL</span><span class="sxs-lookup"><span data-stu-id="fe553-130">URL</span></span>    | <span data-ttu-id="fe553-131">string</span><span class="sxs-lookup"><span data-stu-id="fe553-131">string</span></span>  | <span data-ttu-id="fe553-132">はい</span><span class="sxs-lookup"><span data-stu-id="fe553-132">yes</span></span>      | <span data-ttu-id="fe553-133">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="fe553-133">The package ID, lowercased</span></span>

<span data-ttu-id="fe553-134">この `LOWER_ID` 値は、によって実装されたルールを使用して、必要なパッケージ ID を小文字にしたものです。NET の [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) メソッド。</span><span class="sxs-lookup"><span data-stu-id="fe553-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

### <a name="response"></a><span data-ttu-id="fe553-135">応答</span><span class="sxs-lookup"><span data-stu-id="fe553-135">Response</span></span>

<span data-ttu-id="fe553-136">パッケージソースに提供されているパッケージ ID のバージョンがない場合は、404状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="fe553-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="fe553-137">パッケージソースに1つ以上のバージョンがある場合は、200状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="fe553-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="fe553-138">応答本文は、次のプロパティを持つ JSON オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="fe553-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="fe553-139">名前</span><span class="sxs-lookup"><span data-stu-id="fe553-139">Name</span></span>     | <span data-ttu-id="fe553-140">Type</span><span class="sxs-lookup"><span data-stu-id="fe553-140">Type</span></span>             | <span data-ttu-id="fe553-141">必須</span><span class="sxs-lookup"><span data-stu-id="fe553-141">Required</span></span> | <span data-ttu-id="fe553-142">Notes</span><span class="sxs-lookup"><span data-stu-id="fe553-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="fe553-143">versions</span><span class="sxs-lookup"><span data-stu-id="fe553-143">versions</span></span> | <span data-ttu-id="fe553-144">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="fe553-144">array of strings</span></span> | <span data-ttu-id="fe553-145">はい</span><span class="sxs-lookup"><span data-stu-id="fe553-145">yes</span></span>      | <span data-ttu-id="fe553-146">使用可能なバージョン</span><span class="sxs-lookup"><span data-stu-id="fe553-146">The versions available</span></span>

<span data-ttu-id="fe553-147">配列内の文字列 `versions` は、すべて小文字で正規化された [NuGet バージョン文字列](../concepts/package-versioning.md#normalized-version-numbers)です。</span><span class="sxs-lookup"><span data-stu-id="fe553-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="fe553-148">バージョン文字列に SemVer 2.0.0 ビルドメタデータが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="fe553-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="fe553-149">目的は、この配列で見つかったバージョン文字列を、 `LOWER_VERSION` 次のエンドポイントにあるトークンに対して逐語的に使用できることです。</span><span class="sxs-lookup"><span data-stu-id="fe553-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="fe553-150">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="fe553-150">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/owin/index.json
```

### <a name="sample-response"></a><span data-ttu-id="fe553-151">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="fe553-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="fe553-152">パッケージコンテンツのダウンロード (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="fe553-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="fe553-153">クライアントがパッケージ ID とバージョンを認識し、パッケージコンテンツをダウンロードする必要がある場合は、次の URL を構築するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="fe553-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg
```

### <a name="request-parameters"></a><span data-ttu-id="fe553-154">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="fe553-154">Request parameters</span></span>

<span data-ttu-id="fe553-155">名前</span><span class="sxs-lookup"><span data-stu-id="fe553-155">Name</span></span>          | <span data-ttu-id="fe553-156">/</span><span class="sxs-lookup"><span data-stu-id="fe553-156">In</span></span>     | <span data-ttu-id="fe553-157">Type</span><span class="sxs-lookup"><span data-stu-id="fe553-157">Type</span></span>   | <span data-ttu-id="fe553-158">必須</span><span class="sxs-lookup"><span data-stu-id="fe553-158">Required</span></span> | <span data-ttu-id="fe553-159">Notes</span><span class="sxs-lookup"><span data-stu-id="fe553-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="fe553-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="fe553-160">LOWER_ID</span></span>      | <span data-ttu-id="fe553-161">URL</span><span class="sxs-lookup"><span data-stu-id="fe553-161">URL</span></span>    | <span data-ttu-id="fe553-162">string</span><span class="sxs-lookup"><span data-stu-id="fe553-162">string</span></span> | <span data-ttu-id="fe553-163">はい</span><span class="sxs-lookup"><span data-stu-id="fe553-163">yes</span></span>      | <span data-ttu-id="fe553-164">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="fe553-164">The package ID, lowercase</span></span>
<span data-ttu-id="fe553-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="fe553-165">LOWER_VERSION</span></span> | <span data-ttu-id="fe553-166">URL</span><span class="sxs-lookup"><span data-stu-id="fe553-166">URL</span></span>    | <span data-ttu-id="fe553-167">string</span><span class="sxs-lookup"><span data-stu-id="fe553-167">string</span></span> | <span data-ttu-id="fe553-168">はい</span><span class="sxs-lookup"><span data-stu-id="fe553-168">yes</span></span>      | <span data-ttu-id="fe553-169">パッケージのバージョン、正規化、および小文字</span><span class="sxs-lookup"><span data-stu-id="fe553-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="fe553-170">とはどちらも、 `LOWER_ID` `LOWER_VERSION` によって実装される規則を使用した小文字です。NET の [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="fe553-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true)</span></span>
<span data-ttu-id="fe553-171">メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="fe553-171">method.</span></span>

<span data-ttu-id="fe553-172">は、 `LOWER_VERSION` NuGet のバージョン [正規化規則](../concepts/package-versioning.md#normalized-version-numbers)を使用して正規化された、必要なパッケージバージョンです。</span><span class="sxs-lookup"><span data-stu-id="fe553-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="fe553-173">これは、この場合、SemVer 2.0.0 仕様で許可されているビルドメタデータを除外する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="fe553-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="fe553-174">応答本文</span><span class="sxs-lookup"><span data-stu-id="fe553-174">Response body</span></span>

<span data-ttu-id="fe553-175">パッケージがパッケージソースに存在する場合は、200状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="fe553-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="fe553-176">応答本文は、パッケージコンテンツ自体になります。</span><span class="sxs-lookup"><span data-stu-id="fe553-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="fe553-177">パッケージがパッケージソースに存在しない場合は、404状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="fe553-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="fe553-178">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="fe553-178">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg
```

### <a name="sample-response"></a><span data-ttu-id="fe553-179">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="fe553-179">Sample response</span></span>

<span data-ttu-id="fe553-180">9.0.1 上の Newtonsoft.Jsのの nupkg のバイナリストリーム。</span><span class="sxs-lookup"><span data-stu-id="fe553-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="fe553-181">パッケージマニフェストのダウンロード (. nuspec)</span><span class="sxs-lookup"><span data-stu-id="fe553-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="fe553-182">クライアントがパッケージ ID とバージョンを認識し、パッケージマニフェストをダウンロードする必要がある場合は、次の URL を構築するだけで済みます。</span><span class="sxs-lookup"><span data-stu-id="fe553-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

```
GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec
```

### <a name="request-parameters"></a><span data-ttu-id="fe553-183">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="fe553-183">Request parameters</span></span>

<span data-ttu-id="fe553-184">名前</span><span class="sxs-lookup"><span data-stu-id="fe553-184">Name</span></span>          | <span data-ttu-id="fe553-185">/</span><span class="sxs-lookup"><span data-stu-id="fe553-185">In</span></span>     | <span data-ttu-id="fe553-186">Type</span><span class="sxs-lookup"><span data-stu-id="fe553-186">Type</span></span>   | <span data-ttu-id="fe553-187">必須</span><span class="sxs-lookup"><span data-stu-id="fe553-187">Required</span></span> | <span data-ttu-id="fe553-188">Notes</span><span class="sxs-lookup"><span data-stu-id="fe553-188">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="fe553-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="fe553-189">LOWER_ID</span></span>      | <span data-ttu-id="fe553-190">URL</span><span class="sxs-lookup"><span data-stu-id="fe553-190">URL</span></span>    | <span data-ttu-id="fe553-191">string</span><span class="sxs-lookup"><span data-stu-id="fe553-191">string</span></span> | <span data-ttu-id="fe553-192">はい</span><span class="sxs-lookup"><span data-stu-id="fe553-192">yes</span></span>      | <span data-ttu-id="fe553-193">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="fe553-193">The package ID, lowercase</span></span>
<span data-ttu-id="fe553-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="fe553-194">LOWER_VERSION</span></span> | <span data-ttu-id="fe553-195">URL</span><span class="sxs-lookup"><span data-stu-id="fe553-195">URL</span></span>    | <span data-ttu-id="fe553-196">string</span><span class="sxs-lookup"><span data-stu-id="fe553-196">string</span></span> | <span data-ttu-id="fe553-197">はい</span><span class="sxs-lookup"><span data-stu-id="fe553-197">yes</span></span>      | <span data-ttu-id="fe553-198">パッケージのバージョン、正規化、および小文字</span><span class="sxs-lookup"><span data-stu-id="fe553-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="fe553-199">とはどちらも、 `LOWER_ID` `LOWER_VERSION` によって実装される規則を使用した小文字です。NET の [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) メソッド。</span><span class="sxs-lookup"><span data-stu-id="fe553-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant&preserve-view=true) method.</span></span>

<span data-ttu-id="fe553-200">は、 `LOWER_VERSION` NuGet のバージョン [正規化規則](../concepts/package-versioning.md#normalized-version-numbers)を使用して正規化された、必要なパッケージバージョンです。</span><span class="sxs-lookup"><span data-stu-id="fe553-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../concepts/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="fe553-201">これは、この場合、SemVer 2.0.0 仕様で許可されているビルドメタデータを除外する必要があることを意味します。</span><span class="sxs-lookup"><span data-stu-id="fe553-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="fe553-202">応答本文</span><span class="sxs-lookup"><span data-stu-id="fe553-202">Response body</span></span>

<span data-ttu-id="fe553-203">パッケージがパッケージソースに存在する場合は、200状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="fe553-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="fe553-204">応答本文はパッケージマニフェストになります。これは、対応する. nupkg に含まれている nuspec です。</span><span class="sxs-lookup"><span data-stu-id="fe553-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="fe553-205">Nuspec は XML ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="fe553-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="fe553-206">パッケージがパッケージソースに存在しない場合は、404状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="fe553-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="fe553-207">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="fe553-207">Sample request</span></span>

```
GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec
```

### <a name="sample-response"></a><span data-ttu-id="fe553-208">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="fe553-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
