---
title: NuGet 2.8.1 リリース ノート
description: NuGet 2.8.1 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 8787aee36d31ed5d8071b35a8c243823029d135f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="67a9a-103">NuGet 2.8.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="67a9a-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="67a9a-104">[NuGet 2.8 リリース ノート](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 リリース ノート](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="67a9a-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="67a9a-105">NuGet 2.8.1 は、2014 年 4 月 2 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="67a9a-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="67a9a-106">リリースで注目に値する機能</span><span class="sxs-lookup"><span data-stu-id="67a9a-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="67a9a-107">Windows Phone 8.1 プロジェクトのサポート</span><span class="sxs-lookup"><span data-stu-id="67a9a-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="67a9a-108">このリリースでは、Windows Phone 8.1 を対象のプロジェクトに使用できる次の新しいターゲット フレームワーク モニカーできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="67a9a-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="67a9a-109">WindowsPhone81/WP81 (Silverlight ベースの Windows Phone プロジェクトに対して)</span><span class="sxs-lookup"><span data-stu-id="67a9a-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="67a9a-110">WindowsPhoneApp81/WPA81 (WinRT ベースの Windows Phone アプリ プロジェクトに対して)</span><span class="sxs-lookup"><span data-stu-id="67a9a-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="67a9a-111">NuGet WebMatrix 拡張機能の更新</span><span class="sxs-lookup"><span data-stu-id="67a9a-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="67a9a-112">このリリースを更新するために WebMatrix で見つかった NuGet クライアント[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 され XDT 変換などの機能です。</span><span class="sxs-lookup"><span data-stu-id="67a9a-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="67a9a-113">2.6.1 さらに、コア更新により、WebMatrix クライアントを含むより新しいバージョンの NuGet パッケージをインストールする、`.nuspec`スキーマがあり、ASP.NET の NuGet パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="67a9a-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="67a9a-114">WebMatrix 拡張機能の更新に関する詳細についてを参照してください特化[リリース ノート](../release-notes/nuget-2.6.1-for-WebMatrix.md)です。</span><span class="sxs-lookup"><span data-stu-id="67a9a-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="67a9a-115">バグ修正</span><span class="sxs-lookup"><span data-stu-id="67a9a-115">Bug Fixes</span></span>
<span data-ttu-id="67a9a-116">これらの機能だけでなく NuGet のこのリリースには、その他のバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="67a9a-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="67a9a-117">リリースで解決される 16 の合計の問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="67a9a-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="67a9a-118">作業の完全な一覧の項目で修正 NuGet 2.8.1、くださいビュー、[今回のリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)です。</span><span class="sxs-lookup"><span data-stu-id="67a9a-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="67a9a-119">With Visual Studio「14」CTP を reshipping</span><span class="sxs-lookup"><span data-stu-id="67a9a-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="67a9a-120">第 3 の 2014 年 6 月にリリースされた Visual Studio「14」ctp では、NuGet 2.8.1 はボックスに付属しています。</span><span class="sxs-lookup"><span data-stu-id="67a9a-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="67a9a-121">Par でままですが、サポートとその他の 2.8.1 VSIXes など Visual Studio 2013 用の 1 つです。</span><span class="sxs-lookup"><span data-stu-id="67a9a-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
