---
title: "NuGet パッケージ マネージャー コンソール ガイド |Microsoft ドキュメント"
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
description: "Visual Studio で NuGet パッケージ マネージャー コンソールを使用してパッケージを操作するための手順です。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet powershell、NuGet パッケージを管理します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d9df514c6f92a3ea0841503d86c44271e70f95f2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-manager-console"></a><span data-ttu-id="e5076-104">パッケージ マネージャー コンソール</span><span class="sxs-lookup"><span data-stu-id="e5076-104">Package Manager Console</span></span>

<span data-ttu-id="e5076-105">NuGet パッケージ マネージャー コンソールは、Windows 2012 以降のバージョンの Visual Studio に組み込まれています。</span><span class="sxs-lookup"><span data-stu-id="e5076-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="e5076-106">(にない Mac または Visual Studio のコード用の Visual Studio に含まれています。)</span><span class="sxs-lookup"><span data-stu-id="e5076-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="e5076-107">コンソールでは、使用できます。 [NuGet PowerShell コマンド](../tools/powershell-reference.md)見つけるには、インストール、アンインストール、および NuGet パッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="e5076-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="e5076-108">コンソールを使用する場合は必要、パッケージ マネージャーの UI が操作を実行する方法を提供できません。</span><span class="sxs-lookup"><span data-stu-id="e5076-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span>

<span data-ttu-id="e5076-109">たとえば、検索し、パッケージをインストールするは 3 つの簡単な手順で行います。</span><span class="sxs-lookup"><span data-stu-id="e5076-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="e5076-110">Visual Studio でプロジェクト/ソリューションを開きを使用してコンソールを開き、**ツール > NuGet Package Manager > パッケージ マネージャー コンソール**コマンド。</span><span class="sxs-lookup"><span data-stu-id="e5076-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="e5076-111">インストールするパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="e5076-111">Find the package you want to install.</span></span> <span data-ttu-id="e5076-112">この既にわかっている場合は、手順 3. に進みます。</span><span class="sxs-lookup"><span data-stu-id="e5076-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="e5076-113">インストール コマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="e5076-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

<span data-ttu-id="e5076-114">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="e5076-114">In this topic:</span></span>

