---
title: NuGet 2.2.1 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.2.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776801"
---
# <a name="nuget-221-release-notes"></a><span data-ttu-id="3c121-103">NuGet 2.2.1 リリースノート</span><span class="sxs-lookup"><span data-stu-id="3c121-103">NuGet 2.2.1 Release Notes</span></span>

<span data-ttu-id="3c121-104">[NuGet 2.2 リリースノート](../release-notes/nuget-2.2.md)  | [NuGet 2.5 リリースノート](../release-notes/nuget-2.5.md)</span><span class="sxs-lookup"><span data-stu-id="3c121-104">[NuGet 2.2 Release Notes](../release-notes/nuget-2.2.md) | [NuGet 2.5 Release Notes](../release-notes/nuget-2.5.md)</span></span>

<span data-ttu-id="3c121-105">NuGet 2.2.1 は2013年2月15日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="3c121-105">NuGet 2.2.1 was released on February 15, 2013.</span></span>  <span data-ttu-id="3c121-106">VS 拡張機能のバージョン番号は2.2.40116.9051 です。</span><span class="sxs-lookup"><span data-stu-id="3c121-106">The VS Extension version number is 2.2.40116.9051.</span></span>

## <a name="localization-refresh"></a><span data-ttu-id="3c121-107">ローカリゼーションの更新</span><span class="sxs-lookup"><span data-stu-id="3c121-107">Localization Refresh</span></span>
<span data-ttu-id="3c121-108">NuGet が Visual Studio 2012 の一部として出荷された場合、英語 + 13 の他の言語に完全にローカライズされています。</span><span class="sxs-lookup"><span data-stu-id="3c121-108">When NuGet shipped as part of Visual Studio 2012, it was fully localized into English + 13 other languages.</span></span>  <span data-ttu-id="3c121-109">その後、NuGet 2.1 および2.2 は出荷されましたが、ローカライズは更新されていません。</span><span class="sxs-lookup"><span data-stu-id="3c121-109">Since then, NuGet 2.1 and 2.2 have shipped but the localization had not been refreshed.</span></span>  <span data-ttu-id="3c121-110">NuGet 2.2.1 リリースでは、ローカライズを更新しています。</span><span class="sxs-lookup"><span data-stu-id="3c121-110">The NuGet 2.2.1 release refreshes our localization.</span></span>

<span data-ttu-id="3c121-111">NuGet の UI と PowerShell コンソールは、次の言語にローカライズされています。</span><span class="sxs-lookup"><span data-stu-id="3c121-111">NuGet's UI and PowerShell Console are localized into the following languages:</span></span>

