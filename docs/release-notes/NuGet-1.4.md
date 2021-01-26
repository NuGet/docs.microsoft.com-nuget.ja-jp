---
title: NuGet 1.4 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.4 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e51083be308d97110be9fd67b68f6ba68ccd3df5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777145"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="ba7d3-103">NuGet 1.4 リリースノート</span><span class="sxs-lookup"><span data-stu-id="ba7d3-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="ba7d3-104">[NuGet 1.3 リリースノート](../release-notes/nuget-1.3.md)  | [NuGet 1.5 リリースノート](../release-notes/nuget-1.5.md)</span><span class="sxs-lookup"><span data-stu-id="ba7d3-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="ba7d3-105">NuGet 1.4 は、2011年6月17日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="ba7d3-106">特徴</span><span class="sxs-lookup"><span data-stu-id="ba7d3-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="ba7d3-107">Update-Package の機能強化</span><span class="sxs-lookup"><span data-stu-id="ba7d3-107">Update-Package improvements</span></span>
<span data-ttu-id="ba7d3-108">NuGet 1.4 では、Update-Package コマンドが大幅に改善され、ソリューション内の複数のプロジェクトで同じバージョンのパッケージを簡単に保持できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="ba7d3-109">たとえば、パッケージを最新バージョンにアップグレードする場合、そのパッケージがインストールされているすべてのプロジェクトを同じバージョンに更新することが非常に一般的です。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="ba7d3-110">`Update-Package`コマンドを使用すると、次の操作が簡単になります。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="ba7d3-111">1つのプロジェクト内のすべてのパッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="ba7d3-111">Update all packages in a single project</span></span>

```
Update-Package -Project MvcApplication1
```

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="ba7d3-112">すべてのプロジェクトのパッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="ba7d3-112">Update a package in all projects</span></span>

```
Update-Package PackageId
```

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="ba7d3-113">すべてのプロジェクトのすべてのパッケージを更新する</span><span class="sxs-lookup"><span data-stu-id="ba7d3-113">Update all packages in all projects</span></span>

```
Update-Package
```

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="ba7d3-114">すべてのパッケージに対して "安全な" 更新を実行する</span><span class="sxs-lookup"><span data-stu-id="ba7d3-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="ba7d3-115">フラグは、 `-Safe` メジャーバージョンとマイナーバージョンの同じコンポーネントを持つバージョンにのみアップグレードを制限します。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="ba7d3-116">たとえば、パッケージのバージョン1.0.0 がインストールされていて、バージョン1.0.1、1.0.2、および1.1 がフィードで使用できる場合、このフラグによって `-Safe` パッケージが1.0.2 に更新されます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="ba7d3-117">フラグを指定せず `-Safe` にアップグレードすると、パッケージが最新バージョン1.1 にアップグレードされます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

