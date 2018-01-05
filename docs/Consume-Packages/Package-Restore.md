---
title: "NuGet パッケージの復元 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: a7bf21da-86ae-4c2d-8750-04ff53f41967
description: "プロジェクトが依存しているパッケージを NuGet が復元する方法について説明します。復元を無効にする方法や、バージョンを制約する方法についても触れます。"
keywords: "NuGet パッケージの復元, NuGet パッケージのインストール, パッケージのインストール, パッケージの復元, 依存関係のバージョン, 自動復元の無効化, パッケージのバージョンの制約"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c2567f45b6bb36cdd94c4ce6f1418cb1c7ceac5e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-restore"></a><span data-ttu-id="a9ee5-104">パッケージの復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-104">Package Restore</span></span>

<span data-ttu-id="a9ee5-105">開発環境をいっそうクリーンにしてリポジトリのサイズを減らすため、NuGet の**パッケージの復元**では、プロジェクトがビルドされる前に、参照されているすべてのパッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-105">To promote a cleaner development environment and to reduce repository size, NuGet **Package Restore** installs all referenced packages before a project is built.</span></span> <span data-ttu-id="a9ee5-106">この広く使われている機能により、これらのパッケージをソース管理に格納しなくても、すべての依存関係をプロジェクトで利用できます (パッケージのバイナリを除外するようにリポジトリを構成する方法については、「[パッケージとソース管理](../consume-packages/packages-and-source-control.md)」をご覧ください)。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-106">This widely-used feature ensures that all dependencies are available in a project without requiring those packages to be stored in source control (see [Packages and Source Control](../consume-packages/packages-and-source-control.md) on how to configure your repository to exclude package binaries).</span></span>

