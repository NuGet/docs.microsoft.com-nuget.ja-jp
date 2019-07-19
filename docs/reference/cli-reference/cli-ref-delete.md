---
title: NuGet CLI の削除コマンド
description: Nuget.exe delete コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327839"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="f92dc-103">delete コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f92dc-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="f92dc-104">**適用対象:** パッケージ発行&bullet;の**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="f92dc-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f92dc-105">パッケージソースからパッケージを削除または一覧から削除します。</span><span class="sxs-lookup"><span data-stu-id="f92dc-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="f92dc-106">Nuget.org の場合、delete コマンドを実行すると、[パッケージの一覧](../../nuget-org/policies/deleting-packages.md)が解除されます。</span><span class="sxs-lookup"><span data-stu-id="f92dc-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f92dc-107">使用法</span><span class="sxs-lookup"><span data-stu-id="f92dc-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="f92dc-108">`<packageID>` と`<packageVersion>`は、削除するパッケージまたは一覧から削除を指定します。</span><span class="sxs-lookup"><span data-stu-id="f92dc-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="f92dc-109">実際の動作は、ソースによって異なります。</span><span class="sxs-lookup"><span data-stu-id="f92dc-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="f92dc-110">たとえば、ローカルフォルダーの場合、パッケージは削除されます。nuget.org の場合、パッケージは一覧から削除されます。</span><span class="sxs-lookup"><span data-stu-id="f92dc-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="f92dc-111">オプション</span><span class="sxs-lookup"><span data-stu-id="f92dc-111">Options</span></span>

| <span data-ttu-id="f92dc-112">オプション</span><span class="sxs-lookup"><span data-stu-id="f92dc-112">Option</span></span> | <span data-ttu-id="f92dc-113">説明</span><span class="sxs-lookup"><span data-stu-id="f92dc-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f92dc-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="f92dc-114">ApiKey</span></span> | <span data-ttu-id="f92dc-115">ターゲットリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="f92dc-115">The API key for the target repository.</span></span> <span data-ttu-id="f92dc-116">存在しない場合は、構成ファイルで指定されたものが使用されます。</span><span class="sxs-lookup"><span data-stu-id="f92dc-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="f92dc-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f92dc-117">ConfigFile</span></span> | <span data-ttu-id="f92dc-118">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="f92dc-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f92dc-119">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="f92dc-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f92dc-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f92dc-120">ForceEnglishOutput</span></span> | <span data-ttu-id="f92dc-121">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="f92dc-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f92dc-122">Help</span><span class="sxs-lookup"><span data-stu-id="f92dc-122">Help</span></span> | <span data-ttu-id="f92dc-123">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="f92dc-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="f92dc-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f92dc-124">NonInteractive</span></span> | <span data-ttu-id="f92dc-125">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="f92dc-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f92dc-126">Source</span><span class="sxs-lookup"><span data-stu-id="f92dc-126">Source</span></span> | <span data-ttu-id="f92dc-127">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f92dc-127">Specifies the server URL.</span></span> <span data-ttu-id="f92dc-128">Nuget.org の URL は`https://api.nuget.org/v3/index.json`です。</span><span class="sxs-lookup"><span data-stu-id="f92dc-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="f92dc-129">プライベートフィードの場合は、ホスト名に置き換えます (例 *% hostname%/api/v3*)。</span><span class="sxs-lookup"><span data-stu-id="f92dc-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="f92dc-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="f92dc-130">Verbosity</span></span> | <span data-ttu-id="f92dc-131">出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="f92dc-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f92dc-132">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="f92dc-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f92dc-133">使用例</span><span class="sxs-lookup"><span data-stu-id="f92dc-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
