---
title: NuGet CLI の init コマンド
description: Nuget.exe init コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327779"
---
# <a name="init-command-nuget-cli"></a><span data-ttu-id="ef7a2-103">init コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ef7a2-103">init command (NuGet CLI)</span></span>

<span data-ttu-id="ef7a2-104">**適用対象:** パッケージ作成&bullet;で**サポートされているバージョン:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="ef7a2-104">**Applies to:** package creation &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="ef7a2-105">[[追加] コマンド](cli-ref-add.md)の説明に従って階層構造を使用して、フラットフォルダーのすべてのパッケージをコピー先フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-105">Copies all the packages from a flat folder to a destination folder using a hierarchical layout as described for the [add command](cli-ref-add.md).</span></span> <span data-ttu-id="ef7a2-106">つまり、を使用`init`することは、フォルダー `add`内の各パッケージに対してコマンドを使用することと同じです。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-106">That is, using `init` is equivalent to using the `add` command on each package in the folder.</span></span>

<span data-ttu-id="ef7a2-107">と`add`同様に、コピー先はローカルフォルダーまたは UNC パスである必要があります。Nuget.org やプライベートサーバーなどの HTTP パッケージリポジトリはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-107">As with `add`, the destination must be either a local folder or a UNC path; HTTP package repositories such as nuget.org or private servers are not supported.</span></span>

## <a name="usage"></a><span data-ttu-id="ef7a2-108">使用法</span><span class="sxs-lookup"><span data-stu-id="ef7a2-108">Usage</span></span>

```cli
nuget init <source> <destination> [options]
```

<span data-ttu-id="ef7a2-109">ここ`<source>`で、は`<destination>`パッケージを含むフォルダーで、はパッケージのコピー先のローカルフォルダーまたは UNC パス名です。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-109">where `<source>` is the folder containing packages and `<destination>` is the local folder or UNC pathname to which the packages are copied.</span></span>

## <a name="options"></a><span data-ttu-id="ef7a2-110">オプション</span><span class="sxs-lookup"><span data-stu-id="ef7a2-110">Options</span></span>

| <span data-ttu-id="ef7a2-111">オプション</span><span class="sxs-lookup"><span data-stu-id="ef7a2-111">Option</span></span> | <span data-ttu-id="ef7a2-112">説明</span><span class="sxs-lookup"><span data-stu-id="ef7a2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef7a2-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ef7a2-113">ConfigFile</span></span> | <span data-ttu-id="ef7a2-114">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ef7a2-115">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ef7a2-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ef7a2-116">ForceEnglishOutput</span></span> | <span data-ttu-id="ef7a2-117">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ef7a2-118">Expand</span><span class="sxs-lookup"><span data-stu-id="ef7a2-118">Expand</span></span> | <span data-ttu-id="ef7a2-119">パッケージソースに追加された各パッケージ内のすべてのファイルを追加します。`-Expand` コマンド`add`と同じです。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-119">Adds all files in each package that's added to the package source; same as `-Expand` with the `add` command.</span></span> |
| <span data-ttu-id="ef7a2-120">Help</span><span class="sxs-lookup"><span data-stu-id="ef7a2-120">Help</span></span> | <span data-ttu-id="ef7a2-121">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="ef7a2-122">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ef7a2-122">NonInteractive</span></span> | <span data-ttu-id="ef7a2-123">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ef7a2-124">Verbosity</span><span class="sxs-lookup"><span data-stu-id="ef7a2-124">Verbosity</span></span> | <span data-ttu-id="ef7a2-125">出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="ef7a2-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ef7a2-126">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="ef7a2-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ef7a2-127">使用例</span><span class="sxs-lookup"><span data-stu-id="ef7a2-127">Examples</span></span>

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
