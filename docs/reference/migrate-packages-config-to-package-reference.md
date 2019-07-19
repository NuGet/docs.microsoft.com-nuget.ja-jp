---
title: App.config から PackageReference 形式への移行
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているように、プロジェクトを app.config 管理形式から PackageReference に移行する方法の詳細について説明します。
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 39f260835989cbbcc7293d9db27ac7b2c32debaa
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317231"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="b6090-103">App.config から PackageReference への移行</span><span class="sxs-lookup"><span data-stu-id="b6090-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="b6090-104">Visual Studio 2017 バージョン15.7 以降では、[パッケージ](./packages-config.md)の管理形式から[PackageReference](../consume-packages/Package-References-in-Project-Files.md)形式へのプロジェクトの移行がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="b6090-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="b6090-105">PackageReference を使用する利点</span><span class="sxs-lookup"><span data-stu-id="b6090-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="b6090-106">**すべてのプロジェクトの依存関係を1か所で管理**します。プロジェクト間参照やアセンブリ参照と同様に、NuGet パッケージ参照 ( `PackageReference`ノードを使用) は、個別のパッケージ .config ファイルを使用するのではなく、プロジェクトファイル内で直接管理されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="b6090-107">**最上位レベルの依存関係のすっきりしたビュー**:PackageReference とは異なり、では、プロジェクトに直接インストールした NuGet パッケージのみが一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="b6090-108">その結果、NuGet パッケージマネージャー UI とプロジェクトファイルが下位レベルの依存関係と共に乱雑になることはありません。</span><span class="sxs-lookup"><span data-stu-id="b6090-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="b6090-109">**パフォーマンスの向上**:PackageReference を使用する場合、パッケージは、ソリューション内の`packages`フォルダーではなく、グローバルパッケージ[とキャッシュフォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)に関するページで説明されているように、"*グローバルパッケージ*" フォルダーに保持されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="b6090-110">その結果、PackageReference のパフォーマンスが向上し、使用するディスク領域も少なくなります。</span><span class="sxs-lookup"><span data-stu-id="b6090-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="b6090-111">**依存関係とコンテンツフローを細かく制御し**ます。MSBuild の既存の機能を使用すると、 [NuGet パッケージを条件付きで参照](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)し、ターゲットフレームワーク、構成、プラットフォーム、またはその他のピボットごとにパッケージ参照を選択できます。</span><span class="sxs-lookup"><span data-stu-id="b6090-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="b6090-112">**PackageReference はアクティブな開発中**です。[GitHub の PackageReference の問題を](https://aka.ms/nuget-pr-improvements)参照してください。</span><span class="sxs-lookup"><span data-stu-id="b6090-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="b6090-113">app.config は、アクティブな開発ではなくなりました。</span><span class="sxs-lookup"><span data-stu-id="b6090-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="b6090-114">制限事項</span><span class="sxs-lookup"><span data-stu-id="b6090-114">Limitations</span></span>

* <span data-ttu-id="b6090-115">NuGet PackageReference は、Visual Studio 2015 以前では使用できません。</span><span class="sxs-lookup"><span data-stu-id="b6090-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="b6090-116">移行されたプロジェクトは、Visual Studio 2017 でのみ開くことができます。</span><span class="sxs-lookup"><span data-stu-id="b6090-116">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="b6090-117">C++ プロジェクトと ASP.NET プロジェクトについては、現在のところ、移行を利用できません。</span><span class="sxs-lookup"><span data-stu-id="b6090-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="b6090-118">一部のパッケージは、PackageReference と完全に互換性がない場合があります。</span><span class="sxs-lookup"><span data-stu-id="b6090-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="b6090-119">詳細については、「[パッケージの互換性の問題](#package-compatibility-issues)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b6090-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="b6090-120">既知の問題</span><span class="sxs-lookup"><span data-stu-id="b6090-120">Known Issues</span></span>

1. <span data-ttu-id="b6090-121">右クリックのコンテキスト メニューで `Migrate packages.config to PackageReference...` オプションを使用できない</span><span class="sxs-lookup"><span data-stu-id="b6090-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="b6090-122">懸案事項</span><span class="sxs-lookup"><span data-stu-id="b6090-122">Issue</span></span> 
 
<span data-ttu-id="b6090-123">プロジェクトを最初に開いたとき、NuGet 操作を行うまで NuGet が初期化されていない場合があります。</span><span class="sxs-lookup"><span data-stu-id="b6090-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="b6090-124">これにより、`packages.config` または `References` 上の右クリックのコンテキスト メニューで、移行オプションが表示されません。</span><span class="sxs-lookup"><span data-stu-id="b6090-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="b6090-125">回避策</span><span class="sxs-lookup"><span data-stu-id="b6090-125">Workaround</span></span> 

