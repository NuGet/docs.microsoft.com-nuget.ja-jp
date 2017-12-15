---
title: "NuGet CLI リスト コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 728c8452-0457-4bb8-bfdc-de77fe1570bd
description: "Nuget.exe 一覧のコマンドのリファレンス"
keywords: "nuget の一覧の参照、パッケージの一覧表示コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 62a7077e7adac1e4d8cf305fd6e66a6ce5ebfb76
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="list-command-nuget-cli"></a><span data-ttu-id="b8417-104">list コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b8417-104">list command (NuGet CLI)</span></span>

<span data-ttu-id="b8417-105">**適用されます:**パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="b8417-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b8417-106">指定されたソースからのパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="b8417-106">Displays a list of packages from a given source.</span></span> <span data-ttu-id="b8417-107">すべてのソースが、グローバル構成ファイルで定義されているソースが指定されていない場合`%AppData%\NuGet\NuGet.Config`、使用されます。</span><span class="sxs-lookup"><span data-stu-id="b8417-107">If no sources are specified, all sources defined in the global configuration file, `%AppData%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="b8417-108">場合`NuGet.Config`し、ソースを指定しません`list`既定のフィード (nuget.org) を使用します。</span><span class="sxs-lookup"><span data-stu-id="b8417-108">If `NuGet.Config` specifies no sources, then `list` uses the default feed (nuget.org).</span></span>

## <a name="usage"></a><span data-ttu-id="b8417-109">使用方法</span><span class="sxs-lookup"><span data-stu-id="b8417-109">Usage</span></span>

```
nuget list [search terms] [options]
```

<span data-ttu-id="b8417-110">ここで、省略可能な検索用語は、表示される一覧にフィルターされます。</span><span class="sxs-lookup"><span data-stu-id="b8417-110">where the optional search terms will filter the displayed list.</span></span> <span data-ttu-id="b8417-111">検索語句は、パッケージ、タグ、およびパッケージの説明の名前に適用されます。</span><span class="sxs-lookup"><span data-stu-id="b8417-111">Search terms are applied to the names of packages, tags, and package descriptions.</span></span>

## <a name="options"></a><span data-ttu-id="b8417-112">オプション</span><span class="sxs-lookup"><span data-stu-id="b8417-112">Options</span></span>
| <span data-ttu-id="b8417-113">オプション</span><span class="sxs-lookup"><span data-stu-id="b8417-113">Option</span></span> | <span data-ttu-id="b8417-114">説明</span><span class="sxs-lookup"><span data-stu-id="b8417-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b8417-115">AllVersions</span><span class="sxs-lookup"><span data-stu-id="b8417-115">AllVersions</span></span> | <span data-ttu-id="b8417-116">パッケージのすべてのバージョンを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b8417-116">List all versions of a package.</span></span> <span data-ttu-id="b8417-117">既定では、最新のバージョンのパッケージのみが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b8417-117">By default, only the latest package version is displayed.</span></span> |
| <span data-ttu-id="b8417-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b8417-118">ConfigFile</span></span> | <span data-ttu-id="b8417-119">*(2.5 +)* NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="b8417-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="b8417-120">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="b8417-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="b8417-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b8417-121">ForceEnglishOutput</span></span> | <span data-ttu-id="b8417-122">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="b8417-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b8417-123">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="b8417-123">Help</span></span> | <span data-ttu-id="b8417-124">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="b8417-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="b8417-125">IncludeDelisted</span><span class="sxs-lookup"><span data-stu-id="b8417-125">IncludeDelisted</span></span> | <span data-ttu-id="b8417-126">*(3.2 +)*一覧にないパッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="b8417-126">*(3.2+)* Display unlisted packages.</span></span> |
| <span data-ttu-id="b8417-127">非対話型</span><span class="sxs-lookup"><span data-stu-id="b8417-127">NonInteractive</span></span> | <span data-ttu-id="b8417-128">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="b8417-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b8417-129">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="b8417-129">PreRelease</span></span> | <span data-ttu-id="b8417-130">一覧には、プレリリースのパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b8417-130">Includes prerelease packages in the list.</span></span> |
| <span data-ttu-id="b8417-131">ソース</span><span class="sxs-lookup"><span data-stu-id="b8417-131">Source</span></span> | <span data-ttu-id="b8417-132">検索するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="b8417-132">Specifies a list of packages sources to search.</span></span> |
| <span data-ttu-id="b8417-133">詳細度</span><span class="sxs-lookup"><span data-stu-id="b8417-133">Verbosity</span></span> | <span data-ttu-id="b8417-134">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="b8417-134">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="b8417-135">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b8417-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b8417-136">例</span><span class="sxs-lookup"><span data-stu-id="b8417-136">Examples</span></span>

```
nuget list

nuget list -Verbosity detailed -AllVersions
```
