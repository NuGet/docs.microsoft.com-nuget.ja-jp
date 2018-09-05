---
title: NuGet 2.8.6 リリース ノート
description: NuGet 2.8.6 などのリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d57c658999ed3c79b962de84fd973276833ef3fd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546492"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="69390-103">NuGet 2.8.6 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="69390-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="69390-104">[NuGet 2.8.5 リリース ノート](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 リリース ノート](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="69390-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="69390-105">NuGet 2.8.6 がリリースされた修正プログラムと機能強化、Windows 10 UWP 開発モデル対応の配信可能性がありますパッケージをサポートするために、2.8.5 のマイナー アップデートとして、2015 年 7 月 20日一部の VSIX を対象とします。</span><span class="sxs-lookup"><span data-stu-id="69390-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="69390-106">このバージョンの NuGet パッケージ マネージャー拡張機能は、Visual Studio 2013 のサポートのみを提供します。</span><span class="sxs-lookup"><span data-stu-id="69390-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="69390-107">このリリースでは、NuGet パッケージ マネージャー ダイアログのサポートが追加必要があります。</span><span class="sxs-lookup"><span data-stu-id="69390-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="69390-108">Windows 10 のアプリケーションの開発をサポートするために UAP ターゲット フレームワーク モニカーが導入されました。</span><span class="sxs-lookup"><span data-stu-id="69390-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="69390-109">NuGet プロトコル バージョン 3 のエンドポイント</span><span class="sxs-lookup"><span data-stu-id="69390-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="69390-110">サポート[Nuget.Config](../consume-packages/configuring-nuget-behavior.md)リポジトリ ソース protocolVersion 属性。</span><span class="sxs-lookup"><span data-stu-id="69390-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="69390-111">既定値は「2」</span><span class="sxs-lookup"><span data-stu-id="69390-111">Default value is "2"</span></span>
* <span data-ttu-id="69390-112">ローカル キャッシュ内で必要なパッケージ バージョンが使用できない場合、リモート リポジトリにフォールバック</span><span class="sxs-lookup"><span data-stu-id="69390-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>