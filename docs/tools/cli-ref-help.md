---
title: NuGet CLI ヘルプ コマンド
description: Nuget.exe の help コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546564"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="99662-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="99662-103">help or ?</span></span> <span data-ttu-id="99662-104">コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="99662-104">command (NuGet CLI)</span></span>

<span data-ttu-id="99662-105">**適用対象:** すべて&bullet;**サポートされているバージョン**: すべて</span><span class="sxs-lookup"><span data-stu-id="99662-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="99662-106">表示の [全般] では、ヘルプ情報と、特定のコマンドに関するヘルプ情報。</span><span class="sxs-lookup"><span data-stu-id="99662-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="99662-107">使用法</span><span class="sxs-lookup"><span data-stu-id="99662-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="99662-108">[コマンド] で、ヘルプを表示する特定のコマンドを識別する場所。</span><span class="sxs-lookup"><span data-stu-id="99662-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="99662-109">いくつかのコマンドを使用するを指定することに注意してください*ヘルプ*でとして初めて、 `nuget help install`nuget.org で「ヘルプ」をという名前のパッケージがあるためです。コマンドを指定する場合`nuget install help`、インストール コマンドのヘルプを表示しませんが、代わりにはヘルプをという名前のパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="99662-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="99662-110">オプション</span><span class="sxs-lookup"><span data-stu-id="99662-110">Options</span></span>

| <span data-ttu-id="99662-111">オプション</span><span class="sxs-lookup"><span data-stu-id="99662-111">Option</span></span> | <span data-ttu-id="99662-112">説明</span><span class="sxs-lookup"><span data-stu-id="99662-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="99662-113">All</span><span class="sxs-lookup"><span data-stu-id="99662-113">All</span></span> | <span data-ttu-id="99662-114">すべての利用可能なコマンドは詳細なヘルプを印刷します。特定のコマンドを指定した場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="99662-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="99662-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="99662-115">ConfigFile</span></span> | <span data-ttu-id="99662-116">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="99662-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="99662-117">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="99662-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="99662-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="99662-118">ForceEnglishOutput</span></span> | <span data-ttu-id="99662-119">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="99662-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="99662-120">Help</span><span class="sxs-lookup"><span data-stu-id="99662-120">Help</span></span> | <span data-ttu-id="99662-121">ヘルプ、ヘルプ コマンド自体の情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="99662-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="99662-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="99662-122">Markdown</span></span> | <span data-ttu-id="99662-123">Markdown 形式で使用する場合に詳細なヘルプを印刷`-All`します。</span><span class="sxs-lookup"><span data-stu-id="99662-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="99662-124">それ以外の場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="99662-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="99662-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="99662-125">NonInteractive</span></span> | <span data-ttu-id="99662-126">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="99662-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="99662-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="99662-127">Verbosity</span></span> | <span data-ttu-id="99662-128">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="99662-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="99662-129">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="99662-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="99662-130">使用例</span><span class="sxs-lookup"><span data-stu-id="99662-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
