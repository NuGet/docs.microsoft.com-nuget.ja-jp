---
title: "NuGet 2.2.1 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 2.2.1 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.2.1 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c3e912dcabeb3a26c880b42560a3cec6f7bf2db9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="97ea0-104">NuGet 2.2.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="97ea0-104">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="97ea0-105">[NuGet 2.2 リリース ノート](../release-notes/nuget-2.2.md) | [NuGet 2.5 リリース ノート](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="97ea0-105">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="97ea0-106">NuGet 2.2.1 は、2013 年 2 月 15 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="97ea0-106">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="97ea0-107">VS 拡張機能のバージョン番号は、2.2.40116.9051 です。</span><span class="sxs-lookup"><span data-stu-id="97ea0-107">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="97ea0-108">ローカリゼーションの更新</span><span class="sxs-lookup"><span data-stu-id="97ea0-108">Localization Refresh</span></span>
<span data-ttu-id="97ea0-109">NuGet は Visual Studio 2012 の一部として提供されている、ときに、英語 + 13 の他の言語に完全にローカライズされます。</span><span class="sxs-lookup"><span data-stu-id="97ea0-109">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="97ea0-110">それ以降は、NuGet 2.1、2.2 が付属しているが、ローカリゼーションが更新されていません。</span><span class="sxs-lookup"><span data-stu-id="97ea0-110">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="97ea0-111">NuGet 2.2.1 リリースでは、ローカリゼーションを更新します。</span><span class="sxs-lookup"><span data-stu-id="97ea0-111">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="97ea0-112">NuGet の UI と PowerShell コンソールは、次の言語にローカライズされます。</span><span class="sxs-lookup"><span data-stu-id="97ea0-112">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="97ea0-113">中国語 (簡体字、中国)</span><span class="sxs-lookup"><span data-stu-id="97ea0-113">Chinese (Simplified)</span></span>
1. <span data-ttu-id="97ea0-114">では </span><span class="sxs-lookup"><span data-stu-id="97ea0-114">Chinese (Traditional)</span></span>
1. <span data-ttu-id="97ea0-115">チェコ語</span><span class="sxs-lookup"><span data-stu-id="97ea0-115">Czech</span></span>
1. <span data-ttu-id="97ea0-116">英語</span><span class="sxs-lookup"><span data-stu-id="97ea0-116">English</span></span>
1. <span data-ttu-id="97ea0-117">フランス語</span><span class="sxs-lookup"><span data-stu-id="97ea0-117">French</span></span>
1. <span data-ttu-id="97ea0-118">ドイツ語</span><span class="sxs-lookup"><span data-stu-id="97ea0-118">German</span></span>
1. <span data-ttu-id="97ea0-119">イタリア語</span><span class="sxs-lookup"><span data-stu-id="97ea0-119">Italian</span></span>
1. <span data-ttu-id="97ea0-120">日本語</span><span class="sxs-lookup"><span data-stu-id="97ea0-120">Japanese</span></span>
1. <span data-ttu-id="97ea0-121">韓国語</span><span class="sxs-lookup"><span data-stu-id="97ea0-121">Korean</span></span>
1. <span data-ttu-id="97ea0-122">ポーランド語</span><span class="sxs-lookup"><span data-stu-id="97ea0-122">Polish</span></span>
1. <span data-ttu-id="97ea0-123">ポルトガル語 (ブラジル)</span><span class="sxs-lookup"><span data-stu-id="97ea0-123">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="97ea0-124">ロシア語</span><span class="sxs-lookup"><span data-stu-id="97ea0-124">Russian</span></span>
1. <span data-ttu-id="97ea0-125">スペイン語</span><span class="sxs-lookup"><span data-stu-id="97ea0-125">Spanish</span></span>
1. <span data-ttu-id="97ea0-126">トルコ語</span><span class="sxs-lookup"><span data-stu-id="97ea0-126">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="97ea0-127">Visual Studio のテンプレートが複数のプレインストールされたパッケージ リポジトリをサポートします。</span><span class="sxs-lookup"><span data-stu-id="97ea0-127">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="97ea0-128">Visual Studio のテンプレートを作成する場合は、NuGet を使用できます[パッケージをプレインストール](../visual-studio-extensibility/visual-studio-templates.md)テンプレートの一部として。</span><span class="sxs-lookup"><span data-stu-id="97ea0-128">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="97ea0-129">この機能が制限をこれまでは、同じソースから入手するすべてのパッケージに必要なです。</span><span class="sxs-lookup"><span data-stu-id="97ea0-129">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="97ea0-130">ただし、NuGet 2.2.1 では、(テンプレートを VSIX や、レジストリで定義されているディスク上のフォルダー) 内の複数のリポジトリからインストールされているパッケージを設定できます。</span><span class="sxs-lookup"><span data-stu-id="97ea0-130">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="97ea0-131">この機能の主なシナリオは、カスタムの ASP.NET プロジェクト テンプレートです。</span><span class="sxs-lookup"><span data-stu-id="97ea0-131">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="97ea0-132">組み込みの ASP.NET テンプレートは、ローカル ディスクからのパッケージの抽出、プレインストールされたパッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="97ea0-132">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="97ea0-133">ASP.NET がインストールされている既存のパッケージを使用するカスタム ASP.NET プロジェクト テンプレートを作成するようになりましたが、テンプレートに追加の NuGet パッケージを追加できます。</span><span class="sxs-lookup"><span data-stu-id="97ea0-133">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="97ea0-134">バグ修正</span><span class="sxs-lookup"><span data-stu-id="97ea0-134">Bug Fixes</span></span>
<span data-ttu-id="97ea0-135">NuGet 2.2.1 には、対象となる、いくつかのバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="97ea0-135">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="97ea0-136">作業の一覧の項目で修正 NuGet 2.2.1、してください。 ビュー、[今回のリリースの NuGet Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)です。</span><span class="sxs-lookup"><span data-stu-id="97ea0-136">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="97ea0-137">既知の問題</span><span class="sxs-lookup"><span data-stu-id="97ea0-137">Known Issues</span></span>

<span data-ttu-id="97ea0-138">プレインストールされたパッケージのすべてのリポジトリが、同じ値を使用する必要があります ASP.NET プロジェクト テンプレートを拡張する場合、`isPreunzipped`属性。</span><span class="sxs-lookup"><span data-stu-id="97ea0-138">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
