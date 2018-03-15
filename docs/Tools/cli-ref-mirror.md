---
title: "NuGet CLI ミラー コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe ミラー コマンドのリファレンス"
keywords: "nuget ミラー参照、ミラー コマンドです。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c1969cc04b2e2cead5e9dadf9739fdabdf65f6c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="d51a5-104">[ミラー] (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d51a5-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="d51a5-105">**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:** 3.2 以降で廃止されました</span><span class="sxs-lookup"><span data-stu-id="d51a5-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="d51a5-106">パッケージとターゲットのリポジトリに指定されたソース リポジトリからその依存関係を反映します。</span><span class="sxs-lookup"><span data-stu-id="d51a5-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="d51a5-107">このコマンドは、NuGet のバージョン 3.2 の前に有効にするには[ https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)を最新の安定版リリースを選択し、ダウンロード`NuGet.ServerExtensions.dll`と`Nuget-Signed.exe`、ローカル ディスクと名前の変更に`Nuget-Signed.exe`に`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="d51a5-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="d51a5-108">使用法</span><span class="sxs-lookup"><span data-stu-id="d51a5-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="d51a5-109">ここで`<packageID>`をミラー化すると、パッケージまたは`<configFilePath>`を識別、`packages.config`をミラー化するパッケージの一覧を含むファイルです。</span><span class="sxs-lookup"><span data-stu-id="d51a5-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="d51a5-110">`<listUrlTarget>`ソース リポジトリを指定し、`<publishUrlTarget>`ターゲットのリポジトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="d51a5-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="d51a5-111">場合は、ターゲットのリポジトリ`https://machine/repo`を実行している[NuGet.Server](../hosting-packages/nuget-server.md)、リストとプッシュ url になります`https://machine/repo/nuget`と`https://machine/repo/api/v2/package`、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="d51a5-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="d51a5-112">オプション</span><span class="sxs-lookup"><span data-stu-id="d51a5-112">Options</span></span>

| <span data-ttu-id="d51a5-113">オプション</span><span class="sxs-lookup"><span data-stu-id="d51a5-113">Option</span></span> | <span data-ttu-id="d51a5-114">説明</span><span class="sxs-lookup"><span data-stu-id="d51a5-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d51a5-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="d51a5-115">ApiKey</span></span> | <span data-ttu-id="d51a5-116">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="d51a5-116">The API key for the target repository.</span></span> <span data-ttu-id="d51a5-117">かどうか、存在していない構成ファイルで指定した期間が使用 (`%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux))。</span><span class="sxs-lookup"><span data-stu-id="d51a5-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="d51a5-118">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="d51a5-118">Help</span></span> | <span data-ttu-id="d51a5-119">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d51a5-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="d51a5-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="d51a5-120">NoCache</span></span> | <span data-ttu-id="d51a5-121">NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="d51a5-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="d51a5-122">noop</span><span class="sxs-lookup"><span data-stu-id="d51a5-122">Noop</span></span> | <span data-ttu-id="d51a5-123">新機能が不要になる行いません; 操作をログに記録します。プッシュ操作に成功した場合を想定しています。</span><span class="sxs-lookup"><span data-stu-id="d51a5-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="d51a5-124">PreRelease</span><span class="sxs-lookup"><span data-stu-id="d51a5-124">PreRelease</span></span> | <span data-ttu-id="d51a5-125">ミラーリングの操作では、プレリリースのパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="d51a5-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="d51a5-126">ソース</span><span class="sxs-lookup"><span data-stu-id="d51a5-126">Source</span></span> | <span data-ttu-id="d51a5-127">ミラー化するパッケージ ソースの一覧です。</span><span class="sxs-lookup"><span data-stu-id="d51a5-127">A list of package sources to mirror.</span></span> <span data-ttu-id="d51a5-128">ものがで定義されているソースが指定されていない場合 nuget.org に既定の指定がない場合、構成ファイルを使用、(ApiKey 上記を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="d51a5-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="d51a5-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="d51a5-129">Timeout</span></span> | <span data-ttu-id="d51a5-130">(秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。</span><span class="sxs-lookup"><span data-stu-id="d51a5-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="d51a5-131">既定では 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="d51a5-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="d51a5-132">Version</span><span class="sxs-lookup"><span data-stu-id="d51a5-132">Version</span></span> | <span data-ttu-id="d51a5-133">インストールするパッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="d51a5-133">The version of the package to install.</span></span> <span data-ttu-id="d51a5-134">指定しない場合、最新バージョンがミラー化されます。</span><span class="sxs-lookup"><span data-stu-id="d51a5-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="d51a5-135">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d51a5-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d51a5-136">使用例</span><span class="sxs-lookup"><span data-stu-id="d51a5-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
