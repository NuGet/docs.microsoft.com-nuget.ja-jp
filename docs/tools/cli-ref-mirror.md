---
title: ミラーの NuGet CLI コマンド
description: Nuget.exe のミラー コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550207"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="c01a3-103">mirror コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="c01a3-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="c01a3-104">**適用対象:** パッケージの発行&bullet;**サポートされているバージョン:** 3.2 + で非推奨とされます</span><span class="sxs-lookup"><span data-stu-id="c01a3-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="c01a3-105">パッケージをターゲットのリポジトリを指定したソース リポジトリからその依存関係をミラー化します。</span><span class="sxs-lookup"><span data-stu-id="c01a3-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="c01a3-106">このコマンドは、NuGet のバージョン 3.2 の前に有効にするには[ https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)ダウンロード、最新の安定版リリースを選択`NuGet.ServerExtensions.dll` と`Nuget-Signed.exe` と、ローカル ディスクと名前の変更を`Nuget-Signed.exe` に`nuget.exe` 。</span><span class="sxs-lookup"><span data-stu-id="c01a3-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="c01a3-107">使用法</span><span class="sxs-lookup"><span data-stu-id="c01a3-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="c01a3-108">場所`<packageID>`を反映するには、パッケージまたは`<configFilePath>`識別、`packages.config`ミラー化するパッケージを一覧するファイル。</span><span class="sxs-lookup"><span data-stu-id="c01a3-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="c01a3-109">`<listUrlTarget>` 、ソース リポジトリを指定し、`<publishUrlTarget>`ターゲット リポジトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="c01a3-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="c01a3-110">ターゲットのリポジトリがある場合`https://machine/repo`を実行している[NuGet.Server](../hosting-packages/nuget-server.md)、リストとプッシュの url になります`https://machine/repo/nuget`と`https://machine/repo/api/v2/package`、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="c01a3-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="c01a3-111">オプション</span><span class="sxs-lookup"><span data-stu-id="c01a3-111">Options</span></span>

| <span data-ttu-id="c01a3-112">オプション</span><span class="sxs-lookup"><span data-stu-id="c01a3-112">Option</span></span> | <span data-ttu-id="c01a3-113">説明</span><span class="sxs-lookup"><span data-stu-id="c01a3-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c01a3-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="c01a3-114">ApiKey</span></span> | <span data-ttu-id="c01a3-115">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="c01a3-115">The API key for the target repository.</span></span> <span data-ttu-id="c01a3-116">かどうか、存在していない、構成ファイルで指定された 1 つが使用されます (`%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux))。</span><span class="sxs-lookup"><span data-stu-id="c01a3-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="c01a3-117">Help</span><span class="sxs-lookup"><span data-stu-id="c01a3-117">Help</span></span> | <span data-ttu-id="c01a3-118">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="c01a3-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="c01a3-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="c01a3-119">NoCache</span></span> | <span data-ttu-id="c01a3-120">NuGet がキャッシュされたパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="c01a3-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="c01a3-121">参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。</span><span class="sxs-lookup"><span data-stu-id="c01a3-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="c01a3-122">Noop</span><span class="sxs-lookup"><span data-stu-id="c01a3-122">Noop</span></span> | <span data-ttu-id="c01a3-123">ログに記録内容が行いますが、アクションは行われませんプッシュ操作の成功を前提としています。</span><span class="sxs-lookup"><span data-stu-id="c01a3-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="c01a3-124">PreRelease</span><span class="sxs-lookup"><span data-stu-id="c01a3-124">PreRelease</span></span> | <span data-ttu-id="c01a3-125">ミラーリングの操作では、プレリリース パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c01a3-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="c01a3-126">Source</span><span class="sxs-lookup"><span data-stu-id="c01a3-126">Source</span></span> | <span data-ttu-id="c01a3-127">ミラー化するパッケージ ソースの一覧。</span><span class="sxs-lookup"><span data-stu-id="c01a3-127">A list of package sources to mirror.</span></span> <span data-ttu-id="c01a3-128">定義されているソースが指定されていない場合が指定されていない場合、nuget.org を既定値、構成ファイルが使用されます (ApiKey 上記を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="c01a3-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="c01a3-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="c01a3-129">Timeout</span></span> | <span data-ttu-id="c01a3-130">サーバーにプッシュするための秒単位のタイムアウトを指定します。</span><span class="sxs-lookup"><span data-stu-id="c01a3-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="c01a3-131">既定では 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="c01a3-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="c01a3-132">Version</span><span class="sxs-lookup"><span data-stu-id="c01a3-132">Version</span></span> | <span data-ttu-id="c01a3-133">インストールするパッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="c01a3-133">The version of the package to install.</span></span> <span data-ttu-id="c01a3-134">指定しない場合、最新のバージョンがミラー化します。</span><span class="sxs-lookup"><span data-stu-id="c01a3-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="c01a3-135">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c01a3-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c01a3-136">使用例</span><span class="sxs-lookup"><span data-stu-id="c01a3-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
