---
title: NuGet CLI spec コマンド
description: Nuget.exe spec コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327569"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="d1e87-103">spec コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d1e87-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="d1e87-104">**適用対象:** パッケージ作成&bullet;で**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="d1e87-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d1e87-105">新しいパッケージ`.nuspec`のファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="d1e87-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="d1e87-106">プロジェクトファイルと同じフォルダー (`.csproj`、 `.vbproj`、 `.fsproj`) で実行すると、 `spec`はトークン`.nuspec`化されたファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="d1e87-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="d1e87-107">詳細については、「[パッケージの作成](../../create-packages/creating-a-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d1e87-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d1e87-108">使用法</span><span class="sxs-lookup"><span data-stu-id="d1e87-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="d1e87-109">ここ`<packageID>`で、は、 `.nuspec`ファイルに保存するオプションのパッケージ識別子です。</span><span class="sxs-lookup"><span data-stu-id="d1e87-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="d1e87-110">オプション</span><span class="sxs-lookup"><span data-stu-id="d1e87-110">Options</span></span>

| <span data-ttu-id="d1e87-111">オプション</span><span class="sxs-lookup"><span data-stu-id="d1e87-111">Option</span></span> | <span data-ttu-id="d1e87-112">説明</span><span class="sxs-lookup"><span data-stu-id="d1e87-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d1e87-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="d1e87-113">AssemblyPath</span></span> | <span data-ttu-id="d1e87-114">メタデータに使用するアセンブリへのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="d1e87-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="d1e87-115">必ず</span><span class="sxs-lookup"><span data-stu-id="d1e87-115">Force</span></span> | <span data-ttu-id="d1e87-116">既存`.nuspec`のファイルを上書きします。</span><span class="sxs-lookup"><span data-stu-id="d1e87-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="d1e87-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d1e87-117">ForceEnglishOutput</span></span> | <span data-ttu-id="d1e87-118">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="d1e87-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d1e87-119">Help</span><span class="sxs-lookup"><span data-stu-id="d1e87-119">Help</span></span> | <span data-ttu-id="d1e87-120">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d1e87-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="d1e87-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d1e87-121">NonInteractive</span></span> | <span data-ttu-id="d1e87-122">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="d1e87-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d1e87-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d1e87-123">Verbosity</span></span> | <span data-ttu-id="d1e87-124">出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="d1e87-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d1e87-125">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="d1e87-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d1e87-126">使用例</span><span class="sxs-lookup"><span data-stu-id="d1e87-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
