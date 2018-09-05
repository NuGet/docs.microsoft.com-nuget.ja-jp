---
title: NuGet 2.8.5 リリース ノート
description: NuGet 2.8.5 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: aa03b00a0043a4805f33900124c13b0777c2b7a3
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548626"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="a01f5-103">NuGet 2.8.5 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="a01f5-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="a01f5-104">[NuGet 2.8.3 リリース ノート](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 リリース ノート](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="a01f5-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="a01f5-105">NuGet 2.8.5 は、2015 年 3 月 30 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="a01f5-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="a01f5-106">マイナー更新は、2.8.3 に一部の VSIX に修正プログラムが対象とします。</span><span class="sxs-lookup"><span data-stu-id="a01f5-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="a01f5-107">このリリースで NuGet パッケージ マネージャー ダイアログのサポートが追加された[DNX ターゲット フレームワーク モニカー](https://github.com/aspnet/dnx)します。</span><span class="sxs-lookup"><span data-stu-id="a01f5-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="a01f5-108">サポートされているこれらの新しいフレームワーク モニカーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a01f5-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="a01f5-109">**core50** - 'base' のターゲット フレームワーク モニカー (TFM)、Core CLR と互換性があります。</span><span class="sxs-lookup"><span data-stu-id="a01f5-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="a01f5-110">**dnx452** - 完全 4.5.2 を使用して A TFM を DNX ベース特定のアプリ、フレームワークのバージョン</span><span class="sxs-lookup"><span data-stu-id="a01f5-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="a01f5-111">**dnx46** - 4.6 を完全なバージョンの framework を使用して A TFM を DNX ベース特定のアプリ</span><span class="sxs-lookup"><span data-stu-id="a01f5-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="a01f5-112">**dnxcore50** - Core 5.0 のバージョンの framework を使用して、TFM を DNX ベース特定のアプリ</span><span class="sxs-lookup"><span data-stu-id="a01f5-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="a01f5-113">1 つのバグには、FSharp プロジェクトに正しくインストールされませんでした、パッケージが修正済み。</span><span class="sxs-lookup"><span data-stu-id="a01f5-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400