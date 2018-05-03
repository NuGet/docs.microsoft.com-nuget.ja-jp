---
title: NuGet CLI help コマンド
description: Nuget.exe help コマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="6dc66-103">役立ちますか?</span><span class="sxs-lookup"><span data-stu-id="6dc66-103">help or ?</span></span> <span data-ttu-id="6dc66-104">コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6dc66-104">command (NuGet CLI)</span></span>

<span data-ttu-id="6dc66-105">**適用されます:** すべて&bullet;**サポートされているバージョン**: すべて</span><span class="sxs-lookup"><span data-stu-id="6dc66-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="6dc66-106">ヘルプ情報と、特定のコマンドに関するヘルプ情報する一般的な表示にします。</span><span class="sxs-lookup"><span data-stu-id="6dc66-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="6dc66-107">使用法</span><span class="sxs-lookup"><span data-stu-id="6dc66-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="6dc66-108">ここで [コマンド] は、ヘルプを表示する対象の特定のコマンドを識別します。</span><span class="sxs-lookup"><span data-stu-id="6dc66-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="6dc66-109">いくつかのコマンドで指定を考慮する*ヘルプ*first、としての`nuget help install`nuget.org に"help"をという名前のパッケージがあるため、します。コマンドを付ける場合`nuget install help`、-install コマンドのヘルプを表示しませんが、ヘルプをという名前のパッケージを代わりにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="6dc66-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="6dc66-110">オプション</span><span class="sxs-lookup"><span data-stu-id="6dc66-110">Options</span></span>

| <span data-ttu-id="6dc66-111">オプション</span><span class="sxs-lookup"><span data-stu-id="6dc66-111">Option</span></span> | <span data-ttu-id="6dc66-112">説明</span><span class="sxs-lookup"><span data-stu-id="6dc66-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6dc66-113">すべて</span><span class="sxs-lookup"><span data-stu-id="6dc66-113">All</span></span> | <span data-ttu-id="6dc66-114">すべての利用可能なコマンドは詳細なヘルプを表示します。特定のコマンドを指定した場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="6dc66-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="6dc66-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6dc66-115">ConfigFile</span></span> | <span data-ttu-id="6dc66-116">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="6dc66-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6dc66-117">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="6dc66-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6dc66-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6dc66-118">ForceEnglishOutput</span></span> | <span data-ttu-id="6dc66-119">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="6dc66-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6dc66-120">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="6dc66-120">Help</span></span> | <span data-ttu-id="6dc66-121">ヘルプ コマンド自体の情報のヘルプを表示します。</span><span class="sxs-lookup"><span data-stu-id="6dc66-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="6dc66-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="6dc66-122">Markdown</span></span> | <span data-ttu-id="6dc66-123">マークダウン形式で使用する場合の詳細なヘルプを印刷`-All`です。</span><span class="sxs-lookup"><span data-stu-id="6dc66-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="6dc66-124">それ以外の場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="6dc66-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="6dc66-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6dc66-125">NonInteractive</span></span> | <span data-ttu-id="6dc66-126">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="6dc66-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6dc66-127">詳細度</span><span class="sxs-lookup"><span data-stu-id="6dc66-127">Verbosity</span></span> | <span data-ttu-id="6dc66-128">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="6dc66-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6dc66-129">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6dc66-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6dc66-130">使用例</span><span class="sxs-lookup"><span data-stu-id="6dc66-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
