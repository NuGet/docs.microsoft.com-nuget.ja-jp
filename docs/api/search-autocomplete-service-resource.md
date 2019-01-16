---
title: オートコンプリートを NuGet API
description: 検索のオートコンプリートのサービスでは、パッケージ Id の対話型の検出とバージョンをサポートします。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2d2b20c1ea439ec0a3225cf983d9a4d2eedb0333
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324761"
---
# <a name="autocomplete"></a><span data-ttu-id="f3a0b-103">オートコンプリート</span><span class="sxs-lookup"><span data-stu-id="f3a0b-103">Autocomplete</span></span>

<span data-ttu-id="f3a0b-104">V3 API を使用してパッケージ ID とバージョンをオートコンプリート エクスペリエンス構築することになります。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="f3a0b-105">オートコンプリート クエリを行うために使用されるリソースは、`SearchAutocompleteService`リソースで見つかった、[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="f3a0b-106">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="f3a0b-106">Versioning</span></span>

<span data-ttu-id="f3a0b-107">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-107">The following `@type` values are used:</span></span>

<span data-ttu-id="f3a0b-108">@type の値</span><span class="sxs-lookup"><span data-stu-id="f3a0b-108">@type value</span></span>                          | <span data-ttu-id="f3a0b-109">メモ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="f3a0b-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="f3a0b-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="f3a0b-111">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="f3a0b-111">The initial release</span></span>
<span data-ttu-id="f3a0b-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="f3a0b-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="f3a0b-113">エイリアス `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="f3a0b-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="f3a0b-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="f3a0b-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="f3a0b-115">エイリアス `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="f3a0b-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="f3a0b-116">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="f3a0b-116">Base URL</span></span>

<span data-ttu-id="f3a0b-117">次の Api のベース URL の値は、`@id`前述のリソースのいずれかに関連付けられているプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="f3a0b-118">次のドキュメントで、プレース ホルダーのベース URL`{@id}`使用されます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="f3a0b-119">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="f3a0b-119">HTTP Methods</span></span>

<span data-ttu-id="f3a0b-120">HTTP メソッドの登録のリソースのサポートで検出されたすべての Url`GET`と`HEAD`します。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="f3a0b-121">パッケージ Id を検索</span><span class="sxs-lookup"><span data-stu-id="f3a0b-121">Search for package IDs</span></span>

<span data-ttu-id="f3a0b-122">最初のオートコンプリート API では、パッケージの ID 文字列の一部の検索をサポートします。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="f3a0b-123">これは、操作は、NuGet パッケージのソースと統合ユーザー インターフェイスで、パッケージの先行入力機能を提供したい場合に優れたです。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="f3a0b-124">一覧から削除されたバージョンのみを持つパッケージは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="f3a0b-125">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="f3a0b-125">Request parameters</span></span>

<span data-ttu-id="f3a0b-126">名前</span><span class="sxs-lookup"><span data-stu-id="f3a0b-126">Name</span></span>        | <span data-ttu-id="f3a0b-127">イン</span><span class="sxs-lookup"><span data-stu-id="f3a0b-127">In</span></span>     | <span data-ttu-id="f3a0b-128">型</span><span class="sxs-lookup"><span data-stu-id="f3a0b-128">Type</span></span>    | <span data-ttu-id="f3a0b-129">必須</span><span class="sxs-lookup"><span data-stu-id="f3a0b-129">Required</span></span> | <span data-ttu-id="f3a0b-130">メモ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="f3a0b-131">q</span><span class="sxs-lookup"><span data-stu-id="f3a0b-131">q</span></span>           | <span data-ttu-id="f3a0b-132">URL</span><span class="sxs-lookup"><span data-stu-id="f3a0b-132">URL</span></span>    | <span data-ttu-id="f3a0b-133">string</span><span class="sxs-lookup"><span data-stu-id="f3a0b-133">string</span></span>  | <span data-ttu-id="f3a0b-134">Ｘ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-134">no</span></span>       | <span data-ttu-id="f3a0b-135">パッケージ Id と比較する文字列</span><span class="sxs-lookup"><span data-stu-id="f3a0b-135">The string to compare against package IDs</span></span>
<span data-ttu-id="f3a0b-136">スキップ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-136">skip</span></span>        | <span data-ttu-id="f3a0b-137">URL</span><span class="sxs-lookup"><span data-stu-id="f3a0b-137">URL</span></span>    | <span data-ttu-id="f3a0b-138">整数</span><span class="sxs-lookup"><span data-stu-id="f3a0b-138">integer</span></span> | <span data-ttu-id="f3a0b-139">Ｘ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-139">no</span></span>       | <span data-ttu-id="f3a0b-140">改ページをスキップする結果の数</span><span class="sxs-lookup"><span data-stu-id="f3a0b-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="f3a0b-141">Take</span><span class="sxs-lookup"><span data-stu-id="f3a0b-141">take</span></span>        | <span data-ttu-id="f3a0b-142">URL</span><span class="sxs-lookup"><span data-stu-id="f3a0b-142">URL</span></span>    | <span data-ttu-id="f3a0b-143">整数</span><span class="sxs-lookup"><span data-stu-id="f3a0b-143">integer</span></span> | <span data-ttu-id="f3a0b-144">Ｘ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-144">no</span></span>       | <span data-ttu-id="f3a0b-145">結果を返すには、改ページの数</span><span class="sxs-lookup"><span data-stu-id="f3a0b-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="f3a0b-146">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="f3a0b-146">prerelease</span></span>  | <span data-ttu-id="f3a0b-147">URL</span><span class="sxs-lookup"><span data-stu-id="f3a0b-147">URL</span></span>    | <span data-ttu-id="f3a0b-148">boolean</span><span class="sxs-lookup"><span data-stu-id="f3a0b-148">boolean</span></span> | <span data-ttu-id="f3a0b-149">Ｘ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-149">no</span></span>       | <span data-ttu-id="f3a0b-150">`true` または`false`含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="f3a0b-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="f3a0b-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="f3a0b-151">semVerLevel</span></span> | <span data-ttu-id="f3a0b-152">URL</span><span class="sxs-lookup"><span data-stu-id="f3a0b-152">URL</span></span>    | <span data-ttu-id="f3a0b-153">string</span><span class="sxs-lookup"><span data-stu-id="f3a0b-153">string</span></span>  | <span data-ttu-id="f3a0b-154">Ｘ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-154">no</span></span>       | <span data-ttu-id="f3a0b-155">SemVer 1.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="f3a0b-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="f3a0b-156">オートコンプリート クエリ`q`サーバー実装で定義されている方法で解析されます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="f3a0b-157">nuget.org では、キャメル ケースと記号の文字で、元のパッケージ ID トークンは、ページの分割によって生成された ID の断片のプレフィックスにクエリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="f3a0b-158">`skip`パラメーターの既定値を 0 にします。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="f3a0b-159">`take`パラメーターは 0 より大きい整数である必要があります。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="f3a0b-160">サーバーの実装では、最大値をかける場合があります。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="f3a0b-161">場合`prerelease`が提供されていない場合、プレリリース パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="f3a0b-162">`semVerLevel`クエリ パラメーターの使用をオプトインする[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)します。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="f3a0b-163">このクエリ パラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージ Id のみが返されます (で、 [NuGet バージョン管理の標準](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="f3a0b-164">場合`semVerLevel=2.0.0`が指定されて、SemVer 1.0.0 および SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="f3a0b-165">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="f3a0b-166">応答</span><span class="sxs-lookup"><span data-stu-id="f3a0b-166">Response</span></span>

<span data-ttu-id="f3a0b-167">応答は JSON ドキュメントを含む最大`take`オートコンプリートの結果。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="f3a0b-168">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="f3a0b-169">名前</span><span class="sxs-lookup"><span data-stu-id="f3a0b-169">Name</span></span>      | <span data-ttu-id="f3a0b-170">種類</span><span class="sxs-lookup"><span data-stu-id="f3a0b-170">Type</span></span>             | <span data-ttu-id="f3a0b-171">必須</span><span class="sxs-lookup"><span data-stu-id="f3a0b-171">Required</span></span> | <span data-ttu-id="f3a0b-172">メモ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="f3a0b-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="f3a0b-173">totalHits</span></span> | <span data-ttu-id="f3a0b-174">整数</span><span class="sxs-lookup"><span data-stu-id="f3a0b-174">integer</span></span>          | <span data-ttu-id="f3a0b-175">可</span><span class="sxs-lookup"><span data-stu-id="f3a0b-175">yes</span></span>      | <span data-ttu-id="f3a0b-176">無視すると、一致の合計数`skip`と `take`</span><span class="sxs-lookup"><span data-stu-id="f3a0b-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="f3a0b-177">[データ]</span><span class="sxs-lookup"><span data-stu-id="f3a0b-177">data</span></span>      | <span data-ttu-id="f3a0b-178">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="f3a0b-178">array of strings</span></span> | <span data-ttu-id="f3a0b-179">可</span><span class="sxs-lookup"><span data-stu-id="f3a0b-179">yes</span></span>      | <span data-ttu-id="f3a0b-180">要求によって、パッケージ Id が一致します。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="f3a0b-181">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="f3a0b-181">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="f3a0b-182">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="f3a0b-182">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="f3a0b-183">パッケージのバージョンを列挙します。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-183">Enumerate package versions</span></span>

<span data-ttu-id="f3a0b-184">以前の API を使用してパッケージ ID が検出されると、クライアントが指定されたパッケージ ID のパッケージのバージョンを列挙するのにオートコンプリート API を使用できます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-184">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="f3a0b-185">表示されているパッケージのバージョンは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-185">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="f3a0b-186">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="f3a0b-186">Request parameters</span></span>

<span data-ttu-id="f3a0b-187">名前</span><span class="sxs-lookup"><span data-stu-id="f3a0b-187">Name</span></span>        | <span data-ttu-id="f3a0b-188">イン</span><span class="sxs-lookup"><span data-stu-id="f3a0b-188">In</span></span>     | <span data-ttu-id="f3a0b-189">型</span><span class="sxs-lookup"><span data-stu-id="f3a0b-189">Type</span></span>    | <span data-ttu-id="f3a0b-190">必須</span><span class="sxs-lookup"><span data-stu-id="f3a0b-190">Required</span></span> | <span data-ttu-id="f3a0b-191">メモ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-191">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="f3a0b-192">ID</span><span class="sxs-lookup"><span data-stu-id="f3a0b-192">id</span></span>          | <span data-ttu-id="f3a0b-193">URL</span><span class="sxs-lookup"><span data-stu-id="f3a0b-193">URL</span></span>    | <span data-ttu-id="f3a0b-194">string</span><span class="sxs-lookup"><span data-stu-id="f3a0b-194">string</span></span>  | <span data-ttu-id="f3a0b-195">可</span><span class="sxs-lookup"><span data-stu-id="f3a0b-195">yes</span></span>      | <span data-ttu-id="f3a0b-196">バージョンをフェッチするパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="f3a0b-196">The package ID to fetch versions for</span></span>
<span data-ttu-id="f3a0b-197">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="f3a0b-197">prerelease</span></span>  | <span data-ttu-id="f3a0b-198">URL</span><span class="sxs-lookup"><span data-stu-id="f3a0b-198">URL</span></span>    | <span data-ttu-id="f3a0b-199">boolean</span><span class="sxs-lookup"><span data-stu-id="f3a0b-199">boolean</span></span> | <span data-ttu-id="f3a0b-200">Ｘ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-200">no</span></span>       | <span data-ttu-id="f3a0b-201">`true` または`false`含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="f3a0b-201">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="f3a0b-202">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="f3a0b-202">semVerLevel</span></span> | <span data-ttu-id="f3a0b-203">URL</span><span class="sxs-lookup"><span data-stu-id="f3a0b-203">URL</span></span>    | <span data-ttu-id="f3a0b-204">string</span><span class="sxs-lookup"><span data-stu-id="f3a0b-204">string</span></span>  | <span data-ttu-id="f3a0b-205">Ｘ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-205">no</span></span>       | <span data-ttu-id="f3a0b-206">A SemVer 2.0.0 version string</span><span class="sxs-lookup"><span data-stu-id="f3a0b-206">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="f3a0b-207">場合`prerelease`が提供されていない場合、プレリリース パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-207">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="f3a0b-208">`semVerLevel` SemVer 2.0.0 パッケージにオプトインするクエリ パラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-208">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="f3a0b-209">このクエリ パラメーターを含めない場合は、SemVer 1.0.0 バージョンのみが返されます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-209">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="f3a0b-210">場合`semVerLevel=2.0.0`が指定されて、SemVer 1.0.0 および SemVer 2.0.0 バージョンの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-210">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="f3a0b-211">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-211">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="f3a0b-212">応答</span><span class="sxs-lookup"><span data-stu-id="f3a0b-212">Response</span></span>

<span data-ttu-id="f3a0b-213">応答は、指定されたパッケージ ID は、指定されたクエリ パラメーターでフィルター処理のすべてのパッケージ バージョンを含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-213">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="f3a0b-214">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-214">The root JSON object has the following property:</span></span>

<span data-ttu-id="f3a0b-215">名前</span><span class="sxs-lookup"><span data-stu-id="f3a0b-215">Name</span></span>      | <span data-ttu-id="f3a0b-216">種類</span><span class="sxs-lookup"><span data-stu-id="f3a0b-216">Type</span></span>             | <span data-ttu-id="f3a0b-217">必須</span><span class="sxs-lookup"><span data-stu-id="f3a0b-217">Required</span></span> | <span data-ttu-id="f3a0b-218">メモ</span><span class="sxs-lookup"><span data-stu-id="f3a0b-218">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="f3a0b-219">[データ]</span><span class="sxs-lookup"><span data-stu-id="f3a0b-219">data</span></span>      | <span data-ttu-id="f3a0b-220">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="f3a0b-220">array of strings</span></span> | <span data-ttu-id="f3a0b-221">可</span><span class="sxs-lookup"><span data-stu-id="f3a0b-221">yes</span></span>      | <span data-ttu-id="f3a0b-222">要求に一致するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="f3a0b-222">The package versions matched by the request</span></span>

<span data-ttu-id="f3a0b-223">パッケージのバージョンを`data`配列は SemVer 2.0.0 ビルド メタデータを含む可能性があります (例: `1.0.0+metadata`) 場合、`semVerLevel=2.0.0`クエリ文字列で提供されていた。</span><span class="sxs-lookup"><span data-stu-id="f3a0b-223">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="f3a0b-224">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="f3a0b-224">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="f3a0b-225">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="f3a0b-225">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