<span data-ttu-id="a9ee5-107">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="a9ee5-107">In this topic:</span></span>
- [<span data-ttu-id="a9ee5-108">パッケージの復元の簡単なガイド</span><span class="sxs-lookup"><span data-stu-id="a9ee5-108">Quick guide to package restore</span></span>](#quick-guide-to-package-restore)
- [<span data-ttu-id="a9ee5-109">パッケージの復元の概要</span><span class="sxs-lookup"><span data-stu-id="a9ee5-109">Package restore overview</span></span>](#package-restore-overview)
- [<span data-ttu-id="a9ee5-110">パッケージの復元の有効化と無効化</span><span class="sxs-lookup"><span data-stu-id="a9ee5-110">Enabling and disabling package restore</span></span>](#enabling-and-disabling-package-restore)
- [<span data-ttu-id="a9ee5-111">復元でのパッケージのバージョンの制約</span><span class="sxs-lookup"><span data-stu-id="a9ee5-111">Constraining package versions with restore</span></span>](#constraining-package-versions-with-restore)
- <span data-ttu-id="a9ee5-112">[コマンド ラインでの復元](#command-line-restore) (NuGet のすべてのバージョン)</span><span class="sxs-lookup"><span data-stu-id="a9ee5-112">[Command-line restore](#command-line-restore), for all versions of NuGet</span></span>
- <span data-ttu-id="a9ee5-113">[Visual Studio での自動復元](#automatic-restore-in-visual-studio) (or NuGet 2.7 以降)</span><span class="sxs-lookup"><span data-stu-id="a9ee5-113">[Automatic restore in Visual Studio](#automatic-restore-in-visual-studio), for NuGet 2.7 and later.</span></span>
- <span data-ttu-id="a9ee5-114">[Visual Studio での MSBuild に統合された復元](#msbuild-integrated-restore) (or NuGet 2.6 以降)</span><span class="sxs-lookup"><span data-stu-id="a9ee5-114">[MSBuild-integrated restore in Visual Studio](#msbuild-integrated-restore), for NuGet 2.6 and earlier.</span></span>
- [<span data-ttu-id="a9ee5-115">Team Foundation ビルドでのパッケージの復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-115">Package restore with Team Foundation Build</span></span>](#package-restore-with-team-foundation-build)

<span data-ttu-id="a9ee5-116">復元の動作はバージョンによって異なります。お使いの NuGet のバージョンを確認するには、コマンド ラインで `nuget.exe` を実行して、出力の最初の行を調べます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-116">Restore behavior does vary by version; to check your NuGet version, simply run `nuget.exe` on the command line and look at the first line of output.</span></span>

<span data-ttu-id="a9ee5-117">ビルド サーバーでのパッケージの復元について詳しくは、[TFBuild でのパッケージの復元](../consume-packages/team-foundation-build.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-117">For additional details on package restore on build servers, see [Package restore with TFBuild](../consume-packages/team-foundation-build.md).</span></span>

> [!Note]
> <span data-ttu-id="a9ee5-118">パッケージ復元用に構成されたプロジェクトは、Mono の xbuild でも動作します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-118">Projects configured for package restore also work with xbuild on Mono.</span></span>

## <a name="quick-guide-to-package-restore"></a><span data-ttu-id="a9ee5-119">パッケージの復元の簡単なガイド</span><span class="sxs-lookup"><span data-stu-id="a9ee5-119">Quick guide to package restore</span></span>

[!INCLUDE[package-restore](../includes/package-restore.md)]

> [!Note]
> <span data-ttu-id="a9ee5-120">"このプロジェクトは、このコンピューター上にない NuGet パッケージを参照しています" または "1 つ以上の NuGet パッケージを復元する必要がありますが、同意が与えられていないため、復元できませんでした" というエラーが表示される場合は、「[パッケージの復元の有効化と無効化](#enabling-and-disabling-package-restore)」の手順に従って、自動復元を有効にしてください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-120">If you see the error "This project references NuGet package(s) that are missing on this computer" or "One or more NuGet packages need to be restored but couldn't be because consent has not been granted," turn on automatic restore by following the instructions under [Enabling and disabling package restore](#enabling-and-disabling-package-restore).</span></span>

## <a name="package-restore-overview"></a><span data-ttu-id="a9ee5-121">パッケージの復元の概要</span><span class="sxs-lookup"><span data-stu-id="a9ee5-121">Package restore overview</span></span>

<span data-ttu-id="a9ee5-122">最初に、パッケージの参照は、プロジェクトの種類と NuGet のバージョンに応じて、次のいずれかのパッケージ管理形式で保持されています </span><span class="sxs-lookup"><span data-stu-id="a9ee5-122">First, package references are maintained in one of the following package management formats, depending on project type and NuGet version.</span></span> <span data-ttu-id="a9ee5-123">(NuGet 4 と MSBuild 15.1 は Visual Studio 2017 でインストールされることに注意してください)。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-123">(Note that NuGet 4 and MSBuild 15.1 are installed with Visual Studio 2017.)</span></span>

| <span data-ttu-id="a9ee5-124">メソッド</span><span class="sxs-lookup"><span data-stu-id="a9ee5-124">Method</span></span> | <span data-ttu-id="a9ee5-125">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="a9ee5-125">NuGet Version</span></span> | <span data-ttu-id="a9ee5-126">説明</span><span class="sxs-lookup"><span data-stu-id="a9ee5-126">Description</span></span> | 
| --- | --- | --- |
| `packages.config` | <span data-ttu-id="a9ee5-127">2.x 以降</span><span class="sxs-lookup"><span data-stu-id="a9ee5-127">2.x+</span></span> | <span data-ttu-id="a9ee5-128">依存関係の完全なディープ セットが列記されています。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-128">Lists the complete deep set of dependencies.</span></span> <span data-ttu-id="a9ee5-129">`packages.config` に追加されたパッケージはプロジェクト ファイルにも追加される必要があり、ターゲットとプロパティもプロジェクト ファイルに追加される必要があります。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-129">Packages added to `packages.config` must also be added to the project file, and Targets and Props must also be added to the project file.</span></span> <span data-ttu-id="a9ee5-130">これは NuGet のすべてのバージョンの基本となる方法ですが、パフォーマンスは他のオプションより低下します </span><span class="sxs-lookup"><span data-stu-id="a9ee5-130">This is the baseline method for all versions of NuGet, but has slower performance compared with the other options.</span></span> <span data-ttu-id="a9ee5-131">([packages.config のスキーマ](../schema/packages-config.md)に関するページを参照)。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-131">(See [packages.config schema](../schema/packages-config.md).)</span></span> | 
| `project.json` | <span data-ttu-id="a9ee5-132">3.x 以降</span><span class="sxs-lookup"><span data-stu-id="a9ee5-132">3.x+</span></span> | <span data-ttu-id="a9ee5-133">UWP プロジェクトでの既定としてのみ使われますが、プロジェクトを `packages.config` から変換できます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-133">Used only by default with UWP projects, but projects can be converted from `packages.config`.</span></span> <span data-ttu-id="a9ee5-134">`project.json` には、最上位の依存関係のみが列記されます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-134">`project.json` lists only top-level dependencies.</span></span> <span data-ttu-id="a9ee5-135">参照、ターゲット、プロパティはビルドの間にプロジェクトに動的に追加され、パフォーマンスは `packages.config` よりよくなります </span><span class="sxs-lookup"><span data-stu-id="a9ee5-135">References, Targets, and Props are added dynamically to the project during build, resulting in better performance compared with `packages.config`.</span></span> <span data-ttu-id="a9ee5-136">([project.json のスキーマ](../schema/project-json.md)に関するページを参照)。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-136">(See [project.json schema](../schema/project-json.md).)</span></span>|
| <span data-ttu-id="a9ee5-137">PackageReference</span><span class="sxs-lookup"><span data-stu-id="a9ee5-137">PackageReference</span></span> | <span data-ttu-id="a9ee5-138">4.x 以降</span><span class="sxs-lookup"><span data-stu-id="a9ee5-138">4.x+</span></span> | <span data-ttu-id="a9ee5-139">依存関係は、プロジェクト ファイルの `<PackageReference>` ノードに、`<Reference>` および `<ProjectReference>` と共に直接列記されます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-139">Lists dependencies directly in the project file in the `<PackageReference>` node, alongside `<Reference>` and `<ProjectReference>`.</span></span> <span data-ttu-id="a9ee5-140">`project.json` と同じように動作します。[プロジェクト ファイルでのパッケージの参照](../Consume-Packages/Package-References-in-Project-Files.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-140">Works similarly to `project.json`; see [Package references in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> |

<span data-ttu-id="a9ee5-141">次に、さまざまな方法で参照リストを使って復元を開始します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-141">Second, you start a restore using the reference list in a variety of ways:</span></span>

<span data-ttu-id="a9ee5-142">コマンド ラインからまたは[パッケージ マネージャー コンソール](../tools/Package-Manager-Console.md)から:</span><span class="sxs-lookup"><span data-stu-id="a9ee5-142">From the command line or [Package Manager Console](../tools/Package-Manager-Console.md):</span></span>

| <span data-ttu-id="a9ee5-143">コマンド</span><span class="sxs-lookup"><span data-stu-id="a9ee5-143">Command</span></span> | <span data-ttu-id="a9ee5-144">該当シナリオ</span><span class="sxs-lookup"><span data-stu-id="a9ee5-144">Applicable scenarios</span></span> |
| --- | --- | 
| `nuget restore` | <span data-ttu-id="a9ee5-145">すべてのバージョンの NuGet およびすべての参照の種類。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-145">All versions of NuGet and all reference types.</span></span> <span data-ttu-id="a9ee5-146">後の「[コマンド ラインでの復元](#command-line-restore)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-146">See [Command-line restore](#command-line-restore) below.</span></span> | 
| `dotnet restore` | <span data-ttu-id="a9ee5-147">.NET Core プロジェクトの場合の `nuget restore` と同じです。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-147">Same as `nuget restore` for .NET Core projects.</span></span> <span data-ttu-id="a9ee5-148">「[dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-148">See [dotnet restore](https://docs.microsoft.com/dotnet/articles/core/tools/dotnet-restore).</span></span> |
| `msbuild /t:restore` | <span data-ttu-id="a9ee5-149">[プロジェクト ファイルでのパッケージ参照](../Consume-Packages/Package-References-in-Project-Files.md)のみを使う Nuget 4.x 以降および MSBuild 15.1 以降。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-149">Nuget 4.x+ and MSBuild 15.1+ with [package references in project files](../Consume-Packages/Package-References-in-Project-Files.md) only.</span></span> <span data-ttu-id="a9ee5-150">`nuget restore` と `dotnet restore` はどちらも、このコマンドを該当するプロジェクトに使います。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-150">`nuget restore` and `dotnet restore` both use this command for applicable projects.</span></span> <span data-ttu-id="a9ee5-151">「NuGet pack and restore as MSBuild targets」(MSBuild ターゲットとしての NuGet のパックと復元) の「[restore target](../schema/msbuild-targets.md#restore-target)」(ターゲットの復元) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-151">See [NuGet pack and restore as MSBuild targets- restore target](../schema/msbuild-targets.md#restore-target).</span></span>|

<span data-ttu-id="a9ee5-152">visual Studio 自体もさまざまなタイミングでパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-152">Visual Studio itself also restores packages at different times:</span></span>

| <span data-ttu-id="a9ee5-153">型</span><span class="sxs-lookup"><span data-stu-id="a9ee5-153">Type</span></span> | <span data-ttu-id="a9ee5-154">復元が行われるタイミング</span><span class="sxs-lookup"><span data-stu-id="a9ee5-154">When restore happens</span></span> |
| --- | --- |
| <span data-ttu-id="a9ee5-155">テンプレートの復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-155">Template restore</span></span> | <span data-ttu-id="a9ee5-156">新しいプロジェクトの作成時に、一部のテンプレートが外部パッケージに依存している場合。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-156">During creation of a new project, as some templates depend on external packages.</span></span> |
| <span data-ttu-id="a9ee5-157">ビルドの復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-157">Build restore</span></span> | <span data-ttu-id="a9ee5-158">ビルドの最初のステップとして。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-158">As the first step of a build.</span></span> |
| <span data-ttu-id="a9ee5-159">ソリューションの復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-159">Solution restore</span></span> | <span data-ttu-id="a9ee5-160">ユーザーがソリューションを右クリックして **[NuGet パッケージの復元]** を選んだとき。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-160">When user right-clicks a solution and selects **Restore NuGet Packages**.</span></span> |
| <span data-ttu-id="a9ee5-161">プロジェクト変更時の復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-161">Restore on project change</span></span> | <span data-ttu-id="a9ee5-162">*(NuGet 4.x のみ)* .NET Core SDK ベースのプロジェクトが使われているとき (プロジェクトの状態変化を含む)。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-162">*(NuGet 4.x only)* When a .NET Core SDK-based project is used, including when project state changes.</span></span> |

## <a name="enabling-and-disabling-package-restore"></a><span data-ttu-id="a9ee5-163">パッケージの復元の有効化と無効化</span><span class="sxs-lookup"><span data-stu-id="a9ee5-163">Enabling and disabling package restore</span></span>

<span data-ttu-id="a9ee5-164">パッケージの復元を有効にするには、主に Visual Studio の **[ツール] > [オプション] > [NuGet パッケージ マネージャー]** を使います。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-164">Package restore is primarily enabled through **Tools > Options > NuGet Package Manager** in Visual Studio:</span></span>

![NuGet パッケージ マネージャーのオプションによるパッケージ復元動作の制御](media/Restore-01-AutoRestoreOptions.png)

- <span data-ttu-id="a9ee5-166">**見つからないパッケージのダウンロードを NuGet に許可**: 次に示すように、`%AppData%\NuGet\NuGet.Config` ファイルの `packageRestore/enabled` の設定を変更することによって、パッケージ復元のすべての形式を制御します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-166">**Allow NuGet to download missing packages**: controls all forms of package restore by changing the `packageRestore/enabled` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>

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
    >  <span data-ttu-id="a9ee5-167">`packageRestore/enabled` の設定は、Visual Studio の起動前またはビルドの開始前に環境変数 **EnableNuGetPackageRestore** の値を TRUE または FALSE に設定することにより、グローバルに上書きできます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-167">The `packageRestore/enabled` setting can be overridden globally by setting an environment variable called **EnableNuGetPackageRestore** with a value of TRUE or FALSE before launching Visual Studio or starting a build.</span></span>
    

- <span data-ttu-id="a9ee5-168">**Visual Studio でのビルド中に見つからないパッケージを自動的に確認**: 次に示すように、`%AppData%\NuGet\NuGet.Config` ファイルの `packageRestore/automatic` の設定を変更することにより、NuGet 2.7 以降での自動復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-168">**Automatically check for missing packages during build in Visual Studio**: controls automatic restore for NuGet 2.7 and later by changing the `packageRestore/automatic` setting in the `%AppData%\NuGet\NuGet.Config` file as shown below.</span></span>
            
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

<span data-ttu-id="a9ee5-169">詳しくは、「NuGet config file」(NuGet config ファイル) の「[packageRestore section](../Schema/nuget-config-file.md#packagerestore-section)」(packageRestore セクション) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-169">For reference, see the [NuGet config file - packageRestore section](../Schema/nuget-config-file.md#packagerestore-section).</span></span>

<span data-ttu-id="a9ee5-170">開発者や会社が、すべてのユーザーに対する既定値を使って、コンピューターでのパッケージの復元を有効または無効にすることを望む場合があります。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-170">In some cases, a developer or company might want to enable or disable package restore on a machine by default for all users.</span></span> <span data-ttu-id="a9ee5-171">これは、上と同じ設定を `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]` にあるグローバルな NuGet 構成ファイルに追加することによって実現できます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-171">This can be done by adding the same settings above to the global NuGet configuration file located in `%ProgramData%\NuGet\Config[\{IDE}[\{Version}[\{SKU}]]]`.</span></span> <span data-ttu-id="a9ee5-172">その場合、個々のユーザーは、必要に応じてプロジェクト レベルで選択的に復元を有効にできます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-172">Individual users can then selectively enable restore as needed on a project level.</span></span> <span data-ttu-id="a9ee5-173">NuGet が複数の構成ファイルの優先順位を決める方法について詳しくは、「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)」(NuGet の動作を構成する) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-173">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied) for exact details on how NuGet prioritizes multiple config files.</span></span>

## <a name="constraining-package-versions-with-restore"></a><span data-ttu-id="a9ee5-174">復元でのパッケージのバージョンの制約</span><span class="sxs-lookup"><span data-stu-id="a9ee5-174">Constraining package versions with restore</span></span>

<span data-ttu-id="a9ee5-175">NuGet は、いずれかの方法でパッケージを復元するとき、`packages.config`、`project.json`、またはプロジェクト ファイルで指定されている制約に従います。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-175">When NuGet restores packages through any method, it will honor any constraints specified in `packages.config`, `project.json`, or the project file:</span></span>

- <span data-ttu-id="a9ee5-176">`packages.config`: 依存関係の `allowedVersion` プロパティでバージョンの範囲を指定します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-176">`packages.config`: Specify a version range in the `allowedVersion` property of the dependency.</span></span> <span data-ttu-id="a9ee5-177">「[Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)」(パッケージの再インストールと更新) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-177">See [Reinstalling and Updating Packages](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions).</span></span> <span data-ttu-id="a9ee5-178">例:</span><span class="sxs-lookup"><span data-stu-id="a9ee5-178">For example:</span></span>

    ```xml
    <package id="Newtonsoft.json" version="6.0.4" allowedVersions="[6,7)" />
    ```

- <span data-ttu-id="a9ee5-179">`project.json`: 依存関係のバージョン番号でバージョンの範囲を直接指定します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-179">`project.json`: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="a9ee5-180">例:</span><span class="sxs-lookup"><span data-stu-id="a9ee5-180">For example:</span></span>

    ```json
    "Newtonsoft.json": "[6, 7)"
    ```

- <span data-ttu-id="a9ee5-181">プロジェクト ファイルのパッケージ参照: 依存関係のバージョン番号でバージョン範囲を直接指定します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-181">Package references in project files: Specify a version range directly with the dependency's version number.</span></span> <span data-ttu-id="a9ee5-182">例:</span><span class="sxs-lookup"><span data-stu-id="a9ee5-182">For example:</span></span>
 
    ```xml
    <PackageReference Include="Newtonsoft.json" Version="[6, 7)" />  
    ```

<span data-ttu-id="a9ee5-183">いずれの場合も、「[Package versioning](../reference/package-versioning.md)」(パッケージのバージョン管理) で説明されている表記を使います。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-183">In all cases, use the notation described in [Package versioning](../reference/package-versioning.md).</span></span>

## <a name="command-line-restore"></a><span data-ttu-id="a9ee5-184">コマンド ラインでの復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-184">Command-line restore</span></span>

<span data-ttu-id="a9ee5-185">NuGet 2.7 以降では、[restore](../tools/cli-ref-restore.md) コマンドを使ってソリューション内のすべてのパッケージを復元します (`packages.config`、`project.json`、プロジェクト ファイル内のパッケージ参照のどれを使っている場合でも)。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-185">For NuGet 2.7 and above, use the [Restore](../tools/cli-ref-restore.md) command to restore all packages in a solution (whether it uses `packages.config`, `project.json`, or package references in project files).</span></span> <span data-ttu-id="a9ee5-186">次のどのバリエーションも、`c:\proj\app` などの指定されたプロジェクト フォルダーのパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-186">For a given project folder such as `c:\proj\app`, the common variations below each restore the packages:</span></span>

```
c:\proj\app\> nuget restore
c:\proj\app\> nuget.exe restore app.sln
c:\proj\> nuget restore app
```

<span data-ttu-id="a9ee5-187">NuGet 4.0 以降および MSBuild 15.1 以降の場合は、「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) で説明されている `MSBuild /t:restore` を使うこともできます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-187">For NuGet 4.0+ and MSBuild 15.1+, you can also use `MSBuild /t:restore` as described on [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="build-time-restore-in-visual-studio"></a><span data-ttu-id="a9ee5-188">Visual Studio でのビルド時の復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-188">Build-time restore in Visual Studio</span></span>

<span data-ttu-id="a9ee5-189">Visual Studio は、既定で、ビルドの開始時に足りないパッケージを自動的に復元します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-189">Visual Studio automatically restores missing packages by default at the beginning of a build.</span></span> <span data-ttu-id="a9ee5-190">この動作は、**[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [全般] > [Visual Studio でのビルド中に見つからないパッケージを自動的に確認]** をオフにすることによって変更できます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-190">This behavior can be changed by clearing **Tools > Options > NuGet Package Manager > General > Automatically check for missing packages during build in Visual Studio**.</span></span>

<span data-ttu-id="a9ee5-191">有効にした場合、自動復元は次のように機能します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-191">When enabled, automatic restore works as follows:</span></span>

1. <span data-ttu-id="a9ee5-192">ビルドが開始すると、Visual Studio はパッケージを復元するよう NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-192">When a build begins, Visual Studio instructs NuGet to restore packages.</span></span>
1. <span data-ttu-id="a9ee5-193">NuGet は、ソリューション内のすべての `packages.config` ファイルを再帰的に調べるか、`project.json` を調べるか、またはプロジェクト ファイル内を調べます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-193">NuGet recursively looks for all `packages.config` files in the solution, looks for `project.json`, or looks in the project file.</span></span>
1. <span data-ttu-id="a9ee5-194">参照ファイルに列記されている各パッケージについて、NuGet はソリューションに既に存在するかどうかを調べます (プロジェクトが `packages.config`、`project.json`、またはプロジェクト ファイル内のパッケージ参照のいずれを使っているかに応じて、`packages` フォルダー、`project.lock.json`、または `project.assets.json` を調べます)。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-194">For each packages listed in the reference files, NuGet checks if it already exists in the solution (the `packages` folder, `project.lock.json`, or `project.assets.json` depending on whether the project is using `packages.config`, `project.json`, or package references in project files).</span></span>
1. <span data-ttu-id="a9ee5-195">パッケージが見つからない場合、NuGet は最初にキャッシュからのパッケージの取得を試みます (「[NuGet のキャッシュを管理する](../consume-packages/managing-the-nuget-cache.md)」を参照)。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-195">If the package is not found, NuGet attempts to retrieve the package from its cache first (see [Managing the NuGet cache](../consume-packages/managing-the-nuget-cache.md).</span></span> <span data-ttu-id="a9ee5-196">パッケージがキャッシュにない場合、NuGet は **[ツール] > [オプション] > [NuGet パッケージ マネージャー] > [パッケージ ソース]** に列記されている有効なソースから、列記されている順序で、パッケージのダウンロードを試みます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-196">If the package is not in the cache, NuGet attempts to download the package from the enabled sources as listed in **Tools > Options > NuGet Package Manager > Package Sources**, in the order that the sources appear.</span></span> <span data-ttu-id="a9ee5-197">この場合、NuGet は、すべてのソースの確認が済むまでパッケージが見つからなかったことを示しません。すべてのソースを確認した時点で、リストの最後のソースについてのみ、エラーを報告します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-197">In this case, NuGet does not indicate a failure to find the package until all the sources have been checked, at which time it reports the failure only for the last source in the list.</span></span> <span data-ttu-id="a9ee5-198">このエラーが表示された場合は、他のソースについて個別にエラーが表示されなくても、パッケージがどのソースにも存在しなかったことを意味します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-198">By implication such an error also means that the package wasn't present on any of the other sources either, even though errors were not shown for those sources individually.</span></span>
1. <span data-ttu-id="a9ee5-199">ダウンロードが成功した場合、NuGet はパッケージをキャッシュに格納して、ソリューションにインストールします (やはり、`packages` フォルダー、`project.lock.json`、または `project.assets.json` に)。ダウンロードが成功しなかった場合、NuGet は失敗し、ビルドは行われません。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-199">If the download is successful, NuGet caches the package and installs it into the solution (again, into either the `packages` folder, `project.lock.json`, or `project.assets.json`); otherwise NuGet fails and the build fails.</span></span>

<span data-ttu-id="a9ee5-200">このプロセスの間、進行状況ダイアログが表示され、パッケージの復元をキャンセルできます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-200">During this process, you see a progress dialog with the option to cancel package restore.</span></span>

## <a name="package-restore-with-team-foundation-build"></a><span data-ttu-id="a9ee5-201">Team Foundation ビルドでのパッケージの復元</span><span class="sxs-lookup"><span data-stu-id="a9ee5-201">Package Restore with Team Foundation Build</span></span>

<span data-ttu-id="a9ee5-202">パッケージの復元は、一般に、Team Foundation Server (TFS) や Visual Studio Team Services (および、ここでは説明されていない他のビルド システム) と同様に、ビルド サーバーでプロジェクトをビルドするときに使われます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-202">Package restore is commonly used when building projects on build servers, as with Team Foundation Server (TFS) and Visual Studio Team Services (as well as other build systems, which are not covered here).</span></span>

### <a name="visual-studio-team-services"></a><span data-ttu-id="a9ee5-203">Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="a9ee5-203">Visual Studio Team Services</span></span>

<span data-ttu-id="a9ee5-204">Team Services でビルド定義を作成するときは、定義の他のビルド タスクの前に NuGet パッケージの復元タスクを単に追加します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-204">When creating a build definition on Team Services, simply include the Restore NuGet Packages task in the definition before any build task.</span></span> <span data-ttu-id="a9ee5-205">このタスクは、多くのビルド テンプレートに既定で含まれます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-205">This task is included by default in a number of build templates.</span></span>

![Visual Studio Team Service のビルド定義での NuGet パッケージの復元タスク](media/Restore-02-VSTSBuild.png)

### <a name="team-foundation-server"></a><span data-ttu-id="a9ee5-207">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="a9ee5-207">Team Foundation Server</span></span>

<span data-ttu-id="a9ee5-208">Team Foundation Server 2013 以降では、TFS 2013 以降用のチーム ビルド テンプレートを使っていると、ビルドの間に既定でパッケージが自動的に復元されます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-208">With TFS 2013 and later, packages are automatically restored by default during build, provided that you're using a Team Build Template for Team Foundation Server 2013 or later.</span></span>

<span data-ttu-id="a9ee5-209">以前のバージョンのビルド テンプレートを使っている場合は (以前のバージョンの TFS から移行したプロジェクトなど)、ビルド テンプレートも TFS 2013 に移行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-209">If you're using a previous version of build templates (such as in a project that's been migrated from earlier versions of TFS), you'll need to also migrate those build templates to TFS 2013.</span></span> <span data-ttu-id="a9ee5-210">これは基本的に、お使いのソース管理 (TFVC または Git) の適切なテンプレートを使って、ビルド テンプレートのカスタム部分を作成し直すことを意味します。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-210">This essentially means recreating the custom parts of the Build Templates using the appropriate template for your source control (TFVC or Git).</span></span>

<span data-ttu-id="a9ee5-211">以前のバージョンの TFS では、前に説明したように、ビルド ステップを含めるだけで[コマンド ライン復元](#command-line-restore)を開始できます。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-211">For earlier version of TFS, you can simply include a build step to invoke [command-line restore](#command-line-restore) as described earlier.</span></span>

<span data-ttu-id="a9ee5-212">詳しくは、「[Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md)」(Team Foundation ビルドでのパッケージの復元のチュートリアル) をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="a9ee5-212">For more details see then [Walkthrough of Package Restore with Team Foundation Build](../consume-packages/team-foundation-build.md).</span></span>    