<span data-ttu-id="b6090-126">次の NuGet アクションのいずれかを実行します。</span><span class="sxs-lookup"><span data-stu-id="b6090-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="b6090-127">パッケージ マネージャー UI を開く - `References` を右クリックし、`Manage NuGet Packages...` を選択する</span><span class="sxs-lookup"><span data-stu-id="b6090-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="b6090-128">パッケージ マネージャー コンソールを開く - `Tools > NuGet Package Manager` から、`Package Manager Console` を選択する</span><span class="sxs-lookup"><span data-stu-id="b6090-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="b6090-129">NuGet 復元を実行する - ソリューション エクスプローラーのソリューション ノードを右クリックし、`Restore NuGet Packages` を選択する</span><span class="sxs-lookup"><span data-stu-id="b6090-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="b6090-130">NuGet 復元もトリガーするプロジェクトをビルドする</span><span class="sxs-lookup"><span data-stu-id="b6090-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="b6090-131">これで、移行オプションを表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="b6090-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="b6090-132">このオプションは ASP.NET と C++ のプロジェクト タイプではサポートされておらず、表示されません。</span><span class="sxs-lookup"><span data-stu-id="b6090-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="b6090-133">移行手順</span><span class="sxs-lookup"><span data-stu-id="b6090-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="b6090-134">移行を開始する前に、Visual Studio によってプロジェクトのバックアップが作成され、必要に応じて、 [app.config にロールバック](#how-to-roll-back-to-packagesconfig)できるようになります。</span><span class="sxs-lookup"><span data-stu-id="b6090-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="b6090-135">を使用して`packages.config`プロジェクトを含むソリューションを開きます。</span><span class="sxs-lookup"><span data-stu-id="b6090-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="b6090-136">**ソリューションエクスプローラー**で、 **[参照]** `packages.config`ノードまたはファイルを右クリックし、 **[パッケージを PackageReference に移行する]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="b6090-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="b6090-137">Migrator は、プロジェクトの NuGet パッケージ参照を分析し、**トップレベルの依存関係**(直接インストールされた nuget パッケージ) と**推移的な依存関係**(としてインストールされたパッケージ) に分類しようとします。最上位レベルのパッケージの依存関係)。</span><span class="sxs-lookup"><span data-stu-id="b6090-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="b6090-138">PackageReference は推移的なパッケージの復元をサポートし、依存関係を動的に解決します。つまり、推移的な依存関係を明示的にインストールする必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b6090-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="b6090-139">Optionalパッケージの**最上位レベル**のオプションを選択することで、依存関係として指定された NuGet パッケージを最上位レベルの依存関係として扱うことができます。</span><span class="sxs-lookup"><span data-stu-id="b6090-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="b6090-140">`build`このオプションは`analyzers` `buildCrossTargeting`、推移的(`developmentDependency = "true"`、、 、またはフォルダー内)ではなく、開発の依存関係()としてマークされている資産を含むパッケージに対して自動的に設定されます。`contentFiles`</span><span class="sxs-lookup"><span data-stu-id="b6090-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="b6090-141">パッケージの[互換性の問題](#package-compatibility-issues)を確認します。</span><span class="sxs-lookup"><span data-stu-id="b6090-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="b6090-142">**[OK]** を選択して移行を開始します。</span><span class="sxs-lookup"><span data-stu-id="b6090-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="b6090-143">移行の最後に、Visual Studio によって、バックアップのパス、インストールされているパッケージの一覧 (最上位の依存関係)、推移的な依存関係として参照されるパッケージの一覧、およびの開始時に識別される互換性の問題の一覧が表示されます。移動.</span><span class="sxs-lookup"><span data-stu-id="b6090-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="b6090-144">レポートがバックアップフォルダーに保存されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="b6090-145">ソリューションがビルドされ、実行されることを確認します。</span><span class="sxs-lookup"><span data-stu-id="b6090-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="b6090-146">問題が発生した場合は、 [GitHub で問題](https://github.com/NuGet/Home/issues/)を発生させることができます。</span><span class="sxs-lookup"><span data-stu-id="b6090-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="b6090-147">App.config にロールバックする方法</span><span class="sxs-lookup"><span data-stu-id="b6090-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="b6090-148">移行されたプロジェクトを閉じます。</span><span class="sxs-lookup"><span data-stu-id="b6090-148">Close the migrated project.</span></span>

1. <span data-ttu-id="b6090-149">プロジェクトファイルと`packages.config`バックアップ (通常は`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) をプロジェクトフォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="b6090-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="b6090-150">Obj フォルダーがプロジェクトのルートディレクトリに存在する場合は、削除します。</span><span class="sxs-lookup"><span data-stu-id="b6090-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="b6090-151">プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="b6090-151">Open the project.</span></span>

1. <span data-ttu-id="b6090-152">**[ツール > NuGet パッケージマネージャー > パッケージマネージャーコンソール]** メニューコマンドを使用して、パッケージマネージャーコンソールを開きます。</span><span class="sxs-lookup"><span data-stu-id="b6090-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="b6090-153">コンソールで次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="b6090-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="b6090-154">移行後にパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="b6090-154">Create a package after migration</span></span>

<span data-ttu-id="b6090-155">移行が完了したら、 [nuget. build. tasks. pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget パッケージへの参照を追加し、 [msbuild-](../reference/msbuild-targets.md#pack-target) n パッケージを使用してパッケージを作成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="b6090-155">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild -t:pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="b6090-156">`dotnet.exe pack` の`msbuild -t:pack`代わりにを使用できるシナリオもありますが、推奨されません。</span><span class="sxs-lookup"><span data-stu-id="b6090-156">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild -t:pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="b6090-157">パッケージの互換性の問題</span><span class="sxs-lookup"><span data-stu-id="b6090-157">Package compatibility issues</span></span>

<span data-ttu-id="b6090-158">PackageReference でサポートされていたいくつかの側面は、ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b6090-158">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="b6090-159">Migrator は、このような問題を分析して検出します。</span><span class="sxs-lookup"><span data-stu-id="b6090-159">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="b6090-160">次の問題が1つ以上発生するパッケージは、移行後に予期したとおりに動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b6090-160">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="b6090-161">移行後にパッケージをインストールすると、"install. ps1" スクリプトは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-161">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6090-162">**説明**</span><span class="sxs-lookup"><span data-stu-id="b6090-162">**Description**</span></span> | <span data-ttu-id="b6090-163">PackageReference では、パッケージをインストールまたはアンインストールするときに、ps1 と uninstall. ps1 PowerShell スクリプトは実行されません。</span><span class="sxs-lookup"><span data-stu-id="b6090-163">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="b6090-164">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="b6090-164">**Potential impact**</span></span> | <span data-ttu-id="b6090-165">これらのスクリプトに依存するパッケージは、変換先プロジェクトの動作を構成するために、期待どおりに機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="b6090-165">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="b6090-166">移行後にパッケージをインストールすると、"コンテンツ" 資産は使用できません。</span><span class="sxs-lookup"><span data-stu-id="b6090-166">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6090-167">**説明**</span><span class="sxs-lookup"><span data-stu-id="b6090-167">**Description**</span></span> | <span data-ttu-id="b6090-168">パッケージの`content`フォルダー内の資産は、PackageReference ではサポートされておらず、無視されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-168">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="b6090-169">PackageReference では、 `contentFiles`のサポートを追加して、推移的なサポートと共有コンテンツを向上させることができます。</span><span class="sxs-lookup"><span data-stu-id="b6090-169">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="b6090-170">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="b6090-170">**Potential impact**</span></span> | <span data-ttu-id="b6090-171">の資産`content`はプロジェクトにコピーされません。また、これらの資産の存在に依存するプロジェクトコードには、リファクタリングが必要です。</span><span class="sxs-lookup"><span data-stu-id="b6090-171">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="b6090-172">アップグレード後にパッケージをインストールするときに XDT 変換が適用されない</span><span class="sxs-lookup"><span data-stu-id="b6090-172">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6090-173">**説明**</span><span class="sxs-lookup"><span data-stu-id="b6090-173">**Description**</span></span> | <span data-ttu-id="b6090-174">Xdt 変換は PackageReference ではサポートさ`.xdt`れていません。パッケージをインストールまたはアンインストールするときに、ファイルは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-174">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="b6090-175">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="b6090-175">**Potential impact**</span></span> | <span data-ttu-id="b6090-176">Xdt 変換は、プロジェクトの XML ファイル (通常は) `web.config.install.xdt` `web.config.uninstall.xdt`には適用されません。つまり` web.config` 、パッケージをインストールまたはアンインストールしても、プロジェクトのファイルは更新されません。</span><span class="sxs-lookup"><span data-stu-id="b6090-176">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="b6090-177">移行後にパッケージをインストールすると、lib ルート内のアセンブリは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-177">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b6090-178">**説明**</span><span class="sxs-lookup"><span data-stu-id="b6090-178">**Description**</span></span> | <span data-ttu-id="b6090-179">PackageReference では、ターゲットフレームワーク固有のサブ`lib`フォルダーのないフォルダーのルートにあるアセンブリは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b6090-179">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="b6090-180">NuGet は、プロジェクトのターゲットフレームワークに対応するターゲットフレームワークモニカー (TFM) に一致するサブフォルダーを検索し、一致するアセンブリをプロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="b6090-180">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="b6090-181">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="b6090-181">**Potential impact**</span></span> | <span data-ttu-id="b6090-182">プロジェクトのターゲットフレームワークに対応するターゲットフレームワークモニカー (TFM) と一致するサブフォルダーがないパッケージは、移行後に予期したとおりに動作しないか、移行中にインストールが失敗する可能性があります</span><span class="sxs-lookup"><span data-stu-id="b6090-182">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="b6090-183">問題が見つかりましたか?</span><span class="sxs-lookup"><span data-stu-id="b6090-183">Found an issue?</span></span> <span data-ttu-id="b6090-184">レポートを作成します。</span><span class="sxs-lookup"><span data-stu-id="b6090-184">Report it!</span></span>

<span data-ttu-id="b6090-185">移行環境で問題が発生した場合は、 [NuGet GitHub リポジトリで問題](https://github.com/NuGet/Home/issues/)を報告してください。</span><span class="sxs-lookup"><span data-stu-id="b6090-185">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
