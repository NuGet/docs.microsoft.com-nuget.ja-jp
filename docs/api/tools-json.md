---
title: nuget.exe バージョンを検出するための tools.js
description: のエンドポイント
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: eb28ccbc4460663b0f149d2d08e9b47dd69847c7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773815"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="96680-103">nuget.exe バージョンを検出するための tools.js</span><span class="sxs-lookup"><span data-stu-id="96680-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="96680-104">現在、コンピューター上の最新バージョンの nuget.exe をスクリプトによって取得する方法はいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="96680-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="96680-105">たとえば、nuget.org からパッケージをダウンロードして抽出することができ [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) ます。これにはいくつかの複雑さがあります。これは、既に nuget.exe (の場合) を持っている必要があるか、 `nuget.exe install` または基本的な解凍ツールを使用して nupkg を解凍し、内部でバイナリを検索する必要があるためです。</span><span class="sxs-lookup"><span data-stu-id="96680-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="96680-106">既に nuget.exe がある場合は、を使用することもでき `nuget.exe update -self` ますが、nuget.exe の既存のコピーが必要です。</span><span class="sxs-lookup"><span data-stu-id="96680-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="96680-107">この方法では、最新バージョンも更新されます。</span><span class="sxs-lookup"><span data-stu-id="96680-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="96680-108">特定のバージョンを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="96680-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="96680-109">`tools.json`エンドポイントは、ブートストラップの問題を解決し、ダウンロードする nuget.exe のバージョンを制御できるようにするために使用できます。</span><span class="sxs-lookup"><span data-stu-id="96680-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="96680-110">これは、CI/CD 環境またはカスタムスクリプトで使用して、nuget.exe のリリースバージョンを検出してダウンロードすることができます。</span><span class="sxs-lookup"><span data-stu-id="96680-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="96680-111">`tools.json`エンドポイントは、認証されていない HTTP 要求 (PowerShell やなど) を使用してフェッチでき `Invoke-WebRequest` `wget` ます。</span><span class="sxs-lookup"><span data-stu-id="96680-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="96680-112">JSON デシリアライザーを使用して解析できます。それ以降の nuget.exe ダウンロード Url は、認証されていない HTTP 要求を使用してフェッチすることもできます。</span><span class="sxs-lookup"><span data-stu-id="96680-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="96680-113">エンドポイントは、メソッドを使用してフェッチでき `GET` ます。</span><span class="sxs-lookup"><span data-stu-id="96680-113">The endpoint can be fetched using the `GET` method:</span></span>

```
GET https://dist.nuget.org/tools.json
```

