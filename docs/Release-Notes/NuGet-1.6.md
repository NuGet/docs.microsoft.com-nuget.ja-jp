---
title: "NuGet 1.6 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 1.6 リリース ノートです。"
keywords: "NuGet 1.6 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 114b03cede24dee520ace1d8aa920a648ad16af1
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="f43d7-104">NuGet 1.6 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="f43d7-104">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="f43d7-105">[NuGet 1.5 のリリース ノート](../release-notes/nuget-1.5.md) | [NuGet 1.7 リリース ノート](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="f43d7-105">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="f43d7-106">NuGet 1.6 は、2011 年 12 月 13 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="f43d7-106">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="f43d7-107">インストールの既知の問題</span><span class="sxs-lookup"><span data-stu-id="f43d7-107">Known Installation Issue</span></span>
<span data-ttu-id="f43d7-108">VS 2010 SP1 を実行している場合、インストールされている古いバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーに発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f43d7-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="f43d7-109">回避策では、NuGet をシンプルにアンインストールし、VS 拡張機能ギャラリーからインストールします。</span><span class="sxs-lookup"><span data-stu-id="f43d7-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="f43d7-110">詳細については、[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f43d7-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="f43d7-111">注意: Visual Studio には、(削除 ボタンは無効になっている) 拡張機能をアンインストールすることを許可しません、可能性の高い場合"管理者として実行 を使用して Visual Studio を再起動するには</span><span class="sxs-lookup"><span data-stu-id="f43d7-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="f43d7-112">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="f43d7-112">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="f43d7-113">セマンティック バージョニングとプレリリースのパッケージのサポート</span><span class="sxs-lookup"><span data-stu-id="f43d7-113">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="f43d7-114">NuGet 1.6 には、セマンティック バージョニング (SemVer) のサポートが導入されています。</span><span class="sxs-lookup"><span data-stu-id="f43d7-114">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="f43d7-115">SemVer を使用する方法の詳細については、読み取り、[バージョン管理のドキュメント](../create-packages/prerelease-packages.md)です。</span><span class="sxs-lookup"><span data-stu-id="f43d7-115">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="f43d7-116">パッケージ (パッケージの復元) をチェックインせず NuGet を使用します。</span><span class="sxs-lookup"><span data-stu-id="f43d7-116">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="f43d7-117">NuGet 1.6 では、どの NuGet でパッケージは、ソース管理に追加されませんが代わりには復元ビルド時に存在しない場合、ワークフローの最初のクラスのサポートできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="f43d7-117">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="f43d7-118">詳細については、読み取り、[をソース管理パッケージをコミットすることがなくを使用して NuGet](../consume-packages/packages-and-source-control.md)トピックです。</span><span class="sxs-lookup"><span data-stu-id="f43d7-118">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="f43d7-119">NuGet パッケージのインストール項目テンプレート</span><span class="sxs-lookup"><span data-stu-id="f43d7-119">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="f43d7-120">Visual Studio プロジェクト テンプレートにプレインストールされている NuGet パッケージをサポートする作業の構築、NuGet 1.6 はまた、Visual Studio 項目テンプレートのサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="f43d7-120">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="f43d7-121">項目テンプレートには、内のテンプレートが呼び出されたときにインストールされている NuGet パッケージを関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="f43d7-121">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="f43d7-122">NuGet パッケージをインストールするプロジェクト/項目テンプレートを変更する方法の詳細については、読み取り、 [Visual Studio のテンプレート内のパッケージ](../visual-studio-extensibility/visual-studio-templates.md)トピックです。</span><span class="sxs-lookup"><span data-stu-id="f43d7-122">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="f43d7-123">パッケージ ソースを無効にするためのサポート</span><span class="sxs-lookup"><span data-stu-id="f43d7-123">Support for disabling package sources</span></span>
<span data-ttu-id="f43d7-124">複数のパッケージ ソースを構成したら、NuGet はパッケージとその依存関係のインストール中にパッケージの 1 つずつになります。</span><span class="sxs-lookup"><span data-stu-id="f43d7-124">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="f43d7-125">何らかの理由により著しく遅くなる可能性が NuGet、ダウンされているパッケージのソース。</span><span class="sxs-lookup"><span data-stu-id="f43d7-125">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="f43d7-126">NuGet 1.6 する前にパッケージ ソースを削除する可能性がありますが、しに再び追加する場合の詳細を注意してください。</span><span class="sxs-lookup"><span data-stu-id="f43d7-126">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="f43d7-127">NuGet 1.6 では、無効にし、それを確保するためのパッケージ ソースをオフにするを使用できます。</span><span class="sxs-lookup"><span data-stu-id="f43d7-127">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![パッケージを無効にします。](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="f43d7-129">バグ修正</span><span class="sxs-lookup"><span data-stu-id="f43d7-129">Bug Fixes</span></span>
<span data-ttu-id="f43d7-130">NuGet 1.6 では、作業項目の固定 106 の合計がありました。</span><span class="sxs-lookup"><span data-stu-id="f43d7-130">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="f43d7-131">これらの 95 はバグとして分類され、機能は、そのうち 10 でした。</span><span class="sxs-lookup"><span data-stu-id="f43d7-131">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="f43d7-132">作業の完全な一覧の項目で修正 NuGet 1.6 くださいビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="f43d7-132">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
