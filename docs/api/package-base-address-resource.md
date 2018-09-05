---
title: NuGet API、パッケージの内容
description: パッケージのベース アドレスは、パッケージ自体を取得するための単純なインターフェイスです。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547155"
---
# <a name="package-content"></a><span data-ttu-id="765ae-103">パッケージのコンテンツ</span><span class="sxs-lookup"><span data-stu-id="765ae-103">Package Content</span></span>

<span data-ttu-id="765ae-104">V3 API を使用して、任意のパッケージのコンテンツ (.nupkg ファイル) をフェッチする URL を生成することになります。</span><span class="sxs-lookup"><span data-stu-id="765ae-104">It is possible to generate a URL to fetch an arbitrary package's content (the .nupkg file) using the V3 API.</span></span> <span data-ttu-id="765ae-105">パッケージのコンテンツを取得するために使用されるリソースは、`PackageBaseAddress`リソースで見つかった、[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="765ae-105">The resource used for fetching package content is the `PackageBaseAddress` resource found in the [service index](service-index.md).</span></span> <span data-ttu-id="765ae-106">このリソースも表示されているパッケージのすべてのバージョンの探索を有効にまたは一覧から削除されました。</span><span class="sxs-lookup"><span data-stu-id="765ae-106">This resource also enables discovery of all versions of a package, listed or unlisted.</span></span>

<span data-ttu-id="765ae-107">このリソースが、いずれかの"パッケージ ベース アドレスとして"または"フラット container"よくと呼ばれます。</span><span class="sxs-lookup"><span data-stu-id="765ae-107">This resource is commonly referred to as either the "package base address" or as the "flat container".</span></span>

## <a name="versioning"></a><span data-ttu-id="765ae-108">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="765ae-108">Versioning</span></span>

<span data-ttu-id="765ae-109">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="765ae-109">The following `@type` value is used:</span></span>

<span data-ttu-id="765ae-110">@type の値</span><span class="sxs-lookup"><span data-stu-id="765ae-110">@type value</span></span>              | <span data-ttu-id="765ae-111">メモ</span><span class="sxs-lookup"><span data-stu-id="765ae-111">Notes</span></span>
------------------------ | -----
<span data-ttu-id="765ae-112">PackageBaseAddress/3.0.0</span><span class="sxs-lookup"><span data-stu-id="765ae-112">PackageBaseAddress/3.0.0</span></span> | <span data-ttu-id="765ae-113">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="765ae-113">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="765ae-114">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="765ae-114">Base URL</span></span>

<span data-ttu-id="765ae-115">次の Api のベース URL の値は、`@id`前述のリソースに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="765ae-115">The base URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="765ae-116">次のドキュメントで、プレース ホルダーのベース URL`{@id}`使用されます。</span><span class="sxs-lookup"><span data-stu-id="765ae-116">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="765ae-117">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="765ae-117">HTTP methods</span></span>

<span data-ttu-id="765ae-118">HTTP メソッドの登録のリソースのサポートで検出されたすべての Url`GET`と`HEAD`します。</span><span class="sxs-lookup"><span data-stu-id="765ae-118">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="enumerate-package-versions"></a><span data-ttu-id="765ae-119">パッケージのバージョンを列挙します。</span><span class="sxs-lookup"><span data-stu-id="765ae-119">Enumerate package versions</span></span>

<span data-ttu-id="765ae-120">クライアントがパッケージ ID を知っているし、するパッケージのバージョンのパッケージを検出したい場合は、ソースで使用できるように、クライアントは、すべてのパッケージ バージョンを列挙するために予測可能な URL を構築できます。</span><span class="sxs-lookup"><span data-stu-id="765ae-120">If the client knows a package ID and wants to discover which package versions the package source has available, the client can construct a predictable URL to enumerate all package versions.</span></span> <span data-ttu-id="765ae-121">この一覧は「ディレクトリの一覧」をパッケージのコンテンツ api を以下に説明したもの。</span><span class="sxs-lookup"><span data-stu-id="765ae-121">This list is meant to be a "directory listing" for the package content API mentioned below.</span></span>

> [!Note]
> <span data-ttu-id="765ae-122">この一覧には、両方の一覧と一覧にないパッケージのバージョンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="765ae-122">This list contains both listed and unlisted package versions.</span></span>

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a><span data-ttu-id="765ae-123">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="765ae-123">Request parameters</span></span>

