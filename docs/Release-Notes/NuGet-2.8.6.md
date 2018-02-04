---
title: "NuGet 2.8.6 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "NuGet 2.8.6 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 2.8.6 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dfd0a76967280cc6a16b37fe2b2a3362231fce5
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="8e4a8-104">NuGet 2.8.6 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="8e4a8-104">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="8e4a8-105">[NuGet 2.8.5 リリース ノート](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 リリース ノート](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="8e4a8-105">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="8e4a8-106">NuGet 2.8.6 がリリースされた修正と Windows 10 UWP 開発モデルのサポートされる可能性があるパッケージをサポートするために強化、2.8.5 のマイナー アップデートとして、2015 年 7 月 20日の VSIX を対象とします。</span><span class="sxs-lookup"><span data-stu-id="8e4a8-106">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="8e4a8-107">このバージョンの NuGet パッケージ マネージャー拡張機能は、Visual Studio 2013 のサポートのみを提供します。</span><span class="sxs-lookup"><span data-stu-id="8e4a8-107">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="8e4a8-108">このリリースでは、NuGet Package Manager ダイアログには、サポートの追加が必要があります。</span><span class="sxs-lookup"><span data-stu-id="8e4a8-108">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="8e4a8-109">Windows 10 のアプリケーションの開発をサポートするために UAP ターゲット フレームワーク モニカーが導入されました。</span><span class="sxs-lookup"><span data-stu-id="8e4a8-109">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="8e4a8-110">NuGet プロトコル バージョン 3 のエンドポイント</span><span class="sxs-lookup"><span data-stu-id="8e4a8-110">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="8e4a8-111">サポート[Nuget.Config](../consume-packages/configuring-nuget-behavior.md)リポジトリ ソースに対する protocolVersion 属性。</span><span class="sxs-lookup"><span data-stu-id="8e4a8-111">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="8e4a8-112">既定値は「2」</span><span class="sxs-lookup"><span data-stu-id="8e4a8-112">Default value is "2"</span></span>
* <span data-ttu-id="8e4a8-113">ローカル キャッシュ内では、必要なパッケージのバージョンが使用できない場合に、リモート リポジトリに戻る</span><span class="sxs-lookup"><span data-stu-id="8e4a8-113">Falling back to remote repository if a required package version is not available in the local cache</span></span>