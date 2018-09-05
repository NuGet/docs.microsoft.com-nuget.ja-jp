---
title: NuGet 2.8.1 のリリース ノート
description: NuGet 2.8.1 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 39fb7db00e18e32eef15adc11764a122c97ddfd5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545240"
---
# <a name="nuget-281-release-notes"></a><span data-ttu-id="20890-103">NuGet 2.8.1 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="20890-103">NuGet 2.8.1 Release Notes</span></span>

<span data-ttu-id="20890-104">[NuGet 2.8 のリリース ノート](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 リリース ノート](../release-notes/nuget-2.8.2.md)</span><span class="sxs-lookup"><span data-stu-id="20890-104">[NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md) | [NuGet 2.8.2 Release Notes](../release-notes/nuget-2.8.2.md)</span></span>

<span data-ttu-id="20890-105">NuGet 2.8.1 は、2014 年 4 月 2 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="20890-105">NuGet 2.8.1 was released on April 2, 2014.</span></span>

## <a name="notable-features-in-the-release"></a><span data-ttu-id="20890-106">リリースで注目すべき機能</span><span class="sxs-lookup"><span data-stu-id="20890-106">Notable features in the release</span></span>

### <a name="support-for-windows-phone-81-projects"></a><span data-ttu-id="20890-107">Windows Phone 8.1 プロジェクトのサポート</span><span class="sxs-lookup"><span data-stu-id="20890-107">Support for Windows Phone 8.1 Projects</span></span>
<span data-ttu-id="20890-108">このリリースでは、Windows Phone 8.1 をターゲット プロジェクトに使用できる次の新しいターゲット フレームワーク モニカーできるようになりました。</span><span class="sxs-lookup"><span data-stu-id="20890-108">This release now supports the following new target framework monikers which can be used to target Windows Phone 8.1 projects:</span></span>

* <span data-ttu-id="20890-109">WindowsPhone81/(Windows Phone の Silverlight ベースのプロジェクト) に対して WP81</span><span class="sxs-lookup"><span data-stu-id="20890-109">WindowsPhone81 / WP81 (for Silverlight-based Windows Phone projects)</span></span>
* <span data-ttu-id="20890-110">WindowsPhoneApp81/WPA81 (の WinRT ベースの Windows Phone アプリ プロジェクトの場合)</span><span class="sxs-lookup"><span data-stu-id="20890-110">WindowsPhoneApp81 / WPA81 (for WinRT-based Windows Phone App projects)</span></span>

### <a name="update-of-the-nuget-webmatrix-extension"></a><span data-ttu-id="20890-111">WebMatrix の NuGet 拡張機能の更新</span><span class="sxs-lookup"><span data-stu-id="20890-111">Update of the NuGet WebMatrix Extension</span></span>
<span data-ttu-id="20890-112">このリリースで更新するために WebMatrix に、NuGet クライアント[NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 し、XDT 変換などの機能が使用されます。</span><span class="sxs-lookup"><span data-stu-id="20890-112">This release updates the NuGet client found in WebMatrix to [NuGet.Core](https://www.nuget.org/packages/Nuget.Core/2.6.1) 2.6.1 and brings with it features such as XDT transformations.</span></span> <span data-ttu-id="20890-113">2.6.1 さらに、中核となる更新プログラムによりより新しいバージョンを含む NuGet パッケージをインストールする WebMatrix クライアント、`.nuspec`スキーマで、ASP.NET の NuGet パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="20890-113">More importantly, the 2.6.1 core update enables the WebMatrix client to install NuGet packages which contain more recent versions of the `.nuspec` schema, which includes the ASP.NET NuGet packages.</span></span>

<span data-ttu-id="20890-114">WebMatrix 拡張機能の更新プログラムの詳細については、これらの参照してください[リリース ノート](../release-notes/nuget-2.6.1-for-WebMatrix.md)します。</span><span class="sxs-lookup"><span data-stu-id="20890-114">For more information about the WebMatrix Extension update, see those specific [release notes](../release-notes/nuget-2.6.1-for-WebMatrix.md).</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="20890-115">バグ修正</span><span class="sxs-lookup"><span data-stu-id="20890-115">Bug Fixes</span></span>
<span data-ttu-id="20890-116">これらの機能に加えて NuGet のこのリリースには、その他のバグ修正が含まれています。</span><span class="sxs-lookup"><span data-stu-id="20890-116">In addition to these features, this release of NuGet includes other bug fixes.</span></span> <span data-ttu-id="20890-117">リリースで解決された問題の合計 16 が発生しました。</span><span class="sxs-lookup"><span data-stu-id="20890-117">There were 16 total issues addressed in the release.</span></span> <span data-ttu-id="20890-118">作業の完全な一覧については固定のアイテムの nuget 2.8.1、くださいビュー、[このリリースの NuGet Issue Tracker](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All)します。</span><span class="sxs-lookup"><span data-stu-id="20890-118">For a full list of the work items fixed in NuGet 2.8.1, please view the [NuGet Issue Tracker for this release](https://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%202.8.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0&reasonClosed=All).</span></span>

### <a name="reshipping-with-visual-studio-14-ctp"></a><span data-ttu-id="20890-119">Visual studio「14」CTP を reshipping</span><span class="sxs-lookup"><span data-stu-id="20890-119">Reshipping with Visual Studio "14" CTP</span></span>
<span data-ttu-id="20890-120">3 番目の 2014 年 6 月にリリースされた Visual Studio「14」ctp では、NuGet 2.8.1 は、ボックスに付属しています。</span><span class="sxs-lookup"><span data-stu-id="20890-120">In Visual Studio "14" CTP released on June 3rd 2014, NuGet 2.8.1 is shipped in the box.</span></span> <span data-ttu-id="20890-121">ですが、サポート機能には、同等がそのまま他 2.8.1 で VSIXes for Visual Studio 2013 など。</span><span class="sxs-lookup"><span data-stu-id="20890-121">The features it support remain in-par with other 2.8.1 VSIXes such as the one for Visual Studio 2013.</span></span>
