---
title: package.config から PackageReference 形式への移行
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているように、プロジェクトを package.config 管理形式から PackageReference に移行する方法について詳しく説明します
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 8e825410d621ff2946e23e80173292f24f9d21f2
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428523"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="93724-103">packages.config から PackageReference への移行</span><span class="sxs-lookup"><span data-stu-id="93724-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="93724-104">Visual Studio 2017 バージョン 15.7 以降では、[packages.config](../reference/packages-config.md) 管理形式から [PackageReference](../consume-packages/Package-References-in-Project-Files.md) 形式へのプロジェクトの移行がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="93724-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](../reference/packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="93724-105">PackageReference を使用する利点</span><span class="sxs-lookup"><span data-stu-id="93724-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="93724-106">**すべてのプロジェクトの依存関係を 1 か所で管理**:プロジェクト間参照やアセンブリ参照と同様に、NuGet パッケージ参照 (`PackageReference` ノードを使用) は、個別の packages.config ファイルを使用するのではなく、プロジェクト ファイル内で直接管理されます。</span><span class="sxs-lookup"><span data-stu-id="93724-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="93724-107">**最上位の依存関係のすっきりしたビュー**:packages.config とは異なり、PackageReference では、プロジェクトに直接インストールした NuGet パッケージのみが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="93724-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="93724-108">その結果、NuGet パッケージ マネージャー UI とプロジェクト ファイルが下位レベルの依存関係によって乱雑になることはありません。</span><span class="sxs-lookup"><span data-stu-id="93724-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="93724-109">**パフォーマンスの向上**:PackageReference を使用する場合、(「[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)」で説明されているように) パッケージはソリューション内の `packages` フォルダーではなく "*グローバル パッケージ*" フォルダー内で管理されます。</span><span class="sxs-lookup"><span data-stu-id="93724-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="93724-110">その結果、PackageReference のパフォーマンスが向上し、使用するディスク領域も少なくなります。</span><span class="sxs-lookup"><span data-stu-id="93724-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="93724-111">**依存関係とコンテンツ フローのきめ細かな制御**:MSBuild の既存の機能を使用して、[NuGet パッケージを条件付きで参照](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)し、ターゲット フレームワーク、構成、プラットフォーム、またはその他のピボットごとにパッケージ参照を選択できます。</span><span class="sxs-lookup"><span data-stu-id="93724-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="93724-112">**PackageReference はアクティブに開発中**:[GitHub 上の PackageReference の問題](https://aka.ms/nuget-pr-improvements)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="93724-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="93724-113">packages.config の開発は現在継続されていません。</span><span class="sxs-lookup"><span data-stu-id="93724-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="93724-114">制限事項</span><span class="sxs-lookup"><span data-stu-id="93724-114">Limitations</span></span>

* <span data-ttu-id="93724-115">NuGet PackageReference は、Visual Studio 2015 以前では使用できません。</span><span class="sxs-lookup"><span data-stu-id="93724-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="93724-116">移行されたプロジェクトは、Visual Studio 2017 以降でのみ開くことができます。</span><span class="sxs-lookup"><span data-stu-id="93724-116">Migrated projects can be opened only in Visual Studio 2017 and later.</span></span>
* <span data-ttu-id="93724-117">C++ プロジェクトと ASP.NET プロジェクトについては、現在のところ、移行を利用できません。</span><span class="sxs-lookup"><span data-stu-id="93724-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="93724-118">一部のパッケージは、PackageReference と完全に互換ではない場合があります。</span><span class="sxs-lookup"><span data-stu-id="93724-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="93724-119">詳しくは、「[パッケージの互換性の問題](#package-compatibility-issues)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="93724-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

<span data-ttu-id="93724-120">また、PackageReferences のしくみには、packages.config と比べていくつかの違いがあります。たとえば、[アップグレード バージョンを制限する](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)ことは、PackageReference ではサポートされていませんが、[浮動小数点バージョン](../consume-packages/package-references-in-project-files.md#floating-versions)のサポートが追加されています。</span><span class="sxs-lookup"><span data-stu-id="93724-120">In addition, there are some differences in how PackageReferences work compared to packages.config. For example - [constraining upgrade versions](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions) is not supprted by PackageReference but add support for [Floating Versions](../consume-packages/package-references-in-project-files.md#floating-versions).</span></span>

### <a name="known-issues"></a><span data-ttu-id="93724-121">既知の問題</span><span class="sxs-lookup"><span data-stu-id="93724-121">Known Issues</span></span>

1. <span data-ttu-id="93724-122">右クリックのコンテキスト メニューで `Migrate packages.config to PackageReference...` オプションを使用できない</span><span class="sxs-lookup"><span data-stu-id="93724-122">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="93724-123">懸案事項</span><span class="sxs-lookup"><span data-stu-id="93724-123">Issue</span></span> 
 
<span data-ttu-id="93724-124">プロジェクトを最初に開いたとき、NuGet 操作を行うまで NuGet が初期化されていない場合があります。</span><span class="sxs-lookup"><span data-stu-id="93724-124">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="93724-125">これにより、`packages.config` または `References` 上の右クリックのコンテキスト メニューで、移行オプションが表示されません。</span><span class="sxs-lookup"><span data-stu-id="93724-125">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="93724-126">回避策</span><span class="sxs-lookup"><span data-stu-id="93724-126">Workaround</span></span> 

<span data-ttu-id="93724-127">次の NuGet アクションのいずれかを実行します。</span><span class="sxs-lookup"><span data-stu-id="93724-127">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="93724-128">パッケージ マネージャー UI を開く - `References` を右クリックし、`Manage NuGet Packages...` を選択する</span><span class="sxs-lookup"><span data-stu-id="93724-128">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="93724-129">パッケージ マネージャー コンソールを開く - `Tools > NuGet Package Manager` から、`Package Manager Console` を選択する</span><span class="sxs-lookup"><span data-stu-id="93724-129">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="93724-130">NuGet 復元を実行する - ソリューション エクスプローラーのソリューション ノードを右クリックし、`Restore NuGet Packages` を選択する</span><span class="sxs-lookup"><span data-stu-id="93724-130">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="93724-131">NuGet 復元もトリガーするプロジェクトをビルドする</span><span class="sxs-lookup"><span data-stu-id="93724-131">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="93724-132">これで、移行オプションを表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="93724-132">You should now be able to see the migration option.</span></span> <span data-ttu-id="93724-133">このオプションは ASP.NET と C++ のプロジェクト タイプではサポートされておらず、表示されません。</span><span class="sxs-lookup"><span data-stu-id="93724-133">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="93724-134">移行の手順</span><span class="sxs-lookup"><span data-stu-id="93724-134">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="93724-135">移行を開始する前に、必要に応じて [packages.config にロールバック](#how-to-roll-back-to-packagesconfig)できるように Visual Studio によってプロジェクトのバックアップが作成されます。</span><span class="sxs-lookup"><span data-stu-id="93724-135">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="93724-136">`packages.config` を使用してプロジェクトを含むソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="93724-136">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="93724-137">**ソリューション エクスプローラー**で、 **[参照]** ノードまたは `packages.config` ファイルを右クリックし、 **[packages.config を PackageReference に移行する...]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="93724-137">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="93724-138">移行プログラムによってプロジェクトの NuGet パッケージ参照が分析され、**最上位の依存関係** (直接インストールした NuGet パッケージ) と**推移的依存関係** (最上位のパッケージの依存関係としてインストールされたパッケージ) への分類が試行されます。</span><span class="sxs-lookup"><span data-stu-id="93724-138">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="93724-139">PackageReference では推移的なパッケージの復元がサポートされ、依存関係が動的に解決されます。つまり、推移的依存関係を明示的にインストールする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="93724-139">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="93724-140">(省略可能) パッケージに対して **[最上位]** オプションを選択することで、推移的依存関係として分類された NuGet パッケージを最上位の依存関係として扱うことを選択できます。</span><span class="sxs-lookup"><span data-stu-id="93724-140">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="93724-141">このオプションは、推移的にフローしないアセットを含む (`build`、`buildCrossTargeting`、`contentFiles`、または `analyzers` フォルダー内にある) パッケージと、開発の依存関係 (`developmentDependency = "true"`) としてマークされているパッケージに対して自動的に設定されます。</span><span class="sxs-lookup"><span data-stu-id="93724-141">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="93724-142">「[パッケージの互換性の問題](#package-compatibility-issues)」をご確認ください。</span><span class="sxs-lookup"><span data-stu-id="93724-142">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="93724-143">**[OK]** を選択して移行を開始します。</span><span class="sxs-lookup"><span data-stu-id="93724-143">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="93724-144">移行の最後に、Visual Studio によって、バックアップのパス、インストールされているパッケージの一覧 (最上位の依存関係)、推移的依存関係として参照されるパッケージの一覧、移行の開始時に識別される互換性の問題の一覧に関するレポートが提供されます。</span><span class="sxs-lookup"><span data-stu-id="93724-144">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="93724-145">レポートがバックアップ フォルダーに保存されます。</span><span class="sxs-lookup"><span data-stu-id="93724-145">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="93724-146">ソリューションがビルドされ、実行されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="93724-146">Validate that the solution builds and runs.</span></span> <span data-ttu-id="93724-147">問題が発生した場合は、[問題を GitHub に報告](https://github.com/NuGet/Home/issues/)します。</span><span class="sxs-lookup"><span data-stu-id="93724-147">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="93724-148">packages.config にロールバックする方法</span><span class="sxs-lookup"><span data-stu-id="93724-148">How to roll back to packages.config</span></span>

1. <span data-ttu-id="93724-149">移行されたプロジェクトを閉じます。</span><span class="sxs-lookup"><span data-stu-id="93724-149">Close the migrated project.</span></span>

1. <span data-ttu-id="93724-150">プロジェクト ファイルと `packages.config` をバックアップ (通常は `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) からプロジェクト フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="93724-150">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="93724-151">obj フォルダーがプロジェクトのルート ディレクトリに存在する場合は、これを削除します。</span><span class="sxs-lookup"><span data-stu-id="93724-151">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="93724-152">プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="93724-152">Open the project.</span></span>

1. <span data-ttu-id="93724-153">**[ツール] > [NuGet パッケージ マネージャー] > [パッケージ マネージャー コンソール]** メニュー コマンドを使用して [パッケージ マネージャー コンソール] を開きます。</span><span class="sxs-lookup"><span data-stu-id="93724-153">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="93724-154">コンソール内で、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="93724-154">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="93724-155">移行後にパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="93724-155">Create a package after migration</span></span>

<span data-ttu-id="93724-156">移行が完了したら [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget パッケージへの参照を追加し、[msbuild -t:pack](../reference/msbuild-targets.md#pack-target) を使用してパッケージを作成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="93724-156">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="93724-157">`msbuild -t:pack` の代わりに `dotnet.exe pack` を使用できるシナリオもありますが、推奨されません。</span><span class="sxs-lookup"><span data-stu-id="93724-157">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="93724-158">パッケージの互換性の問題</span><span class="sxs-lookup"><span data-stu-id="93724-158">Package compatibility issues</span></span>

<span data-ttu-id="93724-159">packages.config でサポートされていたいくつかの機能は、PackageReference ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="93724-159">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="93724-160">移行プログラムでは、このような問題が分析および検出されます。</span><span class="sxs-lookup"><span data-stu-id="93724-160">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="93724-161">以下の問題が 1 つ以上あるパッケージは、移行後に期待どおりに動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="93724-161">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="93724-162">移行後にパッケージをインストールするときに、"install. ps1" スクリプトが無視される</span><span class="sxs-lookup"><span data-stu-id="93724-162">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="93724-163">**説明**</span><span class="sxs-lookup"><span data-stu-id="93724-163">**Description**</span></span> | <span data-ttu-id="93724-164">PackageReference では、パッケージをインストールまたはアンインストールするときに、install.ps1 および uninstall.ps1 PowerShell スクリプトは実行されません。</span><span class="sxs-lookup"><span data-stu-id="93724-164">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="93724-165">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="93724-165">**Potential impact**</span></span> | <span data-ttu-id="93724-166">これらのスクリプトに依存して移行先プロジェクト内の一部の動作を構成するパッケージは、期待どおりに動作しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="93724-166">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="93724-167">移行後にパッケージをインストールするときに、"コンテンツ" アセットを使用できない</span><span class="sxs-lookup"><span data-stu-id="93724-167">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="93724-168">**説明**</span><span class="sxs-lookup"><span data-stu-id="93724-168">**Description**</span></span> | <span data-ttu-id="93724-169">パッケージの `content` フォルダー内のアセットは、PackageReference ではサポートされず、無視されます。</span><span class="sxs-lookup"><span data-stu-id="93724-169">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="93724-170">PackageReference では、推移的なサポートと共有コンテンツを向上させるために `contentFiles` のサポートが追加されています。</span><span class="sxs-lookup"><span data-stu-id="93724-170">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="93724-171">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="93724-171">**Potential impact**</span></span> | <span data-ttu-id="93724-172">`content` 内のアセットはプロジェクトにコピーされず、これらのアセットの存在に依存するプロジェクト コードにはリファクタリングが必要です。</span><span class="sxs-lookup"><span data-stu-id="93724-172">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="93724-173">アップグレード後にパッケージをインストールするときに XDT 変換が適用されない</span><span class="sxs-lookup"><span data-stu-id="93724-173">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="93724-174">**説明**</span><span class="sxs-lookup"><span data-stu-id="93724-174">**Description**</span></span> | <span data-ttu-id="93724-175">XDT 変換は PackageReference ではサポートされず、パッケージをインストールまたはアンインストールするときに `.xdt` ファイルは無視されます。</span><span class="sxs-lookup"><span data-stu-id="93724-175">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="93724-176">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="93724-176">**Potential impact**</span></span> | <span data-ttu-id="93724-177">XDT 変換は、プロジェクトの XML ファイル (通常は `web.config.install.xdt` と `web.config.uninstall.xdt`) には適用されません。つまり、パッケージをインストールまたはアンインストールしても、プロジェクトの ` web.config` ファイルは更新されません。</span><span class="sxs-lookup"><span data-stu-id="93724-177">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="93724-178">移行後にパッケージをインストールするときに、lib ルート内のアセンブリが無視される</span><span class="sxs-lookup"><span data-stu-id="93724-178">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="93724-179">**説明**</span><span class="sxs-lookup"><span data-stu-id="93724-179">**Description**</span></span> | <span data-ttu-id="93724-180">PackageReference では、ターゲット フレームワーク固有のサブフォルダーがない `lib` フォルダーのルートにあるアセンブリは無視されます。</span><span class="sxs-lookup"><span data-stu-id="93724-180">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="93724-181">NuGet では、プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブフォルダーが検索され、一致するアセンブリがプロジェクトにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="93724-181">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="93724-182">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="93724-182">**Potential impact**</span></span> | <span data-ttu-id="93724-183">プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) と一致するサブフォルダーがないパッケージは、移行後に期待どおりに動作しない場合や、移行中にインストールが失敗する場合があります</span><span class="sxs-lookup"><span data-stu-id="93724-183">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="93724-184">見つかった問題の</span><span class="sxs-lookup"><span data-stu-id="93724-184">Found an issue?</span></span> <span data-ttu-id="93724-185">報告</span><span class="sxs-lookup"><span data-stu-id="93724-185">Report it!</span></span>

<span data-ttu-id="93724-186">移行のエクスペリエンスに問題が発生した場合は、[NuGet GitHub リポジトリに問題を報告](https://github.com/NuGet/Home/issues/)してください。</span><span class="sxs-lookup"><span data-stu-id="93724-186">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
