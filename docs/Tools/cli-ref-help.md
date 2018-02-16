---
title: "NuGet CLI help コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe help コマンドのリファレンス"
keywords: "nuget ヘルプ リファレンス、コマンドのヘルプします。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b4255c353e412cf1d1a59590ee816b7887c90653
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="a0002-104">役立ちますか?</span><span class="sxs-lookup"><span data-stu-id="a0002-104">help or ?</span></span> <span data-ttu-id="a0002-105">コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a0002-105">command (NuGet CLI)</span></span>

<span data-ttu-id="a0002-106">**適用されます:**すべて&bullet;**サポートされているバージョン**: すべて</span><span class="sxs-lookup"><span data-stu-id="a0002-106">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="a0002-107">ヘルプ情報と、特定のコマンドに関するヘルプ情報する一般的な表示にします。</span><span class="sxs-lookup"><span data-stu-id="a0002-107">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="a0002-108">使用法</span><span class="sxs-lookup"><span data-stu-id="a0002-108">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="a0002-109">ここで [コマンド] は、ヘルプを表示する対象の特定のコマンドを識別します。</span><span class="sxs-lookup"><span data-stu-id="a0002-109">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="a0002-110">いくつかのコマンドで指定を考慮する*ヘルプ*first、としての`nuget help install`nuget.org に"help"をという名前のパッケージがあるため、します。コマンドを付ける場合`nuget install help`、-install コマンドのヘルプを表示しませんが、ヘルプをという名前のパッケージを代わりにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a0002-110">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="a0002-111">オプション</span><span class="sxs-lookup"><span data-stu-id="a0002-111">Options</span></span>

| <span data-ttu-id="a0002-112">オプション</span><span class="sxs-lookup"><span data-stu-id="a0002-112">Option</span></span> | <span data-ttu-id="a0002-113">説明</span><span class="sxs-lookup"><span data-stu-id="a0002-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a0002-114">すべて</span><span class="sxs-lookup"><span data-stu-id="a0002-114">All</span></span> | <span data-ttu-id="a0002-115">すべての利用可能なコマンドは詳細なヘルプを表示します。特定のコマンドを指定した場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="a0002-115">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="a0002-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a0002-116">ConfigFile</span></span> | <span data-ttu-id="a0002-117">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="a0002-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a0002-118">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="a0002-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="a0002-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a0002-119">ForceEnglishOutput</span></span> | <span data-ttu-id="a0002-120">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="a0002-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a0002-121">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="a0002-121">Help</span></span> | <span data-ttu-id="a0002-122">ヘルプ コマンド自体の情報のヘルプを表示します。</span><span class="sxs-lookup"><span data-stu-id="a0002-122">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="a0002-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="a0002-123">Markdown</span></span> | <span data-ttu-id="a0002-124">マークダウン形式で使用する場合の詳細なヘルプを印刷`-All`です。</span><span class="sxs-lookup"><span data-stu-id="a0002-124">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="a0002-125">それ以外の場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="a0002-125">Ignored otherwise.</span></span> |
| <span data-ttu-id="a0002-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a0002-126">NonInteractive</span></span> | <span data-ttu-id="a0002-127">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="a0002-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a0002-128">詳細度</span><span class="sxs-lookup"><span data-stu-id="a0002-128">Verbosity</span></span> | <span data-ttu-id="a0002-129">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="a0002-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a0002-130">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a0002-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a0002-131">使用例</span><span class="sxs-lookup"><span data-stu-id="a0002-131">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
