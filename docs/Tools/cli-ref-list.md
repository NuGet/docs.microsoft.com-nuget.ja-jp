---
title: NuGet CLI の一覧表示コマンド
description: Nuget.exe 一覧のコマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f4a44c70937e7cb49e472c53e9857e9f44d269f7
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="93aad-103">list コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="93aad-103">list command (NuGet CLI)</span></span>

<span data-ttu-id="93aad-104">**適用されます:** パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="93aad-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="93aad-105">指定されたソースからのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="93aad-105">Displays a list of packages from a given source.</span></span> <span data-ttu-id="93aad-106">すべてのソースが、グローバル構成ファイルで定義されているソースが指定されていない場合`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`、使用されます。</span><span class="sxs-lookup"><span data-stu-id="93aad-106">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config`, are used.</span></span> <span data-ttu-id="93aad-107">場合`NuGet.Config`し、ソースを指定しません`list`既定のフィード (nuget.org) を使用します。</span><span class="sxs-lookup"><span data-stu-id="93aad-107">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="93aad-108">使用法</span><span class="sxs-lookup"><span data-stu-id="93aad-108">Usage</span></span>

```cli
nuget list [search terms] [options]
```

<span data-ttu-id="93aad-109">ここで、省略可能な検索用語は、表示される一覧にフィルターされます。</span><span class="sxs-lookup"><span data-stu-id="93aad-109">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="93aad-110">検索語句は、nuget.org にそれらを使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前に適用されます。</span><span class="sxs-lookup"><span data-stu-id="93aad-110">Search terms are applied to the names of packages, tags, and package descriptions just as they are when using them on nuget.org.</span></span>

## <a name="options"></a><span data-ttu-id="93aad-111">オプション</span><span class="sxs-lookup"><span data-stu-id="93aad-111">Options</span></span>

| <span data-ttu-id="93aad-112">オプション</span><span class="sxs-lookup"><span data-stu-id="93aad-112">Option</span></span> | <span data-ttu-id="93aad-113">説明</span><span class="sxs-lookup"><span data-stu-id="93aad-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93aad-114">AllVersions</span><span class="sxs-lookup"><span data-stu-id="93aad-114">AllVersions</span></span> | <span data-ttu-id="93aad-115">パッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="93aad-115">List all versions of a package.</span></span> <span data-ttu-id="93aad-116">既定では、最新のバージョンのパッケージのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="93aad-116">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="93aad-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="93aad-117">ConfigFile</span></span> | <span data-ttu-id="93aad-118">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="93aad-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="93aad-119">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="93aad-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="93aad-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="93aad-120">ForceEnglishOutput</span></span> | <span data-ttu-id="93aad-121">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="93aad-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="93aad-122">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="93aad-122">Help</span></span> | <span data-ttu-id="93aad-123">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="93aad-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="93aad-124">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="93aad-124">IncludeDelisted</span></span> | <span data-ttu-id="93aad-125">*(3.2 +)* 一覧にないパッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="93aad-125">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="93aad-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="93aad-126">NonInteractive</span></span> | <span data-ttu-id="93aad-127">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="93aad-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="93aad-128">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="93aad-128">PreRelease</span></span> | <span data-ttu-id="93aad-129">一覧には、プレリリースのパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="93aad-129">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="93aad-130">ソース</span><span class="sxs-lookup"><span data-stu-id="93aad-130">Source</span></span> | <span data-ttu-id="93aad-131">検索するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="93aad-131">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="93aad-132">詳細度</span><span class="sxs-lookup"><span data-stu-id="93aad-132">Verbosity</span></span> | <span data-ttu-id="93aad-133">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="93aad-133">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="93aad-134">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="93aad-134">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="93aad-135">使用例</span><span class="sxs-lookup"><span data-stu-id="93aad-135">Examples</span></span>

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
