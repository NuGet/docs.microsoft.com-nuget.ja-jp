---
title: NuGet CLI の一覧表示コマンド
description: Nuget.exe list コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549802"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="949f3-103">(NuGet CLI) の一覧表示コマンド</span><span class="sxs-lookup"><span data-stu-id="949f3-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="949f3-104">**適用対象:** パッケージの使用、公開&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="949f3-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="949f3-105">指定したソースからのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="949f3-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="949f3-106">すべてのソースが、グローバル構成ファイルで定義されているソースが指定されていない場合`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`、使用されます。</span><span class="sxs-lookup"><span data-stu-id="949f3-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="949f3-107">場合`NuGet.Config`し、ソースを指定しません`list`(nuget.org) の既定のフィードを使用します。</span><span class="sxs-lookup"><span data-stu-id="949f3-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="949f3-108">使用法</span><span class="sxs-lookup"><span data-stu-id="949f3-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="949f3-109">省略可能な検索語句は、表示される一覧にフィルターされます。</span><span class="sxs-lookup"><span data-stu-id="949f3-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="949f3-110">検索語句は、nuget.org でそれらを使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前に適用されます。</span><span class="sxs-lookup"><span data-stu-id="949f3-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="949f3-111">オプション</span><span class="sxs-lookup"><span data-stu-id="949f3-111">Options</span></span>

| <span data-ttu-id="949f3-112">オプション</span><span class="sxs-lookup"><span data-stu-id="949f3-112">Option</span></span> | <span data-ttu-id="949f3-113">説明</span><span class="sxs-lookup"><span data-stu-id="949f3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="949f3-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="949f3-114">AllVersions</span></span> | <span data-ttu-id="949f3-115">パッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="949f3-115">List all versions of a package.</span></span> <span data-ttu-id="949f3-116">既定では、最新のバージョンのパッケージのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="949f3-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="949f3-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="949f3-117">ConfigFile</span></span> | <span data-ttu-id="949f3-118">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="949f3-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="949f3-119">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="949f3-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="949f3-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="949f3-120">ForceEnglishOutput</span></span> | <span data-ttu-id="949f3-121">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="949f3-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="949f3-122">Help</span><span class="sxs-lookup"><span data-stu-id="949f3-122">Help</span></span> | <span data-ttu-id="949f3-123">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="949f3-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="949f3-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="949f3-124">IncludeDelisted</span></span> | <span data-ttu-id="949f3-125">*(3.2 以降)* 一覧から削除されたパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="949f3-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="949f3-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="949f3-126">NonInteractive</span></span> | <span data-ttu-id="949f3-127">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="949f3-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="949f3-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="949f3-128">PreRelease</span></span> | <span data-ttu-id="949f3-129">一覧には、プレリリース パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="949f3-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="949f3-130">Source</span><span class="sxs-lookup"><span data-stu-id="949f3-130">Source</span></span> | <span data-ttu-id="949f3-131">検索するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="949f3-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="949f3-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="949f3-132">Verbosity</span></span> | <span data-ttu-id="949f3-133">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="949f3-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="949f3-134">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="949f3-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="949f3-135">使用例</span><span class="sxs-lookup"><span data-stu-id="949f3-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
