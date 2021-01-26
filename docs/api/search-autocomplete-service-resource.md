---
title: オートコンプリート、NuGet API
description: 検索オートコンプリートサービスでは、パッケージ Id とバージョンの対話型検出がサポートされています。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773961"
---
# <a name="autocomplete"></a><span data-ttu-id="ebe06-103">オートコンプリート</span><span class="sxs-lookup"><span data-stu-id="ebe06-103">Autocomplete</span></span>

<span data-ttu-id="ebe06-104">V3 API を使用して、パッケージ ID とバージョンのオートコンプリートエクスペリエンスを構築することができます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="ebe06-105">オートコンプリートクエリを作成するために使用されるリソースは、 `SearchAutocompleteService` [サービスインデックス](service-index.md)で検出されたリソースです。</span><span class="sxs-lookup"><span data-stu-id="ebe06-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="ebe06-106">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="ebe06-106">Versioning</span></span>

<span data-ttu-id="ebe06-107">次の `@type` 値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-107">The following `@type` values are used:</span></span>

<span data-ttu-id="ebe06-108">@type 値</span><span class="sxs-lookup"><span data-stu-id="ebe06-108">@type value</span></span>                          | <span data-ttu-id="ebe06-109">Notes</span><span class="sxs-lookup"><span data-stu-id="ebe06-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="ebe06-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="ebe06-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="ebe06-111">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="ebe06-111">The initial release</span></span>
<span data-ttu-id="ebe06-112">SearchAutocompleteService/3.0.0-ベータ</span><span class="sxs-lookup"><span data-stu-id="ebe06-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="ebe06-113">エイリアス `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="ebe06-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="ebe06-114">SearchAutocompleteService/3.0.0</span><span class="sxs-lookup"><span data-stu-id="ebe06-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="ebe06-115">エイリアス `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="ebe06-115">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="ebe06-116">SearchAutocompleteService/3.5.0</span><span class="sxs-lookup"><span data-stu-id="ebe06-116">SearchAutocompleteService/3.5.0</span></span>      | <span data-ttu-id="ebe06-117">クエリパラメーターのサポートを含む `packageType`</span><span class="sxs-lookup"><span data-stu-id="ebe06-117">Includes support for `packageType` query parameter</span></span>

### <a name="searchautocompleteservice350"></a><span data-ttu-id="ebe06-118">SearchAutocompleteService/3.5.0</span><span class="sxs-lookup"><span data-stu-id="ebe06-118">SearchAutocompleteService/3.5.0</span></span>
<span data-ttu-id="ebe06-119">このバージョン `packageType` では、クエリパラメーターのサポートが導入されており、作成者が定義したパッケージの種類でフィルター処理できます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-119">This version introduces support for the `packageType` query parameter, allowing filtering by author defined package types.</span></span> <span data-ttu-id="ebe06-120">に対するクエリと完全に下位互換性が `SearchAutocompleteService` あります。</span><span class="sxs-lookup"><span data-stu-id="ebe06-120">It is fully backwards compatible with queries to `SearchAutocompleteService`.</span></span>

## <a name="base-url"></a><span data-ttu-id="ebe06-121">ベース URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-121">Base URL</span></span>

<span data-ttu-id="ebe06-122">次の Api のベース URL は、 `@id` 前述のいずれかのリソース値に関連付けられているプロパティの値です `@type` 。</span><span class="sxs-lookup"><span data-stu-id="ebe06-122">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="ebe06-123">次のドキュメントでは、プレースホルダーのベース URL `{@id}` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-123">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="ebe06-124">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="ebe06-124">HTTP Methods</span></span>

<span data-ttu-id="ebe06-125">登録リソースで見つかったすべての Url は、HTTP メソッドとをサポートして `GET` `HEAD` います。</span><span class="sxs-lookup"><span data-stu-id="ebe06-125">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="ebe06-126">パッケージ Id の検索</span><span class="sxs-lookup"><span data-stu-id="ebe06-126">Search for package IDs</span></span>

