---
title: "NuGet 1.4 のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: e4856d0a-b408-4c60-ac51-f80ea06d9f79
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.4 のリリース ノートします。"
keywords: "NuGet 1.4 のリリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c4c27861c8697c75a06712b8ca6243b3b206cbb3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="50fd2-104">NuGet 1.4 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="50fd2-104">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="50fd2-105">[NuGet 1.3 リリース ノート](../release-notes/nuget-1.3.md) | [NuGet 1.5 のリリース ノート](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="50fd2-105">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="50fd2-106">NuGet 1.4 は、2011 年 6 月 17 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="50fd2-106">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="50fd2-107">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="50fd2-107">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="50fd2-108">更新プログラム パッケージの機能強化</span><span class="sxs-lookup"><span data-stu-id="50fd2-108">Update-Package improvements</span></span>
<span data-ttu-id="50fd2-109">NuGet 1.4 には、多数の更新プログラム パッケージ コマンドがソリューション内の複数のプロジェクトにわたって、同じバージョンにパッケージを維持するが容易に機能強化が導入されています。</span><span class="sxs-lookup"><span data-stu-id="50fd2-109">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="50fd2-110">たとえば、パッケージを最新バージョンにアップグレードする場合は、ごく一般的を同じバージョンに更新するインストール パッケージにすべてのプロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-110">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="50fd2-111">`Update-Package`コマンドようになりましたしやすきます。</span><span class="sxs-lookup"><span data-stu-id="50fd2-111">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="50fd2-112">1 つのプロジェクトのすべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-112">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="50fd2-113">すべてのプロジェクトでパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-113">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="50fd2-114">すべてのプロジェクト内のすべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-114">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="50fd2-115">すべてのパッケージに対して「安全な」の更新を実行します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-115">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="50fd2-116">`-Safe`フラグが同じメジャーおよびマイナー バージョン コンポーネントを含む唯一のバージョンにアップグレードを制限します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-116">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="50fd2-117">たとえば、パッケージの version 1.0.0 がインストールされているし、バージョン 1.0.1、1.0.2、および 1.1 がフィードで使用可能な場合、`-Safe`フラグによってパッケージが 1.0.2 に更新します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-117">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="50fd2-118">なくをアップグレードする、`-Safe`フラグは、最新のバージョン 1.1 に、パッケージをアップグレードするとします。</span><span class="sxs-lookup"><span data-stu-id="50fd2-118">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="50fd2-119">ソリューション レベルでのパッケージを管理します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-119">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="50fd2-120">NuGet 1.4 の前に、複数のプロジェクトにパッケージをインストールする、ダイアログを使用して複雑でした。</span><span class="sxs-lookup"><span data-stu-id="50fd2-120">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="50fd2-121">プロジェクトごとに 1 回 ダイアログを起動することが必要です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-121">It required launching the dialog once per project.</span></span>