```
Update-Package -Safe
```

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="ba7d3-118">ソリューションレベルでのパッケージの管理</span><span class="sxs-lookup"><span data-stu-id="ba7d3-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="ba7d3-119">NuGet 1.4 より前では、複数のプロジェクトへのパッケージのインストールは、ダイアログを使用すると煩雑でした。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="ba7d3-120">プロジェクトごとに1回ダイアログを起動する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="ba7d3-121">NuGet 1.4 では、複数のプロジェクトで同時にパッケージをインストール/アンインストール/更新するためのサポートが追加されています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="ba7d3-122">を起動するには、ソリューションを右クリックし、[ **NuGet パッケージの管理** ] メニューオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![ソリューションレベルの NuGet パッケージの管理ダイアログ](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="ba7d3-124">ダイアログのタイトルバーには、プロジェクトの名前ではなく、ソリューションの名前が表示されていることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="ba7d3-125">パッケージ操作で、操作を適用するプロジェクトの一覧を含むチェックボックスの一覧が提供されるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![NuGet パッケージプロジェクト選択の管理](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="ba7d3-127">詳細については、 [ソリューションのパッケージの管理](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution)に関するトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="ba7d3-128">許可されているバージョンへのアップグレードを制限する</span><span class="sxs-lookup"><span data-stu-id="ba7d3-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="ba7d3-129">既定で `Update-Package` は、パッケージに対してコマンドを実行する (または、ダイアログを使用してパッケージを更新する) と、フィードの最新バージョンに更新されます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="ba7d3-130">すべてのパッケージを更新するための新しいサポートでは、パッケージを特定のバージョン範囲にロックすることが必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="ba7d3-131">たとえば、アプリケーションが3.0 以降ではなく、パッケージのバージョン 2. \* のみで動作することが事前にわかっている場合があります。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="ba7d3-132">パッケージが誤って3に更新されないようにするため、NuGet 1.4 では、新しい属性を使用してファイルを手動で編集することによって、パッケージをアップグレードできるバージョンの範囲を制限するためのサポートが追加さ `packages.config` `allowedVersions` れています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="ba7d3-133">たとえば、次の例では、 `SomePackage` パッケージをバージョン範囲 2.0-3.0 (排他) にロックする方法を示しています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="ba7d3-134">属性は、 `allowedVersions` [バージョン範囲形式](../concepts/package-versioning.md#version-ranges)を使用して値を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="ba7d3-135">1.4 では、特定のバージョン範囲へのパッケージのロックを手動で編集する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="ba7d3-136">NuGet 1.5 では、コマンドを使用して、この範囲を配置するためのサポートを追加する予定 `Install-Package` です。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="ba7d3-137">パッケージビジュアライザー</span><span class="sxs-lookup"><span data-stu-id="ba7d3-137">Package Visualizer</span></span>
<span data-ttu-id="ba7d3-138">[**ツール** ライブラリパッケージマネージャーパッケージビジュアライザー] メニューオプションを使用して起動された新しいパッケージビジュアライザーを使用すると、  ->    ->  ソリューション内のすべてのプロジェクトとそのパッケージの依存関係を簡単に視覚化できます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="ba7d3-139">_**重要な注意:** この機能は、Visual Studio の DGML サポートを利用します。視覚エフェクトの作成は、Visual Studio Ultimate でのみサポートされています。DGML 図の表示は Visual Studio Premium 以降でのみサポートされています。_</span><span class="sxs-lookup"><span data-stu-id="ba7d3-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![パッケージビジュアライザー](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="ba7d3-141">NuGet ダイアログの自動更新チェック</span><span class="sxs-lookup"><span data-stu-id="ba7d3-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="ba7d3-142">NuGet のバージョンによっては、 `.nuspec` 古いバージョンの nuget ダイアログでは認識されない、ファイルによって表される新機能が導入されています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="ba7d3-143">1つの例として、 [フレームワークアセンブリを指定](../release-notes/nuget-1.2.md#framework-assembly-refs)するための NuGet 1.4 の概要を示します。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="ba7d3-144">このため、最新バージョンの NuGet を使用して、最新の機能を利用してパッケージを使用できるようにすることが重要です。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="ba7d3-145">NuGet の更新をより見やすくするために、NuGet ダイアログには、新しいバージョンが利用可能になったときに強調表示するロジックが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="ba7d3-146">_**注**: 現在のセッションで [ **オンライン** ] タブが選択されている場合にのみチェックが行われます。_</span><span class="sxs-lookup"><span data-stu-id="ba7d3-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![新しいバージョンを使用できるようになった [NuGet パッケージの管理] ダイアログ](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="ba7d3-148">更新プログラムの自動チェックをオフにするには、[NuGet の設定] ダイアログボックスで、[ **更新プログラムの自動確認] チェック** ボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![NuGet の設定](./media/nuget-settings.png)

<span data-ttu-id="ba7d3-150">この機能は NuGet 1.3 で実際に追加されましたが、もちろん、NuGet 1.4 などの1.3 の更新が利用可能になるまでは表示されません。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="ba7d3-151">パッケージマネージャーダイアログの機能強化</span><span class="sxs-lookup"><span data-stu-id="ba7d3-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="ba7d3-152">**メニュー名が改善** されました: わかりやすくするために、ダイアログを起動するメニューオプションの名前を変更しました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="ba7d3-153">メニューオプションは **NuGet パッケージを管理** するようになりました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="ba7d3-154">[**詳細] ウィンドウに最新の更新日が表示** されます。 [**オンライン**] または [**更新**] タブが選択されている場合、[NuGet] ダイアログには、パッケージの [詳細] ウィンドウに最新の更新プログラムの日付が表示されます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="ba7d3-155">**表示されるタグの一覧**: [Nuget] ダイアログにタグが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="ba7d3-156">Powershell の機能強化</span><span class="sxs-lookup"><span data-stu-id="ba7d3-156">Powershell Improvements</span></span>
* <span data-ttu-id="ba7d3-157">**署名済み powershell スクリプト**: NuGet には、より制限の厳しい環境での使用を可能にする署名付きの powershell スクリプトが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="ba7d3-158">**サポート** の確認: パッケージマネージャーコンソールで、 `$host.ui.Prompt` コマンドとコマンドを使用したプロンプトがサポートされるようになりました `$host.ui.PromptForChoice` 。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="ba7d3-159">パッケージソース **名**: フラグを使用してパッケージソースを指定するときに、パッケージソースの名前を指定することがサポートされてい `-Source` ます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="ba7d3-160">nuget.exe コマンドラインの機能強化</span><span class="sxs-lookup"><span data-stu-id="ba7d3-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="ba7d3-161">**NuGet カスタムコマンド**: nuget.exe は、MEF を使用したカスタムコマンドを使用して拡張できます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="ba7d3-162">**シンボルパッケージを作成するためのワークフローの簡素化**: フラグは、 `-Symbols` 標準規則ベースのフォルダー構造に適用できます。これにより、フォルダー内にソースとファイルのみを含めることで、シンボルパッケージが作成され `.pdb` ます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="ba7d3-163">**複数のソースの指定**: コマンドは、 `NuGet install` セミコロンを区切り記号として使用するか、複数回指定することにより、複数のソースの指定をサポートします `-Source` 。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="ba7d3-164">**プロキシ認証のサポート**: nuget 1.4 では、認証を必要とするプロキシの背後で nuget を使用するときに、ユーザー資格情報の入力を求めるためのサポートが追加されます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="ba7d3-165">**更新** `-Self` に関する重大な変更のnuget.exe: フラグは、nuget.exe を更新するために必要になりました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="ba7d3-166">`nuget.exe Update` は、ファイルへのパスを取得 `packages.config` し、パッケージの更新を試みます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="ba7d3-167">この更新は、プロジェクトファイル内のコンテンツの更新、追加、削除を行わないという点で制限されています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="ba7d3-168">\* \* パッケージ内で Powershell スクリプトを実行します。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="ba7d3-169">nuget.exe を使用したパッケージのプッシュに対する NuGet サーバーのサポート</span><span class="sxs-lookup"><span data-stu-id="ba7d3-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="ba7d3-170">NuGet には、nuget パッケージを使用して [軽量の web ベースの nuget リポジトリ](../hosting-packages/nuget-server.md) をホストする簡単な方法が用意されてい `NuGet.Server` ます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="ba7d3-171">NuGet 1.4 では、ライトウェイトサーバーは nuget.exe を使用したパッケージのプッシュと削除をサポートします。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="ba7d3-172">最新バージョンのでは、 `NuGet.Server` という名前の新しいが追加され `appSetting` `apiKey` ます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="ba7d3-173">キーを省略した場合、または空白のままにした場合、フィードへのパッケージのプッシュは無効になります。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="ba7d3-174">ApiKey を値 (理想的には強力なパスワード) に設定すると、nuget.exe を使用してパッケージをプッシュできます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="ba7d3-175">Windows Phone Tools Mango Edition のサポート</span><span class="sxs-lookup"><span data-stu-id="ba7d3-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="ba7d3-176">Windows Phone Tools for Mango のリリース候補版で NuGet がサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="ba7d3-177">現時点では、Windows Phone ツールは Visual Studio 拡張機能マネージャーをサポートしていないため、Windows Phone ツール用の NuGet をインストールするには、VSIX を手動でダウンロードして実行する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="ba7d3-178">Windows Phone ツールの NuGet をアンインストールするには、次のコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

```
vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5
```

## <a name="bug-fixes"></a><span data-ttu-id="ba7d3-179">バグの修正</span><span class="sxs-lookup"><span data-stu-id="ba7d3-179">Bug Fixes</span></span>
<span data-ttu-id="ba7d3-180">NuGet 1.4 では、合計88個の作業項目が修正済みです。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="ba7d3-181">これらの71はバグとしてマークされています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="ba7d3-182">NuGet 1.4 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="ba7d3-183">バグ修正:</span><span class="sxs-lookup"><span data-stu-id="ba7d3-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="ba7d3-184">[問題 603](http://nuget.codeplex.com/workitem/603): 特定のパッケージソースを指定すると、異なるリポジトリ間のパッケージの依存関係が正しく解決されます。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="ba7d3-185">[問題 1036](http://nuget.codeplex.com/workitem/1036): `NuGet Pack SomeProject.csproj` ビルド後イベントへの追加で、無限ループが発生しなくなりました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="ba7d3-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` フラグは相対パスをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="ba7d3-187">NuGet 1.4 更新プログラム</span><span class="sxs-lookup"><span data-stu-id="ba7d3-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="ba7d3-188">NuGet 1.4 のリリース直後、修正が必要ないくつかの問題が見つかりました。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="ba7d3-189">この更新プログラムの1.4 への特定のバージョン番号は1.4.20615.9020 です。</span><span class="sxs-lookup"><span data-stu-id="ba7d3-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="ba7d3-190">バグの修正</span><span class="sxs-lookup"><span data-stu-id="ba7d3-190">Bug Fixes</span></span>
* <span data-ttu-id="ba7d3-191">[問題 1220](http://nuget.codeplex.com/workitem/1220): 複数の `install.ps1` / `uninstall.ps1` プロジェクトがある場合、すべてのプロジェクトで Update-Package が実行されない</span><span class="sxs-lookup"><span data-stu-id="ba7d3-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="ba7d3-192">[問題 1156](http://nuget.codeplex.com/workitem/1156): パッケージマネージャー consol が W2K3/XP でスタックしている (Powershell 2 がインストールされていない場合)</span><span class="sxs-lookup"><span data-stu-id="ba7d3-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
