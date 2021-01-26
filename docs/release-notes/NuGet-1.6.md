---
title: NuGet 1.6 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 1.6 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777012"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="a4d70-103">NuGet 1.6 リリースノート</span><span class="sxs-lookup"><span data-stu-id="a4d70-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="a4d70-104">[NuGet 1.5 リリースノート](../release-notes/nuget-1.5.md)  | [NuGet 1.7 リリースノート](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="a4d70-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="a4d70-105">NuGet 1.6 は、2011年12月13日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="a4d70-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="a4d70-106">インストールに関する既知の問題</span><span class="sxs-lookup"><span data-stu-id="a4d70-106">Known Installation Issue</span></span>
<span data-ttu-id="a4d70-107">VS 2010 SP1 を実行している場合は、以前のバージョンがインストールされている場合に NuGet をアップグレードしようとすると、インストールエラーが発生することがあります。</span><span class="sxs-lookup"><span data-stu-id="a4d70-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="a4d70-108">この回避策は、単純に NuGet をアンインストールし、VS 拡張機能ギャラリーからインストールすることです。</span><span class="sxs-lookup"><span data-stu-id="a4d70-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="a4d70-109">詳細については、「 <https://support.microsoft.com/kb/2581019> 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4d70-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="a4d70-110">注: Visual Studio で拡張機能をアンインストールできない場合 ([アンインストール] ボタンが無効になっている場合)、"管理者として実行" を使用して Visual Studio を再起動する必要が生じる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a4d70-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="a4d70-111">特徴</span><span class="sxs-lookup"><span data-stu-id="a4d70-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="a4d70-112">セマンティックバージョン管理とプレリリースパッケージのサポート</span><span class="sxs-lookup"><span data-stu-id="a4d70-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="a4d70-113">NuGet 1.6 では、セマンティックバージョン管理 (SemVer) のサポートが導入されています。</span><span class="sxs-lookup"><span data-stu-id="a4d70-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="a4d70-114">SemVer の使用方法の詳細については、 [バージョン管理に関するドキュメント](../create-packages/prerelease-packages.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4d70-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="a4d70-115">パッケージをチェックインせずに NuGet を使用する (パッケージの復元)</span><span class="sxs-lookup"><span data-stu-id="a4d70-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="a4d70-116">NuGet 1.6 では、NuGet パッケージがソース管理に追加されないワークフローに対して、最初のクラスがサポートされるようになりましたが、必要でない場合はビルド時に復元されます。</span><span class="sxs-lookup"><span data-stu-id="a4d70-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="a4d70-117">詳細については、「 [パッケージをソース管理にコミットせずに NuGet を使用](../consume-packages/packages-and-source-control.md) する」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4d70-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="a4d70-118">NuGet パッケージをインストールする項目テンプレート</span><span class="sxs-lookup"><span data-stu-id="a4d70-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="a4d70-119">Visual Studio プロジェクトテンプレートへのプレインストールされた NuGet パッケージをサポートする作業をビルドすると、NuGet 1.6 では Visual Studio 項目テンプレートのサポートも追加されます。</span><span class="sxs-lookup"><span data-stu-id="a4d70-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="a4d70-120">項目テンプレートには、テンプレートが呼び出されたときにインストールされる NuGet パッケージを関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="a4d70-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="a4d70-121">プロジェクト/項目テンプレートを変更して NuGet パッケージをインストールする方法の詳細については、「 [Visual Studio テンプレートのパッケージ](../visual-studio-extensibility/visual-studio-templates.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4d70-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="a4d70-122">パッケージソースの無効化のサポート</span><span class="sxs-lookup"><span data-stu-id="a4d70-122">Support for disabling package sources</span></span>
<span data-ttu-id="a4d70-123">複数のパッケージソースが構成されている場合、NuGet では、パッケージとその依存関係のインストール中にパッケージごとにパッケージが検索されます。</span><span class="sxs-lookup"><span data-stu-id="a4d70-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="a4d70-124">何らかの理由で停止しているパッケージソースがあると、NuGet の速度が著しく低下する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a4d70-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="a4d70-125">NuGet 1.6 より前では、パッケージソースを削除することもできましたが、その後、に再度追加する必要がある場合の詳細について覚えておく必要があります。</span><span class="sxs-lookup"><span data-stu-id="a4d70-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="a4d70-126">NuGet 1.6 では、パッケージソースをオフにして無効にすることができますが、そのままにしておいてください。</span><span class="sxs-lookup"><span data-stu-id="a4d70-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![パッケージの無効化](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="a4d70-128">バグの修正</span><span class="sxs-lookup"><span data-stu-id="a4d70-128">Bug Fixes</span></span>
<span data-ttu-id="a4d70-129">NuGet 1.6 では、合計106個の作業項目が修正済みです。</span><span class="sxs-lookup"><span data-stu-id="a4d70-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="a4d70-130">これらのうちの95はバグとして分類され、そのうちの10は機能でした。</span><span class="sxs-lookup"><span data-stu-id="a4d70-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="a4d70-131">NuGet 1.6 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4d70-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