<span data-ttu-id="96680-114">エンドポイントの [JSON スキーマ](https://json-schema.org/) については、次を参照してください。</span><span class="sxs-lookup"><span data-stu-id="96680-114">The [JSON schema](https://json-schema.org/) for the endpoint is available here:</span></span>

```
GET https://dist.nuget.org/tools.schema.json
```

## <a name="response"></a><span data-ttu-id="96680-115">応答</span><span class="sxs-lookup"><span data-stu-id="96680-115">Response</span></span>

<span data-ttu-id="96680-116">応答は、使用可能なすべてのバージョンの nuget.exe を含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="96680-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="96680-117">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="96680-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="96680-118">名前</span><span class="sxs-lookup"><span data-stu-id="96680-118">Name</span></span>      | <span data-ttu-id="96680-119">Type</span><span class="sxs-lookup"><span data-stu-id="96680-119">Type</span></span>             | <span data-ttu-id="96680-120">必須</span><span class="sxs-lookup"><span data-stu-id="96680-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="96680-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="96680-121">nuget.exe</span></span> | <span data-ttu-id="96680-122">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="96680-122">array of objects</span></span> | <span data-ttu-id="96680-123">はい</span><span class="sxs-lookup"><span data-stu-id="96680-123">yes</span></span>

<span data-ttu-id="96680-124">配列内の各オブジェクト `nuget.exe` には、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="96680-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="96680-125">名前</span><span class="sxs-lookup"><span data-stu-id="96680-125">Name</span></span>     | <span data-ttu-id="96680-126">Type</span><span class="sxs-lookup"><span data-stu-id="96680-126">Type</span></span>   | <span data-ttu-id="96680-127">必須</span><span class="sxs-lookup"><span data-stu-id="96680-127">Required</span></span> | <span data-ttu-id="96680-128">Notes</span><span class="sxs-lookup"><span data-stu-id="96680-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="96680-129">version</span><span class="sxs-lookup"><span data-stu-id="96680-129">version</span></span>  | <span data-ttu-id="96680-130">string</span><span class="sxs-lookup"><span data-stu-id="96680-130">string</span></span> | <span data-ttu-id="96680-131">はい</span><span class="sxs-lookup"><span data-stu-id="96680-131">yes</span></span>      | <span data-ttu-id="96680-132">SemVer 2.0.0 文字列</span><span class="sxs-lookup"><span data-stu-id="96680-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="96680-133">url</span><span class="sxs-lookup"><span data-stu-id="96680-133">url</span></span>      | <span data-ttu-id="96680-134">string</span><span class="sxs-lookup"><span data-stu-id="96680-134">string</span></span> | <span data-ttu-id="96680-135">はい</span><span class="sxs-lookup"><span data-stu-id="96680-135">yes</span></span>      | <span data-ttu-id="96680-136">このバージョンの nuget.exe をダウンロードするための絶対 URL</span><span class="sxs-lookup"><span data-stu-id="96680-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="96680-137">準備</span><span class="sxs-lookup"><span data-stu-id="96680-137">stage</span></span>    | <span data-ttu-id="96680-138">string</span><span class="sxs-lookup"><span data-stu-id="96680-138">string</span></span> | <span data-ttu-id="96680-139">はい</span><span class="sxs-lookup"><span data-stu-id="96680-139">yes</span></span>      | <span data-ttu-id="96680-140">列挙型文字列</span><span class="sxs-lookup"><span data-stu-id="96680-140">An enum string</span></span>
<span data-ttu-id="96680-141">アップロード</span><span class="sxs-lookup"><span data-stu-id="96680-141">uploaded</span></span> | <span data-ttu-id="96680-142">string</span><span class="sxs-lookup"><span data-stu-id="96680-142">string</span></span> | <span data-ttu-id="96680-143">はい</span><span class="sxs-lookup"><span data-stu-id="96680-143">yes</span></span>      | <span data-ttu-id="96680-144">バージョンが使用可能になったときの ISO 8601 の概算タイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="96680-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="96680-145">配列内の項目は、SemVer 2.0.0 order の降順で並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="96680-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="96680-146">この保証は、最も高いバージョン番号に関心のあるクライアントの負担を軽減することを目的としています。</span><span class="sxs-lookup"><span data-stu-id="96680-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="96680-147">ただし、これは、リストが時系列順に並べ替えられていないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="96680-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="96680-148">たとえば、古いメジャーバージョンが上位のメジャーバージョンより後の日付でサービスされている場合、このサービスバージョンは一覧の先頭に表示されません。</span><span class="sxs-lookup"><span data-stu-id="96680-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="96680-149">*タイムスタンプ* によって最新バージョンがリリースされるようにするには、単に文字列で配列を並べ替え `uploaded` ます。</span><span class="sxs-lookup"><span data-stu-id="96680-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="96680-150">これは、 `uploaded` タイムスタンプが [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) 形式であり、辞書式並べ替え (つまり、単純な文字列の並べ替え) を使用して時系列で並べ替えることができるためです。</span><span class="sxs-lookup"><span data-stu-id="96680-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="96680-151">プロパティは、 `stage` このバージョンのツールがどのように吟味されるかを示します。</span><span class="sxs-lookup"><span data-stu-id="96680-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="96680-152">段階</span><span class="sxs-lookup"><span data-stu-id="96680-152">Stage</span></span>              | <span data-ttu-id="96680-153">意味</span><span class="sxs-lookup"><span data-stu-id="96680-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="96680-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="96680-154">EarlyAccessPreview</span></span> | <span data-ttu-id="96680-155">[ダウンロード web ページ](https://www.nuget.org/downloads)にはまだ表示されていないため、パートナーが検証する必要があります</span><span class="sxs-lookup"><span data-stu-id="96680-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="96680-156">リリース済み</span><span class="sxs-lookup"><span data-stu-id="96680-156">Released</span></span>           | <span data-ttu-id="96680-157">ダウンロードサイトで利用できますが、大規模な消費にはまだ推奨されていません。</span><span class="sxs-lookup"><span data-stu-id="96680-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="96680-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="96680-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="96680-159">ダウンロードサイトで利用可能であり、使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="96680-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="96680-160">最新の推奨バージョンを使用するための簡単な方法の1つは、リストの値がである最初のバージョンを取得することです `stage` `ReleasedAndBlessed` 。</span><span class="sxs-lookup"><span data-stu-id="96680-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="96680-161">これは、バージョンが SemVer 2.0.0 order で並べ替えられているために機能します。</span><span class="sxs-lookup"><span data-stu-id="96680-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="96680-162">`NuGet.CommandLine`Nuget.org のパッケージは、通常、バージョンでのみ更新され `ReleasedAndBlessed` ます。</span><span class="sxs-lookup"><span data-stu-id="96680-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="96680-163">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="96680-163">Sample request</span></span>

```
GET https://dist.nuget.org/tools.json
```

### <a name="sample-response"></a><span data-ttu-id="96680-164">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="96680-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
