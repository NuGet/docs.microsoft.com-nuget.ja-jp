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
ms.openlocfilehash: 80b8f9a3b74030ffd3f1c7b784204d98be67d684
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="02c40-104">[ミラー] (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="02c40-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="02c40-105">**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:** 3.2 以降で廃止されました</span><span class="sxs-lookup"><span data-stu-id="02c40-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="02c40-106">パッケージとターゲットのリポジトリに指定されたソース リポジトリからその依存関係を反映します。</span><span class="sxs-lookup"><span data-stu-id="02c40-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="02c40-107">このコマンドは、NuGet のバージョン 3.2 の前に有効にするには[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)を最新の安定版リリースを選択し、ダウンロード`NuGet.ServerExtensions.dll`と`Nuget-Signed.exe`、ローカル ディスクと名前の変更に`Nuget-Signed.exe`に`nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="02c40-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="02c40-108">使用法</span><span class="sxs-lookup"><span data-stu-id="02c40-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="02c40-109">ここで`<packageID>`をミラー化すると、パッケージまたは`<configFilePath>`を識別、`packages.config`をミラー化するパッケージの一覧を含むファイルです。</span><span class="sxs-lookup"><span data-stu-id="02c40-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="02c40-110">`<listUrlTarget>`ソース リポジトリを指定し、`<publishUrlTarget>`ターゲットのリポジトリを指定します。</span><span class="sxs-lookup"><span data-stu-id="02c40-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="02c40-111">場合は、ターゲットのリポジトリ`https://machine/repo`を実行している[NuGet.Server](../hosting-packages/nuget-server.md)、リストとプッシュ url になります`https://machine/repo/nuget`と`https://machine/repo/api/v2/package`、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="02c40-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="02c40-112">オプション</span><span class="sxs-lookup"><span data-stu-id="02c40-112">Options</span></span>

| <span data-ttu-id="02c40-113">オプション</span><span class="sxs-lookup"><span data-stu-id="02c40-113">Option</span></span> | <span data-ttu-id="02c40-114">説明</span><span class="sxs-lookup"><span data-stu-id="02c40-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="02c40-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="02c40-115">ApiKey</span></span> | <span data-ttu-id="02c40-116">ターゲットのリポジトリの API キー。</span><span class="sxs-lookup"><span data-stu-id="02c40-116">The API key for the target repository.</span></span> <span data-ttu-id="02c40-117">存在しない場合、いずれかで指定されている*%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="02c40-117">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="02c40-118">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="02c40-118">Help</span></span> | <span data-ttu-id="02c40-119">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="02c40-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="02c40-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="02c40-120">NoCache</span></span> | <span data-ttu-id="02c40-121">NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="02c40-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="02c40-122">noop</span><span class="sxs-lookup"><span data-stu-id="02c40-122">Noop</span></span> | <span data-ttu-id="02c40-123">新機能が不要になる行いません; 操作をログに記録します。プッシュ操作に成功した場合を想定しています。</span><span class="sxs-lookup"><span data-stu-id="02c40-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="02c40-124">PreRelease</span><span class="sxs-lookup"><span data-stu-id="02c40-124">PreRelease</span></span> | <span data-ttu-id="02c40-125">ミラーリングの操作では、プレリリースのパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="02c40-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="02c40-126">ソース</span><span class="sxs-lookup"><span data-stu-id="02c40-126">Source</span></span> | <span data-ttu-id="02c40-127">ミラー化するパッケージ ソースの一覧です。</span><span class="sxs-lookup"><span data-stu-id="02c40-127">A list of package sources to mirror.</span></span> <span data-ttu-id="02c40-128">ものがで定義されているソースが指定されていない場合*%AppData%\NuGet\NuGet.Config*が使用すると、指定がない場合は、nuget.org を既定とします。</span><span class="sxs-lookup"><span data-stu-id="02c40-128">If no sources are specified, the ones defined in *%AppData%\NuGet\NuGet.Config* are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="02c40-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="02c40-129">Timeout</span></span> | <span data-ttu-id="02c40-130">(秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。</span><span class="sxs-lookup"><span data-stu-id="02c40-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="02c40-131">既定では 300 秒 (5 分) です。</span><span class="sxs-lookup"><span data-stu-id="02c40-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="02c40-132">Version</span><span class="sxs-lookup"><span data-stu-id="02c40-132">Version</span></span> | <span data-ttu-id="02c40-133">インストールするパッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="02c40-133">The version of the package to install.</span></span> <span data-ttu-id="02c40-134">指定しない場合、最新バージョンがミラー化されます。</span><span class="sxs-lookup"><span data-stu-id="02c40-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="02c40-135">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="02c40-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="02c40-136">使用例</span><span class="sxs-lookup"><span data-stu-id="02c40-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
