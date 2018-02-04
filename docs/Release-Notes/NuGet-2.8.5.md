---
title: "NuGet 2.8.5 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet 2.8.5 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.8.5 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ace56284e56f24394d49c0598ec3604b62caaf67
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="e053c-104">NuGet 2.8.5 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="e053c-104">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="e053c-105">[NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 リリース ノート](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="e053c-105">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="e053c-106">NuGet 2.8.5 は、2015 年 3 月 30 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="e053c-106">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="e053c-107">マイナー アップデートはいくつかで VSIX、2.8.3 に修正プログラムを対象とします。</span><span class="sxs-lookup"><span data-stu-id="e053c-107">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="e053c-108">このリリースでは、NuGet パッケージ マネージャー ダイアログ ボックスのサポートが追加されました[DNX ターゲット フレームワーク モニカー](https://github.com/aspnet/dnx)です。</span><span class="sxs-lookup"><span data-stu-id="e053c-108">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="e053c-109">サポートされているこれらの新しいフレームワーク モニカーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="e053c-109">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="e053c-110">**core50** - a 'base' のターゲット フレームワーク モニカー (TFM) Core CLR と互換性があります。</span><span class="sxs-lookup"><span data-stu-id="e053c-110">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="e053c-111">**dnx452** - A TFM DNX ベースを特定のアプリをフル 4.5.2 を使用して framework のバージョン</span><span class="sxs-lookup"><span data-stu-id="e053c-111">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="e053c-112">**dnx46** - framework の 4.6 完全バージョンを使用して A TFM DNX ベースを特定のアプリ</span><span class="sxs-lookup"><span data-stu-id="e053c-112">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="e053c-113">**dnxcore50** - A TFM DNX ベースを特定のアプリを Core 5.0 のバージョンの framework を使用します。</span><span class="sxs-lookup"><span data-stu-id="e053c-113">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="e053c-114">1 つのバグが修正された FSharp プロジェクトに正しくインストールされないパッケージ化するされませんでした。</span><span class="sxs-lookup"><span data-stu-id="e053c-114">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

<span data-ttu-id="e053c-115">https://nuget.codeplex.com/workitem/4400</span><span class="sxs-lookup"><span data-stu-id="e053c-115">https://nuget.codeplex.com/workitem/4400</span></span>