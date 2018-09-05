---
title: オートコンプリートを NuGet API
description: 検索のオートコンプリートのサービスでは、パッケージ Id の対話型の検出とバージョンをサポートします。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 01f919dc3bbfb6752c8f8e055a3cd473ad194e75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549084"
---
# <a name="autocomplete"></a><span data-ttu-id="d5027-103">オートコンプリート</span><span class="sxs-lookup"><span data-stu-id="d5027-103">Autocomplete</span></span>

<span data-ttu-id="d5027-104">V3 API を使用してパッケージ ID とバージョンをオートコンプリート エクスペリエンス構築することになります。</span><span class="sxs-lookup"><span data-stu-id="d5027-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="d5027-105">オートコンプリート クエリを行うために使用されるリソースは、`SearchAutocompleteService`リソースで見つかった、[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="d5027-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="d5027-106">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="d5027-106">Versioning</span></span>

<span data-ttu-id="d5027-107">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5027-107">The following `@type` values are used:</span></span>

<span data-ttu-id="d5027-108">@type の値</span><span class="sxs-lookup"><span data-stu-id="d5027-108">@type value</span></span>                          | <span data-ttu-id="d5027-109">メモ</span><span class="sxs-lookup"><span data-stu-id="d5027-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="d5027-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="d5027-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="d5027-111">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="d5027-111">The initial release</span></span>
<span data-ttu-id="d5027-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="d5027-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="d5027-113">エイリアス `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d5027-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="d5027-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="d5027-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="d5027-115">エイリアス `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="d5027-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="d5027-116">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="d5027-116">Base URL</span></span>

<span data-ttu-id="d5027-117">次の Api のベース URL の値は、`@id`前述のリソースのいずれかに関連付けられているプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="d5027-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="d5027-118">次のドキュメントで、プレース ホルダーのベース URL`{@id}`使用されます。</span><span class="sxs-lookup"><span data-stu-id="d5027-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="d5027-119">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="d5027-119">HTTP Methods</span></span>

<span data-ttu-id="d5027-120">HTTP メソッドの登録のリソースのサポートで検出されたすべての Url`GET`と`HEAD`します。</span><span class="sxs-lookup"><span data-stu-id="d5027-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="d5027-121">パッケージ Id を検索</span><span class="sxs-lookup"><span data-stu-id="d5027-121">Search for package IDs</span></span>

<span data-ttu-id="d5027-122">最初のオートコンプリート API では、パッケージの ID 文字列の一部の検索をサポートします。</span><span class="sxs-lookup"><span data-stu-id="d5027-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="d5027-123">これは、操作は、NuGet パッケージのソースと統合ユーザー インターフェイスで、パッケージの先行入力機能を提供したい場合に優れたです。</span><span class="sxs-lookup"><span data-stu-id="d5027-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="d5027-124">一覧から削除されたバージョンのみを持つパッケージは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="d5027-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d5027-125">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="d5027-125">Request parameters</span></span>

