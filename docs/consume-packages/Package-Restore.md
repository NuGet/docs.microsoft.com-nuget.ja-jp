---
title: NuGet パッケージの復元
description: プロジェクトが依存しているパッケージを NuGet が復元する方法について概要を説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 0df2b0ebcf438fba99291558f1cf929dcb32618b
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316987"
---
# <a name="package-restore-options"></a><span data-ttu-id="66b10-103">パッケージの復元オプション</span><span class="sxs-lookup"><span data-stu-id="66b10-103">Package Restore options</span></span>

<span data-ttu-id="66b10-104">開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクト ファイルか `packages.config` に記載されているすべてのプロジェクトの依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="66b10-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="66b10-105">.NET Core 2.0+ の `dotnet build` コマンドと `dotnet run` コマンドでは、パッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="66b10-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="66b10-106">Visual Studio では、プロジェクトのビルド時、パッケージを自動的に復元できます。ユーザーは Visual Studio、`nuget restore`、`dotnet restore`、Mono の xbuild を利用し、いつでもパッケージを復元できます。</span><span class="sxs-lookup"><span data-stu-id="66b10-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="66b10-107">パッケージの復元によって、ソース コントロール内に格納しなくても、すべてのプロジェクトの依存関係が使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="66b10-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="66b10-108">パッケージ バイナリを除外するようにソース コントロール リポジトリを構成するには、[パッケージとソースの管理](../consume-packages/packages-and-source-control.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="66b10-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="66b10-109">パッケージの復元の概要</span><span class="sxs-lookup"><span data-stu-id="66b10-109">Package Restore overview</span></span>

<span data-ttu-id="66b10-110">パッケージの復元では、最初に、必要に応じて、プロジェクトの直接的な依存関係がインストールされます。この後、依存関係グラフ全体にパッケージの依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="66b10-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="66b10-111">パッケージがまだインストールされていない場合、NuGet は最初に、パッケージを[キャッシュ](../consume-packages/managing-the-global-packages-and-cache-folders.md)からのパッケージの取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="66b10-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="66b10-112">パッケージがキャッシュにない場合、NuGet は、Visual Studio で **[ツール]** 、 **[オプション]** 、 **[NuGet パッケージ マネージャー]** 、 **[パッケージ ソース]** の順に選択すると一覧表示される、すべての有効なソースからのパッケージのダウンロードを試みます。</span><span class="sxs-lookup"><span data-stu-id="66b10-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="66b10-113">復元時には、NuGet は、要求に最初に応答するソースのパッケージを使用し、パッケージ ソースの順序を無視します。</span><span class="sxs-lookup"><span data-stu-id="66b10-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="66b10-114">NuGet の動作については、[一般的な NuGet 構成](Configuring-NuGet-Behavior.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="66b10-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="66b10-115">NuGet では、すべてのソースがチェックされるまで、パッケージの復元の失敗が表示されません。</span><span class="sxs-lookup"><span data-stu-id="66b10-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="66b10-116">このとき、NuGet では一覧の最後のソースについてのみ障害が報告されます。</span><span class="sxs-lookup"><span data-stu-id="66b10-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="66b10-117">このエラーは、ソースごとに個別にエラーが表示されていなくても、パッケージが他のソースの*いずれ*にも存在しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="66b10-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

## <a name="restore-packages"></a><span data-ttu-id="66b10-118">パッケージの復元</span><span class="sxs-lookup"><span data-stu-id="66b10-118">Restore packages</span></span>

<span data-ttu-id="66b10-119">パッケージの復元は次のいずれかの方法で開始できます。</span><span class="sxs-lookup"><span data-stu-id="66b10-119">You can trigger Package Restore in any of the following ways:</span></span>

- <span data-ttu-id="66b10-120">**Visual Studio**:Windows の Visual Studio で、次のいずれかの方法を使用します。</span><span class="sxs-lookup"><span data-stu-id="66b10-120">**Visual Studio**: In Visual Studio on Windows, use one of the following methods.</span></span>

    - <span data-ttu-id="66b10-121">パッケージを自動的に復元する。</span><span class="sxs-lookup"><span data-stu-id="66b10-121">Restore packages automatically.</span></span> <span data-ttu-id="66b10-122">パッケージの復元は、テンプレートからプロジェクトを作成するとき、またはプロジェクトをビルドするときに、「[パッケージ復元の有効化と無効化](#enable-and-disable-package-restore-visual-studio)」に記載されているオプションに基づいて自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="66b10-122">Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore-visual-studio).</span></span> <span data-ttu-id="66b10-123">NuGet 4.0+ では、SDK スタイルのプロジェクト (通常は .NET Core または .NET Standard プロジェクト) の変更時にも復元が行われます。</span><span class="sxs-lookup"><span data-stu-id="66b10-123">In NuGet 4.0+, restore also happens automatically when you make changes to a SDK-style project (typically a .NET Core or .NET Standard project).</span></span>

    - <span data-ttu-id="66b10-124">パッケージを手動で復元する。</span><span class="sxs-lookup"><span data-stu-id="66b10-124">Restore packages manually.</span></span> <span data-ttu-id="66b10-125">手動で復元するには、**ソリューション エクスプローラー**でソリューションを右クリックして、 **[NuGet パッケージの復元]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="66b10-125">To restore manually, right-click the solution in **Solution Explorer** and select **Restore NuGet Packages**.</span></span> <span data-ttu-id="66b10-126">1 つまたは複数の個別パッケージが正しくインストールされていない場合、 **[ソリューション エクスプローラー]** にエラー アイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="66b10-126">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="66b10-127">右クリックして **[NuGet パッケージの管理]** を選択し、 **[パッケージ マネージャー]** を使用し、影響を受けるパッケージをアンインストールし、再インストールします。</span><span class="sxs-lookup"><span data-stu-id="66b10-127">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="66b10-128">詳細については、「[パッケージを再インストールして更新する](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="66b10-128">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

    <span data-ttu-id="66b10-129">"このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、[自動復元を有効にしてください](#enable-and-disable-package-restore-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="66b10-129">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-visual-studio).</span></span> <span data-ttu-id="66b10-130">また、[パッケージの自動復元への移行](#migrate-to-automatic-package-restore-visual-studio)および[パッケージの復元のトラブルシューティング](Package-restore-troubleshooting.md)に関するページもご覧ください。</span><span class="sxs-lookup"><span data-stu-id="66b10-130">Also, see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio) and [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

- <span data-ttu-id="66b10-131">**dotnet CLI**:コマンド ラインで、使用するプロジェクトが含まれているフォルダーに切り替えてから、[dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) コマンドを使用して、[PackageReference](../consume-packages/package-references-in-project-files.md) でプロジェクト ファイルに記載されているパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="66b10-131">**dotnet CLI**: In the command line, switch to the folder that contains your project, and then use the [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x) command to restore packages listed in the project file with [PackageReference](../consume-packages/package-references-in-project-files.md).</span></span> <span data-ttu-id="66b10-132">.NET Core 2.0 以降では、復元は `dotnet build` コマンドと `dotnet run` コマンドで自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="66b10-132">With .NET Core 2.0 and later, restore happens automatically with the `dotnet build` and `dotnet run` commands.</span></span>  

- <span data-ttu-id="66b10-133">**nuget.exe CLI**:コマンド ラインで、使用するプロジェクトが含まれているフォルダーに切り替えてから、[nuget restore](../reference/cli-reference/cli-ref-restore.md) コマンドを使用して、プロジェクトやソリューション ファイル、または　`packages.config` に記載されているパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="66b10-133">**nuget.exe CLI**: In the command line, switch to the folder that contains your project, and then use the [nuget restore](../reference/cli-reference/cli-ref-restore.md) command to restore packages listed in a project or solution file, or in `packages.config`.</span></span> 

- <span data-ttu-id="66b10-134">**MSBuild**:[msbuild -t:restore](../reference/msbuild-targets.md#restore-target) コマンドを使用して、PackageReference を使用するプロジェクト ファイルに一覧表示されているパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="66b10-134">**MSBuild**: Use the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command to restore packages listed in the project file with PackageReference.</span></span> <span data-ttu-id="66b10-135">このコマンドは、Visual Studio 2017 以降のバージョン含まれる NuGet 4.x+ と MSBuild 15.1+ でのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="66b10-135">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="66b10-136">`nuget restore` と `dotnet restore` の両方で、該当するプロジェクトにこのコマンドが使用されます。</span><span class="sxs-lookup"><span data-stu-id="66b10-136">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

- <span data-ttu-id="66b10-137">**Azure Pipelines**:Azure Pipelines でビルド定義を作成するとき、定義の中でビルド タスクの前に NuGet [復元](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages)または .NET Core [復元](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops)タスクを含めます。</span><span class="sxs-lookup"><span data-stu-id="66b10-137">**Azure Pipelines**: When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task in the definition before any build tasks.</span></span> <span data-ttu-id="66b10-138">一部のビルド テンプレートには、既定で復元タスクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="66b10-138">Some build templates include the restore task by default.</span></span>

- <span data-ttu-id="66b10-139">**Azure DevOps Server**:Azure DevOps Server と TFS 2013 以降では、TFS 2013 以降のチーム ビルド テンプレートを使用している場合、ビルド時にパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="66b10-139">**Azure DevOps Server**: Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="66b10-140">それより前の TFS バージョンの場合、コマンドラインで復元を実行するビルド ステップを含めたり、任意で、ビルド テンプレートを後続のバージョンに移行したりできます。</span><span class="sxs-lookup"><span data-stu-id="66b10-140">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="66b10-141">詳細については、[Team Foundation ビルドでパッケージ復元を設定する](../consume-packages/team-foundation-build.md)方法に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="66b10-141">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="enable-and-disable-package-restore-visual-studio"></a><span data-ttu-id="66b10-142">パッケージ復元の有効化と無効化 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="66b10-142">Enable and disable package restore (Visual Studio)</span></span>

<span data-ttu-id="66b10-143">Visual Studio では、パッケージ復元の管理は主に、 **[ツール]** 、 **[オプション]** 、 **[NuGet パッケージ マネージャー]** の順に選択して行います。</span><span class="sxs-lookup"><span data-stu-id="66b10-143">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![NuGet パッケージ マネージャーのオプションによるパッケージ復元の制御](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="66b10-145">**見つからないパッケージのダウンロードを NuGet に許可**: `NuGet.Config` ファイル (Windows では `%AppData%\NuGet\`、Mac/Linux では `~/.nuget/NuGet/`) の [packageRestore セクション](../reference/nuget-config-file.md#packagerestore-section)の `packageRestore/enabled` 設定を変更することによって、パッケージ復元のすべての形式を制御します。</span><span class="sxs-lookup"><span data-stu-id="66b10-145">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="66b10-146">また、この設定により、Visual Studio でソリューションのコンテキスト メニューの **[NuGet パッケージの復元]** コマンドが有効になります。</span><span class="sxs-lookup"><span data-stu-id="66b10-146">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

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
  > <span data-ttu-id="66b10-147">`packageRestore/enabled` 設定をグローバルにオーバーライドするには、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定します。</span><span class="sxs-lookup"><span data-stu-id="66b10-147">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="66b10-148">**Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: `NuGet.Config` ファイルの [packageRestore セクション](../reference/nuget-config-file.md#packagerestore-section)の `packageRestore/automatic` 設定を変更することにより、自動復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="66b10-148">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="66b10-149">このオプションを True に設定していると、Visual Studio からビルドを実行したとき、欠落しているパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="66b10-149">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="66b10-150">この設定が MSBuild コマンド ラインから実行されるビルドに影響を与えることはありません。</span><span class="sxs-lookup"><span data-stu-id="66b10-150">This setting doesn't affect builds run from the MSBuild command line.</span></span>

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

<span data-ttu-id="66b10-151">コンピューター上のすべてのユーザーに対してパッケージ復元を有効または無効にする目的で、開発者または会社は構成設定をグローバル `nuget.config` ファイルに追加できます。</span><span class="sxs-lookup"><span data-stu-id="66b10-151">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="66b10-152">グローバル `nuget.config` は Windows の `%ProgramData%\NuGet\Config` の特定の `\{IDE}\{Version}\{SKU}\` Visual Studio フォルダーにある場合があります。Mac/Linux の場合は `~/.local/share` です。</span><span class="sxs-lookup"><span data-stu-id="66b10-152">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="66b10-153">その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="66b10-153">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="66b10-154">NuGet で複数の構成ファイルに優先順位を付けるしくみについては、[共通 NuGet 構成](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="66b10-154">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="66b10-155">`nuget.config` で直接、`packageRestore` 設定を編集する場合、 **[オプション]** ダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="66b10-155">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="66b10-156">復元でパッケージ バージョンを制約する</span><span class="sxs-lookup"><span data-stu-id="66b10-156">Constrain package versions with restore</span></span>

<span data-ttu-id="66b10-157">NuGet で何らかの方法でパッケージを復元するとき、`packages.config` またはプロジェクト ファイルに指定した制約が適用されます。</span><span class="sxs-lookup"><span data-stu-id="66b10-157">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="66b10-158">`packages.config` では、依存関係の `allowedVersion` プロパティでバージョン範囲を指定できます。</span><span class="sxs-lookup"><span data-stu-id="66b10-158">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="66b10-159">詳細については、[アップグレード バージョンの制約](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="66b10-159">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="66b10-160">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="66b10-160">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="66b10-161">プロジェクト ファイルでは、PackageReference を使用し、依存関係の範囲を直接指定できます。</span><span class="sxs-lookup"><span data-stu-id="66b10-161">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="66b10-162">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="66b10-162">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="66b10-163">いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。</span><span class="sxs-lookup"><span data-stu-id="66b10-163">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="66b10-164">パッケージ ソースから強制的に復元する</span><span class="sxs-lookup"><span data-stu-id="66b10-164">Force restore from package sources</span></span>

<span data-ttu-id="66b10-165">[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)に関するページで説明されているように、既定では、NuGet の復元操作では、"*グローバル パッケージ*" フォルダーと "*HTTP キャッシュ*" フォルダーのパッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="66b10-165">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="66b10-166">"*グローバル パッケージ*" フォルダーの使用を回避するには、次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="66b10-166">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="66b10-167">`nuget locals global-packages -clear` または `dotnet nuget locals global-packages --clear` を使用して、フォルダーをクリアします。</span><span class="sxs-lookup"><span data-stu-id="66b10-167">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="66b10-168">次のいずれかの方法で、復元操作の前に "*グローバル パッケージ*" フォルダーの場所を一時的に変更します。</span><span class="sxs-lookup"><span data-stu-id="66b10-168">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="66b10-169">NUGET_PACKAGES 環境変数を別のフォルダーに設定する。</span><span class="sxs-lookup"><span data-stu-id="66b10-169">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="66b10-170">`globalPackagesFolder` (PackageReference を使用している場合) または `repositoryPath` (`packages.config` を使用している場合) を別のフォルダーに設定した `NuGet.Config` ファイルを作成する。</span><span class="sxs-lookup"><span data-stu-id="66b10-170">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="66b10-171">[構成設定](../reference/nuget-config-file.md#config-section)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="66b10-171">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="66b10-172">MSBuild のみ:`RestorePackagesPath` プロパティで別のフォルダーを指定する。</span><span class="sxs-lookup"><span data-stu-id="66b10-172">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="66b10-173">HTTP ソースのキャッシュの使用を回避するには、次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="66b10-173">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="66b10-174">`nuget restore` で `-NoCache` オプションを使用するか、`dotnet restore` で `--no-cache` オプションを使用する。</span><span class="sxs-lookup"><span data-stu-id="66b10-174">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="66b10-175">これらのオプションは、Visual Studio パッケージ マネージャーまたはコンソールを経由した復元操作には影響しません。</span><span class="sxs-lookup"><span data-stu-id="66b10-175">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="66b10-176">`nuget locals http-cache -clear` または `dotnet nuget locals http-cache --clear` を使用してキャッシュをクリアする。</span><span class="sxs-lookup"><span data-stu-id="66b10-176">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="66b10-177">一時的に NUGET_HTTP_CACHE_PATH 環境変数を別のフォルダーに設定する。</span><span class="sxs-lookup"><span data-stu-id="66b10-177">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="migrate-to-automatic-package-restore-visual-studio"></a><span data-ttu-id="66b10-178">パッケージの自動復元への移行 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="66b10-178">Migrate to automatic package restore (Visual Studio)</span></span>

<span data-ttu-id="66b10-179">NuGet 2.6 およびそれ以前では、以前は MSBuild に統合されたパッケージの復元がサポートされていましたが、現在ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="66b10-179">For NuGet 2.6 and earlier, an MSBuild-integrated package restore was previously supported but that is no longer true.</span></span> <span data-ttu-id="66b10-180">(これは通常、Visual Studio でソリューションを右クリックし、 **[NuGet パッケージの復元を有効にする]** を選択することで有効になりました)。</span><span class="sxs-lookup"><span data-stu-id="66b10-180">(It was typically enabled by right-clicking a solution in Visual Studio and selecting **Enable NuGet Package Restore**).</span></span> <span data-ttu-id="66b10-181">ご自身のプロジェクトで、非推奨の、MSBuild に統合されたパッケージの復元を使用する場合は、パッケージの自動復元に移行してください。</span><span class="sxs-lookup"><span data-stu-id="66b10-181">If your project uses the deprecated MSBuild-integrated package restore, please migrate to automatic package restore.</span></span>

<span data-ttu-id="66b10-182">MSBuild に統合されたパッケージの復元が使用されるプロジェクトには、通常、次の 3 つのファイルを含む *.nuget* フォルダーが含まれています:*NuGet.config*、*nuget.exe*、*NuGet.targets*。</span><span class="sxs-lookup"><span data-stu-id="66b10-182">Projects that use MSBuild-Integrated package restore typically contain a *.nuget* folder with three files: *NuGet.config*, *nuget.exe*, and *NuGet.targets*.</span></span> <span data-ttu-id="66b10-183">*NuGet.targets* ファイルの存在によって、NuGet で MSBuild に統合されたアプローチが引き続き使用されるかどうかが決まります。そのため、移行中にこのファイルを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="66b10-183">The presence of a *NuGet.targets* file determines whether NuGet will continue to use the MSBuild-untegrated approach, so this file must be removed during the migration.</span></span>

<span data-ttu-id="66b10-184">パッケージの自動復元に移行するには:</span><span class="sxs-lookup"><span data-stu-id="66b10-184">To migrate to automatic package restore:</span></span>

1. <span data-ttu-id="66b10-185">Visual Studio を閉じます。</span><span class="sxs-lookup"><span data-stu-id="66b10-185">Close Visual Studio.</span></span>
2. <span data-ttu-id="66b10-186">*.nuget/nuget.exe* と *.nuget/NuGet.targets* を削除します。</span><span class="sxs-lookup"><span data-stu-id="66b10-186">Delete *.nuget/nuget.exe* and *.nuget/NuGet.targets*.</span></span>
3. <span data-ttu-id="66b10-187">各プロジェクト ファイルごとに、`<RestorePackages>` 要素を削除し、*NuGet.targets* への参照をすべて削除します。</span><span class="sxs-lookup"><span data-stu-id="66b10-187">For each project file, remove the `<RestorePackages>` element and remove any reference to *NuGet.targets*.</span></span>

<span data-ttu-id="66b10-188">パッケージの自動復元をテストするには:</span><span class="sxs-lookup"><span data-stu-id="66b10-188">To test the automatic package restore:</span></span>

1. <span data-ttu-id="66b10-189">ソリューションから *packages* フォルダーを削除します。</span><span class="sxs-lookup"><span data-stu-id="66b10-189">Remove the *packages* folder from the solution.</span></span>
2. <span data-ttu-id="66b10-190">Visual Studio でソリューションを開き、ビルドを開始します。</span><span class="sxs-lookup"><span data-stu-id="66b10-190">Open the solution in Visual Studio and start a build.</span></span>

   <span data-ttu-id="66b10-191">パッケージの自動復元によって、各依存関係パッケージがダウンロードおよびインストールされ、それらがソース管理に追加されることはありません。</span><span class="sxs-lookup"><span data-stu-id="66b10-191">Automatic package restore should download and install each dependency package, without adding them to source control.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="66b10-192">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="66b10-192">Troubleshooting</span></span>

<span data-ttu-id="66b10-193">[パッケージの復元のトラブルシューティング](package-restore-troubleshooting.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="66b10-193">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
