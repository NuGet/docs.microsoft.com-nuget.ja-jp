---
title: NuGet CLI ミラーコマンド
description: nuget.exe mirror コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a7247aeb21418e78dbfe9be15c2e7cd152aa3f4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622968"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="61d99-103">mirror コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="61d99-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="61d99-104">**適用対象:** パッケージ発行が &bullet; **サポートされているバージョン:** 3.2 以降では非推奨です。</span><span class="sxs-lookup"><span data-stu-id="61d99-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="61d99-105">指定されたソースリポジトリからターゲットリポジトリにパッケージとその依存関係をミラー化します。</span><span class="sxs-lookup"><span data-stu-id="61d99-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="61d99-106">以前に NuGet 2.x でこのコマンドをサポートしていた NuGet.ServerExtensions.dll と NuGet-Signed.exe (NuGet-Signed.exe 名前を nuget.exe に変更) は、ダウンロードできなくなりました。</span><span class="sxs-lookup"><span data-stu-id="61d99-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="61d99-107">このようなコマンドを使用するには、 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)を試してください。</span><span class="sxs-lookup"><span data-stu-id="61d99-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="61d99-108">使用法</span><span class="sxs-lookup"><span data-stu-id="61d99-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="61d99-109">`<packageID>`は、ミラー化するパッケージ、または `<configFilePath>` ミラー化 `packages.config` するパッケージの一覧を示すファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="61d99-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="61d99-110">は `<listUrlTarget>` ソースリポジトリを指定し、は `<publishUrlTarget>` ターゲットリポジトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="61d99-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="61d99-111">ターゲットリポジトリが、NuGet を実行しているである場合 `https://machine/repo` 、リストとプッシュ url は[NuGet.Server](../../hosting-packages/nuget-server.md) `https://machine/repo/nuget` それぞれと `https://machine/repo/api/v2/package` になります。</span><span class="sxs-lookup"><span data-stu-id="61d99-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="61d99-112">Options</span><span class="sxs-lookup"><span data-stu-id="61d99-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="61d99-113">ターゲットリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="61d99-113">The API key for the target repository.</span></span> <span data-ttu-id="61d99-114">存在しない場合は、構成ファイルで指定されているものが使用され `%AppData%\NuGet\NuGet.Config` ます ((Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux))。</span><span class="sxs-lookup"><span data-stu-id="61d99-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="61d99-115">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="61d99-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="61d99-116">NuGet がキャッシュされたパッケージを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="61d99-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="61d99-117">「 [グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="61d99-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="61d99-118">実行される処理をログに記録しますが、アクションは実行しません。プッシュ操作の成功を想定します。</span><span class="sxs-lookup"><span data-stu-id="61d99-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="61d99-119">ミラーリング操作にプレリリースパッケージを含めます。</span><span class="sxs-lookup"><span data-stu-id="61d99-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="61d99-120">ミラー化するパッケージソースの一覧。</span><span class="sxs-lookup"><span data-stu-id="61d99-120">A list of package sources to mirror.</span></span> <span data-ttu-id="61d99-121">ソースが指定されていない場合は、構成ファイルで定義されているもの (上記の ApiKey を参照) が使用され、何も指定されていない場合は nuget.org が既定値となります。</span><span class="sxs-lookup"><span data-stu-id="61d99-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="61d99-122">サーバーにプッシュするときのタイムアウトを秒単位で指定します。</span><span class="sxs-lookup"><span data-stu-id="61d99-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="61d99-123">設定値の既定は 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="61d99-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="61d99-124">インストールするパッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="61d99-124">The version of the package to install.</span></span> <span data-ttu-id="61d99-125">指定しない場合、最新バージョンがミラー化されます。</span><span class="sxs-lookup"><span data-stu-id="61d99-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="61d99-126">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="61d99-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="61d99-127">使用例</span><span class="sxs-lookup"><span data-stu-id="61d99-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
