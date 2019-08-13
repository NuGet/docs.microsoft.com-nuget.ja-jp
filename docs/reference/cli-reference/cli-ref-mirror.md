---
title: NuGet CLI の mirror コマンド
description: Nuget.exe mirror コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959710"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="93ec4-103">mirror コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="93ec4-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="93ec4-104">**適用対象:** パッケージ発行&bullet;が**サポートされているバージョン:** 3.2 以降では非推奨です。</span><span class="sxs-lookup"><span data-stu-id="93ec4-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="93ec4-105">指定されたソースリポジトリからターゲットリポジトリにパッケージとその依存関係をミラー化します。</span><span class="sxs-lookup"><span data-stu-id="93ec4-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="93ec4-106">Nuget 2.x で以前にこのコマンドをサポートしていた Nuget.exe と NuGet-Signed (NuGet-Signed を nuget.exe に変更することによって) は、ダウンロードできなくなりました。</span><span class="sxs-lookup"><span data-stu-id="93ec4-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="93ec4-107">このようなコマンドを使用するには、 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)を試してください。</span><span class="sxs-lookup"><span data-stu-id="93ec4-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="93ec4-108">使用法</span><span class="sxs-lookup"><span data-stu-id="93ec4-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="93ec4-109">は、ミラー化するパッケージ、また`<configFilePath>`はミラー `packages.config`化するパッケージの一覧を示すファイルを指定します。 `<packageID>`</span><span class="sxs-lookup"><span data-stu-id="93ec4-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="93ec4-110">は`<listUrlTarget>`ソースリポジトリ`<publishUrlTarget>`を指定し、はターゲットリポジトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="93ec4-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="93ec4-111">ターゲットリポジトリが、 [NuGet](../../hosting-packages/nuget-server.md)を`https://machine/repo`実行しているである場合、リストと`https://machine/repo/nuget`プッシュ url はそれぞれと`https://machine/repo/api/v2/package`になります。</span><span class="sxs-lookup"><span data-stu-id="93ec4-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="93ec4-112">オプション</span><span class="sxs-lookup"><span data-stu-id="93ec4-112">Options</span></span>

| <span data-ttu-id="93ec4-113">オプション</span><span class="sxs-lookup"><span data-stu-id="93ec4-113">Option</span></span> | <span data-ttu-id="93ec4-114">説明</span><span class="sxs-lookup"><span data-stu-id="93ec4-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="93ec4-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="93ec4-115">ApiKey</span></span> | <span data-ttu-id="93ec4-116">ターゲットリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="93ec4-116">The API key for the target repository.</span></span> <span data-ttu-id="93ec4-117">存在しない場合は、構成ファイルで指定されている`%AppData%\NuGet\NuGet.Config`ものが使用さ`~/.nuget/NuGet/NuGet.Config`れます ((Windows) または (Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="93ec4-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="93ec4-118">Help</span><span class="sxs-lookup"><span data-stu-id="93ec4-118">Help</span></span> | <span data-ttu-id="93ec4-119">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="93ec4-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="93ec4-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="93ec4-120">NoCache</span></span> | <span data-ttu-id="93ec4-121">NuGet がキャッシュされたパッケージを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="93ec4-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="93ec4-122">「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="93ec4-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="93ec4-123">Noop</span><span class="sxs-lookup"><span data-stu-id="93ec4-123">Noop</span></span> | <span data-ttu-id="93ec4-124">実行される処理をログに記録しますが、アクションは実行しません。プッシュ操作の成功を想定します。</span><span class="sxs-lookup"><span data-stu-id="93ec4-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="93ec4-125">PreRelease</span><span class="sxs-lookup"><span data-stu-id="93ec4-125">PreRelease</span></span> | <span data-ttu-id="93ec4-126">ミラーリング操作にプレリリースパッケージを含めます。</span><span class="sxs-lookup"><span data-stu-id="93ec4-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="93ec4-127">Source</span><span class="sxs-lookup"><span data-stu-id="93ec4-127">Source</span></span> | <span data-ttu-id="93ec4-128">ミラー化するパッケージソースの一覧。</span><span class="sxs-lookup"><span data-stu-id="93ec4-128">A list of package sources to mirror.</span></span> <span data-ttu-id="93ec4-129">ソースが指定されていない場合は、構成ファイルで定義されているもの (上記の ApiKey を参照) が使用され、何も指定されていない場合は nuget.org が既定値となります。</span><span class="sxs-lookup"><span data-stu-id="93ec4-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="93ec4-130">Timeout</span><span class="sxs-lookup"><span data-stu-id="93ec4-130">Timeout</span></span> | <span data-ttu-id="93ec4-131">サーバーにプッシュするときのタイムアウトを秒単位で指定します。</span><span class="sxs-lookup"><span data-stu-id="93ec4-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="93ec4-132">既定値は300秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="93ec4-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="93ec4-133">Version</span><span class="sxs-lookup"><span data-stu-id="93ec4-133">Version</span></span> | <span data-ttu-id="93ec4-134">インストールするパッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="93ec4-134">The version of the package to install.</span></span> <span data-ttu-id="93ec4-135">指定しない場合、最新バージョンがミラー化されます。</span><span class="sxs-lookup"><span data-stu-id="93ec4-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="93ec4-136">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="93ec4-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="93ec4-137">使用例</span><span class="sxs-lookup"><span data-stu-id="93ec4-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
