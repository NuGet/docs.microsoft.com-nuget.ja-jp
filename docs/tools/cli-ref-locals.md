---
title: NuGet CLI [ローカル] コマンド
description: Nuget.exe [ローカル] コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818202"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="34bed-103">locals コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="34bed-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="34bed-104">**適用されます:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="34bed-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="34bed-105">消去または NuGet のローカル リソースを一覧表示など、 *http キャッシュ*、*グローバル パッケージ*フォルダー、および一時フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="34bed-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="34bed-106">`locals`コマンドを使用してこれらの場所の一覧を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="34bed-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="34bed-107">詳細については、次を参照してください。[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。</span><span class="sxs-lookup"><span data-stu-id="34bed-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="34bed-108">使用法</span><span class="sxs-lookup"><span data-stu-id="34bed-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="34bed-109">ここで`<folder>`の 1 つ`all`、 `http-cache`、 `packages-cache` *(3.5 およびそれ以前)*、 `global-packages`、および`temp` *(3.4 以降)* です。</span><span class="sxs-lookup"><span data-stu-id="34bed-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="34bed-110">オプション</span><span class="sxs-lookup"><span data-stu-id="34bed-110">Options</span></span>

| <span data-ttu-id="34bed-111">オプション</span><span class="sxs-lookup"><span data-stu-id="34bed-111">Option</span></span> | <span data-ttu-id="34bed-112">説明</span><span class="sxs-lookup"><span data-stu-id="34bed-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34bed-113">Clear</span><span class="sxs-lookup"><span data-stu-id="34bed-113">Clear</span></span> | <span data-ttu-id="34bed-114">指定したフォルダーを消去します。</span><span class="sxs-lookup"><span data-stu-id="34bed-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="34bed-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="34bed-115">ConfigFile</span></span> | <span data-ttu-id="34bed-116">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="34bed-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="34bed-117">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="34bed-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="34bed-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="34bed-118">ForceEnglishOutput</span></span> | <span data-ttu-id="34bed-119">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="34bed-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="34bed-120">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="34bed-120">Help</span></span> | <span data-ttu-id="34bed-121">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="34bed-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="34bed-122">リスト</span><span class="sxs-lookup"><span data-stu-id="34bed-122">List</span></span> | <span data-ttu-id="34bed-123">指定したフォルダーの場所またはを使用すると、すべてのフォルダーの場所を一覧表示*すべて*です。</span><span class="sxs-lookup"><span data-stu-id="34bed-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="34bed-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="34bed-124">NonInteractive</span></span> | <span data-ttu-id="34bed-125">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="34bed-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="34bed-126">詳細度</span><span class="sxs-lookup"><span data-stu-id="34bed-126">Verbosity</span></span> | <span data-ttu-id="34bed-127">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="34bed-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="34bed-128">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="34bed-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="34bed-129">使用例</span><span class="sxs-lookup"><span data-stu-id="34bed-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="34bed-130">その他の例では、次を参照してください。[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。</span><span class="sxs-lookup"><span data-stu-id="34bed-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
