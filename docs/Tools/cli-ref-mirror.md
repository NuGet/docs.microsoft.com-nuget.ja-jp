---
title: "NuGet CLI ミラー コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Nuget.exe ミラー コマンドのリファレンス"
keywords: "nuget ミラー参照、ミラー コマンドです。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="3b962-104">[ミラー] (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="3b962-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="3b962-105">**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:** 3.2 以降で廃止されました</span><span class="sxs-lookup"><span data-stu-id="3b962-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="3b962-106">パッケージとターゲットのリポジトリに指定されたソース リポジトリからその依存関係を反映します。</span><span class="sxs-lookup"><span data-stu-id="3b962-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="3b962-107">このコマンドは、NuGet のバージョン 3.2 の前に有効にするには[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)を最新の安定版リリースを選択し、ダウンロード`NuGet.ServerExtensions.dll`と`Nuget-Signed.exe`、ローカル ディスクと名前の変更に`Nuget-Signed.exe`に`nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="3b962-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="3b962-108">使用方法</span><span class="sxs-lookup"><span data-stu-id="3b962-108">Usage</span></span>

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="3b962-109">ここで`<packageID>`をミラー化すると、パッケージまたは`<configFilePath>`を識別、`packages.config`をミラー化するパッケージの一覧を含むファイルです。</span><span class="sxs-lookup"><span data-stu-id="3b962-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="3b962-110">`<listUrlTarget>`ソース リポジトリを指定し、`<publishUrlTarget>`ターゲットのリポジトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="3b962-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="3b962-111">場合は、ターゲットのリポジトリ`https://machine/repo`を実行している[NuGet.Server](../hosting-packages/NuGet-Server.md)、リストとプッシュ url になります`https://machine/repo/nuget`と`https://machine/repo/api/v2/package`、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="3b962-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/NuGet-Server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="3b962-112">オプション</span><span class="sxs-lookup"><span data-stu-id="3b962-112">Options</span></span>

| <span data-ttu-id="3b962-113">オプション</span><span class="sxs-lookup"><span data-stu-id="3b962-113">Option</span></span> | <span data-ttu-id="3b962-114">説明</span><span class="sxs-lookup"><span data-stu-id="3b962-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3b962-115">apiKey</span><span class="sxs-lookup"><span data-stu-id="3b962-115">ApiKey</span></span> | <span data-ttu-id="3b962-116">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="3b962-116">The API key for the target repository.</span></span> <span data-ttu-id="3b962-117">存在しない場合、いずれかで指定されている*%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="3b962-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="3b962-118">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="3b962-118">Help</span></span> | <span data-ttu-id="3b962-119">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="3b962-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="3b962-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="3b962-120">NoCache</span></span> | <span data-ttu-id="3b962-121">NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="3b962-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="3b962-122">noop</span><span class="sxs-lookup"><span data-stu-id="3b962-122">Noop</span></span> | <span data-ttu-id="3b962-123">新機能が不要になる行いません; 操作をログに記録します。プッシュ操作に成功した場合を想定しています。</span><span class="sxs-lookup"><span data-stu-id="3b962-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="3b962-124">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="3b962-124">PreRelease</span></span> | <span data-ttu-id="3b962-125">ミラーリングの操作では、プレリリースのパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3b962-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="3b962-126">ソース</span><span class="sxs-lookup"><span data-stu-id="3b962-126">Source</span></span> | <span data-ttu-id="3b962-127">ミラー化するパッケージ ソースの一覧です。</span><span class="sxs-lookup"><span data-stu-id="3b962-127">A list of package sources to mirror.</span></span> <span data-ttu-id="3b962-128">ものがで定義されているソースが指定されていない場合*%AppData%\NuGet\NuGet.Config*が使用すると、指定がない場合は、nuget.org を既定とします。</span><span class="sxs-lookup"><span data-stu-id="3b962-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="3b962-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="3b962-129">Timeout</span></span> | <span data-ttu-id="3b962-130">(秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。</span><span class="sxs-lookup"><span data-stu-id="3b962-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="3b962-131">既定では 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="3b962-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="3b962-132">Version</span><span class="sxs-lookup"><span data-stu-id="3b962-132">Version</span></span> | <span data-ttu-id="3b962-133">インストールするパッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="3b962-133">The version of the package to install.</span></span> <span data-ttu-id="3b962-134">指定しない場合、最新バージョンがミラー化されます。</span><span class="sxs-lookup"><span data-stu-id="3b962-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="3b962-135">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3b962-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3b962-136">例</span><span class="sxs-lookup"><span data-stu-id="3b962-136">Examples</span></span>

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
