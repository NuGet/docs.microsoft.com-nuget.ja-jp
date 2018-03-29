---
title: NuGet CLI ミラー コマンド |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe ミラー コマンドのリファレンス
keywords: nuget ミラー参照、ミラー コマンドです。
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="2d0e0-104">[ミラー] (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2d0e0-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="2d0e0-105">**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:** 3.2 以降で廃止されました</span><span class="sxs-lookup"><span data-stu-id="2d0e0-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="2d0e0-106">パッケージとターゲットのリポジトリに指定されたソース リポジトリからその依存関係を反映します。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="2d0e0-107">このコマンドは、NuGet のバージョン 3.2 の前に有効にするには[ https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)を最新の安定版リリースを選択し、ダウンロード`NuGet.ServerExtensions.dll`と`Nuget-Signed.exe`、ローカル ディスクと名前の変更に`Nuget-Signed.exe`に`nuget.exe`。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="2d0e0-108">使用法</span><span class="sxs-lookup"><span data-stu-id="2d0e0-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="2d0e0-109">ここで`<packageID>`をミラー化すると、パッケージまたは`<configFilePath>`を識別、`packages.config`をミラー化するパッケージの一覧を含むファイルです。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="2d0e0-110">`<listUrlTarget>`ソース リポジトリを指定し、`<publishUrlTarget>`ターゲットのリポジトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="2d0e0-111">場合は、ターゲットのリポジトリ`https://machine/repo`を実行している[NuGet.Server](../hosting-packages/nuget-server.md)、リストとプッシュ url になります`https://machine/repo/nuget`と`https://machine/repo/api/v2/package`、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="2d0e0-112">オプション</span><span class="sxs-lookup"><span data-stu-id="2d0e0-112">Options</span></span>

| <span data-ttu-id="2d0e0-113">オプション</span><span class="sxs-lookup"><span data-stu-id="2d0e0-113">Option</span></span> | <span data-ttu-id="2d0e0-114">説明</span><span class="sxs-lookup"><span data-stu-id="2d0e0-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2d0e0-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="2d0e0-115">ApiKey</span></span> | <span data-ttu-id="2d0e0-116">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-116">The API key for the target repository.</span></span> <span data-ttu-id="2d0e0-117">かどうか、存在していない構成ファイルで指定した期間が使用 (`%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux))。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="2d0e0-118">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="2d0e0-118">Help</span></span> | <span data-ttu-id="2d0e0-119">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="2d0e0-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="2d0e0-120">NoCache</span></span> | <span data-ttu-id="2d0e0-121">NuGet がキャッシュされているパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="2d0e0-122">参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="2d0e0-123">noop</span><span class="sxs-lookup"><span data-stu-id="2d0e0-123">Noop</span></span> | <span data-ttu-id="2d0e0-124">新機能が不要になる行いません; 操作をログに記録します。プッシュ操作に成功した場合を想定しています。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="2d0e0-125">PreRelease</span><span class="sxs-lookup"><span data-stu-id="2d0e0-125">PreRelease</span></span> | <span data-ttu-id="2d0e0-126">ミラーリングの操作では、プレリリースのパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="2d0e0-127">ソース</span><span class="sxs-lookup"><span data-stu-id="2d0e0-127">Source</span></span> | <span data-ttu-id="2d0e0-128">ミラー化するパッケージ ソースの一覧です。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-128">A list of package sources to mirror.</span></span> <span data-ttu-id="2d0e0-129">ものがで定義されているソースが指定されていない場合 nuget.org に既定の指定がない場合、構成ファイルを使用、(ApiKey 上記を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="2d0e0-130">Timeout</span><span class="sxs-lookup"><span data-stu-id="2d0e0-130">Timeout</span></span> | <span data-ttu-id="2d0e0-131">(秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="2d0e0-132">既定では 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="2d0e0-133">Version</span><span class="sxs-lookup"><span data-stu-id="2d0e0-133">Version</span></span> | <span data-ttu-id="2d0e0-134">インストールするパッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-134">The version of the package to install.</span></span> <span data-ttu-id="2d0e0-135">指定しない場合、最新バージョンがミラー化されます。</span><span class="sxs-lookup"><span data-stu-id="2d0e0-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="2d0e0-136">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2d0e0-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2d0e0-137">使用例</span><span class="sxs-lookup"><span data-stu-id="2d0e0-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
