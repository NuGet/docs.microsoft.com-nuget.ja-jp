---
title: オートコンプリートを NuGet API
description: 検索のオートコンプリート機能のサービスは、パッケージ Id の対話型の検出とバージョンをサポートします。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822137"
---
# <a name="autocomplete"></a><span data-ttu-id="8c2d3-103">オートコンプリート</span><span class="sxs-lookup"><span data-stu-id="8c2d3-103">Autocomplete</span></span>

<span data-ttu-id="8c2d3-104">パッケージ ID とバージョン オートコンプリート エクスペリエンスを V3 API を使用して行うことができます。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-104">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="8c2d3-105">オートコンプリート クエリを実行するためのシステム リソースが、`SearchAutocompleteService`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-105">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="8c2d3-106">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="8c2d3-106">Versioning</span></span>

<span data-ttu-id="8c2d3-107">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-107">The following `@type` values are used:</span></span>

<span data-ttu-id="8c2d3-108">@type の値</span><span class="sxs-lookup"><span data-stu-id="8c2d3-108">@type value</span></span>                          | <span data-ttu-id="8c2d3-109">メモ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-109">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="8c2d3-110">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="8c2d3-110">SearchAutocompleteService</span></span>            | <span data-ttu-id="8c2d3-111">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="8c2d3-111">The initial release</span></span>
<span data-ttu-id="8c2d3-112">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="8c2d3-112">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="8c2d3-113">エイリアス `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="8c2d3-113">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="8c2d3-114">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="8c2d3-114">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="8c2d3-115">エイリアス `SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="8c2d3-115">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="8c2d3-116">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="8c2d3-116">Base URL</span></span>

<span data-ttu-id="8c2d3-117">次の Api のベース URL の値、`@id`前述のリソースのいずれかに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-117">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="8c2d3-118">次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-118">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="8c2d3-119">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="8c2d3-119">HTTP Methods</span></span>

<span data-ttu-id="8c2d3-120">HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-120">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="8c2d3-121">パッケージ Id を検索</span><span class="sxs-lookup"><span data-stu-id="8c2d3-121">Search for package IDs</span></span>

<span data-ttu-id="8c2d3-122">最初のオートコンプリート機能 API は、パッケージ ID 文字列の一部の検索をサポートします。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-122">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="8c2d3-123">これは、操作は、NuGet パッケージのソースと統合されてユーザー インターフェイスでのパッケージは入力行機能を提供する場合に優れたです。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-123">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="8c2d3-124">一覧にないバージョンのみを使用してパッケージは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-124">A package with only unlisted versions will not appear in the results.</span></span>

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="8c2d3-125">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="8c2d3-125">Request parameters</span></span>

