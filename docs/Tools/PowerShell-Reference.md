---
title: "NuGet PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで利用できる PowerShell コマンドの完全な参照です。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0cbd9b13b34bd93fea6c6684c03bca9cff5d9e5e
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="powershell-reference"></a><span data-ttu-id="5a8bf-104">PowerShell リファレンス</span><span class="sxs-lookup"><span data-stu-id="5a8bf-104">PowerShell reference</span></span>

<span data-ttu-id="5a8bf-105">パッケージ マネージャー コンソールは、以下に示す特定のコマンドを使用して NuGet を使って操作する Windows 上の Visual Studio 内での PowerShell インターフェイスを提供します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-105">The Package Manager Console provides a PowerShell interface within Visual Studio on Windows to interact with NuGet through the specific commands listed below.</span></span> <span data-ttu-id="5a8bf-106">(コンソールは Visual Studio for mac で現在使用できません)コンソールの使用にについては、次を参照してください。、 [Package Manager Console](../tools/package-manager-console.md)トピックです。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-106">(The console is not presently available in Visual Studio for Mac.) For a guide to using the console, see the [Package Manager Console](../tools/package-manager-console.md) topic.</span></span>

> [!Tip]
> <span data-ttu-id="5a8bf-107">すべての PowerShell コマンドは、パッケージの消費量にのみ関連します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-107">All PowerShell commands relate only to package consumption.</span></span> <span data-ttu-id="5a8bf-108">PowerShell コマンドは、作成、およびパッケージには、他のパッケージのコンシューマーことができます。 その範囲内に以外のパッケージを公開には関連ありません。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-108">No PowerShell commands relate to creating and publishing packages except to the extent that a package can also be a consumer of other packages.</span></span>

> [!Important]
> <span data-ttu-id="5a8bf-109">ここに示すコマンドは、Visual Studio で、パッケージ マネージャー コンソールに固有とは異なる、[パッケージ管理モジュールのコマンド](/powershell/module/packagemanagement/?view=powershell-6)一般的な PowerShell 環境で使用可能なことです。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-109">The commands listed here are specific to the Package Manager Console in Visual Studio, and differ from the [Package Management module commands](/powershell/module/packagemanagement/?view=powershell-6) that are available in a general PowerShell environment.</span></span> <span data-ttu-id="5a8bf-110">具体的には、各環境には、他のでは使用できないコマンドと同じ名前のコマンドは特定の引数も異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-110">Specifically, each environment has commands that are not available in the other, and commands with the same name may also differ in their specific arguments.</span></span> <span data-ttu-id="5a8bf-111">Visual Studio でパッケージの管理コンソールを使用すると、コマンドと引数のこのトピックに記載されていますが適用されます。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-111">When using the Package Management Console in Visual Studio, the commands and arguments documented in this present topic apply.</span></span>

