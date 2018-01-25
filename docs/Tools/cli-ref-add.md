---
title: "NuGet CLI コマンドを追加する |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "コマンドを追加、nuget.exe への参照"
keywords: "nuget の参照を追加する、パッケージのコマンドを追加"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 70c86f8d240bd308224f6b7887b630cc1e953bf8
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="33c01-104">コマンド (NuGet CLI) を追加します。</span><span class="sxs-lookup"><span data-stu-id="33c01-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="33c01-105">**適用されます**: パッケージの発行&bullet;**サポートされているバージョン**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="33c01-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="33c01-106">指定したパッケージをパッケージ ID とバージョン番号のフォルダーを作成する場合、階層構造での HTTP 以外のパッケージ ソース (フォルダーまたは UNC パス) に追加します。</span><span class="sxs-lookup"><span data-stu-id="33c01-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="33c01-107">例:</span><span class="sxs-lookup"><span data-stu-id="33c01-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="33c01-108">復元すると、パッケージ ソースに対して更新階層構造は、パフォーマンスが著しく向上を提供します。</span><span class="sxs-lookup"><span data-stu-id="33c01-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="33c01-109">変換先のパッケージ ソースに、パッケージ内のすべてのファイルを拡張しを使用して、`-Expand`スイッチします。</span><span class="sxs-lookup"><span data-stu-id="33c01-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="33c01-110">など、変換先に表示される他のサブフォルダーでこの結果、ほとんど`tools`と`lib`です。</span><span class="sxs-lookup"><span data-stu-id="33c01-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="33c01-111">使用法</span><span class="sxs-lookup"><span data-stu-id="33c01-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="33c01-112">ここで`<packagePath>`を追加するためのパッケージへのパス名と`<sourcePath>`パッケージの追加先となるフォルダーに基づくパッケージのソースを指定します。</span><span class="sxs-lookup"><span data-stu-id="33c01-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="33c01-113">HTTP ソースはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="33c01-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="33c01-114">オプション</span><span class="sxs-lookup"><span data-stu-id="33c01-114">Options</span></span>

| <span data-ttu-id="33c01-115">オプション</span><span class="sxs-lookup"><span data-stu-id="33c01-115">Option</span></span> | <span data-ttu-id="33c01-116">説明</span><span class="sxs-lookup"><span data-stu-id="33c01-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="33c01-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="33c01-117">ConfigFile</span></span> | <span data-ttu-id="33c01-118">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="33c01-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="33c01-119">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="33c01-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span>| 
| <span data-ttu-id="33c01-120">Expand</span><span class="sxs-lookup"><span data-stu-id="33c01-120">Expand</span></span> | <span data-ttu-id="33c01-121">パッケージ ソースに、パッケージ内のすべてのファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="33c01-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="33c01-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="33c01-122">ForceEnglishOutput</span></span> | <span data-ttu-id="33c01-123">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="33c01-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="33c01-124">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="33c01-124">Help</span></span> | <span data-ttu-id="33c01-125">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="33c01-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="33c01-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="33c01-126">NonInteractive</span></span> | <span data-ttu-id="33c01-127">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="33c01-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="33c01-128">詳細度</span><span class="sxs-lookup"><span data-stu-id="33c01-128">Verbosity</span></span> | <span data-ttu-id="33c01-129">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="33c01-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="33c01-130">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="33c01-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="33c01-131">使用例</span><span class="sxs-lookup"><span data-stu-id="33c01-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
