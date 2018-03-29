---
title: NuGet パッケージ マネージャー コンソール ガイド |Microsoft ドキュメント
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
f1_keywords:
- vs.nuget.packagemanager.console
description: Visual Studio で NuGet パッケージ マネージャー コンソールを使用してパッケージを操作するための手順です。
keywords: NuGet パッケージ マネージャー コンソールで、NuGet powershell、NuGet パッケージを管理します。
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: af22a524f6b4a41a4c24077fe396846da6fb1ff8
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="2cae0-104">パッケージ マネージャー コンソール</span><span class="sxs-lookup"><span data-stu-id="2cae0-104">Package Manager Console</span></span>

<span data-ttu-id="2cae0-105">NuGet パッケージ マネージャー コンソールは、Windows 2012 以降のバージョンの Visual Studio に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="2cae0-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="2cae0-106">(にない Mac または Visual Studio のコード用の Visual Studio に含まれています。)</span><span class="sxs-lookup"><span data-stu-id="2cae0-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="2cae0-107">コンソールでは、使用できます。 [NuGet PowerShell コマンド](../tools/powershell-reference.md)見つけるには、インストール、アンインストール、および NuGet パッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="2cae0-108">コンソールを使用する場合は必要、パッケージ マネージャーの UI が操作を実行する方法を提供できません。</span><span class="sxs-lookup"><span data-stu-id="2cae0-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="2cae0-109">使用する`nuget.exe`コマンド コンソールを参照してください[コンソールで nuget.exe CLI を使用して](#using-the-nugetexe-cli-in-the-console)です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-109">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="2cae0-110">たとえば、検索し、パッケージをインストールするは 3 つの簡単な手順で行います。</span><span class="sxs-lookup"><span data-stu-id="2cae0-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="2cae0-111">Visual Studio でプロジェクト/ソリューションを開きを使用してコンソールを開き、**ツール > NuGet Package Manager > パッケージ マネージャー コンソール**コマンド。</span><span class="sxs-lookup"><span data-stu-id="2cae0-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="2cae0-112">インストールするパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-112">Find the package you want to install.</span></span> <span data-ttu-id="2cae0-113">この既にわかっている場合は、手順 3. に進みます。</span><span class="sxs-lookup"><span data-stu-id="2cae0-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="2cae0-114">インストール コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="2cae0-115">コンソールで使用できるすべての操作を実行することも、 [NuGet CLI](../tools/nuget-exe-cli-reference.md)です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="2cae0-116">ただし、コンソールのコマンドは、Visual Studio と保存されているプロジェクト/ソリューションのコンテキスト内で動作し、多くの場合、それと等価の CLI コマンドよりも多くの作業します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="2cae0-117">たとえば、コンソールを使用してパッケージをインストールする参照を追加プロジェクトに、CLI コマンドは実行されません。</span><span class="sxs-lookup"><span data-stu-id="2cae0-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="2cae0-118">このため、通常 Visual Studio で作業する開発者は、CLI にコンソールを使用してを選びます。</span><span class="sxs-lookup"><span data-stu-id="2cae0-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="2cae0-119">多くのコンソール操作は、既知のパス名で Visual Studio で開くソリューションによって異なります。</span><span class="sxs-lookup"><span data-stu-id="2cae0-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="2cae0-120">エラーを確認できます、保存されていないソリューションまたはソリューションがない場合、"ソリューションが開かれていないか、保存されません。</span><span class="sxs-lookup"><span data-stu-id="2cae0-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="2cae0-121">確認してください、開く、保存されているソリューションがある。"</span><span class="sxs-lookup"><span data-stu-id="2cae0-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="2cae0-122">これは、コンソールで、ソリューション フォルダーを特定できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="2cae0-123">保存されていないソリューションを保存または作成があるない場合は、ソリューションを保存する場合は、エラーを修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cae0-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="2cae0-124">コンソール ウィンドウとコンソールのコントロールを開く</span><span class="sxs-lookup"><span data-stu-id="2cae0-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="2cae0-125">Visual Studio を使用して、コンソールを開き、**ツール > NuGet Package Manager > パッケージ マネージャー コンソール**コマンド。</span><span class="sxs-lookup"><span data-stu-id="2cae0-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="2cae0-126">コンソールでは、Visual Studio のウィンドウを配置し、たいただし配置されていることができます (を参照してください[Visual Studio でのウィンドウ レイアウトをカスタマイズ](/visualstudio/ide/customizing-window-layouts-in-visual-studio))。</span><span class="sxs-lookup"><span data-stu-id="2cae0-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="2cae0-127">既定では、ウィンドウの上部にあるコントロールで設定されているコンソール コマンドが特定のパッケージのソース ファイルおよびプロジェクトに対して操作します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![パッケージ ソース ファイルおよびプロジェクトのパッケージ マネージャー コンソールのコントロール](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="2cae0-129">別のパッケージのソースまたはプロジェクトを選択すると、後続のコマンドの既定の設定を変更します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="2cae0-130">上書きをこれらの設定、既定値を変更することがなくほとんどのコマンド サポート`-Source`と`-ProjectName`オプション。</span><span class="sxs-lookup"><span data-stu-id="2cae0-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="2cae0-131">パッケージ ソースを管理するには、歯車アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="2cae0-132">これへのショートカットを**ツール > オプション > NuGet Package Manager > パッケージ ソース** ダイアログ ボックスの定義に従って、[パッケージ マネージャーの UI](package-manager-ui.md#package-sources)ページ。</span><span class="sxs-lookup"><span data-stu-id="2cae0-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="2cae0-133">また、コントロールをプロジェクトのセレクターの右側には、本体の内容をクリアします。</span><span class="sxs-lookup"><span data-stu-id="2cae0-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![パッケージ マネージャー コンソールの設定およびクリア コントロール](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="2cae0-135">一番右のボタンは、実行時間の長いコマンドを中断します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="2cae0-136">たとえば、実行している`Get-Package -ListAvailable -PageSize 500`上位 500 のパッケージを実行するのに数分かかる場合があります (など nuget.org)、既定のソースを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Package Manager Console ストップ コントロール](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="2cae0-138">パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2cae0-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="2cae0-139">参照してください[Install-package](../tools/ps-ref-install-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="2cae0-140">コンソールでパッケージをインストールするどおりに、同じ手順で説明されている[パッケージがインストールされているときに起こる](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed)、以下が追加されます。</span><span class="sxs-lookup"><span data-stu-id="2cae0-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="2cae0-141">コンソールでは、黙示の許諾契約書には、そのウィンドウに適用されるライセンス条項を表示します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="2cae0-142">条項に同意しない場合は、パッケージをすぐにアンインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="2cae0-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="2cae0-143">パッケージへの参照は、プロジェクト ファイルに追加されに表示されます**ソリューション エクスプ ローラー**下にある、**参照**ノード、プロジェクト ファイル内の変更を直接表示するプロジェクトを保存する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2cae0-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="2cae0-144">パッケージをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="2cae0-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="2cae0-145">参照してください[Uninstall-package](../tools/ps-ref-uninstall-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="2cae0-146">使用して[Get-package](../tools/ps-ref-get-package.md)する識別子を検索する必要がある場合の既定のプロジェクトに現在インストールされているすべてのパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2cae0-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="2cae0-147">パッケージをアンインストールするには、次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="2cae0-148">プロジェクト (および、使用されている管理形式) から、パッケージへの参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="2cae0-149">参照には現れません**ソリューション エクスプ ローラー**です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="2cae0-150">(表示から削除するプロジェクトをリビルドする必要があります、 **Bin**フォルダーです)。</span><span class="sxs-lookup"><span data-stu-id="2cae0-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="2cae0-151">加えられた変更を反転させます`app.config`または`web.config`パッケージがインストールされている場合。</span><span class="sxs-lookup"><span data-stu-id="2cae0-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="2cae0-152">以前にインストールされている削除の依存関係残存するパッケージがそれらの依存関係を使用しない場合。</span><span class="sxs-lookup"><span data-stu-id="2cae0-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="2cae0-153">パッケージの更新</span><span class="sxs-lookup"><span data-stu-id="2cae0-153">Updating a package</span></span>

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

<span data-ttu-id="2cae0-154">参照してください[Get-package](../tools/ps-ref-get-package.md)と[更新プログラム パッケージ](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="2cae0-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="2cae0-155">パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-155">Finding a package</span></span>

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

<span data-ttu-id="2cae0-156">参照してください[Find-package](../tools/ps-ref-find-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="2cae0-157">Visual Studio 2013 以前のバージョンでを使用して[Get-package](../tools/ps-ref-get-package.md)代わりにします。</span><span class="sxs-lookup"><span data-stu-id="2cae0-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="2cae0-158">コンソールの可用性</span><span class="sxs-lookup"><span data-stu-id="2cae0-158">Availability of the console</span></span>

<span data-ttu-id="2cae0-159">Visual Studio 2017 で NuGet と NuGet パッケージ マネージャーが自動的にインストールを選択するときにします。NET に関連するワークロードです。インストールすることも、個別にチェックして、**個々 のコンポーネント > コード ツール > の NuGet package manager** Visual Studio 2017 インストーラー オプション。</span><span class="sxs-lookup"><span data-stu-id="2cae0-159">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="2cae0-160">NuGet パッケージ マネージャー Visual Studio 2015 以前のバージョンで、欠落している場合は確認も、**ツール > 拡張機能と更新しています.** NuGet Package Manager 拡張機能を検索します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="2cae0-161">直接、拡張機能をダウンロードするには Visual Studio での拡張機能インストーラーを使用することがない場合は、 [ https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="2cae0-162">パッケージ マネージャー コンソールは Visual Studio for mac と共に現在使用できません。</span><span class="sxs-lookup"><span data-stu-id="2cae0-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="2cae0-163">同等のコマンドがを介して使用できる、 [NuGet CLI](nuget-exe-CLI-reference.md)です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="2cae0-164">Visual Studio for Mac は、NuGet パッケージを管理するための UI を持つはできます。</span><span class="sxs-lookup"><span data-stu-id="2cae0-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="2cae0-165">参照してください[などの NuGet パッケージ、プロジェクトの](/visualstudio/mac/nuget-walkthrough)します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="2cae0-166">パッケージ マネージャー コンソールは、Visual Studio のコードに含まれていません。</span><span class="sxs-lookup"><span data-stu-id="2cae0-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="2cae0-167">パッケージ マネージャー コンソールの拡張</span><span class="sxs-lookup"><span data-stu-id="2cae0-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="2cae0-168">一部のパッケージは、コンソールの新しいコマンドをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2cae0-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="2cae0-169">たとえば、`MvcScaffolding`のようなコマンドを作成`Scaffold`次に示すを生成する ASP.NET MVC のコント ローラーとビュー。</span><span class="sxs-lookup"><span data-stu-id="2cae0-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![インストールと MvcScaffold の使用](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="2cae0-171">NuGet PowerShell プロファイルを設定します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="2cae0-172">PowerShell のプロファイルでは、PowerShell を使用する場合、一般的に使用されるコマンドを使用できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="2cae0-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="2cae0-173">NuGet は、通常、次の場所で見つかった NuGet 固有のプロファイルをサポートします。</span><span class="sxs-lookup"><span data-stu-id="2cae0-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="2cae0-174">プロファイルを検索するには、次のように入力します。`$profile`コンソール。</span><span class="sxs-lookup"><span data-stu-id="2cae0-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="2cae0-175">詳細についてを参照してください[Windows PowerShell プロファイル](https://technet.microsoft.com/library/bb613488.aspx)です。</span><span class="sxs-lookup"><span data-stu-id="2cae0-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="2cae0-176">コンソールで nuget.exe CLI を使用します。</span><span class="sxs-lookup"><span data-stu-id="2cae0-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="2cae0-177">させる、 [ `nuget.exe` CLI](nuget-exe-cli-reference.md)パッケージ マネージャー コンソールで、使用可能なインストール、 [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/)コンソールからのパッケージ。</span><span class="sxs-lookup"><span data-stu-id="2cae0-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
