---
title: NuGet CLI のヘルプコマンド
description: nuget.exe ヘルプコマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623111"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="cf0f2-103">help または ?</span><span class="sxs-lookup"><span data-stu-id="cf0f2-103">help or ?</span></span> <span data-ttu-id="cf0f2-104">コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cf0f2-104">command (NuGet CLI)</span></span>

<span data-ttu-id="cf0f2-105">**適用対象:** &bullet; **サポートされている**すべてのバージョン: すべて</span><span class="sxs-lookup"><span data-stu-id="cf0f2-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="cf0f2-106">特定のコマンドに関する一般的なヘルプ情報とヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="cf0f2-107">使用法</span><span class="sxs-lookup"><span data-stu-id="cf0f2-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="cf0f2-108">ここで [command] は、ヘルプを表示する特定のコマンドを識別します。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="cf0f2-109">一部のコマンドでは、 *help* `nuget help install` nuget.org に "help" という名前のパッケージが存在するので、最初にヘルプを指定することに注意してください。コマンドを指定した場合 `nuget install help` 、install コマンドのヘルプは表示されませんが、help という名前のパッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="cf0f2-110">Options</span><span class="sxs-lookup"><span data-stu-id="cf0f2-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="cf0f2-111">使用可能なすべてのコマンドの詳細なヘルプを印刷します。特定のコマンドが指定されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="cf0f2-112">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cf0f2-113">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="cf0f2-114">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="cf0f2-115">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="cf0f2-116">で使用する場合は、markdown 形式の詳細なヘルプを印刷 `-All` します。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="cf0f2-117">それ以外の場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="cf0f2-118">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="cf0f2-119">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="cf0f2-120">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="cf0f2-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cf0f2-121">使用例</span><span class="sxs-lookup"><span data-stu-id="cf0f2-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
