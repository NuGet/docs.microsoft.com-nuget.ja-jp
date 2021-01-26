---
title: NuGet 2.8.6 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 2.8.6 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776703"
---
# <a name="nuget-286-release-notes"></a><span data-ttu-id="0facb-103">NuGet 2.8.6 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="0facb-103">NuGet 2.8.6 Release Notes</span></span>

<span data-ttu-id="0facb-104">[NuGet 2.8.5 のリリースノート](../release-notes/nuget-2.8.5.md)  | [NuGet 2.8.7 のリリースノート](../release-notes/nuget-2.8.7.md)</span><span class="sxs-lookup"><span data-stu-id="0facb-104">[NuGet 2.8.5 Release Notes](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md)</span></span>

<span data-ttu-id="0facb-105">NuGet 2.8.6 は、2015年7月20日にリリースされました。また、Windows 10 UWP 開発モデルのサポートと共に提供される可能性のあるパッケージのサポートを対象とした修正プログラムと機能強化が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0facb-105">NuGet 2.8.6 was released July 20, 2015 as a minor update to our 2.8.5 VSIX with some targeted fixes and improvements to support packages that may be delivered with support for the Windows 10 UWP development model.</span></span>

<span data-ttu-id="0facb-106">このバージョンの NuGet パッケージマネージャー拡張機能では Visual Studio 2013 のみがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="0facb-106">This version of the NuGet package manager extension provides support for Visual Studio 2013 only.</span></span>

<span data-ttu-id="0facb-107">このリリースでは、NuGet パッケージマネージャーダイアログで次の機能が追加されました。</span><span class="sxs-lookup"><span data-stu-id="0facb-107">In this release, the NuGet Package Manager dialog had support added for:</span></span>

* <span data-ttu-id="0facb-108">Windows 10 アプリケーション開発をサポートする UAP ターゲットフレームワークモニカーが導入されました。</span><span class="sxs-lookup"><span data-stu-id="0facb-108">Introduced the UAP Target Framework Moniker to support Windows 10 Application Development.</span></span>
* <span data-ttu-id="0facb-109">NuGet プロトコルバージョン3エンドポイント</span><span class="sxs-lookup"><span data-stu-id="0facb-109">NuGet protocol version 3 endpoints</span></span>
* <span data-ttu-id="0facb-110">リポジトリソースでの [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion 属性のサポート。</span><span class="sxs-lookup"><span data-stu-id="0facb-110">Support for [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) protocolVersion attribute on repository sources.</span></span> <span data-ttu-id="0facb-111">既定値は "2" です。</span><span class="sxs-lookup"><span data-stu-id="0facb-111">Default value is "2"</span></span>
* <span data-ttu-id="0facb-112">必要なパッケージバージョンがローカルキャッシュで利用できない場合に、リモートリポジトリにフォールバックする</span><span class="sxs-lookup"><span data-stu-id="0facb-112">Falling back to remote repository if a required package version is not available in the local cache</span></span>