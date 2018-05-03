---
title: NuGet CLI delete コマンド
description: Nuget.exe delete コマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="9dddb-103">delete コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="9dddb-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="9dddb-104">**適用されます:** パッケージの発行&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="9dddb-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="9dddb-105">削除またはパッケージ ソースからパッケージを unlists します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="9dddb-106">Nuget.org、delete コマンドの[unlists パッケージ](../policies/deleting-packages.md)です。</span><span class="sxs-lookup"><span data-stu-id="9dddb-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="9dddb-107">使用法</span><span class="sxs-lookup"><span data-stu-id="9dddb-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="9dddb-108">ここで`<packageID>`と`<packageVersion>`非公開または削除する正確なパッケージを識別します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="9dddb-109">正確な動作は、ソースによって異なります。</span><span class="sxs-lookup"><span data-stu-id="9dddb-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="9dddb-110">ローカル フォルダー、たとえば、パッケージが削除される;nuget.org パッケージが一覧表示ではありません。</span><span class="sxs-lookup"><span data-stu-id="9dddb-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="9dddb-111">オプション</span><span class="sxs-lookup"><span data-stu-id="9dddb-111">Options</span></span>

| <span data-ttu-id="9dddb-112">オプション</span><span class="sxs-lookup"><span data-stu-id="9dddb-112">Option</span></span> | <span data-ttu-id="9dddb-113">説明</span><span class="sxs-lookup"><span data-stu-id="9dddb-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="9dddb-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="9dddb-114">ApiKey</span></span> | <span data-ttu-id="9dddb-115">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="9dddb-115">The API key for the target repository.</span></span> <span data-ttu-id="9dddb-116">存在しない場合は、構成ファイルで指定されているが使用されます。</span><span class="sxs-lookup"><span data-stu-id="9dddb-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="9dddb-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="9dddb-117">ConfigFile</span></span> | <span data-ttu-id="9dddb-118">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="9dddb-119">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="9dddb-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="9dddb-120">ForceEnglishOutput</span></span> | <span data-ttu-id="9dddb-121">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="9dddb-122">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="9dddb-122">Help</span></span> | <span data-ttu-id="9dddb-123">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="9dddb-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="9dddb-124">NonInteractive</span></span> | <span data-ttu-id="9dddb-125">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="9dddb-126">ソース</span><span class="sxs-lookup"><span data-stu-id="9dddb-126">Source</span></span> | <span data-ttu-id="9dddb-127">サーバー URL を指定します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-127">Specifies the server URL.</span></span> <span data-ttu-id="9dddb-128">Nuget.org の URL は`https://api.nuget.org/v3/index.json`します。</span><span class="sxs-lookup"><span data-stu-id="9dddb-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="9dddb-129">たとえば、プライベート フィードは、置き換えるホスト名、 *%hostname%/api/v3*です。</span><span class="sxs-lookup"><span data-stu-id="9dddb-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="9dddb-130">詳細度</span><span class="sxs-lookup"><span data-stu-id="9dddb-130">Verbosity</span></span> | <span data-ttu-id="9dddb-131">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="9dddb-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="9dddb-132">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="9dddb-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="9dddb-133">使用例</span><span class="sxs-lookup"><span data-stu-id="9dddb-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
