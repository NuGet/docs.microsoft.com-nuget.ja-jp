---
title: NuGet 3.0 RC リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.0 RC のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776567"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="13ae7-103">NuGet 3.0 RC リリースノート</span><span class="sxs-lookup"><span data-stu-id="13ae7-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="13ae7-104">[NuGet 3.0 ベータリリースノート](../release-notes/nuget-3.0-beta.md)  | [NuGet 3.0 RC2 リリースノート](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="13ae7-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="13ae7-105">NuGet 3.0 RC は、Visual Studio 2015 RC リリースで2015年4月29日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="13ae7-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="13ae7-106">このリリースには、新しいフレームワークをサポートするために、いくつかの重要なバグ修正、パフォーマンスの向上、および更新が含まれています。</span><span class="sxs-lookup"><span data-stu-id="13ae7-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="13ae7-107">これは、Visual Studio 2015 でのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="13ae7-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="13ae7-108">パフォーマンスについての継続的な取り組み</span><span class="sxs-lookup"><span data-stu-id="13ae7-108">Continued Focus on Performance</span></span>

<span data-ttu-id="13ae7-109">NuGet クエリの安定性とパフォーマンスは、注目している最新のトピックとして引き続き利用できます。</span><span class="sxs-lookup"><span data-stu-id="13ae7-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="13ae7-110">このリリースでは、NuGet UI と web サイトで非常に簡単な検索操作を確認できます。</span><span class="sxs-lookup"><span data-stu-id="13ae7-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="13ae7-111">サービスを監視し、サービスの使用方法を監視して、引き続きこれらの操作を調整できるようにします。</span><span class="sxs-lookup"><span data-stu-id="13ae7-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="13ae7-112">重大な問題の解決</span><span class="sxs-lookup"><span data-stu-id="13ae7-112">Significant Issues Resolved</span></span>

<span data-ttu-id="13ae7-113">NuGet クライアントを安定化するために、このリリースの一部として多くの問題を解決しました。</span><span class="sxs-lookup"><span data-stu-id="13ae7-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="13ae7-114">次に、いくつかの重要な問題の解決方法を簡単に示します。</span><span class="sxs-lookup"><span data-stu-id="13ae7-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="13ae7-115">ASP.NET 5 用の K フレームワークの名前変更の一部として、dnx および dnxcore[リンク](https://github.com/NuGet/Home/issues/215)を処理するようにフレームワークモニカーが更新されました。</span><span class="sxs-lookup"><span data-stu-id="13ae7-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="13ae7-116">Visual Studio UI[リンク](https://github.com/NuGet/Home/issues/232)のリンクからヘルプドキュメントを追加しました</span><span class="sxs-lookup"><span data-stu-id="13ae7-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="13ae7-117">`.nuspec`コンマ区切りフレームワーク参照[リンク](https://github.com/NuGet/Home/issues/276)を使用したでの複雑な参照の処理の向上</span><span class="sxs-lookup"><span data-stu-id="13ae7-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="13ae7-118">日本語のカルチャ[リンク](https://github.com/NuGet/Home/issues/253)のサポートを修正した</span><span class="sxs-lookup"><span data-stu-id="13ae7-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="13ae7-119">ASP.NET 5 プロジェクトが新しい v3 エンドポイント[リンク](https://github.com/NuGet/Home/issues/219)を使用できるように更新されたクライアント</span><span class="sxs-lookup"><span data-stu-id="13ae7-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="13ae7-120">ソース管理[リンク](https://github.com/NuGet/Home/issues/56)を使用してパッケージフォルダーをより適切に処理するよう更新されました</span><span class="sxs-lookup"><span data-stu-id="13ae7-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="13ae7-121">サテライトパッケージ[リンク](https://github.com/NuGet/Home/issues/17)のサポートを修正した</span><span class="sxs-lookup"><span data-stu-id="13ae7-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="13ae7-122">フレームワーク固有のコンテンツファイル[リンク](https://github.com/NuGet/Home/issues/18)のサポートを修正しました</span><span class="sxs-lookup"><span data-stu-id="13ae7-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="13ae7-123">GitHub のプレゼンスの見直し</span><span class="sxs-lookup"><span data-stu-id="13ae7-123">GitHub presence overhaul</span></span>

<span data-ttu-id="13ae7-124">[GitHub のソースコードリポジトリ](http://github.com/nuget/home)にいくつかの変更を加えました。</span><span class="sxs-lookup"><span data-stu-id="13ae7-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="13ae7-125">NuGet Visual Studio クライアント、Powershell コマンド、またはコマンドライン実行可能ファイルに問題がある場合は、それらの問題をログに記録し、 [GitHub ホームリポジトリの問題リスト](http://github.com/nuget/home/issues)で進行状況を監視することができます。</span><span class="sxs-lookup"><span data-stu-id="13ae7-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="13ae7-126">[GitHub NuGetGallery リポジトリ](http://github.com/nuget/NuGetGallery/issues)でギャラリーの問題を追跡しています。</span><span class="sxs-lookup"><span data-stu-id="13ae7-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="13ae7-127">引き続きご期待ください</span><span class="sxs-lookup"><span data-stu-id="13ae7-127">Stay Tuned</span></span>

<span data-ttu-id="13ae7-128">NuGet 3.0 の進行状況と発表の詳細については、 [ブログをご覧](http://blog.nuget.org) ください。</span><span class="sxs-lookup"><span data-stu-id="13ae7-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>