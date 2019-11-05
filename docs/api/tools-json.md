---
title: nuget.exe バージョンを検出するためのツール。
description: のエンドポイント
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: a186db9727bdfd1b55bf73a1f29283352555dede
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611030"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="160b2-103">nuget.exe バージョンを検出するためのツール。</span><span class="sxs-lookup"><span data-stu-id="160b2-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="160b2-104">現在、コンピューター上の最新バージョンの nuget.exe をスクリプト可能な方法で入手するには、いくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="160b2-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="160b2-105">たとえば、nuget.org から[`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/)パッケージをダウンロードして抽出することができます。これにはいくつかの複雑さがあります。これは、既に nuget.exe がある (`nuget.exe install`) 必要があるか、または基本的な解凍ツールを使用して nupkg を解凍し、内部でバイナリを検索する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="160b2-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="160b2-106">既に nuget.exe を持っている場合は、`nuget.exe update -self`を使用することもできますが、これには nuget.exe の既存のコピーが必要です。</span><span class="sxs-lookup"><span data-stu-id="160b2-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="160b2-107">この方法では、最新バージョンも更新されます。</span><span class="sxs-lookup"><span data-stu-id="160b2-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="160b2-108">特定のバージョンを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="160b2-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="160b2-109">`tools.json` エンドポイントを使用して、ブートストラップの問題を解決し、ダウンロードする nuget.exe のバージョンを制御することができます。</span><span class="sxs-lookup"><span data-stu-id="160b2-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="160b2-110">これは、CI/CD 環境またはカスタムスクリプトで使用して、任意のリリースバージョンの nuget.exe を検出してダウンロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="160b2-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="160b2-111">`tools.json` エンドポイントは、認証されていない HTTP 要求 (PowerShell や `wget`の `Invoke-WebRequest` など) を使用してフェッチできます。</span><span class="sxs-lookup"><span data-stu-id="160b2-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="160b2-112">これは、JSON デシリアライザーを使用して解析できます。その後の nuget ダウンロード Url は、認証されていない HTTP 要求を使用してフェッチすることもできます。</span><span class="sxs-lookup"><span data-stu-id="160b2-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="160b2-113">エンドポイントは、`GET` メソッドを使用してフェッチできます。</span><span class="sxs-lookup"><span data-stu-id="160b2-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="160b2-114">エンドポイントの[JSON スキーマ](https://json-schema.org/)については、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="160b2-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="160b2-115">応答</span><span class="sxs-lookup"><span data-stu-id="160b2-115">Response</span></span>

<span data-ttu-id="160b2-116">応答は、使用可能なすべてのバージョンの nuget.exe を含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="160b2-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="160b2-117">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="160b2-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="160b2-118">名</span><span class="sxs-lookup"><span data-stu-id="160b2-118">Name</span></span>      | <span data-ttu-id="160b2-119">[種類]</span><span class="sxs-lookup"><span data-stu-id="160b2-119">Type</span></span>             | <span data-ttu-id="160b2-120">必要</span><span class="sxs-lookup"><span data-stu-id="160b2-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="160b2-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="160b2-121">nuget.exe</span></span> | <span data-ttu-id="160b2-122">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="160b2-122">array of objects</span></span> | <span data-ttu-id="160b2-123">可</span><span class="sxs-lookup"><span data-stu-id="160b2-123">yes</span></span>

<span data-ttu-id="160b2-124">`nuget.exe` 配列の各オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="160b2-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="160b2-125">名</span><span class="sxs-lookup"><span data-stu-id="160b2-125">Name</span></span>     | <span data-ttu-id="160b2-126">[種類]</span><span class="sxs-lookup"><span data-stu-id="160b2-126">Type</span></span>   | <span data-ttu-id="160b2-127">必要</span><span class="sxs-lookup"><span data-stu-id="160b2-127">Required</span></span> | <span data-ttu-id="160b2-128">ノート</span><span class="sxs-lookup"><span data-stu-id="160b2-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="160b2-129">version</span><span class="sxs-lookup"><span data-stu-id="160b2-129">version</span></span>  | <span data-ttu-id="160b2-130">string</span><span class="sxs-lookup"><span data-stu-id="160b2-130">string</span></span> | <span data-ttu-id="160b2-131">可</span><span class="sxs-lookup"><span data-stu-id="160b2-131">yes</span></span>      | <span data-ttu-id="160b2-132">SemVer 2.0.0 文字列</span><span class="sxs-lookup"><span data-stu-id="160b2-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="160b2-133">url</span><span class="sxs-lookup"><span data-stu-id="160b2-133">url</span></span>      | <span data-ttu-id="160b2-134">string</span><span class="sxs-lookup"><span data-stu-id="160b2-134">string</span></span> | <span data-ttu-id="160b2-135">可</span><span class="sxs-lookup"><span data-stu-id="160b2-135">yes</span></span>      | <span data-ttu-id="160b2-136">このバージョンの nuget.exe をダウンロードするための絶対 URL</span><span class="sxs-lookup"><span data-stu-id="160b2-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="160b2-137">準備</span><span class="sxs-lookup"><span data-stu-id="160b2-137">stage</span></span>    | <span data-ttu-id="160b2-138">string</span><span class="sxs-lookup"><span data-stu-id="160b2-138">string</span></span> | <span data-ttu-id="160b2-139">可</span><span class="sxs-lookup"><span data-stu-id="160b2-139">yes</span></span>      | <span data-ttu-id="160b2-140">列挙型文字列</span><span class="sxs-lookup"><span data-stu-id="160b2-140">An enum string</span></span>
<span data-ttu-id="160b2-141">アップロード</span><span class="sxs-lookup"><span data-stu-id="160b2-141">uploaded</span></span> | <span data-ttu-id="160b2-142">string</span><span class="sxs-lookup"><span data-stu-id="160b2-142">string</span></span> | <span data-ttu-id="160b2-143">可</span><span class="sxs-lookup"><span data-stu-id="160b2-143">yes</span></span>      | <span data-ttu-id="160b2-144">バージョンが使用可能になったときの ISO 8601 の概算タイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="160b2-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="160b2-145">配列内の項目は、SemVer 2.0.0 order の降順で並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="160b2-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="160b2-146">この保証は、最も高いバージョン番号に関心のあるクライアントの負担を軽減することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="160b2-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="160b2-147">ただし、これは、リストが時系列順に並べ替えられていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="160b2-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="160b2-148">たとえば、古いメジャーバージョンが上位のメジャーバージョンより後の日付でサービスされている場合、このサービスバージョンは一覧の先頭に表示されません。</span><span class="sxs-lookup"><span data-stu-id="160b2-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="160b2-149">*タイムスタンプ*によって最新バージョンがリリースされるようにするには、単に `uploaded` 文字列で配列を並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="160b2-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="160b2-150">これは、`uploaded` タイムスタンプが[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)形式であり、辞書式並べ替え (つまり、単純な文字列の並べ替え) を使用して時系列で並べ替えることができるためです。</span><span class="sxs-lookup"><span data-stu-id="160b2-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="160b2-151">`stage` プロパティは、このバージョンのツールがどのように吟味されるかを示します。</span><span class="sxs-lookup"><span data-stu-id="160b2-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="160b2-152">段階</span><span class="sxs-lookup"><span data-stu-id="160b2-152">Stage</span></span>              | <span data-ttu-id="160b2-153">説明</span><span class="sxs-lookup"><span data-stu-id="160b2-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="160b2-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="160b2-154">EarlyAccessPreview</span></span> | <span data-ttu-id="160b2-155">[ダウンロード web ページ](https://www.nuget.org/downloads)にはまだ表示されていないため、パートナーが検証する必要があります</span><span class="sxs-lookup"><span data-stu-id="160b2-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="160b2-156">リリース済み</span><span class="sxs-lookup"><span data-stu-id="160b2-156">Released</span></span>           | <span data-ttu-id="160b2-157">ダウンロードサイトで利用できますが、大規模な消費にはまだ推奨されていません。</span><span class="sxs-lookup"><span data-stu-id="160b2-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="160b2-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="160b2-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="160b2-159">ダウンロードサイトで利用可能であり、使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="160b2-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="160b2-160">最新の推奨バージョンを使用するための簡単な方法の1つは、リスト内の `stage` 値が `ReleasedAndBlessed`の最初のバージョンを取得することです。</span><span class="sxs-lookup"><span data-stu-id="160b2-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="160b2-161">これは、バージョンが SemVer 2.0.0 order で並べ替えられているために機能します。</span><span class="sxs-lookup"><span data-stu-id="160b2-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="160b2-162">Nuget.org の `NuGet.CommandLine` パッケージは、通常、`ReleasedAndBlessed` バージョンでのみ更新されます。</span><span class="sxs-lookup"><span data-stu-id="160b2-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="160b2-163">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="160b2-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="160b2-164">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="160b2-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
