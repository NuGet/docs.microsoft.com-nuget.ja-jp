---
title: nuget.exe のバージョンを検出するための tools.json
description: エンドポイント
author: jver
ms.author: jver
ms.date: 08/16/2018
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: 003139abac7808dbdaef4aa66119e09772db2b4f
ms.sourcegitcommit: b6efd4b210d92bf163c67e412ca9a5a018d117f0
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/26/2019
ms.locfileid: "56852534"
---
# <a name="toolsjson-for-discovering-nugetexe-versions"></a><span data-ttu-id="039fc-103">nuget.exe のバージョンを検出するための tools.json</span><span class="sxs-lookup"><span data-stu-id="039fc-103">tools.json for discovering nuget.exe versions</span></span>

<span data-ttu-id="039fc-104">今日では、これにはスクリプト可能な方法でコンピューターに最新バージョンの nuget.exe を取得するいくつかの方法があります。</span><span class="sxs-lookup"><span data-stu-id="039fc-104">Today, there are a few ways to get the latest version of nuget.exe on your machine in a scriptable fashion.</span></span> <span data-ttu-id="039fc-105">たとえば、ダウンロードして抽出、 [ `NuGet.CommandLine` ](https://www.nuget.org/packages/NuGet.CommandLine/) nuget.org からパッケージ。Nuget.exe があるかが何らかの複雑性があります (の`nuget.exe install`) か、基本的な解凍ツールを使用して .nupkg を解凍し、バイナリの内側の検索にあります。</span><span class="sxs-lookup"><span data-stu-id="039fc-105">For example, you can download and extract the [`NuGet.CommandLine`](https://www.nuget.org/packages/NuGet.CommandLine/) package from nuget.org. This has some complexity since it either requires that you already have nuget.exe (for `nuget.exe install`) or you have to unzip the .nupkg using a basic unzip tool and find the binary inside.</span></span>

<span data-ttu-id="039fc-106">Nuget.exe 既にある場合も行えます`nuget.exe update -self`nuget.exe の既存のコピーをしなくても必要です。</span><span class="sxs-lookup"><span data-stu-id="039fc-106">If you already have nuget.exe, you can also use `nuget.exe update -self`, however this also requires having an existing copy of nuget.exe.</span></span> <span data-ttu-id="039fc-107">このアプローチでは、最新バージョンにしても更新されます。</span><span class="sxs-lookup"><span data-stu-id="039fc-107">This approach also updates you to the latest version.</span></span> <span data-ttu-id="039fc-108">特定のバージョンの使用はできません。</span><span class="sxs-lookup"><span data-stu-id="039fc-108">It does not allow the use of a specific version.</span></span>

<span data-ttu-id="039fc-109">`tools.json`エンドポイントがあるブートス トラップの問題を解決両方をダウンロードする nuget.exe のバージョンを制御できるようにするとします。</span><span class="sxs-lookup"><span data-stu-id="039fc-109">The `tools.json` endpoint is available to both solve the bootstrapping problem and to give control of the version of nuget.exe that you download.</span></span> <span data-ttu-id="039fc-110">これは、できます CI/CD 環境や、カスタム スクリプトで検出し、任意のリリース バージョンの nuget.exe をダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="039fc-110">This can be used in CI/CD environments or in custom scripts to discover and download any released version of nuget.exe.</span></span>

<span data-ttu-id="039fc-111">`tools.json`エンドポイントは、認証されていない HTTP 要求を使用して取得できます (例: `Invoke-WebRequest` powershell または`wget`)。</span><span class="sxs-lookup"><span data-stu-id="039fc-111">The `tools.json` endpoint can be fetched using an unauthenticated HTTP request (e.g. `Invoke-WebRequest` in PowerShell or `wget`).</span></span> <span data-ttu-id="039fc-112">JSON デシリアライザーを使用して解析できを使用して Url をフェッチすることも、後続の nuget.exe ダウンロードには、HTTP 要求が認証されていません。</span><span class="sxs-lookup"><span data-stu-id="039fc-112">It can be parsed using a JSON deserializer and subsequent nuget.exe download URLs can also be fetched using unauthenticated HTTP requests.</span></span>

<span data-ttu-id="039fc-113">使用して、エンドポイントをフェッチすることができます、`GET`メソッド。</span><span class="sxs-lookup"><span data-stu-id="039fc-113">The endpoint can be fetched using the `GET` method:</span></span>

    GET https://dist.nuget.org/tools.json

<span data-ttu-id="039fc-114">[JSON スキーマ](http://json-schema.org/)のエンドポイントは、ここで使用します。</span><span class="sxs-lookup"><span data-stu-id="039fc-114">The [JSON schema](http://json-schema.org/) for the endpoint is available here:</span></span>

    GET https://dist.nuget.org/tools.schema.json

## <a name="response"></a><span data-ttu-id="039fc-115">応答</span><span class="sxs-lookup"><span data-stu-id="039fc-115">Response</span></span>

<span data-ttu-id="039fc-116">応答は、すべての利用可能なバージョンの nuget.exe を含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="039fc-116">The response is a JSON document containing all of the available versions of nuget.exe.</span></span>

<span data-ttu-id="039fc-117">ルート JSON オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="039fc-117">The root JSON object has the following property:</span></span>

<span data-ttu-id="039fc-118">名前</span><span class="sxs-lookup"><span data-stu-id="039fc-118">Name</span></span>      | <span data-ttu-id="039fc-119">種類</span><span class="sxs-lookup"><span data-stu-id="039fc-119">Type</span></span>             | <span data-ttu-id="039fc-120">必須</span><span class="sxs-lookup"><span data-stu-id="039fc-120">Required</span></span>
--------- | ---------------- | --------
<span data-ttu-id="039fc-121">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="039fc-121">nuget.exe</span></span> | <span data-ttu-id="039fc-122">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="039fc-122">array of objects</span></span> | <span data-ttu-id="039fc-123">可</span><span class="sxs-lookup"><span data-stu-id="039fc-123">yes</span></span>

<span data-ttu-id="039fc-124">内の各オブジェクト、`nuget.exe`配列は、次のプロパティ。</span><span class="sxs-lookup"><span data-stu-id="039fc-124">Each object in the `nuget.exe` array has the following properties:</span></span>

<span data-ttu-id="039fc-125">名前</span><span class="sxs-lookup"><span data-stu-id="039fc-125">Name</span></span>     | <span data-ttu-id="039fc-126">種類</span><span class="sxs-lookup"><span data-stu-id="039fc-126">Type</span></span>   | <span data-ttu-id="039fc-127">必須</span><span class="sxs-lookup"><span data-stu-id="039fc-127">Required</span></span> | <span data-ttu-id="039fc-128">メモ</span><span class="sxs-lookup"><span data-stu-id="039fc-128">Notes</span></span>
-------- | ------ | -------- | -----
<span data-ttu-id="039fc-129">version</span><span class="sxs-lookup"><span data-stu-id="039fc-129">version</span></span>  | <span data-ttu-id="039fc-130">string</span><span class="sxs-lookup"><span data-stu-id="039fc-130">string</span></span> | <span data-ttu-id="039fc-131">可</span><span class="sxs-lookup"><span data-stu-id="039fc-131">yes</span></span>      | <span data-ttu-id="039fc-132">A SemVer 2.0.0 string</span><span class="sxs-lookup"><span data-stu-id="039fc-132">A SemVer 2.0.0 string</span></span>
<span data-ttu-id="039fc-133">url</span><span class="sxs-lookup"><span data-stu-id="039fc-133">url</span></span>      | <span data-ttu-id="039fc-134">string</span><span class="sxs-lookup"><span data-stu-id="039fc-134">string</span></span> | <span data-ttu-id="039fc-135">可</span><span class="sxs-lookup"><span data-stu-id="039fc-135">yes</span></span>      | <span data-ttu-id="039fc-136">このバージョンの nuget.exe をダウンロードするための絶対 URL</span><span class="sxs-lookup"><span data-stu-id="039fc-136">An absolute URL for downloading this version of nuget.exe</span></span>
<span data-ttu-id="039fc-137">ステージ</span><span class="sxs-lookup"><span data-stu-id="039fc-137">stage</span></span>    | <span data-ttu-id="039fc-138">string</span><span class="sxs-lookup"><span data-stu-id="039fc-138">string</span></span> | <span data-ttu-id="039fc-139">可</span><span class="sxs-lookup"><span data-stu-id="039fc-139">yes</span></span>      | <span data-ttu-id="039fc-140">列挙型の文字列</span><span class="sxs-lookup"><span data-stu-id="039fc-140">An enum string</span></span>
<span data-ttu-id="039fc-141">アップロード</span><span class="sxs-lookup"><span data-stu-id="039fc-141">uploaded</span></span> | <span data-ttu-id="039fc-142">string</span><span class="sxs-lookup"><span data-stu-id="039fc-142">string</span></span> | <span data-ttu-id="039fc-143">可</span><span class="sxs-lookup"><span data-stu-id="039fc-143">yes</span></span>      | <span data-ttu-id="039fc-144">バージョンを利用可能であった場合のおおよその ISO 8601 のタイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="039fc-144">An approximate ISO 8601 timestamp of when the version was made available</span></span>

<span data-ttu-id="039fc-145">配列内の項目は SemVer 2.0.0 の順序を降順で並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="039fc-145">The items in the array will be sorted in descending, SemVer 2.0.0 order.</span></span> <span data-ttu-id="039fc-146">この保証は最新のバージョン番号に関心がクライアントの負荷を軽減するためのものです。</span><span class="sxs-lookup"><span data-stu-id="039fc-146">This guarantee is meant to reduce the burden of a client that is interested in highest version number.</span></span> <span data-ttu-id="039fc-147">ただし、リストが順に並べ替えられていないことをこのわけです。</span><span class="sxs-lookup"><span data-stu-id="039fc-147">However this does mean that the list is not sorted in chronological order.</span></span> <span data-ttu-id="039fc-148">たとえば、下のメジャー バージョンは、以上のメジャー バージョンより後の日付でサービスが場合、このサービスのバージョンは、一覧の上部にあるは表示されません。</span><span class="sxs-lookup"><span data-stu-id="039fc-148">For example, if a lower major version is serviced at a date later than a higher major version, this serviced version will not appear at the top of the list.</span></span> <span data-ttu-id="039fc-149">リリースされた最新バージョンの場合*タイムスタンプ*、単に、配列の並べ替え、`uploaded`文字列。</span><span class="sxs-lookup"><span data-stu-id="039fc-149">If you want the latest version released by *timestamp*, simply sort the array by the `uploaded` string.</span></span> <span data-ttu-id="039fc-150">なので、`uploaded`タイムスタンプが、 [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)形式を辞書式順序の並べ替え (単純な文字列の並べ替えなど) を使用して古い順に並べ替えできます。</span><span class="sxs-lookup"><span data-stu-id="039fc-150">This works because the `uploaded` timestamp is in the [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) format which can be sorted chronologically by using a lexicographical sort (i.e. a simple string sort).</span></span>

<span data-ttu-id="039fc-151">`stage`プロパティは、ツールのこのバージョンは、審査に合格した方法を示します。</span><span class="sxs-lookup"><span data-stu-id="039fc-151">The `stage` property indicates how vetted this version of the tool is.</span></span> 

<span data-ttu-id="039fc-152">段階</span><span class="sxs-lookup"><span data-stu-id="039fc-152">Stage</span></span>              | <span data-ttu-id="039fc-153">説明</span><span class="sxs-lookup"><span data-stu-id="039fc-153">Meaning</span></span>
------------------ | ------
<span data-ttu-id="039fc-154">EarlyAccessPreview</span><span class="sxs-lookup"><span data-stu-id="039fc-154">EarlyAccessPreview</span></span> | <span data-ttu-id="039fc-155">まだ表示されない、[ダウンロード web ページ](https://www.nuget.org/downloads)とパートナーで検証する必要があります</span><span class="sxs-lookup"><span data-stu-id="039fc-155">Not yet visible on the [download web page](https://www.nuget.org/downloads) and should be validated by partners</span></span>
<span data-ttu-id="039fc-156">リリース済み</span><span class="sxs-lookup"><span data-stu-id="039fc-156">Released</span></span>           | <span data-ttu-id="039fc-157">まだ広く使用されている使用量のことをお勧めしますのダウンロード サイトで利用可能</span><span class="sxs-lookup"><span data-stu-id="039fc-157">Available on the download site but is not yet recommended for wide-spread consumption</span></span>
<span data-ttu-id="039fc-158">ReleasedAndBlessed</span><span class="sxs-lookup"><span data-stu-id="039fc-158">ReleasedAndBlessed</span></span> | <span data-ttu-id="039fc-159">ダウンロード サイトで使用可能な従量課金のためお勧め</span><span class="sxs-lookup"><span data-stu-id="039fc-159">Available on the download site and is recommended for consumption</span></span>

<span data-ttu-id="039fc-160">リストを持つ最初のバージョンを最新の 1 つの簡単な方法、推奨されるバージョンは、 `stage` @property`ReleasedAndBlessed`します。</span><span class="sxs-lookup"><span data-stu-id="039fc-160">One simple approach for having the latest, recommended version is to take the first version in the list that has the `stage` value of `ReleasedAndBlessed`.</span></span> <span data-ttu-id="039fc-161">これが機能のバージョンは SemVer 2.0.0 の順序で並べ替えられます。</span><span class="sxs-lookup"><span data-stu-id="039fc-161">This works because the versions are sorted in SemVer 2.0.0 order.</span></span>

<span data-ttu-id="039fc-162">`NuGet.CommandLine`で nuget.org でパッケージがのみ更新通常`ReleasedAndBlessed`バージョン。</span><span class="sxs-lookup"><span data-stu-id="039fc-162">The `NuGet.CommandLine` package on nuget.org is typically only updated with `ReleasedAndBlessed` versions.</span></span>

### <a name="sample-request"></a><span data-ttu-id="039fc-163">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="039fc-163">Sample request</span></span>

    GET https://dist.nuget.org/tools.json

### <a name="sample-response"></a><span data-ttu-id="039fc-164">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="039fc-164">Sample response</span></span>

[!code-JSON [tools-json.json](./_data/tools-json.json)]
