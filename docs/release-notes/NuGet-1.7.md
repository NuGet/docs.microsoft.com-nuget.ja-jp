---
title: NuGet 1.7 のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.7 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 07cd541ef215d2a1bacc45995a22dadb6dfeac6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551468"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="3d95b-103">NuGet 1.7 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="3d95b-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="3d95b-104">[NuGet 1.6 リリース ノート](../release-notes/nuget-1.6.md) | [NuGet 1.8 のリリース ノート](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="3d95b-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="3d95b-105">NuGet 1.7 は、2012 年 4 月 4 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="3d95b-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="3d95b-106">インストールの既知の問題</span><span class="sxs-lookup"><span data-stu-id="3d95b-106">Known Installation Issue</span></span>
<span data-ttu-id="3d95b-107">VS 2010 SP1 を実行している場合は、インストールされている以前のバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーが発生実行可能性があります。</span><span class="sxs-lookup"><span data-stu-id="3d95b-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="3d95b-108">回避策では、単に NuGet をアンインストールしてから、VS 拡張ギャラリーからインストールします。</span><span class="sxs-lookup"><span data-stu-id="3d95b-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="3d95b-109">詳細については、「[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3d95b-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="3d95b-110">注: Visual Studio ([アンインストール] ボタンは無効です) 拡張機能をアンインストールすることができず、しの場合必要があります「管理者として実行」を使用して Visual Studio を再起動するには</span><span class="sxs-lookup"><span data-stu-id="3d95b-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="3d95b-111">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="3d95b-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="3d95b-112">サポートのインストール後に readme.txt ファイルを開く</span><span class="sxs-lookup"><span data-stu-id="3d95b-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="3d95b-113">パッケージが含まれている場合、1.7 では新しい、`readme.txt`パッケージのインストールが完了した後は、NuGet パッケージのルートにあるファイルにこのファイルは開く自動的にします。</span><span class="sxs-lookup"><span data-stu-id="3d95b-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="3d95b-114">NuGet の管理の [パッケージ] ダイアログ ボックスのプレリリース パッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="3d95b-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="3d95b-115">NuGet パッケージの管理 ダイアログには、プレリリース パッケージを表示するオプションを提供するドロップダウン リストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="3d95b-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![プレリリース パッケージを表示](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="3d95b-117">パッケージ ファイルが見つからない場合は、パッケージの復元 ボタンを表示します。</span><span class="sxs-lookup"><span data-stu-id="3d95b-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="3d95b-118">パッケージ マネージャー コンソールを開くか Manager NuGet パッケージのダイアログ、NuGet は、現在のソリューションがパッケージの復元モードを有効なかどうかを確認し、すべてのパッケージ ファイルがない場合、`packages`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="3d95b-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="3d95b-119">これら 2 つの条件が満たされた場合、NuGet は通知して、便利な復元 ボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="3d95b-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="3d95b-120">このボタンをクリックすると、NuGet に不足しているすべてのパッケージの復元がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="3d95b-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![ダイアログ ボックスでパッケージの復元 ボタン](./media/packagerestore-dialog.png)

![コンソールでパッケージの復元 ボタン](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="3d95b-123">ソリューション レベルの packages.config ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="3d95b-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="3d95b-124">以前のバージョンの NuGet では、各プロジェクトには、`packages.config`ファイルを追跡する NuGet パッケージは、そのプロジェクトにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="3d95b-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="3d95b-125">ただし、なかったようなファイルをソリューション レベル パッケージの追跡ソリューション レベルで。</span><span class="sxs-lookup"><span data-stu-id="3d95b-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="3d95b-126">その結果、ソリューション レベル パッケージを復元する方法がありませんでした。</span><span class="sxs-lookup"><span data-stu-id="3d95b-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="3d95b-127">NuGet 1.7 でこの機能が実装されているようになりました。</span><span class="sxs-lookup"><span data-stu-id="3d95b-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="3d95b-128">ソリューション レベル`packages.config`ファイルが下に配置、`.nuget`ソリューションの下のフォルダーのルートし、のみのソリューション レベル パッケージを格納します。</span><span class="sxs-lookup"><span data-stu-id="3d95b-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="3d95b-129">新規パッケージのコマンドを削除します。</span><span class="sxs-lookup"><span data-stu-id="3d95b-129">Remove New-Package command</span></span>
<span data-ttu-id="3d95b-130">使用率が低いため、新規パッケージ コマンドが削除されました。</span><span class="sxs-lookup"><span data-stu-id="3d95b-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="3d95b-131">Nuget.exe または便利な NuGet パッケージ エクスプ ローラーを使用してパッケージを作成するには、開発者がお勧めします。</span><span class="sxs-lookup"><span data-stu-id="3d95b-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="3d95b-132">バグ修正</span><span class="sxs-lookup"><span data-stu-id="3d95b-132">Bug Fixes</span></span>
<span data-ttu-id="3d95b-133">NuGet 1.7 は、パッケージの復元ワークフローとネットワーク/ソース管理のシナリオに関して、多くのバグを修正しました。</span><span class="sxs-lookup"><span data-stu-id="3d95b-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="3d95b-134">作業の完全な一覧の項目で修正された NuGet 1.7、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="3d95b-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
