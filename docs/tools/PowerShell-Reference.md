---
title: NuGet PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで使用できる PowerShell コマンドの完全なリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 45c8be9956ceaab844bdcd89f1b96adc256f805c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546665"
---
# <a name="powershell-reference"></a><span data-ttu-id="95142-103">PowerShell リファレンス</span><span class="sxs-lookup"><span data-stu-id="95142-103">PowerShell reference</span></span>

<span data-ttu-id="95142-104">パッケージ マネージャー コンソールでは、以下に示す特定のコマンドを使用して、NuGet と対話する Windows 上の Visual Studio 内での PowerShell インターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="95142-104">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="95142-105">(コンソールは Visual Studio for mac で現在使用できません)コンソールの使用にガイドについては、次を参照してください。、[パッケージ マネージャー コンソール](../tools/package-manager-console.md)トピック。</span><span class="sxs-lookup"><span data-stu-id="95142-105">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="95142-106">すべての PowerShell コマンドは、パッケージの使用にのみ関連します。</span><span class="sxs-lookup"><span data-stu-id="95142-106">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="95142-107">作成とパッケージは、他のパッケージのコンシューマーをすることもできますを除くパッケージを公開する PowerShell コマンドが関係ありません。</span><span class="sxs-lookup"><span data-stu-id="95142-107">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="95142-108">ここに表示するコマンドは、Visual Studio でパッケージ マネージャー コンソールに固有でありとは異なる、[パッケージ管理モジュールのコマンド](/powershell/module/packagemanagement/?view=powershell-6)一般的な PowerShell 環境では使用できます。</span><span class="sxs-lookup"><span data-stu-id="95142-108">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="95142-109">具体的には、各環境には、その他では使用できないコマンドと同じ名前のコマンドも特定の引数は、異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="95142-109">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="95142-110">Visual Studio でのパッケージの管理コンソールを使用する場合、コマンドとこのトピックに記載されている引数が適用されます。</span><span class="sxs-lookup"><span data-stu-id="95142-110">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="95142-111">一般的なコマンド</span><span class="sxs-lookup"><span data-stu-id="95142-111">Common Commands</span></span> | <span data-ttu-id="95142-112">説明</span><span class="sxs-lookup"><span data-stu-id="95142-112">Description</span></span> | <span data-ttu-id="95142-113">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="95142-113">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="95142-114">Install-Package</span><span class="sxs-lookup"><span data-stu-id="95142-114">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="95142-115">プロジェクトにパッケージとその依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="95142-115">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="95142-116">すべて</span><span class="sxs-lookup"><span data-stu-id="95142-116">All</span></span> |
| [<span data-ttu-id="95142-117">Update-Package</span><span class="sxs-lookup"><span data-stu-id="95142-117">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="95142-118">パッケージとその依存関係、またはプロジェクト内のすべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="95142-118">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="95142-119">すべて</span><span class="sxs-lookup"><span data-stu-id="95142-119">All</span></span> |
| [<span data-ttu-id="95142-120">Find-Package</span><span class="sxs-lookup"><span data-stu-id="95142-120">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="95142-121">パッケージ ID またはキーワードを使用してパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="95142-121">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="95142-122">3.0+</span><span class="sxs-lookup"><span data-stu-id="95142-122">3.0+</span></span> |
| [<span data-ttu-id="95142-123">Get-Package</span><span class="sxs-lookup"><span data-stu-id="95142-123">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="95142-124">、ローカル リポジトリにインストールされているパッケージの一覧を取得またはパッケージのソースから使用可能なパッケージを一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="95142-124">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="95142-125">すべて</span><span class="sxs-lookup"><span data-stu-id="95142-125">All</span></span> |

| <span data-ttu-id="95142-126">セカンダリ コマンド</span><span class="sxs-lookup"><span data-stu-id="95142-126">Secondary Commands</span></span> | <span data-ttu-id="95142-127">説明</span><span class="sxs-lookup"><span data-stu-id="95142-127">Description</span></span> | <span data-ttu-id="95142-128">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="95142-128">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="95142-129">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="95142-129">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="95142-130">プロジェクトの出力パス内のすべてのアセンブリを調べ、バインド リダイレクトを追加、`app.config`または`web.config`必要な場所。</span><span class="sxs-lookup"><span data-stu-id="95142-130">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="95142-131">すべて</span><span class="sxs-lookup"><span data-stu-id="95142-131">All</span></span> |
| [<span data-ttu-id="95142-132">Get-Project</span><span class="sxs-lookup"><span data-stu-id="95142-132">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="95142-133">既定値または指定されたプロジェクトについての情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="95142-133">Displays information about the default or specified project.</span></span> | <span data-ttu-id="95142-134">3.0+</span><span class="sxs-lookup"><span data-stu-id="95142-134">3.0+</span></span> |
| [<span data-ttu-id="95142-135">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="95142-135">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="95142-136">プロジェクト、ライセンス、またはレポートの指定したパッケージの URL の不正使用の既定のブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="95142-136">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="95142-137">3\.0 + で非推奨とされます。</span><span class="sxs-lookup"><span data-stu-id="95142-137">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="95142-138">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="95142-138">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="95142-139">一般的に使用されるパラメーターの値は、カスタマイズされた展開を作成することができます、コマンドのパラメーターにタブ拡張を登録します。</span><span class="sxs-lookup"><span data-stu-id="95142-139">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="95142-140">すべて</span><span class="sxs-lookup"><span data-stu-id="95142-140">All</span></span> |
| [<span data-ttu-id="95142-141">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="95142-141">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="95142-142">バージョンには、パッケージがインストールされている get では、プロジェクトを指定し、ソリューション内のプロジェクトの他のバージョンが同期します。</span><span class="sxs-lookup"><span data-stu-id="95142-142">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="95142-143">3.0+</span><span class="sxs-lookup"><span data-stu-id="95142-143">3.0+</span></span> |
| [<span data-ttu-id="95142-144">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="95142-144">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="95142-145">必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="95142-145">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="95142-146">すべて</span><span class="sxs-lookup"><span data-stu-id="95142-146">All</span></span> |

<span data-ttu-id="95142-147">コンソール内でこれらのコマンドのいずれかで完全かつ詳細なヘルプ、のみ対象のコマンド名を持つ、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="95142-147">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="95142-148">すべてのパッケージ マネージャー コンソール コマンドは、次をサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="95142-148">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="95142-149">Debug</span><span class="sxs-lookup"><span data-stu-id="95142-149">Debug</span></span>
- <span data-ttu-id="95142-150">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="95142-150">ErrorAction</span></span>
- <span data-ttu-id="95142-151">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="95142-151">ErrorVariable</span></span>
- <span data-ttu-id="95142-152">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="95142-152">OutBuffer</span></span>
- <span data-ttu-id="95142-153">OutVariable</span><span class="sxs-lookup"><span data-stu-id="95142-153">OutVariable</span></span>
- <span data-ttu-id="95142-154">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="95142-154">PipelineVariable</span></span>
- <span data-ttu-id="95142-155">Verbose</span><span class="sxs-lookup"><span data-stu-id="95142-155">Verbose</span></span>
- <span data-ttu-id="95142-156">WarningAction</span><span class="sxs-lookup"><span data-stu-id="95142-156">WarningAction</span></span>
- <span data-ttu-id="95142-157">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="95142-157">WarningVariable</span></span>

<span data-ttu-id="95142-158">詳細については、 [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell ドキュメントにします。</span><span class="sxs-lookup"><span data-stu-id="95142-158">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
