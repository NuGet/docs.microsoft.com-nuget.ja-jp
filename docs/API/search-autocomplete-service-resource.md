---
title: "オートコンプリートは、NuGet API |Microsoft ドキュメント"
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
description: "検索のオートコンプリート機能のサービスは、パッケージ Id の対話型の検出とバージョンをサポートします。"
keywords: "NuGet のオートコンプリート機能の API では、NuGet パッケージ ID、パッケージ ID の部分文字列を検索します。"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 7c984ca61799293d7832851b80cf3fefc4734288
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="autocomplete"></a><span data-ttu-id="e94d8-104">オートコンプリート</span><span class="sxs-lookup"><span data-stu-id="e94d8-104">Autocomplete</span></span>

<span data-ttu-id="e94d8-105">パッケージ ID とバージョン オートコンプリート エクスペリエンスを V3 API を使用して行うことができます。</span><span class="sxs-lookup"><span data-stu-id="e94d8-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="e94d8-106">オートコンプリート クエリを実行するためのシステム リソースが、`SearchAutocompleteService`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="e94d8-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="e94d8-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="e94d8-107">Versioning</span></span>

<span data-ttu-id="e94d8-108">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="e94d8-108">The following `@type` values are used:</span></span>

<span data-ttu-id="e94d8-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="e94d8-109">@type value</span></span>                          | <span data-ttu-id="e94d8-110">メモ</span><span class="sxs-lookup"><span data-stu-id="e94d8-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="e94d8-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="e94d8-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="e94d8-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="e94d8-112">The initial release</span></span>
<span data-ttu-id="e94d8-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="e94d8-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="e94d8-114">エイリアス`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e94d8-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="e94d8-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="e94d8-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="e94d8-116">エイリアス`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="e94d8-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="e94d8-117">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="e94d8-117">Base URL</span></span>

<span data-ttu-id="e94d8-118">次の Api のベース URL の値、`@id`前述のリソースのいずれかに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="e94d8-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="e94d8-119">次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。</span><span class="sxs-lookup"><span data-stu-id="e94d8-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e94d8-120">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="e94d8-120">HTTP Methods</span></span>

<span data-ttu-id="e94d8-121">HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。</span><span class="sxs-lookup"><span data-stu-id="e94d8-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="e94d8-122">パッケージ Id を検索</span><span class="sxs-lookup"><span data-stu-id="e94d8-122">Search for package IDs</span></span>

<span data-ttu-id="e94d8-123">最初のオートコンプリート機能 API は、パッケージ ID 文字列の一部の検索をサポートします。</span><span class="sxs-lookup"><span data-stu-id="e94d8-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="e94d8-124">これは、操作は、NuGet パッケージのソースと統合されてユーザー インターフェイスでのパッケージは入力行機能を提供する場合に優れたです。</span><span class="sxs-lookup"><span data-stu-id="e94d8-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="e94d8-125">一覧にないバージョンのみを使用してパッケージは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="e94d8-125">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e94d8-126">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="e94d8-126">Request parameters</span></span>

