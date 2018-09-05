---
title: NuGet 2.2.1 リリース ノート
description: NuGet 2.2.1 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550699"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="860e2-103">NuGet 2.2.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="860e2-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="860e2-104">[NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md) | [NuGet 2.5 リリース ノート](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="860e2-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="860e2-105">NuGet 2.2.1 は、2013 年 2 月 15 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="860e2-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="860e2-106">VS 拡張機能のバージョン番号は、2.2.40116.9051 です。</span><span class="sxs-lookup"><span data-stu-id="860e2-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="860e2-107">ローカリゼーションの更新</span><span class="sxs-lookup"><span data-stu-id="860e2-107">Localization Refresh</span></span>
<span data-ttu-id="860e2-108">NuGet が Visual Studio 2012 の一部として出荷されたときに、英語とその他の 13 か国語にローカライズが完全に。</span><span class="sxs-lookup"><span data-stu-id="860e2-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="860e2-109">その後、NuGet 2.1、2.2 の配布が始まりましたが、ローカリゼーションが更新されていません。</span><span class="sxs-lookup"><span data-stu-id="860e2-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="860e2-110">NuGet 2.2.1 リリースでは、ローカリゼーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="860e2-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="860e2-111">NuGet の UI と PowerShell コンソールは、次の言語にローカライズされます。</span><span class="sxs-lookup"><span data-stu-id="860e2-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="860e2-112">中国語 (簡体字、中国)</span><span class="sxs-lookup"><span data-stu-id="860e2-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="860e2-113">では [</span><span class="sxs-lookup"><span data-stu-id="860e2-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="860e2-114">チェコ語</span><span class="sxs-lookup"><span data-stu-id="860e2-114">Czech</span></span>
1. <span data-ttu-id="860e2-115">英語</span><span class="sxs-lookup"><span data-stu-id="860e2-115">English</span></span>
1. <span data-ttu-id="860e2-116">フランス語</span><span class="sxs-lookup"><span data-stu-id="860e2-116">French</span></span>
1. <span data-ttu-id="860e2-117">ドイツ語</span><span class="sxs-lookup"><span data-stu-id="860e2-117">German</span></span>
1. <span data-ttu-id="860e2-118">イタリア語</span><span class="sxs-lookup"><span data-stu-id="860e2-118">Italian</span></span>
1. <span data-ttu-id="860e2-119">日本語</span><span class="sxs-lookup"><span data-stu-id="860e2-119">Japanese</span></span>
1. <span data-ttu-id="860e2-120">韓国語</span><span class="sxs-lookup"><span data-stu-id="860e2-120">Korean</span></span>
1. <span data-ttu-id="860e2-121">ポーランド語</span><span class="sxs-lookup"><span data-stu-id="860e2-121">Polish</span></span>
1. <span data-ttu-id="860e2-122">ポルトガル語 (ブラジル)</span><span class="sxs-lookup"><span data-stu-id="860e2-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="860e2-123">ロシア語</span><span class="sxs-lookup"><span data-stu-id="860e2-123">Russian</span></span>
1. <span data-ttu-id="860e2-124">スペイン語</span><span class="sxs-lookup"><span data-stu-id="860e2-124">Spanish</span></span>
1. <span data-ttu-id="860e2-125">トルコ語</span><span class="sxs-lookup"><span data-stu-id="860e2-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="860e2-126">Visual Studio テンプレートは、複数のパッケージがプレインストールされているリポジトリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="860e2-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="860e2-127">Visual Studio テンプレートを作成する場合は、NuGet を使用できます[パッケージがプレインストール](../visual-studio-extensibility/visual-studio-templates.md)テンプレートの一部として。</span><span class="sxs-lookup"><span data-stu-id="860e2-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="860e2-128">この機能が制限をこれまで、同じソースからのものに必要であるすべてのパッケージ。</span><span class="sxs-lookup"><span data-stu-id="860e2-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="860e2-129">ただし、NuGet 2.2.1 では、(テンプレート、VSIX、またはレジストリで定義されているディスク上のフォルダー) 内の複数のリポジトリからインストールされているパッケージができます。</span><span class="sxs-lookup"><span data-stu-id="860e2-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="860e2-130">この機能の主なシナリオは、カスタムの ASP.NET プロジェクト テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="860e2-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="860e2-131">組み込みの ASP.NET テンプレートでは、ローカル ディスクからのパッケージを引き出して、プレインストールされているパッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="860e2-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="860e2-132">ASP.NET がインストールされている既存のパッケージを使用するカスタムの ASP.NET プロジェクト テンプレートを作成するようになりましたがテンプレートに追加の NuGet パッケージを追加できます。</span><span class="sxs-lookup"><span data-stu-id="860e2-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="860e2-133">バグ修正</span><span class="sxs-lookup"><span data-stu-id="860e2-133">Bug Fixes</span></span>
<span data-ttu-id="860e2-134">NuGet 2.2.1 では、対象となるいくつかのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="860e2-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="860e2-135">作業の一覧の項目で修正された NuGet 2.2.1 くださいビュー、[このリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)します。</span><span class="sxs-lookup"><span data-stu-id="860e2-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="860e2-136">既知の問題</span><span class="sxs-lookup"><span data-stu-id="860e2-136">Known Issues</span></span>

<span data-ttu-id="860e2-137">プレインストールされているパッケージのすべてのリポジトリが、同じ値を使用する必要があります ASP.NET プロジェクト テンプレートを拡張する場合、`isPreunzipped`属性。</span><span class="sxs-lookup"><span data-stu-id="860e2-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
