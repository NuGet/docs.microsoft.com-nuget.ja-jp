---
title: NuGet CLI init コマンド
description: Nuget.exe の init コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551411"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="3a1d0-103">init コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3a1d0-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="3a1d0-104">**適用対象:** パッケージの作成&bullet;**サポートされているバージョン:** 3.3 以降</span><span class="sxs-lookup"><span data-stu-id="3a1d0-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="3a1d0-105">説明に従って、階層構造を使用して目的のフォルダーにフラットなフォルダーからすべてのパッケージをコピー、[コマンドを追加](cli-ref-add.md)します。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="3a1d0-106">使用して、`init`を使用すると、`add`フォルダー内の各パッケージにコマンド。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="3a1d0-107">同様`add`、変換先がローカル フォルダーまたは UNC パスのいずれかにする必要がありますNuget.org やプライベート サーバーなどの HTTP パッケージ リポジトリがサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="3a1d0-108">使用法</span><span class="sxs-lookup"><span data-stu-id="3a1d0-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="3a1d0-109">場所`<source>`パッケージを含むフォルダーと`<destination>`ローカル フォルダーまたはパッケージのコピー先となる UNC パス名です。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="3a1d0-110">オプション</span><span class="sxs-lookup"><span data-stu-id="3a1d0-110">Options</span></span>

| <span data-ttu-id="3a1d0-111">オプション</span><span class="sxs-lookup"><span data-stu-id="3a1d0-111">Option</span></span> | <span data-ttu-id="3a1d0-112">説明</span><span class="sxs-lookup"><span data-stu-id="3a1d0-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3a1d0-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3a1d0-113">ConfigFile</span></span> | <span data-ttu-id="3a1d0-114">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3a1d0-115">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3a1d0-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3a1d0-116">ForceEnglishOutput</span></span> | <span data-ttu-id="3a1d0-117">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3a1d0-118">Expand</span><span class="sxs-lookup"><span data-stu-id="3a1d0-118">Expand</span></span> | <span data-ttu-id="3a1d0-119">パッケージのソースに追加される各パッケージ内のすべてのファイルを追加します。同じ`-Expand`で、`add`コマンド。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="3a1d0-120">Help</span><span class="sxs-lookup"><span data-stu-id="3a1d0-120">Help</span></span> | <span data-ttu-id="3a1d0-121">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="3a1d0-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3a1d0-122">NonInteractive</span></span> | <span data-ttu-id="3a1d0-123">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="3a1d0-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3a1d0-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="3a1d0-124">Verbosity</span></span> | <span data-ttu-id="3a1d0-125">出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="3a1d0-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3a1d0-126">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3a1d0-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3a1d0-127">使用例</span><span class="sxs-lookup"><span data-stu-id="3a1d0-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
