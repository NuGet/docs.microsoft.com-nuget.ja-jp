---
title: "NuGet CLI 仕様コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Nuget.exe spec コマンドのリファレンス"
keywords: "nuget spec 参照、spec コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a><span data-ttu-id="15e99-104">spec コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="15e99-104">spec command (NuGet CLI)</span></span>

<span data-ttu-id="15e99-105">**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="15e99-105">**Applies to:** package creation &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="15e99-106">生成、`.nuspec`新しいパッケージのファイルです。</span><span class="sxs-lookup"><span data-stu-id="15e99-106">Generates a `.nuspec` file for a new package.</span></span> <span data-ttu-id="15e99-107">プロジェクト ファイルと同じフォルダーで実行された場合 (`.csproj`、 `.vbproj`、 `.fsproj`)、 `spec` 、トークン化された作成`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="15e99-107">If run in the same folder as a project file (`.csproj`, `.vbproj`, `.fsproj`), `spec` creates a tokenized `.nuspec` file.</span></span> <span data-ttu-id="15e99-108">詳細については、次を参照してください。[パッケージを作成する](../create-packages/creating-a-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="15e99-108">For additional information, see [Creating a Package](../create-packages/creating-a-package.md).</span></span>

## <a name="usage"></a><span data-ttu-id="15e99-109">使用方法</span><span class="sxs-lookup"><span data-stu-id="15e99-109">Usage</span></span>

```
nuget spec [<packageID>] [options]
```

<span data-ttu-id="15e99-110">ここで`<packageID>`で保存する省略可能なパッケージ識別子、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="15e99-110">where `<packageID>` is an optional package identifier to save in the `.nuspec` file.</span></span>

## <a name="options"></a><span data-ttu-id="15e99-111">オプション</span><span class="sxs-lookup"><span data-stu-id="15e99-111">Options</span></span>

| <span data-ttu-id="15e99-112">オプション</span><span class="sxs-lookup"><span data-stu-id="15e99-112">Option</span></span> | <span data-ttu-id="15e99-113">説明</span><span class="sxs-lookup"><span data-stu-id="15e99-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="15e99-114">AssemblyPath</span><span class="sxs-lookup"><span data-stu-id="15e99-114">AssemblyPath</span></span> | <span data-ttu-id="15e99-115">メタデータに使用するアセンブリへのパスを指定します。</span><span class="sxs-lookup"><span data-stu-id="15e99-115">Specifies the path to the assembly to use for metadata.</span></span> |
| <span data-ttu-id="15e99-116">Force</span><span class="sxs-lookup"><span data-stu-id="15e99-116">Force</span></span> | <span data-ttu-id="15e99-117">既存のすべてを上書き`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="15e99-117">Overwrites any existing `.nuspec` file.</span></span> |
| <span data-ttu-id="15e99-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="15e99-118">ForceEnglishOutput</span></span> | <span data-ttu-id="15e99-119">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="15e99-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="15e99-120">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="15e99-120">Help</span></span> | <span data-ttu-id="15e99-121">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="15e99-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="15e99-122">非対話型</span><span class="sxs-lookup"><span data-stu-id="15e99-122">NonInteractive</span></span> | <span data-ttu-id="15e99-123">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="15e99-123">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="15e99-124">詳細度</span><span class="sxs-lookup"><span data-stu-id="15e99-124">Verbosity</span></span> | <span data-ttu-id="15e99-125">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="15e99-125">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="15e99-126">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="15e99-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="15e99-127">例</span><span class="sxs-lookup"><span data-stu-id="15e99-127">Examples</span></span>

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
