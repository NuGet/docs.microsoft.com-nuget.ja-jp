---
title: NuGet PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで利用できる PowerShell コマンドの完全な参照です。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: ba9f5dc2b570298d9011f62a081631ec31623701
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817004"
---
# <a name="powershell-reference"></a><span data-ttu-id="d3ca2-103">PowerShell リファレンス</span><span class="sxs-lookup"><span data-stu-id="d3ca2-103">PowerShell reference</span></span>

<span data-ttu-id="d3ca2-104">パッケージ マネージャー コンソールは、以下に示す特定のコマンドを使用して NuGet を使って操作する Windows 上の Visual Studio 内での PowerShell インターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="d3ca2-105">(コンソールは Visual Studio for mac で現在使用できません)コンソールの使用にについては、次を参照してください。、 [Package Manager Console](../tools/package-manager-console.md)トピックです。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="d3ca2-106">すべての PowerShell コマンドは、パッケージの消費量にのみ関連します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="d3ca2-107">PowerShell コマンドは、作成、およびパッケージには、他のパッケージのコンシューマーことができます。 その範囲内に以外のパッケージを公開には関連ありません。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="d3ca2-108">ここに示すコマンドは、Visual Studio で、パッケージ マネージャー コンソールに固有とは異なる、[パッケージ管理モジュールのコマンド](/powershell/module/packagemanagement/?view=powershell-6)一般的な PowerShell 環境で使用可能なことです。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="d3ca2-109">具体的には、各環境には、他のでは使用できないコマンドと同じ名前のコマンドは特定の引数も異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="d3ca2-110">Visual Studio でパッケージの管理コンソールを使用すると、コマンドと引数のこのトピックに記載されていますが適用されます。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="d3ca2-111">一般的なコマンド</span><span class="sxs-lookup"><span data-stu-id="d3ca2-111">Common Commands</span></span> | <span data-ttu-id="d3ca2-112">説明</span><span class="sxs-lookup"><span data-stu-id="d3ca2-112">Description</span></span> | <span data-ttu-id="d3ca2-113">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="d3ca2-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="d3ca2-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="d3ca2-114">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="d3ca2-115">プロジェクトにパッケージとその依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="d3ca2-116">すべて</span><span class="sxs-lookup"><span data-stu-id="d3ca2-116">All</span></span> |
| [<span data-ttu-id="d3ca2-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="d3ca2-117">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="d3ca2-118">パッケージとその依存関係またはプロジェクト内のすべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="d3ca2-119">すべて</span><span class="sxs-lookup"><span data-stu-id="d3ca2-119">All</span></span> |
| [<span data-ttu-id="d3ca2-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="d3ca2-120">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="d3ca2-121">パッケージ ID またはキーワードを使用して、パッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="d3ca2-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="d3ca2-122">3.0+</span></span> |
| [<span data-ttu-id="d3ca2-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="d3ca2-123">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="d3ca2-124">ローカル リポジトリにインストールされているパッケージの一覧を取得またはパッケージ ソースから使用可能なパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="d3ca2-125">すべて</span><span class="sxs-lookup"><span data-stu-id="d3ca2-125">All</span></span> |

| <span data-ttu-id="d3ca2-126">セカンダリ コマンド</span><span class="sxs-lookup"><span data-stu-id="d3ca2-126">Secondary Commands</span></span> | <span data-ttu-id="d3ca2-127">説明</span><span class="sxs-lookup"><span data-stu-id="d3ca2-127">Description</span></span> | <span data-ttu-id="d3ca2-128">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="d3ca2-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="d3ca2-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="d3ca2-129">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="d3ca2-130">プロジェクトの出力パス内のすべてのアセンブリを調べ、バインド リダイレクトを追加、`app.config`または`web.config`必要な場合です。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="d3ca2-131">すべて</span><span class="sxs-lookup"><span data-stu-id="d3ca2-131">All</span></span> |
| [<span data-ttu-id="d3ca2-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="d3ca2-132">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="d3ca2-133">既定値または指定したプロジェクトについての情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="d3ca2-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="d3ca2-134">3.0+</span></span> |
| [<span data-ttu-id="d3ca2-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="d3ca2-135">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="d3ca2-136">プロジェクト、ライセンス、または指定したパッケージの不正使用を URL のレポートで既定のブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="d3ca2-137">3.0 以降で廃止されました</span><span class="sxs-lookup"><span data-stu-id="d3ca2-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="d3ca2-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="d3ca2-138">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="d3ca2-139">一般的に使用されるパラメーター値では、カスタマイズされた展開を作成することができます、コマンドのパラメーターにタブ拡張を登録します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="d3ca2-140">すべて</span><span class="sxs-lookup"><span data-stu-id="d3ca2-140">All</span></span> |
| [<span data-ttu-id="d3ca2-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="d3ca2-141">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="d3ca2-142">バージョンがインストール パッケージから取得では、プロジェクトを指定し、ソリューション内のプロジェクトの残りの部分のバージョンを同期します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="d3ca2-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="d3ca2-143">3.0+</span></span> |
| [<span data-ttu-id="d3ca2-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="d3ca2-144">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="d3ca2-145">必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="d3ca2-146">すべて</span><span class="sxs-lookup"><span data-stu-id="d3ca2-146">All</span></span> |

<span data-ttu-id="d3ca2-147">コンソール内でこれらのコマンドのいずれかを完全かつ詳細なヘルプ、だけ対象のコマンド名を持つ、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="d3ca2-148">パッケージ マネージャー コンソールのすべてのコマンドは、次をサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="d3ca2-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="d3ca2-149">デバッグ</span><span class="sxs-lookup"><span data-stu-id="d3ca2-149">Debug</span></span>
- <span data-ttu-id="d3ca2-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="d3ca2-150">ErrorAction</span></span>
- <span data-ttu-id="d3ca2-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="d3ca2-151">ErrorVariable</span></span>
- <span data-ttu-id="d3ca2-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="d3ca2-152">OutBuffer</span></span>
- <span data-ttu-id="d3ca2-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="d3ca2-153">OutVariable</span></span>
- <span data-ttu-id="d3ca2-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="d3ca2-154">PipelineVariable</span></span>
- <span data-ttu-id="d3ca2-155">詳細</span><span class="sxs-lookup"><span data-stu-id="d3ca2-155">Verbose</span></span>
- <span data-ttu-id="d3ca2-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="d3ca2-156">WarningAction</span></span>
- <span data-ttu-id="d3ca2-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="d3ca2-157">WarningVariable</span></span>

<span data-ttu-id="d3ca2-158">詳細についてを参照してください[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell ドキュメントにします。</span><span class="sxs-lookup"><span data-stu-id="d3ca2-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
