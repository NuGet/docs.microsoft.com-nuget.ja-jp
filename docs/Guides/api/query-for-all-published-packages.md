---
title: nuget.org に発行されたすべてのパッケージに対するクエリの実行
description: NuGet API を使用して、nuget.org に発行されたすべてのパッケージに対してクエリを実行し、時間が経過しても最新の状態を把握することができます。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 11/02/2017
ms.topic: tutorial
ms.reviewer: kraigb
ms.openlocfilehash: 4190cfb500127f117ea1067f0679e5c248bffb3d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="query-for-all-packages-published-to-nugetorg"></a><span data-ttu-id="be06c-103">nuget.org に発行されたすべてのパッケージに対するクエリの実行</span><span class="sxs-lookup"><span data-stu-id="be06c-103">Query for all packages published to nuget.org</span></span>

<span data-ttu-id="be06c-104">従来の OData V2 API に共通のクエリ パターンの 1 つは、nuget.org に発行されたすべてのパッケージを、そのパッケージの発行順に列挙するというものでした。</span><span class="sxs-lookup"><span data-stu-id="be06c-104">One common query pattern on the legacy OData V2 API was enumerating all packages published to nuget.org, ordered by when the package was published.</span></span> <span data-ttu-id="be06c-105">nuget.org に対するこの種のクエリに必要なシナリオは、次のように大きく異なります。</span><span class="sxs-lookup"><span data-stu-id="be06c-105">Scenarios requiring this kind of query against nuget.org vary widely:</span></span>

- <span data-ttu-id="be06c-106">nuget.org を完全にレプリケートする</span><span class="sxs-lookup"><span data-stu-id="be06c-106">Replicating nuget.org entirely</span></span>
- <span data-ttu-id="be06c-107">パッケージの新しいバージョンがリリースされたときに検出する</span><span class="sxs-lookup"><span data-stu-id="be06c-107">Detecting when packages have new versions released</span></span>
- <span data-ttu-id="be06c-108">使用しているパッケージに依存するパッケージを検索する</span><span class="sxs-lookup"><span data-stu-id="be06c-108">Finding packages that depend on your package</span></span>

<span data-ttu-id="be06c-109">これを行う従来の方法は、一般的に、タイムスタンプによる OData パッケージ エンティティの並べ替え、および `skip` と `top` (ページ サイズ) パラメーターを使用する大規模な結果セットでのページングによって異なりました。</span><span class="sxs-lookup"><span data-stu-id="be06c-109">The legacy way of doing this typically depended on sorting the OData package entity by a timestamp and paging across the massive result set using `skip` and `top` (page size) parameters.</span></span> <span data-ttu-id="be06c-110">残念ながら、この方法には次のようないくつかの欠点があります。</span><span class="sxs-lookup"><span data-stu-id="be06c-110">Unfortunately, this approach has some drawbacks:</span></span>

- <span data-ttu-id="be06c-111">多くの場合、クエリはデータに対して変更順に実行されるため、パッケージが欠落する可能性がある</span><span class="sxs-lookup"><span data-stu-id="be06c-111">Possibility of missing packages, because the queries are being made on data that is often changing order</span></span>
- <span data-ttu-id="be06c-112">クエリが最適化されていないため、クエリの応答時間が遅くなる (最も最適化されたクエリとは、公式の NuGet クライアントの主要なシナリオをサポートするクエリのことです)</span><span class="sxs-lookup"><span data-stu-id="be06c-112">Slow query response time, because the queries are not optimized (the most optimized queries are ones that support a mainline scenario for the official NuGet client)</span></span>
- <span data-ttu-id="be06c-113">非推奨とされた、ドキュメント化もされていない API の使用 (このようなクエリのサポートは将来的に保証されないことを意味します)</span><span class="sxs-lookup"><span data-stu-id="be06c-113">Use of deprecated and undocumented API, meaning the support of such queries in the future is not guaranteed</span></span>
- <span data-ttu-id="be06c-114">正確な発生順に履歴を再生できない</span><span class="sxs-lookup"><span data-stu-id="be06c-114">Inability to replay history in the exact order that it transpired</span></span>

