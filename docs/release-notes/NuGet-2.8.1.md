---
title: NuGet 2.8.1 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4dcd8ab140026c39345f850ac00a7a5f26a0e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776768"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="55f49-103">NuGet 2.8.1 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="55f49-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="55f49-104">[NuGet 2.8 リリースノート](../release-notes/nuget-2.8.md)  | [NuGet 2.8.2 のリリースノート](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="55f49-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="55f49-105">NuGet 2.8.1 は2014年4月2日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="55f49-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="55f49-106">リリースの注目すべき機能</span><span class="sxs-lookup"><span data-stu-id="55f49-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="55f49-107">Windows Phone 8.1 プロジェクトのサポート</span><span class="sxs-lookup"><span data-stu-id="55f49-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="55f49-108">このリリースでは、Windows Phone 8.1 プロジェクトのターゲットとして使用できる次の新しいターゲットフレームワークモニカーがサポートされるようになりました。</span><span class="sxs-lookup"><span data-stu-id="55f49-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="55f49-109">WindowsPhone81/WP81 (Silverlight ベースの Windows Phone プロジェクトの場合)</span><span class="sxs-lookup"><span data-stu-id="55f49-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="55f49-110">WindowsPhoneApp81/WPA81 (WinRT ベースの Windows Phone アプリプロジェクト用)</span><span class="sxs-lookup"><span data-stu-id="55f49-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="55f49-111">NuGet WebMatrix 拡張機能の更新</span><span class="sxs-lookup"><span data-stu-id="55f49-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="55f49-112">このリリースでは、WebMatrix の NuGet クライアントを [2.6.1 に](https://www.nuget.org/packages/Nuget.Core/2.6.1) 更新し、xdt 変換などの it 機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="55f49-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="55f49-113">さらに重要な点として、2.6.1 core 更新プログラムを使用すると、WebMatrix クライアントは、ASP.NET NuGet パッケージを含む、より新しいバージョンのスキーマを含む NuGet パッケージをインストールでき `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="55f49-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="55f49-114">WebMatrix 拡張機能の更新の詳細については、これらの特定の [リリースノート](../release-notes/nuget-2.6.1-for-WebMatrix.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="55f49-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="55f49-115">バグの修正</span><span class="sxs-lookup"><span data-stu-id="55f49-115">Bug Fixes</span></span>
<span data-ttu-id="55f49-116">これらの機能に加えて、この NuGet のリリースには他のバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="55f49-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="55f49-117">リリースで解決された問題の合計数は16個でした。</span><span class="sxs-lookup"><span data-stu-id="55f49-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="55f49-118">NuGet 2.8.1 で修正された作業項目の完全な一覧については、 [このリリースの Nuget Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="55f49-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="55f49-119">Visual Studio "14" CTP での再配布</span><span class="sxs-lookup"><span data-stu-id="55f49-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="55f49-120">2014年6月3日にリリースされた Visual Studio "14" CTP では、このボックスに NuGet 2.8.1 が付属しています。</span><span class="sxs-lookup"><span data-stu-id="55f49-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="55f49-121">サポートされている機能は、Visual Studio 2013 のような他の 2.8.1 VSIXes と同等のものです。</span><span class="sxs-lookup"><span data-stu-id="55f49-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
