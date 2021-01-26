---
title: NuGet CLI 検索コマンド
description: nuget.exe search コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779154"
---
# <a name="search-command-nuget-cli"></a><span data-ttu-id="db2ec-103">search コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="db2ec-103">search command (NuGet CLI)</span></span>

<span data-ttu-id="db2ec-104">**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 5.8 +</span><span class="sxs-lookup"><span data-stu-id="db2ec-104">**Applies to:** package consumption &bullet; **Supported versions:** 5.8+</span></span>

<span data-ttu-id="db2ec-105">指定されたクエリ文字列を使用して、指定されたソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="db2ec-105">Searches a given source using the query string provided.</span></span> <span data-ttu-id="db2ec-106">ソースが指定されていない場合は、% AppData% \NuGet\NuGet.config で定義されているすべてのソースが使用されます。</span><span class="sxs-lookup"><span data-stu-id="db2ec-106">If no sources are specified, all sources defined in %AppData%\NuGet\NuGet.config are used.</span></span>

## <a name="usage"></a><span data-ttu-id="db2ec-107">使用方法</span><span class="sxs-lookup"><span data-stu-id="db2ec-107">Usage</span></span>

```cli
nuget search [search terms] [options]
```

<span data-ttu-id="db2ec-108">ここでは、nuget.org で使用する場合と同じように、パッケージ、タグ、およびパッケージの説明の名前に検索語句が適用されます。</span><span class="sxs-lookup"><span data-stu-id="db2ec-108">where the search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="db2ec-109">オプション</span><span class="sxs-lookup"><span data-stu-id="db2ec-109">Options</span></span>

| <span data-ttu-id="db2ec-110">名前</span><span class="sxs-lookup"><span data-stu-id="db2ec-110">Name</span></span> | <span data-ttu-id="db2ec-111">説明</span><span class="sxs-lookup"><span data-stu-id="db2ec-111">Description</span></span> | <span data-ttu-id="db2ec-112">使用法</span><span class="sxs-lookup"><span data-stu-id="db2ec-112">Usage</span></span> |
| ---  |     ---     |  :-:  |
| <span data-ttu-id="db2ec-113">リリース</span><span class="sxs-lookup"><span data-stu-id="db2ec-113">PreRelease</span></span> | <span data-ttu-id="db2ec-114">プレリリースパッケージは既定では含まれていませんが、この引数を使用して含めることができます。</span><span class="sxs-lookup"><span data-stu-id="db2ec-114">Pre-release packages are not included by default, but can be included by using this argument</span></span> | <span data-ttu-id="db2ec-115">-プレリリース</span><span class="sxs-lookup"><span data-stu-id="db2ec-115">-PreRelease</span></span> |
| <span data-ttu-id="db2ec-116">source</span><span class="sxs-lookup"><span data-stu-id="db2ec-116">Source</span></span> | <span data-ttu-id="db2ec-117">__nuget.config__ の既定のソースに対してクエリを実行するのではなく、検索する特定のパッケージソース</span><span class="sxs-lookup"><span data-stu-id="db2ec-117">Specific package source(s) to search instead of querying the default sources in __nuget.config__</span></span> | <span data-ttu-id="db2ec-118">-ソース `<Source URL>`</span><span class="sxs-lookup"><span data-stu-id="db2ec-118">-Source `<Source URL>`</span></span>|
| <span data-ttu-id="db2ec-119">Take</span><span class="sxs-lookup"><span data-stu-id="db2ec-119">Take</span></span> | <span data-ttu-id="db2ec-120">返される結果の数。</span><span class="sxs-lookup"><span data-stu-id="db2ec-120">The number of results to return.</span></span> <span data-ttu-id="db2ec-121">既定値は 20 です。</span><span class="sxs-lookup"><span data-stu-id="db2ec-121">The default value is 20.</span></span> | <span data-ttu-id="db2ec-122">-Take `<positive integer>`</span><span class="sxs-lookup"><span data-stu-id="db2ec-122">-Take `<positive integer>`</span></span> |
| <span data-ttu-id="db2ec-123">詳細度</span><span class="sxs-lookup"><span data-stu-id="db2ec-123">Verbosity</span></span> | <span data-ttu-id="db2ec-124">出力に表示する詳細のレベル。</span><span class="sxs-lookup"><span data-stu-id="db2ec-124">The level of detail to display in the output.</span></span> <span data-ttu-id="db2ec-125">既定値は _normal_ です。</span><span class="sxs-lookup"><span data-stu-id="db2ec-125">The default is _normal_.</span></span> <span data-ttu-id="db2ec-126">(下のメモを参照してください)</span><span class="sxs-lookup"><span data-stu-id="db2ec-126">(See the note below)</span></span>  | <span data-ttu-id="db2ec-127">-詳細度 `<quiet|normal|detailed>`</span><span class="sxs-lookup"><span data-stu-id="db2ec-127">-Verbosity `<quiet|normal|detailed>`</span></span> |
| <span data-ttu-id="db2ec-128">Help</span><span class="sxs-lookup"><span data-stu-id="db2ec-128">Help</span></span> | <span data-ttu-id="db2ec-129">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="db2ec-129">Displays help information for the command</span></span> | <span data-ttu-id="db2ec-130">-ヘルプ</span><span class="sxs-lookup"><span data-stu-id="db2ec-130">-Help</span></span> |

