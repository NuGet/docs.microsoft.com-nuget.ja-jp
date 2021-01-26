---
title: NuGet 1.7 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.7 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 50eb326c5ada4f74685b07c0d1b0f84b14e547ac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777064"
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="6a087-103">NuGet 1.7 リリースノート</span><span class="sxs-lookup"><span data-stu-id="6a087-103">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="6a087-104">[NuGet 1.6 リリースノート](../release-notes/nuget-1.6.md)  | [NuGet 1.8 リリースノート](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="6a087-104">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="6a087-105">NuGet 1.7 は、2012年4月4日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="6a087-105">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="6a087-106">インストールに関する既知の問題</span><span class="sxs-lookup"><span data-stu-id="6a087-106">Known Installation Issue</span></span>
<span data-ttu-id="6a087-107">VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="6a087-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="6a087-108">この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。</span><span class="sxs-lookup"><span data-stu-id="6a087-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="6a087-109">詳細については、「 <https://support.microsoft.com/kb/2581019> 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6a087-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="6a087-110">注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6a087-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="6a087-111">特徴</span><span class="sxs-lookup"><span data-stu-id="6a087-111">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="6a087-112">インストール後に readme.txt ファイルを開くことをサポートする</span><span class="sxs-lookup"><span data-stu-id="6a087-112">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="6a087-113">1.7 の新機能では、パッケージのルートにファイルが含まれている場合 `readme.txt` 、NuGet はパッケージのインストールが完了した後、このファイルを自動的に開きます。</span><span class="sxs-lookup"><span data-stu-id="6a087-113">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="6a087-114">[NuGet パッケージの管理] ダイアログボックスでプレリリースパッケージを表示する</span><span class="sxs-lookup"><span data-stu-id="6a087-114">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="6a087-115">[NuGet パッケージの管理] ダイアログボックスに、プレリリースパッケージを表示するオプションを提供するドロップダウンが追加されました。</span><span class="sxs-lookup"><span data-stu-id="6a087-115">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![プレリリースパッケージの表示](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="6a087-117">パッケージファイルが見つからないときに [パッケージの復元] ボタンを表示する</span><span class="sxs-lookup"><span data-stu-id="6a087-117">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="6a087-118">パッケージマネージャーコンソールまたは [マネージャー NuGet パッケージ] ダイアログを開くと、現在のソリューションでパッケージ復元モードが有効になっているかどうか、およびフォルダーにパッケージファイルが見つからないかどうかが NuGet によって確認され `packages` ます。</span><span class="sxs-lookup"><span data-stu-id="6a087-118">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="6a087-119">これら2つの条件が満たされている場合は、NuGet によって通知され、便利な [復元] ボタンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="6a087-119">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="6a087-120">このボタンをクリックすると、NuGet がトリガーされ、不足しているすべてのパッケージが復元されます。</span><span class="sxs-lookup"><span data-stu-id="6a087-120">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![ダイアログの [パッケージの復元] ボタン](./media/packagerestore-dialog.png)

![コンソールの [パッケージの復元] ボタン](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="6a087-123">ソリューションレベルの packages.config ファイルの追加</span><span class="sxs-lookup"><span data-stu-id="6a087-123">Add solution-level packages.config file</span></span>
<span data-ttu-id="6a087-124">以前のバージョンの NuGet では、各プロジェクトには、 `packages.config` そのプロジェクトにインストールされている nuget パッケージを追跡するファイルがあります。</span><span class="sxs-lookup"><span data-stu-id="6a087-124">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="6a087-125">ただし、ソリューションレベルでは、ソリューションレベルのパッケージを追跡するための類似したファイルはありませんでした。</span><span class="sxs-lookup"><span data-stu-id="6a087-125">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="6a087-126">そのため、ソリューションレベルのパッケージを復元する方法はありませんでした。</span><span class="sxs-lookup"><span data-stu-id="6a087-126">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="6a087-127">この機能は現在、NuGet 1.7 で実装されています。</span><span class="sxs-lookup"><span data-stu-id="6a087-127">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="6a087-128">ソリューションレベルの `packages.config` ファイルは、ソリューションルートの下のフォルダーに配置され、 `.nuget` ソリューションレベルのパッケージのみを格納します。</span><span class="sxs-lookup"><span data-stu-id="6a087-128">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="6a087-129">New-Package コマンドの削除</span><span class="sxs-lookup"><span data-stu-id="6a087-129">Remove New-Package command</span></span>
<span data-ttu-id="6a087-130">使用率が低いため、New-Package コマンドは削除されました。</span><span class="sxs-lookup"><span data-stu-id="6a087-130">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="6a087-131">開発者は、nuget.exe または便利な NuGet パッケージエクスプローラーを使用してパッケージを作成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="6a087-131">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6a087-132">バグの修正</span><span class="sxs-lookup"><span data-stu-id="6a087-132">Bug Fixes</span></span>
<span data-ttu-id="6a087-133">NuGet 1.7 では、パッケージの復元ワークフローとネットワーク/ソース管理のシナリオに関する多くのバグが修正されています。</span><span class="sxs-lookup"><span data-stu-id="6a087-133">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="6a087-134">NuGet 1.7 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6a087-134">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
