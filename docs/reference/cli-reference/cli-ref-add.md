---
title: NuGet CLI の追加コマンド
description: Nuget.exe の add コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327859"
---
# <a name="add-command-nuget-cli"></a><span data-ttu-id="5c804-103">addコマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5c804-103">add command (NuGet CLI)</span></span>

<span data-ttu-id="5c804-104">**適用対象**: パッケージ発行&bullet;が**サポートされているバージョン**:3.3+</span><span class="sxs-lookup"><span data-stu-id="5c804-104">**Applies to**: package publishing &bullet; **Supported versions**: 3.3+</span></span>

<span data-ttu-id="5c804-105">指定されたパッケージを非 HTTP パッケージソース (フォルダーまたは UNC パス) に階層構造で追加します。この場合、パッケージ ID とバージョン番号に対してフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="5c804-105">Adds a specified package to a non-HTTP package source (a folder or UNC path) in a hierarchical layout, wherein folders are created for the package ID and version number.</span></span> <span data-ttu-id="5c804-106">例えば:</span><span class="sxs-lookup"><span data-stu-id="5c804-106">For example:</span></span>

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

<span data-ttu-id="5c804-107">パッケージソースに対して復元または更新を行う場合、階層レイアウトはパフォーマンスを大幅に向上させます。</span><span class="sxs-lookup"><span data-stu-id="5c804-107">When restoring or updating against the package source, hierarchical layout provides significantly better performance.</span></span>

<span data-ttu-id="5c804-108">パッケージ内のすべてのファイルを目的のパッケージソースに展開するには`-Expand` 、スイッチを使用します。</span><span class="sxs-lookup"><span data-stu-id="5c804-108">To expand all the files in the package to the destination package source, use the `-Expand` switch.</span></span> <span data-ttu-id="5c804-109">通常、これにより、 `tools`や`lib`などの追加のサブフォルダーが変換先に表示されます。</span><span class="sxs-lookup"><span data-stu-id="5c804-109">This typically results in additional subfolders appearing in the destination, such as `tools` and `lib`.</span></span>

## <a name="usage"></a><span data-ttu-id="5c804-110">使用法</span><span class="sxs-lookup"><span data-stu-id="5c804-110">Usage</span></span>

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

<span data-ttu-id="5c804-111">は、追加するパッケージのパス名です。は`<sourcePath>` 、パッケージの追加先となるフォルダーベースのパッケージソースを指定します。 `<packagePath>`</span><span class="sxs-lookup"><span data-stu-id="5c804-111">where `<packagePath>` is the pathname to the package to add, and `<sourcePath>` specifies the folder-based package source to which the package will be added.</span></span> <span data-ttu-id="5c804-112">HTTP ソースはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="5c804-112">HTTP sources are not supported.</span></span>

## <a name="options"></a><span data-ttu-id="5c804-113">オプション</span><span class="sxs-lookup"><span data-stu-id="5c804-113">Options</span></span>

| <span data-ttu-id="5c804-114">オプション</span><span class="sxs-lookup"><span data-stu-id="5c804-114">Option</span></span> | <span data-ttu-id="5c804-115">説明</span><span class="sxs-lookup"><span data-stu-id="5c804-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5c804-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5c804-116">ConfigFile</span></span> | <span data-ttu-id="5c804-117">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="5c804-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5c804-118">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="5c804-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5c804-119">Expand</span><span class="sxs-lookup"><span data-stu-id="5c804-119">Expand</span></span> | <span data-ttu-id="5c804-120">パッケージ内のすべてのファイルをパッケージソースに追加します。</span><span class="sxs-lookup"><span data-stu-id="5c804-120">Adds all the files in the package to the package source.</span></span> |
| <span data-ttu-id="5c804-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5c804-121">ForceEnglishOutput</span></span> | <span data-ttu-id="5c804-122">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="5c804-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5c804-123">Help</span><span class="sxs-lookup"><span data-stu-id="5c804-123">Help</span></span> | <span data-ttu-id="5c804-124">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="5c804-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="5c804-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5c804-125">NonInteractive</span></span> | <span data-ttu-id="5c804-126">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="5c804-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5c804-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5c804-127">Verbosity</span></span> | <span data-ttu-id="5c804-128">出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="5c804-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5c804-129">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="5c804-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5c804-130">使用例</span><span class="sxs-lookup"><span data-stu-id="5c804-130">Examples</span></span>

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