| <span data-ttu-id="5a8bf-112">一般的なコマンド</span><span class="sxs-lookup"><span data-stu-id="5a8bf-112">Common Commands</span></span> | <span data-ttu-id="5a8bf-113">説明</span><span class="sxs-lookup"><span data-stu-id="5a8bf-113">Description</span></span> | <span data-ttu-id="5a8bf-114">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="5a8bf-114">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="5a8bf-115">Install-Package</span><span class="sxs-lookup"><span data-stu-id="5a8bf-115">Install-Package</span></span>](ps-ref-install-package.md) | <span data-ttu-id="5a8bf-116">プロジェクトにパッケージとその依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-116">Installs a package and its dependencies into the project.</span></span> | <span data-ttu-id="5a8bf-117">すべて</span><span class="sxs-lookup"><span data-stu-id="5a8bf-117">All</span></span> |
| [<span data-ttu-id="5a8bf-118">Update-Package</span><span class="sxs-lookup"><span data-stu-id="5a8bf-118">Update-Package</span></span>](ps-ref-update-package.md) | <span data-ttu-id="5a8bf-119">パッケージとその依存関係またはプロジェクト内のすべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-119">Updates a package and its dependencies, or all packages in a project.</span></span> | <span data-ttu-id="5a8bf-120">すべて</span><span class="sxs-lookup"><span data-stu-id="5a8bf-120">All</span></span> |
| [<span data-ttu-id="5a8bf-121">Find-Package</span><span class="sxs-lookup"><span data-stu-id="5a8bf-121">Find-Package</span></span>](ps-ref-find-package.md) | <span data-ttu-id="5a8bf-122">パッケージ ID またはキーワードを使用して、パッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-122">Searches a package source using a package ID or keywords.</span></span> | <span data-ttu-id="5a8bf-123">3.0+</span><span class="sxs-lookup"><span data-stu-id="5a8bf-123">3.0+</span></span> |
| [<span data-ttu-id="5a8bf-124">Get-Package</span><span class="sxs-lookup"><span data-stu-id="5a8bf-124">Get-Package</span></span>](ps-ref-get-package.md) | <span data-ttu-id="5a8bf-125">ローカル リポジトリにインストールされているパッケージの一覧を取得またはパッケージ ソースから使用可能なパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-125">Retrieves the list of packages installed in the local repository, or lists packages available from a package source.</span></span> | <span data-ttu-id="5a8bf-126">すべて</span><span class="sxs-lookup"><span data-stu-id="5a8bf-126">All</span></span> |

| <span data-ttu-id="5a8bf-127">セカンダリ コマンド</span><span class="sxs-lookup"><span data-stu-id="5a8bf-127">Secondary Commands</span></span> | <span data-ttu-id="5a8bf-128">説明</span><span class="sxs-lookup"><span data-stu-id="5a8bf-128">Description</span></span> | <span data-ttu-id="5a8bf-129">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="5a8bf-129">NuGet Version</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="5a8bf-130">Add-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="5a8bf-130">Add-BindingRedirect</span></span>](ps-ref-add-bindingredirect.md) | <span data-ttu-id="5a8bf-131">プロジェクトの出力パス内のすべてのアセンブリを調べ、バインド リダイレクトを追加、`app.config`または`web.config`必要な場合です。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-131">Examines all assemblies within the output path for a project and adds binding redirects to the `app.config` or `web.config` where necessary.</span></span> | <span data-ttu-id="5a8bf-132">すべて</span><span class="sxs-lookup"><span data-stu-id="5a8bf-132">All</span></span> |
| [<span data-ttu-id="5a8bf-133">Get-Project</span><span class="sxs-lookup"><span data-stu-id="5a8bf-133">Get-Project</span></span>](ps-ref-get-project.md) | <span data-ttu-id="5a8bf-134">既定値または指定したプロジェクトについての情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-134">Displays information about the default or specified project.</span></span> | <span data-ttu-id="5a8bf-135">3.0+</span><span class="sxs-lookup"><span data-stu-id="5a8bf-135">3.0+</span></span> |
| [<span data-ttu-id="5a8bf-136">Open-PackagePage</span><span class="sxs-lookup"><span data-stu-id="5a8bf-136">Open-PackagePage</span></span>](ps-ref-open-packagepage.md) | <span data-ttu-id="5a8bf-137">プロジェクト、ライセンス、または指定したパッケージの不正使用を URL のレポートで既定のブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-137">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span> | <span data-ttu-id="5a8bf-138">3.0 以降で廃止されました</span><span class="sxs-lookup"><span data-stu-id="5a8bf-138">Deprecated in 3.0+</span></span> |
| [<span data-ttu-id="5a8bf-139">Register-TabExpansion</span><span class="sxs-lookup"><span data-stu-id="5a8bf-139">Register-TabExpansion</span></span>](ps-ref-register-tabexpansion.md) | <span data-ttu-id="5a8bf-140">一般的に使用されるパラメーター値では、カスタマイズされた展開を作成することができます、コマンドのパラメーターにタブ拡張を登録します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-140">Registers a tab expansion for the parameters of a command, allowing you to create customized expansions for commonly-used parameter values.</span></span> | <span data-ttu-id="5a8bf-141">すべて</span><span class="sxs-lookup"><span data-stu-id="5a8bf-141">All</span></span> |
| [<span data-ttu-id="5a8bf-142">Sync-Package</span><span class="sxs-lookup"><span data-stu-id="5a8bf-142">Sync-Package</span></span>](ps-ref-sync-package.md) | <span data-ttu-id="5a8bf-143">バージョンがインストール パッケージから取得では、プロジェクトを指定し、ソリューション内のプロジェクトの残りの部分のバージョンを同期します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-143">Get the version of installed package from specified project and syncs the version to the rest of projects in the solution.</span></span> | <span data-ttu-id="5a8bf-144">3.0+</span><span class="sxs-lookup"><span data-stu-id="5a8bf-144">3.0+</span></span> |
| [<span data-ttu-id="5a8bf-145">Uninstall-Package</span><span class="sxs-lookup"><span data-stu-id="5a8bf-145">Uninstall-Package</span></span>](ps-ref-uninstall-package.md) | <span data-ttu-id="5a8bf-146">必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-146">Removes a package from a project, optionally removing its dependencies.</span></span> | <span data-ttu-id="5a8bf-147">すべて</span><span class="sxs-lookup"><span data-stu-id="5a8bf-147">All</span></span> |