<span data-ttu-id="50fd2-122">NuGet 1.4 は、同時に複数のプロジェクトでパッケージのインストール/アンインストール/更新のサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-122">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="50fd2-123">単を起動して、ソリューションを右クリックしを選択すると、 **NuGet パッケージの管理**メニュー オプション。</span><span class="sxs-lookup"><span data-stu-id="50fd2-123">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![ソリューションの NuGet パッケージの管理レベル ダイアログ](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="50fd2-125">ダイアログ ボックスのタイトル バーで、ソリューションの名前が表示されることに注意してください、プロジェクト名ではありません。</span><span class="sxs-lookup"><span data-stu-id="50fd2-125">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="50fd2-126">パッケージの操作は、プロジェクトに適用操作の一覧と対応するチェック ボックスの一覧を提供するようになりました。</span><span class="sxs-lookup"><span data-stu-id="50fd2-126">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![NuGet パッケージのプロジェクトの選択範囲を管理します。](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="50fd2-128">詳細については、のトピックを参照してください。[ソリューションのパッケージを管理する](../tools/package-manager-ui.md#managing-packages-for-the-solution)です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-128">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="50fd2-129">許容バージョンにアップグレードを制限します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-129">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="50fd2-130">既定を実行しているときに、`Update-Package`コマンドをパッケージ (またはダイアログを使用してパッケージを更新して)、フィード内の最新バージョンに更新されます。</span><span class="sxs-lookup"><span data-stu-id="50fd2-130">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="50fd2-131">すべてのパッケージを更新するための新しいサポート、特定のバージョンの範囲内にパッケージをロックする場合があります。</span><span class="sxs-lookup"><span data-stu-id="50fd2-131">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="50fd2-132">たとえば、可能性がありますがあらかじめわかって、アプリケーションが 3.0 ではありませんが、以降、パッケージのバージョン 2.* でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="50fd2-132">For example, you may know in advance that your application will only work with version 2.* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="50fd2-133">パッケージは、手動で編集にアップグレードできるバージョンの範囲を制限するサポートを追加する NuGet 1.4 を誤って 3 に、パッケージの更新を回避するために、`packages.config`新しいツールを使用して`allowedVersions`属性。</span><span class="sxs-lookup"><span data-stu-id="50fd2-133">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="50fd2-134">たとえば、次の例をロックする方法、`SomePackage`パッケージ バージョン 2.0、3.0 (排他) の範囲です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-134">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="50fd2-135">`allowedVersions`属性を使用して値を受け入れる、[バージョン範囲形式](../reference/package-versioning.md#version-ranges-and-wildcards)です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-135">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="50fd2-136">1.4 で特定のバージョンの範囲内にパッケージをロックする必要があります手動で編集に注意してください。</span><span class="sxs-lookup"><span data-stu-id="50fd2-136">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="50fd2-137">使用してこの範囲を配置するためのサポートを追加する NuGet 1.5 の予定、`Install-Package`コマンド。</span><span class="sxs-lookup"><span data-stu-id="50fd2-137">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="50fd2-138">パッケージのビジュアライザー</span><span class="sxs-lookup"><span data-stu-id="50fd2-138">Package Visualizer</span></span>
<span data-ttu-id="50fd2-139">新しいパッケージ ビジュアライザーから起動、**ツール** -> **ライブラリ パッケージ マネージャー** -> **パッケージ ビジュアライザー**メニュー オプションを有効にします。すべてのプロジェクトおよびソリューション内でそのパッケージの依存関係を簡単に視覚化できます。</span><span class="sxs-lookup"><span data-stu-id="50fd2-139">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="50fd2-140">_**重要なメモ:**この機能では、Visual Studio の DGML サポートの活用します。視覚エフェクトの作成は、Visual Studio Ultimate でのみサポートされます。DGML 図の表示は、Visual Studio Premium または高でのみサポートされます。_</span><span class="sxs-lookup"><span data-stu-id="50fd2-140">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![パッケージのビジュアライザー](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="50fd2-142">NuGet のダイアログ ボックスの自動更新チェック</span><span class="sxs-lookup"><span data-stu-id="50fd2-142">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="50fd2-143">一部のバージョンの NuGet 経由で表される新しい機能が導入されて、 `.nuspec` NuGet のダイアログ ボックスの以前のバージョンによって認識されないファイルです。</span><span class="sxs-lookup"><span data-stu-id="50fd2-143">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="50fd2-144">1 つの例は、の NuGet 1.4 の導入[フレームワーク アセンブリを指定する](../release-notes/nuget-1.2.md#framework-assembly-refs)です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-144">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="50fd2-145">このためには、NuGet の最新バージョンを使用して、最新の機能を活用するパッケージを使用することを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50fd2-145">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="50fd2-146">NuGet への更新プログラムを目立たせる、NuGet のダイアログには、新しいバージョンが利用可能なときに強調表示するためのロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="50fd2-146">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="50fd2-147">_**注**: 場合にのみ、チェックが行われます、**オンライン**現在のセッション タブが選択されています。_</span><span class="sxs-lookup"><span data-stu-id="50fd2-147">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![使用可能な新しいバージョンの NuGet パッケージ ダイアログを管理します。](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="50fd2-149">更新プログラムの自動チェックをオフに NuGet の [設定] ダイアログ ボックスに移動し、オフにして**更新プログラムを自動的に確認**です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-149">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet の設定](./media/nuget-settings.png)

<span data-ttu-id="50fd2-151">この機能は、NuGet 1.3 で実際に追加されましたは表示されません、もちろん、NuGet 1.4 など、1.3 を更新するまでに用意されていました。</span><span class="sxs-lookup"><span data-stu-id="50fd2-151">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="50fd2-152">パッケージ マネージャー ダイアログ ボックスの機能強化</span><span class="sxs-lookup"><span data-stu-id="50fd2-152">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="50fd2-153">**メニュー名向上**: わかりやすくするためのダイアログを起動するメニュー オプションが変更されました。</span><span class="sxs-lookup"><span data-stu-id="50fd2-153">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="50fd2-154">メニュー オプションは、今すぐ**NuGet パッケージの管理**です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-154">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="50fd2-155">**詳細ペインが最新の更新日を表示**: NuGet ダイアログは、詳細ウィンドウで、パッケージの最新の更新プログラムの日付を表示時に、**オンライン**または**更新**タブが選択されています。</span><span class="sxs-lookup"><span data-stu-id="50fd2-155">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="50fd2-156">**表示されているタグの一覧**: Nuget ダイアログには、タグが表示されます。</span><span class="sxs-lookup"><span data-stu-id="50fd2-156">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="50fd2-157">Powershell の機能強化</span><span class="sxs-lookup"><span data-stu-id="50fd2-157">Powershell Improvements</span></span>
* <span data-ttu-id="50fd2-158">**PowerShell スクリプトを署名**: NuGet にはより制限の厳しい環境で使用状況を有効にすると、署名済みの Powershell スクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="50fd2-158">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="50fd2-159">**サポートを求める**:「パッケージ マネージャー コンソールでは経由でメッセージを表示、`$host.ui.Prompt`と`$host.ui.PromptForChoice`コマンド。</span><span class="sxs-lookup"><span data-stu-id="50fd2-159">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="50fd2-160">**ソース名をパッケージ化**: を使用してパッケージ ソースを指定する場合はサポートされてパッケージ ソースの名前を指定して、`-Source`フラグ。</span><span class="sxs-lookup"><span data-stu-id="50fd2-160">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="50fd2-161">nuget.exe コマンドラインの機能強化</span><span class="sxs-lookup"><span data-stu-id="50fd2-161">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="50fd2-162">**カスタムの NuGet コマンド**: nuget.exe は MEF を使用してカスタムのコマンドを使用して拡張できます。</span><span class="sxs-lookup"><span data-stu-id="50fd2-162">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="50fd2-163">**単純なシンボル パッケージを作成するためのワークフロー**:`-Symbols`フラグのみ、ソースを含めることによってシンボル パッケージを作成する標準規約に基づくフォルダー構造に適用できますと`.pdb`フォルダー内のファイルです。</span><span class="sxs-lookup"><span data-stu-id="50fd2-163">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="50fd2-164">**複数のソースを指定する**:`NuGet install`コマンドでは、区切り記号としてセミコロンを使用を指定することによって複数のソースを指定することがサポートする`-Source`複数回です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-164">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="50fd2-165">**プロキシ認証がサポート**: NuGet 1.4 は、NuGet を使用して認証を必要とするプロキシの背後にあるときにユーザーの資格情報の入力を求めてのサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-165">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="50fd2-166">**nuget.exe 互換性に影響する変更の更新**:`-Self`フラグが、それ自体を更新する nuget.exe のために必要なです。</span><span class="sxs-lookup"><span data-stu-id="50fd2-166">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="50fd2-167">`nuget.exe Update`パスでは、`packages.config`ファイルし、パッケージの更新を試みます。</span><span class="sxs-lookup"><span data-stu-id="50fd2-167">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="50fd2-168">されませんが、この更新プログラムが制限されるに注意してください: * * 更新、追加、プロジェクト ファイルのコンテンツを削除します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-168">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="50fd2-169">* *、パッケージ内の Powershell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-169">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="50fd2-170">Nuget.exe を使用したプッシュのパッケージの NuGet サーバーのサポート</span><span class="sxs-lookup"><span data-stu-id="50fd2-170">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="50fd2-171">NuGet にホストを簡単な方法が含まれています、[かつ軽量の web ベースの NuGet リポジトリ](../hosting-packages/NuGet-Server.md)を介して、 `NuGet.Server` NuGet パッケージです。</span><span class="sxs-lookup"><span data-stu-id="50fd2-171">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/NuGet-Server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="50fd2-172">NuGet 1.4 では、軽量なサーバーは、プッシュおよび nuget.exe を使用してパッケージの削除をサポートします。</span><span class="sxs-lookup"><span data-stu-id="50fd2-172">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="50fd2-173">最新バージョン`NuGet.Server`新しい`appSetting`、名前付き`apiKey`します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-173">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="50fd2-174">キーを省略するか、空白のまま、フィードへのパッケージのプッシュが無効になります。</span><span class="sxs-lookup"><span data-stu-id="50fd2-174">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="50fd2-175">ApiKey を値 (理想的には強力なパスワード) に設定すると、nuget.exe を使用したプッシュのパッケージが有効になります。</span><span class="sxs-lookup"><span data-stu-id="50fd2-175">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="50fd2-176">Windows Phone ツール Mango Edition のサポート</span><span class="sxs-lookup"><span data-stu-id="50fd2-176">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="50fd2-177">NuGet は、Windows Phone 用のツール Mango リリース候補版ではサポートされています。</span><span class="sxs-lookup"><span data-stu-id="50fd2-177">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="50fd2-178">現時点では、Windows Phone ツールには、Windows Phone ツールの NuGet をインストールするための Visual Studio 拡張機能マネージャーのサポートはありません、ダウンロードして、VSIX を手動で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="50fd2-178">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="50fd2-179">Windows Phone NuGet ツールをアンインストールするには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-179">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="50fd2-180">バグ修正</span><span class="sxs-lookup"><span data-stu-id="50fd2-180">Bug Fixes</span></span>
<span data-ttu-id="50fd2-181">NuGet 1.4 は、作業項目の固定 88 の合計がありました。</span><span class="sxs-lookup"><span data-stu-id="50fd2-181">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="50fd2-182">これらの 71 はバグとしてマークされています。</span><span class="sxs-lookup"><span data-stu-id="50fd2-182">71 of those were marked as bugs.</span></span>

<span data-ttu-id="50fd2-183">作業の完全な一覧アイテムを固定 NuGet 1.4 にしてください。 ビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-183">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="50fd2-184">注目すべきバグ修正:</span><span class="sxs-lookup"><span data-stu-id="50fd2-184">Bug fixes worth noting:</span></span>

* <span data-ttu-id="50fd2-185">[問題 603](http://nuget.codeplex.com/workitem/603): 特定のパッケージ ソースを指定するときに、別のリポジトリ パッケージの依存関係が適切に解決します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-185">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="50fd2-186">[問題 1036](http://nuget.codeplex.com/workitem/1036): 追加`NuGet Pack SomeProject.csproj`ビルド後イベントに不要になったに無限ループが発生します。</span><span class="sxs-lookup"><span data-stu-id="50fd2-186">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="50fd2-187">[問題 961](http://nuget.codeplex.com/workitem/961):`-Source`フラグは、相対パスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="50fd2-187">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

# <a name="nuget-14-update"></a><span data-ttu-id="50fd2-188">NuGet 1.4 の更新</span><span class="sxs-lookup"><span data-stu-id="50fd2-188">NuGet 1.4 Update</span></span>
<span data-ttu-id="50fd2-189">NuGet 1.4 のリリースでは、すぐ後に、いくつかの修正する必要がある問題が見つかりました。</span><span class="sxs-lookup"><span data-stu-id="50fd2-189">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="50fd2-190">1.4 にこの更新プログラムの特定のバージョン番号は、1.4.20615.9020 です。</span><span class="sxs-lookup"><span data-stu-id="50fd2-190">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="50fd2-191">バグ修正</span><span class="sxs-lookup"><span data-stu-id="50fd2-191">Bug Fixes</span></span>
* <span data-ttu-id="50fd2-192">[問題 1220](http://nuget.codeplex.com/workitem/1220): 更新プログラム パッケージを実行しない`install.ps1` / `uninstall.ps1`で複数のプロジェクトがある場合に、すべてのプロジェクト</span><span class="sxs-lookup"><span data-stu-id="50fd2-192">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="50fd2-193">[問題 1156](http://nuget.codeplex.com/workitem/1156): (Powershell 2 がインストールされていない) 場合、パッケージ マネージャー コンソールが W2K3/XP にスタックしました。</span><span class="sxs-lookup"><span data-stu-id="50fd2-193">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