<span data-ttu-id="8c2d3-126">名前</span><span class="sxs-lookup"><span data-stu-id="8c2d3-126">Name</span></span>        | <span data-ttu-id="8c2d3-127">イン</span><span class="sxs-lookup"><span data-stu-id="8c2d3-127">In</span></span>     | <span data-ttu-id="8c2d3-128">型</span><span class="sxs-lookup"><span data-stu-id="8c2d3-128">Type</span></span>    | <span data-ttu-id="8c2d3-129">必須</span><span class="sxs-lookup"><span data-stu-id="8c2d3-129">Required</span></span> | <span data-ttu-id="8c2d3-130">メモ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-130">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="8c2d3-131">q</span><span class="sxs-lookup"><span data-stu-id="8c2d3-131">q</span></span>           | <span data-ttu-id="8c2d3-132">URL</span><span class="sxs-lookup"><span data-stu-id="8c2d3-132">URL</span></span>    | <span data-ttu-id="8c2d3-133">string</span><span class="sxs-lookup"><span data-stu-id="8c2d3-133">string</span></span>  | <span data-ttu-id="8c2d3-134">Ｘ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-134">no</span></span>       | <span data-ttu-id="8c2d3-135">パッケージ Id と比較する文字列</span><span class="sxs-lookup"><span data-stu-id="8c2d3-135">The string to compare against package IDs</span></span>
<span data-ttu-id="8c2d3-136">スキップ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-136">skip</span></span>        | <span data-ttu-id="8c2d3-137">URL</span><span class="sxs-lookup"><span data-stu-id="8c2d3-137">URL</span></span>    | <span data-ttu-id="8c2d3-138">整数</span><span class="sxs-lookup"><span data-stu-id="8c2d3-138">integer</span></span> | <span data-ttu-id="8c2d3-139">Ｘ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-139">no</span></span>       | <span data-ttu-id="8c2d3-140">改ページをスキップします。 結果の数</span><span class="sxs-lookup"><span data-stu-id="8c2d3-140">The number of results to skip, for pagination</span></span>
<span data-ttu-id="8c2d3-141">take</span><span class="sxs-lookup"><span data-stu-id="8c2d3-141">take</span></span>        | <span data-ttu-id="8c2d3-142">URL</span><span class="sxs-lookup"><span data-stu-id="8c2d3-142">URL</span></span>    | <span data-ttu-id="8c2d3-143">整数</span><span class="sxs-lookup"><span data-stu-id="8c2d3-143">integer</span></span> | <span data-ttu-id="8c2d3-144">Ｘ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-144">no</span></span>       | <span data-ttu-id="8c2d3-145">結果を返すには、改ページの数</span><span class="sxs-lookup"><span data-stu-id="8c2d3-145">The number of results to return, for pagination</span></span>
<span data-ttu-id="8c2d3-146">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="8c2d3-146">prerelease</span></span>  | <span data-ttu-id="8c2d3-147">URL</span><span class="sxs-lookup"><span data-stu-id="8c2d3-147">URL</span></span>    | <span data-ttu-id="8c2d3-148">boolean</span><span class="sxs-lookup"><span data-stu-id="8c2d3-148">boolean</span></span> | <span data-ttu-id="8c2d3-149">Ｘ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-149">no</span></span>       | <span data-ttu-id="8c2d3-150">`true` または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8c2d3-150">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="8c2d3-151">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="8c2d3-151">semVerLevel</span></span> | <span data-ttu-id="8c2d3-152">URL</span><span class="sxs-lookup"><span data-stu-id="8c2d3-152">URL</span></span>    | <span data-ttu-id="8c2d3-153">string</span><span class="sxs-lookup"><span data-stu-id="8c2d3-153">string</span></span>  | <span data-ttu-id="8c2d3-154">Ｘ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-154">no</span></span>       | <span data-ttu-id="8c2d3-155">SemVer 1.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="8c2d3-155">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="8c2d3-156">オートコンプリート クエリ`q`はサーバーの実装で定義されている方法で解析します。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-156">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="8c2d3-157">nuget.org は camel 形式の大文字と記号の文字で元の spliting によって生成される ID の部分は、パッケージ ID のトークンのプレフィックスのクエリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-157">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="8c2d3-158">`skip`パラメーターの既定値を 0 にします。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-158">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="8c2d3-159">`take`パラメーターは 0 より大きい整数である必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-159">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="8c2d3-160">サーバーの実装では、最大値をかける場合があります。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-160">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="8c2d3-161">場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-161">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="8c2d3-162">`semVerLevel`クエリ パラメーターを使用するオプトイン[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)です。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-162">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="8c2d3-163">このクエリのパラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージ Id のみが返されます (で、[標準の NuGet バージョン管理](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-163">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="8c2d3-164">場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-164">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="8c2d3-165">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-165">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="8c2d3-166">応答</span><span class="sxs-lookup"><span data-stu-id="8c2d3-166">Response</span></span>

<span data-ttu-id="8c2d3-167">応答は最大含む JSON ドキュメント`take`オートコンプリートの結果。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-167">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="8c2d3-168">ルートの JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-168">The root JSON object has the following properties:</span></span>

<span data-ttu-id="8c2d3-169">名前</span><span class="sxs-lookup"><span data-stu-id="8c2d3-169">Name</span></span>      | <span data-ttu-id="8c2d3-170">種類</span><span class="sxs-lookup"><span data-stu-id="8c2d3-170">Type</span></span>             | <span data-ttu-id="8c2d3-171">必須</span><span class="sxs-lookup"><span data-stu-id="8c2d3-171">Required</span></span> | <span data-ttu-id="8c2d3-172">メモ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-172">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="8c2d3-173">totalHits</span><span class="sxs-lookup"><span data-stu-id="8c2d3-173">totalHits</span></span> | <span data-ttu-id="8c2d3-174">整数</span><span class="sxs-lookup"><span data-stu-id="8c2d3-174">integer</span></span>          | <span data-ttu-id="8c2d3-175">可</span><span class="sxs-lookup"><span data-stu-id="8c2d3-175">yes</span></span>      | <span data-ttu-id="8c2d3-176">無視すると、一致の合計数`skip`と `take`</span><span class="sxs-lookup"><span data-stu-id="8c2d3-176">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="8c2d3-177">[データ]</span><span class="sxs-lookup"><span data-stu-id="8c2d3-177">data</span></span>      | <span data-ttu-id="8c2d3-178">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="8c2d3-178">array of strings</span></span> | <span data-ttu-id="8c2d3-179">可</span><span class="sxs-lookup"><span data-stu-id="8c2d3-179">yes</span></span>      | <span data-ttu-id="8c2d3-180">パッケージ Id と一致した要求</span><span class="sxs-lookup"><span data-stu-id="8c2d3-180">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="8c2d3-181">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="8c2d3-181">Sample request</span></span>

<span data-ttu-id="8c2d3-182">取得 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span><span class="sxs-lookup"><span data-stu-id="8c2d3-182">GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true</span></span>

### <a name="sample-response"></a><span data-ttu-id="8c2d3-183">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="8c2d3-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="8c2d3-184">パッケージのバージョンを列挙します。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-184">Enumerate package versions</span></span>

<span data-ttu-id="8c2d3-185">クライアントが提供されたパッケージ ID のパッケージのバージョンを列挙するのに API オートコンプリート機能を使用できます、前の API を使用して、パッケージ ID が検出されると、</span><span class="sxs-lookup"><span data-stu-id="8c2d3-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="8c2d3-186">一覧にあるパッケージのバージョンは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-186">A package version that is unlisted will not appear in the results.</span></span>

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a><span data-ttu-id="8c2d3-187">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="8c2d3-187">Request parameters</span></span>

<span data-ttu-id="8c2d3-188">名前</span><span class="sxs-lookup"><span data-stu-id="8c2d3-188">Name</span></span>        | <span data-ttu-id="8c2d3-189">イン</span><span class="sxs-lookup"><span data-stu-id="8c2d3-189">In</span></span>     | <span data-ttu-id="8c2d3-190">型</span><span class="sxs-lookup"><span data-stu-id="8c2d3-190">Type</span></span>    | <span data-ttu-id="8c2d3-191">必須</span><span class="sxs-lookup"><span data-stu-id="8c2d3-191">Required</span></span> | <span data-ttu-id="8c2d3-192">メモ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="8c2d3-193">ID</span><span class="sxs-lookup"><span data-stu-id="8c2d3-193">id</span></span>          | <span data-ttu-id="8c2d3-194">URL</span><span class="sxs-lookup"><span data-stu-id="8c2d3-194">URL</span></span>    | <span data-ttu-id="8c2d3-195">string</span><span class="sxs-lookup"><span data-stu-id="8c2d3-195">string</span></span>  | <span data-ttu-id="8c2d3-196">可</span><span class="sxs-lookup"><span data-stu-id="8c2d3-196">yes</span></span>      | <span data-ttu-id="8c2d3-197">バージョンを取得するパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="8c2d3-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="8c2d3-198">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="8c2d3-198">prerelease</span></span>  | <span data-ttu-id="8c2d3-199">URL</span><span class="sxs-lookup"><span data-stu-id="8c2d3-199">URL</span></span>    | <span data-ttu-id="8c2d3-200">boolean</span><span class="sxs-lookup"><span data-stu-id="8c2d3-200">boolean</span></span> | <span data-ttu-id="8c2d3-201">Ｘ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-201">no</span></span>       | <span data-ttu-id="8c2d3-202">`true` または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="8c2d3-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="8c2d3-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="8c2d3-203">semVerLevel</span></span> | <span data-ttu-id="8c2d3-204">URL</span><span class="sxs-lookup"><span data-stu-id="8c2d3-204">URL</span></span>    | <span data-ttu-id="8c2d3-205">string</span><span class="sxs-lookup"><span data-stu-id="8c2d3-205">string</span></span>  | <span data-ttu-id="8c2d3-206">Ｘ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-206">no</span></span>       | <span data-ttu-id="8c2d3-207">SemVer 2.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="8c2d3-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="8c2d3-208">場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="8c2d3-209">`semVerLevel` SemVer 2.0.0 パッケージにオプトインするクエリ パラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="8c2d3-210">このクエリのパラメーターを除外すると、SemVer 1.0.0 バージョンのみが返されます。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="8c2d3-211">場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 のバージョンの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="8c2d3-212">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="8c2d3-213">応答</span><span class="sxs-lookup"><span data-stu-id="8c2d3-213">Response</span></span>

<span data-ttu-id="8c2d3-214">応答は、指定されたパッケージの ID を指定されたクエリ パラメーターでフィルター処理のすべてのパッケージ バージョンを含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="8c2d3-215">ルートの JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="8c2d3-216">名前</span><span class="sxs-lookup"><span data-stu-id="8c2d3-216">Name</span></span>      | <span data-ttu-id="8c2d3-217">種類</span><span class="sxs-lookup"><span data-stu-id="8c2d3-217">Type</span></span>             | <span data-ttu-id="8c2d3-218">必須</span><span class="sxs-lookup"><span data-stu-id="8c2d3-218">Required</span></span> | <span data-ttu-id="8c2d3-219">メモ</span><span class="sxs-lookup"><span data-stu-id="8c2d3-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="8c2d3-220">[データ]</span><span class="sxs-lookup"><span data-stu-id="8c2d3-220">data</span></span>      | <span data-ttu-id="8c2d3-221">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="8c2d3-221">array of strings</span></span> | <span data-ttu-id="8c2d3-222">可</span><span class="sxs-lookup"><span data-stu-id="8c2d3-222">yes</span></span>      | <span data-ttu-id="8c2d3-223">要求に一致するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="8c2d3-223">The package versions matched by the request</span></span>

<span data-ttu-id="8c2d3-224">パッケージのバージョンを`data`配列が SemVer 2.0.0 ビルド メタデータを含む可能性があります (例: `1.0.0+metadata`) 場合、`semVerLevel=2.0.0`クエリ文字列で提供されました。</span><span class="sxs-lookup"><span data-stu-id="8c2d3-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="8c2d3-225">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="8c2d3-225">Sample request</span></span>

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a><span data-ttu-id="8c2d3-226">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="8c2d3-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