<span data-ttu-id="e94d8-127">name</span><span class="sxs-lookup"><span data-stu-id="e94d8-127">Name</span></span>        | <span data-ttu-id="e94d8-128">イン</span><span class="sxs-lookup"><span data-stu-id="e94d8-128">In</span></span>     | <span data-ttu-id="e94d8-129">型</span><span class="sxs-lookup"><span data-stu-id="e94d8-129">Type</span></span>    | <span data-ttu-id="e94d8-130">必須</span><span class="sxs-lookup"><span data-stu-id="e94d8-130">Required</span></span> | <span data-ttu-id="e94d8-131">メモ</span><span class="sxs-lookup"><span data-stu-id="e94d8-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e94d8-132">q</span><span class="sxs-lookup"><span data-stu-id="e94d8-132">q</span></span>           | <span data-ttu-id="e94d8-133">URL</span><span class="sxs-lookup"><span data-stu-id="e94d8-133">URL</span></span>    | <span data-ttu-id="e94d8-134">string</span><span class="sxs-lookup"><span data-stu-id="e94d8-134">string</span></span>  | <span data-ttu-id="e94d8-135">Ｘ</span><span class="sxs-lookup"><span data-stu-id="e94d8-135">no</span></span>       | <span data-ttu-id="e94d8-136">パッケージ Id と比較する文字列</span><span class="sxs-lookup"><span data-stu-id="e94d8-136">The string to compare against package IDs</span></span>
<span data-ttu-id="e94d8-137">スキップ</span><span class="sxs-lookup"><span data-stu-id="e94d8-137">skip</span></span>        | <span data-ttu-id="e94d8-138">URL</span><span class="sxs-lookup"><span data-stu-id="e94d8-138">URL</span></span>    | <span data-ttu-id="e94d8-139">整数</span><span class="sxs-lookup"><span data-stu-id="e94d8-139">integer</span></span> | <span data-ttu-id="e94d8-140">Ｘ</span><span class="sxs-lookup"><span data-stu-id="e94d8-140">no</span></span>       | <span data-ttu-id="e94d8-141">改ページをスキップします。 結果の数</span><span class="sxs-lookup"><span data-stu-id="e94d8-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="e94d8-142">take</span><span class="sxs-lookup"><span data-stu-id="e94d8-142">take</span></span>        | <span data-ttu-id="e94d8-143">URL</span><span class="sxs-lookup"><span data-stu-id="e94d8-143">URL</span></span>    | <span data-ttu-id="e94d8-144">整数</span><span class="sxs-lookup"><span data-stu-id="e94d8-144">integer</span></span> | <span data-ttu-id="e94d8-145">Ｘ</span><span class="sxs-lookup"><span data-stu-id="e94d8-145">no</span></span>       | <span data-ttu-id="e94d8-146">結果を返すには、改ページの数</span><span class="sxs-lookup"><span data-stu-id="e94d8-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="e94d8-147">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="e94d8-147">prerelease</span></span>  | <span data-ttu-id="e94d8-148">URL</span><span class="sxs-lookup"><span data-stu-id="e94d8-148">URL</span></span>    | <span data-ttu-id="e94d8-149">boolean</span><span class="sxs-lookup"><span data-stu-id="e94d8-149">boolean</span></span> | <span data-ttu-id="e94d8-150">Ｘ</span><span class="sxs-lookup"><span data-stu-id="e94d8-150">no</span></span>       | <span data-ttu-id="e94d8-151">`true`または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e94d8-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e94d8-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e94d8-152">semVerLevel</span></span> | <span data-ttu-id="e94d8-153">URL</span><span class="sxs-lookup"><span data-stu-id="e94d8-153">URL</span></span>    | <span data-ttu-id="e94d8-154">string</span><span class="sxs-lookup"><span data-stu-id="e94d8-154">string</span></span>  | <span data-ttu-id="e94d8-155">Ｘ</span><span class="sxs-lookup"><span data-stu-id="e94d8-155">no</span></span>       | <span data-ttu-id="e94d8-156">SemVer 1.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="e94d8-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="e94d8-157">オートコンプリート クエリ`q`はサーバーの実装で定義されている方法で解析します。</span><span class="sxs-lookup"><span data-stu-id="e94d8-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="e94d8-158">nuget.org は camel 形式の大文字と記号の文字で元の spliting によって生成される ID の部分は、パッケージ ID のトークンのプレフィックスのクエリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="e94d8-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="e94d8-159">`skip`パラメーターの既定値を 0 にします。</span><span class="sxs-lookup"><span data-stu-id="e94d8-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="e94d8-160">`take`パラメーターは 0 より大きい整数である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e94d8-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="e94d8-161">サーバーの実装では、最大値をかける場合があります。</span><span class="sxs-lookup"><span data-stu-id="e94d8-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="e94d8-162">場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="e94d8-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e94d8-163">`semVerLevel`クエリ パラメーターを使用するオプトイン[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)です。</span><span class="sxs-lookup"><span data-stu-id="e94d8-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="e94d8-164">このクエリのパラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージ Id のみが返されます (で、[標準の NuGet バージョン管理](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。</span><span class="sxs-lookup"><span data-stu-id="e94d8-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="e94d8-165">場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="e94d8-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="e94d8-166">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="e94d8-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e94d8-167">応答</span><span class="sxs-lookup"><span data-stu-id="e94d8-167">Response</span></span>

