---
title: Package.config から PackageReference 形式への移行
description: NuGet 4.0 + と VS2017 および .NET Core 2.0 でサポートされている PackageReference に package.config 管理形式からプロジェクトを移行する方法の詳細について
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: 09d132aeaf00d2a1d095b9638b455cc23de91f2c
ms.sourcegitcommit: b8c63744252a5a37a2843f6bc1d5917496ee40dd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2019
ms.locfileid: "66812878"
---
# <a name="migrate-from-packagesconfig-to-packagereference"></a><span data-ttu-id="b7014-103">Packages.config から PackageReference に移行します。</span><span class="sxs-lookup"><span data-stu-id="b7014-103">Migrate from packages.config to PackageReference</span></span>

<span data-ttu-id="b7014-104">以降のサポートからプロジェクトを移行している visual Studio 2017 バージョン 15.7年、 [packages.config](./packages-config.md)管理形式を[PackageReference](../consume-packages/Package-References-in-Project-Files.md)形式。</span><span class="sxs-lookup"><span data-stu-id="b7014-104">Visual Studio 2017 Version 15.7 and later supports migrating a project from the [packages.config](./packages-config.md) management format to the [PackageReference](../consume-packages/Package-References-in-Project-Files.md) format.</span></span>

## <a name="benefits-of-using-packagereference"></a><span data-ttu-id="b7014-105">PackageReference を使用する利点</span><span class="sxs-lookup"><span data-stu-id="b7014-105">Benefits of using PackageReference</span></span>

