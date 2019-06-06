---
title: NuGet CLI 仕様コマンド
description: Nuget.exe spec コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546450"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="a96b3-103">spec コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a96b3-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="a96b3-104">**適用対象:** パッケージの作成&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="a96b3-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a96b3-105">生成、`.nuspec`新しいパッケージのファイル。</span><span class="sxs-lookup"><span data-stu-id="a96b3-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="a96b3-106">プロジェクト ファイルと同じフォルダーで実行された場合 (`.csproj`、 `.vbproj`、 `.fsproj`)、`spec`をトークン化された作成`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="a96b3-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="a96b3-107">詳細については、[パッケージを作成する](../create-packages/creating-a-package.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a96b3-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a96b3-108">使用法</span><span class="sxs-lookup"><span data-stu-id="a96b3-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="a96b3-109">場所`<packageID>`で保存するオプションのパッケージ識別子、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="a96b3-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="a96b3-110">オプション</span><span class="sxs-lookup"><span data-stu-id="a96b3-110">Options</span></span>

| <span data-ttu-id="a96b3-111">オプション</span><span class="sxs-lookup"><span data-stu-id="a96b3-111">Option</span></span> | <span data-ttu-id="a96b3-112">説明</span><span class="sxs-lookup"><span data-stu-id="a96b3-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a96b3-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="a96b3-113">AssemblyPath</span></span> | <span data-ttu-id="a96b3-114">メタデータに使用するアセンブリへのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="a96b3-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="a96b3-115">Force</span><span class="sxs-lookup"><span data-stu-id="a96b3-115">Force</span></span> | <span data-ttu-id="a96b3-116">既存のすべての上書き`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="a96b3-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="a96b3-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a96b3-117">ForceEnglishOutput</span></span> | <span data-ttu-id="a96b3-118">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="a96b3-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a96b3-119">Help</span><span class="sxs-lookup"><span data-stu-id="a96b3-119">Help</span></span> | <span data-ttu-id="a96b3-120">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="a96b3-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="a96b3-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a96b3-121">NonInteractive</span></span> | <span data-ttu-id="a96b3-122">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="a96b3-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a96b3-123">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a96b3-123">Verbosity</span></span> | <span data-ttu-id="a96b3-124">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="a96b3-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a96b3-125">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a96b3-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a96b3-126">使用例</span><span class="sxs-lookup"><span data-stu-id="a96b3-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
