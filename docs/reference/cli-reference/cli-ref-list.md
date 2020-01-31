---
title: NuGet CLI の list コマンド
description: Nuget.exe list コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813339"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="d1137-103">list コマンド(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d1137-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="d1137-104">**適用対象:** パッケージの使用、発行 &bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="d1137-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d1137-105">指定されたソースからのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="d1137-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="d1137-106">ソースが指定されていない場合は、グローバル構成 `%AppData%\NuGet\NuGet.Config` ファイル (Windows) または `~/.nuget/NuGet/NuGet.Config`で定義されているすべてのソースが使用されます。</span><span class="sxs-lookup"><span data-stu-id="d1137-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="d1137-107">`NuGet.Config` がソースを指定しない場合、`list` は既定のフィード (nuget.org) を使用します。</span><span class="sxs-lookup"><span data-stu-id="d1137-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="d1137-108">使用状況</span><span class="sxs-lookup"><span data-stu-id="d1137-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="d1137-109">オプションの検索語句を使用すると、表示される一覧がフィルター処理されます。</span><span class="sxs-lookup"><span data-stu-id="d1137-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="d1137-110">Nuget.org で使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前には検索語句が適用されます。</span><span class="sxs-lookup"><span data-stu-id="d1137-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="d1137-111">[オプション]</span><span class="sxs-lookup"><span data-stu-id="d1137-111">Options</span></span>

| <span data-ttu-id="d1137-112">オプション</span><span class="sxs-lookup"><span data-stu-id="d1137-112">Option</span></span> | <span data-ttu-id="d1137-113">説明</span><span class="sxs-lookup"><span data-stu-id="d1137-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1137-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="d1137-114">AllVersions</span></span> | <span data-ttu-id="d1137-115">パッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="d1137-115">List all versions of a package.</span></span> <span data-ttu-id="d1137-116">既定では、最新のパッケージバージョンのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="d1137-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="d1137-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d1137-117">ConfigFile</span></span> | <span data-ttu-id="d1137-118">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="d1137-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d1137-119">指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="d1137-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d1137-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d1137-120">ForceEnglishOutput</span></span> | <span data-ttu-id="d1137-121">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="d1137-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d1137-122">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="d1137-122">Help</span></span> | <span data-ttu-id="d1137-123">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d1137-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="d1137-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="d1137-124">IncludeDelisted</span></span> | <span data-ttu-id="d1137-125">*(3.2 +)* 一覧にないパッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="d1137-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="d1137-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d1137-126">NonInteractive</span></span> | <span data-ttu-id="d1137-127">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="d1137-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d1137-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="d1137-128">PreRelease</span></span> | <span data-ttu-id="d1137-129">には、一覧にプレリリースパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d1137-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="d1137-130">Source</span><span class="sxs-lookup"><span data-stu-id="d1137-130">Source</span></span> | <span data-ttu-id="d1137-131">検索するパッケージソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="d1137-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="d1137-132">詳細度</span><span class="sxs-lookup"><span data-stu-id="d1137-132">Verbosity</span></span> | <span data-ttu-id="d1137-133">出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="d1137-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d1137-134">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="d1137-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d1137-135">使用例</span><span class="sxs-lookup"><span data-stu-id="d1137-135">Examples</span></span>

<span data-ttu-id="d1137-136">構成されたフィードからすべてのパッケージを一覧表示する:</span><span class="sxs-lookup"><span data-stu-id="d1137-136">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="d1137-137">詳細な詳細度で Azure 関連パッケージを一覧表示する:</span><span class="sxs-lookup"><span data-stu-id="d1137-137">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="d1137-138">構成済みのフィードから Azure 関連のパッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="d1137-138">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="d1137-139">指定したソース/フィードから、JSON 関連のパッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="d1137-139">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="d1137-140">複数のソース/フィードから JSON 関連のパッケージを一覧表示する:</span><span class="sxs-lookup"><span data-stu-id="d1137-140">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