<span data-ttu-id="e94d8-168">応答は最大含む JSON ドキュメント`take`オートコンプリートの結果。</span><span class="sxs-lookup"><span data-stu-id="e94d8-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="e94d8-169">ルートの JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="e94d8-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="e94d8-170">name</span><span class="sxs-lookup"><span data-stu-id="e94d8-170">Name</span></span>      | <span data-ttu-id="e94d8-171">種類</span><span class="sxs-lookup"><span data-stu-id="e94d8-171">Type</span></span>             | <span data-ttu-id="e94d8-172">必須</span><span class="sxs-lookup"><span data-stu-id="e94d8-172">Required</span></span> | <span data-ttu-id="e94d8-173">メモ</span><span class="sxs-lookup"><span data-stu-id="e94d8-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e94d8-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="e94d8-174">totalHits</span></span> | <span data-ttu-id="e94d8-175">整数</span><span class="sxs-lookup"><span data-stu-id="e94d8-175">integer</span></span>          | <span data-ttu-id="e94d8-176">可</span><span class="sxs-lookup"><span data-stu-id="e94d8-176">yes</span></span>      | <span data-ttu-id="e94d8-177">無視すると、一致の合計数`skip`と`take`</span><span class="sxs-lookup"><span data-stu-id="e94d8-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="e94d8-178">[データ]</span><span class="sxs-lookup"><span data-stu-id="e94d8-178">data</span></span>      | <span data-ttu-id="e94d8-179">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="e94d8-179">array of strings</span></span> | <span data-ttu-id="e94d8-180">可</span><span class="sxs-lookup"><span data-stu-id="e94d8-180">yes</span></span>      | <span data-ttu-id="e94d8-181">パッケージ Id と一致した要求</span><span class="sxs-lookup"><span data-stu-id="e94d8-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="e94d8-182">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="e94d8-182">Sample request</span></span>

<span data-ttu-id="e94d8-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="e94d8-183">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="e94d8-184">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="e94d8-184">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="e94d8-185">パッケージのバージョンを列挙します。</span><span class="sxs-lookup"><span data-stu-id="e94d8-185">Enumerate package versions</span></span>

<span data-ttu-id="e94d8-186">クライアントが提供されたパッケージ ID のパッケージのバージョンを列挙するのに API オートコンプリート機能を使用できます、前の API を使用して、パッケージ ID が検出されると、</span><span class="sxs-lookup"><span data-stu-id="e94d8-186">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="e94d8-187">一覧にあるパッケージのバージョンは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="e94d8-187">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="e94d8-188">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="e94d8-188">Request parameters</span></span>

