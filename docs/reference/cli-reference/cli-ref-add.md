---
title: NuGet CLI の追加コマンド
description: nuget.exe add コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 096d2f7a61a3c861ce2084368500ab8e8b21f212
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776092"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="63ad0-103">コマンドの追加 (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="63ad0-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="63ad0-104">**適用対象**: パッケージ発行が &bullet; **サポートされているバージョン**: 3.3 以降</span><span class="sxs-lookup"><span data-stu-id="63ad0-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="63ad0-105">指定されたパッケージを非 HTTP パッケージソース (フォルダーまたは UNC パス) に階層構造で追加します。この場合、パッケージ ID とバージョン番号に対してフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="63ad0-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="63ad0-106">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="63ad0-106">For example:</span></span>

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

<span data-ttu-id="63ad0-107">パッケージソースに対して復元または更新を行う場合、階層レイアウトはパフォーマンスを大幅に向上させます。</span><span class="sxs-lookup"><span data-stu-id="63ad0-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="63ad0-108">パッケージ内のすべてのファイルを目的のパッケージソースに展開するには、スイッチを使用し `-Expand` ます。</span><span class="sxs-lookup"><span data-stu-id="63ad0-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="63ad0-109">通常、これにより、やなどの追加のサブフォルダーが変換先に表示され `tools` `lib` ます。</span><span class="sxs-lookup"><span data-stu-id="63ad0-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="63ad0-110">使用方法</span><span class="sxs-lookup"><span data-stu-id="63ad0-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="63ad0-111">`<packagePath>`は、追加するパッケージのパス名です。は、 `<sourcePath>` パッケージの追加先となるフォルダーベースのパッケージソースを指定します。</span><span class="sxs-lookup"><span data-stu-id="63ad0-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="63ad0-112">HTTP ソースはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="63ad0-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="63ad0-113">Options</span><span class="sxs-lookup"><span data-stu-id="63ad0-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="63ad0-114">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="63ad0-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="63ad0-115">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="63ad0-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Expand`**

  <span data-ttu-id="63ad0-116">パッケージ内のすべてのファイルをパッケージソースに追加します。</span><span class="sxs-lookup"><span data-stu-id="63ad0-116">Adds all the files in the package to the package source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="63ad0-117">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="63ad0-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>
<span data-ttu-id="63ad0-118">不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="63ad0-118">Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="63ad0-119">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="63ad0-119">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="63ad0-120">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="63ad0-120">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

   <span data-ttu-id="63ad0-121">Nupkg を追加するフォルダーまたは UNC 共有のパッケージソースを指定します。</span><span class="sxs-lookup"><span data-stu-id="63ad0-121">Specifies the package source, which is a folder or UNC share, to which the nupkg will be added.</span></span> <span data-ttu-id="63ad0-122">Http ソースはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="63ad0-122">Http sources are not supported.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="63ad0-123">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="63ad0-123">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="63ad0-124">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="63ad0-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="63ad0-125">使用例</span><span class="sxs-lookup"><span data-stu-id="63ad0-125">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
