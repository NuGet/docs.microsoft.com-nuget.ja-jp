---
title: NuGet CLI spec コマンド
description: nuget.exe spec コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622565"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="8c7ec-103">spec コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8c7ec-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="8c7ec-104">**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="8c7ec-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8c7ec-105">`.nuspec`新しいパッケージのファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="8c7ec-106">プロジェクトファイルと同じフォルダー (、、) で実行すると `.csproj` `.vbproj` 、はトークン化 `.fsproj` `spec` されたファイルを作成し `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="8c7ec-107">詳細については、「 [パッケージの作成](../../create-packages/creating-a-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-107">For additional information, see [Creating a Package](../../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8c7ec-108">使用法</span><span class="sxs-lookup"><span data-stu-id="8c7ec-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="8c7ec-109">ここ `<packageID>` で、は、ファイルに保存するオプションのパッケージ識別子です `.nuspec` 。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="8c7ec-110">Options</span><span class="sxs-lookup"><span data-stu-id="8c7ec-110">Options</span></span>

- **`-AssemblyPath`**

  <span data-ttu-id="8c7ec-111">メタデータに使用するアセンブリへのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-111">Specifies the path to the assembly to use for metadata.</span></span>

- **`-Force`**

  <span data-ttu-id="8c7ec-112">既存の `.nuspec` ファイルを上書きします。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-112">Overwrites any existing `.nuspec` file.</span></span>


- **`-ForceEnglishOutput`**

  <span data-ttu-id="8c7ec-113">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-113">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="8c7ec-114">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-114">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="8c7ec-115">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-115">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="8c7ec-116">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-116">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="8c7ec-117">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="8c7ec-117">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8c7ec-118">使用例</span><span class="sxs-lookup"><span data-stu-id="8c7ec-118">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
