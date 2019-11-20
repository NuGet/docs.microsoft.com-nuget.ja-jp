---
title: NuGet パッケージの復元
description: プロジェクトが依存しているパッケージを NuGet が復元する方法について概要を説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: 93a94a5468b48179d27b89825cebf2447657c8f2
ms.sourcegitcommit: 7c9f157ba02d9be543de34ab06813ab1ec10192a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/23/2019
ms.locfileid: "69999984"
---
# <a name="restore-packages-using-package-restore"></a><span data-ttu-id="c05ca-103">[パッケージの復元] を使用したパッケージの復元</span><span class="sxs-lookup"><span data-stu-id="c05ca-103">Restore packages using Package Restore</span></span>

<span data-ttu-id="c05ca-104">開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクト ファイルか `packages.config` に記載されているすべてのプロジェクトの依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c05ca-104">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all of a project's dependencies listed in either the project file or `packages.config`.</span></span> <span data-ttu-id="c05ca-105">.NET Core 2.0+ の `dotnet build` コマンドと `dotnet run` コマンドでは、パッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-105">The .NET Core 2.0+ `dotnet build` and `dotnet run` commands do an automatic package restore.</span></span> <span data-ttu-id="c05ca-106">Visual Studio では、プロジェクトのビルド時、パッケージを自動的に復元できます。ユーザーは Visual Studio、`nuget restore`、`dotnet restore`、Mono の xbuild を利用し、いつでもパッケージを復元できます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-106">Visual Studio can restore packages automatically when it builds a project, and you can restore packages at any time through Visual Studio, `nuget restore`, `dotnet restore`, and xbuild on Mono.</span></span>

<span data-ttu-id="c05ca-107">パッケージの復元によって、ソース コントロール内に格納しなくても、すべてのプロジェクトの依存関係が使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="c05ca-107">Package Restore makes sure that all a project's dependencies are available, without having to store them in source control.</span></span> <span data-ttu-id="c05ca-108">パッケージ バイナリを除外するようにソース コントロール リポジトリを構成するには、[パッケージとソースの管理](../consume-packages/packages-and-source-control.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-108">To configure your source control repository to exclude the package binaries, see [Packages and source control](../consume-packages/packages-and-source-control.md).</span></span> 

## <a name="package-restore-overview"></a><span data-ttu-id="c05ca-109">パッケージの復元の概要</span><span class="sxs-lookup"><span data-stu-id="c05ca-109">Package Restore overview</span></span>

<span data-ttu-id="c05ca-110">パッケージの復元では、最初に、必要に応じて、プロジェクトの直接的な依存関係がインストールされます。この後、依存関係グラフ全体にパッケージの依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-110">Package Restore first installs the direct dependencies of a project as needed, then installs any dependencies of those packages throughout the entire dependency graph.</span></span>

<span data-ttu-id="c05ca-111">パッケージがまだインストールされていない場合、NuGet は最初に、[キャッシュ](../consume-packages/managing-the-global-packages-and-cache-folders.md)からパッケージの取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-111">If a package isn't already installed, NuGet first attempts to retrieve it from the [cache](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> <span data-ttu-id="c05ca-112">パッケージがキャッシュにない場合、NuGet は、Visual Studio で **[ツール]** 、 **[オプション]** 、 **[NuGet パッケージ マネージャー]** 、 **[パッケージ ソース]** の順に選択すると一覧表示される、すべての有効なソースからのパッケージのダウンロードを試みます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-112">If the package isn't in the cache, NuGet tries to download the package from all enabled sources in the list at **Tools** > **Options** > **NuGet Package Manager** > **Package Sources** in Visual Studio.</span></span> <span data-ttu-id="c05ca-113">復元時には、NuGet は、要求に最初に応答するソースのパッケージを使用し、パッケージ ソースの順序を無視します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-113">During restore, NuGet ignores the order of package sources, and uses the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="c05ca-114">NuGet の動作については、[一般的な NuGet 構成](Configuring-NuGet-Behavior.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-114">For more information about how NuGet behaves, see [Common NuGet configurations](Configuring-NuGet-Behavior.md).</span></span> 

> [!Note]
> <span data-ttu-id="c05ca-115">NuGet では、すべてのソースがチェックされるまで、パッケージの復元の失敗が表示されません。</span><span class="sxs-lookup"><span data-stu-id="c05ca-115">NuGet doesn't indicate a failure to restore a package until all the sources have been checked.</span></span> <span data-ttu-id="c05ca-116">このとき、NuGet では一覧の最後のソースについてのみ障害が報告されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-116">At that time, NuGet reports a failure for only the last source in the list.</span></span> <span data-ttu-id="c05ca-117">このエラーは、ソースごとに個別にエラーが表示されていなくても、パッケージが他のソースの*いずれ*にも存在しないことを意味します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-117">The error implies that the package wasn't present on *any* of the other sources, even though errors aren't shown for each of those sources individually.</span></span>

