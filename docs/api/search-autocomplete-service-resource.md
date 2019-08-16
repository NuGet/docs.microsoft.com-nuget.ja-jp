---
title: オートコンプリート、NuGet API
description: 検索オートコンプリートサービスでは、パッケージ Id とバージョンの対話型検出がサポートされています。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488306"
---
# <a name="autocomplete"></a><span data-ttu-id="b5afa-103">オートコンプリート</span><span class="sxs-lookup"><span data-stu-id="b5afa-103">Autocomplete</span></span>

<span data-ttu-id="b5afa-104">V3 API を使用して、パッケージ ID とバージョンのオートコンプリートエクスペリエンスを構築することができます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="b5afa-105">オートコンプリートクエリを作成するために使用`SearchAutocompleteService`されるリソースは、[サービスインデックス](service-index.md)で検出されたリソースです。</span><span class="sxs-lookup"><span data-stu-id="b5afa-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="b5afa-106">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="b5afa-106">Versioning</span></span>

<span data-ttu-id="b5afa-107">次`@type`の値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-107">The following `@type` values are used:</span></span>

<span data-ttu-id="b5afa-108">@type の値</span><span class="sxs-lookup"><span data-stu-id="b5afa-108">@type value</span></span>                          | <span data-ttu-id="b5afa-109">メモ</span><span class="sxs-lookup"><span data-stu-id="b5afa-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="b5afa-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="b5afa-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="b5afa-111">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="b5afa-111">The initial release</span></span>
<span data-ttu-id="b5afa-112">SearchAutocompleteService/3.0.0-ベータ</span><span class="sxs-lookup"><span data-stu-id="b5afa-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="b5afa-113">エイリアス`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="b5afa-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="b5afa-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="b5afa-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="b5afa-115">エイリアス`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="b5afa-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="b5afa-116">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="b5afa-116">Base URL</span></span>

<span data-ttu-id="b5afa-117">次の api のベース URL は、前述のいずれか`@id`のリソース`@type`値に関連付けられているプロパティの値です。</span><span class="sxs-lookup"><span data-stu-id="b5afa-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="b5afa-118">次のドキュメントでは、プレースホルダーのベース`{@id}` URL が使用されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="b5afa-119">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="b5afa-119">HTTP Methods</span></span>

<span data-ttu-id="b5afa-120">登録リソースで見つかったすべての url は、HTTP `GET`メソッド`HEAD`とをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b5afa-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="b5afa-121">パッケージ Id の検索</span><span class="sxs-lookup"><span data-stu-id="b5afa-121">Search for package IDs</span></span>

<span data-ttu-id="b5afa-122">最初のオートコンプリート API は、パッケージ ID 文字列の一部の検索をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b5afa-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="b5afa-123">これは、NuGet パッケージソースと統合されたユーザーインターフェイスで package 先行入力機能を提供する場合に適しています。</span><span class="sxs-lookup"><span data-stu-id="b5afa-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="b5afa-124">一覧にないバージョンのみを含むパッケージは、結果に表示されません。</span><span class="sxs-lookup"><span data-stu-id="b5afa-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="b5afa-125">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="b5afa-125">Request parameters</span></span>

<span data-ttu-id="b5afa-126">名前</span><span class="sxs-lookup"><span data-stu-id="b5afa-126">Name</span></span>        | <span data-ttu-id="b5afa-127">イン</span><span class="sxs-lookup"><span data-stu-id="b5afa-127">In</span></span>     | <span data-ttu-id="b5afa-128">型</span><span class="sxs-lookup"><span data-stu-id="b5afa-128">Type</span></span>    | <span data-ttu-id="b5afa-129">必須</span><span class="sxs-lookup"><span data-stu-id="b5afa-129">Required</span></span> | <span data-ttu-id="b5afa-130">メモ</span><span class="sxs-lookup"><span data-stu-id="b5afa-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="b5afa-131">q</span><span class="sxs-lookup"><span data-stu-id="b5afa-131">q</span></span>           | <span data-ttu-id="b5afa-132">URL</span><span class="sxs-lookup"><span data-stu-id="b5afa-132">URL</span></span>    | <span data-ttu-id="b5afa-133">string</span><span class="sxs-lookup"><span data-stu-id="b5afa-133">string</span></span>  | <span data-ttu-id="b5afa-134">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b5afa-134">no</span></span>       | <span data-ttu-id="b5afa-135">パッケージ Id と比較する文字列</span><span class="sxs-lookup"><span data-stu-id="b5afa-135">The string to compare against package IDs</span></span>
<span data-ttu-id="b5afa-136">skip</span><span class="sxs-lookup"><span data-stu-id="b5afa-136">skip</span></span>        | <span data-ttu-id="b5afa-137">URL</span><span class="sxs-lookup"><span data-stu-id="b5afa-137">URL</span></span>    | <span data-ttu-id="b5afa-138">integer</span><span class="sxs-lookup"><span data-stu-id="b5afa-138">integer</span></span> | <span data-ttu-id="b5afa-139">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b5afa-139">no</span></span>       | <span data-ttu-id="b5afa-140">改ページ位置の自動修正のためにスキップする結果の数</span><span class="sxs-lookup"><span data-stu-id="b5afa-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="b5afa-141">take</span><span class="sxs-lookup"><span data-stu-id="b5afa-141">take</span></span>        | <span data-ttu-id="b5afa-142">URL</span><span class="sxs-lookup"><span data-stu-id="b5afa-142">URL</span></span>    | <span data-ttu-id="b5afa-143">integer</span><span class="sxs-lookup"><span data-stu-id="b5afa-143">integer</span></span> | <span data-ttu-id="b5afa-144">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b5afa-144">no</span></span>       | <span data-ttu-id="b5afa-145">改ページ位置の自動修正の対象となる結果の数</span><span class="sxs-lookup"><span data-stu-id="b5afa-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="b5afa-146">prerelease</span><span class="sxs-lookup"><span data-stu-id="b5afa-146">prerelease</span></span>  | <span data-ttu-id="b5afa-147">URL</span><span class="sxs-lookup"><span data-stu-id="b5afa-147">URL</span></span>    | <span data-ttu-id="b5afa-148">boolean</span><span class="sxs-lookup"><span data-stu-id="b5afa-148">boolean</span></span> | <span data-ttu-id="b5afa-149">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b5afa-149">no</span></span>       | <span data-ttu-id="b5afa-150">`true`また`false`は[プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する</span><span class="sxs-lookup"><span data-stu-id="b5afa-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="b5afa-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="b5afa-151">semVerLevel</span></span> | <span data-ttu-id="b5afa-152">URL</span><span class="sxs-lookup"><span data-stu-id="b5afa-152">URL</span></span>    | <span data-ttu-id="b5afa-153">string</span><span class="sxs-lookup"><span data-stu-id="b5afa-153">string</span></span>  | <span data-ttu-id="b5afa-154">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b5afa-154">no</span></span>       | <span data-ttu-id="b5afa-155">SemVer 1.0.0 のバージョン文字列</span><span class="sxs-lookup"><span data-stu-id="b5afa-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="b5afa-156">オートコンプリートクエリ`q`は、サーバー実装によって定義された方法で解析されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="b5afa-157">nuget.org では、パッケージ ID トークンのプレフィックスのクエリをサポートしています。これは、元の文字を camel 形式と記号で表現して生成された ID の一部です。</span><span class="sxs-lookup"><span data-stu-id="b5afa-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="b5afa-158">パラメーター `skip`の既定値は0です。</span><span class="sxs-lookup"><span data-stu-id="b5afa-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="b5afa-159">パラメーター `take`には、0より大きい整数を指定してください。</span><span class="sxs-lookup"><span data-stu-id="b5afa-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="b5afa-160">サーバーの実装では、最大値が適用される場合があります。</span><span class="sxs-lookup"><span data-stu-id="b5afa-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="b5afa-161">が`prerelease`指定されていない場合、プレリリースパッケージは除外されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="b5afa-162">クエリ`semVerLevel`パラメーターは、 [semver 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)にオプトインするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="b5afa-163">このクエリパラメーターを除外すると、SemVer 1.0.0 互換バージョンのパッケージ Id のみが返されます (4 つの整数部分を持つバージョン文字列など、NuGet のバージョン管理に関する[標準的](../concepts/package-versioning.md)な注意点があります)。</span><span class="sxs-lookup"><span data-stu-id="b5afa-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../concepts/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="b5afa-164">を`semVerLevel=2.0.0`指定した場合、semver 1.0.0 と semver 2.0.0 互換性のあるパッケージの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="b5afa-165">詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b5afa-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="b5afa-166">応答</span><span class="sxs-lookup"><span data-stu-id="b5afa-166">Response</span></span>

<span data-ttu-id="b5afa-167">応答は、オートコンプリートの結果を`take`含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="b5afa-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="b5afa-168">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="b5afa-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="b5afa-169">名前</span><span class="sxs-lookup"><span data-stu-id="b5afa-169">Name</span></span>      | <span data-ttu-id="b5afa-170">種類</span><span class="sxs-lookup"><span data-stu-id="b5afa-170">Type</span></span>             | <span data-ttu-id="b5afa-171">必須</span><span class="sxs-lookup"><span data-stu-id="b5afa-171">Required</span></span> | <span data-ttu-id="b5afa-172">メモ</span><span class="sxs-lookup"><span data-stu-id="b5afa-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="b5afa-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="b5afa-173">totalHits</span></span> | <span data-ttu-id="b5afa-174">integer</span><span class="sxs-lookup"><span data-stu-id="b5afa-174">integer</span></span>          | <span data-ttu-id="b5afa-175">可</span><span class="sxs-lookup"><span data-stu-id="b5afa-175">yes</span></span>      | <span data-ttu-id="b5afa-176">一致の合計数、無視`skip`と`take`</span><span class="sxs-lookup"><span data-stu-id="b5afa-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="b5afa-177">data</span><span class="sxs-lookup"><span data-stu-id="b5afa-177">data</span></span>      | <span data-ttu-id="b5afa-178">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="b5afa-178">array of strings</span></span> | <span data-ttu-id="b5afa-179">可</span><span class="sxs-lookup"><span data-stu-id="b5afa-179">yes</span></span>      | <span data-ttu-id="b5afa-180">要求に一致するパッケージ Id</span><span class="sxs-lookup"><span data-stu-id="b5afa-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="b5afa-181">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="b5afa-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="b5afa-182">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="b5afa-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="b5afa-183">パッケージバージョンの列挙</span><span class="sxs-lookup"><span data-stu-id="b5afa-183">Enumerate package versions</span></span>

<span data-ttu-id="b5afa-184">前の API を使用してパッケージ ID が検出されると、クライアントは autocomplete API を使用して、指定されたパッケージ ID のパッケージバージョンを列挙できます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="b5afa-185">一覧から削除されたパッケージのバージョンは、結果に表示されません。</span><span class="sxs-lookup"><span data-stu-id="b5afa-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="b5afa-186">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="b5afa-186">Request parameters</span></span>

<span data-ttu-id="b5afa-187">名前</span><span class="sxs-lookup"><span data-stu-id="b5afa-187">Name</span></span>        | <span data-ttu-id="b5afa-188">イン</span><span class="sxs-lookup"><span data-stu-id="b5afa-188">In</span></span>     | <span data-ttu-id="b5afa-189">型</span><span class="sxs-lookup"><span data-stu-id="b5afa-189">Type</span></span>    | <span data-ttu-id="b5afa-190">必須</span><span class="sxs-lookup"><span data-stu-id="b5afa-190">Required</span></span> | <span data-ttu-id="b5afa-191">メモ</span><span class="sxs-lookup"><span data-stu-id="b5afa-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="b5afa-192">id</span><span class="sxs-lookup"><span data-stu-id="b5afa-192">id</span></span>          | <span data-ttu-id="b5afa-193">URL</span><span class="sxs-lookup"><span data-stu-id="b5afa-193">URL</span></span>    | <span data-ttu-id="b5afa-194">string</span><span class="sxs-lookup"><span data-stu-id="b5afa-194">string</span></span>  | <span data-ttu-id="b5afa-195">可</span><span class="sxs-lookup"><span data-stu-id="b5afa-195">yes</span></span>      | <span data-ttu-id="b5afa-196">バージョンをフェッチするパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="b5afa-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="b5afa-197">prerelease</span><span class="sxs-lookup"><span data-stu-id="b5afa-197">prerelease</span></span>  | <span data-ttu-id="b5afa-198">URL</span><span class="sxs-lookup"><span data-stu-id="b5afa-198">URL</span></span>    | <span data-ttu-id="b5afa-199">boolean</span><span class="sxs-lookup"><span data-stu-id="b5afa-199">boolean</span></span> | <span data-ttu-id="b5afa-200">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b5afa-200">no</span></span>       | <span data-ttu-id="b5afa-201">`true`また`false`は[プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する</span><span class="sxs-lookup"><span data-stu-id="b5afa-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="b5afa-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="b5afa-202">semVerLevel</span></span> | <span data-ttu-id="b5afa-203">URL</span><span class="sxs-lookup"><span data-stu-id="b5afa-203">URL</span></span>    | <span data-ttu-id="b5afa-204">string</span><span class="sxs-lookup"><span data-stu-id="b5afa-204">string</span></span>  | <span data-ttu-id="b5afa-205">Ｘ</span><span class="sxs-lookup"><span data-stu-id="b5afa-205">no</span></span>       | <span data-ttu-id="b5afa-206">SemVer 2.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="b5afa-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="b5afa-207">が`prerelease`指定されていない場合、プレリリースパッケージは除外されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="b5afa-208">クエリ`semVerLevel`パラメーターは、semver 2.0.0 パッケージにオプトインするために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="b5afa-209">このクエリパラメーターを除外すると、SemVer 1.0.0 のバージョンのみが返されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="b5afa-210">を`semVerLevel=2.0.0`指定した場合は、semver 1.0.0 と semver 2.0.0 の両方のバージョンが返されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="b5afa-211">詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b5afa-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="b5afa-212">応答</span><span class="sxs-lookup"><span data-stu-id="b5afa-212">Response</span></span>

<span data-ttu-id="b5afa-213">応答は、指定されたパッケージ ID のすべてのパッケージバージョンを含む JSON ドキュメントで、指定されたクエリパラメーターによってフィルター処理されます。</span><span class="sxs-lookup"><span data-stu-id="b5afa-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="b5afa-214">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="b5afa-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="b5afa-215">Name</span><span class="sxs-lookup"><span data-stu-id="b5afa-215">Name</span></span>      | <span data-ttu-id="b5afa-216">種類</span><span class="sxs-lookup"><span data-stu-id="b5afa-216">Type</span></span>             | <span data-ttu-id="b5afa-217">必須</span><span class="sxs-lookup"><span data-stu-id="b5afa-217">Required</span></span> | <span data-ttu-id="b5afa-218">メモ</span><span class="sxs-lookup"><span data-stu-id="b5afa-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="b5afa-219">data</span><span class="sxs-lookup"><span data-stu-id="b5afa-219">data</span></span>      | <span data-ttu-id="b5afa-220">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="b5afa-220">array of strings</span></span> | <span data-ttu-id="b5afa-221">可</span><span class="sxs-lookup"><span data-stu-id="b5afa-221">yes</span></span>      | <span data-ttu-id="b5afa-222">要求に一致するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="b5afa-222">The package versions matched by the request</span></span>

<span data-ttu-id="b5afa-223">がクエリ文字列に指定`data`されている場合、配列内のパッケージバージョン`1.0.0+metadata`に semver 2.0.0 build メタデータ (など) が含まれている可能性があります。 `semVerLevel=2.0.0`</span><span class="sxs-lookup"><span data-stu-id="b5afa-223">The package versions in the `data` array may contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` is provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="b5afa-224">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="b5afa-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="b5afa-225">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="b5afa-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