1. <span data-ttu-id="3c121-112">簡体中国語</span><span class="sxs-lookup"><span data-stu-id="3c121-112">Chinese (Simplified)</span></span>
1. <span data-ttu-id="3c121-113">繁体中国語</span><span class="sxs-lookup"><span data-stu-id="3c121-113">Chinese (Traditional)</span></span>
1. <span data-ttu-id="3c121-114">チェコ語</span><span class="sxs-lookup"><span data-stu-id="3c121-114">Czech</span></span>
1. <span data-ttu-id="3c121-115">英語</span><span class="sxs-lookup"><span data-stu-id="3c121-115">English</span></span>
1. <span data-ttu-id="3c121-116">フランス語</span><span class="sxs-lookup"><span data-stu-id="3c121-116">French</span></span>
1. <span data-ttu-id="3c121-117">ドイツ語</span><span class="sxs-lookup"><span data-stu-id="3c121-117">German</span></span>
1. <span data-ttu-id="3c121-118">イタリア語</span><span class="sxs-lookup"><span data-stu-id="3c121-118">Italian</span></span>
1. <span data-ttu-id="3c121-119">日本語</span><span class="sxs-lookup"><span data-stu-id="3c121-119">Japanese</span></span>
1. <span data-ttu-id="3c121-120">韓国語</span><span class="sxs-lookup"><span data-stu-id="3c121-120">Korean</span></span>
1. <span data-ttu-id="3c121-121">ポーランド語</span><span class="sxs-lookup"><span data-stu-id="3c121-121">Polish</span></span>
1. <span data-ttu-id="3c121-122">ポルトガル語 (ブラジル)</span><span class="sxs-lookup"><span data-stu-id="3c121-122">Portuguese (Brazil)</span></span>
1. <span data-ttu-id="3c121-123">ロシア語</span><span class="sxs-lookup"><span data-stu-id="3c121-123">Russian</span></span>
1. <span data-ttu-id="3c121-124">スペイン語</span><span class="sxs-lookup"><span data-stu-id="3c121-124">Spanish</span></span>
1. <span data-ttu-id="3c121-125">トルコ語</span><span class="sxs-lookup"><span data-stu-id="3c121-125">Turkish</span></span>

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a><span data-ttu-id="3c121-126">Visual Studio テンプレートでは、複数のプレインストール済みパッケージリポジトリがサポート</span><span class="sxs-lookup"><span data-stu-id="3c121-126">Visual Studio Templates Support Multiple Preinstalled Package Repositories</span></span>
<span data-ttu-id="3c121-127">Visual Studio テンプレートを作成する場合は、NuGet を使用して、テンプレートの一部として [パッケージをプレインストール](../visual-studio-extensibility/visual-studio-templates.md) できます。</span><span class="sxs-lookup"><span data-stu-id="3c121-127">If you produce Visual Studio templates, you can use NuGet to [preinstall packages](../visual-studio-extensibility/visual-studio-templates.md) as part of the template.</span></span>  <span data-ttu-id="3c121-128">これまで、この機能では、すべてのパッケージが同じソースから取得される必要があるという制限がありました。</span><span class="sxs-lookup"><span data-stu-id="3c121-128">Until now, this feature had a limitation that all of the packages needed to come from the same source.</span></span>  <span data-ttu-id="3c121-129">ただし、NuGet 2.2.1 を使用すると、複数のリポジトリ (テンプレート内、VSIX 内、またはレジストリで定義されているディスク上のフォルダー内) からパッケージをインストールできます。</span><span class="sxs-lookup"><span data-stu-id="3c121-129">With NuGet 2.2.1 though, you can have packages installed from multiple repositories (within the template, a VSIX, or a folder on disk defined in the registry).</span></span>

<span data-ttu-id="3c121-130">この機能の主なシナリオは、カスタム ASP.NET プロジェクトテンプレートです。</span><span class="sxs-lookup"><span data-stu-id="3c121-130">The main scenario for this feature is custom ASP.NET project templates.</span></span>  <span data-ttu-id="3c121-131">組み込みの ASP.NET テンプレートでは、プレインストールされたパッケージを使用して、ローカルディスクからパッケージをプルします。</span><span class="sxs-lookup"><span data-stu-id="3c121-131">The built-in ASP.NET templates use preinstalled packages, pulling packages from local disk.</span></span>  <span data-ttu-id="3c121-132">ASP.NET によってインストールされた既存のパッケージを使用するカスタム ASP.NET プロジェクトテンプレートを作成できるようになりましたが、テンプレートに追加の NuGet パッケージを追加できます。</span><span class="sxs-lookup"><span data-stu-id="3c121-132">You can now create a custom ASP.NET project template that uses the existing packages installed by ASP.NET but add extra NuGet packages into your template.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="3c121-133">バグの修正</span><span class="sxs-lookup"><span data-stu-id="3c121-133">Bug Fixes</span></span>
<span data-ttu-id="3c121-134">NuGet 2.2.1 には、いくつかの対象となるバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="3c121-134">NuGet 2.2.1 includes a few targeted bug fixes.</span></span> <span data-ttu-id="3c121-135">NuGet 2.2.1 で修正された作業項目の一覧については、 [このリリースの Nuget Issue Tracker](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="3c121-135">For a list of work items fixed in NuGet 2.2.1, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>


## <a name="known-issues"></a><span data-ttu-id="3c121-136">既知の問題</span><span class="sxs-lookup"><span data-stu-id="3c121-136">Known Issues</span></span>

<span data-ttu-id="3c121-137">ASP.NET プロジェクトテンプレートを拡張する場合は、インストールされているすべてのパッケージリポジトリで属性に同じ値を使用する必要があり `isPreunzipped` ます。</span><span class="sxs-lookup"><span data-stu-id="3c121-137">If you are extending ASP.NET project templates, all preinstalled package repositories must use the same value for the `isPreunzipped` attribute.</span></span>
