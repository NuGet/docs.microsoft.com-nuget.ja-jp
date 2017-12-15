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
ms.assetid: ead5cf7a-e51e-4cbb-8798-58226f4c853f
description: "検索のオートコンプリート機能のサービスは、パッケージ Id の対話型の検出とバージョンをサポートします。"
keywords: "NuGet のオートコンプリート機能の API では、NuGet パッケージ ID、パッケージ ID の部分文字列を検索します。"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 313ceb630947b46c34b98e14044ecf121b725087
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="autocomplete"></a><span data-ttu-id="9d559-104">オートコンプリート</span><span class="sxs-lookup"><span data-stu-id="9d559-104">Autocomplete</span></span>

<span data-ttu-id="9d559-105">パッケージ ID とバージョン オートコンプリート エクスペリエンスを V3 API を使用して行うことができます。</span><span class="sxs-lookup"><span data-stu-id="9d559-105">It is possible to build a package ID and version autocomplete experience using the V3 API.</span></span> <span data-ttu-id="9d559-106">オートコンプリート クエリを実行するためのシステム リソースが、`SearchAutocompleteService`リソースで見つかった、[サービス インデックス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="9d559-106">The resource used for making autocomplete queries is the `SearchAutocompleteService` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="9d559-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="9d559-107">Versioning</span></span>

<span data-ttu-id="9d559-108">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="9d559-108">The following `@type` values are used:</span></span>

<span data-ttu-id="9d559-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="9d559-109">@type value</span></span>                          | <span data-ttu-id="9d559-110">メモ</span><span class="sxs-lookup"><span data-stu-id="9d559-110">Notes</span></span>
------------------------------------ | -----
<span data-ttu-id="9d559-111">SearchAutocompleteService</span><span class="sxs-lookup"><span data-stu-id="9d559-111">SearchAutocompleteService</span></span>            | <span data-ttu-id="9d559-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="9d559-112">The initial release</span></span>
<span data-ttu-id="9d559-113">SearchAutocompleteService/3.0.0-beta</span><span class="sxs-lookup"><span data-stu-id="9d559-113">SearchAutocompleteService/3.0.0-beta</span></span> | <span data-ttu-id="9d559-114">エイリアス`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="9d559-114">Alias of `SearchAutocompleteService`</span></span>
<span data-ttu-id="9d559-115">SearchAutocompleteService/3.0.0-rc</span><span class="sxs-lookup"><span data-stu-id="9d559-115">SearchAutocompleteService/3.0.0-rc</span></span>   | <span data-ttu-id="9d559-116">エイリアス`SearchAutocompleteService`</span><span class="sxs-lookup"><span data-stu-id="9d559-116">Alias of `SearchAutocompleteService`</span></span>

## <a name="base-url"></a><span data-ttu-id="9d559-117">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="9d559-117">Base URL</span></span>

<span data-ttu-id="9d559-118">次の Api のベース URL の値、`@id`前述のリソースのいずれかに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="9d559-118">The base URL for the following APIs is the value of the `@id` property associated with one of the aforementioned resource `@type` values.</span></span> <span data-ttu-id="9d559-119">次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。</span><span class="sxs-lookup"><span data-stu-id="9d559-119">In the following document, the placeholder base URL `{@id}` will be used.</span></span>

## <a name="http-methods"></a><span data-ttu-id="9d559-120">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="9d559-120">HTTP Methods</span></span>

<span data-ttu-id="9d559-121">HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。</span><span class="sxs-lookup"><span data-stu-id="9d559-121">All URLs found in the registration resource support the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="search-for-package-ids"></a><span data-ttu-id="9d559-122">パッケージ Id を検索</span><span class="sxs-lookup"><span data-stu-id="9d559-122">Search for package IDs</span></span>

<span data-ttu-id="9d559-123">最初のオートコンプリート機能 API は、パッケージ ID 文字列の一部の検索をサポートします。</span><span class="sxs-lookup"><span data-stu-id="9d559-123">The first autocomplete API supports searching for part of a package ID string.</span></span> <span data-ttu-id="9d559-124">これは、操作は、NuGet パッケージのソースと統合されてユーザー インターフェイスでのパッケージは入力行機能を提供する場合に優れたです。</span><span class="sxs-lookup"><span data-stu-id="9d559-124">This is great when you want to provide a package typeahead feature in a user interface integrated with a NuGet package source.</span></span>

<span data-ttu-id="9d559-125">一覧にないバージョンのみを使用してパッケージは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="9d559-125">A package with only unlisted versions will not appear in the results.</span></span>

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="9d559-126">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="9d559-126">Request parameters</span></span>

<span data-ttu-id="9d559-127">名前</span><span class="sxs-lookup"><span data-stu-id="9d559-127">Name</span></span>        | <span data-ttu-id="9d559-128">イン</span><span class="sxs-lookup"><span data-stu-id="9d559-128">In</span></span>     | <span data-ttu-id="9d559-129">型</span><span class="sxs-lookup"><span data-stu-id="9d559-129">Type</span></span>    | <span data-ttu-id="9d559-130">必須</span><span class="sxs-lookup"><span data-stu-id="9d559-130">Required</span></span> | <span data-ttu-id="9d559-131">メモ</span><span class="sxs-lookup"><span data-stu-id="9d559-131">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="9d559-132">q</span><span class="sxs-lookup"><span data-stu-id="9d559-132">q</span></span>           | <span data-ttu-id="9d559-133">URL</span><span class="sxs-lookup"><span data-stu-id="9d559-133">URL</span></span>    | <span data-ttu-id="9d559-134">string</span><span class="sxs-lookup"><span data-stu-id="9d559-134">string</span></span>  | <span data-ttu-id="9d559-135">Ｘ</span><span class="sxs-lookup"><span data-stu-id="9d559-135">no</span></span>       | <span data-ttu-id="9d559-136">パッケージ Id と比較する文字列</span><span class="sxs-lookup"><span data-stu-id="9d559-136">The string to compare against package IDs</span></span>
<span data-ttu-id="9d559-137">スキップ</span><span class="sxs-lookup"><span data-stu-id="9d559-137">skip</span></span>        | <span data-ttu-id="9d559-138">URL</span><span class="sxs-lookup"><span data-stu-id="9d559-138">URL</span></span>    | <span data-ttu-id="9d559-139">整数</span><span class="sxs-lookup"><span data-stu-id="9d559-139">integer</span></span> | <span data-ttu-id="9d559-140">Ｘ</span><span class="sxs-lookup"><span data-stu-id="9d559-140">no</span></span>       | <span data-ttu-id="9d559-141">改ページをスキップします。 結果の数</span><span class="sxs-lookup"><span data-stu-id="9d559-141">The number of results to skip, for pagination</span></span>
<span data-ttu-id="9d559-142">take</span><span class="sxs-lookup"><span data-stu-id="9d559-142">take</span></span>        | <span data-ttu-id="9d559-143">URL</span><span class="sxs-lookup"><span data-stu-id="9d559-143">URL</span></span>    | <span data-ttu-id="9d559-144">整数</span><span class="sxs-lookup"><span data-stu-id="9d559-144">integer</span></span> | <span data-ttu-id="9d559-145">Ｘ</span><span class="sxs-lookup"><span data-stu-id="9d559-145">no</span></span>       | <span data-ttu-id="9d559-146">結果を返すには、改ページの数</span><span class="sxs-lookup"><span data-stu-id="9d559-146">The number of results to return, for pagination</span></span>
<span data-ttu-id="9d559-147">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="9d559-147">prerelease</span></span>  | <span data-ttu-id="9d559-148">URL</span><span class="sxs-lookup"><span data-stu-id="9d559-148">URL</span></span>    | <span data-ttu-id="9d559-149">boolean</span><span class="sxs-lookup"><span data-stu-id="9d559-149">boolean</span></span> | <span data-ttu-id="9d559-150">Ｘ</span><span class="sxs-lookup"><span data-stu-id="9d559-150">no</span></span>       | <span data-ttu-id="9d559-151">`true`または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9d559-151">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="9d559-152">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="9d559-152">semVerLevel</span></span> | <span data-ttu-id="9d559-153">URL</span><span class="sxs-lookup"><span data-stu-id="9d559-153">URL</span></span>    | <span data-ttu-id="9d559-154">string</span><span class="sxs-lookup"><span data-stu-id="9d559-154">string</span></span>  | <span data-ttu-id="9d559-155">Ｘ</span><span class="sxs-lookup"><span data-stu-id="9d559-155">no</span></span>       | <span data-ttu-id="9d559-156">SemVer 1.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="9d559-156">A SemVer 1.0.0 version string</span></span> 

<span data-ttu-id="9d559-157">オートコンプリート クエリ`q`はサーバーの実装で定義されている方法で解析します。</span><span class="sxs-lookup"><span data-stu-id="9d559-157">The autocomplete query `q` is parsed in a manner that is defined by the server implementation.</span></span> <span data-ttu-id="9d559-158">nuget.org は camel 形式の大文字と記号の文字で元の spliting によって生成される ID の部分は、パッケージ ID のトークンのプレフィックスのクエリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="9d559-158">nuget.org supports querying for the prefix of package ID tokens, which are pieces of the ID produced by spliting the original by camel case and symbol characters.</span></span>

<span data-ttu-id="9d559-159">`skip`パラメーターの既定値を 0 にします。</span><span class="sxs-lookup"><span data-stu-id="9d559-159">The `skip` parameter defaults to 0.</span></span>

<span data-ttu-id="9d559-160">`take`パラメーターは 0 より大きい整数である必要があります。</span><span class="sxs-lookup"><span data-stu-id="9d559-160">The `take` parameter should be an integer greater than zero.</span></span> <span data-ttu-id="9d559-161">サーバーの実装では、最大値をかける場合があります。</span><span class="sxs-lookup"><span data-stu-id="9d559-161">The server implementation may impose a maximum value.</span></span>

<span data-ttu-id="9d559-162">場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="9d559-162">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="9d559-163">`semVerLevel`クエリ パラメーターを使用するオプトイン[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)です。</span><span class="sxs-lookup"><span data-stu-id="9d559-163">The `semVerLevel` query parameter is used to opt-in to [SemVer 2.0.0 packages](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages).</span></span>
<span data-ttu-id="9d559-164">このクエリのパラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージ Id のみが返されます (で、[標準の NuGet バージョン管理](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。</span><span class="sxs-lookup"><span data-stu-id="9d559-164">If this query parameter is excluded, only package IDs with SemVer 1.0.0 compatible versions will be returned (with the [standard NuGet versioning](../reference/package-versioning.md) caveats, such as version strings with 4 integer pieces).</span></span>
<span data-ttu-id="9d559-165">場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="9d559-165">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 compatible packages will be returned.</span></span> <span data-ttu-id="9d559-166">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="9d559-166">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="9d559-167">応答</span><span class="sxs-lookup"><span data-stu-id="9d559-167">Response</span></span>

<span data-ttu-id="9d559-168">応答は最大含む JSON ドキュメント`take`オートコンプリートの結果。</span><span class="sxs-lookup"><span data-stu-id="9d559-168">The response is JSON document containing up to `take` autocomplete results.</span></span>

<span data-ttu-id="9d559-169">ルートの JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="9d559-169">The root JSON object has the following properties:</span></span>

<span data-ttu-id="9d559-170">名前</span><span class="sxs-lookup"><span data-stu-id="9d559-170">Name</span></span>      | <span data-ttu-id="9d559-171">種類</span><span class="sxs-lookup"><span data-stu-id="9d559-171">Type</span></span>             | <span data-ttu-id="9d559-172">必須</span><span class="sxs-lookup"><span data-stu-id="9d559-172">Required</span></span> | <span data-ttu-id="9d559-173">メモ</span><span class="sxs-lookup"><span data-stu-id="9d559-173">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="9d559-174">totalHits</span><span class="sxs-lookup"><span data-stu-id="9d559-174">totalHits</span></span> | <span data-ttu-id="9d559-175">整数</span><span class="sxs-lookup"><span data-stu-id="9d559-175">integer</span></span>          | <span data-ttu-id="9d559-176">可</span><span class="sxs-lookup"><span data-stu-id="9d559-176">yes</span></span>      | <span data-ttu-id="9d559-177">無視すると、一致の合計数`skip`と`take`</span><span class="sxs-lookup"><span data-stu-id="9d559-177">The total number of matches, disregarding `skip` and `take`</span></span>
<span data-ttu-id="9d559-178">[データ]</span><span class="sxs-lookup"><span data-stu-id="9d559-178">data</span></span>      | <span data-ttu-id="9d559-179">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="9d559-179">array of strings</span></span> | <span data-ttu-id="9d559-180">可</span><span class="sxs-lookup"><span data-stu-id="9d559-180">yes</span></span>      | <span data-ttu-id="9d559-181">パッケージ Id と一致した要求</span><span class="sxs-lookup"><span data-stu-id="9d559-181">The package IDs matched by the request</span></span>

### <a name="sample-request"></a><span data-ttu-id="9d559-182">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="9d559-182">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="9d559-183">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="9d559-183">Sample response</span></span>

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a><span data-ttu-id="9d559-184">パッケージのバージョンを列挙します。</span><span class="sxs-lookup"><span data-stu-id="9d559-184">Enumerate package versions</span></span>

<span data-ttu-id="9d559-185">クライアントが提供されたパッケージ ID のパッケージのバージョンを列挙するのに API オートコンプリート機能を使用できます、前の API を使用して、パッケージ ID が検出されると、</span><span class="sxs-lookup"><span data-stu-id="9d559-185">Once a package ID is discovered using the previous API, a client can use the autocomplete API to enumerate package versions for a provided package ID.</span></span>

<span data-ttu-id="9d559-186">一覧にあるパッケージのバージョンは、結果には表示されません。</span><span class="sxs-lookup"><span data-stu-id="9d559-186">A package version that is unlisted will not appear in the results.</span></span>

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a><span data-ttu-id="9d559-187">要求パラメーター</span><span class="sxs-lookup"><span data-stu-id="9d559-187">Request parameters</span></span>

<span data-ttu-id="9d559-188">名前</span><span class="sxs-lookup"><span data-stu-id="9d559-188">Name</span></span>        | <span data-ttu-id="9d559-189">イン</span><span class="sxs-lookup"><span data-stu-id="9d559-189">In</span></span>     | <span data-ttu-id="9d559-190">型</span><span class="sxs-lookup"><span data-stu-id="9d559-190">Type</span></span>    | <span data-ttu-id="9d559-191">必須</span><span class="sxs-lookup"><span data-stu-id="9d559-191">Required</span></span> | <span data-ttu-id="9d559-192">メモ</span><span class="sxs-lookup"><span data-stu-id="9d559-192">Notes</span></span>
----------- | ------ | ------- | -------- | -----
<span data-ttu-id="9d559-193">ID</span><span class="sxs-lookup"><span data-stu-id="9d559-193">id</span></span>          | <span data-ttu-id="9d559-194">URL</span><span class="sxs-lookup"><span data-stu-id="9d559-194">URL</span></span>    | <span data-ttu-id="9d559-195">string</span><span class="sxs-lookup"><span data-stu-id="9d559-195">string</span></span>  | <span data-ttu-id="9d559-196">可</span><span class="sxs-lookup"><span data-stu-id="9d559-196">yes</span></span>      | <span data-ttu-id="9d559-197">バージョンを取得するパッケージ ID</span><span class="sxs-lookup"><span data-stu-id="9d559-197">The package ID to fetch versions for</span></span>
<span data-ttu-id="9d559-198">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="9d559-198">prerelease</span></span>  | <span data-ttu-id="9d559-199">URL</span><span class="sxs-lookup"><span data-stu-id="9d559-199">URL</span></span>    | <span data-ttu-id="9d559-200">boolean</span><span class="sxs-lookup"><span data-stu-id="9d559-200">boolean</span></span> | <span data-ttu-id="9d559-201">Ｘ</span><span class="sxs-lookup"><span data-stu-id="9d559-201">no</span></span>       | <span data-ttu-id="9d559-202">`true`または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)</span><span class="sxs-lookup"><span data-stu-id="9d559-202">`true` or `false` determining whether to include [pre-release packages](../create-packages/prerelease-packages.md)</span></span>
<span data-ttu-id="9d559-203">semVerLevel</span><span class="sxs-lookup"><span data-stu-id="9d559-203">semVerLevel</span></span> | <span data-ttu-id="9d559-204">URL</span><span class="sxs-lookup"><span data-stu-id="9d559-204">URL</span></span>    | <span data-ttu-id="9d559-205">string</span><span class="sxs-lookup"><span data-stu-id="9d559-205">string</span></span>  | <span data-ttu-id="9d559-206">Ｘ</span><span class="sxs-lookup"><span data-stu-id="9d559-206">no</span></span>       | <span data-ttu-id="9d559-207">SemVer 2.0.0 バージョン文字列</span><span class="sxs-lookup"><span data-stu-id="9d559-207">A SemVer 2.0.0 version string</span></span> 

<span data-ttu-id="9d559-208">場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。</span><span class="sxs-lookup"><span data-stu-id="9d559-208">If `prerelease` is not provided, pre-release packages are excluded.</span></span>

<span data-ttu-id="9d559-209">`semVerLevel` SemVer 2.0.0 パッケージにオプトインするクエリ パラメーターを使用します。</span><span class="sxs-lookup"><span data-stu-id="9d559-209">The `semVerLevel` query parameter is used to opt-in to SemVer 2.0.0 packages.</span></span> <span data-ttu-id="9d559-210">このクエリのパラメーターを除外すると、SemVer 1.0.0 バージョンのみが返されます。</span><span class="sxs-lookup"><span data-stu-id="9d559-210">If this query parameter is excluded, only SemVer 1.0.0 versions will be returned.</span></span> <span data-ttu-id="9d559-211">場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 のバージョンの両方が返されます。</span><span class="sxs-lookup"><span data-stu-id="9d559-211">If `semVerLevel=2.0.0` is provided, both SemVer 1.0.0 and SemVer 2.0.0 versions will be returned.</span></span> <span data-ttu-id="9d559-212">参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="9d559-212">See the [SemVer 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) for more information.</span></span>

### <a name="response"></a><span data-ttu-id="9d559-213">応答</span><span class="sxs-lookup"><span data-stu-id="9d559-213">Response</span></span>

<span data-ttu-id="9d559-214">応答は、指定されたパッケージの ID を指定されたクエリ パラメーターでフィルター処理のすべてのパッケージ バージョンを含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="9d559-214">The response is JSON document containing all package versions of the provided package ID, filtering by the given query parameters.</span></span>

<span data-ttu-id="9d559-215">ルートの JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="9d559-215">The root JSON object has the following property:</span></span>

<span data-ttu-id="9d559-216">名前</span><span class="sxs-lookup"><span data-stu-id="9d559-216">Name</span></span>      | <span data-ttu-id="9d559-217">種類</span><span class="sxs-lookup"><span data-stu-id="9d559-217">Type</span></span>             | <span data-ttu-id="9d559-218">必須</span><span class="sxs-lookup"><span data-stu-id="9d559-218">Required</span></span> | <span data-ttu-id="9d559-219">メモ</span><span class="sxs-lookup"><span data-stu-id="9d559-219">Notes</span></span>
--------- | ---------------- | -------- | -----
<span data-ttu-id="9d559-220">[データ]</span><span class="sxs-lookup"><span data-stu-id="9d559-220">data</span></span>      | <span data-ttu-id="9d559-221">文字列の配列</span><span class="sxs-lookup"><span data-stu-id="9d559-221">array of strings</span></span> | <span data-ttu-id="9d559-222">可</span><span class="sxs-lookup"><span data-stu-id="9d559-222">yes</span></span>      | <span data-ttu-id="9d559-223">要求に一致するパッケージのバージョン</span><span class="sxs-lookup"><span data-stu-id="9d559-223">The package versions matched by the request</span></span>

<span data-ttu-id="9d559-224">パッケージのバージョンを`data`配列が SemVer 2.0.0 ビルド メタデータを含む可能性があります (例: `1.0.0+metadata`) 場合、`semVerLevel=2.0.0`クエリ文字列で提供されました。</span><span class="sxs-lookup"><span data-stu-id="9d559-224">The package versions in the `data` array could contain SemVer 2.0.0 build metadata (e.g. `1.0.0+metadata`) if the `semVerLevel=2.0.0` was provided in the query string.</span></span>

### <a name="sample-request"></a><span data-ttu-id="9d559-225">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="9d559-225">Sample request</span></span>

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a><span data-ttu-id="9d559-226">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="9d559-226">Sample response</span></span>

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
