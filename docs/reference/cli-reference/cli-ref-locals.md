---
title: NuGet CLI の locals コマンド
description: Nuget.exe locals コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327809"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="5947d-103">locals コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5947d-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="5947d-104">**適用対象:** パッケージの使用3&bullet;が**サポートされているバージョン:** 3.3+</span><span class="sxs-lookup"><span data-stu-id="5947d-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="5947d-105">*Http キャッシュ*、*グローバルパッケージ*フォルダー、一時フォルダーなどのローカル NuGet リソースをクリアまたは一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="5947d-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="5947d-106">また`locals` 、コマンドを使用して、これらの場所の一覧を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="5947d-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="5947d-107">詳細については、「[グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5947d-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5947d-108">使用法</span><span class="sxs-lookup"><span data-stu-id="5947d-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="5947d-109">ここ`<folder>`で、は`all`、 `http-cache` `temp` `global-packages` `plugins-cache`、(3.5 以前)、、(3.4 +)、および (4.8 +) のいずれかです。 `packages-cache`</span><span class="sxs-lookup"><span data-stu-id="5947d-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="5947d-110">オプション</span><span class="sxs-lookup"><span data-stu-id="5947d-110">Options</span></span>

| <span data-ttu-id="5947d-111">オプション</span><span class="sxs-lookup"><span data-stu-id="5947d-111">Option</span></span> | <span data-ttu-id="5947d-112">説明</span><span class="sxs-lookup"><span data-stu-id="5947d-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5947d-113">Clear</span><span class="sxs-lookup"><span data-stu-id="5947d-113">Clear</span></span> | <span data-ttu-id="5947d-114">指定されたフォルダーをクリアします。</span><span class="sxs-lookup"><span data-stu-id="5947d-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="5947d-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5947d-115">ConfigFile</span></span> | <span data-ttu-id="5947d-116">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="5947d-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5947d-117">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="5947d-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5947d-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5947d-118">ForceEnglishOutput</span></span> | <span data-ttu-id="5947d-119">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="5947d-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5947d-120">Help</span><span class="sxs-lookup"><span data-stu-id="5947d-120">Help</span></span> | <span data-ttu-id="5947d-121">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="5947d-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="5947d-122">List</span><span class="sxs-lookup"><span data-stu-id="5947d-122">List</span></span> | <span data-ttu-id="5947d-123">指定したフォルダーの場所、または*すべて*のフォルダーを使用する場合はすべてのフォルダーの場所を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="5947d-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="5947d-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5947d-124">NonInteractive</span></span> | <span data-ttu-id="5947d-125">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="5947d-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5947d-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5947d-126">Verbosity</span></span> | <span data-ttu-id="5947d-127">出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="5947d-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5947d-128">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="5947d-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5947d-129">使用例</span><span class="sxs-lookup"><span data-stu-id="5947d-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="5947d-130">その他の例については、「[グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5947d-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
