---
title: NuGet パッケージの復元
description: プロジェクトが依存しているパッケージを NuGet が復元する方法について概要を説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 3b64c035886818496339fe1bdd8f9abce060278a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467797"
---
# <a name="package-restore"></a><span data-ttu-id="0c055-103">パッケージの復元</span><span class="sxs-lookup"><span data-stu-id="0c055-103">Package Restore</span></span>

<span data-ttu-id="0c055-104">開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクト ファイルか `packages.config` に記載されているすべてのプロジェクトの依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="0c055-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="0c055-105">.NET Core 2.0+ の `dotnet build` コマンドと `dotnet run` コマンドでは、パッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="0c055-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="0c055-106">Visual Studio では、プロジェクトのビルド時、パッケージを自動的に復元できます。ユーザーは Visual Studio、`nuget restore`、`dotnet restore`、Mono の xbuild を利用し、いつでもパッケージを復元できます。</span><span class="sxs-lookup"><span data-stu-id="0c055-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="0c055-107">パッケージの復元によって、ソース コントロール内に格納しなくても、すべてのプロジェクトの依存関係が使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="0c055-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="0c055-108">パッケージ バイナリを除外するようにソース コントロール リポジトリを構成するには、[パッケージとソースの管理](../consume-packages/packages-and-source-control.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c055-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="0c055-109">パッケージの復元の概要</span><span class="sxs-lookup"><span data-stu-id="0c055-109">Package Restore overview</span></span>

<span data-ttu-id="0c055-110">パッケージの復元では、最初に、必要に応じて、プロジェクトの直接的な依存関係がインストールされます。この後、依存関係グラフ全体にパッケージの依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="0c055-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="0c055-111">パッケージがまだインストールされていない場合、NuGet は最初に、パッケージを[キャッシュ](../consume-packages/managing-the-global-packages-and-cache-folders.md)からのパッケージの取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="0c055-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="0c055-112">パッケージがキャッシュにない場合、NuGet は、Visual Studio で **[ツール]** 、 **[オプション]** 、 **[NuGet パッケージ マネージャー]** 、 **[パッケージ ソース]** の順に選択すると一覧表示される、すべての有効なソースからのパッケージのダウンロードを試みます。</span><span class="sxs-lookup"><span data-stu-id="0c055-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="0c055-113">復元時には、NuGet は、要求に最初に応答するソースのパッケージを使用し、パッケージ ソースの順序を無視します。</span><span class="sxs-lookup"><span data-stu-id="0c055-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="0c055-114">NuGet の動作については、[一般的な NuGet 構成](Configuring-NuGet-Behavior.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c055-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="0c055-115">NuGet では、すべてのソースがチェックされるまで、パッケージの復元の失敗が表示されません。</span><span class="sxs-lookup"><span data-stu-id="0c055-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="0c055-116">このとき、NuGet では一覧の最後のソースについてのみ障害が報告されます。</span><span class="sxs-lookup"><span data-stu-id="0c055-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="0c055-117">このエラーは、ソースごとに個別にエラーが表示されていなくても、パッケージが他のソースの*いずれ*にも存在しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="0c055-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

<span data-ttu-id="0c055-118">パッケージの復元は次のいずれかの方法で開始できます。</span><span class="sxs-lookup"><span data-stu-id="0c055-118">You can trigger Package Restore in any of the following ways:</span></span>

- <span data-ttu-id="0c055-119">**dotnet CLI**:[dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用して、[PackageReference](../consume-packages/package-references-in-project-files.md) を使用するプロジェクト ファイルに一覧表示されたパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="0c055-119">**dotnet CLI**: Use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command to restore packages listed in the project file with [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span> <span data-ttu-id="0c055-120">.NET Core 2.0 以降では、復元は `dotnet build` コマンドと `dotnet run` コマンドで自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="0c055-120">With .NET Core 2.0 and later, restore happens automatically with the `dotnet build` and `dotnet run` commands.</span></span>  

- <span data-ttu-id="0c055-121">**パッケージ マネージャー**:Windows の Visual Studio では、パッケージの復元は、「[パッケージ復元の有効化と無効化](#enable-and-disable-package-restore)」のオプションに基づき、テンプレートからプロジェクトを作成するとき、あるいはプロジェクトをビルドするときに自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="0c055-121">**Package Manager**: In Visual Studio on Windows, Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore).</span></span> <span data-ttu-id="0c055-122">NuGet 4.0+ では、.NET Core SDK ベースのプロジェクトの変更時にも復元が行われます。</span><span class="sxs-lookup"><span data-stu-id="0c055-122">In NuGet 4.0+, restore also happens automatically when you make changes to a .NET Core SDK-based project.</span></span>

    <span data-ttu-id="0c055-123">パッケージを手動で復元するには、 **[ソリューション エクスプローラー]** でソリューションを右クリックし、 **[NuGet パッケージの復元]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="0c055-123">To restore packages manually, right-click the solution in **Solution Explorer** and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="0c055-124">1 つまたは複数の個別パッケージが正しくインストールされていない場合、 **[ソリューション エクスプローラー]** にエラー アイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="0c055-124">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="0c055-125">右クリックして **[NuGet パッケージの管理]** を選択し、 **[パッケージ マネージャー]** を使用し、影響を受けるパッケージをアンインストールし、再インストールします。</span><span class="sxs-lookup"><span data-stu-id="0c055-125">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="0c055-126">詳細については、「[パッケージを再インストールして更新する](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c055-126">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="0c055-127">"このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、[自動復元を有効にしてください](#enable-and-disable-package-restore)。</span><span class="sxs-lookup"><span data-stu-id="0c055-127">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore).</span></span> <span data-ttu-id="0c055-128">[パッケージの復元のトラブルシューティング](Package-restore-troubleshooting.md)に関するページもご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c055-128">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="0c055-129">**nuget.exe CLI**:[nuget restore](../tools/cli-ref-restore.md) コマンドを使用し、プロジェクト ファイル、ソリューション ファイル、または `packages.config` に一覧表示されるパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="0c055-129">**nuget.exe CLI**: Use the [nuget restore](../tools/cli-ref-restore.md) command to restore packages listed in a project or solution file, or in `packages.config`.</span></span> 

- <span data-ttu-id="0c055-130">**MSBuild**:[msbuild -t:restore](../reference/msbuild-targets.md#restore-target) コマンドを使用して、PackageReference を使用するプロジェクト ファイルに一覧表示されているパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="0c055-130">**MSBuild**: Use the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command to restore packages listed in the project file with PackageReference.</span></span> <span data-ttu-id="0c055-131">このコマンドは、Visual Studio 2017 以降のバージョン含まれる NuGet 4.x+ と MSBuild 15.1+ でのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="0c055-131">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="0c055-132">`nuget restore` と `dotnet restore` の両方で、該当するプロジェクトにこのコマンドが使用されます。</span><span class="sxs-lookup"><span data-stu-id="0c055-132">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

- <span data-ttu-id="0c055-133">**Azure Pipelines**:Azure Pipelines でビルド定義を作成するとき、定義の中でビルド タスクの前に NuGet [復元](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages)または .NET Core [復元](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages)タスクを含めます。</span><span class="sxs-lookup"><span data-stu-id="0c055-133">**Azure Pipelines**: When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core#restore-nuget-packages) task in the definition before any build tasks.</span></span> <span data-ttu-id="0c055-134">一部のビルド テンプレートには、既定で復元タスクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0c055-134">Some build templates include the restore task by default.</span></span>

- <span data-ttu-id="0c055-135">**Azure DevOps Server**:Azure DevOps Server と TFS 2013 以降では、TFS 2013 以降のチーム ビルド テンプレートを使用している場合、ビルド時にパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="0c055-135">**Azure DevOps Server**: Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="0c055-136">それより前の TFS バージョンの場合、コマンドラインで復元を実行するビルド ステップを含めたり、任意で、ビルド テンプレートを後続のバージョンに移行したりできます。</span><span class="sxs-lookup"><span data-stu-id="0c055-136">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="0c055-137">詳細については、[Team Foundation ビルドでパッケージ復元を設定する](../consume-packages/team-foundation-build.md)方法に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="0c055-137">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enable-and-disable-package-restore"></a><span data-ttu-id="0c055-138">パッケージ復元の有効化と無効化</span><span class="sxs-lookup"><span data-stu-id="0c055-138">Enable and disable package restore</span></span>

<span data-ttu-id="0c055-139">Visual Studio では、パッケージ復元の管理は主に、 **[ツール]** 、 **[オプション]** 、 **[NuGet パッケージ マネージャー]** の順に選択して行います。</span><span class="sxs-lookup"><span data-stu-id="0c055-139">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![NuGet パッケージ マネージャーのオプションによるパッケージ復元の制御](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="0c055-141">**見つからないパッケージのダウンロードを NuGet に許可**: `NuGet.Config` ファイル (Windows では `%AppData%\NuGet\`、Mac/Linux では `~/.nuget/NuGet/`) の [packageRestore セクション](../reference/nuget-config-file.md#packagerestore-section)の `packageRestore/enabled` 設定を変更することによって、パッケージ復元のすべての形式を制御します。</span><span class="sxs-lookup"><span data-stu-id="0c055-141">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="0c055-142">また、この設定により、Visual Studio でソリューションのコンテキスト メニューの **[NuGet パッケージの復元]** コマンドが有効になります。</span><span class="sxs-lookup"><span data-stu-id="0c055-142">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

    ```xml
    <configuration>
        <packageRestore>
            <!-- The 'enabled' key is True when the "Allow NuGet to download missing packages" checkbox is set.
                 Clearing the box sets this to False, disabling command-line, automatic, and MSBuild-integrated restore. -->
            <add key="enabled" value="True" />
        </packageRestore>
    </configuration>
    ```
    
  > [!Note]
  > <span data-ttu-id="0c055-143">`packageRestore/enabled` 設定をグローバルにオーバーライドするには、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定します。</span><span class="sxs-lookup"><span data-stu-id="0c055-143">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="0c055-144">**Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: `NuGet.Config` ファイルの [packageRestore セクション](../reference/nuget-config-file.md#packagerestore-section)の `packageRestore/automatic` 設定を変更することにより、自動復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="0c055-144">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="0c055-145">このオプションを True に設定していると、Visual Studio からビルドを実行したとき、欠落しているパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="0c055-145">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="0c055-146">この設定が MSBuild コマンド ラインから実行されるビルドに影響を与えることはありません。</span><span class="sxs-lookup"><span data-stu-id="0c055-146">This setting doesn't affect builds run from the MSBuild command line.</span></span>

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

<span data-ttu-id="0c055-147">コンピューター上のすべてのユーザーに対してパッケージ復元を有効または無効にする目的で、開発者または会社は構成設定をグローバル `nuget.config` ファイルに追加できます。</span><span class="sxs-lookup"><span data-stu-id="0c055-147">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="0c055-148">グローバル `nuget.config` は Windows の `%ProgramData%\NuGet\Config` の特定の `\{IDE}\{Version}\{SKU}\` Visual Studio フォルダーにある場合があります。Mac/Linux の場合は `~/.local/share` です。</span><span class="sxs-lookup"><span data-stu-id="0c055-148">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="0c055-149">その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="0c055-149">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="0c055-150">NuGet で複数の構成ファイルに優先順位を付けるしくみについては、[共通 NuGet 構成](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c055-150">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="0c055-151">`nuget.config` で直接、`packageRestore` 設定を編集する場合、 **[オプション]** ダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="0c055-151">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="0c055-152">復元でパッケージ バージョンを制約する</span><span class="sxs-lookup"><span data-stu-id="0c055-152">Constrain package versions with restore</span></span>

<span data-ttu-id="0c055-153">NuGet で何らかの方法でパッケージを復元するとき、`packages.config` またはプロジェクト ファイルに指定した制約が適用されます。</span><span class="sxs-lookup"><span data-stu-id="0c055-153">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="0c055-154">`packages.config` では、依存関係の `allowedVersion` プロパティでバージョン範囲を指定できます。</span><span class="sxs-lookup"><span data-stu-id="0c055-154">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="0c055-155">詳細については、[アップグレード バージョンの制約](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c055-155">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="0c055-156">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0c055-156">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="0c055-157">プロジェクト ファイルでは、PackageReference を使用し、依存関係の範囲を直接指定できます。</span><span class="sxs-lookup"><span data-stu-id="0c055-157">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="0c055-158">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="0c055-158">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="0c055-159">いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。</span><span class="sxs-lookup"><span data-stu-id="0c055-159">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="0c055-160">パッケージ ソースから強制的に復元する</span><span class="sxs-lookup"><span data-stu-id="0c055-160">Force restore from package sources</span></span>

<span data-ttu-id="0c055-161">[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)に関するページで説明されているように、既定では、NuGet の復元操作では、"*グローバル パッケージ*" フォルダーと "*HTTP キャッシュ*" フォルダーのパッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="0c055-161">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="0c055-162">"*グローバル パッケージ*" フォルダーの使用を回避するには、次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="0c055-162">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="0c055-163">`nuget locals global-packages -clear` または `dotnet nuget locals global-packages --clear` を使用して、フォルダーをクリアします。</span><span class="sxs-lookup"><span data-stu-id="0c055-163">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="0c055-164">次のいずれかの方法で、復元操作の前に "*グローバル パッケージ*" フォルダーの場所を一時的に変更します。</span><span class="sxs-lookup"><span data-stu-id="0c055-164">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="0c055-165">NUGET_PACKAGES 環境変数を別のフォルダーに設定する。</span><span class="sxs-lookup"><span data-stu-id="0c055-165">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="0c055-166">`globalPackagesFolder` (PackageReference を使用している場合) または `repositoryPath` (`packages.config` を使用している場合) を別のフォルダーに設定した `NuGet.Config` ファイルを作成する。</span><span class="sxs-lookup"><span data-stu-id="0c055-166">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="0c055-167">[構成設定](../reference/nuget-config-file.md#config-section)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c055-167">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="0c055-168">MSBuild のみ:`RestorePackagesPath` プロパティで別のフォルダーを指定する。</span><span class="sxs-lookup"><span data-stu-id="0c055-168">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="0c055-169">HTTP ソースのキャッシュの使用を回避するには、次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="0c055-169">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="0c055-170">`nuget restore` で `-NoCache` オプションを使用するか、`dotnet restore` で `--no-cache` オプションを使用する。</span><span class="sxs-lookup"><span data-stu-id="0c055-170">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="0c055-171">これらのオプションは、Visual Studio パッケージ マネージャーまたはコンソールを経由した復元操作には影響しません。</span><span class="sxs-lookup"><span data-stu-id="0c055-171">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="0c055-172">`nuget locals http-cache -clear` または `dotnet nuget locals http-cache --clear` を使用してキャッシュをクリアする。</span><span class="sxs-lookup"><span data-stu-id="0c055-172">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="0c055-173">一時的に NUGET_HTTP_CACHE_PATH 環境変数を別のフォルダーに設定する。</span><span class="sxs-lookup"><span data-stu-id="0c055-173">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="0c055-174">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="0c055-174">Troubleshooting</span></span>

<span data-ttu-id="0c055-175">[パッケージの復元のトラブルシューティング](package-restore-troubleshooting.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="0c055-175">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
