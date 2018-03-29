---
title: NuGet CLI init コマンド |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe init コマンドのリファレンス
keywords: nuget init 参照、init コマンド
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 01a3553622020b5868e33ece09cd7555cb712fd3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="f920e-104">init コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f920e-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="f920e-105">**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="f920e-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="f920e-106">説明に従って、階層構造を使用して目的のフォルダーにフラット フォルダーからすべてのパッケージをコピー、[コマンド追加](cli-ref-add.md)です。</span><span class="sxs-lookup"><span data-stu-id="f920e-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="f920e-107">使用して、`init`を使用すると、`add`フォルダー内の各パッケージにコマンド。</span><span class="sxs-lookup"><span data-stu-id="f920e-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="f920e-108">同様に`add`、変換先がローカル フォルダーまたは UNC パスのいずれかにする必要がありますNuget.org またはプライベート サーバーなどのパッケージ リポジトリの HTTP はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="f920e-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="f920e-109">使用法</span><span class="sxs-lookup"><span data-stu-id="f920e-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="f920e-110">ここで`<source>`パッケージを含むフォルダーと`<destination>`は、ローカル フォルダーまたは UNC のパス名が、パッケージのコピー先となります。</span><span class="sxs-lookup"><span data-stu-id="f920e-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="f920e-111">オプション</span><span class="sxs-lookup"><span data-stu-id="f920e-111">Options</span></span>

| <span data-ttu-id="f920e-112">オプション</span><span class="sxs-lookup"><span data-stu-id="f920e-112">Option</span></span> | <span data-ttu-id="f920e-113">説明</span><span class="sxs-lookup"><span data-stu-id="f920e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f920e-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f920e-114">ConfigFile</span></span> | <span data-ttu-id="f920e-115">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="f920e-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f920e-116">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="f920e-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f920e-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f920e-117">ForceEnglishOutput</span></span> | <span data-ttu-id="f920e-118">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="f920e-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f920e-119">Expand</span><span class="sxs-lookup"><span data-stu-id="f920e-119">Expand</span></span> | <span data-ttu-id="f920e-120">パッケージ ソースに追加される各パッケージ内のすべてのファイルを追加します。同じ`-Expand`で、`add`コマンド。</span><span class="sxs-lookup"><span data-stu-id="f920e-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="f920e-121">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="f920e-121">Help</span></span> | <span data-ttu-id="f920e-122">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="f920e-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="f920e-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f920e-123">NonInteractive</span></span> | <span data-ttu-id="f920e-124">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="f920e-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f920e-125">詳細度</span><span class="sxs-lookup"><span data-stu-id="f920e-125">Verbosity</span></span> | <span data-ttu-id="f920e-126">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="f920e-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f920e-127">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f920e-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f920e-128">使用例</span><span class="sxs-lookup"><span data-stu-id="f920e-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
