---
title: NuGet 2.8.5 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f729092bc964b286a007564bd3bbd8c79bc895c9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780355"
---
# <a name="nuget-285-release-notes"></a><span data-ttu-id="5dd3c-103">NuGet 2.8.5 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="5dd3c-103">NuGet 2.8.5 Release Notes</span></span>

<span data-ttu-id="5dd3c-104">[NuGet 2.8.3 のリリースノート](../release-notes/nuget-2.8.3.md)  | [NuGet 2.8.6 のリリースノート](../release-notes/nuget-2.8.6.md)</span><span class="sxs-lookup"><span data-stu-id="5dd3c-104">[NuGet 2.8.3 Release Notes](../release-notes/nuget-2.8.3.md) | [NuGet 2.8.6 Release Notes](../release-notes/nuget-2.8.6.md)</span></span>

<span data-ttu-id="5dd3c-105">NuGet 2.8.5 は2015年3月30日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="5dd3c-105">NuGet 2.8.5 was released March 30, 2015.</span></span> <span data-ttu-id="5dd3c-106">これは、一部の修正プログラムが適用された 2.8.3 VSIX のマイナー更新です。</span><span class="sxs-lookup"><span data-stu-id="5dd3c-106">It is a minor update to our 2.8.3 VSIX with some targeted fixes.</span></span>

<span data-ttu-id="5dd3c-107">このリリースでは、 [Dnx ターゲットフレームワークモニカー](https://github.com/aspnet/dnx)の [NuGet パッケージマネージャーのサポート] ダイアログが追加されました。</span><span class="sxs-lookup"><span data-stu-id="5dd3c-107">In this release, the support for NuGet Package Manager dialog was added for [DNX Target Framework Monikers](https://github.com/aspnet/dnx).</span></span>  <span data-ttu-id="5dd3c-108">次のような新しいフレームワークモニカーがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="5dd3c-108">These new framework monikers that are supported include:</span></span>

* <span data-ttu-id="5dd3c-109">**core50** -コア CLR と互換性のある ' base ' ターゲットフレームワークモニカー (tfm) です。</span><span class="sxs-lookup"><span data-stu-id="5dd3c-109">**core50** - A 'base' target framework moniker (TFM) that is compatible with the Core CLR.</span></span>
* <span data-ttu-id="5dd3c-110">**dnx452** -完全な4.5.2 バージョンのフレームワークを使用する dnx ベースのアプリに固有の A tfm</span><span class="sxs-lookup"><span data-stu-id="5dd3c-110">**dnx452** - A TFM specific to DNX-based apps using the full 4.5.2 version of the framework</span></span>
* <span data-ttu-id="5dd3c-111">**dnx46** -完全な4.6 バージョンのフレームワークを使用する dnx ベースのアプリに固有の A tfm</span><span class="sxs-lookup"><span data-stu-id="5dd3c-111">**dnx46** - A TFM specific to DNX-based apps using the full 4.6 version of the framework</span></span>
* <span data-ttu-id="5dd3c-112">**dnxcore50** -Core 5.0 バージョンのフレームワークを使用する dnx ベースのアプリに固有の A tfm</span><span class="sxs-lookup"><span data-stu-id="5dd3c-112">**dnxcore50** - A TFM specific to DNX-based apps using the Core 5.0 version of the framework</span></span>

<span data-ttu-id="5dd3c-113">1つのバグが修正されました。これにより、パッケージを Fsharp.core プロジェクトに適切にインストールできませんでした。</span><span class="sxs-lookup"><span data-stu-id="5dd3c-113">One bug was fixed that prevented packages from installing into FSharp projects properly:</span></span>

https://nuget.codeplex.com/workitem/4400