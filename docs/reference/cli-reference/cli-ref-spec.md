---
title: NuGet CLI spec コマンド
description: nuget.exe spec コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b7780ee5d2e722da5e1623f44709059dd9aa3d45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779144"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="cc4e3-103">spec コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cc4e3-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="cc4e3-104">**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="cc4e3-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="cc4e3-105">`.nuspec`新しいパッケージのファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="cc4e3-106">プロジェクトファイルと同じフォルダー (、、) で実行すると `.csproj` `.vbproj` 、はトークン化 `.fsproj` `spec` されたファイルを作成し `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="cc4e3-107">詳細については、「 [パッケージの作成](../../create-packages/creating-a-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="cc4e3-108">使用方法</span><span class="sxs-lookup"><span data-stu-id="cc4e3-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="cc4e3-109">ここ `<packageID>` で、は、ファイルに保存するオプションのパッケージ識別子です `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="cc4e3-110">Options</span><span class="sxs-lookup"><span data-stu-id="cc4e3-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="cc4e3-111">メタデータに使用するアセンブリへのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="cc4e3-112">既存の `.nuspec` ファイルを上書きします。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="cc4e3-113">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="cc4e3-114">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="cc4e3-115">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="cc4e3-116">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="cc4e3-117">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="cc4e3-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cc4e3-118">使用例</span><span class="sxs-lookup"><span data-stu-id="cc4e3-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