<span data-ttu-id="ebe06-127">最初のオートコンプリート API は、パッケージ ID 文字列の一部の検索をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ebe06-127">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="ebe06-128">これは、NuGet パッケージソースと統合されたユーザーインターフェイスで package 先行入力機能を提供する場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="ebe06-128">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="ebe06-129">一覧にないバージョンのみを含むパッケージは、結果に表示されません。</span><span class="sxs-lookup"><span data-stu-id="ebe06-129">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a><span data-ttu-id="ebe06-130">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="ebe06-130">Request parameters</span></span>

<span data-ttu-id="ebe06-131">名前</span><span class="sxs-lookup"><span data-stu-id="ebe06-131">Name</span></span>        | <span data-ttu-id="ebe06-132">/</span><span class="sxs-lookup"><span data-stu-id="ebe06-132">In</span></span>     | <span data-ttu-id="ebe06-133">Type</span><span class="sxs-lookup"><span data-stu-id="ebe06-133">Type</span></span>    | <span data-ttu-id="ebe06-134">必須</span><span class="sxs-lookup"><span data-stu-id="ebe06-134">Required</span></span> | <span data-ttu-id="ebe06-135">Notes</span><span class="sxs-lookup"><span data-stu-id="ebe06-135">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ebe06-136">q</span><span class="sxs-lookup"><span data-stu-id="ebe06-136">q</span></span>           | <span data-ttu-id="ebe06-137">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-137">URL</span></span>    | <span data-ttu-id="ebe06-138">string</span><span class="sxs-lookup"><span data-stu-id="ebe06-138">string</span></span>  | <span data-ttu-id="ebe06-139">no</span><span class="sxs-lookup"><span data-stu-id="ebe06-139">no</span></span>       | <span data-ttu-id="ebe06-140">パッケージ Id と比較する文字列</span><span class="sxs-lookup"><span data-stu-id="ebe06-140">The string to compare against package IDs</span></span>
<span data-ttu-id="ebe06-141">skip</span><span class="sxs-lookup"><span data-stu-id="ebe06-141">skip</span></span>        | <span data-ttu-id="ebe06-142">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-142">URL</span></span>    | <span data-ttu-id="ebe06-143">integer</span><span class="sxs-lookup"><span data-stu-id="ebe06-143">integer</span></span> | <span data-ttu-id="ebe06-144">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebe06-144">no</span></span>       | <span data-ttu-id="ebe06-145">改ページ位置の自動修正のためにスキップする結果の数</span><span class="sxs-lookup"><span data-stu-id="ebe06-145">The number of results to skip, for pagination</span></span>
<span data-ttu-id="ebe06-146">take</span><span class="sxs-lookup"><span data-stu-id="ebe06-146">take</span></span>        | <span data-ttu-id="ebe06-147">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-147">URL</span></span>    | <span data-ttu-id="ebe06-148">integer</span><span class="sxs-lookup"><span data-stu-id="ebe06-148">integer</span></span> | <span data-ttu-id="ebe06-149">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebe06-149">no</span></span>       | <span data-ttu-id="ebe06-150">改ページ位置の自動修正の対象となる結果の数</span><span class="sxs-lookup"><span data-stu-id="ebe06-150">The number of results to return, for pagination</span></span>
<span data-ttu-id="ebe06-151">リリース</span><span class="sxs-lookup"><span data-stu-id="ebe06-151">prerelease</span></span>  | <span data-ttu-id="ebe06-152">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-152">URL</span></span>    | <span data-ttu-id="ebe06-153">boolean</span><span class="sxs-lookup"><span data-stu-id="ebe06-153">boolean</span></span> | <span data-ttu-id="ebe06-154">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebe06-154">no</span></span>       | <span data-ttu-id="ebe06-155">`true`または `false` [プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する</span><span class="sxs-lookup"><span data-stu-id="ebe06-155">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ebe06-156">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ebe06-156">semVerLevel</span></span> | <span data-ttu-id="ebe06-157">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-157">URL</span></span>    | <span data-ttu-id="ebe06-158">string</span><span class="sxs-lookup"><span data-stu-id="ebe06-158">string</span></span>  | <span data-ttu-id="ebe06-159">no</span><span class="sxs-lookup"><span data-stu-id="ebe06-159">no</span></span>       | <span data-ttu-id="ebe06-160">SemVer 1.0.0 のバージョン文字列</span><span class="sxs-lookup"><span data-stu-id="ebe06-160">A SemVer 1.0.0 version string</span></span> 
<span data-ttu-id="ebe06-161">packageType</span><span class="sxs-lookup"><span data-stu-id="ebe06-161">packageType</span></span> | <span data-ttu-id="ebe06-162">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-162">URL</span></span>    | <span data-ttu-id="ebe06-163">string</span><span class="sxs-lookup"><span data-stu-id="ebe06-163">string</span></span>  | <span data-ttu-id="ebe06-164">no</span><span class="sxs-lookup"><span data-stu-id="ebe06-164">no</span></span>       | <span data-ttu-id="ebe06-165">パッケージをフィルター処理するために使用するパッケージの種類 (で追加 `SearchAutocompleteService/3.5.0` )</span><span class="sxs-lookup"><span data-stu-id="ebe06-165">The package type to use to filter packages (added in `SearchAutocompleteService/3.5.0`)</span></span>

<span data-ttu-id="ebe06-166">オートコンプリートクエリ `q` は、サーバー実装によって定義された方法で解析されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-166">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="ebe06-167">nuget.org では、パッケージ ID トークンのプレフィックスのクエリをサポートしています。これは、元の文字を camel 形式と記号で表現して生成された ID の一部です。</span><span class="sxs-lookup"><span data-stu-id="ebe06-167">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="ebe06-168">`skip`パラメーターの既定値は0です。</span><span class="sxs-lookup"><span data-stu-id="ebe06-168">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="ebe06-169">パラメーターには、 `take` 0 より大きい整数を指定してください。</span><span class="sxs-lookup"><span data-stu-id="ebe06-169">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="ebe06-170">サーバーの実装では、最大値が適用される場合があります。</span><span class="sxs-lookup"><span data-stu-id="ebe06-170">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="ebe06-171">が指定されて `prerelease` いない場合、プレリリースパッケージは除外されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-171">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ebe06-172">`semVerLevel`クエリパラメーターは、 [semver 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)にオプトインするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-172">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="ebe06-173">このクエリパラメーターを除外すると、SemVer 1.0.0 互換バージョンのパッケージ Id のみが返されます (4 つの整数部分を持つバージョン文字列など、NuGet のバージョン管理に関する [標準的](../concepts/package-versioning.md) な注意点があります)。</span><span class="sxs-lookup"><span data-stu-id="ebe06-173">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="ebe06-174">を指定した場合 `semVerLevel=2.0.0` 、semver 1.0.0 と semver 2.0.0 互換性のあるパッケージの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-174">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="ebe06-175">詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ebe06-175">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

<span data-ttu-id="ebe06-176">パラメーターを使用して、 `packageType` オートコンプリートの結果をさらにフィルター処理して、パッケージの種類名と一致するパッケージの種類が少なくとも1つあるパッケージのみを表示します。</span><span class="sxs-lookup"><span data-stu-id="ebe06-176">The `packageType` parameter is used to further filter the autocomplete results to only packages that have at least one package type matching the package type name.</span></span>
<span data-ttu-id="ebe06-177">指定されたパッケージの種類が、 [パッケージの種類のドキュメント](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)で定義されている有効なパッケージの種類ではない場合は、空の結果が返されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-177">If the provided package type is not a valid package type as defined by the [Package Type document](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D), an empty result will returned.</span></span>
<span data-ttu-id="ebe06-178">指定されたパッケージの種類が空の場合、フィルターは適用されません。</span><span class="sxs-lookup"><span data-stu-id="ebe06-178">If the provided package type is empty, no filter will be applied.</span></span> <span data-ttu-id="ebe06-179">つまり、パラメーターに値を渡さないと、パラメーターが渡されなかった `packageType` かのように動作します。</span><span class="sxs-lookup"><span data-stu-id="ebe06-179">In other words, passing no value to the `packageType` parameter will behave as if the parameter was not passed.</span></span>

### <a name="response"></a><span data-ttu-id="ebe06-180">応答</span><span class="sxs-lookup"><span data-stu-id="ebe06-180">Response</span></span>

<span data-ttu-id="ebe06-181">応答は、オートコンプリートの結果を含む JSON ドキュメントです `take` 。</span><span class="sxs-lookup"><span data-stu-id="ebe06-181">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="ebe06-182">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="ebe06-182">The root JSON object has the following properties:</span></span>

<span data-ttu-id="ebe06-183">名前</span><span class="sxs-lookup"><span data-stu-id="ebe06-183">Name</span></span>      | <span data-ttu-id="ebe06-184">Type</span><span class="sxs-lookup"><span data-stu-id="ebe06-184">Type</span></span>             | <span data-ttu-id="ebe06-185">必須</span><span class="sxs-lookup"><span data-stu-id="ebe06-185">Required</span></span> | <span data-ttu-id="ebe06-186">Notes</span><span class="sxs-lookup"><span data-stu-id="ebe06-186">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ebe06-187">totalHits</span><span class="sxs-lookup"><span data-stu-id="ebe06-187">totalHits</span></span> | <span data-ttu-id="ebe06-188">integer</span><span class="sxs-lookup"><span data-stu-id="ebe06-188">integer</span></span>          | <span data-ttu-id="ebe06-189">はい</span><span class="sxs-lookup"><span data-stu-id="ebe06-189">yes</span></span>      | <span data-ttu-id="ebe06-190">一致の合計数、無視 `skip` と `take`</span><span class="sxs-lookup"><span data-stu-id="ebe06-190">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="ebe06-191">data</span><span class="sxs-lookup"><span data-stu-id="ebe06-191">data</span></span>      | <span data-ttu-id="ebe06-192">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="ebe06-192">array of strings</span></span> | <span data-ttu-id="ebe06-193">はい</span><span class="sxs-lookup"><span data-stu-id="ebe06-193">yes</span></span>      | <span data-ttu-id="ebe06-194">要求に一致するパッケージ Id</span><span class="sxs-lookup"><span data-stu-id="ebe06-194">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="ebe06-195">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="ebe06-195">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="ebe06-196">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="ebe06-196">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="ebe06-197">パッケージバージョンの列挙</span><span class="sxs-lookup"><span data-stu-id="ebe06-197">Enumerate package versions</span></span>

<span data-ttu-id="ebe06-198">前の API を使用してパッケージ ID が検出されると、クライアントは autocomplete API を使用して、指定されたパッケージ ID のパッケージバージョンを列挙できます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-198">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="ebe06-199">一覧から削除されたパッケージのバージョンは、結果に表示されません。</span><span class="sxs-lookup"><span data-stu-id="ebe06-199">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="ebe06-200">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="ebe06-200">Request parameters</span></span>

<span data-ttu-id="ebe06-201">名前</span><span class="sxs-lookup"><span data-stu-id="ebe06-201">Name</span></span>        | <span data-ttu-id="ebe06-202">/</span><span class="sxs-lookup"><span data-stu-id="ebe06-202">In</span></span>     | <span data-ttu-id="ebe06-203">Type</span><span class="sxs-lookup"><span data-stu-id="ebe06-203">Type</span></span>    | <span data-ttu-id="ebe06-204">必須</span><span class="sxs-lookup"><span data-stu-id="ebe06-204">Required</span></span> | <span data-ttu-id="ebe06-205">Notes</span><span class="sxs-lookup"><span data-stu-id="ebe06-205">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="ebe06-206">id</span><span class="sxs-lookup"><span data-stu-id="ebe06-206">id</span></span>          | <span data-ttu-id="ebe06-207">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-207">URL</span></span>    | <span data-ttu-id="ebe06-208">string</span><span class="sxs-lookup"><span data-stu-id="ebe06-208">string</span></span>  | <span data-ttu-id="ebe06-209">はい</span><span class="sxs-lookup"><span data-stu-id="ebe06-209">yes</span></span>      | <span data-ttu-id="ebe06-210">バージョンをフェッチするパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="ebe06-210">The package ID to fetch versions for</span></span>
<span data-ttu-id="ebe06-211">リリース</span><span class="sxs-lookup"><span data-stu-id="ebe06-211">prerelease</span></span>  | <span data-ttu-id="ebe06-212">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-212">URL</span></span>    | <span data-ttu-id="ebe06-213">boolean</span><span class="sxs-lookup"><span data-stu-id="ebe06-213">boolean</span></span> | <span data-ttu-id="ebe06-214">いいえ</span><span class="sxs-lookup"><span data-stu-id="ebe06-214">no</span></span>       | <span data-ttu-id="ebe06-215">`true`または `false` [プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する</span><span class="sxs-lookup"><span data-stu-id="ebe06-215">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="ebe06-216">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="ebe06-216">semVerLevel</span></span> | <span data-ttu-id="ebe06-217">URL</span><span class="sxs-lookup"><span data-stu-id="ebe06-217">URL</span></span>    | <span data-ttu-id="ebe06-218">string</span><span class="sxs-lookup"><span data-stu-id="ebe06-218">string</span></span>  | <span data-ttu-id="ebe06-219">no</span><span class="sxs-lookup"><span data-stu-id="ebe06-219">no</span></span>       | <span data-ttu-id="ebe06-220">SemVer 2.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="ebe06-220">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="ebe06-221">が指定されて `prerelease` いない場合、プレリリースパッケージは除外されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-221">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="ebe06-222">`semVerLevel`クエリパラメーターは、SemVer 2.0.0 パッケージにオプトインするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-222">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="ebe06-223">このクエリパラメーターを除外すると、SemVer 1.0.0 のバージョンのみが返されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-223">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="ebe06-224">を指定した場合は `semVerLevel=2.0.0` 、semver 1.0.0 と semver 2.0.0 の両方のバージョンが返されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-224">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="ebe06-225">詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ebe06-225">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="ebe06-226">応答</span><span class="sxs-lookup"><span data-stu-id="ebe06-226">Response</span></span>

<span data-ttu-id="ebe06-227">応答は、指定されたパッケージ ID のすべてのパッケージバージョンを含む JSON ドキュメントで、指定されたクエリパラメーターによってフィルター処理されます。</span><span class="sxs-lookup"><span data-stu-id="ebe06-227">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="ebe06-228">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="ebe06-228">The root JSON object has the following property:</span></span>

<span data-ttu-id="ebe06-229">名前</span><span class="sxs-lookup"><span data-stu-id="ebe06-229">Name</span></span>      | <span data-ttu-id="ebe06-230">Type</span><span class="sxs-lookup"><span data-stu-id="ebe06-230">Type</span></span>             | <span data-ttu-id="ebe06-231">必須</span><span class="sxs-lookup"><span data-stu-id="ebe06-231">Required</span></span> | <span data-ttu-id="ebe06-232">Notes</span><span class="sxs-lookup"><span data-stu-id="ebe06-232">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="ebe06-233">data</span><span class="sxs-lookup"><span data-stu-id="ebe06-233">data</span></span>      | <span data-ttu-id="ebe06-234">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="ebe06-234">array of strings</span></span> | <span data-ttu-id="ebe06-235">はい</span><span class="sxs-lookup"><span data-stu-id="ebe06-235">yes</span></span>      | <span data-ttu-id="ebe06-236">要求に一致するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="ebe06-236">The package versions matched by the request</span></span>

<span data-ttu-id="ebe06-237">`data` `1.0.0+metadata` `semVerLevel=2.0.0` がクエリ文字列に指定されている場合、配列内のパッケージバージョンに semver 2.0.0 build メタデータ (など) が含まれている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ebe06-237">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="ebe06-238">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="ebe06-238">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="ebe06-239">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="ebe06-239">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
