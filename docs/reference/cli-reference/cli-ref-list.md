---
title: NuGet CLI リストコマンド
description: nuget.exe list コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d8e5c8574b44375e651f3ff1a4868681b3ce6d66
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699846"
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="bbe0c-103">list コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bbe0c-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="bbe0c-104">**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン** の発行: すべて</span><span class="sxs-lookup"><span data-stu-id="bbe0c-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="bbe0c-105">指定されたソースからのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="bbe0c-106">ソースが指定されていない場合は、グローバル構成ファイル (Windows) またはで定義されているすべてのソース `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="bbe0c-107">が `NuGet.Config` ソースを指定しない場合、は `list` 既定のフィード (nuget.org) を使用します。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="bbe0c-108">使用法</span><span class="sxs-lookup"><span data-stu-id="bbe0c-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="bbe0c-109">オプションの検索語句を使用すると、表示される一覧がフィルター処理されます。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="bbe0c-110">Nuget.org で使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前には[検索語句](../../consume-packages/finding-and-choosing-packages.md#search-syntax)が適用されます。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-110">[Search terms](../../consume-packages/finding-and-choosing-packages.md#search-syntax) are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span> 

## <a name="options"></a><span data-ttu-id="bbe0c-111">オプション</span><span class="sxs-lookup"><span data-stu-id="bbe0c-111">Options</span></span>

- **`-AllVersions`**

  <span data-ttu-id="bbe0c-112">パッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-112">List all versions of a package.</span></span> <span data-ttu-id="bbe0c-113">既定では、最新のパッケージバージョンのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-113">By default, only the latest package version is displayed.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="bbe0c-114">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bbe0c-115">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="bbe0c-116">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="bbe0c-117">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-117">Displays help information for the command.</span></span>

- **`-IncludeDelisted`**

  <span data-ttu-id="bbe0c-118">*(3.2 +)* 一覧にないパッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-118">*(3.2+)* Display unlisted packages.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="bbe0c-119">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-119">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="bbe0c-120">には、一覧にプレリリースパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-120">Includes prerelease packages in the list.</span></span>

- **`-Source`**

  <span data-ttu-id="bbe0c-121">検索するパッケージソース。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-121">The package source to search.</span></span> <span data-ttu-id="bbe0c-122">オプションを複数回使用して、複数のソースを指定でき `-Source` ます。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-122">You can specify multiple sources by using the `-Source` option multiple times.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="bbe0c-123">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="bbe0c-124">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="bbe0c-125">例</span><span class="sxs-lookup"><span data-stu-id="bbe0c-125">Examples</span></span>

<span data-ttu-id="bbe0c-126">構成されたフィードからすべてのパッケージを一覧表示する:</span><span class="sxs-lookup"><span data-stu-id="bbe0c-126">List all packages from configured feeds:</span></span>
```
nuget list
```
<span data-ttu-id="bbe0c-127">詳細な詳細度で Azure 関連パッケージを一覧表示する:</span><span class="sxs-lookup"><span data-stu-id="bbe0c-127">List Azure-related packages with detailed verbosity:</span></span>
```
nuget list Azure -Verbosity detailed
```
<span data-ttu-id="bbe0c-128">構成済みのフィードから Azure 関連のパッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-128">List all versions of Azure-related packages from configured feeds:</span></span>
```
nuget list Azure -AllVersions
```
<span data-ttu-id="bbe0c-129">指定したソース/フィードから、JSON 関連のパッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="bbe0c-129">List all versions of JSON-related packages from specified source/feed:</span></span>
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
<span data-ttu-id="bbe0c-130">複数のソース/フィードから JSON 関連のパッケージを一覧表示する:</span><span class="sxs-lookup"><span data-stu-id="bbe0c-130">List JSON-related packages from multiple sources/feeds:</span></span>
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
