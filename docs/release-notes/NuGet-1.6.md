---
title: NuGet 1.6 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 1.6 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549013"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="feda1-103">NuGet 1.6 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="feda1-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="feda1-104">[NuGet 1.5 のリリース ノート](../release-notes/nuget-1.5.md) | [NuGet 1.7 のリリース ノート](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="feda1-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="feda1-105">NuGet 1.6 は、2011 年 12 月 13 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="feda1-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="feda1-106">インストールの既知の問題</span><span class="sxs-lookup"><span data-stu-id="feda1-106">Known Installation Issue</span></span>
<span data-ttu-id="feda1-107">VS 2010 SP1 を実行している場合は、インストールされている以前のバージョンがある場合は、NuGet をアップグレードしようとしています。 インストール エラーが発生実行可能性があります。</span><span class="sxs-lookup"><span data-stu-id="feda1-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="feda1-108">回避策では、単に NuGet をアンインストールしてから、VS 拡張ギャラリーからインストールします。</span><span class="sxs-lookup"><span data-stu-id="feda1-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="feda1-109">詳細については、「[http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="feda1-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="feda1-110">注: Visual Studio ([アンインストール] ボタンは無効です) 拡張機能をアンインストールすることができず、しの場合必要があります「管理者として実行」を使用して Visual Studio を再起動するには</span><span class="sxs-lookup"><span data-stu-id="feda1-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="feda1-111">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="feda1-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="feda1-112">セマンティック バージョン管理とプレリリース パッケージのサポート</span><span class="sxs-lookup"><span data-stu-id="feda1-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="feda1-113">NuGet 1.6 では、セマンティック バージョン管理 (SemVer) のサポートについて説明します。</span><span class="sxs-lookup"><span data-stu-id="feda1-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="feda1-114">SemVer を使用する方法の詳細については、読み取り、[バージョン管理ドキュメント](../create-packages/prerelease-packages.md)します。</span><span class="sxs-lookup"><span data-stu-id="feda1-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="feda1-115">パッケージ (パッケージの復元) をチェックインせずに NuGet を使用します。</span><span class="sxs-lookup"><span data-stu-id="feda1-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="feda1-116">NuGet 1.6 では、どの nuget パッケージは、ソース管理に追加されませんが代わりには復元ビルド時に不足している場合、ワークフローのファースト クラス サポートできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="feda1-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="feda1-117">詳細については、読み取り、 [NuGet パッケージをソース管理にコミットせずを使用して](../consume-packages/packages-and-source-control.md)トピック。</span><span class="sxs-lookup"><span data-stu-id="feda1-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="feda1-118">NuGet パッケージをインストールする項目テンプレート</span><span class="sxs-lookup"><span data-stu-id="feda1-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="feda1-119">Visual Studio プロジェクト テンプレートにプレインストールされている NuGet パッケージをサポートする作業に基づき、NuGet 1.6 はまた、Visual Studio 項目テンプレートのサポートを追加します。</span><span class="sxs-lookup"><span data-stu-id="feda1-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="feda1-120">項目テンプレートには、内のテンプレートが呼び出されたときにインストールされている NuGet パッケージを関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="feda1-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="feda1-121">NuGet パッケージをインストールするプロジェクト/項目テンプレートを変更する方法の詳細については、読み取り、 [Visual Studio テンプレート パッケージ](../visual-studio-extensibility/visual-studio-templates.md)トピック。</span><span class="sxs-lookup"><span data-stu-id="feda1-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="feda1-122">パッケージ ソースを無効にするためのサポート</span><span class="sxs-lookup"><span data-stu-id="feda1-122">Support for disabling package sources</span></span>
<span data-ttu-id="feda1-123">複数のパッケージ ソースが構成されている場合、パッケージとその依存関係のインストール中に NuGet はパッケージごとに 1 つになります。</span><span class="sxs-lookup"><span data-stu-id="feda1-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="feda1-124">パッケージ ソースをダウンは何らかの理由は、NuGet に深刻な低速化できます。</span><span class="sxs-lookup"><span data-stu-id="feda1-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="feda1-125">NuGet 1.6 では、前に、パッケージ ソースを削除する可能性がありますをもう一度追加する場合の詳細を覚える必要がし。</span><span class="sxs-lookup"><span data-stu-id="feda1-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="feda1-126">NuGet 1.6 は、無効にし、それを確保するためのパッケージ ソースをオフにするを使用できます。</span><span class="sxs-lookup"><span data-stu-id="feda1-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![パッケージを無効にします。](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="feda1-128">バグ修正</span><span class="sxs-lookup"><span data-stu-id="feda1-128">Bug Fixes</span></span>
<span data-ttu-id="feda1-129">NuGet 1.6 では、作業項目の固定 106 の合計がありました。</span><span class="sxs-lookup"><span data-stu-id="feda1-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="feda1-130">バグとして分類されたこれらの 95 と機能は、そのうち 10 でした。</span><span class="sxs-lookup"><span data-stu-id="feda1-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="feda1-131">作業の完全な一覧の項目で修正された NuGet 1.6 では、くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="feda1-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