<span data-ttu-id="5a8bf-148">コンソール内でこれらのコマンドのいずれかを完全かつ詳細なヘルプ、だけ対象のコマンド名を持つ、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-148">For complete, detailed help on any of these commands within the console, just run the following with the command name in question:</span></span>

```ps
Get-Help <command> -full
```

<span data-ttu-id="5a8bf-149">パッケージ マネージャー コンソールのすべてのコマンドは、次をサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):</span><span class="sxs-lookup"><span data-stu-id="5a8bf-149">All Package Manager Console commands support the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216):</span></span>

- <span data-ttu-id="5a8bf-150">デバッグ</span><span class="sxs-lookup"><span data-stu-id="5a8bf-150">Debug</span></span>
- <span data-ttu-id="5a8bf-151">ErrorAction</span><span class="sxs-lookup"><span data-stu-id="5a8bf-151">ErrorAction</span></span>
- <span data-ttu-id="5a8bf-152">ErrorVariable</span><span class="sxs-lookup"><span data-stu-id="5a8bf-152">ErrorVariable</span></span>
- <span data-ttu-id="5a8bf-153">OutBuffer</span><span class="sxs-lookup"><span data-stu-id="5a8bf-153">OutBuffer</span></span>
- <span data-ttu-id="5a8bf-154">OutVariable</span><span class="sxs-lookup"><span data-stu-id="5a8bf-154">OutVariable</span></span>
- <span data-ttu-id="5a8bf-155">PipelineVariable</span><span class="sxs-lookup"><span data-stu-id="5a8bf-155">PipelineVariable</span></span>
- <span data-ttu-id="5a8bf-156">詳細</span><span class="sxs-lookup"><span data-stu-id="5a8bf-156">Verbose</span></span>
- <span data-ttu-id="5a8bf-157">WarningAction</span><span class="sxs-lookup"><span data-stu-id="5a8bf-157">WarningAction</span></span>
- <span data-ttu-id="5a8bf-158">WarningVariable</span><span class="sxs-lookup"><span data-stu-id="5a8bf-158">WarningVariable</span></span>

<span data-ttu-id="5a8bf-159">詳細についてを参照してください[about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) PowerShell ドキュメントにします。</span><span class="sxs-lookup"><span data-stu-id="5a8bf-159">For details, refer to [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in the PowerShell documentation.</span></span>