<span data-ttu-id="765ae-124">名前</span><span class="sxs-lookup"><span data-stu-id="765ae-124">Name</span></span>     | <span data-ttu-id="765ae-125">イン</span><span class="sxs-lookup"><span data-stu-id="765ae-125">In</span></span>     | <span data-ttu-id="765ae-126">型</span><span class="sxs-lookup"><span data-stu-id="765ae-126">Type</span></span>    | <span data-ttu-id="765ae-127">必須</span><span class="sxs-lookup"><span data-stu-id="765ae-127">Required</span></span> | <span data-ttu-id="765ae-128">メモ</span><span class="sxs-lookup"><span data-stu-id="765ae-128">Notes</span></span>
-------- | ------ | ------- | -------- | -----
<span data-ttu-id="765ae-129">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="765ae-129">LOWER_ID</span></span> | <span data-ttu-id="765ae-130">URL</span><span class="sxs-lookup"><span data-stu-id="765ae-130">URL</span></span>    | <span data-ttu-id="765ae-131">string</span><span class="sxs-lookup"><span data-stu-id="765ae-131">string</span></span>  | <span data-ttu-id="765ae-132">可</span><span class="sxs-lookup"><span data-stu-id="765ae-132">yes</span></span>      | <span data-ttu-id="765ae-133">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="765ae-133">The package ID, lowercase</span></span>

<span data-ttu-id="765ae-134">`LOWER_ID`値は小文字で実装されたルールを使用して、目的のパッケージ ID。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。</span><span class="sxs-lookup"><span data-stu-id="765ae-134">The `LOWER_ID` value is the desired package ID lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

### <a name="response"></a><span data-ttu-id="765ae-135">応答</span><span class="sxs-lookup"><span data-stu-id="765ae-135">Response</span></span>

<span data-ttu-id="765ae-136">指定されたパッケージ ID のバージョンのパッケージ ソースがない場合は、404 状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="765ae-136">If the package source has no versions of the provided package ID, a 404 status code is returned.</span></span>

<span data-ttu-id="765ae-137">パッケージ ソースに 1 つまたは複数のバージョンがある場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="765ae-137">If the package source has one or more versions, a 200 status code is returned.</span></span> <span data-ttu-id="765ae-138">応答本文では、次のプロパティを持つ JSON オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="765ae-138">The response body is a JSON object with the following property:</span></span>

<span data-ttu-id="765ae-139">名前</span><span class="sxs-lookup"><span data-stu-id="765ae-139">Name</span></span>     | <span data-ttu-id="765ae-140">種類</span><span class="sxs-lookup"><span data-stu-id="765ae-140">Type</span></span>             | <span data-ttu-id="765ae-141">必須</span><span class="sxs-lookup"><span data-stu-id="765ae-141">Required</span></span> | <span data-ttu-id="765ae-142">メモ</span><span class="sxs-lookup"><span data-stu-id="765ae-142">Notes</span></span>
-------- | ---------------- | -------- | -----
<span data-ttu-id="765ae-143">バージョン</span><span class="sxs-lookup"><span data-stu-id="765ae-143">versions</span></span> | <span data-ttu-id="765ae-144">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="765ae-144">array of strings</span></span> | <span data-ttu-id="765ae-145">可</span><span class="sxs-lookup"><span data-stu-id="765ae-145">yes</span></span>      | <span data-ttu-id="765ae-146">パッケージに使用できる Id</span><span class="sxs-lookup"><span data-stu-id="765ae-146">The package IDs available</span></span>

