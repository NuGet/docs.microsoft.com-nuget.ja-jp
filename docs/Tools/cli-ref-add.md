---
title: NuGet CLI コマンドを追加する |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: コマンドを追加、nuget.exe への参照
keywords: nuget の参照を追加する、パッケージのコマンドを追加
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 48e093cbae2cecb1652e17a9b26920107aa8aef7
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="cff37-104">コマンド (NuGet CLI) を追加します。</span><span class="sxs-lookup"><span data-stu-id="cff37-104">add command (NuGet CLI)</span></span>

<span data-ttu-id="cff37-105">**適用されます**: パッケージの発行&bullet;**サポートされているバージョン**: 3.3 +</span><span class="sxs-lookup"><span data-stu-id="cff37-105">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="cff37-106">指定したパッケージをパッケージ ID とバージョン番号のフォルダーを作成する場合、階層構造での HTTP 以外のパッケージ ソース (フォルダーまたは UNC パス) に追加します。</span><span class="sxs-lookup"><span data-stu-id="cff37-106">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="cff37-107">例えば:</span><span class="sxs-lookup"><span data-stu-id="cff37-107">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="cff37-108">復元すると、パッケージ ソースに対して更新階層構造は、パフォーマンスが著しく向上を提供します。</span><span class="sxs-lookup"><span data-stu-id="cff37-108">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="cff37-109">変換先のパッケージ ソースに、パッケージ内のすべてのファイルを拡張しを使用して、`-Expand`スイッチします。</span><span class="sxs-lookup"><span data-stu-id="cff37-109">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="cff37-110">など、変換先に表示される他のサブフォルダーでこの結果、ほとんど`tools`と`lib`です。</span><span class="sxs-lookup"><span data-stu-id="cff37-110">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="cff37-111">使用法</span><span class="sxs-lookup"><span data-stu-id="cff37-111">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="cff37-112">ここで`<packagePath>`を追加するためのパッケージへのパス名と`<sourcePath>`パッケージの追加先となるフォルダーに基づくパッケージのソースを指定します。</span><span class="sxs-lookup"><span data-stu-id="cff37-112">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="cff37-113">HTTP ソースはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="cff37-113">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="cff37-114">オプション</span><span class="sxs-lookup"><span data-stu-id="cff37-114">Options</span></span>

| <span data-ttu-id="cff37-115">オプション</span><span class="sxs-lookup"><span data-stu-id="cff37-115">Option</span></span> | <span data-ttu-id="cff37-116">説明</span><span class="sxs-lookup"><span data-stu-id="cff37-116">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cff37-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cff37-117">ConfigFile</span></span> | <span data-ttu-id="cff37-118">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="cff37-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cff37-119">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="cff37-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cff37-120">Expand</span><span class="sxs-lookup"><span data-stu-id="cff37-120">Expand</span></span> | <span data-ttu-id="cff37-121">パッケージ ソースに、パッケージ内のすべてのファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="cff37-121">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="cff37-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cff37-122">ForceEnglishOutput</span></span> | <span data-ttu-id="cff37-123">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="cff37-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cff37-124">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="cff37-124">Help</span></span> | <span data-ttu-id="cff37-125">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="cff37-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="cff37-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cff37-126">NonInteractive</span></span> | <span data-ttu-id="cff37-127">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="cff37-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cff37-128">詳細度</span><span class="sxs-lookup"><span data-stu-id="cff37-128">Verbosity</span></span> | <span data-ttu-id="cff37-129">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="cff37-129">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="cff37-130">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cff37-130">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cff37-131">使用例</span><span class="sxs-lookup"><span data-stu-id="cff37-131">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
