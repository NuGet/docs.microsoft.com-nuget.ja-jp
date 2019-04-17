---
title: NuGet CLI delete コマンド
description: Nuget.exe 削除コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548511"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="60953-103">delete コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="60953-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="60953-104">**適用対象:** パッケージの発行&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="60953-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="60953-105">パッケージ ソースからパッケージを一覧から、または削除します。</span><span class="sxs-lookup"><span data-stu-id="60953-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="60953-106">Nuget.org には、delete コマンドの[パッケージを一覧から](../policies/deleting-packages.md)します。</span><span class="sxs-lookup"><span data-stu-id="60953-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="60953-107">使用法</span><span class="sxs-lookup"><span data-stu-id="60953-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="60953-108">場所`<packageID>`と`<packageVersion>`を削除または一覧から削除する正確なパッケージを識別します。</span><span class="sxs-lookup"><span data-stu-id="60953-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="60953-109">正確な動作は、ソースによって異なります。</span><span class="sxs-lookup"><span data-stu-id="60953-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="60953-110">ローカル フォルダーは、たとえば、パッケージを削除します。nuget.org のパッケージが一覧表示されているではありません。</span><span class="sxs-lookup"><span data-stu-id="60953-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="60953-111">オプション</span><span class="sxs-lookup"><span data-stu-id="60953-111">Options</span></span>

| <span data-ttu-id="60953-112">オプション</span><span class="sxs-lookup"><span data-stu-id="60953-112">Option</span></span> | <span data-ttu-id="60953-113">説明</span><span class="sxs-lookup"><span data-stu-id="60953-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="60953-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="60953-114">ApiKey</span></span> | <span data-ttu-id="60953-115">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="60953-115">The API key for the target repository.</span></span> <span data-ttu-id="60953-116">存在しない場合は、構成ファイルで指定された 1 つが使用されます。</span><span class="sxs-lookup"><span data-stu-id="60953-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="60953-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="60953-117">ConfigFile</span></span> | <span data-ttu-id="60953-118">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="60953-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="60953-119">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="60953-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="60953-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="60953-120">ForceEnglishOutput</span></span> | <span data-ttu-id="60953-121">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="60953-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="60953-122">Help</span><span class="sxs-lookup"><span data-stu-id="60953-122">Help</span></span> | <span data-ttu-id="60953-123">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="60953-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="60953-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="60953-124">NonInteractive</span></span> | <span data-ttu-id="60953-125">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="60953-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="60953-126">Source</span><span class="sxs-lookup"><span data-stu-id="60953-126">Source</span></span> | <span data-ttu-id="60953-127">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="60953-127">Specifies the server URL.</span></span> <span data-ttu-id="60953-128">Nuget.org の URL は`https://api.nuget.org/v3/index.json`します。</span><span class="sxs-lookup"><span data-stu-id="60953-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="60953-129">たとえば、プライベート フィードを置き換えて、ホスト名 *%hostname%/api/v3*します。</span><span class="sxs-lookup"><span data-stu-id="60953-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="60953-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="60953-130">Verbosity</span></span> | <span data-ttu-id="60953-131">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="60953-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="60953-132">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="60953-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="60953-133">使用例</span><span class="sxs-lookup"><span data-stu-id="60953-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
