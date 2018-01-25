---
title: "NuGet CLI ローカル コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe [ローカル] コマンドのリファレンス"
keywords: "nuget ローカル変数の参照、[ローカル] コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="d95f2-104">[ローカル] コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d95f2-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="d95f2-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="d95f2-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="d95f2-106">消去または http 要求のキャッシュ、パッケージ キャッシュ、および、コンピューター全体のグローバル パッケージ フォルダーなどのローカルの NuGet リソースを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="d95f2-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="d95f2-107">`locals`コマンドを使用してこれらの場所の一覧を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="d95f2-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="d95f2-108">詳細については、次を参照してください。 [NuGet キャッシュを管理する](../consume-packages/managing-the-nuget-cache.md)です。</span><span class="sxs-lookup"><span data-stu-id="d95f2-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d95f2-109">使用法</span><span class="sxs-lookup"><span data-stu-id="d95f2-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="d95f2-110">ここで`<cache>`の 1 つ`all`、 `http-cache`、 `packages-cache`、 `global-packages`、および`temp` *(3.4 以降)*です。</span><span class="sxs-lookup"><span data-stu-id="d95f2-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="d95f2-111">オプション</span><span class="sxs-lookup"><span data-stu-id="d95f2-111">Options</span></span>

| <span data-ttu-id="d95f2-112">オプション</span><span class="sxs-lookup"><span data-stu-id="d95f2-112">Option</span></span> | <span data-ttu-id="d95f2-113">説明</span><span class="sxs-lookup"><span data-stu-id="d95f2-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d95f2-114">Clear</span><span class="sxs-lookup"><span data-stu-id="d95f2-114">Clear</span></span> | <span data-ttu-id="d95f2-115">指定されたキャッシュをクリアします。</span><span class="sxs-lookup"><span data-stu-id="d95f2-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="d95f2-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d95f2-116">ConfigFile</span></span> | <span data-ttu-id="d95f2-117">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="d95f2-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d95f2-118">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="d95f2-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="d95f2-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d95f2-119">ForceEnglishOutput</span></span> | <span data-ttu-id="d95f2-120">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="d95f2-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d95f2-121">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="d95f2-121">Help</span></span> | <span data-ttu-id="d95f2-122">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d95f2-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="d95f2-123">リスト</span><span class="sxs-lookup"><span data-stu-id="d95f2-123">List</span></span> | <span data-ttu-id="d95f2-124">指定されたキャッシュの場所またはを使用すると、すべてのキャッシュの場所を一覧表示*すべて*です。</span><span class="sxs-lookup"><span data-stu-id="d95f2-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="d95f2-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d95f2-125">NonInteractive</span></span> | <span data-ttu-id="d95f2-126">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="d95f2-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d95f2-127">詳細度</span><span class="sxs-lookup"><span data-stu-id="d95f2-127">Verbosity</span></span> | <span data-ttu-id="d95f2-128">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="d95f2-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d95f2-129">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d95f2-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d95f2-130">使用例</span><span class="sxs-lookup"><span data-stu-id="d95f2-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