<span data-ttu-id="e94d8-189">name</span><span class="sxs-lookup"><span data-stu-id="e94d8-189">Name</span></span>        | <span data-ttu-id="e94d8-190">イン</span><span class="sxs-lookup"><span data-stu-id="e94d8-190">In</span></span>     | <span data-ttu-id="e94d8-191">型</span><span class="sxs-lookup"><span data-stu-id="e94d8-191">Type</span></span>    | <span data-ttu-id="e94d8-192">必須</span><span class="sxs-lookup"><span data-stu-id="e94d8-192">Required</span></span> | <span data-ttu-id="e94d8-193">メモ</span><span class="sxs-lookup"><span data-stu-id="e94d8-193">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="e94d8-194">ID</span><span class="sxs-lookup"><span data-stu-id="e94d8-194">id</span></span>          | <span data-ttu-id="e94d8-195">URL</span><span class="sxs-lookup"><span data-stu-id="e94d8-195">URL</span></span>    | <span data-ttu-id="e94d8-196">string</span><span class="sxs-lookup"><span data-stu-id="e94d8-196">string</span></span>  | <span data-ttu-id="e94d8-197">可</span><span class="sxs-lookup"><span data-stu-id="e94d8-197">yes</span></span>      | <span data-ttu-id="e94d8-198">バージョンを取得するパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="e94d8-198">The package ID to fetch versions for</span></span>
<span data-ttu-id="e94d8-199">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="e94d8-199">prerelease</span></span>  | <span data-ttu-id="e94d8-200">URL</span><span class="sxs-lookup"><span data-stu-id="e94d8-200">URL</span></span>    | <span data-ttu-id="e94d8-201">boolean</span><span class="sxs-lookup"><span data-stu-id="e94d8-201">boolean</span></span> | <span data-ttu-id="e94d8-202">Ｘ</span><span class="sxs-lookup"><span data-stu-id="e94d8-202">no</span></span>       | <span data-ttu-id="e94d8-203">`true`または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="e94d8-203">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="e94d8-204">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="e94d8-204">semVerLevel</span></span> | <span data-ttu-id="e94d8-205">URL</span><span class="sxs-lookup"><span data-stu-id="e94d8-205">URL</span></span>    | <span data-ttu-id="e94d8-206">string</span><span class="sxs-lookup"><span data-stu-id="e94d8-206">string</span></span>  | <span data-ttu-id="e94d8-207">Ｘ</span><span class="sxs-lookup"><span data-stu-id="e94d8-207">no</span></span>       | <span data-ttu-id="e94d8-208">SemVer 2.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="e94d8-208">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="e94d8-209">場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="e94d8-209">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="e94d8-210">`semVerLevel` SemVer 2.0.0 パッケージにオプトインするクエリ パラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="e94d8-210">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="e94d8-211">このクエリのパラメーターを除外すると、SemVer 1.0.0 バージョンのみが返されます。</span><span class="sxs-lookup"><span data-stu-id="e94d8-211">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="e94d8-212">場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 のバージョンの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="e94d8-212">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="e94d8-213">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="e94d8-213">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="e94d8-214">応答</span><span class="sxs-lookup"><span data-stu-id="e94d8-214">Response</span></span>

<span data-ttu-id="e94d8-215">応答は、指定されたパッケージの ID を指定されたクエリ パラメーターでフィルター処理のすべてのパッケージ バージョンを含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="e94d8-215">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="e94d8-216">ルートの JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="e94d8-216">The root JSON object has the following property:</span></span>

<span data-ttu-id="e94d8-217">name</span><span class="sxs-lookup"><span data-stu-id="e94d8-217">Name</span></span>      | <span data-ttu-id="e94d8-218">種類</span><span class="sxs-lookup"><span data-stu-id="e94d8-218">Type</span></span>             | <span data-ttu-id="e94d8-219">必須</span><span class="sxs-lookup"><span data-stu-id="e94d8-219">Required</span></span> | <span data-ttu-id="e94d8-220">メモ</span><span class="sxs-lookup"><span data-stu-id="e94d8-220">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="e94d8-221">[データ]</span><span class="sxs-lookup"><span data-stu-id="e94d8-221">data</span></span>      | <span data-ttu-id="e94d8-222">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="e94d8-222">array of strings</span></span> | <span data-ttu-id="e94d8-223">可</span><span class="sxs-lookup"><span data-stu-id="e94d8-223">yes</span></span>      | <span data-ttu-id="e94d8-224">要求に一致するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="e94d8-224">The package versions matched by the request</span></span>

<span data-ttu-id="e94d8-225">パッケージのバージョンを`data`配列が SemVer 2.0.0 ビルド メタデータを含む可能性があります (例: `1.0.0+metadata`) 場合、`semVerLevel=2.0.0`クエリ文字列で提供されました。</span><span class="sxs-lookup"><span data-stu-id="e94d8-225">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e94d8-226">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="e94d8-226">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="e94d8-227">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="e94d8-227">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