<span data-ttu-id="be06c-115">このような理由から、以下のガイドに従うことで、より信頼性の高い将来性のある方法で前述のシナリオに対処できます。</span><span class="sxs-lookup"><span data-stu-id="be06c-115">For this reason, the following guide can be followed to address the aforementioned scenarios in a more reliable and future-proof way.</span></span>

## <a name="overview"></a><span data-ttu-id="be06c-116">概要</span><span class="sxs-lookup"><span data-stu-id="be06c-116">Overview</span></span>

<span data-ttu-id="be06c-117">このガイドの中心となるのは、**カタログ**と呼ばれる [NuGet API](../../api/overview.md) のリソースです。</span><span class="sxs-lookup"><span data-stu-id="be06c-117">At the center of this guide is resource in the [NuGet API](../../api/overview.md) called the **catalog**.</span></span> <span data-ttu-id="be06c-118">カタログは追加専用の API であり、これを使用することで、呼び出し元は nuget.org で追加、変更、および削除されたパッケージのすべての履歴を確認することができます。nuget.org に発行されたパッケージのすべて (あるいは一部でも) に関心がある場合、カタログは、時間が経過しても現在使用可能なパッケージ セットを常に把握することができる優れた方法です。</span><span class="sxs-lookup"><span data-stu-id="be06c-118">The catalog is an append-only API that allows the caller to see a full history of packages added to, modified, and deleted from nuget.org. If you are interested in all or even a subset of packages published to nuget.org, the catalog is a great way to stay up-to-date with the set of currently available packages as time goes on.</span></span>

