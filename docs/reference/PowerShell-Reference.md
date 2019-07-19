---
title: NuGet PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで使用できる PowerShell コマンドの完全なリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 142af9c4f7d25c3b0d986524313851cceb1e4c60
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327929"
---
# <a name="powershell-reference"></a><span data-ttu-id="680c5-103">PowerShell 参照</span><span class="sxs-lookup"><span data-stu-id="680c5-103">PowerShell reference</span></span>

<span data-ttu-id="680c5-104">パッケージマネージャーコンソールでは、Windows 上の Visual Studio 内で PowerShell インターフェイスを使用して、以下に示す特定のコマンドを使用して NuGet と対話します。</span><span class="sxs-lookup"><span data-stu-id="680c5-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="680c5-105">(コンソールは現在 Visual Studio for Mac では使用できません)。コンソールの使用ガイドについては、「[パッケージマネージャーコンソールを使用したパッケージのインストールと管理](../consume-packages/install-use-packages-powershell.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="680c5-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="680c5-106">すべての PowerShell コマンドは、パッケージの使用のみに関連しています。</span><span class="sxs-lookup"><span data-stu-id="680c5-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="680c5-107">パッケージが他のパッケージのコンシューマーでもある場合を除き、パッケージの作成と公開に関連する PowerShell コマンドはありません。</span><span class="sxs-lookup"><span data-stu-id="680c5-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="680c5-108">ここに記載されているコマンドは、Visual Studio のパッケージマネージャーコンソールに固有のものであり、一般的な PowerShell 環境で使用できる[Package Management モジュールコマンド](/powershell/module/packagemanagement/?view=powershell-6)とは異なります。</span><span class="sxs-lookup"><span data-stu-id="680c5-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="680c5-109">具体的には、各環境には、他の環境では使用できないコマンドがあり、同じ名前のコマンドが特定の引数で異なる場合もあります。</span><span class="sxs-lookup"><span data-stu-id="680c5-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="680c5-110">Visual Studio で Package Management コンソールを使用する場合は、このトピックに記載されているコマンドと引数が適用されます。</span><span class="sxs-lookup"><span data-stu-id="680c5-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="680c5-111">一般的なコマンド</span><span class="sxs-lookup"><span data-stu-id="680c5-111">Common Commands</span></span> | <span data-ttu-id="680c5-112">説明</span><span class="sxs-lookup"><span data-stu-id="680c5-112">Description</span></span> | <span data-ttu-id="680c5-113">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="680c5-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="680c5-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="680c5-114">Install-Package</span></span>](ps-reference/ps-ref-install-package.md) | <span data-ttu-id="680c5-115">パッケージとその依存関係をプロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="680c5-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="680c5-116">すべて</span><span class="sxs-lookup"><span data-stu-id="680c5-116">All</span></span> |
| [<span data-ttu-id="680c5-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="680c5-117">Update-Package</span></span>](ps-reference/ps-ref-update-package.md) | <span data-ttu-id="680c5-118">パッケージとその依存関係、またはプロジェクト内のすべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="680c5-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="680c5-119">すべて</span><span class="sxs-lookup"><span data-stu-id="680c5-119">All</span></span> |
| [<span data-ttu-id="680c5-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="680c5-120">Find-Package</span></span>](ps-reference/ps-ref-find-package.md) | <span data-ttu-id="680c5-121">パッケージ ID またはキーワードを使用してパッケージソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="680c5-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="680c5-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="680c5-122">3.0+</span></span> |
| [<span data-ttu-id="680c5-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="680c5-123">Get-Package</span></span>](ps-reference/ps-ref-get-package.md) | <span data-ttu-id="680c5-124">ローカルリポジトリにインストールされているパッケージの一覧を取得するか、パッケージソースから使用可能なパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="680c5-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="680c5-125">すべて</span><span class="sxs-lookup"><span data-stu-id="680c5-125">All</span></span> |

| <span data-ttu-id="680c5-126">セカンダリコマンド</span><span class="sxs-lookup"><span data-stu-id="680c5-126">Secondary Commands</span></span> | <span data-ttu-id="680c5-127">説明</span><span class="sxs-lookup"><span data-stu-id="680c5-127">Description</span></span> | <span data-ttu-id="680c5-128">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="680c5-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="680c5-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="680c5-129">Add-BindingRedirect</span></span>](ps-reference/ps-ref-add-bindingredirect.md) | <span data-ttu-id="680c5-130">プロジェクトの出力パス内のすべてのアセンブリを調べ、バインドリダイレクト`app.config`をまたはに追加します ( `web.config`必要な場合)。</span><span class="sxs-lookup"><span data-stu-id="680c5-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="680c5-131">すべて</span><span class="sxs-lookup"><span data-stu-id="680c5-131">All</span></span> |
| [<span data-ttu-id="680c5-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="680c5-132">Get-Project</span></span>](ps-reference/ps-ref-get-project.md) | <span data-ttu-id="680c5-133">既定のプロジェクトまたは指定されたプロジェクトに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="680c5-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="680c5-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="680c5-134">3.0+</span></span> |
| [<span data-ttu-id="680c5-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="680c5-135">Open-PackagePage</span></span>](ps-reference/ps-ref-open-packagepage.md) | <span data-ttu-id="680c5-136">指定されたパッケージのプロジェクト、ライセンス、またはレポート不正使用の URL を使用して、既定のブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="680c5-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="680c5-137">3\.0 以降では非推奨</span><span class="sxs-lookup"><span data-stu-id="680c5-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="680c5-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="680c5-138">Register-TabExpansion</span></span>](ps-reference/ps-ref-register-tabexpansion.md) | <span data-ttu-id="680c5-139">コマンドのパラメーターにタブ拡張を登録します。これにより、よく使用されるパラメーター値用にカスタマイズされた展開を作成できます。</span><span class="sxs-lookup"><span data-stu-id="680c5-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="680c5-140">すべて</span><span class="sxs-lookup"><span data-stu-id="680c5-140">All</span></span> |
| [<span data-ttu-id="680c5-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="680c5-141">Sync-Package</span></span>](ps-reference/ps-ref-sync-package.md) | <span data-ttu-id="680c5-142">指定したプロジェクトからインストールされているパッケージのバージョンを取得し、そのバージョンをソリューション内の残りのプロジェクトと同期します。</span><span class="sxs-lookup"><span data-stu-id="680c5-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="680c5-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="680c5-143">3.0+</span></span> |
| [<span data-ttu-id="680c5-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="680c5-144">Uninstall-Package</span></span>](ps-reference/ps-ref-uninstall-package.md) | <span data-ttu-id="680c5-145">プロジェクトからパッケージを削除し、必要に応じて依存関係を削除します。</span><span class="sxs-lookup"><span data-stu-id="680c5-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="680c5-146">すべて</span><span class="sxs-lookup"><span data-stu-id="680c5-146">All</span></span> |

<span data-ttu-id="680c5-147">コンソール内のこれらのコマンドの詳細なヘルプを表示するには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="680c5-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="680c5-148">すべてのパッケージマネージャーコンソールコマンドは、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="680c5-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="680c5-149">Debug</span><span class="sxs-lookup"><span data-stu-id="680c5-149">Debug</span></span>
- <span data-ttu-id="680c5-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="680c5-150">ErrorAction</span></span>
- <span data-ttu-id="680c5-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="680c5-151">ErrorVariable</span></span>
- <span data-ttu-id="680c5-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="680c5-152">OutBuffer</span></span>
- <span data-ttu-id="680c5-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="680c5-153">OutVariable</span></span>
- <span data-ttu-id="680c5-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="680c5-154">PipelineVariable</span></span>
- <span data-ttu-id="680c5-155">Verbose</span><span class="sxs-lookup"><span data-stu-id="680c5-155">Verbose</span></span>
- <span data-ttu-id="680c5-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="680c5-156">WarningAction</span></span>
- <span data-ttu-id="680c5-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="680c5-157">WarningVariable</span></span>

<span data-ttu-id="680c5-158">詳細については、PowerShell のドキュメントの[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="680c5-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
