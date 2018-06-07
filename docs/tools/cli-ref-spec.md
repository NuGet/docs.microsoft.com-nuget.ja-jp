---
title: NuGet CLI 仕様コマンド
description: Nuget.exe spec コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817087"
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="8e0c7-103">spec コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8e0c7-103">spec command (NuGet CLI)</span></span>

<span data-ttu-id="8e0c7-104">**適用されます:** パッケージの作成&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="8e0c7-104">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="8e0c7-105">生成、`.nuspec`新しいパッケージのファイルです。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-105">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="8e0c7-106">プロジェクト ファイルと同じフォルダーで実行された場合 (`.csproj`、 `.vbproj`、 `.fsproj`)、 `spec` 、トークン化された作成`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-106">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="8e0c7-107">詳細については、次を参照してください。[パッケージを作成する](../create-packages/creating-a-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-107">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="8e0c7-108">使用法</span><span class="sxs-lookup"><span data-stu-id="8e0c7-108">Usage</span></span>

```cli
nuget spec [<packageID>] [options]
```

<span data-ttu-id="8e0c7-109">ここで`<packageID>`で保存する省略可能なパッケージ識別子、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-109">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="8e0c7-110">オプション</span><span class="sxs-lookup"><span data-stu-id="8e0c7-110">Options</span></span>

| <span data-ttu-id="8e0c7-111">オプション</span><span class="sxs-lookup"><span data-stu-id="8e0c7-111">Option</span></span> | <span data-ttu-id="8e0c7-112">説明</span><span class="sxs-lookup"><span data-stu-id="8e0c7-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8e0c7-113">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="8e0c7-113">AssemblyPath</span></span> | <span data-ttu-id="8e0c7-114">メタデータに使用するアセンブリへのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-114">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="8e0c7-115">Force</span><span class="sxs-lookup"><span data-stu-id="8e0c7-115">Force</span></span> | <span data-ttu-id="8e0c7-116">既存のすべてを上書き`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-116">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="8e0c7-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8e0c7-117">ForceEnglishOutput</span></span> | <span data-ttu-id="8e0c7-118">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8e0c7-119">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="8e0c7-119">Help</span></span> | <span data-ttu-id="8e0c7-120">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="8e0c7-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="8e0c7-121">NonInteractive</span></span> | <span data-ttu-id="8e0c7-122">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="8e0c7-123">詳細度</span><span class="sxs-lookup"><span data-stu-id="8e0c7-123">Verbosity</span></span> | <span data-ttu-id="8e0c7-124">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="8e0c7-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="8e0c7-125">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8e0c7-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="8e0c7-126">使用例</span><span class="sxs-lookup"><span data-stu-id="8e0c7-126">Examples</span></span>

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
