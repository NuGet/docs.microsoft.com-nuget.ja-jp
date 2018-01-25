---
title: "NuGet CLI init コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe init コマンドのリファレンス"
keywords: "nuget init 参照、init コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="862fe-104">init コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="862fe-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="862fe-105">**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="862fe-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="862fe-106">説明に従って、階層構造を使用して目的のフォルダーにフラット フォルダーからすべてのパッケージをコピー、[コマンド追加](cli-ref-add.md)です。</span><span class="sxs-lookup"><span data-stu-id="862fe-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="862fe-107">使用して、`init`を使用すると、`add`フォルダー内の各パッケージにコマンド。</span><span class="sxs-lookup"><span data-stu-id="862fe-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="862fe-108">同様に`add`、変換先がローカル フォルダーまたは UNC パスのいずれかにする必要がありますNuget.org またはプライベート サーバーなどのパッケージ リポジトリの HTTP はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="862fe-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="862fe-109">使用法</span><span class="sxs-lookup"><span data-stu-id="862fe-109">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="862fe-110">ここで`<source>`パッケージを含むフォルダーと`<destination>`は、ローカル フォルダーまたは UNC のパス名が、パッケージのコピー先となります。</span><span class="sxs-lookup"><span data-stu-id="862fe-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="862fe-111">オプション</span><span class="sxs-lookup"><span data-stu-id="862fe-111">Options</span></span>

| <span data-ttu-id="862fe-112">オプション</span><span class="sxs-lookup"><span data-stu-id="862fe-112">Option</span></span> | <span data-ttu-id="862fe-113">説明</span><span class="sxs-lookup"><span data-stu-id="862fe-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="862fe-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="862fe-114">ConfigFile</span></span> | <span data-ttu-id="862fe-115">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="862fe-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="862fe-116">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="862fe-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="862fe-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="862fe-117">ForceEnglishOutput</span></span> | <span data-ttu-id="862fe-118">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="862fe-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="862fe-119">Expand</span><span class="sxs-lookup"><span data-stu-id="862fe-119">Expand</span></span> | <span data-ttu-id="862fe-120">パッケージ ソースに追加される各パッケージ内のすべてのファイルを追加します。同じ`-Expand`で、`add`コマンド。</span><span class="sxs-lookup"><span data-stu-id="862fe-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="862fe-121">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="862fe-121">Help</span></span> | <span data-ttu-id="862fe-122">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="862fe-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="862fe-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="862fe-123">NonInteractive</span></span> | <span data-ttu-id="862fe-124">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="862fe-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="862fe-125">詳細度</span><span class="sxs-lookup"><span data-stu-id="862fe-125">Verbosity</span></span> | <span data-ttu-id="862fe-126">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="862fe-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="862fe-127">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="862fe-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="862fe-128">使用例</span><span class="sxs-lookup"><span data-stu-id="862fe-128">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