<span data-ttu-id="be06c-119">このガイドは簡単なチュートリアルであるため、カタログの詳細については、[API 参照に関するドキュメント](../../api/catalog-resource.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="be06c-119">This guide is intended to be a high-level walk-through but if you are interested in the fine-grain details of the catalog, see its [API reference document](../../api/catalog-resource.md).</span></span>

<span data-ttu-id="be06c-120">次の手順は任意のプログラミング言語で実行できます。</span><span class="sxs-lookup"><span data-stu-id="be06c-120">The following steps can be implemented in any programming language of your choice.</span></span> <span data-ttu-id="be06c-121">完全な実行サンプルが必要な場合は、以下の [C# のサンプル](#c-sample-code)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="be06c-121">If you want a full running sample, take a look at the [C# sample](#c-sample-code) mentioned below.</span></span>

<span data-ttu-id="be06c-122">それ以外の場合は、以下のガイドに従って、信頼性の高いカタログ リーダーをビルドします。</span><span class="sxs-lookup"><span data-stu-id="be06c-122">Otherwise, follow the guide below to build a reliable catalog reader.</span></span>

## <a name="initialize-a-cursor"></a><span data-ttu-id="be06c-123">カーソルを初期化する</span><span class="sxs-lookup"><span data-stu-id="be06c-123">Initialize a cursor</span></span>

<span data-ttu-id="be06c-124">信頼性の高いカタログ リーダーをビルドする最初の手順は、カーソルの実装です。</span><span class="sxs-lookup"><span data-stu-id="be06c-124">The first step in building a reliable catalog reader is implementing a cursor.</span></span> <span data-ttu-id="be06c-125">カタログ カーソルの設計の詳細については、[カタログ参照に関するドキュメント](../../api/catalog-resource.md#cursor)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="be06c-125">For full details about the design of a catalog cursor, see the [catalog reference document](../../api/catalog-resource.md#cursor).</span></span> <span data-ttu-id="be06c-126">要するに、カーソルは、カタログ内のイベントがどの時点まで処理されたかを示すものです。</span><span class="sxs-lookup"><span data-stu-id="be06c-126">In short, cursor is a point in time up to which you have processed events in the catalog.</span></span> <span data-ttu-id="be06c-127">カタログ内のイベントはあるパッケージの発行と他のパッケージの変更を示します。</span><span class="sxs-lookup"><span data-stu-id="be06c-127">Events in the catalog represent package publishes and other package changes.</span></span> <span data-ttu-id="be06c-128">これまでに (開始以降) NuGet に発行されたすべてのパッケージに関心がある場合は、カーソルを初期化してタイムスタンプが "最小値" (.NET の場合は `DateTime.MinValue` など) になるようにします。</span><span class="sxs-lookup"><span data-stu-id="be06c-128">If you care about all packages ever published to NuGet (since the beginning of time), you would initialize your cursor to a "minimum value" timestamp (e.g. `DateTime.MinValue` in .NET).</span></span> <span data-ttu-id="be06c-129">これから発行されるパッケージのみに関心がある場合は、カーソル値を初期化する際に現在のタイムスタンプを使用します。</span><span class="sxs-lookup"><span data-stu-id="be06c-129">If you care only about packages published starting now, you would use the current timestamp as your initial cursor value.</span></span>

<span data-ttu-id="be06c-130">このガイドでは、タイムスタンプが 1 時間前になるようにカーソルを初期化します。</span><span class="sxs-lookup"><span data-stu-id="be06c-130">For this guide, we'll initialize our cursor to a timestamp one hour ago.</span></span> <span data-ttu-id="be06c-131">ここでは、単にそのタイムスタンプをメモリに保存します。</span><span class="sxs-lookup"><span data-stu-id="be06c-131">For now, just save that timestamp in memory.</span></span>

```cs
DateTime cursor = DateTime.UtcNow.AddHours(-1);
```

## <a name="determine-catalog-index-url"></a><span data-ttu-id="be06c-132">カタログ インデックス URL を判別する</span><span class="sxs-lookup"><span data-stu-id="be06c-132">Determine catalog index URL</span></span>

<span data-ttu-id="be06c-133">NuGet API のすべてのリソース (エンドポイント) の場所は、[サービス インデックス](../../api/service-index.md)を使用して検出する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be06c-133">The location of every resource (endpoint) in the NuGet API should be discovered using the [service index](../../api/service-index.md).</span></span> <span data-ttu-id="be06c-134">このガイドでは nuget.org に焦点を当てているため、nuget.org のサービス インデックスを使用します。</span><span class="sxs-lookup"><span data-stu-id="be06c-134">Because this guide focuses on nuget.org, we'll be using nuget.org's service index.</span></span>

    GET https://api.nuget.org/v3/index.json

<span data-ttu-id="be06c-135">サービス ドキュメントは、nuget.org のすべてのリソースを含む JSON ドキュメントです。`@type` プロパティの値が `Catalog/3.0.0` のリソースを見つけてください。</span><span class="sxs-lookup"><span data-stu-id="be06c-135">The service document is JSON document containing all of the resources on nuget.org. Look for the resource having the `@type` property value of `Catalog/3.0.0`.</span></span> <span data-ttu-id="be06c-136">関連付けられている `@id`プロパティの値は、カタログ インデックス自体の URL です。</span><span class="sxs-lookup"><span data-stu-id="be06c-136">The associated `@id` property value is the URL to the catalog index itself.</span></span> 

## <a name="find-new-catalog-leaves"></a><span data-ttu-id="be06c-137">新しいカタログ リーフを見つける</span><span class="sxs-lookup"><span data-stu-id="be06c-137">Find new catalog leaves</span></span>

<span data-ttu-id="be06c-138">前の手順で見つけた `@id` プロパティの値を使用して、カタログ インデックスをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="be06c-138">Using the `@id` property value found in the previous step, download the catalog index:</span></span>

    GET https://api.nuget.org/v3/catalog0/index.json

<span data-ttu-id="be06c-139">[カタログ インデックス](../../api/catalog-resource.md#catalog-index)を逆シリアル化します。</span><span class="sxs-lookup"><span data-stu-id="be06c-139">Deserialize the [catalog index](../../api/catalog-resource.md#catalog-index).</span></span> <span data-ttu-id="be06c-140">すべての[カタログ ページ オブジェクト](../../api/catalog-resource.md#catalog-page-object-in-the-index)を、現在のカーソル値以下の `commitTimeStamp` でフィルタリングします。</span><span class="sxs-lookup"><span data-stu-id="be06c-140">Filter out all [catalog page objects](../../api/catalog-resource.md#catalog-page-object-in-the-index) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="be06c-141">残りのカタログ ページごとに、`@id` プロパティを使用して完全なドキュメントをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="be06c-141">For each remaining catalog page, download the full document using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/page2926.json

<span data-ttu-id="be06c-142">[カタログ ページ](../../api/catalog-resource.md#catalog-page)を逆シリアル化します。</span><span class="sxs-lookup"><span data-stu-id="be06c-142">Deserialize the [catalog page](../../api/catalog-resource.md#catalog-page).</span></span> <span data-ttu-id="be06c-143">すべての[カタログ リーフ オブジェクト](../../api/catalog-resource.md#catalog-item-object-in-a-page)を、現在のカーソル値以下の `commitTimeStamp` でフィルタリングします。</span><span class="sxs-lookup"><span data-stu-id="be06c-143">Filter out all [catalog leaf objects](../../api/catalog-resource.md#catalog-item-object-in-a-page) with `commitTimeStamp` less than or equal to your current cursor value.</span></span>

<span data-ttu-id="be06c-144">フィルタリングされなかったカタログ ページをすべてダウンロードした後、カーソルのタイムスタンプから今までに公開、リスト解除、リスト、または削除されたパッケージを表す一連のカタログ リーフ オブジェクトが示されます。</span><span class="sxs-lookup"><span data-stu-id="be06c-144">After you have downloaded all of the catalog pages not filtered out, you have a set of catalog leaf objects representing packages that have been published, unlisted, listed, or deleted in the time between your cursor timestamp and now.</span></span>

## <a name="process-catalog-leaves"></a><span data-ttu-id="be06c-145">カタログ リーフを処理する</span><span class="sxs-lookup"><span data-stu-id="be06c-145">Process catalog leaves</span></span>

<span data-ttu-id="be06c-146">この時点で、カタログ項目に対して必要なカスタム処理を実行することができます。</span><span class="sxs-lookup"><span data-stu-id="be06c-146">At this point, you can perform any custom processing you'd like on the catalog items.</span></span> <span data-ttu-id="be06c-147">必要なものがパッケージの ID とバージョンのみである場合は、ページで検出されたカタログ項目オブジェクトの `nuget:id` および `nuget:version` プロパティを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="be06c-147">If all you need is the ID and version of the package, you can inspect the `nuget:id` and `nuget:version` properties on the catalog item objects found in the pages.</span></span> <span data-ttu-id="be06c-148">必ず、`@type` プロパティを調べ、カタログ項目が既存のパッケージと削除されたパッケージのどちらに関するものであるかを確認してください。</span><span class="sxs-lookup"><span data-stu-id="be06c-148">Make sure to look at the `@type` property to know if the catalog item concerns an existing package or a deleted package.</span></span>

<span data-ttu-id="be06c-149">パッケージに関するメタデータ (説明、依存関係、.nupkg のサイズなど) に関心がある場合は、`@id` プロパティを使用して[カタログ リーフ ドキュメント](../../api/catalog-resource.md#catalog-leaf)をフェッチできます。</span><span class="sxs-lookup"><span data-stu-id="be06c-149">If you are interested in the metadata about the package (such at the description, dependencies, .nupkg size, etc), you can fetch the [catalog leaf document](../../api/catalog-resource.md#catalog-leaf) using the `@id` property.</span></span>

    GET https://api.nuget.org/v3/catalog0/data/2015.02.01.11.18.40/windowsazure.storage.1.0.0.json

<span data-ttu-id="be06c-150">このドキュメントには、[パッケージ メタデータ リソース](../../api/registration-base-url-resource.md)などに含まれるすべてのメタデータが示されます。</span><span class="sxs-lookup"><span data-stu-id="be06c-150">This document has all of the metadata included in the [package metadata resource](../../api/registration-base-url-resource.md), and more!</span></span>

<span data-ttu-id="be06c-151">この手順では、カスタム ロジックを実装します。</span><span class="sxs-lookup"><span data-stu-id="be06c-151">This step is where you implement your custom logic.</span></span> <span data-ttu-id="be06c-152">このガイドの他の手順は、カタログ リーフでの実行内容に関係なく、ほとんど同じ方法で行われます。</span><span class="sxs-lookup"><span data-stu-id="be06c-152">The other steps in this guide are implemented in pretty much the same way not matter what you are doing with the catalog leaves.</span></span>

### <a name="downloading-the-nupkg"></a><span data-ttu-id="be06c-153">.nupkg のダウンロード</span><span class="sxs-lookup"><span data-stu-id="be06c-153">Downloading the .nupkg</span></span>

<span data-ttu-id="be06c-154">カタログで検出されたパッケージ用の .nupkg をダウンロードしたい場合は、[パッケージ コンテンツ リソース](../../api/package-base-address-resource.md)を使用できます。</span><span class="sxs-lookup"><span data-stu-id="be06c-154">If you are interested in downloading the .nupkg's for packages found in the catalog, you can use the [package content resource](../../api/package-base-address-resource.md).</span></span> <span data-ttu-id="be06c-155">ただし、パッケージがカタログで検出されてから、パッケージ コンテンツ リソースで使用できるようになるまで短い遅延が発生することに注意してください。</span><span class="sxs-lookup"><span data-stu-id="be06c-155">However, note that there is a short delay between when a package is found in catalog and when it's available in the package content resource.</span></span> <span data-ttu-id="be06c-156">したがって、カタログで検出されたパッケージの .nupkg をダウンロードしようとしたときに `404 Not Found` が発生した場合は、しばらくしてから再試行するだけです。</span><span class="sxs-lookup"><span data-stu-id="be06c-156">Therefore, if you encounter `404 Not Found` when attempting to download a .nupkg for a package that you found in the catalog, simply retry a short time later.</span></span> <span data-ttu-id="be06c-157">この遅延の修正については、GitHub の問題 [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455) で追跡されています。</span><span class="sxs-lookup"><span data-stu-id="be06c-157">Fixing this delay is tracked by GitHub issue [NuGet/NuGetGallery#3455](https://github.com/NuGet/NuGetGallery/issues/3455).</span></span>

## <a name="move-the-cursor-forward"></a><span data-ttu-id="be06c-158">カーソルを先に進める</span><span class="sxs-lookup"><span data-stu-id="be06c-158">Move the cursor forward</span></span>

<span data-ttu-id="be06c-159">カタログ項目を正しく処理したら、保存する新しいカーソル値を判別する必要があります。</span><span class="sxs-lookup"><span data-stu-id="be06c-159">Once you have successfully processed the catalog items, you need to determine the new cursor value to save.</span></span> <span data-ttu-id="be06c-160">これを行うには、処理したすべてのカタログ項目の最大 (最新) `commitTimeStamp` を検索します。</span><span class="sxs-lookup"><span data-stu-id="be06c-160">To do this, find the maximum (latest chronologically) `commitTimeStamp` of all catalog items that you processed.</span></span> <span data-ttu-id="be06c-161">これが新しいカーソル値になります。</span><span class="sxs-lookup"><span data-stu-id="be06c-161">This is your new cursor value.</span></span> <span data-ttu-id="be06c-162">データベース、ファイル システム、または BLOB ストレージなどのいくつかの固定ストアに保存します。</span><span class="sxs-lookup"><span data-stu-id="be06c-162">Save it to some persistent store, like a database, file system, or blob storage.</span></span> <span data-ttu-id="be06c-163">カタログ項目をさらに取得する場合は、この固定ストアのカーソル値を初期化して、[最初の手順](#initialize-a-cursor)から開始するだけです。</span><span class="sxs-lookup"><span data-stu-id="be06c-163">When you want to get more catalog items, simply start from the [first step](#initialize-a-cursor) by initializing your cursor value from this persistent store.</span></span>

<span data-ttu-id="be06c-164">アプリケーションが例外やフォールトをスローする場合は、カーソルを先に進めないでください。</span><span class="sxs-lookup"><span data-stu-id="be06c-164">If your application throws an exception or faults, don't move the cursor forward.</span></span> <span data-ttu-id="be06c-165">カーソルを先に進めるということは、カーソルの前のカタログ項目を再度処理する必要がないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="be06c-165">Moving the cursor forward has the meaning that you never again need to process catalog items before your cursor.</span></span>

<span data-ttu-id="be06c-166">なんらかの理由で、カタログ リーフの処理方法にバグが発生した場合は、その時点までカーソルを戻すだけで、コードで以前のカタログ項目を再処理することができます。</span><span class="sxs-lookup"><span data-stu-id="be06c-166">If, for some reason, you have a bug in how you process catalog leaves, you can simply move your cursor backward in time and allow your code to reprocess the old catalog items.</span></span>

## <a name="c-sample-code"></a><span data-ttu-id="be06c-167">C# のサンプル コード</span><span class="sxs-lookup"><span data-stu-id="be06c-167">C# sample code</span></span>

<span data-ttu-id="be06c-168">カタログは HTTP 経由で使用可能な一連の JSON ドキュメントであるため、HTTP クライアントと JSON デシリアライザーを持つ任意のプログラミング言語を使用して対話することができます。</span><span class="sxs-lookup"><span data-stu-id="be06c-168">Because the catalog is a set of JSON documents available over HTTP, it can be interacted with using any programming language that has an HTTP client and JSON deserializer.</span></span>

<span data-ttu-id="be06c-169">C# のサンプルは、[NuGet/Sample リポジトリ](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample)で入手可能です。</span><span class="sxs-lookup"><span data-stu-id="be06c-169">C# samples are available in the [NuGet/Samples repository](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample).</span></span>

```cli
git clone https://github.com/NuGet/Samples.git
```

### <a name="catalog-sdk"></a><span data-ttu-id="be06c-170">カタログ SDK</span><span class="sxs-lookup"><span data-stu-id="be06c-170">Catalog SDK</span></span>

<span data-ttu-id="be06c-171">カタログを使用する場合、プレリリース版の .NET カタログ SDK パッケージである [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog) を使用するのが最も簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="be06c-171">The easiest way to consume the catalog is to use the pre-release .NET catalog SDK package: [NuGet.Protocol.Catalog](https://dotnet.myget.org/feed/nuget-build/package/nuget/NuGet.Protocol.Catalog).</span></span> <span data-ttu-id="be06c-172">このパッケージは、`nuget-build` MyGet フィード (NuGet パッケージ ソース URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json` を使用する場合) で入手可能です。</span><span class="sxs-lookup"><span data-stu-id="be06c-172">This package is available on the `nuget-build` MyGet feed, for which you use the NuGet package source URL `https://dotnet.myget.org/F/nuget-build/api/v3/index.json`.</span></span>

<span data-ttu-id="be06c-173">このパッケージを、`netstandard1.3` 以上 (.NET Framework 4.6 など) と互換性のあるプロジェクトにインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="be06c-173">You can install this package to a project compatible with `netstandard1.3` or greater (such as .NET Framework 4.6).</span></span>

<span data-ttu-id="be06c-174">このパッケージを使用するサンプルは、GitHub の [NuGet.Protocol.Catalog.Sample プロジェクト](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample)で入手できます。</span><span class="sxs-lookup"><span data-stu-id="be06c-174">A sample using this package is available on GitHub in the [NuGet.Protocol.Catalog.Sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/NuGet.Protocol.Catalog.Sample).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="be06c-175">出力例</span><span class="sxs-lookup"><span data-stu-id="be06c-175">Sample output</span></span>

```output
2017-11-10T22:16:44.8689025+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.2.
2017-11-10T22:16:54.6972769+00:00: Found package details leaf for xSkrape.APIWrapper.REST 1.0.1.
2017-11-10T22:19:20.6385542+00:00: Found package details leaf for Platform.EnUnity 1.0.8.
...
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.1.
2017-11-10T23:05:04.9695890+00:00: Found package details leaf for xSkrape.APIWrapper.Base 1.0.2.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
Processing the catalog leafs failed. Retrying.
fail: NuGet.Protocol.Catalog.LoggerCatalogLeafProcessor[0]
      10 catalog commits have been processed. We will now simulate a failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      Failed to process leaf https://api.nuget.org/v3/catalog0/data/2017.11.10.23.07.23/veiculox.model.0.0.15.json (VeiculoX.Model 0.0.15, PackageDetails).
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      13 out of 59 leaves were left incomplete due to a processing failure.
warn: NuGet.Protocol.Catalog.CatalogProcessor[0]
      1 out of 1 pages were left incomplete due to a processing failure.
2017-11-10T23:07:23.1303569+00:00: Found package details leaf for VeiculoX.Model 0.0.15.
2017-11-10T23:07:33.0212446+00:00: Found package details leaf for VeiculoX.Model 0.0.14.
2017-11-10T23:07:41.6621837+00:00: Found package details leaf for VeiculoX.Model 0.0.13.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for CreaSoft.Composition.Web.Extensions 1.1.0.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for DarkXaHTeP.Extensions.Configuration.Consul 0.0.4.
2017-11-10T23:09:58.5728614+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Imaging.Interop.14.0.DesignTime 14.3.25407.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.Intellisense 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.Language.StandardClassification 15.4.27004.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for Microsoft.VisualStudio.ManagedInterfaces 8.0.50727.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.2.
2017-11-10T23:10:09.0574930+00:00: Found package details leaf for xSkrape.APIWrapper.REST.Sample 1.0.3.
```

### <a name="minimal-sample"></a><span data-ttu-id="be06c-176">最小サンプル</span><span class="sxs-lookup"><span data-stu-id="be06c-176">Minimal sample</span></span>

<span data-ttu-id="be06c-177">カタログとの対話を詳細に示す、いくつかの依存関係を含む例については、[CatalogReaderExample サンプル プロジェクト](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="be06c-177">For an example with fewer dependencies that illustrates the interaction with the catalog in more detail, see the [CatalogReaderExample sample project](https://github.com/NuGet/Samples/tree/master/CatalogReaderExample/CatalogReaderExample).</span></span> <span data-ttu-id="be06c-178">プロジェクトは `netcoreapp2.0` をターゲットとし、[NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (サービス インデックスを解決する場合) および [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (JSON シリアル化解除の場合) に依存します。</span><span class="sxs-lookup"><span data-stu-id="be06c-178">The project targets `netcoreapp2.0` and depends on the [NuGet.Protocol 4.4.0](https://www.nuget.org/packages/NuGet.Protocol/4.4.0) (for resolving the service index) and [Newtonsoft.Json 9.0.1](https://www.nuget.org/packages/Newtonsoft.Json/9.0.1) (for JSON deserialization).</span></span>

<span data-ttu-id="be06c-179">コードの主なロジックは [Program.cs ファイル](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs)に表示されます。</span><span class="sxs-lookup"><span data-stu-id="be06c-179">The main logic of the code is visible in the [Program.cs file](https://github.com/NuGet/Samples/blob/master/CatalogReaderExample/CatalogReaderExample/Program.cs).</span></span>

#### <a name="sample-output"></a><span data-ttu-id="be06c-180">出力例</span><span class="sxs-lookup"><span data-stu-id="be06c-180">Sample output</span></span>

```output
No cursor found. Defaulting to 11/2/2017 9:41:28 PM.
Fetched catalog index https://api.nuget.org/v3/catalog0/index.json.
Fetched catalog page https://api.nuget.org/v3/catalog0/page2935.json.
Processing 69 catalog leaves.
11/2/2017 9:32:35 PM: DotVVM.Compiler.Light 1.1.7 (type is nuget:PackageDetails)
11/2/2017 9:32:35 PM: Momentum.Pm.Api 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:32:44 PM: Momentum.Pm.PortalApi 5.12.181-beta (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Standard 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Genesys.Extensions.Core 3.17.11.40 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.Serialization.Bond 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.AmazonS3 1.0.4 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.DocumentStores.DocumentDb 1.0.6 (type is nuget:PackageDetails)
11/2/2017 9:35:14 PM: Halforbit.DataStores.FileStores.BlobStorage 1.0.5 (type is nuget:PackageDetails)
...
11/2/2017 10:23:54 PM: Cake.GitPackager 0.1.2 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:23:54 PM: UtilPack.NuGet.AssemblyLoading 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Deployment 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:26 PM: UtilPack.NuGet.Common.MSBuild 2.0.0 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: InstaClient 1.0.2 (type is nuget:PackageDetails)
11/2/2017 10:26:36 PM: SecureStrConvertor.VARUN_RUSIYA 1.0.0.5 (type is nuget:PackageDetails)
Writing cursor value: 11/2/2017 10:26:36 PM.
```
