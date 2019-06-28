---
title: インストールして、Visual Studio で NuGet パッケージの管理
description: Visual Studio で NuGet パッケージ マネージャー UI を使用して NuGet パッケージを操作するための手順です。
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426247"
---
# <a name="install-and-manage-packages-in-visual-studio"></a><span data-ttu-id="010a6-103">インストールして、Visual Studio でパッケージの管理</span><span class="sxs-lookup"><span data-stu-id="010a6-103">Install and manage packages in Visual Studio</span></span>

<span data-ttu-id="010a6-104">Windows 上の Visual Studio で NuGet パッケージ マネージャー UI を使用すると、簡単にインストール、アンインストール、およびプロジェクトとソリューションの NuGet パッケージを更新できます。</span><span class="sxs-lookup"><span data-stu-id="010a6-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="010a6-105">Visual studio for Mac のエクスペリエンスを参照してください。[を含む NuGet パッケージをプロジェクトに](/visualstudio/mac/nuget-walkthrough)します。</span><span class="sxs-lookup"><span data-stu-id="010a6-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="010a6-106">パッケージ マネージャー UI では、Visual Studio のコードに含まれません。</span><span class="sxs-lookup"><span data-stu-id="010a6-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="010a6-107">Visual Studio 2015 での NuGet パッケージ マネージャーは不足しているが、場合**ツール > 拡張機能と更新しています.** を検索し、 *NuGet パッケージ マネージャー*拡張機能。</span><span class="sxs-lookup"><span data-stu-id="010a6-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="010a6-108">Visual Studio の拡張機能インストーラーを使用する場合は、ダウンロード、拡張機能から直接[ https://dist.nuget.org/index.html](https://dist.nuget.org/index.html)します。</span><span class="sxs-lookup"><span data-stu-id="010a6-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="010a6-109">Visual Studio 2017 以降、NuGet、NuGet パッケージ マネージャーが自動的にインストールのいずれか。NET に関連するワークロード。</span><span class="sxs-lookup"><span data-stu-id="010a6-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="010a6-110">個別に選択してインストール、**個々 のコンポーネント > コード ツール > NuGet パッケージ マネージャー** Visual Studio インストーラーでオプションです。</span><span class="sxs-lookup"><span data-stu-id="010a6-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="010a6-111">検索して、パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="010a6-111">Finding and installing a package</span></span>

1. <span data-ttu-id="010a6-112">**ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**プロジェクトや選択**NuGet パッケージの管理.** .</span><span class="sxs-lookup"><span data-stu-id="010a6-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![NuGet パッケージのメニュー オプションを管理します。](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="010a6-114">**参照** タブには、現在選択されているソースからの人気度でパッケージが表示されます (を参照してください[パッケージ ソース](#package-sources))。</span><span class="sxs-lookup"><span data-stu-id="010a6-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="010a6-115">検索ボックスを使用して、左上の特定のパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="010a6-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="010a6-116">パッケージを実現する、その情報を表示するには、一覧から選択、**インストール**と共にバージョン選択ドロップダウン ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="010a6-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![NuGet パッケージのダイアログの参照 タブを管理します。](media/Search.png)

1. <span data-ttu-id="010a6-118">ドロップダウン リストから目的のバージョンを選択し、選択**インストール**します。</span><span class="sxs-lookup"><span data-stu-id="010a6-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="010a6-119">Visual Studio では、パッケージとその依存関係をプロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="010a6-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="010a6-120">ライセンス条項に同意を求められる場合があります。</span><span class="sxs-lookup"><span data-stu-id="010a6-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="010a6-121">インストールが完了したら、追加されたパッケージが表示されます、**インストール済み**タブ。パッケージが記載されても、**参照**のソリューション エクスプ ローラーでプロジェクトに参照できますを示すノード`using`ステートメント。</span><span class="sxs-lookup"><span data-stu-id="010a6-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![ソリューション エクスプ ローラー内の参照](media/References.png)

> [!Tip]
> <span data-ttu-id="010a6-123">プレリリース版を検索に含めるし、プレリリース版で使用できるように、バージョン ドロップダウンの選択、**プレリリースを含める**オプション。</span><span class="sxs-lookup"><span data-stu-id="010a6-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="010a6-124">パッケージをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="010a6-124">Uninstalling a package</span></span>

1. <span data-ttu-id="010a6-125">**ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**または目的のプロジェクトと選択**NuGet パッケージの管理.** .</span><span class="sxs-lookup"><span data-stu-id="010a6-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="010a6-126">選択、**インストール済み**タブ。</span><span class="sxs-lookup"><span data-stu-id="010a6-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="010a6-127">(必要な場合は、リストをフィルター処理する検索を使用) をアンインストールするパッケージを選択し、選択**アンインストール**します。</span><span class="sxs-lookup"><span data-stu-id="010a6-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![パッケージをアンインストールします。](media/UninstallPackage.png)

1. <span data-ttu-id="010a6-129">なお、**プレリリースを含める**と**パッケージ ソース**コントロールがある影響しないパッケージをアンインストールするときにします。</span><span class="sxs-lookup"><span data-stu-id="010a6-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="010a6-130">パッケージの更新</span><span class="sxs-lookup"><span data-stu-id="010a6-130">Updating a package</span></span>

1. <span data-ttu-id="010a6-131">**ソリューション エクスプ ローラー**、いずれかを右クリックして**参照**または目的のプロジェクトと選択**NuGet パッケージの管理.** .(Web サイト プロジェクトを右クリックし、 **Bin**フォルダー)。</span><span class="sxs-lookup"><span data-stu-id="010a6-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="010a6-132">選択、**更新**タブを選択したパッケージ ソースから使用可能な更新プログラムのあるパッケージを参照してください。</span><span class="sxs-lookup"><span data-stu-id="010a6-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="010a6-133">選択**プレリリースを含める**更新リストにプレリリース パッケージを含めます。</span><span class="sxs-lookup"><span data-stu-id="010a6-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="010a6-134">パッケージを更新し、右側のドロップダウン リストから目的のバージョンを選択し、選択選択**更新**します。</span><span class="sxs-lookup"><span data-stu-id="010a6-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![パッケージの更新](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="010a6-136">一部のパッケージ、 **Update**ボタンが無効になり、参照されている"暗黙的に、SDK によって"というメッセージが表示されます (または"AutoReferenced")。</span><span class="sxs-lookup"><span data-stu-id="010a6-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="010a6-137">このメッセージは、パッケージが大規模なフレームワークまたは SDK の一部であるとは別には更新されないことを示します。</span><span class="sxs-lookup"><span data-stu-id="010a6-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="010a6-138">(このようなパッケージが内部的に付いて`<IsImplicitlyDefined>True</IsImplicitlyDefined>`)。たとえば、 `Microsoft.NETCore.App` .NET Core SDK の一部であり、パッケージのバージョンでないアプリケーションで使用されるランタイム フレームワークのバージョンと同じです。</span><span class="sxs-lookup"><span data-stu-id="010a6-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="010a6-139">必要がある[、.NET Core のインストールを更新する](https://aka.ms/dotnet-download)を新しいバージョンの ASP.NET Core と .NET Core ランタイムを取得します。</span><span class="sxs-lookup"><span data-stu-id="010a6-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="010a6-140">[.NET Core メタパッケージとバージョン管理の詳細については、このドキュメントを参照してください](/dotnet/core/packages)します。</span><span class="sxs-lookup"><span data-stu-id="010a6-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="010a6-141">これは、次の一般的に使用されるパッケージに適用されます。</span><span class="sxs-lookup"><span data-stu-id="010a6-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="010a6-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="010a6-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="010a6-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="010a6-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="010a6-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="010a6-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="010a6-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="010a6-145">NETStandard.Library</span></span>

    ![参照または AutoReferenced として暗黙的にマークされているパッケージの例](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="010a6-147">最新バージョンに更新プログラムには、複数のパッケージをクリックし、一覧でそれを選択、**更新**リストの上ボタン。</span><span class="sxs-lookup"><span data-stu-id="010a6-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="010a6-148">個々 のパッケージを更新することも、**インストール済み**タブ。パッケージの詳細がここでは、バージョン セレクターを含める (対象に、**プレリリースを含める**オプション)、 **Update**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="010a6-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="010a6-149">ソリューションのパッケージを管理します。</span><span class="sxs-lookup"><span data-stu-id="010a6-149">Managing packages for the solution</span></span>

<span data-ttu-id="010a6-150">ソリューションのパッケージの管理は、複数のプロジェクトを同時に操作する便利な手段です。</span><span class="sxs-lookup"><span data-stu-id="010a6-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="010a6-151">選択、**ツール > NuGet パッケージ マネージャー > ソリューションの NuGet パッケージを管理しています.** メニュー コマンド、またはソリューションを右クリックし  **NuGet パッケージの管理.** :</span><span class="sxs-lookup"><span data-stu-id="010a6-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![ソリューションの NuGet パッケージを管理します。](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="010a6-153">ソリューションのパッケージを管理する場合、UI を使用して、操作によって影響を受けるプロジェクトを選択できます。</span><span class="sxs-lookup"><span data-stu-id="010a6-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![ソリューションのパッケージを管理するときに、プロジェクト セレクター](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="010a6-155">タブを統合します。</span><span class="sxs-lookup"><span data-stu-id="010a6-155">Consolidate tab</span></span>

<span data-ttu-id="010a6-156">開発者と同じソリューション内の別のプロジェクト間で同じ NuGet パッケージの異なるバージョンを使用することを不適切な通常見なします。</span><span class="sxs-lookup"><span data-stu-id="010a6-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="010a6-157">パッケージ マネージャー UI は、ソリューションのパッケージを管理することを選択すると、**統合**を簡単に確認できます個別のバージョン番号を持つパッケージがソリューション内の異なるプロジェクトで使用されているタブ。</span><span class="sxs-lookup"><span data-stu-id="010a6-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![[パッケージ マネージャー UI の統合] タブ](media/ConsolidateTab.png)

<span data-ttu-id="010a6-159">この例で、ClassLibrary1 プロジェクトで使用して EntityFramework 6.2.0、ConsoleApp1 で EntityFramework 6.1.0 を使用している一方です。</span><span class="sxs-lookup"><span data-stu-id="010a6-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="010a6-160">パッケージのバージョンを統合するには、次の操作を行います。</span><span class="sxs-lookup"><span data-stu-id="010a6-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="010a6-161">プロジェクトの一覧で更新するプロジェクトを選択します。</span><span class="sxs-lookup"><span data-stu-id="010a6-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="010a6-162">これらすべてのプロジェクトで使用するバージョンを選択、**バージョン**EntityFramework 6.2.0 などのコントロール。</span><span class="sxs-lookup"><span data-stu-id="010a6-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="010a6-163">選択、**インストール**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="010a6-163">Select the **Install** button.</span></span>

<span data-ttu-id="010a6-164">パッケージ マネージャーは、選択したすべてのプロジェクト、その後、パッケージに表示されなくに選択したパッケージのバージョンをインストール、**統合**タブ。</span><span class="sxs-lookup"><span data-stu-id="010a6-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="010a6-165">パッケージ ソース</span><span class="sxs-lookup"><span data-stu-id="010a6-165">Package sources</span></span>

<span data-ttu-id="010a6-166">Visual Studio のパッケージの取得元のソースを変更するには、ソース セレクターから 1 つを選択します。</span><span class="sxs-lookup"><span data-stu-id="010a6-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![パッケージ マネージャー UI でのパッケージ ソース セレクター](media/PackageSourceDropDown.png)

<span data-ttu-id="010a6-168">パッケージ ソースを管理するには。</span><span class="sxs-lookup"><span data-stu-id="010a6-168">To manage package sources:</span></span>

1. <span data-ttu-id="010a6-169">選択、**設定**パッケージ マネージャー UI のアイコンは、以下に示すまたはを使用して、**ツール > オプション**コマンドをスクロールして**NuGet パッケージ マネージャー**:</span><span class="sxs-lookup"><span data-stu-id="010a6-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![パッケージ マネージャー UI の [設定] アイコン](media/PackageSourceSettings.png)

1. <span data-ttu-id="010a6-171">選択、**パッケージ ソース**ノード。</span><span class="sxs-lookup"><span data-stu-id="010a6-171">Select the **Package Sources** node:</span></span>

    ![パッケージのソース オプション](media/options.png)

1. <span data-ttu-id="010a6-173">ソースを追加するには、次のように選択します。 **+** 、名前を編集、URL またはパスを入力、**ソース**制御、および選択**Update**します。</span><span class="sxs-lookup"><span data-stu-id="010a6-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="010a6-174">ソースは、セレクターのドロップダウン リストに表示されます。</span><span class="sxs-lookup"><span data-stu-id="010a6-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="010a6-175">パッケージ ソースを変更するには、選択しでの編集を行う、**名前**と**ソース**ボックス、および選択**Update**します。</span><span class="sxs-lookup"><span data-stu-id="010a6-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="010a6-176">パッケージ ソースを無効にするには、一覧内の名前の左側にあるボックスをオフにします。</span><span class="sxs-lookup"><span data-stu-id="010a6-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="010a6-177">パッケージ ソースを削除することを選択し、、 **X**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="010a6-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="010a6-178">使用し、下矢印ボタンは変わりませんパッケージ ソースの優先順位。</span><span class="sxs-lookup"><span data-stu-id="010a6-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="010a6-179">Visual Studio は、パッケージ ソースの順序を無視し、要求に応答する最初のソースからパッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="010a6-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="010a6-180">詳細については、次を参照してください。[パッケージの復元](../consume-packages/package-restore.md)します。</span><span class="sxs-lookup"><span data-stu-id="010a6-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="010a6-181">コンピューター レベルまたはユーザー レベルで表示する場合がありますパッケージ ソースを削除した後再表示され場合、`NuGet.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="010a6-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="010a6-182">参照してください[一般的な NuGet 構成](../consume-packages/configuring-nuget-behavior.md)これらのファイルの場所、ファイルを手動で編集するかを使用して、ソースを削除、 [nuget ソース コマンド](../tools/nuget-exe-CLI-reference.md)します。</span><span class="sxs-lookup"><span data-stu-id="010a6-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="010a6-183">パッケージ マネージャーのオプションを制御します。</span><span class="sxs-lookup"><span data-stu-id="010a6-183">Package manager Options control</span></span>

<span data-ttu-id="010a6-184">パッケージ マネージャー UI が、小規模なを表示、パッケージを選択すると、展開可能な**オプション**(ここで両方とも、折りたたみし、展開) バージョン セレクターで、次のコントロール。</span><span class="sxs-lookup"><span data-stu-id="010a6-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="010a6-185">一部のプロジェクトの型だけを**プレビュー ウィンドウの表示**オプションが提供されます。</span><span class="sxs-lookup"><span data-stu-id="010a6-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![パッケージ マネージャーのオプション](media/PackageManagerUIOptions.png)

<span data-ttu-id="010a6-187">次のセクションでは、これらのオプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="010a6-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="010a6-188">プレビュー ウィンドウを表示します。</span><span class="sxs-lookup"><span data-stu-id="010a6-188">Show preview window</span></span>

<span data-ttu-id="010a6-189">選択した場合、モーダル ウィンドウが表示されますが、選択したパッケージの依存関係パッケージをインストールする前に。</span><span class="sxs-lookup"><span data-stu-id="010a6-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![プレビュー ダイアログ ボックスの例](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="010a6-191">インストールと更新プログラムのオプション</span><span class="sxs-lookup"><span data-stu-id="010a6-191">Install and Update Options</span></span>

<span data-ttu-id="010a6-192">(使用できませんのすべてのプロジェクトの種類。)</span><span class="sxs-lookup"><span data-stu-id="010a6-192">(Not available for all project types.)</span></span>

<span data-ttu-id="010a6-193">**依存関係の動作**NuGet がインストールする依存パッケージのバージョンを決定する方法を構成します。</span><span class="sxs-lookup"><span data-stu-id="010a6-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="010a6-194">*依存関係を無視する*おり、インストールされているパッケージを通常それがすべての依存関係のインストールをスキップします。</span><span class="sxs-lookup"><span data-stu-id="010a6-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="010a6-195">*最も低い*[Default] では、プライマリの選択したパッケージの要件を満たす最低限のバージョン番号と共に、依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="010a6-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="010a6-196">*最上位の修正プログラム*でも、同じメジャーおよびマイナー バージョン番号が、パッチ番号の最も高いバージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="010a6-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="010a6-197">たとえば、バージョン 1.2.2 が指定されている場合、最も高いバージョン 1.2 で始まるがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="010a6-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="010a6-198">*最上位のマイナー*同じメジャー バージョン番号が最も高いマイナー番号と修正プログラム番号を使用のバージョンをインストールします。</span><span class="sxs-lookup"><span data-stu-id="010a6-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="010a6-199">バージョン 1.2.2 が指定されている場合、最上位のバージョン 1 で始まるはインストールします。</span><span class="sxs-lookup"><span data-stu-id="010a6-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="010a6-200">*最も高い*最高の使用可能なバージョンのパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="010a6-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="010a6-201">**競合のアクションをファイル**NuGet を使用して、プロジェクトまたはローカル コンピューターに既に存在するパッケージを処理する方法を指定します。</span><span class="sxs-lookup"><span data-stu-id="010a6-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="010a6-202">*プロンプト*NuGet 維持するか既存のパッケージを上書きするかどうかを確認するように指示します。</span><span class="sxs-lookup"><span data-stu-id="010a6-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="010a6-203">*すべて無視*NuGet 既存のパッケージの上書きをスキップするように指示します。</span><span class="sxs-lookup"><span data-stu-id="010a6-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="010a6-204">*すべて上書き*NuGet 既存のパッケージを上書きするように指示します。</span><span class="sxs-lookup"><span data-stu-id="010a6-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="010a6-205">アンインストール オプション</span><span class="sxs-lookup"><span data-stu-id="010a6-205">Uninstall Options</span></span>

<span data-ttu-id="010a6-206">(使用できませんのすべてのプロジェクトの種類。)</span><span class="sxs-lookup"><span data-stu-id="010a6-206">(Not available for all project types.)</span></span>

<span data-ttu-id="010a6-207">**依存関係を削除**: 選択した場合、プロジェクトの他の場所で参照していない場合、依存パッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="010a6-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="010a6-208">**強制アンインストールの依存関係がある場合でも**: 選択すると、引き続きプロジェクトで参照されている場合でも、パッケージをアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="010a6-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="010a6-209">これは通常と組み合わせて使用**依存関係を削除**パッケージをあらゆる要素を削除する依存関係がインストールされていること。</span><span class="sxs-lookup"><span data-stu-id="010a6-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="010a6-210">このオプションを使用するおそれがあります、ただし、プロジェクトに壊れた参照。</span><span class="sxs-lookup"><span data-stu-id="010a6-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="010a6-211">このような場合は、する必要があります[これら他のパッケージを再インストール](../consume-packages/reinstalling-and-updating-packages.md)します。</span><span class="sxs-lookup"><span data-stu-id="010a6-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
