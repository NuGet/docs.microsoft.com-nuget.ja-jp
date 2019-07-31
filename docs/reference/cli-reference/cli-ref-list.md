---
title: NuGet CLI リストコマンド
description: Nuget.exe list コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327739"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="139b7-103">list コマンド(NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="139b7-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="139b7-104">**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン**の発行: すべて</span><span class="sxs-lookup"><span data-stu-id="139b7-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="139b7-105">指定されたソースからのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="139b7-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="139b7-106">ソースが指定されていない場合は、グローバル構成ファイル`%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`で定義されているすべてのソースが使用されます。</span><span class="sxs-lookup"><span data-stu-id="139b7-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="139b7-107">が`NuGet.Config`ソースを指定しない`list`場合、は既定のフィード (nuget.org) を使用します。</span><span class="sxs-lookup"><span data-stu-id="139b7-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="139b7-108">使用法</span><span class="sxs-lookup"><span data-stu-id="139b7-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="139b7-109">オプションの検索語句を使用すると、表示される一覧がフィルター処理されます。</span><span class="sxs-lookup"><span data-stu-id="139b7-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="139b7-110">Nuget.org で使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前には検索語句が適用されます。</span><span class="sxs-lookup"><span data-stu-id="139b7-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="139b7-111">オプション</span><span class="sxs-lookup"><span data-stu-id="139b7-111">Options</span></span>

| <span data-ttu-id="139b7-112">オプション</span><span class="sxs-lookup"><span data-stu-id="139b7-112">Option</span></span> | <span data-ttu-id="139b7-113">説明</span><span class="sxs-lookup"><span data-stu-id="139b7-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="139b7-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="139b7-114">AllVersions</span></span> | <span data-ttu-id="139b7-115">パッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="139b7-115">List all versions of a package.</span></span> <span data-ttu-id="139b7-116">既定では、最新のパッケージバージョンのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="139b7-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="139b7-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="139b7-117">ConfigFile</span></span> | <span data-ttu-id="139b7-118">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="139b7-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="139b7-119">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="139b7-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="139b7-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="139b7-120">ForceEnglishOutput</span></span> | <span data-ttu-id="139b7-121">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="139b7-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="139b7-122">Help</span><span class="sxs-lookup"><span data-stu-id="139b7-122">Help</span></span> | <span data-ttu-id="139b7-123">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="139b7-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="139b7-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="139b7-124">IncludeDelisted</span></span> | <span data-ttu-id="139b7-125">*(3.2 +)* 一覧にないパッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="139b7-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="139b7-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="139b7-126">NonInteractive</span></span> | <span data-ttu-id="139b7-127">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="139b7-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="139b7-128">PreRelease</span><span class="sxs-lookup"><span data-stu-id="139b7-128">PreRelease</span></span> | <span data-ttu-id="139b7-129">には、一覧にプレリリースパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="139b7-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="139b7-130">Source</span><span class="sxs-lookup"><span data-stu-id="139b7-130">Source</span></span> | <span data-ttu-id="139b7-131">検索するパッケージソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="139b7-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="139b7-132">Verbosity</span><span class="sxs-lookup"><span data-stu-id="139b7-132">Verbosity</span></span> | <span data-ttu-id="139b7-133">出力に表示される詳細データの量を指定します: *normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="139b7-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="139b7-134">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="139b7-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="139b7-135">使用例</span><span class="sxs-lookup"><span data-stu-id="139b7-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
