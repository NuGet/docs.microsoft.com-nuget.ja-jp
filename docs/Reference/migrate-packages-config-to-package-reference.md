---
title: Package.config から PackageReference 形式への移行
description: Package.config 管理形式から PackageReference NuGet 4.0 以降および VS2017 と .NET Core 2.0 でサポートされるようにプロジェクトを移行する方法の詳細
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/27/2018
ms.topic: conceptual
ms.openlocfilehash: 2b15d60d4f71fb2777e36c6a948ad72b4e2bc594
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="2278b-103">Packages.config から PackageReference への移行します。</span><span class="sxs-lookup"><span data-stu-id="2278b-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="2278b-104">Visual Studio 2017 バージョン 15.7 Preview 3 からプロジェクトを移行する以降をサポートして、 [packages.config](./packages-config.md)管理形式を[PackageReference](../consume-packages/Package-References-in-Project-Files.md)形式です。</span><span class="sxs-lookup"><span data-stu-id="2278b-104">Visual Studio 2017 Version 15.7 Preview 3 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="2278b-105">PackageReference を使用する利点</span><span class="sxs-lookup"><span data-stu-id="2278b-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="2278b-106">**1 つの場所でのすべてのプロジェクト依存関係の管理**: NuGet パッケージを参照してプロジェクト間参照とアセンブリ参照と同じように (を使用して、`PackageReference`ノード) を別々 のではなく、プロジェクト ファイル内で直接管理packages.config ファイル。</span><span class="sxs-lookup"><span data-stu-id="2278b-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="2278b-107">**最上位レベルの依存関係のっきりビュー**: packages.config とは異なり、PackageReference が直接、プロジェクトにインストールされている NuGet パッケージのみを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="2278b-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="2278b-108">その結果、NuGet パッケージ マネージャーの UI とプロジェクト ファイルは下位レベルの依存関係を持つ整理されています。</span><span class="sxs-lookup"><span data-stu-id="2278b-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="2278b-109">**パフォーマンスの向上**: PackageReference を使用すると、パッケージが管理で、*グローバル パッケージ*フォルダー (の定義に従って[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)なく、`packages`ソリューション内のフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="2278b-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="2278b-110">その結果、PackageReference は高速に実行し、少ないディスク領域を使用します。</span><span class="sxs-lookup"><span data-stu-id="2278b-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="2278b-111">**依存関係とコンテンツのフロー制御を微調整**: MSBuild の既存の機能を使用することにより[条件付きで、NuGet パッケージを参照](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)ターゲット フレームワークでごとのパッケージ参照の選択と構成では、プラットフォーム、またはその他のピボットします。</span><span class="sxs-lookup"><span data-stu-id="2278b-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="2278b-112">**アクティブな開発では、PackageReference**: を参照してください[PackageReference が GitHub の問題](https://aka.ms/nuget-pr-improvements)です。</span><span class="sxs-lookup"><span data-stu-id="2278b-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="2278b-113">packages.config がアクティブな開発ではなくなりました。</span><span class="sxs-lookup"><span data-stu-id="2278b-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="2278b-114">制限事項</span><span class="sxs-lookup"><span data-stu-id="2278b-114">Limitations</span></span>

* <span data-ttu-id="2278b-115">NuGet PackageReference は、Visual Studio 2015 で利用可能な以前ではありません。</span><span class="sxs-lookup"><span data-stu-id="2278b-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="2278b-116">移行後のプロジェクトは、Visual Studio 2017 でのみ開くことができます。</span><span class="sxs-lookup"><span data-stu-id="2278b-116">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="2278b-117">移行は、C++ と ASP.NET プロジェクトに使用できる現在ではありません。</span><span class="sxs-lookup"><span data-stu-id="2278b-117">Migration is not currently available for C++ and ASP.NET project.</span></span>
* <span data-ttu-id="2278b-118">一部のパッケージは、PackageReference と完全に互換性ない場合があります。</span><span class="sxs-lookup"><span data-stu-id="2278b-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="2278b-119">詳細については、次を参照してください。[互換性の問題をパッケージ化](#package-compatibility-issues)です。</span><span class="sxs-lookup"><span data-stu-id="2278b-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

## <a name="migration-steps"></a><span data-ttu-id="2278b-120">移行手順</span><span class="sxs-lookup"><span data-stu-id="2278b-120">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="2278b-121">Visual Studio ができるようにするには、プロジェクトのバックアップを作成する移行を開始する前に[packages.config にロールバック](#how-to-roll-back-to-packagesconfig)必要な場合です。</span><span class="sxs-lookup"><span data-stu-id="2278b-121">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="2278b-122">使用してプロジェクトを含むソリューションを開く`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="2278b-122">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="2278b-123">**ソリューション エクスプ ローラー**を右クリックし、**参照**ノードまたは`packages.config`ファイルおよび選択した**PackageReference に packages.config を移行しています.**.</span><span class="sxs-lookup"><span data-stu-id="2278b-123">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="2278b-124">Migrator は、プロジェクトの NuGet パッケージの参照を分析しに分類しようとしています**最上位レベルの依存関係**(NuGet パッケージをインストールしたディレクトリ) および**推移的な依存関係**。(最上位のパッケージの依存関係としてインストールされたパッケージ)。</span><span class="sxs-lookup"><span data-stu-id="2278b-124">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directory) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="2278b-125">PackageReference 推移的なパッケージの復元をサポートし、解決の依存関係、動的に依存関係が推移的な必要なインストールしないことに明示的に意味します。</span><span class="sxs-lookup"><span data-stu-id="2278b-125">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="2278b-126">(省略可能)選択すると、最上位レベルの依存関係として、推移的な依存関係として分類された NuGet パッケージを処理することもできます、**トップレベル**パッケージのオプションです。</span><span class="sxs-lookup"><span data-stu-id="2278b-126">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="2278b-127">このオプションは推移的にフローしないアセットを含むパッケージを自動的に設定 (内、 `build`、 `buildCrossTargeting`、 `contentFiles`、または`analyzers`フォルダー)、開発の依存関係としてマークされているものと (`developmentDependency = "true"`)。</span><span class="sxs-lookup"><span data-stu-id="2278b-127">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="2278b-128">いずれかを確認[互換性の問題をパッケージ化](#package-compatibility-issues)です。</span><span class="sxs-lookup"><span data-stu-id="2278b-128">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="2278b-129">選択**OK**移行を開始します。</span><span class="sxs-lookup"><span data-stu-id="2278b-129">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="2278b-130">移行の最後に、Visual Studio が、バックアップ、インストールされているパッケージ (最上位レベルの依存関係) の一覧、推移的な依存関係として参照されるパッケージの一覧およびの開始時に特定の互換性の問題の一覧にパスを含むレポートを提供します。移行します。</span><span class="sxs-lookup"><span data-stu-id="2278b-130">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="2278b-131">レポートは、バックアップ フォルダーに保存されます。</span><span class="sxs-lookup"><span data-stu-id="2278b-131">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="2278b-132">ソリューションがビルドされ、実行されることを検証します。</span><span class="sxs-lookup"><span data-stu-id="2278b-132">Validate that the solution builds and runs.</span></span> <span data-ttu-id="2278b-133">問題が発生した場合[GitHub の問題を報告](https://github.com/NuGet/Home/issues/)です。</span><span class="sxs-lookup"><span data-stu-id="2278b-133">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="2278b-134">Packages.config をロールバックする方法</span><span class="sxs-lookup"><span data-stu-id="2278b-134">How to roll back to packages.config</span></span>

1. <span data-ttu-id="2278b-135">移行されたプロジェクトを閉じます。</span><span class="sxs-lookup"><span data-stu-id="2278b-135">Close the migrated project.</span></span>

1. <span data-ttu-id="2278b-136">プロジェクト ファイルをコピーし、`packages.config`バックアップから (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) プロジェクトのフォルダーにします。</span><span class="sxs-lookup"><span data-stu-id="2278b-136">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span>

1. <span data-ttu-id="2278b-137">プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="2278b-137">Open the project.</span></span>

1. <span data-ttu-id="2278b-138">使用してパッケージ マネージャー コンソールを開き、**ツール > NuGet Package Manager > パッケージ マネージャー コンソール**メニュー コマンド。</span><span class="sxs-lookup"><span data-stu-id="2278b-138">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="2278b-139">コンソールで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="2278b-139">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="package-compatibility-issues"></a><span data-ttu-id="2278b-140">パッケージの互換性の問題</span><span class="sxs-lookup"><span data-stu-id="2278b-140">Package compatibility issues</span></span>

<span data-ttu-id="2278b-141">Packages.config にサポートされていた一部の機能は、PackageReference でサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="2278b-141">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="2278b-142">Migrator は、分析し、このような問題を検出します。</span><span class="sxs-lookup"><span data-stu-id="2278b-142">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="2278b-143">次の問題の 1 つ以上を持つすべてのパッケージは、移行後に期待どおりに動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="2278b-143">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="2278b-144">移行後に、パッケージがインストールされている場合、"install.ps1"スクリプトは無視されます。</span><span class="sxs-lookup"><span data-stu-id="2278b-144">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="2278b-145">**説明**</span><span class="sxs-lookup"><span data-stu-id="2278b-145">**Description**</span></span> | <span data-ttu-id="2278b-146">PackageReference をインストールしたり、パッケージのアンインストール中に install.ps1 および uninstall.ps1 PowerShell スクリプトは実行されません。</span><span class="sxs-lookup"><span data-stu-id="2278b-146">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="2278b-147">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="2278b-147">**Potential impact**</span></span> | <span data-ttu-id="2278b-148">ターゲット プロジェクトにいくつかの動作を構成するこれらのスクリプトに依存しているパッケージには、期待どおりに動かないことがあります。</span><span class="sxs-lookup"><span data-stu-id="2278b-148">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="2278b-149">"content"資産は、移行後に、パッケージがインストールされている場合は使用できません。</span><span class="sxs-lookup"><span data-stu-id="2278b-149">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="2278b-150">**説明**</span><span class="sxs-lookup"><span data-stu-id="2278b-150">**Description**</span></span> | <span data-ttu-id="2278b-151">パッケージの内の資産`content`フォルダー PackageReference がサポートされていないは無視されます。</span><span class="sxs-lookup"><span data-stu-id="2278b-151">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="2278b-152">PackageReference サポートを追加する`contentFiles`より推移的なサポートと共有のコンテンツが必要です。</span><span class="sxs-lookup"><span data-stu-id="2278b-152">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="2278b-153">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="2278b-153">**Potential impact**</span></span> | <span data-ttu-id="2278b-154">内の資産`content`はコピーされませんプロジェクトとプロジェクト、それらの資産の存在に依存するコードが必要なにリファクタリングします。</span><span class="sxs-lookup"><span data-stu-id="2278b-154">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="2278b-155">XDT 変換は、アップグレード後に、パッケージがインストールされているときに適用されません。</span><span class="sxs-lookup"><span data-stu-id="2278b-155">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="2278b-156">**説明**</span><span class="sxs-lookup"><span data-stu-id="2278b-156">**Description**</span></span> | <span data-ttu-id="2278b-157">PackageReference XDT 変換はサポートされず`.xdt`インストールまたはパッケージをアンインストールするときに、ファイルは無視されます。</span><span class="sxs-lookup"><span data-stu-id="2278b-157">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="2278b-158">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="2278b-158">**Potential impact**</span></span> | <span data-ttu-id="2278b-159">XDT いない変換は、プロジェクトの XML ファイルを一般的に、`web.config.install.xdt`と`web.config.uninstall.xdt`、つまり、プロジェクトの` web.config`パッケージをインストールまたはアンインストールする場合、ファイルは更新されません。</span><span class="sxs-lookup"><span data-stu-id="2278b-159">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="2278b-160">移行後に、パッケージがインストールされているときに lib ルート内のアセンブリは無視されます。</span><span class="sxs-lookup"><span data-stu-id="2278b-160">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="2278b-161">**説明**</span><span class="sxs-lookup"><span data-stu-id="2278b-161">**Description**</span></span> | <span data-ttu-id="2278b-162">ルートに存在するアセンブリ PackageReference で`lib`ターゲット フレームワークの特定サブ フォルダーがないフォルダーは無視されます。</span><span class="sxs-lookup"><span data-stu-id="2278b-162">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="2278b-163">NuGet は、プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブ フォルダーを検索し、プロジェクトに一致するアセンブリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="2278b-163">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="2278b-164">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="2278b-164">**Potential impact**</span></span> | <span data-ttu-id="2278b-165">プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブ フォルダーがないパッケージの移行後に期待どおりに動作または移行中にインストールが失敗する可能性がありますいません。</span><span class="sxs-lookup"><span data-stu-id="2278b-165">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="2278b-166">問題を発見しますか。</span><span class="sxs-lookup"><span data-stu-id="2278b-166">Found an issue?</span></span> <span data-ttu-id="2278b-167">報告してください。</span><span class="sxs-lookup"><span data-stu-id="2278b-167">Report it!</span></span>

<span data-ttu-id="2278b-168">問題は、移行操作を実行する場合は、次のようにしてください。 [NuGet GitHub リポジトリのファイルの問題](https://github.com/NuGet/Home/issues/)です。</span><span class="sxs-lookup"><span data-stu-id="2278b-168">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