<span data-ttu-id="d5027-126">名前</span><span class="sxs-lookup"><span data-stu-id="d5027-126">Name</span></span>        | <span data-ttu-id="d5027-127">イン</span><span class="sxs-lookup"><span data-stu-id="d5027-127">In</span></span>     | <span data-ttu-id="d5027-128">型</span><span class="sxs-lookup"><span data-stu-id="d5027-128">Type</span></span>    | <span data-ttu-id="d5027-129">必須</span><span class="sxs-lookup"><span data-stu-id="d5027-129">Required</span></span> | <span data-ttu-id="d5027-130">メモ</span><span class="sxs-lookup"><span data-stu-id="d5027-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d5027-131">q</span><span class="sxs-lookup"><span data-stu-id="d5027-131">q</span></span>           | <span data-ttu-id="d5027-132">URL</span><span class="sxs-lookup"><span data-stu-id="d5027-132">URL</span></span>    | <span data-ttu-id="d5027-133">string</span><span class="sxs-lookup"><span data-stu-id="d5027-133">string</span></span>  | <span data-ttu-id="d5027-134">Ｘ</span><span class="sxs-lookup"><span data-stu-id="d5027-134">no</span></span>       | <span data-ttu-id="d5027-135">パッケージ Id と比較する文字列</span><span class="sxs-lookup"><span data-stu-id="d5027-135">The string to compare against package IDs</span></span>
<span data-ttu-id="d5027-136">スキップ</span><span class="sxs-lookup"><span data-stu-id="d5027-136">skip</span></span>        | <span data-ttu-id="d5027-137">URL</span><span class="sxs-lookup"><span data-stu-id="d5027-137">URL</span></span>    | <span data-ttu-id="d5027-138">整数</span><span class="sxs-lookup"><span data-stu-id="d5027-138">integer</span></span> | <span data-ttu-id="d5027-139">Ｘ</span><span class="sxs-lookup"><span data-stu-id="d5027-139">no</span></span>       | <span data-ttu-id="d5027-140">改ページをスキップする結果の数</span><span class="sxs-lookup"><span data-stu-id="d5027-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="d5027-141">Take</span><span class="sxs-lookup"><span data-stu-id="d5027-141">take</span></span>        | <span data-ttu-id="d5027-142">URL</span><span class="sxs-lookup"><span data-stu-id="d5027-142">URL</span></span>    | <span data-ttu-id="d5027-143">整数</span><span class="sxs-lookup"><span data-stu-id="d5027-143">integer</span></span> | <span data-ttu-id="d5027-144">Ｘ</span><span class="sxs-lookup"><span data-stu-id="d5027-144">no</span></span>       | <span data-ttu-id="d5027-145">結果を返すには、改ページの数</span><span class="sxs-lookup"><span data-stu-id="d5027-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="d5027-146">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="d5027-146">prerelease</span></span>  | <span data-ttu-id="d5027-147">URL</span><span class="sxs-lookup"><span data-stu-id="d5027-147">URL</span></span>    | <span data-ttu-id="d5027-148">boolean</span><span class="sxs-lookup"><span data-stu-id="d5027-148">boolean</span></span> | <span data-ttu-id="d5027-149">Ｘ</span><span class="sxs-lookup"><span data-stu-id="d5027-149">no</span></span>       | <span data-ttu-id="d5027-150">`true` または`false`含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d5027-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d5027-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d5027-151">semVerLevel</span></span> | <span data-ttu-id="d5027-152">URL</span><span class="sxs-lookup"><span data-stu-id="d5027-152">URL</span></span>    | <span data-ttu-id="d5027-153">string</span><span class="sxs-lookup"><span data-stu-id="d5027-153">string</span></span>  | <span data-ttu-id="d5027-154">Ｘ</span><span class="sxs-lookup"><span data-stu-id="d5027-154">no</span></span>       | <span data-ttu-id="d5027-155">SemVer 1.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="d5027-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="d5027-156">オートコンプリート クエリ`q`サーバー実装で定義されている方法で解析されます。</span><span class="sxs-lookup"><span data-stu-id="d5027-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="d5027-157">nuget.org では、キャメル ケースと記号の文字で、元のパッケージ ID トークンは、ページの分割によって生成された ID の断片のプレフィックスにクエリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="d5027-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="d5027-158">`skip`パラメーターの既定値を 0 にします。</span><span class="sxs-lookup"><span data-stu-id="d5027-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="d5027-159">`take`パラメーターは 0 より大きい整数である必要があります。</span><span class="sxs-lookup"><span data-stu-id="d5027-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="d5027-160">サーバーの実装では、最大値をかける場合があります。</span><span class="sxs-lookup"><span data-stu-id="d5027-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="d5027-161">場合`prerelease`が提供されていない場合、プレリリース パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="d5027-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d5027-162">`semVerLevel`クエリ パラメーターの使用をオプトインする[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)します。</span><span class="sxs-lookup"><span data-stu-id="d5027-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="d5027-163">このクエリ パラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージ Id のみが返されます (で、 [NuGet バージョン管理の標準](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。</span><span class="sxs-lookup"><span data-stu-id="d5027-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="d5027-164">場合`semVerLevel=2.0.0`が指定されて、SemVer 1.0.0 および SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="d5027-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="d5027-165">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="d5027-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d5027-166">応答</span><span class="sxs-lookup"><span data-stu-id="d5027-166">Response</span></span>

<span data-ttu-id="d5027-167">応答は JSON ドキュメントを含む最大`take`オートコンプリートの結果。</span><span class="sxs-lookup"><span data-stu-id="d5027-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="d5027-168">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="d5027-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="d5027-169">名前</span><span class="sxs-lookup"><span data-stu-id="d5027-169">Name</span></span>      | <span data-ttu-id="d5027-170">種類</span><span class="sxs-lookup"><span data-stu-id="d5027-170">Type</span></span>             | <span data-ttu-id="d5027-171">必須</span><span class="sxs-lookup"><span data-stu-id="d5027-171">Required</span></span> | <span data-ttu-id="d5027-172">メモ</span><span class="sxs-lookup"><span data-stu-id="d5027-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d5027-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="d5027-173">totalHits</span></span> | <span data-ttu-id="d5027-174">整数</span><span class="sxs-lookup"><span data-stu-id="d5027-174">integer</span></span>          | <span data-ttu-id="d5027-175">可</span><span class="sxs-lookup"><span data-stu-id="d5027-175">yes</span></span>      | <span data-ttu-id="d5027-176">無視すると、一致の合計数`skip`と `take`</span><span class="sxs-lookup"><span data-stu-id="d5027-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="d5027-177">[データ]</span><span class="sxs-lookup"><span data-stu-id="d5027-177">data</span></span>      | <span data-ttu-id="d5027-178">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="d5027-178">array of strings</span></span> | <span data-ttu-id="d5027-179">可</span><span class="sxs-lookup"><span data-stu-id="d5027-179">yes</span></span>      | <span data-ttu-id="d5027-180">要求によって、パッケージ Id が一致します。</span><span class="sxs-lookup"><span data-stu-id="d5027-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="d5027-181">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="d5027-181">Sample request</span></span>

<span data-ttu-id="d5027-182">取得 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="d5027-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="d5027-183">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="d5027-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="d5027-184">パッケージのバージョンを列挙します。</span><span class="sxs-lookup"><span data-stu-id="d5027-184">Enumerate package versions</span></span>

<span data-ttu-id="d5027-185">以前の API を使用してパッケージ ID が検出されると、クライアントが指定されたパッケージ ID のパッケージのバージョンを列挙するのにオートコンプリート API を使用できます。</span><span class="sxs-lookup"><span data-stu-id="d5027-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="d5027-186">表示されているパッケージのバージョンは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="d5027-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="d5027-187">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="d5027-187">Request parameters</span></span>

<span data-ttu-id="d5027-188">名前</span><span class="sxs-lookup"><span data-stu-id="d5027-188">Name</span></span>        | <span data-ttu-id="d5027-189">イン</span><span class="sxs-lookup"><span data-stu-id="d5027-189">In</span></span>     | <span data-ttu-id="d5027-190">型</span><span class="sxs-lookup"><span data-stu-id="d5027-190">Type</span></span>    | <span data-ttu-id="d5027-191">必須</span><span class="sxs-lookup"><span data-stu-id="d5027-191">Required</span></span> | <span data-ttu-id="d5027-192">メモ</span><span class="sxs-lookup"><span data-stu-id="d5027-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="d5027-193">ID</span><span class="sxs-lookup"><span data-stu-id="d5027-193">id</span></span>          | <span data-ttu-id="d5027-194">URL</span><span class="sxs-lookup"><span data-stu-id="d5027-194">URL</span></span>    | <span data-ttu-id="d5027-195">string</span><span class="sxs-lookup"><span data-stu-id="d5027-195">string</span></span>  | <span data-ttu-id="d5027-196">可</span><span class="sxs-lookup"><span data-stu-id="d5027-196">yes</span></span>      | <span data-ttu-id="d5027-197">バージョンをフェッチするパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="d5027-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="d5027-198">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="d5027-198">prerelease</span></span>  | <span data-ttu-id="d5027-199">URL</span><span class="sxs-lookup"><span data-stu-id="d5027-199">URL</span></span>    | <span data-ttu-id="d5027-200">boolean</span><span class="sxs-lookup"><span data-stu-id="d5027-200">boolean</span></span> | <span data-ttu-id="d5027-201">Ｘ</span><span class="sxs-lookup"><span data-stu-id="d5027-201">no</span></span>       | <span data-ttu-id="d5027-202">`true` または`false`含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="d5027-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="d5027-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="d5027-203">semVerLevel</span></span> | <span data-ttu-id="d5027-204">URL</span><span class="sxs-lookup"><span data-stu-id="d5027-204">URL</span></span>    | <span data-ttu-id="d5027-205">string</span><span class="sxs-lookup"><span data-stu-id="d5027-205">string</span></span>  | <span data-ttu-id="d5027-206">Ｘ</span><span class="sxs-lookup"><span data-stu-id="d5027-206">no</span></span>       | <span data-ttu-id="d5027-207">SemVer 2.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="d5027-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="d5027-208">場合`prerelease`が提供されていない場合、プレリリース パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="d5027-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="d5027-209">`semVerLevel` SemVer 2.0.0 パッケージにオプトインするクエリ パラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="d5027-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="d5027-210">このクエリ パラメーターを含めない場合は、SemVer 1.0.0 バージョンのみが返されます。</span><span class="sxs-lookup"><span data-stu-id="d5027-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="d5027-211">場合`semVerLevel=2.0.0`が指定されて、SemVer 1.0.0 および SemVer 2.0.0 バージョンの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="d5027-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="d5027-212">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="d5027-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="d5027-213">応答</span><span class="sxs-lookup"><span data-stu-id="d5027-213">Response</span></span>

<span data-ttu-id="d5027-214">応答は、指定されたパッケージ ID は、指定されたクエリ パラメーターでフィルター処理のすべてのパッケージ バージョンを含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="d5027-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="d5027-215">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="d5027-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="d5027-216">名前</span><span class="sxs-lookup"><span data-stu-id="d5027-216">Name</span></span>      | <span data-ttu-id="d5027-217">種類</span><span class="sxs-lookup"><span data-stu-id="d5027-217">Type</span></span>             | <span data-ttu-id="d5027-218">必須</span><span class="sxs-lookup"><span data-stu-id="d5027-218">Required</span></span> | <span data-ttu-id="d5027-219">メモ</span><span class="sxs-lookup"><span data-stu-id="d5027-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="d5027-220">[データ]</span><span class="sxs-lookup"><span data-stu-id="d5027-220">data</span></span>      | <span data-ttu-id="d5027-221">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="d5027-221">array of strings</span></span> | <span data-ttu-id="d5027-222">可</span><span class="sxs-lookup"><span data-stu-id="d5027-222">yes</span></span>      | <span data-ttu-id="d5027-223">要求に一致するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="d5027-223">The package versions matched by the request</span></span>

<span data-ttu-id="d5027-224">パッケージのバージョンを`data`配列は SemVer 2.0.0 ビルド メタデータを含む可能性があります (例: `1.0.0+metadata`) 場合、`semVerLevel=2.0.0`クエリ文字列で提供されていた。</span><span class="sxs-lookup"><span data-stu-id="d5027-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="d5027-225">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="d5027-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="d5027-226">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="d5027-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
