---
title: NuGet CLI コマンドを追加します。
description: Nuget.exe への参照の追加コマンド
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545835"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="26557-103">addコマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="26557-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="26557-104">**適用対象**: パッケージの発行&bullet;**サポートされているバージョン**: 3.3 以降</span><span class="sxs-lookup"><span data-stu-id="26557-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="26557-105">パッケージ ID とバージョン番号のフォルダーを作成する場合、階層構造で、HTTP 以外のパッケージ ソース (フォルダーまたは UNC パス) には、指定したパッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="26557-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="26557-106">例えば:</span><span class="sxs-lookup"><span data-stu-id="26557-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="26557-107">復元またはパッケージのソースに対して更新をするとき、階層構造は、パフォーマンスが著しく向上を提供します。</span><span class="sxs-lookup"><span data-stu-id="26557-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="26557-108">変換先のパッケージ ソースをパッケージ内のすべてのファイルを展開するには、使用、`-Expand`スイッチします。</span><span class="sxs-lookup"><span data-stu-id="26557-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="26557-109">これは通常など、変換先に表示されている他のサブフォルダーになります`tools`と`lib`します。</span><span class="sxs-lookup"><span data-stu-id="26557-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="26557-110">使用法</span><span class="sxs-lookup"><span data-stu-id="26557-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="26557-111">場所`<packagePath>`を追加するパッケージへのパス名と`<sourcePath>`パッケージの追加先となるフォルダー ベースのパッケージ ソースを指定します。</span><span class="sxs-lookup"><span data-stu-id="26557-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="26557-112">HTTP ソースがサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="26557-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="26557-113">オプション</span><span class="sxs-lookup"><span data-stu-id="26557-113">Options</span></span>

| <span data-ttu-id="26557-114">オプション</span><span class="sxs-lookup"><span data-stu-id="26557-114">Option</span></span> | <span data-ttu-id="26557-115">説明</span><span class="sxs-lookup"><span data-stu-id="26557-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26557-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="26557-116">ConfigFile</span></span> | <span data-ttu-id="26557-117">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="26557-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="26557-118">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="26557-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="26557-119">Expand</span><span class="sxs-lookup"><span data-stu-id="26557-119">Expand</span></span> | <span data-ttu-id="26557-120">パッケージ ソースには、パッケージ内のすべてのファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="26557-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="26557-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="26557-121">ForceEnglishOutput</span></span> | <span data-ttu-id="26557-122">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="26557-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="26557-123">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="26557-123">Help</span></span> | <span data-ttu-id="26557-124">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="26557-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="26557-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="26557-125">NonInteractive</span></span> | <span data-ttu-id="26557-126">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="26557-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="26557-127">詳細度</span><span class="sxs-lookup"><span data-stu-id="26557-127">Verbosity</span></span> | <span data-ttu-id="26557-128">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="26557-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="26557-129">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="26557-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="26557-130">使用例</span><span class="sxs-lookup"><span data-stu-id="26557-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
