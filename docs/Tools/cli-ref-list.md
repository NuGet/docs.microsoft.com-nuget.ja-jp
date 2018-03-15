---
title: "NuGet CLI リスト コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 一覧のコマンドのリファレンス"
keywords: "nuget の一覧の参照、パッケージの一覧表示コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7e0945b9e64a15a839f62bde0a0ef8f3d83335d4
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="17d6d-104">list コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="17d6d-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="17d6d-105">**適用されます:**パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="17d6d-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="17d6d-106">指定されたソースからのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="17d6d-107">すべてのソースが、グローバル構成ファイルで定義されているソースが指定されていない場合`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`、使用されます。</span><span class="sxs-lookup"><span data-stu-id="17d6d-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="17d6d-108">場合`NuGet.Config`し、ソースを指定しません`list`既定のフィード (nuget.org) を使用します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="17d6d-109">使用法</span><span class="sxs-lookup"><span data-stu-id="17d6d-109">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="17d6d-110">ここで、省略可能な検索用語は、表示される一覧にフィルターされます。</span><span class="sxs-lookup"><span data-stu-id="17d6d-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="17d6d-111">検索語句は、nuget.org にそれらを使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前に適用されます。</span><span class="sxs-lookup"><span data-stu-id="17d6d-111">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="17d6d-112">オプション</span><span class="sxs-lookup"><span data-stu-id="17d6d-112">Options</span></span>

| <span data-ttu-id="17d6d-113">オプション</span><span class="sxs-lookup"><span data-stu-id="17d6d-113">Option</span></span> | <span data-ttu-id="17d6d-114">説明</span><span class="sxs-lookup"><span data-stu-id="17d6d-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="17d6d-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="17d6d-115">AllVersions</span></span> | <span data-ttu-id="17d6d-116">パッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-116">List all versions of a package.</span></span> <span data-ttu-id="17d6d-117">既定では、最新のバージョンのパッケージのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="17d6d-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="17d6d-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="17d6d-118">ConfigFile</span></span> | <span data-ttu-id="17d6d-119">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="17d6d-120">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="17d6d-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="17d6d-121">ForceEnglishOutput</span></span> | <span data-ttu-id="17d6d-122">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="17d6d-123">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="17d6d-123">Help</span></span> | <span data-ttu-id="17d6d-124">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="17d6d-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="17d6d-125">IncludeDelisted</span></span> | <span data-ttu-id="17d6d-126">*(3.2 +)*一覧にないパッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="17d6d-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="17d6d-127">NonInteractive</span></span> | <span data-ttu-id="17d6d-128">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="17d6d-129">PreRelease</span><span class="sxs-lookup"><span data-stu-id="17d6d-129">PreRelease</span></span> | <span data-ttu-id="17d6d-130">一覧には、プレリリースのパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="17d6d-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="17d6d-131">ソース</span><span class="sxs-lookup"><span data-stu-id="17d6d-131">Source</span></span> | <span data-ttu-id="17d6d-132">検索するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="17d6d-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="17d6d-133">詳細度</span><span class="sxs-lookup"><span data-stu-id="17d6d-133">Verbosity</span></span> | <span data-ttu-id="17d6d-134">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="17d6d-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="17d6d-135">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="17d6d-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="17d6d-136">使用例</span><span class="sxs-lookup"><span data-stu-id="17d6d-136">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
