---
title: "NuGet CLI コマンドの削除 |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe delete コマンドのリファレンス"
keywords: "nuget の参照を削除、パッケージのコマンドを削除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b5d53b83cdccaa8e284b844786b0ec27e7afb63a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="f4829-104">delete コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f4829-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="f4829-105">**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="f4829-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f4829-106">削除またはパッケージ ソースからパッケージを unlists します。</span><span class="sxs-lookup"><span data-stu-id="f4829-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="f4829-107">Nuget.org、delete コマンドの[unlists パッケージ](../policies/deleting-packages.md)です。</span><span class="sxs-lookup"><span data-stu-id="f4829-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f4829-108">使用法</span><span class="sxs-lookup"><span data-stu-id="f4829-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="f4829-109">ここで`<packageID>`と`<packageVersion>`非公開または削除する正確なパッケージを識別します。</span><span class="sxs-lookup"><span data-stu-id="f4829-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="f4829-110">正確な動作は、ソースによって異なります。</span><span class="sxs-lookup"><span data-stu-id="f4829-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="f4829-111">ローカル フォルダー、たとえば、パッケージが削除される;nuget.org パッケージが一覧表示ではありません。</span><span class="sxs-lookup"><span data-stu-id="f4829-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="f4829-112">オプション</span><span class="sxs-lookup"><span data-stu-id="f4829-112">Options</span></span>

| <span data-ttu-id="f4829-113">オプション</span><span class="sxs-lookup"><span data-stu-id="f4829-113">Option</span></span> | <span data-ttu-id="f4829-114">説明</span><span class="sxs-lookup"><span data-stu-id="f4829-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4829-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="f4829-115">ApiKey</span></span> | <span data-ttu-id="f4829-116">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="f4829-116">The API key for the target repository.</span></span> <span data-ttu-id="f4829-117">存在しない場合は、構成ファイルで指定されているが使用されます。</span><span class="sxs-lookup"><span data-stu-id="f4829-117">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="f4829-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f4829-118">ConfigFile</span></span> | <span data-ttu-id="f4829-119">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="f4829-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f4829-120">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="f4829-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f4829-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f4829-121">ForceEnglishOutput</span></span> | <span data-ttu-id="f4829-122">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="f4829-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f4829-123">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="f4829-123">Help</span></span> | <span data-ttu-id="f4829-124">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="f4829-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="f4829-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f4829-125">NonInteractive</span></span> | <span data-ttu-id="f4829-126">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="f4829-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f4829-127">ソース</span><span class="sxs-lookup"><span data-stu-id="f4829-127">Source</span></span> | <span data-ttu-id="f4829-128">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="f4829-128">Specifies the server URL.</span></span> <span data-ttu-id="f4829-129">Nuget.org の URL は`https://api.nuget.org/v3/index.json`します。</span><span class="sxs-lookup"><span data-stu-id="f4829-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="f4829-130">たとえば、プライベート フィードは、置き換えるホスト名、 *%hostname%/api/v3*です。</span><span class="sxs-lookup"><span data-stu-id="f4829-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="f4829-131">詳細度</span><span class="sxs-lookup"><span data-stu-id="f4829-131">Verbosity</span></span> | <span data-ttu-id="f4829-132">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="f4829-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f4829-133">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f4829-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f4829-134">使用例</span><span class="sxs-lookup"><span data-stu-id="f4829-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
