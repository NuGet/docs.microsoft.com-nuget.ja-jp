---
title: NuGet CLI ミラーコマンド
description: Nuget.exe mirror コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327669"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="061d1-103">mirror コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="061d1-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="061d1-104">**適用対象:** パッケージ発行&bullet;が**サポートされているバージョン:** 3.2 以降では非推奨です。</span><span class="sxs-lookup"><span data-stu-id="061d1-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="061d1-105">指定されたソースリポジトリからターゲットリポジトリにパッケージとその依存関係をミラー化します。</span><span class="sxs-lookup"><span data-stu-id="061d1-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="061d1-106">3\.2 より前のバージョンの NuGet でこのコマンドを有効[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)にするには、にアクセスして`Nuget-Signed.exe` 最新の安定版リリースを選択し、をダウンロードしてローカルディスクにダウンロード`NuGet.ServerExtensions.dll` し、名前をに`nuget.exe` 変更`Nuget-Signed.exe` します。</span><span class="sxs-lookup"><span data-stu-id="061d1-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="061d1-107">使用法</span><span class="sxs-lookup"><span data-stu-id="061d1-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="061d1-108">は、ミラー化するパッケージ、また`<configFilePath>`はミラー `packages.config`化するパッケージの一覧を示すファイルを指定します。 `<packageID>`</span><span class="sxs-lookup"><span data-stu-id="061d1-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="061d1-109">は`<listUrlTarget>`ソースリポジトリ`<publishUrlTarget>`を指定し、はターゲットリポジトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="061d1-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="061d1-110">ターゲットリポジトリが、 [NuGet](../../hosting-packages/nuget-server.md)を`https://machine/repo`実行しているである場合、リストと`https://machine/repo/nuget`プッシュ url はそれぞれと`https://machine/repo/api/v2/package`になります。</span><span class="sxs-lookup"><span data-stu-id="061d1-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="061d1-111">オプション</span><span class="sxs-lookup"><span data-stu-id="061d1-111">Options</span></span>

| <span data-ttu-id="061d1-112">オプション</span><span class="sxs-lookup"><span data-stu-id="061d1-112">Option</span></span> | <span data-ttu-id="061d1-113">説明</span><span class="sxs-lookup"><span data-stu-id="061d1-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="061d1-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="061d1-114">ApiKey</span></span> | <span data-ttu-id="061d1-115">ターゲットリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="061d1-115">The API key for the target repository.</span></span> <span data-ttu-id="061d1-116">存在しない場合は、構成ファイルで指定されている`%AppData%\NuGet\NuGet.Config`ものが使用さ`~/.nuget/NuGet/NuGet.Config`れます ((Windows) または (Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="061d1-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="061d1-117">Help</span><span class="sxs-lookup"><span data-stu-id="061d1-117">Help</span></span> | <span data-ttu-id="061d1-118">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="061d1-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="061d1-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="061d1-119">NoCache</span></span> | <span data-ttu-id="061d1-120">NuGet がキャッシュされたパッケージを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="061d1-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="061d1-121">「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="061d1-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="061d1-122">Noop</span><span class="sxs-lookup"><span data-stu-id="061d1-122">Noop</span></span> | <span data-ttu-id="061d1-123">実行される処理をログに記録しますが、アクションは実行しません。プッシュ操作の成功を想定します。</span><span class="sxs-lookup"><span data-stu-id="061d1-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="061d1-124">PreRelease</span><span class="sxs-lookup"><span data-stu-id="061d1-124">PreRelease</span></span> | <span data-ttu-id="061d1-125">ミラーリング操作にプレリリースパッケージを含めます。</span><span class="sxs-lookup"><span data-stu-id="061d1-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="061d1-126">Source</span><span class="sxs-lookup"><span data-stu-id="061d1-126">Source</span></span> | <span data-ttu-id="061d1-127">ミラー化するパッケージソースの一覧。</span><span class="sxs-lookup"><span data-stu-id="061d1-127">A list of package sources to mirror.</span></span> <span data-ttu-id="061d1-128">ソースが指定されていない場合は、構成ファイルで定義されているもの (上記の ApiKey を参照) が使用され、何も指定されていない場合は nuget.org が既定値となります。</span><span class="sxs-lookup"><span data-stu-id="061d1-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="061d1-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="061d1-129">Timeout</span></span> | <span data-ttu-id="061d1-130">サーバーにプッシュするときのタイムアウトを秒単位で指定します。</span><span class="sxs-lookup"><span data-stu-id="061d1-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="061d1-131">既定値は300秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="061d1-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="061d1-132">Version</span><span class="sxs-lookup"><span data-stu-id="061d1-132">Version</span></span> | <span data-ttu-id="061d1-133">インストールするパッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="061d1-133">The version of the package to install.</span></span> <span data-ttu-id="061d1-134">指定しない場合、最新バージョンがミラー化されます。</span><span class="sxs-lookup"><span data-stu-id="061d1-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="061d1-135">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="061d1-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="061d1-136">使用例</span><span class="sxs-lookup"><span data-stu-id="061d1-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
