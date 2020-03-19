---
title: Visual Studio のコンソールを使用して NuGet パッケージをインストールし、管理する
description: Visual Studio で NuGet パッケージ マネージャー コンソールを使用してパッケージを操作する方法について説明します。
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428577"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="24985-103">Visual Studio でパッケージ マネージャー コンソールを使用してパッケージをインストールおよび管理する (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="24985-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="24985-104">Nuget パッケージ マネージャー コンソールでは、[NuGet PowerShell コマンド](../reference/powershell-reference.md)を使用して、NuGet パッケージを検索、インストール、アンインストール、および更新することができます。</span><span class="sxs-lookup"><span data-stu-id="24985-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="24985-105">操作を実行するための手段がパッケージ マネージャー UI で提供されていない場合には、コンソールを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="24985-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="24985-106">コンソールで `nuget.exe` CLI コマンドを使用するには、「[コンソールで nuget.exe CLI を使用する](#use-the-nugetexe-cli-in-the-console)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24985-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="24985-107">コンソールは、Windows の Visual Studio に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="24985-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="24985-108">Visual Studio for Mac や Visual Studio Code には含まれていません。</span><span class="sxs-lookup"><span data-stu-id="24985-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="24985-109">パッケージを検索してインストールする</span><span class="sxs-lookup"><span data-stu-id="24985-109">Find and install a package</span></span>

<span data-ttu-id="24985-110">たとえば、パッケージの検索とインストールは、次の 3 つの簡単な手順で行われます。</span><span class="sxs-lookup"><span data-stu-id="24985-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="24985-111">Visual Studio でプロジェクト/ソリューションを開き、 **[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** コマンドを使用してコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="24985-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="24985-112">インストールするパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="24985-112">Find the package you want to install.</span></span> <span data-ttu-id="24985-113">既にわかっている場合は、手順 3 に進みます。</span><span class="sxs-lookup"><span data-stu-id="24985-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="24985-114">インストール コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="24985-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="24985-115">コンソールで使用できるすべての操作は、[NuGet CLI](../reference/nuget-exe-cli-reference.md) を使用して行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="24985-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="24985-116">ただし、コンソール コマンドは、Visual Studio と保存済みのプロジェクト/ソリューションのコンテキスト内で動作し、多くの場合、同等の CLI コマンドよりも多くの操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="24985-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="24985-117">たとえば、コンソールを使用してパッケージをインストールすると、プロジェクトへの参照が追加されますが、CLI コマンドでは参照は追加されません。</span><span class="sxs-lookup"><span data-stu-id="24985-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="24985-118">このため、Visual Studio で作業する開発者は、通常、CLI ではなくコンソールを優先的に使用します。</span><span class="sxs-lookup"><span data-stu-id="24985-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="24985-119">多くのコンソール操作は、ソリューションが既知のパス名を使用して Visual Studio で開かれていることを前提に動作します。</span><span class="sxs-lookup"><span data-stu-id="24985-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="24985-120">保存されていないソリューションがある場合や、ソリューションがない場合は、"ソリューションが開いていないか、または保存されていません。</span><span class="sxs-lookup"><span data-stu-id="24985-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="24985-121">ソリューションが開いており、保存されていることを確認してください " というエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="24985-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="24985-122">これは、コンソールがソリューション フォルダーを特定できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="24985-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="24985-123">保存されていないソリューションを保存するか、ソリューションを開いていない場合は作成して保存することで、エラーを解決できます。</span><span class="sxs-lookup"><span data-stu-id="24985-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="24985-124">コンソールとコンソール コントロールを開く</span><span class="sxs-lookup"><span data-stu-id="24985-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="24985-125">**[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** コマンドを使用して、Visual Studio でコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="24985-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="24985-126">コンソールは、好みに合わせて配置できる Visual Studio ウィンドウです (「[Visual Studio のウィンドウ レイアウトをカスタマイズする](/visualstudio/ide/customizing-window-layouts-in-visual-studio)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="24985-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="24985-127">既定では、コンソール コマンドは、ウィンドウの上部にあるコントロールで設定された特定のパッケージ ソースとプロジェクトに対して動作します。</span><span class="sxs-lookup"><span data-stu-id="24985-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![パッケージ ソースとプロジェクトのパッケージ マネージャー コンソール コントロール](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="24985-129">別のパッケージ ソースやプロジェクトを選択すると、後続のコマンドの既定値が変更されます。</span><span class="sxs-lookup"><span data-stu-id="24985-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="24985-130">既定値を変更せずにこれらの設定をオーバーライドするために、ほとんどのコマンドで `-Source` および `-ProjectName` オプションがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="24985-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="24985-131">パッケージ ソースを管理するには、歯車アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="24985-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="24985-132">これは、 **[ツール] > [オプション] > [NuGet パッケージ マネージャー]** ダイアログ ボックスへのショートカットです ([パッケージ マネージャー UI](install-use-packages-visual-studio.md#package-sources) に関するページで説明されています)。</span><span class="sxs-lookup"><span data-stu-id="24985-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="24985-133">また、プロジェクト セレクターの右側にあるコントロールを使用すると、コンソールの内容をクリアできます。</span><span class="sxs-lookup"><span data-stu-id="24985-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![パッケージ マネージャー コンソールの設定とクリアのためのコントロール](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="24985-135">右端のボタンをクリックすると、実行時間の長いコマンドが中断されます。</span><span class="sxs-lookup"><span data-stu-id="24985-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="24985-136">たとえば、`Get-Package -ListAvailable -PageSize 500` を実行すると、既定のソース上の上位 500 パッケージ (nuget.org など) が一覧表示されます (これには数分かかることがあります)。</span><span class="sxs-lookup"><span data-stu-id="24985-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![パッケージ マネージャー コンソールの停止コントロール](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="24985-138">パッケージをインストールします</span><span class="sxs-lookup"><span data-stu-id="24985-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="24985-139">「[Install-Package](../reference/ps-reference/ps-ref-install-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24985-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="24985-140">コンソールでパッケージをインストールすると、「[NuGet パッケージのインストールのしくみ](../concepts/package-installation-process.md)」で説明されているのと同じ手順が実行されるのに加えて、次の操作が実行されます。</span><span class="sxs-lookup"><span data-stu-id="24985-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="24985-141">コンソールのウィンドウに、適用されるライセンス条項と暗黙の契約が表示されます。</span><span class="sxs-lookup"><span data-stu-id="24985-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="24985-142">条項に同意しない場合は、パッケージをすぐにアンインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="24985-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="24985-143">また、パッケージへの参照がプロジェクト ファイルに追加され、 **[参照]** ノードの下の**ソリューション エクスプローラー**に表示されます。プロジェクト ファイルの変更内容を直接確認するには、プロジェクトを保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="24985-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="24985-144">パッケージをアンインストールします</span><span class="sxs-lookup"><span data-stu-id="24985-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="24985-145">「[Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24985-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="24985-146">識別子を確認する必要がある場合は、[Get-Package](../reference/ps-reference/ps-ref-get-package.md) を使用して、既定のプロジェクトに現在インストールされているすべてのパッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="24985-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="24985-147">パッケージをアンインストールすると、次の操作が実行されます。</span><span class="sxs-lookup"><span data-stu-id="24985-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="24985-148">パッケージへの参照をプロジェクトから削除します (使用中の管理形式にかかわらず)。</span><span class="sxs-lookup"><span data-stu-id="24985-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="24985-149">参照は**ソリューション エクスプローラー**に表示されなくなります。</span><span class="sxs-lookup"><span data-stu-id="24985-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="24985-150">(**Bin** フォルダーから削除されたことを確認するには、プロジェクトのリビルドが必要になる場合があります。)</span><span class="sxs-lookup"><span data-stu-id="24985-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="24985-151">パッケージがインストールされたときに `app.config` または `web.config` に加えられた変更を元に戻します。</span><span class="sxs-lookup"><span data-stu-id="24985-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="24985-152">以前にインストールされた依存関係を削除します (残りのパッケージがそれらの依存関係を使用していない場合)。</span><span class="sxs-lookup"><span data-stu-id="24985-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="24985-153">パッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="24985-153">Update a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="24985-154">「[Get-Package](../reference/ps-reference/ps-ref-get-package.md)」と「[Update-Package](../reference/ps-reference/ps-ref-update-package.md)」を参照してください</span><span class="sxs-lookup"><span data-stu-id="24985-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="24985-155">パッケージを検索する</span><span class="sxs-lookup"><span data-stu-id="24985-155">Find a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="24985-156">「[Find-Package](../reference/ps-reference/ps-ref-find-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24985-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="24985-157">Visual Studio 2013 以前では、[Get-Package](../reference/ps-reference/ps-ref-get-package.md) を使用してください。</span><span class="sxs-lookup"><span data-stu-id="24985-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="24985-158">コンソールの可用性</span><span class="sxs-lookup"><span data-stu-id="24985-158">Availability of the console</span></span>

<span data-ttu-id="24985-159">Visual Studio 2017 以降では、.NET 関連のワークロードを選択すると、NuGet と NuGet パッケージ マネージャーが自動的にインストールされます。また、Visual Studio インストーラーで **[個別のコンポーネント]** > [コードツール] > [NuGet パッケージ マネージャー] を選択して、個別にインストールすることもできます。</span><span class="sxs-lookup"><span data-stu-id="24985-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="24985-160">また、Visual Studio 2015 以前で NuGet パッケージ マネージャーが見当たらない場合は、 **[ツール] > [拡張機能と更新プログラム]** を選択して、NuGet パッケージ マネージャー拡張機能を検索してください。</span><span class="sxs-lookup"><span data-stu-id="24985-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="24985-161">Visual Studio 内で拡張機能のインストーラーを使用できない場合は、拡張機能を [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) から直接ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="24985-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="24985-162">パッケージ マネージャー コンソールは、現在、Visual Studio for Mac では使用できません。</span><span class="sxs-lookup"><span data-stu-id="24985-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="24985-163">ただし、これと同等のコマンドは、[NuGet CLI](../reference/nuget-exe-CLI-reference.md) を介して使用できます。</span><span class="sxs-lookup"><span data-stu-id="24985-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="24985-164">Visual Studio for Mac には、NuGet パッケージを管理するための UI が用意されています。</span><span class="sxs-lookup"><span data-stu-id="24985-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="24985-165">「[プロジェクトに NuGet パッケージを含める](/visualstudio/mac/nuget-walkthrough)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24985-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="24985-166">パッケージ マネージャー コンソールは、Visual Studio Code には含まれていません。</span><span class="sxs-lookup"><span data-stu-id="24985-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="24985-167">パッケージ マネージャー コンソールを拡張する</span><span class="sxs-lookup"><span data-stu-id="24985-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="24985-168">一部のパッケージでは、コンソール用の新しいコマンドがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="24985-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="24985-169">たとえば、`MvcScaffolding` では、`Scaffold` コマンドが次のように作成され、これにより、ASP.NET MVC のコントローラーとビューが生成されます。</span><span class="sxs-lookup"><span data-stu-id="24985-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![MvcScaffold のインストールと使用](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="24985-171">NuGet PowerShell プロファイルを設定する</span><span class="sxs-lookup"><span data-stu-id="24985-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="24985-172">Powershell プロファイルを使用すると、PowerShell を使用するすべての場所で、一般的に使用されるコマンドを使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="24985-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="24985-173">NuGet では、NuGet 固有のプロファイルがサポートされます。これは通常、次の場所にあります。</span><span class="sxs-lookup"><span data-stu-id="24985-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="24985-174">プロファイルを検索するには、コンソールで「`$profile`」と入力します。</span><span class="sxs-lookup"><span data-stu-id="24985-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="24985-175">詳細については、「[Windows PowerShell プロファイル](https://technet.microsoft.com/library/bb613488.aspx)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24985-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="24985-176">コンソールで nuget.exe CLI を使用する</span><span class="sxs-lookup"><span data-stu-id="24985-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="24985-177">パッケージ マネージャー コンソールで [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) を使用できるようにするには、コンソールから [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="24985-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
