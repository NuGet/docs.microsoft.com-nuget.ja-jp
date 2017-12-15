---
title: "NuGet CLI init コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d413e4f3-1b41-4a92-8df8-87d21b542bd3
description: "Nuget.exe init コマンドのリファレンス"
keywords: "nuget init 参照、init コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f63a3cbcca1aeff02995f23afd217c76e534b3be
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="ab724-104">init コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ab724-104">init command (NuGet CLI)</span></span>

<span data-ttu-id="ab724-105">**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="ab724-105">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="ab724-106">説明に従って、階層構造を使用して目的のフォルダーにフラット フォルダーからすべてのパッケージをコピー、[コマンド追加](#add)上。</span><span class="sxs-lookup"><span data-stu-id="ab724-106">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](#add) above.</span></span> <span data-ttu-id="ab724-107">使用して、`init`を使用すると、`add`フォルダー内の各パッケージにコマンド。</span><span class="sxs-lookup"><span data-stu-id="ab724-107">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="ab724-108">同様に`add`、変換先がローカル フォルダーまたは UNC パスのいずれかにする必要がありますNuget.org またはプライベート サーバーなどのパッケージ リポジトリの HTTP はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ab724-108">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="ab724-109">使用方法</span><span class="sxs-lookup"><span data-stu-id="ab724-109">Usage</span></span>

```
nuget init <source> <destination> [options]
```

<span data-ttu-id="ab724-110">ここで`<source>`パッケージを含むフォルダーと`<destination>`は、ローカル フォルダーまたは UNC のパス名が、パッケージのコピー先となります。</span><span class="sxs-lookup"><span data-stu-id="ab724-110">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages will be copied.</span></span>

## <a name="options"></a><span data-ttu-id="ab724-111">オプション</span><span class="sxs-lookup"><span data-stu-id="ab724-111">Options</span></span>

| <span data-ttu-id="ab724-112">オプション</span><span class="sxs-lookup"><span data-stu-id="ab724-112">Option</span></span> | <span data-ttu-id="ab724-113">説明</span><span class="sxs-lookup"><span data-stu-id="ab724-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ab724-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ab724-114">ConfigFile</span></span> | <span data-ttu-id="ab724-115">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="ab724-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ab724-116">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="ab724-116">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="ab724-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ab724-117">ForceEnglishOutput</span></span> | <span data-ttu-id="ab724-118">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="ab724-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ab724-119">Expand</span><span class="sxs-lookup"><span data-stu-id="ab724-119">Expand</span></span> | <span data-ttu-id="ab724-120">パッケージ ソースに追加される各パッケージ内のすべてのファイルを追加します。同じ`-Expand`で、`add`コマンド。</span><span class="sxs-lookup"><span data-stu-id="ab724-120">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="ab724-121">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="ab724-121">Help</span></span> | <span data-ttu-id="ab724-122">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="ab724-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="ab724-123">非対話型</span><span class="sxs-lookup"><span data-stu-id="ab724-123">NonInteractive</span></span> | <span data-ttu-id="ab724-124">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="ab724-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ab724-125">詳細度</span><span class="sxs-lookup"><span data-stu-id="ab724-125">Verbosity</span></span> | <span data-ttu-id="ab724-126">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="ab724-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="ab724-127">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ab724-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ab724-128">例</span><span class="sxs-lookup"><span data-stu-id="ab724-128">Examples</span></span>

```
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