## <a name="restore-packages"></a><span data-ttu-id="c05ca-118">パッケージの復元</span><span class="sxs-lookup"><span data-stu-id="c05ca-118">Restore packages</span></span>

<span data-ttu-id="c05ca-119">[パッケージの復元] では、プロジェクト ファイル ( *.csproj*) のパッケージ参照か *packages.config* ファイルに一致する正しい状態になるよう、すべてのパッケージの依存関係のインストールを試みます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-119">Package Restore tries to install all package dependencies to the correct state matching the package references in your project file (*.csproj*) or your *packages.config* file.</span></span> <span data-ttu-id="c05ca-120">(Visual Studio では、参照は **[依存関係] \ [NuGet]** または **[参照]** ノードの下にあるソリューション エクスプローラーに表示されます。)</span><span class="sxs-lookup"><span data-stu-id="c05ca-120">(In Visual Studio, the references appear in Solution Explorer under the **Dependencies \ NuGet** or the **References** node.)</span></span>

1. <span data-ttu-id="c05ca-121">プロジェクト ファイルのパッケージ参照が正しい場合は、好みのツールを使用してパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-121">If the package references in your project file are correct, use your preferred tool to restore packages.</span></span>

   - <span data-ttu-id="c05ca-122">[Visual Studio](#restore-using-visual-studio) ([自動復元](#restore-packages-automatically-using-visual-studio)または[手動復元](#restore-packages-manually-using-visual-studio))</span><span class="sxs-lookup"><span data-stu-id="c05ca-122">[Visual Studio](#restore-using-visual-studio) ([automatic restore](#restore-packages-automatically-using-visual-studio) or [manual restore](#restore-packages-manually-using-visual-studio))</span></span>
   - [<span data-ttu-id="c05ca-123">dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="c05ca-123">dotnet CLI</span></span>](#restore-using-the-dotnet-cli)
   - [<span data-ttu-id="c05ca-124">nuget.exe CLI</span><span class="sxs-lookup"><span data-stu-id="c05ca-124">nuget.exe CLI</span></span>](#restore-using-the-nugetexe-cli)
   - [<span data-ttu-id="c05ca-125">MSBuild</span><span class="sxs-lookup"><span data-stu-id="c05ca-125">MSBuild</span></span>](#restore-using-msbuild)
   - [<span data-ttu-id="c05ca-126">Azure Pipelines</span><span class="sxs-lookup"><span data-stu-id="c05ca-126">Azure Pipelines</span></span>](#restore-using-azure-pipelines)
   - [<span data-ttu-id="c05ca-127">Azure DevOps Server</span><span class="sxs-lookup"><span data-stu-id="c05ca-127">Azure DevOps Server</span></span>](#restore-using-azure-devops-server)

   <span data-ttu-id="c05ca-128">プロジェクト ファイル ( *.csproj*) のパッケージ参照、または *packages.config* ファイルが正しくない ([パッケージの復元] 後に必要な状態と一致しない) 場合は、代わりにパッケージをインストールまたは更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c05ca-128">If the package references in your project file (*.csproj*) or your *packages.config* file are incorrect (they do not match your desired state following Package Restore), then you need to either install or update packages instead.</span></span>

   <span data-ttu-id="c05ca-129">PackageReference を使用するプロジェクトの場合は、復元が正常に完了した後、"*グローバル パッケージ*" フォルダーにパッケージが存在し、`obj/project.assets.json` ファイルが再作成されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-129">For projects using PackageReference, after a successful restore, the package should be present in the *global-packages* folder and the `obj/project.assets.json` file is recreated.</span></span> <span data-ttu-id="c05ca-130">`packages.config` を使用するプロジェクトの場合は、プロジェクトの `packages` フォルダーにパッケージが生成されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-130">For projects using `packages.config`, the package should appear in the project's `packages` folder.</span></span> <span data-ttu-id="c05ca-131">この場合、プロジェクトを正常にビルドできるようになります。</span><span class="sxs-lookup"><span data-stu-id="c05ca-131">The project should now build successfully.</span></span> 

2. <span data-ttu-id="c05ca-132">[パッケージの復元] を実行した後も、パッケージの不足やパッケージに関連するエラー (Visual Studio のソリューション エクスプローラーのエラー アイコンなど) が引き続き発生する場合は、「[パッケージの復元エラーのトラブルシューティング](package-restore-troubleshooting.md)」に記載の手順に従うか、あるいは[パッケージを再インストールおよび更新](../consume-packages/reinstalling-and-updating-packages.md)することが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="c05ca-132">After running Package Restore, if you still experience missing packages or package-related errors (such as error icons in Solution Explorer in Visual Studio), you may need to follow instructions described in [Troubleshooting Package Restore errors](package-restore-troubleshooting.md) or, alternatively, [reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>

   <span data-ttu-id="c05ca-133">Visual Studio のパッケージ マネージャー コンソールには、パッケージを再インストールするための柔軟なオプションがいくつか用意されています。</span><span class="sxs-lookup"><span data-stu-id="c05ca-133">In Visual Studio, the Package Manager Console provides several flexible options for reinstalling packages.</span></span> <span data-ttu-id="c05ca-134">[パッケージ更新の使用](reinstalling-and-updating-packages.md#using-update-package)に関する記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-134">See [Using Package-Update](reinstalling-and-updating-packages.md#using-update-package).</span></span>

## <a name="restore-using-visual-studio"></a><span data-ttu-id="c05ca-135">Visual Studio を使用した復元</span><span class="sxs-lookup"><span data-stu-id="c05ca-135">Restore using Visual Studio</span></span>

<span data-ttu-id="c05ca-136">Windows の Visual Studio では、次のいずれかを行います。</span><span class="sxs-lookup"><span data-stu-id="c05ca-136">In Visual Studio on Windows, either:</span></span>

- <span data-ttu-id="c05ca-137">パッケージを自動的に復元する。または</span><span class="sxs-lookup"><span data-stu-id="c05ca-137">Restore packages automatically, or</span></span>

- <span data-ttu-id="c05ca-138">パッケージを手動で復元する</span><span class="sxs-lookup"><span data-stu-id="c05ca-138">Restore packages manually</span></span>

### <a name="restore-packages-automatically-using-visual-studio"></a><span data-ttu-id="c05ca-139">Visual Studio を使用して自動的にパッケージを復元する</span><span class="sxs-lookup"><span data-stu-id="c05ca-139">Restore packages automatically using Visual Studio</span></span>

<span data-ttu-id="c05ca-140">パッケージの復元は、テンプレートからプロジェクトを作成するとき、またはプロジェクトをビルドするときに、「[パッケージ復元の有効化と無効化](#enable-and-disable-package-restore-in-visual-studio)」に記載されているオプションに基づいて自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-140">Package Restore happens automatically when you create a project from a template or build a project, subject to the options in [Enable and disable package restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="c05ca-141">NuGet 4.0+ では、SDK スタイルのプロジェクト (通常は .NET Core または .NET Standard プロジェクト) への変更時にも復元が行われます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-141">In NuGet 4.0+, restore also happens automatically when you make changes to a SDK-style project (typically a .NET Core or .NET Standard project).</span></span>

1. <span data-ttu-id="c05ca-142">パッケージの自動復元を有効にするには、 **[ツール]**  >  **[オプション]**  >  **[NuGet パッケージ マネージャー]** の順に選択してから、 **[パッケージの復元]** の下で **[Visual Studio でのビルド中に見つからないパッケージを自動的に確認]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-142">Enable automatic package restore by choosing **Tools** > **Options** > **NuGet Package Manager**, and then selecting **Automatically check for missing packages during build in Visual Studio** under **Package Restore**.</span></span>

   <span data-ttu-id="c05ca-143">非 SDK スタイルのプロジェクトの場合は、最初に **[見つからないパッケージのダウンロードを NuGet に許可]** を選択して、自動復元オプションを有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c05ca-143">For non-SDK-style projects, you first need to select **Allow NuGet to download missing packages** to enable the automatic restore option.</span></span>

1. <span data-ttu-id="c05ca-144">プロジェクトをビルドします。</span><span class="sxs-lookup"><span data-stu-id="c05ca-144">Build the project.</span></span>

   <span data-ttu-id="c05ca-145">1 つまたは複数の個別パッケージが正しくインストールされていない場合、 **[ソリューション エクスプローラー]** にエラー アイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-145">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="c05ca-146">右クリックして **[NuGet パッケージの管理]** を選択し、 **[パッケージ マネージャー]** を使用し、影響を受けるパッケージをアンインストールし、再インストールします。</span><span class="sxs-lookup"><span data-stu-id="c05ca-146">Right-click and select **Manage NuGet Packages**, and use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="c05ca-147">詳細については、「[パッケージを再インストールして更新する](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-147">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

   <span data-ttu-id="c05ca-148">"このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、[自動復元を有効にしてください](#enable-and-disable-package-restore-in-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="c05ca-148">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="c05ca-149">以前のプロジェクトについては、[パッケージの自動復元への移行](#migrate-to-automatic-package-restore-visual-studio)に関する記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-149">For older projects, also see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio).</span></span> <span data-ttu-id="c05ca-150">[パッケージの復元のトラブルシューティング](Package-restore-troubleshooting.md)に関するページもご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-150">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

### <a name="restore-packages-manually-using-visual-studio"></a><span data-ttu-id="c05ca-151">Visual Studio を使用して手動でパッケージを復元する</span><span class="sxs-lookup"><span data-stu-id="c05ca-151">Restore packages manually using Visual Studio</span></span>

1. <span data-ttu-id="c05ca-152">パッケージの復元を有効にするには、 **[ツール]**  >  **[オプション]**  >  **[NuGet パッケージ マネージャー]** の順に選択します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-152">Enable package restore by choosing **Tools** > **Options** > **NuGet Package Manager**.</span></span> <span data-ttu-id="c05ca-153">**[パッケージの復元]** オプションの下で、 **[見つからないパッケージのダウンロードを NuGet に許可]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-153">Under **Package Restore** options, select **Allow NuGet to download missing packages**.</span></span>

1. <span data-ttu-id="c05ca-154">**ソリューション エクスプローラー**で、ソリューションを右クリックして、 **[NuGet パッケージの復元]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-154">In **Solution Explorer**, right click the solution and select **Restore NuGet Packages**.</span></span>

   <span data-ttu-id="c05ca-155">1 つまたは複数の個別パッケージが正しくインストールされていない場合、 **[ソリューション エクスプローラー]** にエラー アイコンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-155">If one or more individual packages still aren't installed properly, **Solution Explorer** shows an error icon.</span></span> <span data-ttu-id="c05ca-156">右クリックして **[NuGet パッケージの管理]** を選択した後、 **[パッケージ マネージャー]** を使用して、影響を受けるパッケージのアンインストールと再インストールを行います。</span><span class="sxs-lookup"><span data-stu-id="c05ca-156">Right-click and select **Manage NuGet Packages**, and then use **Package Manager** to uninstall and reinstall the affected packages.</span></span> <span data-ttu-id="c05ca-157">詳細については、「[パッケージを再インストールして更新する](../consume-packages/reinstalling-and-updating-packages.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-157">For more information, see [Reinstall and update packages](../consume-packages/reinstalling-and-updating-packages.md)</span></span>

   <span data-ttu-id="c05ca-158">"このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、[自動復元を有効にしてください](#enable-and-disable-package-restore-in-visual-studio)。</span><span class="sxs-lookup"><span data-stu-id="c05ca-158">If you see the error "This project references NuGet package(s) that are missing on this computer," or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," [enable automatic restore](#enable-and-disable-package-restore-in-visual-studio).</span></span> <span data-ttu-id="c05ca-159">以前のプロジェクトについては、[パッケージの自動復元への移行](#migrate-to-automatic-package-restore-visual-studio)に関する記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-159">For older projects, also see [Migrate to automatic package restore](#migrate-to-automatic-package-restore-visual-studio).</span></span> <span data-ttu-id="c05ca-160">[パッケージの復元のトラブルシューティング](Package-restore-troubleshooting.md)に関するページもご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-160">Also see [Package Restore troubleshooting](Package-restore-troubleshooting.md).</span></span>

### <a name="enable-and-disable-package-restore-in-visual-studio"></a><span data-ttu-id="c05ca-161">Visual Studio でパッケージの復元を有効または無効にする</span><span class="sxs-lookup"><span data-stu-id="c05ca-161">Enable and disable package restore in Visual Studio</span></span>

<span data-ttu-id="c05ca-162">Visual Studio では、パッケージ復元の管理は主に、 **[ツール]** 、 **[オプション]** 、 **[NuGet パッケージ マネージャー]** の順に選択して行います。</span><span class="sxs-lookup"><span data-stu-id="c05ca-162">In Visual Studio, you control Package Restore primarily through **Tools** > **Options** > **NuGet Package Manager**:</span></span>

![NuGet パッケージ マネージャーのオプションによるパッケージ復元の制御](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="c05ca-164">**見つからないパッケージのダウンロードを NuGet に許可**: `NuGet.Config` ファイル (Windows では `%AppData%\NuGet\`、Mac/Linux では `~/.nuget/NuGet/`) の [packageRestore セクション](../reference/nuget-config-file.md#packagerestore-section)の `packageRestore/enabled` 設定を変更することによって、パッケージ復元のすべての形式を制御します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-164">**Allow NuGet to download missing packages** controls all forms of package restore by changing the `packageRestore/enabled` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file, at `%AppData%\NuGet\` on Windows, or `~/.nuget/NuGet/` on Mac/Linux.</span></span> <span data-ttu-id="c05ca-165">また、この設定により、Visual Studio でソリューションのコンテキスト メニューの **[NuGet パッケージの復元]** コマンドが有効になります。</span><span class="sxs-lookup"><span data-stu-id="c05ca-165">This setting also enables the **Restore NuGet Packages** command on the solution's context menu in Visual Studio, .</span></span>

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
  > <span data-ttu-id="c05ca-166">`packageRestore/enabled` 設定をグローバルにオーバーライドするには、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-166">To globally override the `packageRestore/enabled` setting, set the environment variable **EnableNuGetPackageRestore** with a value of True or False before launching Visual Studio or starting a build.</span></span>

- <span data-ttu-id="c05ca-167">**Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: `NuGet.Config` ファイルの [packageRestore セクション](../reference/nuget-config-file.md#packagerestore-section)の `packageRestore/automatic` 設定を変更することにより、自動復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-167">**Automatically check for missing packages during build in Visual Studio** controls automatic restore by changing the `packageRestore/automatic` setting in the [packageRestore section](../reference/nuget-config-file.md#packagerestore-section) of the `NuGet.Config` file.</span></span> <span data-ttu-id="c05ca-168">このオプションを True に設定していると、Visual Studio からビルドを実行したとき、欠落しているパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-168">When this option is set to True, running a build from Visual Studio automatically restores any missing packages.</span></span> <span data-ttu-id="c05ca-169">この設定が MSBuild コマンド ラインから実行されるビルドに影響を与えることはありません。</span><span class="sxs-lookup"><span data-stu-id="c05ca-169">This setting doesn't affect builds run from the MSBuild command line.</span></span>

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

<span data-ttu-id="c05ca-170">コンピューター上のすべてのユーザーに対してパッケージ復元を有効または無効にする目的で、開発者または会社は構成設定をグローバル `nuget.config` ファイルに追加できます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-170">To enable or disable Package Restore for all users on a computer, a developer or company can add the configuration settings to the global `nuget.config` file.</span></span> <span data-ttu-id="c05ca-171">グローバル `nuget.config` は Windows の `%ProgramData%\NuGet\Config` の特定の `\{IDE}\{Version}\{SKU}\` Visual Studio フォルダーにある場合があります。Mac/Linux の場合は `~/.local/share` です。</span><span class="sxs-lookup"><span data-stu-id="c05ca-171">The global `nuget.config` is in Windows at `%ProgramData%\NuGet\Config`, sometimes under a specific `\{IDE}\{Version}\{SKU}\` Visual Studio folder, or in Mac/Linux at `~/.local/share`.</span></span> <span data-ttu-id="c05ca-172">その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="c05ca-173">NuGet で複数の構成ファイルに優先順位を付けるしくみについては、[共通 NuGet 構成](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-173">For more details on how NuGet prioritizes multiple config files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied).</span></span>

> [!Important]
> <span data-ttu-id="c05ca-174">`nuget.config` で直接、`packageRestore` 設定を編集する場合、 **[オプション]** ダイアログ ボックスに現在の値が表示されるように Visual Studio を再起動します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-174">If you edit the `packageRestore` settings directly in `nuget.config`, restart Visual Studio, so that the **Options** dialog box shows the current values.</span></span>

## <a name="restore-using-the-dotnet-cli"></a><span data-ttu-id="c05ca-175">dotnet CLI を使用した復元</span><span class="sxs-lookup"><span data-stu-id="c05ca-175">Restore using the dotnet CLI</span></span>

[!INCLUDE [restore-dotnet-cli](includes/restore-dotnet-cli.md)]

> [!IMPORTANT]
> <span data-ttu-id="c05ca-176">不足しているパッケージ参照をプロジェクト ファイルに追加するには、[dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x) を使います。これによって `restore` コマンドも実行されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-176">To add a missing package reference to the project file, use [dotnet add package](/dotnet/core/tools/dotnet-add-package?tabs=netcore2x), which also runs the `restore` command.</span></span>

## <a name="restore-using-the-nugetexe-cli"></a><span data-ttu-id="c05ca-177">nuget.exe CLI を使用した復元</span><span class="sxs-lookup"><span data-stu-id="c05ca-177">Restore using the nuget.exe CLI</span></span>

[!INCLUDE [restore-nuget-exe-cli](includes/restore-nuget-exe-cli.md)]

> [!IMPORTANT]
> <span data-ttu-id="c05ca-178">`restore` コマンドによってプロジェクト ファイルや *packages.config* が変更されることはありません。依存関係を追加するには、Visual Studio でパッケージ マネージャー UI かコンソールを利用してパッケージ復元を追加するか、*packages.config* を変更し、`install` か `restore` を実行します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-178">The `restore`command does not modify a project file or *packages.config*. To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify *packages.config* and then run either `install` or `restore`.</span></span>

## <a name="restore-using-msbuild"></a><span data-ttu-id="c05ca-179">MSBuild を使用した復元</span><span class="sxs-lookup"><span data-stu-id="c05ca-179">Restore using MSBuild</span></span>

<span data-ttu-id="c05ca-180">PackageReference を使うプロジェクト ファイルに記載されているパッケージを復元するには、[msbuild -t:restore](../reference/msbuild-targets.md#restore-target) コマンドを使います。</span><span class="sxs-lookup"><span data-stu-id="c05ca-180">To restore packages listed in the project file with PackageReference, use the the [msbuild -t:restore](../reference/msbuild-targets.md#restore-target) command.</span></span> <span data-ttu-id="c05ca-181">このコマンドは、Visual Studio 2017 以降のバージョンに含まれる NuGet 4.x+ と MSBuild 15.1+ でのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-181">This command is available only in NuGet 4.x+ and MSBuild 15.1+, which are included with Visual Studio 2017 and higher versions.</span></span> <span data-ttu-id="c05ca-182">`nuget restore` と `dotnet restore` の両方で、該当するプロジェクトにこのコマンドが使用されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-182">Both `nuget restore` and `dotnet restore` use this command for applicable projects.</span></span>

1. <span data-ttu-id="c05ca-183">開発者コマンド プロンプトを開きます (**検索**ボックスに「**開発者コマンド プロンプト**」と入力します)。</span><span class="sxs-lookup"><span data-stu-id="c05ca-183">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="c05ca-184">MSBuild に必要なすべてのパスが構成されるため、通常は **[スタート]** メニューから Visual Studio 用開発者コマンド プロンプトを使用します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-184">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

2. <span data-ttu-id="c05ca-185">プロジェクト ファイルが含まれているフォルダーに切り替え、次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-185">Switch to the folder containing the project file and type the following command.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

3. <span data-ttu-id="c05ca-186">次のコマンドを入力して、プロジェクトをリビルドします。</span><span class="sxs-lookup"><span data-stu-id="c05ca-186">Type the following command to rebuild the project.</span></span>

   ```cmd
   msbuild
   ```

   <span data-ttu-id="c05ca-187">MSBuild の出力にビルドが正常に完了したことが示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-187">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="restore-using-azure-pipelines"></a><span data-ttu-id="c05ca-188">Azure Pipelines を使用した復元</span><span class="sxs-lookup"><span data-stu-id="c05ca-188">Restore using Azure Pipelines</span></span>

<span data-ttu-id="c05ca-189">Azure Pipelines でビルド定義を作成するとき、定義の中でビルド タスクの前に NuGet [復元](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages)または .NET Core [復元](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops)タスクを含めます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-189">When you create a build definition in Azure Pipelines, include the NuGet [restore](/azure/devops/pipelines/tasks/package/nuget#restore-nuget-packages) or .NET Core [restore](/azure/devops/pipelines/tasks/build/dotnet-core-cli?view=azure-devops) task in the definition before any build tasks.</span></span> <span data-ttu-id="c05ca-190">一部のビルド テンプレートには、既定で復元タスクが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c05ca-190">Some build templates include the restore task by default.</span></span>

## <a name="restore-using-azure-devops-server"></a><span data-ttu-id="c05ca-191">Azure DevOps Server を使用した復元</span><span class="sxs-lookup"><span data-stu-id="c05ca-191">Restore using Azure DevOps Server</span></span>

<span data-ttu-id="c05ca-192">Azure DevOps Server と TFS 2013 以降では、TFS 2013 以降のチーム ビルド テンプレートを使用している場合、ビルド時にパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-192">Azure DevOps Server and TFS 2013 and later automatically restore packages during build, if you're using a TFS 2013 or later Team Build template.</span></span> <span data-ttu-id="c05ca-193">それより前の TFS バージョンの場合、コマンドラインで復元を実行するビルド ステップを含めたり、任意で、ビルド テンプレートを後続のバージョンに移行したりできます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-193">For earlier TFS versions, you can include a build step to run a command-line restore option, or optionally migrate the build template to a later version.</span></span> <span data-ttu-id="c05ca-194">詳細については、[Team Foundation ビルドでパッケージ復元を設定する](../consume-packages/team-foundation-build.md)方法に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-194">For more information, see [Set up package restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>

## <a name="constrain-package-versions-with-restore"></a><span data-ttu-id="c05ca-195">復元でパッケージ バージョンを制約する</span><span class="sxs-lookup"><span data-stu-id="c05ca-195">Constrain package versions with restore</span></span>

<span data-ttu-id="c05ca-196">NuGet で何らかの方法でパッケージを復元するとき、`packages.config` またはプロジェクト ファイルに指定した制約が適用されます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-196">When NuGet restores packages through any method, it honors any constraints you specified in `packages.config` or the project file:</span></span>

- <span data-ttu-id="c05ca-197">`packages.config` では、依存関係の `allowedVersion` プロパティでバージョン範囲を指定できます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-197">In `packages.config`, you can specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="c05ca-198">詳細については、[アップグレード バージョンの制約](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-198">See [Constrain upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) for more information.</span></span> <span data-ttu-id="c05ca-199">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-199">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="c05ca-200">プロジェクト ファイルでは、PackageReference を使用し、依存関係の範囲を直接指定できます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-200">In a project file, you can use PackageReference to specify a dependency's range directly.</span></span> <span data-ttu-id="c05ca-201">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-201">For example:</span></span>

    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />
    ```

<span data-ttu-id="c05ca-202">いずれの場合も、「[Package versioning](../concepts/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。</span><span class="sxs-lookup"><span data-stu-id="c05ca-202">In all cases, use the notation described in [Package versioning](../concepts/package-versioning.md).</span></span>

## <a name="force-restore-from-package-sources"></a><span data-ttu-id="c05ca-203">パッケージ ソースから強制的に復元する</span><span class="sxs-lookup"><span data-stu-id="c05ca-203">Force restore from package sources</span></span>

<span data-ttu-id="c05ca-204">[グローバル パッケージとキャッシュ フォルダーの管理](managing-the-global-packages-and-cache-folders.md)に関するページで説明されているように、既定では、NuGet の復元操作では、"*グローバル パッケージ*" フォルダーと "*HTTP キャッシュ*" フォルダーのパッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-204">By default, NuGet restore operations use packages from the *global-packages* and *http-cache* folders, which are described in [Manage the global packages and cache folders](managing-the-global-packages-and-cache-folders.md).</span></span>

<span data-ttu-id="c05ca-205">"*グローバル パッケージ*" フォルダーの使用を回避するには、次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="c05ca-205">To avoid using the *global-packages* folder, do one of the following:</span></span>

- <span data-ttu-id="c05ca-206">`nuget locals global-packages -clear` または `dotnet nuget locals global-packages --clear` を使用して、フォルダーをクリアします。</span><span class="sxs-lookup"><span data-stu-id="c05ca-206">Clear the folder using `nuget locals global-packages -clear` or `dotnet nuget locals global-packages --clear`.</span></span>
- <span data-ttu-id="c05ca-207">次のいずれかの方法で、復元操作の前に "*グローバル パッケージ*" フォルダーの場所を一時的に変更します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-207">Temporarily change the location of the *global-packages* folder before the restore operation, using one of the following methods:</span></span>
  - <span data-ttu-id="c05ca-208">NUGET_PACKAGES 環境変数を別のフォルダーに設定する。</span><span class="sxs-lookup"><span data-stu-id="c05ca-208">Set the NUGET_PACKAGES environment variable to a different folder.</span></span>
  - <span data-ttu-id="c05ca-209">`globalPackagesFolder` (PackageReference を使用している場合) または `repositoryPath` (`packages.config` を使用している場合) を別のフォルダーに設定した `NuGet.Config` ファイルを作成する。</span><span class="sxs-lookup"><span data-stu-id="c05ca-209">Create a `NuGet.Config` file that sets `globalPackagesFolder` (if using PackageReference) or `repositoryPath` (if using `packages.config`) to a different folder.</span></span> <span data-ttu-id="c05ca-210">[構成設定](../reference/nuget-config-file.md#config-section)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-210">For more information, see [configuration settings](../reference/nuget-config-file.md#config-section).</span></span>
  - <span data-ttu-id="c05ca-211">MSBuild のみ:`RestorePackagesPath` プロパティで別のフォルダーを指定する。</span><span class="sxs-lookup"><span data-stu-id="c05ca-211">MSBuild only: Specify a different folder with the `RestorePackagesPath` property.</span></span>

<span data-ttu-id="c05ca-212">HTTP ソースのキャッシュの使用を回避するには、次のいずれかの操作を行います。</span><span class="sxs-lookup"><span data-stu-id="c05ca-212">To avoid using the cache for HTTP sources, do one of the following:</span></span>

- <span data-ttu-id="c05ca-213">`nuget restore` で `-NoCache` オプションを使用するか、`dotnet restore` で `--no-cache` オプションを使用する。</span><span class="sxs-lookup"><span data-stu-id="c05ca-213">Use the `-NoCache` option with `nuget restore`, or the `--no-cache` option with `dotnet restore`.</span></span> <span data-ttu-id="c05ca-214">これらのオプションは、Visual Studio パッケージ マネージャーまたはコンソールを経由した復元操作には影響しません。</span><span class="sxs-lookup"><span data-stu-id="c05ca-214">These options don't affect restore operations through the Visual Studio Package Manager or console.</span></span>
- <span data-ttu-id="c05ca-215">`nuget locals http-cache -clear` または `dotnet nuget locals http-cache --clear` を使用してキャッシュをクリアする。</span><span class="sxs-lookup"><span data-stu-id="c05ca-215">Clear the cache using `nuget locals http-cache -clear` or `dotnet nuget locals http-cache --clear`.</span></span>
- <span data-ttu-id="c05ca-216">一時的に NUGET_HTTP_CACHE_PATH 環境変数を別のフォルダーに設定する。</span><span class="sxs-lookup"><span data-stu-id="c05ca-216">Temporarily set the NUGET_HTTP_CACHE_PATH environment variable to a different folder.</span></span>

## <a name="migrate-to-automatic-package-restore-visual-studio"></a><span data-ttu-id="c05ca-217">パッケージの自動復元への移行 (Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="c05ca-217">Migrate to automatic package restore (Visual Studio)</span></span>

<span data-ttu-id="c05ca-218">NuGet 2.6 およびそれ以前では、以前は MSBuild に統合されたパッケージの復元がサポートされていましたが、現在ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="c05ca-218">For NuGet 2.6 and earlier, an MSBuild-integrated package restore was previously supported but that is no longer true.</span></span> <span data-ttu-id="c05ca-219">(これは通常、Visual Studio でソリューションを右クリックし、 **[NuGet パッケージの復元を有効にする]** を選択することで有効になりました)。</span><span class="sxs-lookup"><span data-stu-id="c05ca-219">(It was typically enabled by right-clicking a solution in Visual Studio and selecting **Enable NuGet Package Restore**).</span></span> <span data-ttu-id="c05ca-220">ご自身のプロジェクトで、非推奨の、MSBuild に統合されたパッケージの復元を使用する場合は、パッケージの自動復元に移行してください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-220">If your project uses the deprecated MSBuild-integrated package restore, please migrate to automatic package restore.</span></span>

<span data-ttu-id="c05ca-221">MSBuild に統合されたパッケージの復元が使用されるプロジェクトには、通常、次の 3 つのファイルを含む *.nuget* フォルダーが含まれています:*NuGet.config*、*nuget.exe*、*NuGet.targets*。</span><span class="sxs-lookup"><span data-stu-id="c05ca-221">Projects that use MSBuild-Integrated package restore typically contain a *.nuget* folder with three files: *NuGet.config*, *nuget.exe*, and *NuGet.targets*.</span></span> <span data-ttu-id="c05ca-222">*NuGet.targets* ファイルの存在によって、NuGet で MSBuild に統合されたアプローチが引き続き使用されるかどうかが決まります。そのため、移行中にこのファイルを削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c05ca-222">The presence of a *NuGet.targets* file determines whether NuGet will continue to use the MSBuild-untegrated approach, so this file must be removed during the migration.</span></span>

<span data-ttu-id="c05ca-223">パッケージの自動復元に移行するには:</span><span class="sxs-lookup"><span data-stu-id="c05ca-223">To migrate to automatic package restore:</span></span>

1. <span data-ttu-id="c05ca-224">Visual Studio を閉じます。</span><span class="sxs-lookup"><span data-stu-id="c05ca-224">Close Visual Studio.</span></span>
2. <span data-ttu-id="c05ca-225">*.nuget/nuget.exe* と *.nuget/NuGet.targets* を削除します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-225">Delete *.nuget/nuget.exe* and *.nuget/NuGet.targets*.</span></span>
3. <span data-ttu-id="c05ca-226">各プロジェクト ファイルごとに、`<RestorePackages>` 要素を削除し、*NuGet.targets* への参照をすべて削除します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-226">For each project file, remove the `<RestorePackages>` element and remove any reference to *NuGet.targets*.</span></span>

<span data-ttu-id="c05ca-227">パッケージの自動復元をテストするには:</span><span class="sxs-lookup"><span data-stu-id="c05ca-227">To test the automatic package restore:</span></span>

1. <span data-ttu-id="c05ca-228">ソリューションから *packages* フォルダーを削除します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-228">Remove the *packages* folder from the solution.</span></span>
2. <span data-ttu-id="c05ca-229">Visual Studio でソリューションを開き、ビルドを開始します。</span><span class="sxs-lookup"><span data-stu-id="c05ca-229">Open the solution in Visual Studio and start a build.</span></span>

   <span data-ttu-id="c05ca-230">パッケージの自動復元によって、各依存関係パッケージがダウンロードおよびインストールされ、それらがソース管理に追加されることはありません。</span><span class="sxs-lookup"><span data-stu-id="c05ca-230">Automatic package restore should download and install each dependency package, without adding them to source control.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c05ca-231">トラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="c05ca-231">Troubleshooting</span></span>

<span data-ttu-id="c05ca-232">[パッケージの復元のトラブルシューティング](package-restore-troubleshooting.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="c05ca-232">See [Troubleshoot package restore](package-restore-troubleshooting.md).</span></span>
