---
title: NuGet 1.4 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.4 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f4d712f83ea108a82a1bc4910c2a721a8c24d51
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550632"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="583c7-103">NuGet 1.4 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="583c7-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="583c7-104">[NuGet 1.3 のリリース ノート](../release-notes/nuget-1.3.md) | [NuGet 1.5 のリリース ノート](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="583c7-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="583c7-105">NuGet 1.4 は、2011 年 6 月 17 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="583c7-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="583c7-106">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="583c7-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="583c7-107">更新プログラム パッケージの機能強化</span><span class="sxs-lookup"><span data-stu-id="583c7-107">Update-Package improvements</span></span>
<span data-ttu-id="583c7-108">NuGet 1.4 には、多数のバージョンが同じで、ソリューション内の複数のプロジェクトでパッケージを維持しやすく更新プログラム パッケージ コマンドに機能強化が導入されています。</span><span class="sxs-lookup"><span data-stu-id="583c7-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="583c7-109">たとえば、パッケージを最新バージョンをアップグレードする場合、すべてのプロジェクトを同じバージョンに更新するインストール パッケージにするのには非常に一般的なは。</span><span class="sxs-lookup"><span data-stu-id="583c7-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="583c7-110">`Update-Package`コマンド今すぐ簡単になります。</span><span class="sxs-lookup"><span data-stu-id="583c7-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="583c7-111">1 つのプロジェクトでパッケージをすべて更新します。</span><span class="sxs-lookup"><span data-stu-id="583c7-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="583c7-112">すべてのプロジェクトでパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="583c7-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="583c7-113">すべてのプロジェクトでパッケージをすべて更新します。</span><span class="sxs-lookup"><span data-stu-id="583c7-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="583c7-114">すべてのパッケージで「安全」更新を実行します。</span><span class="sxs-lookup"><span data-stu-id="583c7-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="583c7-115">`-Safe`フラグが同じメジャーおよびマイナー バージョン コンポーネントとの唯一のバージョンにアップグレードを制約します。</span><span class="sxs-lookup"><span data-stu-id="583c7-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="583c7-116">たとえば、バージョン 1.0.0 のパッケージがインストールされている場合、バージョン 1.0.1、1.0.2、および 1.1 が、フィードで利用可能な場合、 `-Safe` 1.0.2 フラグによって、パッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="583c7-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="583c7-117">なしのアップグレード、`-Safe`フラグは、パッケージが最新バージョン 1.1 にアップグレードします。</span><span class="sxs-lookup"><span data-stu-id="583c7-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="583c7-118">ソリューション レベルでパッケージを管理します。</span><span class="sxs-lookup"><span data-stu-id="583c7-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="583c7-119">NuGet 1.4 では、前に、複数のプロジェクトにパッケージをインストール ダイアログを使用して面倒でした。</span><span class="sxs-lookup"><span data-stu-id="583c7-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="583c7-120">プロジェクトごとに 1 回 ダイアログを起動することが必要です。</span><span class="sxs-lookup"><span data-stu-id="583c7-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="583c7-121">NuGet 1.4 では、同時に複数のプロジェクトのパッケージのインストール/アンインストール/更新のサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="583c7-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="583c7-122">単に起動、ソリューションを右クリックしを選択すると、 **NuGet パッケージの管理**メニュー オプション。</span><span class="sxs-lookup"><span data-stu-id="583c7-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![ソリューションの NuGet パッケージの管理レベル ダイアログ](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="583c7-124">ダイアログのタイトル バーで、ソリューションの名前が表示されることに注意してください、プロジェクトの名前ではありません。</span><span class="sxs-lookup"><span data-stu-id="583c7-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="583c7-125">パッケージの操作は、プロジェクトに適用する操作の一覧でチェック ボックスの一覧を提供します。</span><span class="sxs-lookup"><span data-stu-id="583c7-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![管理の NuGet パッケージのプロジェクトの選択](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="583c7-127">詳細については、上のトピックを参照してください。[ソリューションのパッケージを管理する](../tools/package-manager-ui.md#managing-packages-for-the-solution)します。</span><span class="sxs-lookup"><span data-stu-id="583c7-127">For more details, see the topic on [Managing Packages for the Solution](../tools/package-manager-ui.md#managing-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="583c7-128">許容バージョンにアップグレードの制約</span><span class="sxs-lookup"><span data-stu-id="583c7-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="583c7-129">既定で実行するときに、`Update-Package`パッケージ (またはダイアログを使用してパッケージを更新しています) で、コマンドは、フィードで最新バージョンに更新します。</span><span class="sxs-lookup"><span data-stu-id="583c7-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="583c7-130">すべてのパッケージを更新するための新しいサポート、特定のバージョン範囲にパッケージをロックする場合があります。</span><span class="sxs-lookup"><span data-stu-id="583c7-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="583c7-131">たとえば、ご存知かも事前に、アプリケーションは、パッケージ、3.0 ではありませんが、以降のバージョン 2. \* でのみ動作します。</span><span class="sxs-lookup"><span data-stu-id="583c7-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="583c7-132">NuGet 1.4 を誤って 3 に、パッケージの更新を回避するために手動で編集してパッケージをアップグレードできるバージョンの範囲を制限するサポートの追加、 `packages.config` 、新しいツールを使用して`allowedVersions`属性。</span><span class="sxs-lookup"><span data-stu-id="583c7-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="583c7-133">たとえば、次の例をロックする方法を示しています。、`SomePackage`パッケージ バージョンの範囲 (排他) の 2.0 ~ 3.0。</span><span class="sxs-lookup"><span data-stu-id="583c7-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="583c7-134">`allowedVersions`属性を使用して値を受け入れる、[バージョン範囲の形式](../reference/package-versioning.md#version-ranges-and-wildcards)します。</span><span class="sxs-lookup"><span data-stu-id="583c7-134">The `allowedVersions` attribute accepts values using the [version range format](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="583c7-135">なお、1.4 でパッケージを特定のバージョン範囲をロックする必要があります手動で編集です。</span><span class="sxs-lookup"><span data-stu-id="583c7-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="583c7-136">NuGet 1.5 ではこの範囲を使用して配置するためのサポートを追加する予定の`Install-Package`コマンド。</span><span class="sxs-lookup"><span data-stu-id="583c7-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="583c7-137">パッケージのビジュアライザー</span><span class="sxs-lookup"><span data-stu-id="583c7-137">Package Visualizer</span></span>
<span data-ttu-id="583c7-138">使用して起動される、新しいパッケージ ビジュアライザー、**ツール** -> **ライブラリ パッケージ マネージャー** -> **パッケージ ビジュアライザー**のメニュー オプションを使用します。すべてのプロジェクトおよびソリューション内でそのパッケージの依存関係を簡単に視覚化します。</span><span class="sxs-lookup"><span data-stu-id="583c7-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="583c7-139">_**重要な注意:** この機能では、Visual Studio の DGML サポートの活用。視覚エフェクトを作成するは、Visual Studio Ultimate でのみサポートされます。Visual Studio Premium または高では、DGML 図を表示することはサポートされてのみ。_</span><span class="sxs-lookup"><span data-stu-id="583c7-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![パッケージのビジュアライザー](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="583c7-141">NuGet ダイアログの自動更新のチェック</span><span class="sxs-lookup"><span data-stu-id="583c7-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="583c7-142">いくつかのバージョンの NuGet を使用して表される新しい機能が導入されて、 `.nuspec` NuGet ダイアログ ボックスの以前のバージョンによって認識されないファイル。</span><span class="sxs-lookup"><span data-stu-id="583c7-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="583c7-143">1 つの例は導入の NuGet 1.4 で[フレームワーク アセンブリを指定する](../release-notes/nuget-1.2.md#framework-assembly-refs)します。</span><span class="sxs-lookup"><span data-stu-id="583c7-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="583c7-144">このため、NuGet の最新バージョンを使用して、最新の機能を活用するパッケージを使用することを確認する重要ななります。</span><span class="sxs-lookup"><span data-stu-id="583c7-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="583c7-145">NuGet に更新プログラムをよりわかりやすいように、NuGet ダイアログには、新しいバージョンがあるときに強調表示するためのロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="583c7-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="583c7-146">_**注**: 場合にのみ、チェックが行われます、**オンライン** タブは、現在のセッションで選択されています。_</span><span class="sxs-lookup"><span data-stu-id="583c7-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![管理可能な新しいバージョンの NuGet パッケージの ダイアログ ボックス](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="583c7-148">更新プログラムの自動チェックをオフに、NuGet の設定 ダイアログに移動し、オフに**更新プログラムを自動的に確認**します。</span><span class="sxs-lookup"><span data-stu-id="583c7-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet の設定](./media/nuget-settings.png)

<span data-ttu-id="583c7-150">この機能は、NuGet の 1.3 で実際に追加されましたは表示されません、もちろん、1.3、1.4 の NuGet などの更新プログラムまで、利用できるようにしました。</span><span class="sxs-lookup"><span data-stu-id="583c7-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="583c7-151">パッケージ マネージャー ダイアログの改良</span><span class="sxs-lookup"><span data-stu-id="583c7-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="583c7-152">**メニュー名の改善**: わかりやすくするためのダイアログ ボックスを表示するメニュー オプションが変更されています。</span><span class="sxs-lookup"><span data-stu-id="583c7-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="583c7-153">メニュー オプションは現在**NuGet パッケージの管理**します。</span><span class="sxs-lookup"><span data-stu-id="583c7-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="583c7-154">**詳細ウィンドウには、最新の更新日が表示されます。**: NuGet ダイアログは、パッケージの詳細ウィンドウで、最新の更新プログラムの日付を表示しますときに、**オンライン**または**更新**タブが選択されます。</span><span class="sxs-lookup"><span data-stu-id="583c7-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="583c7-155">**表示されているタグの一覧**: Nuget ダイアログには、タグが表示されます。</span><span class="sxs-lookup"><span data-stu-id="583c7-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="583c7-156">Powershell の機能強化</span><span class="sxs-lookup"><span data-stu-id="583c7-156">Powershell Improvements</span></span>
* <span data-ttu-id="583c7-157">**PowerShell スクリプトを署名**: NuGet より制限の厳しい環境での使用状況を有効にすると、署名済みの Powershell スクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="583c7-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="583c7-158">**サポートを求める**: パッケージ マネージャー コンソール サポートを使用して入力を求める、`$host.ui.Prompt`と`$host.ui.PromptForChoice`コマンド。</span><span class="sxs-lookup"><span data-stu-id="583c7-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="583c7-159">**ソース名をパッケージ化**: を使用してパッケージ ソースを指定する場合はパッケージ ソースの名前を指定して、`-Source`フラグ。</span><span class="sxs-lookup"><span data-stu-id="583c7-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="583c7-160">nuget.exe コマンドラインの機能強化</span><span class="sxs-lookup"><span data-stu-id="583c7-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="583c7-161">**カスタムの NuGet コマンド**: nuget.exe は MEF を使用してカスタムのコマンドを使用して拡張します。</span><span class="sxs-lookup"><span data-stu-id="583c7-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="583c7-162">**単純なシンボル パッケージを作成するためのワークフロー**:`-Symbols`のみ、ソースを含めることで、シンボル パッケージを作成する通常の規則ベースのフォルダー構造に適用できるフラグと`.pdb`フォルダー内のファイル。</span><span class="sxs-lookup"><span data-stu-id="583c7-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="583c7-163">**複数のソースを指定する**:`NuGet install`コマンドかを指定して、区切り記号としてセミコロンを使用して複数のソースの指定をサポートしている`-Source`複数回です。</span><span class="sxs-lookup"><span data-stu-id="583c7-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="583c7-164">**プロキシ認証のサポート**: NuGet 1.4 は、認証が必要なプロキシの背後にある NuGet を使用する場合は、ユーザーの資格情報の入力を求めるサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="583c7-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="583c7-165">**nuget.exe 重大な変更を更新**:`-Self`フラグが、nuget.exe 自体を更新するために必要な。</span><span class="sxs-lookup"><span data-stu-id="583c7-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="583c7-166">`nuget.exe Update` パスでは、`packages.config`ファイルし、パッケージを更新しようとします。</span><span class="sxs-lookup"><span data-stu-id="583c7-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="583c7-167">これを行わないことで、この更新プログラムが制限されることに注意してください: * * 更新、追加、プロジェクト ファイルのコンテンツを削除します。</span><span class="sxs-lookup"><span data-stu-id="583c7-167">Note that this update is limited in that it will not: ** Update, add, remove content in the project file.</span></span>
<span data-ttu-id="583c7-168">* *、パッケージ内での Powershell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="583c7-168">** Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="583c7-169">Nuget.exe を使用してプッシュのパッケージの NuGet サーバーのサポート</span><span class="sxs-lookup"><span data-stu-id="583c7-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="583c7-170">NuGet にホストする簡単な方法が含まれています、[かつ軽量の web ベースの NuGet リポジトリ](../hosting-packages/nuget-server.md)を使用して、 `NuGet.Server` NuGet パッケージ。</span><span class="sxs-lookup"><span data-stu-id="583c7-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="583c7-171">NuGet 1.4 とは、軽量のサーバーは、プッシュと nuget.exe を使用してパッケージの削除をサポートします。</span><span class="sxs-lookup"><span data-stu-id="583c7-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="583c7-172">最新バージョンの`NuGet.Server`新しい`appSetting`、名前付き`apiKey`します。</span><span class="sxs-lookup"><span data-stu-id="583c7-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="583c7-173">キーを省略して空白のままにするか、フィードにパッケージをプッシュは無効になります。</span><span class="sxs-lookup"><span data-stu-id="583c7-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="583c7-174">ApiKey を値 (理想的には強力なパスワード) に設定すると、nuget.exe を使用したプッシュのパッケージが有効になります。</span><span class="sxs-lookup"><span data-stu-id="583c7-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="583c7-175">Windows Phone Tools Mango エディションのサポート</span><span class="sxs-lookup"><span data-stu-id="583c7-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="583c7-176">Windows Phone Mango ツールのリリース候補版では、NuGet がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="583c7-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="583c7-177">現時点では、Windows Phone ツールには、Windows Phone NuGet ツールをインストールするための Visual Studio 拡張機能マネージャーのサポートはありません、ダウンロードして、VSIX を手動で実行する必要があります。</span><span class="sxs-lookup"><span data-stu-id="583c7-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="583c7-178">Windows Phone NuGet ツールをアンインストールするには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="583c7-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="583c7-179">バグ修正</span><span class="sxs-lookup"><span data-stu-id="583c7-179">Bug Fixes</span></span>
<span data-ttu-id="583c7-180">NuGet 1.4 では、作業項目の固定が 88 の合計がありました。</span><span class="sxs-lookup"><span data-stu-id="583c7-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="583c7-181">これらの 71 はバグとしてマークされています。</span><span class="sxs-lookup"><span data-stu-id="583c7-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="583c7-182">作業の完全な一覧の項目で修正された NuGet 1.4、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="583c7-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="583c7-183">注目すべきバグ修正:</span><span class="sxs-lookup"><span data-stu-id="583c7-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="583c7-184">[問題 603](http://nuget.codeplex.com/workitem/603): 特定のパッケージ ソースを指定するときに異なるリポジトリ間でパッケージの依存関係が正しく解決します。</span><span class="sxs-lookup"><span data-stu-id="583c7-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="583c7-185">[問題 1036](http://nuget.codeplex.com/workitem/1036): 追加`NuGet Pack SomeProject.csproj`ビルド後イベントにできなくする無限ループが発生します。</span><span class="sxs-lookup"><span data-stu-id="583c7-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="583c7-186">[問題 961](http://nuget.codeplex.com/workitem/961):`-Source`フラグは、相対パスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="583c7-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="583c7-187">NuGet 1.4 の更新</span><span class="sxs-lookup"><span data-stu-id="583c7-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="583c7-188">NuGet 1.4 のリリースでは、直後に解決する重要な問題のいくつかがわかりました。</span><span class="sxs-lookup"><span data-stu-id="583c7-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="583c7-189">この更新プログラムの 1.4 の特定のバージョン番号は、1.4.20615.9020 です。</span><span class="sxs-lookup"><span data-stu-id="583c7-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="583c7-190">バグ修正</span><span class="sxs-lookup"><span data-stu-id="583c7-190">Bug Fixes</span></span>
* <span data-ttu-id="583c7-191">[問題 1220](http://nuget.codeplex.com/workitem/1220): 更新プログラム パッケージは実行されません`install.ps1` / `uninstall.ps1`で 1 つ以上のプロジェクトがある場合に、すべてのプロジェクト</span><span class="sxs-lookup"><span data-stu-id="583c7-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="583c7-192">[問題 1156](http://nuget.codeplex.com/workitem/1156): (Powershell 2 がインストールされていない) 場合に、パッケージ マネージャー コンソールが W2K3/xp スタック</span><span class="sxs-lookup"><span data-stu-id="583c7-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
