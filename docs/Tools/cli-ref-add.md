---
title: NuGet CLI コマンドを追加します。
description: コマンドを追加、nuget.exe への参照
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a4201a321ffe0f7fb61f4e98012a1a2d7d8fda4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="9a037-103">addコマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9a037-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="9a037-104">**適用されます**: パッケージの発行&bullet;**サポートされているバージョン**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="9a037-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="9a037-105">指定したパッケージをパッケージ ID とバージョン番号のフォルダーを作成する場合、階層構造での HTTP 以外のパッケージ ソース (フォルダーまたは UNC パス) に追加します。</span><span class="sxs-lookup"><span data-stu-id="9a037-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="9a037-106">例えば:</span><span class="sxs-lookup"><span data-stu-id="9a037-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="9a037-107">復元すると、パッケージ ソースに対して更新階層構造は、パフォーマンスが著しく向上を提供します。</span><span class="sxs-lookup"><span data-stu-id="9a037-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="9a037-108">変換先のパッケージ ソースに、パッケージ内のすべてのファイルを拡張しを使用して、`-Expand`スイッチします。</span><span class="sxs-lookup"><span data-stu-id="9a037-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="9a037-109">など、変換先に表示される他のサブフォルダーでこの結果、ほとんど`tools`と`lib`です。</span><span class="sxs-lookup"><span data-stu-id="9a037-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="9a037-110">使用法</span><span class="sxs-lookup"><span data-stu-id="9a037-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="9a037-111">ここで`<packagePath>`を追加するためのパッケージへのパス名と`<sourcePath>`パッケージの追加先となるフォルダーに基づくパッケージのソースを指定します。</span><span class="sxs-lookup"><span data-stu-id="9a037-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="9a037-112">HTTP ソースはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="9a037-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="9a037-113">オプション</span><span class="sxs-lookup"><span data-stu-id="9a037-113">Options</span></span>

| <span data-ttu-id="9a037-114">オプション</span><span class="sxs-lookup"><span data-stu-id="9a037-114">Option</span></span> | <span data-ttu-id="9a037-115">説明</span><span class="sxs-lookup"><span data-stu-id="9a037-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9a037-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9a037-116">ConfigFile</span></span> | <span data-ttu-id="9a037-117">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="9a037-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9a037-118">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="9a037-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9a037-119">Expand</span><span class="sxs-lookup"><span data-stu-id="9a037-119">Expand</span></span> | <span data-ttu-id="9a037-120">パッケージ ソースに、パッケージ内のすべてのファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="9a037-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="9a037-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9a037-121">ForceEnglishOutput</span></span> | <span data-ttu-id="9a037-122">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="9a037-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9a037-123">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="9a037-123">Help</span></span> | <span data-ttu-id="9a037-124">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="9a037-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="9a037-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9a037-125">NonInteractive</span></span> | <span data-ttu-id="9a037-126">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="9a037-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9a037-127">詳細度</span><span class="sxs-lookup"><span data-stu-id="9a037-127">Verbosity</span></span> | <span data-ttu-id="9a037-128">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="9a037-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9a037-129">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9a037-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9a037-130">使用例</span><span class="sxs-lookup"><span data-stu-id="9a037-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
