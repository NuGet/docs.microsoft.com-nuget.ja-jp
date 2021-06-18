---
title: NuGet CLI 検索コマンド
description: nuget.exe search コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323662"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="da58d-103">search コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="da58d-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="da58d-104">**適用対象: パッケージ** 消費量 &bullet; **サポートされているバージョン:** 5.8 以上</span><span class="sxs-lookup"><span data-stu-id="da58d-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="da58d-105">指定されたクエリ文字列を使用して、特定のソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="da58d-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="da58d-106">ソースが指定されていない場合は、%AppData%\NuGet\NuGet.Configソースが使用されます。</span><span class="sxs-lookup"><span data-stu-id="da58d-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.Config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="da58d-107">使用方法</span><span class="sxs-lookup"><span data-stu-id="da58d-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="da58d-108">ここで、検索用語は、パッケージ、タグ、パッケージの説明の名前と同様に、パッケージの名前に適用 nuget.org。</span><span class="sxs-lookup"><span data-stu-id="da58d-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="da58d-109">オプション</span><span class="sxs-lookup"><span data-stu-id="da58d-109">Options</span></span>

| <span data-ttu-id="da58d-110">名前</span><span class="sxs-lookup"><span data-stu-id="da58d-110">Name</span></span> | <span data-ttu-id="da58d-111">説明</span><span class="sxs-lookup"><span data-stu-id="da58d-111">Description</span></span> | <span data-ttu-id="da58d-112">使用法</span><span class="sxs-lookup"><span data-stu-id="da58d-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="da58d-113">プレリリース</span><span class="sxs-lookup"><span data-stu-id="da58d-113">PreRelease</span></span> | <span data-ttu-id="da58d-114">プレリリース パッケージは既定では含まれていませんが、この引数を使用して含めできます</span><span class="sxs-lookup"><span data-stu-id="da58d-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="da58d-115">-PreRelease</span><span class="sxs-lookup"><span data-stu-id="da58d-115">-PreRelease</span></span> |
| <span data-ttu-id="da58d-116">source</span><span class="sxs-lookup"><span data-stu-id="da58d-116">Source</span></span> | <span data-ttu-id="da58d-117">既定のソースにクエリを実行する代わりに検索する特定のパッケージ ソースnuget.config</span><span class="sxs-lookup"><span data-stu-id="da58d-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="da58d-118">-Source `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="da58d-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="da58d-119">Take</span><span class="sxs-lookup"><span data-stu-id="da58d-119">Take</span></span> | <span data-ttu-id="da58d-120">返される結果の数。</span><span class="sxs-lookup"><span data-stu-id="da58d-120">The number of results to return.</span></span> <span data-ttu-id="da58d-121">既定値は 20 です。</span><span class="sxs-lookup"><span data-stu-id="da58d-121">The default value is 20.</span></span> | <span data-ttu-id="da58d-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="da58d-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="da58d-123">詳細度</span><span class="sxs-lookup"><span data-stu-id="da58d-123">Verbosity</span></span> | <span data-ttu-id="da58d-124">出力に表示する詳細レベル。</span><span class="sxs-lookup"><span data-stu-id="da58d-124">The level of detail to display in the output.</span></span> <span data-ttu-id="da58d-125">既定値は通常 _の です_。</span><span class="sxs-lookup"><span data-stu-id="da58d-125">The default is _normal_.</span></span> <span data-ttu-id="da58d-126">(下記の注を参照してください)</span><span class="sxs-lookup"><span data-stu-id="da58d-126">(See the note below)</span></span>  | <span data-ttu-id="da58d-127">-Verbosity `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="da58d-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="da58d-128">Help</span><span class="sxs-lookup"><span data-stu-id="da58d-128">Help</span></span> | <span data-ttu-id="da58d-129">コマンドのヘルプ情報を表示します</span><span class="sxs-lookup"><span data-stu-id="da58d-129">Displays help information for the command</span></span> | <span data-ttu-id="da58d-130">-Help</span><span class="sxs-lookup"><span data-stu-id="da58d-130">-Help</span></span> |

<span data-ttu-id="da58d-131">「環境変数 [」も参照してください。](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="da58d-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="da58d-132">詳細レベル:</span><span class="sxs-lookup"><span data-stu-id="da58d-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="da58d-133">_quiet_ - パッケージ ID、バージョン</span><span class="sxs-lookup"><span data-stu-id="da58d-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="da58d-134">_normal_ - パッケージ ID、バージョン、ダウンロード、説明のプレビュー</span><span class="sxs-lookup"><span data-stu-id="da58d-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="da58d-135">_detailed_ - パッケージ ID、バージョン、ダウンロード、完全な説明、クエリ URL などのその他の情報</span><span class="sxs-lookup"><span data-stu-id="da58d-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="da58d-136">例</span><span class="sxs-lookup"><span data-stu-id="da58d-136">Examples</span></span>

<span data-ttu-id="da58d-137">既定のソース *から* ログに関連するパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="da58d-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="da58d-138">詳細な *詳細を* 含むログに関連するパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="da58d-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="da58d-139">ログに *関連する* パッケージを検索し、上位 5 件の結果のみを表示します。</span><span class="sxs-lookup"><span data-stu-id="da58d-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="da58d-140">指定した *ソース/* フィードから、プレリリース バージョンを含む JSON 関連のパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="da58d-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="da58d-141">複数の *ソース/* フィードから JSON 関連のパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="da58d-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
