---
title: "NuGet パッケージ マネージャーの UI リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 62f6962b-7b84-4452-ae0d-a9e1ef1fc6f0
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
description: "Visual Studio で NuGet パッケージ マネージャーの UI を使用して NuGet パッケージを操作するための手順です。"
keywords: "NuGet UI では、NuGet パッケージ マネージャー UI では、NuGet Visual studio で NuGet パッケージの管理、ユーザー インターフェイスの NuGet パッケージ マネージャー Visual Studio での管理"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88e987054f3c59a327f71b15330a99eb350449e5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="6ef54-104">NuGet パッケージ マネージャーの UI</span><span class="sxs-lookup"><span data-stu-id="6ef54-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="6ef54-105">Windows 上の Visual Studio で NuGet パッケージ マネージャー UI を使用すると、インストール、アンインストール、およびプロジェクトおよびソリューションの NuGet パッケージの更新を簡単にできます。</span><span class="sxs-lookup"><span data-stu-id="6ef54-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="6ef54-106">Mac のエクスペリエンスを Visual Studio で、次を参照してください。[などの NuGet パッケージ、プロジェクトの](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough)します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="6ef54-107">パッケージ マネージャーの UI は、Visual Studio のコードに含まれていません。</span><span class="sxs-lookup"><span data-stu-id="6ef54-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="6ef54-108">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="6ef54-108">In this topic:</span></span>

