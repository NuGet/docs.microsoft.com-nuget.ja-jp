---
title: NuGet CLI のヘルプコマンド
description: Nuget.exe ヘルプコマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327799"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="35783-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="35783-103">help or ?</span></span> <span data-ttu-id="35783-104">コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="35783-104">command (NuGet CLI)</span></span>

<span data-ttu-id="35783-105">**適用対象:** &bullet; **サポートされている**すべてのバージョン: すべて</span><span class="sxs-lookup"><span data-stu-id="35783-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="35783-106">特定のコマンドに関する一般的なヘルプ情報とヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="35783-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="35783-107">使用法</span><span class="sxs-lookup"><span data-stu-id="35783-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="35783-108">ここで [command] は、ヘルプを表示する特定のコマンドを識別します。</span><span class="sxs-lookup"><span data-stu-id="35783-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="35783-109">一部のコマンドでは、nuget.org に "help" という`nuget help install`名前のパッケージが存在するので、最初にヘルプを指定することに注意してください。コマンド`nuget install help`を指定した場合、install コマンドのヘルプは表示されませんが、help という名前のパッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="35783-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="35783-110">オプション</span><span class="sxs-lookup"><span data-stu-id="35783-110">Options</span></span>

| <span data-ttu-id="35783-111">オプション</span><span class="sxs-lookup"><span data-stu-id="35783-111">Option</span></span> | <span data-ttu-id="35783-112">説明</span><span class="sxs-lookup"><span data-stu-id="35783-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="35783-113">All</span><span class="sxs-lookup"><span data-stu-id="35783-113">All</span></span> | <span data-ttu-id="35783-114">使用可能なすべてのコマンドの詳細なヘルプを印刷します。特定のコマンドが指定されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="35783-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="35783-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="35783-115">ConfigFile</span></span> | <span data-ttu-id="35783-116">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="35783-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="35783-117">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="35783-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="35783-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="35783-118">ForceEnglishOutput</span></span> | <span data-ttu-id="35783-119">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="35783-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="35783-120">Help</span><span class="sxs-lookup"><span data-stu-id="35783-120">Help</span></span> | <span data-ttu-id="35783-121">ヘルプコマンド自体のヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="35783-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="35783-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="35783-122">Markdown</span></span> | <span data-ttu-id="35783-123">で`-All`使用する場合は、markdown 形式の詳細なヘルプを印刷します。</span><span class="sxs-lookup"><span data-stu-id="35783-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="35783-124">それ以外の場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="35783-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="35783-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="35783-125">NonInteractive</span></span> | <span data-ttu-id="35783-126">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="35783-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="35783-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="35783-127">Verbosity</span></span> | <span data-ttu-id="35783-128">出力に表示される詳細データの量を指定します: *normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="35783-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="35783-129">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="35783-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="35783-130">使用例</span><span class="sxs-lookup"><span data-stu-id="35783-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