- [<span data-ttu-id="e5076-115">コンソールを開く</span><span class="sxs-lookup"><span data-stu-id="e5076-115">Opening the console</span></span>](#opening-the-console-and-console-controls)
- [<span data-ttu-id="e5076-116">パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e5076-116">Installing a package</span></span>](#installing-a-package)
- [<span data-ttu-id="e5076-117">パッケージをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="e5076-117">Uninstalling a package</span></span>](#uninstalling-a-package)
- [<span data-ttu-id="e5076-118">パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="e5076-118">Finding a package</span></span>](#finding-a-package)
- [<span data-ttu-id="e5076-119">パッケージの更新</span><span class="sxs-lookup"><span data-stu-id="e5076-119">Updating a package</span></span>](#updating-a-package)
- [<span data-ttu-id="e5076-120">コンソールの可用性</span><span class="sxs-lookup"><span data-stu-id="e5076-120">Availability of the console</span></span>](#availability-of-the-console)
- [<span data-ttu-id="e5076-121">パッケージ マネージャー コンソールの拡張</span><span class="sxs-lookup"><span data-stu-id="e5076-121">Extending the Package Manager Console</span></span>](#extending-the-package-manager-console)
- [<span data-ttu-id="e5076-122">NuGet PowerShell プロファイルを設定します。</span><span class="sxs-lookup"><span data-stu-id="e5076-122">Setting up a NuGet PowerShell profile</span></span>](#setting-up-a-nuget-powershell-profile)

> [!Important]
> <span data-ttu-id="e5076-123">コンソールで使用できるすべての操作を実行することも、 [NuGet CLI](../tools/nuget-exe-cli-reference.md)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-123">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="e5076-124">ただし、コンソールのコマンドは、Visual Studio と保存されているプロジェクト/ソリューションのコンテキスト内で動作し、多くの場合、それと等価の CLI コマンドよりも多くの作業します。</span><span class="sxs-lookup"><span data-stu-id="e5076-124">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="e5076-125">たとえば、コンソールを使用してパッケージをインストールする参照を追加プロジェクトに、CLI コマンドは実行されません。</span><span class="sxs-lookup"><span data-stu-id="e5076-125">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="e5076-126">このため、通常 Visual Studio で作業する開発者は、CLI にコンソールを使用してを選びます。</span><span class="sxs-lookup"><span data-stu-id="e5076-126">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="e5076-127">多くのコンソール操作は、既知のパス名で Visual Studio で開くソリューションによって異なります。</span><span class="sxs-lookup"><span data-stu-id="e5076-127">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="e5076-128">エラーを確認できます、保存されていないソリューションまたはソリューションがない場合、"ソリューションが開かれていないか、保存されません。</span><span class="sxs-lookup"><span data-stu-id="e5076-128">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="e5076-129">確認してください、開く、保存されているソリューションがある。"</span><span class="sxs-lookup"><span data-stu-id="e5076-129">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="e5076-130">これは、コンソールで、ソリューション フォルダーを特定できないことを示します。</span><span class="sxs-lookup"><span data-stu-id="e5076-130">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="e5076-131">保存されていないソリューションを保存または作成があるない場合は、ソリューションを保存する場合は、エラーを修正する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e5076-131">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="e5076-132">コンソール ウィンドウとコンソールのコントロールを開く</span><span class="sxs-lookup"><span data-stu-id="e5076-132">Opening the console and console controls</span></span>

1. <span data-ttu-id="e5076-133">Visual Studio を使用して、コンソールを開き、**ツール > NuGet Package Manager > パッケージ マネージャー コンソール**コマンド。</span><span class="sxs-lookup"><span data-stu-id="e5076-133">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="e5076-134">コンソールでは、Visual Studio のウィンドウを配置し、たいただし配置されていることができます (を参照してください[Visual Studio でのウィンドウ レイアウトをカスタマイズ](https://docs.microsoft.com/visualstudio/ide/customizing-window-layouts-in-visual-studio))。</span><span class="sxs-lookup"><span data-stu-id="e5076-134">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](https://docs.microsoft.com/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="e5076-135">既定では、ウィンドウの上部にあるコントロールで設定されているコンソール コマンドが特定のパッケージのソース ファイルおよびプロジェクトに対して操作します。</span><span class="sxs-lookup"><span data-stu-id="e5076-135">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![パッケージ ソース ファイルおよびプロジェクトのパッケージ マネージャー コンソールのコントロール](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="e5076-137">別のパッケージのソースまたはプロジェクトを選択すると、後続のコマンドの既定の設定を変更します。</span><span class="sxs-lookup"><span data-stu-id="e5076-137">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="e5076-138">上書きをこれらの設定、既定値を変更することがなくほとんどのコマンド サポート`-Source`と`-ProjectName`オプション。</span><span class="sxs-lookup"><span data-stu-id="e5076-138">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="e5076-139">パッケージ ソースを管理するには、歯車アイコンを選択します。</span><span class="sxs-lookup"><span data-stu-id="e5076-139">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="e5076-140">これへのショートカットを**ツール > オプション > NuGet Package Manager > パッケージ ソース** ダイアログ ボックスの定義に従って、[パッケージ マネージャーの UI](Package-Manager-UI.md#package-sources)ページ。</span><span class="sxs-lookup"><span data-stu-id="e5076-140">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="e5076-141">また、コントロールをプロジェクトのセレクターの右側には、本体の内容をクリアします。</span><span class="sxs-lookup"><span data-stu-id="e5076-141">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![パッケージ マネージャー コンソールの設定およびクリア コントロール](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="e5076-143">一番右のボタンは、実行時間の長いコマンドを中断します。</span><span class="sxs-lookup"><span data-stu-id="e5076-143">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="e5076-144">たとえば、実行している`Get-Package -ListAvailable -PageSize 500`上位 500 のパッケージを実行するのに数分かかる場合があります (など nuget.org)、既定のソースを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="e5076-144">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Package Manager Console ストップ コントロール](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="e5076-146">パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e5076-146">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="e5076-147">参照してください[Install-package](../tools/ps-ref-install-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-147">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="e5076-148">パッケージをインストールするには、次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="e5076-148">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="e5076-149">暗黙的なアグリーメントをコンソール ウィンドウで該当するライセンス条項を表示します。</span><span class="sxs-lookup"><span data-stu-id="e5076-149">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="e5076-150">条項に同意しない場合は、パッケージをすぐにアンインストールしてください。</span><span class="sxs-lookup"><span data-stu-id="e5076-150">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="e5076-151">使用されている参照形式で、プロジェクトへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="e5076-151">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="e5076-152">参照は、ソリューション エクスプ ローラーと、該当する参照のフォーマット ファイルで、後で表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5076-152">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="e5076-153">ただし、PackageReference、使用する必要があるプロジェクト ファイル内の変更を直接表示するプロジェクトを保存します。</span><span class="sxs-lookup"><span data-stu-id="e5076-153">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="e5076-154">パッケージによってキャッシュされます。</span><span class="sxs-lookup"><span data-stu-id="e5076-154">Caches the package:</span></span>
    - <span data-ttu-id="e5076-155">PackageReference: パッケージにキャッシュされた`%USERPROFILE%\.nuget\packages`つまりファイルのロックと`project.assets.json`が更新されます。</span><span class="sxs-lookup"><span data-stu-id="e5076-155">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
    - <span data-ttu-id="e5076-156">`packages.config`: 作成、`packages`フォルダー内にサブフォルダーへのパッケージ ファイル、ソリューションのルートとコピーにします。</span><span class="sxs-lookup"><span data-stu-id="e5076-156">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="e5076-157">`package.config`ファイルを更新します。</span><span class="sxs-lookup"><span data-stu-id="e5076-157">The `package.config` file is updated.</span></span>
- <span data-ttu-id="e5076-158">更新プログラム`app.config`や`web.config`パッケージで使用する場合[ソースと config ファイルの変換](../create-packages/source-and-config-file-transformations.md)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-158">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="e5076-159">プロジェクトに既に存在していない場合は、すべての依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e5076-159">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="e5076-160">プロセスでは、パッケージのバージョンを更新この可能性があります」の説明に従って[依存関係の解決](../consume-packages/dependency-resolution.md)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-160">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="e5076-161">Visual Studio のウィンドウで、使用可能な場合、パッケージの readme ファイルを表示します。</span><span class="sxs-lookup"><span data-stu-id="e5076-161">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="e5076-162">パッケージをインストールする主な利点の 1 つ、`Install-Package`コンソールのコマンドは、パッケージ マネージャーの UI を使用した場合と同様に、プロジェクトへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="e5076-162">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="e5076-163">これに対し、 `nuget install` CLI コマンドは、のみパッケージをダウンロードし、参照を自動的に追加できません。</span><span class="sxs-lookup"><span data-stu-id="e5076-163">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="e5076-164">パッケージをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="e5076-164">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="e5076-165">参照してください[Uninstall-package](../tools/ps-ref-uninstall-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-165">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="e5076-166">使用して[Get-package](../tools/ps-ref-get-package.md)する識別子を検索する必要がある場合の既定のプロジェクトに現在インストールされているすべてのパッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="e5076-166">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="e5076-167">パッケージをアンインストールするには、次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="e5076-167">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="e5076-168">プロジェクト (および、使用されている参照形式) から、パッケージへの参照を削除します。</span><span class="sxs-lookup"><span data-stu-id="e5076-168">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="e5076-169">参照がソリューション エクスプ ローラーで表示されません。</span><span class="sxs-lookup"><span data-stu-id="e5076-169">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="e5076-170">(表示から削除するプロジェクトをリビルドする必要があります、 **Bin**フォルダーです)。</span><span class="sxs-lookup"><span data-stu-id="e5076-170">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="e5076-171">加えられた変更を反転させます`app.config`または`web.config`パッケージがインストールされている場合。</span><span class="sxs-lookup"><span data-stu-id="e5076-171">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="e5076-172">以前にインストールされている削除の依存関係残存するパッケージがそれらの依存関係を使用しない場合。</span><span class="sxs-lookup"><span data-stu-id="e5076-172">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="e5076-173">同様に`Install-Package`、`Uninstall-Package`コマンドとは異なり、プロジェクト内の参照を管理するための利点には、 `nuget uninstall` CLI コマンド。</span><span class="sxs-lookup"><span data-stu-id="e5076-173">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="e5076-174">パッケージの更新</span><span class="sxs-lookup"><span data-stu-id="e5076-174">Updating a package</span></span>

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

<span data-ttu-id="e5076-175">参照してください[Get-package](../tools/ps-ref-get-package.md)と[更新プログラム パッケージ](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="e5076-175">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="e5076-176">パッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="e5076-176">Finding a package</span></span>

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

<span data-ttu-id="e5076-177">参照してください[Find-package](../tools/ps-ref-find-package.md)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-177">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="e5076-178">Visual Studio 2013 以前のバージョンでを使用して[Get-package](../tools/ps-ref-get-package.md)代わりにします。</span><span class="sxs-lookup"><span data-stu-id="e5076-178">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="e5076-179">コンソールの可用性</span><span class="sxs-lookup"><span data-stu-id="e5076-179">Availability of the console</span></span>

<span data-ttu-id="e5076-180">Visual Studio 2017 で NuGet と NuGet パッケージ マネージャーが自動的にインストールを選択するときにします。NET に関連するワークロードです。インストールすることも、個別にチェックして、**個々 のコンポーネント > コード ツール > の NuGet package manager** Visual Studio 2017 インストーラー オプション。</span><span class="sxs-lookup"><span data-stu-id="e5076-180">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="e5076-181">NuGet パッケージ マネージャー Visual Studio 2015 以前のバージョンで、欠落している場合は確認も、**ツール > 拡張機能と更新しています.** NuGet Package Manager 拡張機能を検索します。</span><span class="sxs-lookup"><span data-stu-id="e5076-181">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="e5076-182">直接、拡張機能をダウンロードするには Visual Studio での拡張機能インストーラーを使用することがない場合は、 [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-182">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="e5076-183">パッケージ マネージャー コンソールは Visual Studio for mac と共に現在使用できません。</span><span class="sxs-lookup"><span data-stu-id="e5076-183">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="e5076-184">同等のコマンドがを介して使用できる、 [NuGet CLI](nuget-exe-CLI-reference.md)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-184">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="e5076-185">Visual Studio for Mac は、NuGet パッケージを管理するための UI を持つはできます。</span><span class="sxs-lookup"><span data-stu-id="e5076-185">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="e5076-186">参照してください[などの NuGet パッケージ、プロジェクトの](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough)します。</span><span class="sxs-lookup"><span data-stu-id="e5076-186">See [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="e5076-187">パッケージ マネージャー コンソールは、Visual Studio のコードに含まれていません。</span><span class="sxs-lookup"><span data-stu-id="e5076-187">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="e5076-188">パッケージ マネージャー コンソールの拡張</span><span class="sxs-lookup"><span data-stu-id="e5076-188">Extending the Package Manager Console</span></span>

<span data-ttu-id="e5076-189">一部のパッケージは、コンソールの新しいコマンドをインストールします。</span><span class="sxs-lookup"><span data-stu-id="e5076-189">Some packages install new commands for the console.</span></span> <span data-ttu-id="e5076-190">たとえば、`MvcScaffolding`のようなコマンドを作成`Scaffold`次に示すを生成する ASP.NET MVC のコント ローラーとビュー。</span><span class="sxs-lookup"><span data-stu-id="e5076-190">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![インストールと MvcScaffold の使用](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="e5076-192">NuGet PowerShell プロファイルを設定します。</span><span class="sxs-lookup"><span data-stu-id="e5076-192">Setting up a NuGet PowerShell Profile</span></span>

<span data-ttu-id="e5076-193">PowerShell のプロファイルでは、PowerShell を使用する場合、一般的に使用されるコマンドを使用できるようにすることができます。</span><span class="sxs-lookup"><span data-stu-id="e5076-193">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="e5076-194">NuGet は、通常、次の場所で見つかった NuGet 固有のプロファイルをサポートします。</span><span class="sxs-lookup"><span data-stu-id="e5076-194">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="e5076-195">プロファイルを検索するには、次のように入力します。`$profile`コンソール。</span><span class="sxs-lookup"><span data-stu-id="e5076-195">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="e5076-196">詳細についてを参照してください[Windows PowerShell プロファイル](https://technet.microsoft.com/library/bb613488.aspx)です。</span><span class="sxs-lookup"><span data-stu-id="e5076-196">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>
