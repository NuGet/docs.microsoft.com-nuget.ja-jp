---
title: NuGet CLI delete コマンド
description: Nuget.exe 削除コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426108"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="1cf41-103">delete コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1cf41-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="1cf41-104">**適用対象:** パッケージの発行&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="1cf41-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="1cf41-105">パッケージ ソースからパッケージを一覧から、または削除します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="1cf41-106">Nuget.org には、delete コマンドの[パッケージを一覧から](../nuget-org/policies/deleting-packages.md)します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-106">For nuget.org, the delete command [unlists the package](../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="1cf41-107">使用法</span><span class="sxs-lookup"><span data-stu-id="1cf41-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="1cf41-108">場所`<packageID>`と`<packageVersion>`を削除または一覧から削除する正確なパッケージを識別します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="1cf41-109">正確な動作は、ソースによって異なります。</span><span class="sxs-lookup"><span data-stu-id="1cf41-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="1cf41-110">ローカル フォルダーは、たとえば、パッケージを削除します。nuget.org のパッケージが一覧表示されているではありません。</span><span class="sxs-lookup"><span data-stu-id="1cf41-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="1cf41-111">オプション</span><span class="sxs-lookup"><span data-stu-id="1cf41-111">Options</span></span>

| <span data-ttu-id="1cf41-112">オプション</span><span class="sxs-lookup"><span data-stu-id="1cf41-112">Option</span></span> | <span data-ttu-id="1cf41-113">説明</span><span class="sxs-lookup"><span data-stu-id="1cf41-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1cf41-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="1cf41-114">ApiKey</span></span> | <span data-ttu-id="1cf41-115">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="1cf41-115">The API key for the target repository.</span></span> <span data-ttu-id="1cf41-116">存在しない場合は、構成ファイルで指定された 1 つが使用されます。</span><span class="sxs-lookup"><span data-stu-id="1cf41-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="1cf41-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1cf41-117">ConfigFile</span></span> | <span data-ttu-id="1cf41-118">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="1cf41-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1cf41-119">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1cf41-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1cf41-120">ForceEnglishOutput</span></span> | <span data-ttu-id="1cf41-121">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1cf41-122">Help</span><span class="sxs-lookup"><span data-stu-id="1cf41-122">Help</span></span> | <span data-ttu-id="1cf41-123">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="1cf41-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1cf41-124">NonInteractive</span></span> | <span data-ttu-id="1cf41-125">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1cf41-126">Source</span><span class="sxs-lookup"><span data-stu-id="1cf41-126">Source</span></span> | <span data-ttu-id="1cf41-127">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-127">Specifies the server URL.</span></span> <span data-ttu-id="1cf41-128">Nuget.org の URL は`https://api.nuget.org/v3/index.json`します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="1cf41-129">たとえば、プライベート フィードを置き換えて、ホスト名 *%hostname%/api/v3*します。</span><span class="sxs-lookup"><span data-stu-id="1cf41-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="1cf41-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="1cf41-130">Verbosity</span></span> | <span data-ttu-id="1cf41-131">出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="1cf41-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1cf41-132">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1cf41-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1cf41-133">使用例</span><span class="sxs-lookup"><span data-stu-id="1cf41-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