<span data-ttu-id="765ae-147">内の文字列、`versions`配列はすべて小文字、 [NuGet バージョン文字列を正規化](../reference/package-versioning.md#normalized-version-numbers)します。</span><span class="sxs-lookup"><span data-stu-id="765ae-147">The strings in the `versions` array are all lowercased, [normalized NuGet version strings](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="765ae-148">バージョン文字列では、SemVer 2.0.0 ビルド メタデータは含まれません。</span><span class="sxs-lookup"><span data-stu-id="765ae-148">The version strings do not contain any SemVer 2.0.0 build metadata.</span></span>

<span data-ttu-id="765ae-149">この配列内で見つかったバージョン文字列をそのまま使用できることが目的の`LOWER_VERSION`のトークンが、次のエンドポイント。</span><span class="sxs-lookup"><span data-stu-id="765ae-149">The intent is that the version strings found in this array can be used verbatim for the `LOWER_VERSION` tokens found in the following endpoints.</span></span>

### <a name="sample-request"></a><span data-ttu-id="765ae-150">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="765ae-150">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a><span data-ttu-id="765ae-151">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="765ae-151">Sample response</span></span>

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a><span data-ttu-id="765ae-152">パッケージ コンテンツ (.nupkg) のダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="765ae-152">Download package content (.nupkg)</span></span>

<span data-ttu-id="765ae-153">のみ、クライアントがパッケージ ID とバージョンを把握してパッケージ コンテンツをダウンロードする必要がある場合、次の URL を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="765ae-153">If the client knows a package ID and version and wants to download the package content, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a><span data-ttu-id="765ae-154">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="765ae-154">Request parameters</span></span>

<span data-ttu-id="765ae-155">名前</span><span class="sxs-lookup"><span data-stu-id="765ae-155">Name</span></span>          | <span data-ttu-id="765ae-156">イン</span><span class="sxs-lookup"><span data-stu-id="765ae-156">In</span></span>     | <span data-ttu-id="765ae-157">型</span><span class="sxs-lookup"><span data-stu-id="765ae-157">Type</span></span>   | <span data-ttu-id="765ae-158">必須</span><span class="sxs-lookup"><span data-stu-id="765ae-158">Required</span></span> | <span data-ttu-id="765ae-159">メモ</span><span class="sxs-lookup"><span data-stu-id="765ae-159">Notes</span></span>
------------- | ------ | ------ | -------- | -----
<span data-ttu-id="765ae-160">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="765ae-160">LOWER_ID</span></span>      | <span data-ttu-id="765ae-161">URL</span><span class="sxs-lookup"><span data-stu-id="765ae-161">URL</span></span>    | <span data-ttu-id="765ae-162">string</span><span class="sxs-lookup"><span data-stu-id="765ae-162">string</span></span> | <span data-ttu-id="765ae-163">可</span><span class="sxs-lookup"><span data-stu-id="765ae-163">yes</span></span>      | <span data-ttu-id="765ae-164">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="765ae-164">The package ID, lowercase</span></span>
<span data-ttu-id="765ae-165">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="765ae-165">LOWER_VERSION</span></span> | <span data-ttu-id="765ae-166">URL</span><span class="sxs-lookup"><span data-stu-id="765ae-166">URL</span></span>    | <span data-ttu-id="765ae-167">string</span><span class="sxs-lookup"><span data-stu-id="765ae-167">string</span></span> | <span data-ttu-id="765ae-168">可</span><span class="sxs-lookup"><span data-stu-id="765ae-168">yes</span></span>      | <span data-ttu-id="765ae-169">パッケージのバージョンが正規化され、小文字</span><span class="sxs-lookup"><span data-stu-id="765ae-169">The package version, normalized and lowercased</span></span>

<span data-ttu-id="765ae-170">両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用しては小文字です。NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span><span class="sxs-lookup"><span data-stu-id="765ae-170">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)</span></span>
<span data-ttu-id="765ae-171">メソッドをオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="765ae-171">method.</span></span>

