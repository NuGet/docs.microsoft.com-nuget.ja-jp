---
title: NuGet CLI init コマンド
description: Nuget.exe init コマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f5e819d014637d1ebb0403d9d838f9362efb20f0
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="515bb-103">init コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="515bb-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="515bb-104">**適用されます:** パッケージの作成&bullet;**サポートされているバージョン:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="515bb-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="515bb-105">説明に従って、階層構造を使用して目的のフォルダーにフラット フォルダーからすべてのパッケージをコピー、[コマンド追加](cli-ref-add.md)です。</span><span class="sxs-lookup"><span data-stu-id="515bb-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="515bb-106">使用して、`init`を使用すると、`add`フォルダー内の各パッケージにコマンド。</span><span class="sxs-lookup"><span data-stu-id="515bb-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="515bb-107">同様に`add`、変換先がローカル フォルダーまたは UNC パスのいずれかにする必要がありますNuget.org またはプライベート サーバーなどのパッケージ リポジトリの HTTP はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="515bb-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="515bb-108">使用法</span><span class="sxs-lookup"><span data-stu-id="515bb-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="515bb-109">ここで`<source>`パッケージを含むフォルダーと`<destination>`は、ローカル フォルダーまたは UNC のパス名が、パッケージのコピー先となります。</span><span class="sxs-lookup"><span data-stu-id="515bb-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="515bb-110">オプション</span><span class="sxs-lookup"><span data-stu-id="515bb-110">Options</span></span>

| <span data-ttu-id="515bb-111">オプション</span><span class="sxs-lookup"><span data-stu-id="515bb-111">Option</span></span> | <span data-ttu-id="515bb-112">説明</span><span class="sxs-lookup"><span data-stu-id="515bb-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="515bb-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="515bb-113">ConfigFile</span></span> | <span data-ttu-id="515bb-114">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="515bb-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="515bb-115">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="515bb-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="515bb-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="515bb-116">ForceEnglishOutput</span></span> | <span data-ttu-id="515bb-117">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="515bb-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="515bb-118">Expand</span><span class="sxs-lookup"><span data-stu-id="515bb-118">Expand</span></span> | <span data-ttu-id="515bb-119">パッケージ ソースに追加される各パッケージ内のすべてのファイルを追加します。同じ`-Expand`で、`add`コマンド。</span><span class="sxs-lookup"><span data-stu-id="515bb-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="515bb-120">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="515bb-120">Help</span></span> | <span data-ttu-id="515bb-121">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="515bb-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="515bb-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="515bb-122">NonInteractive</span></span> | <span data-ttu-id="515bb-123">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="515bb-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="515bb-124">詳細度</span><span class="sxs-lookup"><span data-stu-id="515bb-124">Verbosity</span></span> | <span data-ttu-id="515bb-125">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="515bb-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="515bb-126">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="515bb-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="515bb-127">使用例</span><span class="sxs-lookup"><span data-stu-id="515bb-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
