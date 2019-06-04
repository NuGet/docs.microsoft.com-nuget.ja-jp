---
title: ローカルの NuGet CLI コマンド
description: Nuget.exe の [ローカル] コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545029"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="09d12-103">locals コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="09d12-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="09d12-104">**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="09d12-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="09d12-105">クリアまたはローカルの NuGet リソースを一覧表示など、 *http キャッシュ*、*グローバル パッケージ*フォルダー、および一時フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="09d12-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="09d12-106">`locals`コマンドがそれらの場所の一覧を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="09d12-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="09d12-107">詳細については、[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="09d12-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="09d12-108">使用法</span><span class="sxs-lookup"><span data-stu-id="09d12-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="09d12-109">場所`<folder>`の 1 つ`all`、 `http-cache`、 `packages-cache` *(3.5 およびそれ以前)* 、 `global-packages`、 `temp` *(3.4 以上)* 、および`plugins-cache` *(4.8 +)* します。</span><span class="sxs-lookup"><span data-stu-id="09d12-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="09d12-110">オプション</span><span class="sxs-lookup"><span data-stu-id="09d12-110">Options</span></span>

| <span data-ttu-id="09d12-111">オプション</span><span class="sxs-lookup"><span data-stu-id="09d12-111">Option</span></span> | <span data-ttu-id="09d12-112">説明</span><span class="sxs-lookup"><span data-stu-id="09d12-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="09d12-113">Clear</span><span class="sxs-lookup"><span data-stu-id="09d12-113">Clear</span></span> | <span data-ttu-id="09d12-114">指定したフォルダーをクリアします。</span><span class="sxs-lookup"><span data-stu-id="09d12-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="09d12-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="09d12-115">ConfigFile</span></span> | <span data-ttu-id="09d12-116">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="09d12-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="09d12-117">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="09d12-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="09d12-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="09d12-118">ForceEnglishOutput</span></span> | <span data-ttu-id="09d12-119">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="09d12-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="09d12-120">Help</span><span class="sxs-lookup"><span data-stu-id="09d12-120">Help</span></span> | <span data-ttu-id="09d12-121">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="09d12-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="09d12-122">List</span><span class="sxs-lookup"><span data-stu-id="09d12-122">List</span></span> | <span data-ttu-id="09d12-123">指定したフォルダーの場所またはを使用すると、すべてのフォルダーの場所を一覧表示*すべて*します。</span><span class="sxs-lookup"><span data-stu-id="09d12-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="09d12-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="09d12-124">NonInteractive</span></span> | <span data-ttu-id="09d12-125">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="09d12-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="09d12-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="09d12-126">Verbosity</span></span> | <span data-ttu-id="09d12-127">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="09d12-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="09d12-128">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="09d12-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="09d12-129">使用例</span><span class="sxs-lookup"><span data-stu-id="09d12-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="09d12-130">その他の例では、[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="09d12-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
