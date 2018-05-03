---
title: NuGet 2.2.1 リリース ノート
description: NuGet 2.2.1 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="aba33-103">NuGet 2.2.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="aba33-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="aba33-104">[NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md) | [NuGet 2.5 リリース ノート](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="aba33-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="aba33-105">NuGet 2.2.1 は、2013 年 2 月 15 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="aba33-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="aba33-106">VS 拡張機能のバージョン番号は、2.2.40116.9051 です。</span><span class="sxs-lookup"><span data-stu-id="aba33-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="aba33-107">ローカリゼーションの更新</span><span class="sxs-lookup"><span data-stu-id="aba33-107">Localization Refresh</span></span>
<span data-ttu-id="aba33-108">NuGet は Visual Studio 2012 の一部として提供されている、ときに、英語 + 13 の他の言語に完全にローカライズされます。</span><span class="sxs-lookup"><span data-stu-id="aba33-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="aba33-109">それ以降は、NuGet 2.1、2.2 が付属しているが、ローカリゼーションが更新されていません。</span><span class="sxs-lookup"><span data-stu-id="aba33-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="aba33-110">NuGet 2.2.1 リリースでは、ローカリゼーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="aba33-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="aba33-111">NuGet の UI と PowerShell コンソールは、次の言語にローカライズされます。</span><span class="sxs-lookup"><span data-stu-id="aba33-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="aba33-112">中国語 (簡体字、中国)</span><span class="sxs-lookup"><span data-stu-id="aba33-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="aba33-113">では </span><span class="sxs-lookup"><span data-stu-id="aba33-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="aba33-114">チェコ語</span><span class="sxs-lookup"><span data-stu-id="aba33-114">Czech</span></span>
1. <span data-ttu-id="aba33-115">英語</span><span class="sxs-lookup"><span data-stu-id="aba33-115">English</span></span>
1. <span data-ttu-id="aba33-116">フランス語</span><span class="sxs-lookup"><span data-stu-id="aba33-116">French</span></span>
1. <span data-ttu-id="aba33-117">ドイツ語</span><span class="sxs-lookup"><span data-stu-id="aba33-117">German</span></span>
1. <span data-ttu-id="aba33-118">イタリア語</span><span class="sxs-lookup"><span data-stu-id="aba33-118">Italian</span></span>
1. <span data-ttu-id="aba33-119">日本語</span><span class="sxs-lookup"><span data-stu-id="aba33-119">Japanese</span></span>
1. <span data-ttu-id="aba33-120">韓国語</span><span class="sxs-lookup"><span data-stu-id="aba33-120">Korean</span></span>
1. <span data-ttu-id="aba33-121">ポーランド語</span><span class="sxs-lookup"><span data-stu-id="aba33-121">Polish</span></span>
1. <span data-ttu-id="aba33-122">ポルトガル語 (ブラジル)</span><span class="sxs-lookup"><span data-stu-id="aba33-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="aba33-123">ロシア語</span><span class="sxs-lookup"><span data-stu-id="aba33-123">Russian</span></span>
1. <span data-ttu-id="aba33-124">スペイン語</span><span class="sxs-lookup"><span data-stu-id="aba33-124">Spanish</span></span>
1. <span data-ttu-id="aba33-125">トルコ語</span><span class="sxs-lookup"><span data-stu-id="aba33-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="aba33-126">Visual Studio のテンプレートが複数のプレインストールされたパッケージ リポジトリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="aba33-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="aba33-127">Visual Studio のテンプレートを作成する場合は、NuGet を使用できます[パッケージをプレインストール](../visual-studio-extensibility/visual-studio-templates.md)テンプレートの一部として。</span><span class="sxs-lookup"><span data-stu-id="aba33-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="aba33-128">この機能が制限をこれまでは、同じソースから入手するすべてのパッケージに必要なです。</span><span class="sxs-lookup"><span data-stu-id="aba33-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="aba33-129">ただし、NuGet 2.2.1 では、(テンプレートを VSIX や、レジストリで定義されているディスク上のフォルダー) 内の複数のリポジトリからインストールされているパッケージを設定できます。</span><span class="sxs-lookup"><span data-stu-id="aba33-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="aba33-130">この機能の主なシナリオは、カスタムの ASP.NET プロジェクト テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="aba33-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="aba33-131">組み込みの ASP.NET テンプレートは、ローカル ディスクからのパッケージの抽出、プレインストールされたパッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="aba33-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="aba33-132">ASP.NET がインストールされている既存のパッケージを使用するカスタム ASP.NET プロジェクト テンプレートを作成するようになりましたが、テンプレートに追加の NuGet パッケージを追加できます。</span><span class="sxs-lookup"><span data-stu-id="aba33-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="aba33-133">バグ修正</span><span class="sxs-lookup"><span data-stu-id="aba33-133">Bug Fixes</span></span>
<span data-ttu-id="aba33-134">NuGet 2.2.1 には、対象となる、いくつかのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="aba33-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="aba33-135">作業の一覧の項目で修正 NuGet 2.2.1、してください。 ビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="aba33-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="aba33-136">既知の問題</span><span class="sxs-lookup"><span data-stu-id="aba33-136">Known Issues</span></span>

<span data-ttu-id="aba33-137">プレインストールされたパッケージのすべてのリポジトリが、同じ値を使用する必要があります ASP.NET プロジェクト テンプレートを拡張する場合、`isPreunzipped`属性。</span><span class="sxs-lookup"><span data-stu-id="aba33-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