* <span data-ttu-id="b7014-106">**1 か所ですべてのプロジェクトの依存関係を管理**:プロジェクト間参照とアセンブリの参照では、同様の NuGet パッケージの参照 (を使用して、`PackageReference`ノード)、別個の packages.config ファイルを使用するのではなく、プロジェクト ファイル内で直接管理されます。</span><span class="sxs-lookup"><span data-stu-id="b7014-106">**Manage all project dependencies in one place**: Just like project to project references and assembly references, NuGet package references (using the `PackageReference` node) are managed directly within project files rather than using a separate packages.config file.</span></span>
* <span data-ttu-id="b7014-107">**最上位レベルの依存関係の表示をすっきり**:Packages.config とは異なり PackageReference には、直接プロジェクトにインストールされている NuGet パッケージのみが一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="b7014-107">**Uncluttered view of top-level dependencies**: Unlike packages.config, PackageReference lists only those NuGet packages you directly installed in the project.</span></span> <span data-ttu-id="b7014-108">その結果、NuGet パッケージ マネージャー UI とプロジェクト ファイルは、下位レベルの依存関係を持つ乱雑はありません。</span><span class="sxs-lookup"><span data-stu-id="b7014-108">As a result, the NuGet Package Manager UI and the project file aren't cluttered with down-level dependencies.</span></span>
* <span data-ttu-id="b7014-109">**パフォーマンスの向上**:パッケージを管理する PackageReference を使用する場合、*グローバル パッケージ*フォルダー (上の説明に従って[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)なく、`packages`フォルダー内で、ソリューションです。</span><span class="sxs-lookup"><span data-stu-id="b7014-109">**Performance improvements**: When using PackageReference, packages are maintained in the *global-packages* folder (as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md) rather than in a `packages` folder within the solution.</span></span> <span data-ttu-id="b7014-110">その結果、PackageReference は高速に実行し、少ないディスク領域を使用します。</span><span class="sxs-lookup"><span data-stu-id="b7014-110">As a result, PackageReference performs faster and consumes less disk space.</span></span>
* <span data-ttu-id="b7014-111">**依存関係とコンテンツのフロー制御を細かく**:MSBuild の既存の機能を使用することにより[条件付きで NuGet パッケージを参照](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition)ターゲット フレームワーク、構成、プラットフォーム、またはその他のピボットごとにパッケージ参照を選択します。</span><span class="sxs-lookup"><span data-stu-id="b7014-111">**Fine control over dependencies and content flow**: Using the existing features of MSBuild allows you to [conditionally reference a NuGet package](../consume-packages/Package-References-in-Project-Files.md#adding-a-packagereference-condition) and choose package references per target framework, configuration, platform, or other pivots.</span></span>
* <span data-ttu-id="b7014-112">**PackageReference は開発**:参照してください[PackageReference の GitHub 問題](https://aka.ms/nuget-pr-improvements)します。</span><span class="sxs-lookup"><span data-stu-id="b7014-112">**PackageReference is under active development**: See [PackageReference issues on GitHub](https://aka.ms/nuget-pr-improvements).</span></span> <span data-ttu-id="b7014-113">packages.config は、アクティブな開発ではなくなりました。</span><span class="sxs-lookup"><span data-stu-id="b7014-113">packages.config is no longer under active development.</span></span>

### <a name="limitations"></a><span data-ttu-id="b7014-114">制限事項</span><span class="sxs-lookup"><span data-stu-id="b7014-114">Limitations</span></span>

* <span data-ttu-id="b7014-115">NuGet PackageReference は Visual Studio 2015 で使用でき、以前ではありません。</span><span class="sxs-lookup"><span data-stu-id="b7014-115">NuGet PackageReference is not available in Visual Studio 2015 and earlier.</span></span> <span data-ttu-id="b7014-116">移行されたプロジェクトは、Visual Studio 2017 でのみ開くことができます。</span><span class="sxs-lookup"><span data-stu-id="b7014-116">Migrated projects can be opened only in Visual Studio 2017.</span></span>
* <span data-ttu-id="b7014-117">移行は、C++、ASP.NET プロジェクトを現在ご利用いただけません。</span><span class="sxs-lookup"><span data-stu-id="b7014-117">Migration is not currently available for C++ and ASP.NET projects.</span></span>
* <span data-ttu-id="b7014-118">いくつかのパッケージは、PackageReference と完全に互換性がない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b7014-118">Some packages may not be fully compatible with PackageReference.</span></span> <span data-ttu-id="b7014-119">詳細については、次を参照してください。[互換性の問題をパッケージ化](#package-compatibility-issues)します。</span><span class="sxs-lookup"><span data-stu-id="b7014-119">For more information, see [package compatibility issues](#package-compatibility-issues).</span></span>

### <a name="known-issues"></a><span data-ttu-id="b7014-120">既知の問題</span><span class="sxs-lookup"><span data-stu-id="b7014-120">Known Issues</span></span>

1. <span data-ttu-id="b7014-121">右クリックのコンテキスト メニューで `Migrate packages.config to PackageReference...` オプションを使用できない</span><span class="sxs-lookup"><span data-stu-id="b7014-121">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span> 

#### <a name="issue"></a><span data-ttu-id="b7014-122">懸案事項</span><span class="sxs-lookup"><span data-stu-id="b7014-122">Issue</span></span> 
 
<span data-ttu-id="b7014-123">プロジェクトを最初に開いたとき、NuGet 操作を行うまで NuGet が初期化されていない場合があります。</span><span class="sxs-lookup"><span data-stu-id="b7014-123">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="b7014-124">これにより、`packages.config` または `References` 上の右クリックのコンテキスト メニューで、移行オプションが表示されません。</span><span class="sxs-lookup"><span data-stu-id="b7014-124">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span> 

#### <a name="workaround"></a><span data-ttu-id="b7014-125">回避策</span><span class="sxs-lookup"><span data-stu-id="b7014-125">Workaround</span></span> 

<span data-ttu-id="b7014-126">次の NuGet アクションのいずれかを実行します。</span><span class="sxs-lookup"><span data-stu-id="b7014-126">Perform any one of the following NuGet actions:</span></span> 
* <span data-ttu-id="b7014-127">パッケージ マネージャー UI を開く - `References` を右クリックし、`Manage NuGet Packages...` を選択する</span><span class="sxs-lookup"><span data-stu-id="b7014-127">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span> 
* <span data-ttu-id="b7014-128">パッケージ マネージャー コンソールを開く - `Tools > NuGet Package Manager` から、`Package Manager Console` を選択する</span><span class="sxs-lookup"><span data-stu-id="b7014-128">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span> 
* <span data-ttu-id="b7014-129">NuGet 復元を実行する - ソリューション エクスプローラーのソリューション ノードを右クリックし、`Restore NuGet Packages` を選択する</span><span class="sxs-lookup"><span data-stu-id="b7014-129">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span> 
* <span data-ttu-id="b7014-130">NuGet 復元もトリガーするプロジェクトをビルドする</span><span class="sxs-lookup"><span data-stu-id="b7014-130">Build the project which also triggers NuGet restore</span></span> 

<span data-ttu-id="b7014-131">これで、移行オプションを表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="b7014-131">You should now be able to see the migration option.</span></span> <span data-ttu-id="b7014-132">このオプションは ASP.NET と C++ のプロジェクト タイプではサポートされておらず、表示されません。</span><span class="sxs-lookup"><span data-stu-id="b7014-132">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span> 

## <a name="migration-steps"></a><span data-ttu-id="b7014-133">移行の手順</span><span class="sxs-lookup"><span data-stu-id="b7014-133">Migration steps</span></span>

> [!Note]
> <span data-ttu-id="b7014-134">Visual Studio ができるようにするには、プロジェクトのバックアップを作成する移行を開始する前に[packages.config へのロールバック](#how-to-roll-back-to-packagesconfig)必要な場合。</span><span class="sxs-lookup"><span data-stu-id="b7014-134">Before migration begins, Visual Studio creates a backup of the project to allow you to [roll back to packages.config](#how-to-roll-back-to-packagesconfig) if necessary.</span></span>

1. <span data-ttu-id="b7014-135">使用してプロジェクトを含むソリューションを開く`packages.config`します。</span><span class="sxs-lookup"><span data-stu-id="b7014-135">Open a solution containing project using `packages.config`.</span></span>

1. <span data-ttu-id="b7014-136">**ソリューション エクスプ ローラー**を右クリックし、**参照**ノードまたは`packages.config`ファイルおよび選択**packages.config の PackageReference に移行しています.** .</span><span class="sxs-lookup"><span data-stu-id="b7014-136">In **Solution Explorer**, right-click on the **References** node or the `packages.config` file and select **Migrate packages.config to PackageReference...**.</span></span>

1. <span data-ttu-id="b7014-137">Migrator は、プロジェクトの NuGet パッケージ参照を分析し、分類にしようとしています**最上位レベルの依存関係**(直接インストールされている NuGet パッケージ) および**推移的依存関係**。(最上位のパッケージの依存関係としてインストールされたパッケージ)。</span><span class="sxs-lookup"><span data-stu-id="b7014-137">The migrator analyzes the project's NuGet package references and attempts to categorize them into **Top-level dependencies** (NuGet packages that you installed directly) and **Transitive dependencies** (packages that were installed as dependencies of top-level packages).</span></span>

   > [!Note]
   > <span data-ttu-id="b7014-138">PackageReference は推移的なパッケージの復元をサポートしているし、依存関係を動的に解決する推移的依存関係が明示的にインストールしない必要がある意味します。</span><span class="sxs-lookup"><span data-stu-id="b7014-138">PackageReference supports transitive package restore and resolves dependencies dynamically, meaning that transitive dependencies need not be installed explicitly.</span></span>

1. <span data-ttu-id="b7014-139">(省略可能)選択して、最上位レベルの依存関係として推移的依存関係として分類された NuGet パッケージを処理することができます、**トップレベル**パッケージのオプション。</span><span class="sxs-lookup"><span data-stu-id="b7014-139">(Optional) You may choose to treat a NuGet package classified as a transitive dependency as a top-level dependency by selecting the **Top-Level** option for the package.</span></span> <span data-ttu-id="b7014-140">このオプションは、推移的をフローしないアセットが含まれているパッケージは自動的に設定 (内、 `build`、 `buildCrossTargeting`、 `contentFiles`、または`analyzers`フォルダー) と開発の依存関係として指定されている (`developmentDependency = "true"`)。</span><span class="sxs-lookup"><span data-stu-id="b7014-140">This option is automatically set for packages containing assets that do not flow transitively (those in the `build`, `buildCrossTargeting`, `contentFiles`, or `analyzers` folders) and those marked as a development dependency (`developmentDependency = "true"`).</span></span>

1. <span data-ttu-id="b7014-141">いずれかを確認して[互換性の問題をパッケージ化](#package-compatibility-issues)します。</span><span class="sxs-lookup"><span data-stu-id="b7014-141">Review any [package compatibility issues](#package-compatibility-issues).</span></span>

1. <span data-ttu-id="b7014-142">選択**OK**移行を開始します。</span><span class="sxs-lookup"><span data-stu-id="b7014-142">Select **OK** to begin the migration.</span></span>

1. <span data-ttu-id="b7014-143">移行の最後に、Visual Studio は、バックアップ、インストールされているパッケージ (最上位レベルの依存関係) の一覧、推移的依存関係として参照されるパッケージの一覧およびの初めに特定の互換性の問題の一覧にパスを使用してレポートを提供します。移行します。</span><span class="sxs-lookup"><span data-stu-id="b7014-143">At the end of the migration, Visual Studio provides a report with a path to the backup, the list of installed packages (top-level dependencies), a list of packages referenced as transitive dependencies, and a list of compatibility issues identified at the start of migration.</span></span> <span data-ttu-id="b7014-144">レポートは、バックアップ フォルダーに保存されます。</span><span class="sxs-lookup"><span data-stu-id="b7014-144">The report is saved to the backup folder.</span></span>

1. <span data-ttu-id="b7014-145">ソリューションをビルドし、実行を検証します。</span><span class="sxs-lookup"><span data-stu-id="b7014-145">Validate that the solution builds and runs.</span></span> <span data-ttu-id="b7014-146">問題が発生した場合[GitHub で問題を報告](https://github.com/NuGet/Home/issues/)します。</span><span class="sxs-lookup"><span data-stu-id="b7014-146">If you encounter problems, [file an issue on GitHub](https://github.com/NuGet/Home/issues/).</span></span>

## <a name="how-to-roll-back-to-packagesconfig"></a><span data-ttu-id="b7014-147">Packages.config にロールバックする方法</span><span class="sxs-lookup"><span data-stu-id="b7014-147">How to roll back to packages.config</span></span>

1. <span data-ttu-id="b7014-148">移行されたプロジェクトを閉じます。</span><span class="sxs-lookup"><span data-stu-id="b7014-148">Close the migrated project.</span></span>

1. <span data-ttu-id="b7014-149">プロジェクト ファイルをコピーし、 `packages.config` 、バックアップから (通常`<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`)、プロジェクト フォルダーにします。</span><span class="sxs-lookup"><span data-stu-id="b7014-149">Copy the project file and `packages.config` from the backup (typically `<solution_root>\MigrationBackup\<unique_guid>\<project_name>\`) to the project folder.</span></span> <span data-ttu-id="b7014-150">プロジェクトのルート ディレクトリに存在する場合は、obj フォルダーを削除します。</span><span class="sxs-lookup"><span data-stu-id="b7014-150">Delete the obj folder if it exists in the project root directory.</span></span>

1. <span data-ttu-id="b7014-151">プロジェクトを開きます。</span><span class="sxs-lookup"><span data-stu-id="b7014-151">Open the project.</span></span>

1. <span data-ttu-id="b7014-152">使用してパッケージ マネージャー コンソールを開き、**ツール > NuGet パッケージ マネージャー > パッケージ マネージャー コンソール**メニュー コマンド。</span><span class="sxs-lookup"><span data-stu-id="b7014-152">Open the Package Manager Console using the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="b7014-153">コンソールで、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="b7014-153">Run the following command in the Console:</span></span>

   ```ps
   update-package -reinstall
   ```

## <a name="create-a-package-after-migration"></a><span data-ttu-id="b7014-154">移行後にパッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="b7014-154">Create a package after migration</span></span>

<span data-ttu-id="b7014-155">参照を追加することをお勧め、移行が完了すると、 [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget パッケージ化、および使用して[msbuild パック](../reference/msbuild-targets.md#pack-target)パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="b7014-155">Once the migration is complete, we recommend that you add a reference to the [nuget.build.tasks.pack](https://www.nuget.org/packages/nuget.build.tasks.pack) nuget package, and then use [msbuild pack](../reference/msbuild-targets.md#pack-target) to create the package.</span></span> <span data-ttu-id="b7014-156">一部のシナリオで使用できますが`dotnet.exe pack`の代わりに`msbuild pack`をお勧めしません。</span><span class="sxs-lookup"><span data-stu-id="b7014-156">Although in some scenarios you could use `dotnet.exe pack` instead of `msbuild pack`, it is not recommended.</span></span>

## <a name="package-compatibility-issues"></a><span data-ttu-id="b7014-157">パッケージの互換性の問題</span><span class="sxs-lookup"><span data-stu-id="b7014-157">Package compatibility issues</span></span>

<span data-ttu-id="b7014-158">Packages.config でサポートされていた一部の側面は、PackageReference のサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b7014-158">Some aspects that were supported in packages.config are not supported in PackageReference.</span></span> <span data-ttu-id="b7014-159">Migrator は、分析し、このような問題を検出します。</span><span class="sxs-lookup"><span data-stu-id="b7014-159">The migrator analyzes and detects such issues.</span></span> <span data-ttu-id="b7014-160">次の問題の 1 つ以上を持つ任意のパッケージは、移行後も正常動作しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b7014-160">Any package that has one or more of the following issues may not behave as expected after the migration.</span></span>

### <a name="installps1-scripts-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="b7014-161">移行後、パッケージがインストールされている場合、"install.ps1"スクリプトは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b7014-161">"install.ps1" scripts are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7014-162">**説明**</span><span class="sxs-lookup"><span data-stu-id="b7014-162">**Description**</span></span> | <span data-ttu-id="b7014-163">Packagereference の場合、インストールしたり、パッケージのアンインストール中に install.ps1 お uninstall.ps1 の PowerShell スクリプトは実行されません。</span><span class="sxs-lookup"><span data-stu-id="b7014-163">With PackageReference, install.ps1 and uninstall.ps1 PowerShell scripts are not executed while installing or uninstalling a package.</span></span> |
| <span data-ttu-id="b7014-164">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="b7014-164">**Potential impact**</span></span> | <span data-ttu-id="b7014-165">対象のプロジェクトでいくつかの動作を構成するこれらのスクリプトに依存するパッケージが正しく機能しない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b7014-165">Packages that depend on these scripts to configure some behavior in the destination project might not work as expected.</span></span> |

### <a name="content-assets-are-not-available-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="b7014-166">"content"資産は、移行後、パッケージがインストールされている場合は使用できません。</span><span class="sxs-lookup"><span data-stu-id="b7014-166">"content" assets are not available when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7014-167">**説明**</span><span class="sxs-lookup"><span data-stu-id="b7014-167">**Description**</span></span> | <span data-ttu-id="b7014-168">パッケージの資産`content`フォルダーは、PackageReference でサポートされていないは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b7014-168">Assets in a package's `content` folder are not supported with PackageReference and are ignored.</span></span> <span data-ttu-id="b7014-169">PackageReference のサポートが追加`contentFiles`より推移的なサポートと共有のコンテンツを用意します。</span><span class="sxs-lookup"><span data-stu-id="b7014-169">PackageReference adds support for `contentFiles` to have better transitive support and shared content.</span></span>  |
| <span data-ttu-id="b7014-170">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="b7014-170">**Potential impact**</span></span> | <span data-ttu-id="b7014-171">資産`content`はコピーされませんリファクタリングがこれらの資産の存在に依存するコード プロジェクトとプロジェクトに必要です。</span><span class="sxs-lookup"><span data-stu-id="b7014-171">Assets in `content` are not copied into the project and project code that depends on the presence of those assets requires refactoring.</span></span>  |

### <a name="xdt-transforms-are-not-applied-when-the-package-is-installed-after-the-upgrade"></a><span data-ttu-id="b7014-172">アップグレード後に、パッケージがインストールされている場合、XDT 変換は適用されません。</span><span class="sxs-lookup"><span data-stu-id="b7014-172">XDT transforms are not applied when the package is installed after the upgrade</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7014-173">**説明**</span><span class="sxs-lookup"><span data-stu-id="b7014-173">**Description**</span></span> | <span data-ttu-id="b7014-174">PackageReference では、XDT 変換はサポートされていないと`.xdt`のインストールや、パッケージをアンインストールする場合、ファイルは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b7014-174">XDT transforms are not supported with PackageReference and `.xdt` files are ignored when installing or uninstalling a package.</span></span>   |
| <span data-ttu-id="b7014-175">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="b7014-175">**Potential impact**</span></span> | <span data-ttu-id="b7014-176">XDT 変換はほとんどの場合、そのプロジェクトの XML ファイルに適用されません`web.config.install.xdt`と`web.config.uninstall.xdt`、つまり、プロジェクトの` web.config`ファイルは、パッケージをインストールまたはアンインストール時に更新されません。</span><span class="sxs-lookup"><span data-stu-id="b7014-176">XDT transforms are not applied to any project XML files, most commonly, `web.config.install.xdt` and `web.config.uninstall.xdt`, which means the project's` web.config` file is not updated when the package is installed or uninstalled.</span></span> |

### <a name="assemblies-in-the-lib-root-are-ignored-when-the-package-is-installed-after-the-migration"></a><span data-ttu-id="b7014-177">移行後、パッケージがインストールされているときに lib ルート内のアセンブリは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b7014-177">Assemblies in the lib root are ignored when the package is installed after the migration</span></span>

| | |
| --- | --- |
| <span data-ttu-id="b7014-178">**説明**</span><span class="sxs-lookup"><span data-stu-id="b7014-178">**Description**</span></span> | <span data-ttu-id="b7014-179">Packagereference の場合、アセンブリの表示のルートにある`lib`ターゲット フレームワークの特定サブ フォルダーがないフォルダーは無視されます。</span><span class="sxs-lookup"><span data-stu-id="b7014-179">With PackageReference, assemblies present at the root of `lib` folder without a target framework specific sub-folder are ignored.</span></span> <span data-ttu-id="b7014-180">NuGet では、プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブフォルダーを検索し、プロジェクトに一致するアセンブリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="b7014-180">NuGet looks for a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework and installs the matching assemblies into the project.</span></span> |
| <span data-ttu-id="b7014-181">**潜在的な影響**</span><span class="sxs-lookup"><span data-stu-id="b7014-181">**Potential impact**</span></span> | <span data-ttu-id="b7014-182">プロジェクトのターゲット フレームワークに対応するターゲット フレームワーク モニカー (TFM) に一致するサブフォルダーがないパッケージが、移行後に期待どおりに動作しないまたは移行中にインストールが失敗</span><span class="sxs-lookup"><span data-stu-id="b7014-182">Packages that do not have a sub-folder matching the target framework moniker (TFM) corresponding to the project’s target framework may not behave as expected after the transition or fail installation during the migration</span></span> |

## <a name="found-an-issue-report-it"></a><span data-ttu-id="b7014-183">問題が見つかりましたか。</span><span class="sxs-lookup"><span data-stu-id="b7014-183">Found an issue?</span></span> <span data-ttu-id="b7014-184">報告してください。</span><span class="sxs-lookup"><span data-stu-id="b7014-184">Report it!</span></span>

<span data-ttu-id="b7014-185">移行エクスペリエンスに問題が発生した場合のください[NuGet GitHub リポジトリで問題を報告](https://github.com/NuGet/Home/issues/)します。</span><span class="sxs-lookup"><span data-stu-id="b7014-185">If you run into a problem with the migration experience, please [file an issue on the NuGet GitHub repository](https://github.com/NuGet/Home/issues/).</span></span>
