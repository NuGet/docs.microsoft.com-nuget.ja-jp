---
title: "NuGet 1.7 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.7 リリース ノートです。"
keywords: "NuGet 1.7 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 7b16bea8c6bcc77f814dd32a43b895b5e656c95d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-17-release-notes"></a><span data-ttu-id="bb4cb-104">NuGet 1.7 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="bb4cb-104">NuGet 1.7 Release Notes</span></span>

<span data-ttu-id="bb4cb-105">[NuGet 1.6 リリース ノート](../release-notes/nuget-1.6.md) | [NuGet 1.8 リリース ノート](../release-notes/nuget-1.8.md)</span><span class="sxs-lookup"><span data-stu-id="bb4cb-105">[NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md) | [NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md)</span></span>

<span data-ttu-id="bb4cb-106">NuGet 1.7 は、2012 年 4 月 4 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-106">NuGet 1.7 was released on April 4, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="bb4cb-107">インストールの既知の問題</span><span class="sxs-lookup"><span data-stu-id="bb4cb-107">Known Installation Issue</span></span>
<span data-ttu-id="bb4cb-108">VS 2010 SP1 を実行している場合、インストールされている古いバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーに発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="bb4cb-109">回避策では、NuGet をシンプルにアンインストールし、VS 拡張機能ギャラリーからインストールします。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="bb4cb-110">詳細については、[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="bb4cb-111">注意: Visual Studio には、(削除 ボタンは無効になっている) 拡張機能をアンインストールすることを許可しません、可能性の高い場合"管理者として実行 を使用して Visual Studio を再起動するには</span><span class="sxs-lookup"><span data-stu-id="bb4cb-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="bb4cb-112">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="bb4cb-112">Features</span></span>

### <a name="support-opening-readmetxt-file-after-installation"></a><span data-ttu-id="bb4cb-113">サポートのインストール後に readme.txt ファイルを開く</span><span class="sxs-lookup"><span data-stu-id="bb4cb-113">Support opening readme.txt file after installation</span></span>
<span data-ttu-id="bb4cb-114">新機能、1.7、パッケージに含まれる場合、`readme.txt`パッケージのインストールが完了した後は、NuGet パッケージのルートにあるファイルにこのファイルは開く自動的にします。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-114">New in 1.7, if your package includes a `readme.txt` file at the root of the package, NuGet will automatically open this file after it's finished installing your package.</span></span>

### <a name="show-prerelease-packages-in-the-manage-nuget-packages-dialog"></a><span data-ttu-id="bb4cb-115">NuGet の管理の [パッケージ] ダイアログ ボックスのプレリリースのパッケージを表示します。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-115">Show prerelease packages in the Manage NuGet packages dialog</span></span>
<span data-ttu-id="bb4cb-116">[NuGet パッケージの管理] ダイアログには、プレリリースのパッケージを表示するオプションを提供するドロップダウン リストが含まれています。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-116">The Manage NuGet Packages dialog now includes a dropdown which provides option to show prerelease packages.</span></span>

![プレリリースのパッケージを表示](./media/prerelease-dropdown.png)

### <a name="show-package-restore-button-when-package-files-are-missing"></a><span data-ttu-id="bb4cb-118">パッケージ ファイルが見つからない場合は、パッケージの復元 ボタンを表示します。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-118">Show Package Restore button when package files are missing</span></span>
<span data-ttu-id="bb4cb-119">パッケージ マネージャー コンソールを開くか、マネージャーの NuGet パッケージ ダイアログ、NuGet の現在のソリューションが、パッケージの復元モードを有効なかどうかは確認と、すべてのパッケージ ファイルがない場合、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-119">When you open the Package Manager console or the Manager NuGet packages dialog, NuGet will check if the current solution has enabled the Package Restore mode and if any package files are missing from the `packages` folder.</span></span> <span data-ttu-id="bb4cb-120">これら 2 つの条件が満たされた場合 NuGet 通知が表示され、便利な [復元] ボタンを表示します。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-120">If these two conditions are met, NuGet will notify you and will show a convenient Restore button.</span></span> <span data-ttu-id="bb4cb-121">このボタンをクリックすると、不足しているすべてのパッケージを復元する NuGet がトリガーされます。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-121">Clicking this button will trigger NuGet to restore all the missing packages.</span></span>

![ダイアログでパッケージの復元 ボタン](./media/packagerestore-dialog.png)

![コンソールでパッケージの復元 ボタン](./media/packagerestore-console.png)

### <a name="add-solution-level-packagesconfig-file"></a><span data-ttu-id="bb4cb-124">ソリューション レベル packages.config ファイルを追加します。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-124">Add solution-level packages.config file</span></span>
<span data-ttu-id="bb4cb-125">各プロジェクトには NuGet の以前のバージョンで、`packages.config`ファイルを追跡する NuGet パッケージは、そのプロジェクトにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-125">In previous versions of NuGet, each project has a `packages.config` file which keeps track of what NuGet packages are installed in that project.</span></span> <span data-ttu-id="bb4cb-126">ただし、なかった同様のファイル レベルのソリューション パッケージを追跡するため、ソリューション レベルで。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-126">However, there was no similar file at the solution level to keep track of solution-level packages.</span></span> <span data-ttu-id="bb4cb-127">その結果、ソリューション レベルのパッケージを復元する方法がありませんでした。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-127">As a result, there was no way to restore solution-level packages.</span></span>
<span data-ttu-id="bb4cb-128">NuGet 1.7 では、この機能は実装されてようになりました。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-128">This feature is now implemented in NuGet 1.7.</span></span> <span data-ttu-id="bb4cb-129">ソリューション レベル`packages.config`ファイルが下に置かれて、`.nuget`ソリューションの下のフォルダーのルートし、ソリューション レベルのみのパッケージを格納します。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-129">The solution-level `packages.config` file is placed under the `.nuget` folder under solution root and will store only solution-level packages.</span></span>

### <a name="remove-new-package-command"></a><span data-ttu-id="bb4cb-130">新規パッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-130">Remove New-Package command</span></span>
<span data-ttu-id="bb4cb-131">使用頻度の低いため、新規パッケージ コマンドは削除されました。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-131">Due to low usage, the New-Package command has been removed.</span></span> <span data-ttu-id="bb4cb-132">開発者は nuget.exe または NuGet パッケージの便利なエクスプ ローラーを使用してパッケージを作成することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-132">Developers are recommended to use nuget.exe or the handy NuGet Package Explorer to create packages.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="bb4cb-133">バグ修正</span><span class="sxs-lookup"><span data-stu-id="bb4cb-133">Bug Fixes</span></span>
<span data-ttu-id="bb4cb-134">NuGet 1.7 は、パッケージの復元のワークフローとネットワーク/ソース制御シナリオを囲む多くのバグを修正しました。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-134">NuGet 1.7 has fixed many bugs around the Package Restore workflow and Network/Source Control scenarios.</span></span>

<span data-ttu-id="bb4cb-135">作業の完全な一覧の項目で修正 NuGet 1.7 くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="bb4cb-135">For a full list of work items fixed in NuGet 1.7, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.7&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