<span data-ttu-id="765ae-172">`LOWER_VERSION`目的のパッケージ バージョン正規化は、NuGet のバージョンを使用して[正規化ルール](../reference/package-versioning.md#normalized-version-numbers)します。</span><span class="sxs-lookup"><span data-stu-id="765ae-172">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="765ae-173">つまり、SemVer 2.0.0 仕様によって許可されているビルド メタデータをここで除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="765ae-173">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="765ae-174">応答本文</span><span class="sxs-lookup"><span data-stu-id="765ae-174">Response body</span></span>

<span data-ttu-id="765ae-175">パッケージ ソースで、パッケージが存在する場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="765ae-175">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="765ae-176">応答本文は、パッケージ コンテンツ自体になります。</span><span class="sxs-lookup"><span data-stu-id="765ae-176">The response body will be the package content itself.</span></span>

<span data-ttu-id="765ae-177">パッケージ ソースのパッケージが存在しない場合は 404 状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="765ae-177">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="765ae-178">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="765ae-178">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a><span data-ttu-id="765ae-179">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="765ae-179">Sample response</span></span>

<span data-ttu-id="765ae-180">Newtonsoft.Json 9.0.1 の .nupkg をあるバイナリ ストリーム。</span><span class="sxs-lookup"><span data-stu-id="765ae-180">The binary stream that is the .nupkg for Newtonsoft.Json 9.0.1.</span></span>

## <a name="download-package-manifest-nuspec"></a><span data-ttu-id="765ae-181">パッケージ マニフェスト (.nuspec) のダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="765ae-181">Download package manifest (.nuspec)</span></span>

<span data-ttu-id="765ae-182">のみクライアントがパッケージ ID とバージョンを把握して、パッケージ マニフェストをダウンロードする場合、次の URL を作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="765ae-182">If the client knows a package ID and version and wants to download the package manifest, they only need to construct the following URL:</span></span>

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a><span data-ttu-id="765ae-183">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="765ae-183">Request parameters</span></span>

<span data-ttu-id="765ae-184">名前</span><span class="sxs-lookup"><span data-stu-id="765ae-184">Name</span></span>          | <span data-ttu-id="765ae-185">イン</span><span class="sxs-lookup"><span data-stu-id="765ae-185">In</span></span>     | <span data-ttu-id="765ae-186">型</span><span class="sxs-lookup"><span data-stu-id="765ae-186">Type</span></span>    | <span data-ttu-id="765ae-187">必須</span><span class="sxs-lookup"><span data-stu-id="765ae-187">Required</span></span> | <span data-ttu-id="765ae-188">メモ</span><span class="sxs-lookup"><span data-stu-id="765ae-188">Notes</span></span>
------------- | ------ | ------- | -------- | -----
<span data-ttu-id="765ae-189">LOWER_ID</span><span class="sxs-lookup"><span data-stu-id="765ae-189">LOWER_ID</span></span>      | <span data-ttu-id="765ae-190">URL</span><span class="sxs-lookup"><span data-stu-id="765ae-190">URL</span></span>    | <span data-ttu-id="765ae-191">string</span><span class="sxs-lookup"><span data-stu-id="765ae-191">string</span></span>  | <span data-ttu-id="765ae-192">可</span><span class="sxs-lookup"><span data-stu-id="765ae-192">yes</span></span>      | <span data-ttu-id="765ae-193">パッケージ ID、小文字</span><span class="sxs-lookup"><span data-stu-id="765ae-193">The package ID, lowercase</span></span>
<span data-ttu-id="765ae-194">LOWER_VERSION</span><span class="sxs-lookup"><span data-stu-id="765ae-194">LOWER_VERSION</span></span> | <span data-ttu-id="765ae-195">URL</span><span class="sxs-lookup"><span data-stu-id="765ae-195">URL</span></span>    | <span data-ttu-id="765ae-196">整数</span><span class="sxs-lookup"><span data-stu-id="765ae-196">integer</span></span> | <span data-ttu-id="765ae-197">可</span><span class="sxs-lookup"><span data-stu-id="765ae-197">yes</span></span>      | <span data-ttu-id="765ae-198">パッケージのバージョンが正規化され、小文字</span><span class="sxs-lookup"><span data-stu-id="765ae-198">The package version, normalized and lowercased</span></span>

<span data-ttu-id="765ae-199">両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用しては小文字です。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。</span><span class="sxs-lookup"><span data-stu-id="765ae-199">Both `LOWER_ID` and `LOWER_VERSION` are lowercased using the rules implemented by .NET's [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant) method.</span></span>

<span data-ttu-id="765ae-200">`LOWER_VERSION`目的のパッケージ バージョン正規化は、NuGet のバージョンを使用して[正規化ルール](../reference/package-versioning.md#normalized-version-numbers)します。</span><span class="sxs-lookup"><span data-stu-id="765ae-200">The `LOWER_VERSION` is the desired package version normalized using NuGet's version [normalization rules](../reference/package-versioning.md#normalized-version-numbers).</span></span> <span data-ttu-id="765ae-201">つまり、SemVer 2.0.0 仕様によって許可されているビルド メタデータをここで除外する必要があります。</span><span class="sxs-lookup"><span data-stu-id="765ae-201">This means that build metadata that is allowed by the SemVer 2.0.0 specification must be excluded in this case.</span></span>

### <a name="response-body"></a><span data-ttu-id="765ae-202">応答本文</span><span class="sxs-lookup"><span data-stu-id="765ae-202">Response body</span></span>

<span data-ttu-id="765ae-203">パッケージ ソースで、パッケージが存在する場合は、200 ステータス コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="765ae-203">If the package exists on the package source, a 200 status code is returned.</span></span> <span data-ttu-id="765ae-204">応答本文は、これは、対応する .nupkg に含まれている .nuspec パッケージ マニフェストになります。</span><span class="sxs-lookup"><span data-stu-id="765ae-204">The response body will be the package manifest, which is the .nuspec contained in the corresponding .nupkg.</span></span> <span data-ttu-id="765ae-205">.Nuspec は、XML ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="765ae-205">The .nuspec is an XML document.</span></span>

<span data-ttu-id="765ae-206">パッケージ ソースのパッケージが存在しない場合は 404 状態コードが返されます。</span><span class="sxs-lookup"><span data-stu-id="765ae-206">If the package does not exist on the package source, a 404 status code is returned.</span></span>

### <a name="sample-request"></a><span data-ttu-id="765ae-207">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="765ae-207">Sample request</span></span>

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a><span data-ttu-id="765ae-208">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="765ae-208">Sample response</span></span>

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