- <span data-ttu-id="6ef54-109">[検索とインストール パッケージ ([参照] タブ)](#finding-and-installing-a-package)</span><span class="sxs-lookup"><span data-stu-id="6ef54-109">[Finding and installing a package (Browse tab)](#finding-and-installing-a-package)</span></span>
- [<span data-ttu-id="6ef54-110">パッケージ (インストール済み タブ) をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="6ef54-111">[パッケージ (インストールおよび更新 タブ) の更新](#updating-a-package)(が含まれています、 [「SDK によって暗黙的に参照される」または"AutoReferenced"メッセージ](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="6ef54-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="6ef54-112">[ソリューションのパッケージを管理する](#managing-packages-for-the-solution)(同時に複数のプロジェクトの操作)。</span><span class="sxs-lookup"><span data-stu-id="6ef54-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="6ef54-113">パッケージ ソース</span><span class="sxs-lookup"><span data-stu-id="6ef54-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="6ef54-114">パッケージ マネージャーのオプションを制御します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="6ef54-115">Visual Studio 2015 内の NuGet パッケージ マネージャー、欠落している場合は確認**ツール > 拡張機能と更新しています.**を検索し、 *NuGet Package Manager*拡張機能です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="6ef54-116">Visual Studio での拡張機能インストーラーを使用することがない場合は、ダウンロードから直接、拡張機能[https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="6ef54-117">Visual Studio 2017 のいずれかと NuGet と NuGet パッケージ マネージャーが自動的にインストールします。NET に関連するワークロードです。</span><span class="sxs-lookup"><span data-stu-id="6ef54-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="6ef54-118">選択して individuall をインストール、**個々 のコンポーネント > コード ツール > の NuGet package manager** Visual Studio 2017 インストーラー オプション。</span><span class="sxs-lookup"><span data-stu-id="6ef54-118">Install it individuall by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="6ef54-119">検索して、パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-119">Finding and installing a package</span></span>

1. <span data-ttu-id="6ef54-120">**ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**またはプロジェクトと選択**NuGet パッケージを管理しています.**.</span><span class="sxs-lookup"><span data-stu-id="6ef54-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![NuGet パッケージのメニュー オプションを管理します。](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="6ef54-122">**参照** タブでは、現在選択されているソースから人気度によってパッケージが表示されます (を参照してください[ソースをパッケージ化](#package-sources))。</span><span class="sxs-lookup"><span data-stu-id="6ef54-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="6ef54-123">検索ボックスを使用して、左上の特定のパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="6ef54-124">パッケージ一覧から選択できるよう、情報を表示する、**インストール**バージョン選択ドロップダウン リストとボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![[管理] タブの NuGet パッケージ ダイアログの参照](media/Search.png)

1. <span data-ttu-id="6ef54-126">ドロップダウン リストから、必要なバージョンを選択し、選択**インストール**です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="6ef54-127">Visual Studio は、プロジェクトにパッケージとその依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="6ef54-128">ライセンス条項に同意するように求められます。</span><span class="sxs-lookup"><span data-stu-id="6ef54-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="6ef54-129">インストールが完了したらに追加されたパッケージが表示されます。、**インストール**タブです。パッケージが記載されても、**参照**のソリューション エクスプ ローラーで、プロジェクト内に参照できることを示すノード`using`ステートメントです。</span><span class="sxs-lookup"><span data-stu-id="6ef54-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![ソリューション エクスプ ローラー内の参照](media/References.png)

> [!Tip]
    > <span data-ttu-id="6ef54-131">プレリリース バージョンを検索に含めるし、プレリリース版で利用できるように、バージョン ドロップダウンの選択、**プレリリースを含める**オプション。</span><span class="sxs-lookup"><span data-stu-id="6ef54-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="6ef54-132">パッケージをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-132">Uninstalling a package</span></span>

1. <span data-ttu-id="6ef54-133">**ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**または目的のプロジェクトをクリックし、 **NuGet パッケージを管理しています.**.</span><span class="sxs-lookup"><span data-stu-id="6ef54-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="6ef54-134">選択、**インストール**タブです。</span><span class="sxs-lookup"><span data-stu-id="6ef54-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="6ef54-135">(必要な場合は、リストをフィルター処理する検索を使用) をアンインストールするパッケージを選択し、選択**アンインストール**です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![パッケージをアンインストールします。](media/UninstallPackage.png)

1. <span data-ttu-id="6ef54-137">注意してください、 **preprelease を含める**と**パッケージ ソース**コントロールがある影響しないパッケージをアンインストールするとします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-137">Note that the **Include preprelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="6ef54-138">パッケージの更新</span><span class="sxs-lookup"><span data-stu-id="6ef54-138">Updating a package</span></span>

1. <span data-ttu-id="6ef54-139">**ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**または目的のプロジェクトをクリックし、 **NuGet パッケージを管理しています.**.(Web サイト プロジェクトを右クリックし、 **Bin**フォルダーです)。</span><span class="sxs-lookup"><span data-stu-id="6ef54-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="6ef54-140">選択、**更新**タブを選択したパッケージ ソースから使用可能な更新プログラムのあるパッケージを参照してください。</span><span class="sxs-lookup"><span data-stu-id="6ef54-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="6ef54-141">選択**プレリリースを含める**プレリリースのパッケージの一覧に含める、更新します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="6ef54-142">パッケージを更新し、右側のドロップダウン リストから、必要なバージョンを選択して、選択を選択して**更新**です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![パッケージの更新](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="6ef54-144">一部のパッケージ、**更新**ボタンが無効になり、メッセージが参照されている"暗黙的に、SDK によって"というメッセージが表示されます (または"AutoReferenced") です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="6ef54-145">メッセージは、Microsoft.NETCore.App または Microsoft.NETStandard.Library など、パッケージが、大規模なフレームワークまたは SDK の一部であるとは別に更新してはならないことを示します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="6ef54-146">(このような packagee が付いている内部的に`<IsImplicitlyDefined>True</IsImplicitlyDefined>`)。パッケージを更新するが所属する SDK を更新します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-146">(Such packagee are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![参照または AutoReferenced として暗黙的にマークされているパッケージの例](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="6ef54-148">更新するには複数のパッケージを最新のバージョンでそれを選択リストと選択、**更新**一覧の上のボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="6ef54-149">個々 のパッケージを更新することも、**インストール**タブです。ここでは、パッケージの詳細がバージョン セレクターを含める (対象に、 **Include prerelease**オプション) と**更新**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="6ef54-150">ソリューションのパッケージを管理します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-150">Managing packages for the solution</span></span>

<span data-ttu-id="6ef54-151">ソリューションのパッケージの管理は、同時に複数のプロジェクトを操作する便利な手段です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="6ef54-152">選択、**ツール > NuGet Package Manager > ソリューションの NuGet パッケージを管理しています.**メニュー コマンド、またはソリューションを右クリックし  **NuGet パッケージを管理しています.**:</span><span class="sxs-lookup"><span data-stu-id="6ef54-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![ソリューションの NuGet パッケージを管理します。](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="6ef54-154">ソリューションのパッケージを管理する場合、UI 操作によって影響を受けるプロジェクトを選択できます。</span><span class="sxs-lookup"><span data-stu-id="6ef54-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![ソリューションのパッケージを管理するときに、プロジェクト セレクター](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="6ef54-156">タブを統合します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-156">Consolidate tab</span></span>

<span data-ttu-id="6ef54-157">開発者と同じソリューション内の別のプロジェクトにわたって、同じの NuGet パッケージの異なるバージョンを使用することを不適切な通常解釈します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="6ef54-158">ソリューションのパッケージを管理することを選択すると、パッケージ マネージャーの UI を提供する**Consolidate**を簡単にわかるソリューション内の別のプロジェクトで個別のバージョン番号を持つパッケージを使用する場所 タブ。</span><span class="sxs-lookup"><span data-stu-id="6ef54-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![[パッケージ マネージャー UI の統合] タブ](media/ConsolidateTab.png)

<span data-ttu-id="6ef54-160">この例では、ClassLibrary1 プロジェクトは EntityFramework を使用した 6.2.0、EntityFramework 6.2.0 ConsoleApp1 が使用されている一方です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.2.0.</span></span> <span data-ttu-id="6ef54-161">パッケージのバージョンを統合するには、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="6ef54-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="6ef54-162">プロジェクトの一覧で更新するプロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="6ef54-163">内のそれらのすべてのプロジェクトで使用するバージョンを選択して、**バージョン**EntityFramework 6.2.0 などのコントロールです。</span><span class="sxs-lookup"><span data-stu-id="6ef54-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="6ef54-164">選択、**インストール**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-164">Select the **Install** button.</span></span>

<span data-ttu-id="6ef54-165">パッケージ マネージャーでは、選択したパッケージのバージョンをインストールするまで、パッケージは表示されなくなりますで、選択したすべてのプロジェクトに、 **Consolidate**タブです。</span><span class="sxs-lookup"><span data-stu-id="6ef54-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="6ef54-166">パッケージ ソース</span><span class="sxs-lookup"><span data-stu-id="6ef54-166">Package sources</span></span>

<span data-ttu-id="6ef54-167">Visual Studio のパッケージの取得元のソースを変更するには、ソース セレクターから 1 つを選択します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![パッケージ マネージャー UI でパッケージ ソースの選択](media/PackageSourceDropDown.png)

<span data-ttu-id="6ef54-169">パッケージ ソースを管理します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-169">To manage package sources:</span></span>

1. <span data-ttu-id="6ef54-170">選択、**設定**パッケージ マネージャー UI のアイコンが以下に示すか、使用して、**ツール > オプション**コマンドをスクロールして**NuGet Package Manager**:</span><span class="sxs-lookup"><span data-stu-id="6ef54-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![パッケージ マネージャー UI の [設定] アイコン](media/PackageSourceSettings.png)

1. <span data-ttu-id="6ef54-172">選択、**パッケージ ソース**ノード。</span><span class="sxs-lookup"><span data-stu-id="6ef54-172">Select the **Package Sources** node:</span></span>

    ![パッケージ ソースのオプション](media/options.png)

1. <span data-ttu-id="6ef54-174">ソースを追加するには、次のように選択します。  **+** 、名前を編集、URL またはパスを入力、**ソース**制御、および選択**更新**です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="6ef54-175">ソースは、セレクターのドロップダウンに表示されます。</span><span class="sxs-lookup"><span data-stu-id="6ef54-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="6ef54-176">パッケージ ソースを変更するには、選択しでの編集を行う、**名前**と**ソース**ボックス、および選択**更新**です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="6ef54-177">パッケージ ソースを無効にするには、一覧内の名前の左側のボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="6ef54-178">削除するには、パッケージ ソースを選択し、、 **X**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="6ef54-179">上矢印を使用し、下向きの矢印ボタンをパッケージ ソースの優先順位を変更します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="6ef54-180">Visual Studio は、プロジェクトのパッケージを復元するときに、優先順位の順序でこれらのソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="6ef54-181">詳細については、次を参照してください。[パッケージの復元](../Consume-Packages/Package-Restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-181">For more information, see [Package restore](../Consume-Packages/Package-Restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="6ef54-182">場合は、パッケージ ソースでは、削除した後再表示され、コンピューター レベルまたはユーザー レベルで表示場合があります`NuGet.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="6ef54-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="6ef54-183">参照してください[構成 NuGet 動作](../Consume-Packages/Configuring-NuGet-Behavior.md)これらのファイルの場所を削除して、ソース ファイルを手動で編集するかを使用して、 [nuget コマンドをソース](../tools/nuget-exe-CLI-reference.md)です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-183">See [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="6ef54-184">パッケージ マネージャーのオプションを制御します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-184">Package manager Options control</span></span>

<span data-ttu-id="6ef54-185">パッケージを選択すると、パッケージ マネージャーの UI 表示の小さな展開可能な**オプション**コントロール (この図で折りたたまれているし、展開された両方) のバージョンのセレクターの下。</span><span class="sxs-lookup"><span data-stu-id="6ef54-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="6ef54-186">いくつかのプロジェクトの .NET Core とを使用するなどの種類を`project.json`のみ参照形式、**ショー プレビュー ウィンドウ**オプションが用意されてです。</span><span class="sxs-lookup"><span data-stu-id="6ef54-186">Note that for some project types, such as .NET Core and those using the `project.json` reference format, only the **Show preview window** option is provided.</span></span>

![パッケージ マネージャーのオプション](media/PackageManagerUIOptions.png)

<span data-ttu-id="6ef54-188">次のセクションでは、これらのオプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="6ef54-189">プレビュー ウィンドウを表示します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-189">Show preview window</span></span>

<span data-ttu-id="6ef54-190">選択した場合、モーダル ウィンドウが表示されますが、選択したパッケージの依存関係パッケージをインストールする前に。</span><span class="sxs-lookup"><span data-stu-id="6ef54-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![プレビュー ダイアログ ボックスの例](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="6ef54-192">インストールと更新プログラムのオプション</span><span class="sxs-lookup"><span data-stu-id="6ef54-192">Install and Update Options</span></span>

<span data-ttu-id="6ef54-193">(使用できませんのすべてのプロジェクトの種類)。</span><span class="sxs-lookup"><span data-stu-id="6ef54-193">(Not available for all project types.)</span></span>

<span data-ttu-id="6ef54-194">**依存関係の動作**NuGet がインストールする依存パッケージのバージョンを決定する方法を構成します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="6ef54-195">*依存関係を無視する*がインストールされているパッケージを通常破損の依存関係のインストールをスキップします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="6ef54-196">*最小*[既定値] は、プライマリの選択したパッケージの要件を満たしている最小バージョン番号を持つ依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="6ef54-197">*最上位の修正プログラム*同じメジャーおよびマイナー バージョン番号が最新の修正プログラム番号とバージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="6ef54-198">たとえば、バージョン 1.2.2 が指定されている場合、最高バージョン 1.2 で始まるがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="6ef54-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="6ef54-199">*最高のマイナー*バージョンが同じメジャー バージョン番号が、最高のマイナー番号と修正プログラム番号をインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="6ef54-200">1.2.2 のバージョンが指定されている場合、1 で始まる最高のバージョンがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="6ef54-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="6ef54-201">*最も高い*パッケージの利用可能な最高のバージョンがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="6ef54-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="6ef54-202">**競合のアクションをファイル**NuGet を使用して、プロジェクトまたはローカル コンピューターに既に存在するパッケージを処理する方法を指定します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="6ef54-203">*プロンプト*を NuGet に維持するか既存のパッケージを上書きするかどうかを確認するように指示します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="6ef54-204">*すべて無視*を NuGet に既存のパッケージの上書きをスキップするように指示します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="6ef54-205">*すべて上書きする*を NuGet に既存のパッケージを上書きするように指示します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="6ef54-206">アンインストール オプション</span><span class="sxs-lookup"><span data-stu-id="6ef54-206">Uninstall Options</span></span>

<span data-ttu-id="6ef54-207">(使用できませんのすべてのプロジェクトの種類)。</span><span class="sxs-lookup"><span data-stu-id="6ef54-207">(Not available for all project types.)</span></span>

<span data-ttu-id="6ef54-208">**依存関係を削除**: 選択した場合、プロジェクトの他の場所で参照していない場合、依存パッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="6ef54-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="6ef54-209">**強制アンインストールに依存している場合でも**: 選択した場合、プロジェクトにまだ参照されている場合でも、パッケージをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="6ef54-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="6ef54-210">これは通常と組み合わせて使用**依存関係を削除**パッケージとその内容を削除する依存関係がインストールされています。</span><span class="sxs-lookup"><span data-stu-id="6ef54-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="6ef54-211">このオプションを使用するおそれがあります、ただし、プロジェクトに壊れた参照。</span><span class="sxs-lookup"><span data-stu-id="6ef54-211">Using this option may, however, lead to a broken references in the project.</span></span> <span data-ttu-id="6ef54-212">このような場合にする必要があります[これら他のパッケージを再インストール](../consume-packages/reinstalling-and-updating-packages.md)です。</span><span class="sxs-lookup"><span data-stu-id="6ef54-212">In such cases you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
