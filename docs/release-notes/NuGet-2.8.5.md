---
title: NuGet 2.8.5 リリース ノート
description: NuGet 2.8.5 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 40557035e445d07e7acf301e34b750b329ba9990
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820080"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="c1d12-103">NuGet 2.8.5 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="c1d12-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="c1d12-104">[NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 リリース ノート](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="c1d12-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="c1d12-105">NuGet 2.8.5 は、2015 年 3 月 30 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="c1d12-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="c1d12-106">マイナー アップデートはいくつかで VSIX、2.8.3 に修正プログラムを対象とします。</span><span class="sxs-lookup"><span data-stu-id="c1d12-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="c1d12-107">このリリースでは、NuGet パッケージ マネージャー ダイアログ ボックスのサポートが追加されました[DNX ターゲット フレームワーク モニカー](https://github.com/aspnet/dnx)です。</span><span class="sxs-lookup"><span data-stu-id="c1d12-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="c1d12-108">サポートされているこれらの新しいフレームワーク モニカーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="c1d12-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="c1d12-109">**core50** - a 'base' のターゲット フレームワーク モニカー (TFM) Core CLR と互換性があります。</span><span class="sxs-lookup"><span data-stu-id="c1d12-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="c1d12-110">**dnx452** - A TFM DNX ベースを特定のアプリをフル 4.5.2 を使用して framework のバージョン</span><span class="sxs-lookup"><span data-stu-id="c1d12-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="c1d12-111">**dnx46** - framework の 4.6 完全バージョンを使用して A TFM DNX ベースを特定のアプリ</span><span class="sxs-lookup"><span data-stu-id="c1d12-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="c1d12-112">**dnxcore50** - A TFM DNX ベースを特定のアプリを Core 5.0 のバージョンの framework を使用します。</span><span class="sxs-lookup"><span data-stu-id="c1d12-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="c1d12-113">1 つのバグが修正された FSharp プロジェクトに正しくインストールされないパッケージ化するされませんでした。</span><span class="sxs-lookup"><span data-stu-id="c1d12-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400