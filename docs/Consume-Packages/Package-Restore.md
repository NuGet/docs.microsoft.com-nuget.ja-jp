---
title: "NuGet パッケージの復元 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "プロジェクトが依存しているパッケージを NuGet が復元する方法について概要を説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。"
keywords: "NuGet パッケージの復元, NuGet パッケージのインストール, パッケージのインストール, パッケージの復元, 依存関係のバージョン, 自動復元の無効化, パッケージのバージョンの制約"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 761ef86a70e0a681449dc9fe86d6a52ac2b19bb1
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="package-restore"></a><span data-ttu-id="b58cb-104">パッケージの復元</span><span class="sxs-lookup"><span data-stu-id="b58cb-104">Package Restore</span></span>

<span data-ttu-id="b58cb-105">開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクトがビルドされる前に、参照されているすべてのパッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="b58cb-106">&mdash;Visual Studio、.NET Core 2.0 以降、および Mono の xbuild で利用できる&mdash;、この広く使用されている機能により、これらのパッケージをソース管理に格納しなくても、すべての依存関係をプロジェクトで利用できます (パッケージのバイナリを除外するようにリポジトリを構成する方法については、「[パッケージとソース管理](../consume-packages/packages-and-source-control.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="b58cb-106">This widely-used feature&mdash;available in Visual Studio, .NET Core 2.0+, and xbuild on Mono&mdash;ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span> <span data-ttu-id="b58cb-107">パッケージは、いつでも手動で復元できます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-107">You can also manually restore packages at any time.</span></span>

<span data-ttu-id="b58cb-108">ビルド サーバーでのパッケージの復元について詳しくは、[TFBuild でのパッケージの復元](../consume-packages/team-foundation-build.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b58cb-108">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="b58cb-109">パッケージの復元の概要</span><span class="sxs-lookup"><span data-stu-id="b58cb-109">Package restore overview</span></span>

<span data-ttu-id="b58cb-110">パッケージの復元では、最初に、必要に応じて、プロジェクトの直接的な依存関係がインストールされます。この後、依存関係グラフ全体にパッケージの依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-110">Restoring packages first installs the direct dependencies of a project as needed, then installing any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="b58cb-111">パッケージがまだインストールされていない場合、NuGet は最初に、パッケージを[キャッシュ](../consume-packages/managing-the-nuget-cache.md)からのパッケージの取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-111">If a package is not already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="b58cb-112">パッケージがキャッシュにない場合、NuGet は有効なすべてのソースからパッケージをダウンロード (およびキャッシュ) しようとします (「[Configuring NuGet behavior](Configuring-NuGet-Behavior.md)」(NuGet の動作を構成する) を参照してください。ソースは Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [パッケージ ソース]** リストにも表示されます)。</span><span class="sxs-lookup"><span data-stu-id="b58cb-112">If the package is not in the cache, NuGet then attempts to download (and cache) the package from all enabled sources (see [Configuring NuGet behavior](Configuring-NuGet-Behavior.md)); sources also appear in the  **Tools > Options > NuGet Package Manager > Package Sources** list in Visual Studio).</span></span> <span data-ttu-id="b58cb-113">NuGet は、要求に最初に応答するソースのパッケージを使用して、パッケージ ソースの順序を無視します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-113">NuGet ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span>

> [!Note]
> <span data-ttu-id="b58cb-114">NuGet では、すべてのソースがチェックされるまで、パッケージの復元の失敗が表示されません。</span><span class="sxs-lookup"><span data-stu-id="b58cb-114">NuGet does not indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="b58cb-115">このとき、NuGet では一覧の最後のソースについてのみ障害が報告されます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-115">At that time, NuGet reports the failure for only the last source in the list.</span></span> <span data-ttu-id="b58cb-116">このエラーは、ソースごとに個別にエラーが表示されていなくても、パッケージが他のソースの*いずれ*にも存在しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-116">The error implies that the package wasn't present on *any* of the other sources, even though errors are not shown for each of those sources individually.</span></span>

<span data-ttu-id="b58cb-117">パッケージの復元は、次の方法でトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-117">Package restore is triggered in the following ways:</span></span>

- <span data-ttu-id="b58cb-118">**dotnet CLI**: [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用します。このコマンドは、プロジェクト ファイルに列記されたパッケージを復元します (「[PackageReference](../consume-packages/package-references-in-project-files.md)」 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="b58cb-118">**dotnet CLI**: use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="b58cb-119">.NET Core 2.0 以降では、復元は、`dotnet build` と `dotnet run` で自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-119">With .NET Core 2.0 and later, restore is done automatically with `dotnet build` and `dotnet run`.</span></span>

- <span data-ttu-id="b58cb-120">**パッケージ マネージャー UI (Windows 上の Visual Studio)**: プロジェクトは、テンプレートから作成されとき、およびビルドされたときに自動的に復元されます (ただし、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」で説明するオプションに基づきます)。</span><span class="sxs-lookup"><span data-stu-id="b58cb-120">**Package Manager UI (Visual Studio on Windows)**: Packages are restored automatically when creating a project from a template and when building a project (subject to the option described in [Enabling and disabling package restore](#enabling-and-disabling-package-restore)).</span></span> <span data-ttu-id="b58cb-121">NuGet 4.0 以降では、NET Core SDK ベースのプロジェクトを変更した場合も復元が自動的に発生します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-121">In NuGet 4.0+, restore also happens automatically when changes are made to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="b58cb-122">手動で復元するには、ソリューション エクスプローラーでソリューションを右クリックして、**[NuGet パッケージの復元]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-122">To restore manually, right-click the solution in Solution Explorer and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="b58cb-123">1 つ以上の個別のパッケージが、まだ適切にインストールされない場合 (ソリューション エクスプローラーにエラー アイコンが表示されます)、パッケージ マネージャー UI を使用して、影響を受けるパッケージをアンインストールし、再インストールします。</span><span class="sxs-lookup"><span data-stu-id="b58cb-123">If one or more individual packages are still not installed properly (meaning that Solution Explorer shows an error icon), then use the Package Manager UI to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="b58cb-124">「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b58cb-124">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="b58cb-125">"このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」の手順に従って、自動復元を有効にしてください。</span><span class="sxs-lookup"><span data-stu-id="b58cb-125">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

- <span data-ttu-id="b58cb-126">**NuGet CLI**: [nuget restore](../tools/cli-ref-restore.md) コマンドを使用します。このコマンドは、プロジェクト ファイル (「[PackageReference](../consume-packages/package-references-in-project-files.md)」 を参照) または [packages.config](../reference/packages-config.md) に列記されたパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-126">**NuGet CLI**: use the [nuget restore](../tools/cli-ref-restore.md) command, which restores packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)) or in a [packages.config](../reference/packages-config.md) file.</span></span> <span data-ttu-id="b58cb-127">ソリューション ファイルを指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-127">You can also specify a solution file.</span></span>

- <span data-ttu-id="b58cb-128">**MSBuild**: [msbuild /t:restore](../reference/msbuild-targets.md#restore-target)コマンドを使用します。このコマンドは、プロジェクト ファイルに列記されたパッケージを復元します (「[PackageReference](../consume-packages/package-references-in-project-files.md)」 を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="b58cb-128">**MSBuild**: use the [msbuild /t:restore](../reference/msbuild-targets.md#restore-target) command, which restores packages packages listed in the project file (see [PackageReference](../consume-packages/package-references-in-project-files.md)).</span></span> <span data-ttu-id="b58cb-129">NuGet 4.x 以降および MSBuild 15.1 以降でのみ使用できます。これらは、Visual Studio 2017 に含まれています。</span><span class="sxs-lookup"><span data-stu-id="b58cb-129">Available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017.</span></span> <span data-ttu-id="b58cb-130">`nuget restore` と `dotnet restore` はどちらも、このコマンドを該当するプロジェクトに使います。</span><span class="sxs-lookup"><span data-stu-id="b58cb-130">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span>

- <span data-ttu-id="b58cb-131">**Visual Studio Team Services**: Team Services でビルド定義を作成する場合、ビルド タスクの前に、[NuGet の復元](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) タスクまたは [.NET Core の復元](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages)タスクが定義に追加されます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-131">**Visual Studio Team Services**: When creating a build definition on Team Services, include the [NuGet restore](/vsts/build-release/tasks/package/nuget#restore-nuget-packages) or [.NET Core Restore](/vsts/build-release/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build task.</span></span> <span data-ttu-id="b58cb-132">このタスクは、多くのビルド テンプレートに既定で含まれます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-132">This task is included by default in a number of build templates.</span></span>

- <span data-ttu-id="b58cb-133">**Team Foundation Server**: TFS 2013 以降では、TFS 2013 以降用のチーム ビルド テンプレートを使用していれば、ビルド時にパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-133">**Team Foundation Server**: TFS 2013 and later automatically restores packages during build, provided that you're using a Team Build Template for TFS 2013 or later.</span></span> <span data-ttu-id="b58cb-134">以前のバージョンの TFS では、前に説明したように、ビルド ステップを含めるだけでコマンド ラインの復元オプションのいずれかを呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-134">For earlier version of TFS, you can include a build step to invoke one of the command-line restore options above.</span></span> <span data-ttu-id="b58cb-135">必要に応じて、ビルド テンプレートを TFS 2013 に移行できます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-135">You can optionally migrate the build template to TFS 2013.</span></span> <span data-ttu-id="b58cb-136">詳細については、[Team Foundation ビルドでのパッケージの復元](../consume-packages/team-foundation-build.md)に関するチュートリアルをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b58cb-136">For more information, see the [Walkthrough of package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="b58cb-137">パッケージの復元の有効化と無効化</span><span class="sxs-lookup"><span data-stu-id="b58cb-137">Enabling and disabling package restore</span></span>

<span data-ttu-id="b58cb-138">パッケージの復元を有効にするには、主に Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー]** を使います。</span><span class="sxs-lookup"><span data-stu-id="b58cb-138">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![NuGet パッケージ マネージャーのオプションによるパッケージ復元動作の制御](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="b58cb-140">**見つからないパッケージのダウンロードを NuGet に許可**: 次に示すように、`NuGet.Config` ファイル (Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) の `packageRestore/enabled` の設定を変更することによって、パッケージ復元のすべての形式を制御します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-140">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="b58cb-141">Visual Studio では、この設定を使用して、ソリューションのコンテキスト メニューの **[NuGet パッケージの復元]** コマンドを実行できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b58cb-141">In Visual Studio, this setting allows the **Restore NuGet Packages** command on the solution's context menu to work.</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-Integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    <br/>
    > [!Note]
    >  <span data-ttu-id="b58cb-142">`packageRestore/enabled` の設定は、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定することにより、グローバルに上書きできます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-142">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="b58cb-143">**Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: 次に示すように、`NuGet.Config` ファイル (Windows では `%AppData%\NuGet\NuGet.Config`、Mac/Linux では `~/.nuget/NuGet/NuGet.Config`) の `packageRestore/automatic` 設定を変更することにより、自動復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-143">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore by changing the `packageRestore/automatic` setting in the `NuGet.Config` file as shown below (`%AppData%\NuGet\NuGet.Config` on Windows, `~/.nuget/NuGet/NuGet.Config` on Mac/Linux).</span></span> <span data-ttu-id="b58cb-144">このオプションをオンにして Visual Studio からビルドを実行すると、欠落しているパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-144">When this option is set, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="b58cb-145">このオプションは、MSBuild を使用してコマンド ラインから実行されるビルドには影響しません。</span><span class="sxs-lookup"><span data-stu-id="b58cb-145">The option does not affect builds run from the command line using MSBuild.</span></span>

    ```xml
    ...
    <configuration>
        <packageRestore>
            <!-- The 'automatic' key is set to True when the "Automatically check for missing packages during
                 build in Visual Studio" checkbox is set. Clearing the box sets this to False and disables
                 automatic restore. -->
            <add key="automatic" value="True" />
        </packageRestore>
    </configuration>
    ```

<span data-ttu-id="b58cb-146">詳しくは、「NuGet config file」(NuGet config ファイル) の「[packageRestore section](../reference/nuget-config-file.md#packagerestore-section)」(packageRestore セクション) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b58cb-146">For reference, see the [NuGet config file - packageRestore section](../reference/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="b58cb-147">開発者や会社が、すべてのユーザーに対して、コンピューターでのパッケージの復元を有効または無効にすることが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="b58cb-147">In some cases, a developer or company might want to enable or disable package restore for all users on a computer.</span></span> <span data-ttu-id="b58cb-148">これは、前述の設定と同じ設定を、`%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` にあるグローバルな NuGet 構成ファイルに追加することによって実現できます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-148">This is done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="b58cb-149">その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="b58cb-149">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="b58cb-150">NuGet が複数の構成ファイルの優先順位を決定する方法の詳細については、「[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b58cb-150">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="b58cb-151">復元でのパッケージのバージョンの制約</span><span class="sxs-lookup"><span data-stu-id="b58cb-151">Constraining package versions with restore</span></span>

<span data-ttu-id="b58cb-152">NuGet は、いずれかの方法でパッケージを復元する際、`packages.config`またはプロジェクト ファイルで指定されている制約に従います。</span><span class="sxs-lookup"><span data-stu-id="b58cb-152">When restoring packages through any method, NuGet honors any constraints specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="b58cb-153">`packages.config`: 依存関係の `allowedVersion` プロパティでバージョンの範囲を指定します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-153">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="b58cb-154">「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b58cb-154">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="b58cb-155">例:</span><span class="sxs-lookup"><span data-stu-id="b58cb-155">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="b58cb-156">PackageReference: 依存関係のバージョン番号でバージョンの範囲を直接指定します。</span><span class="sxs-lookup"><span data-stu-id="b58cb-156">PackageReference: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="b58cb-157">例:</span><span class="sxs-lookup"><span data-stu-id="b58cb-157">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="b58cb-158">いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。</span><span class="sxs-lookup"><span data-stu-id="b58cb-158">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b58cb-159">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="b58cb-159">Troubleshooting</span></span>

<span data-ttu-id="b58cb-160">[パッケージの復元のトラブルシューティング](package-restore-troubleshooting.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b58cb-160">See [Troubleshooting package restore](package-restore-troubleshooting.md).</span></span>