<span data-ttu-id="db2ec-131">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="db2ec-131">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

> [!NOTE] 
> <span data-ttu-id="db2ec-132">詳細レベル:</span><span class="sxs-lookup"><span data-stu-id="db2ec-132">Verbosity Levels:</span></span>
> * <span data-ttu-id="db2ec-133">_quiet_ -パッケージ ID、バージョン</span><span class="sxs-lookup"><span data-stu-id="db2ec-133">_quiet_ - Package ID, Version</span></span>
> * <span data-ttu-id="db2ec-134">_通常_ -パッケージ ID、バージョン、ダウンロード、説明のプレビュー</span><span class="sxs-lookup"><span data-stu-id="db2ec-134">_normal_ - Package ID, Version, Downloads, Preview of Description</span></span>
> * <span data-ttu-id="db2ec-135">_詳細_ -パッケージ ID、バージョン、ダウンロード、完全な説明、クエリ URL などのその他の情報</span><span class="sxs-lookup"><span data-stu-id="db2ec-135">_detailed_ - Package ID, Version, Downloads, Full Description, Other information such as the query URL</span></span>

## <a name="examples"></a><span data-ttu-id="db2ec-136">例</span><span class="sxs-lookup"><span data-stu-id="db2ec-136">Examples</span></span>

<span data-ttu-id="db2ec-137">既定のソースから *ログ* 関連パッケージを検索する:</span><span class="sxs-lookup"><span data-stu-id="db2ec-137">Search for *logging*-related packages from default sources:</span></span>
```
nuget search logging
```
<span data-ttu-id="db2ec-138">詳細な詳細情報を含む *ログ* 関連パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="db2ec-138">Search for *logging*-related packages with detailed verbosity:</span></span>
```
nuget search logging -Verbosity detailed
```
<span data-ttu-id="db2ec-139">*ログ* 関連パッケージを検索し、上位5件の結果のみを表示します。</span><span class="sxs-lookup"><span data-stu-id="db2ec-139">Search for *logging*-related packages, and only show the top 5 results:</span></span>
```
nuget search logging -Take 5
```
<span data-ttu-id="db2ec-140">指定したソース/フィードから、プレリリースバージョンを含む *JSON* 関連パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="db2ec-140">Search for *JSON*-related packages, including pre-release versions, from specified source/feed:</span></span>
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
<span data-ttu-id="db2ec-141">複数のソース/フィードから *JSON* 関連のパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="db2ec-141">Search for *JSON*-related packages from multiple sources/feeds:</span></span>
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
