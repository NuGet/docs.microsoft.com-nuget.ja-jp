---
title: NuGet 3.0 RC リリース ノートします。
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.0 RC のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551720"
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="9132a-103">NuGet 3.0 RC リリース ノートします。</span><span class="sxs-lookup"><span data-stu-id="9132a-103">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="9132a-104">[NuGet 3.0 ベータ版のリリース ノート](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 リリース ノート](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="9132a-104">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="9132a-105">NuGet 3.0 RC は、Visual Studio 2015 RC リリースでは、2015 年 4 月 29 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="9132a-105">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="9132a-106">このリリースではさまざまな重要なバグの修正、パフォーマンスの向上と新しいフレームワークをサポートするために更新します。</span><span class="sxs-lookup"><span data-stu-id="9132a-106">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="9132a-107">Visual Studio 2015 の使用可能なは。</span><span class="sxs-lookup"><span data-stu-id="9132a-107">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="9132a-108">パフォーマンスで継続的なフォーカス</span><span class="sxs-lookup"><span data-stu-id="9132a-108">Continued Focus on Performance</span></span>

<span data-ttu-id="9132a-109">安定性と NuGet のクエリのパフォーマンスに注目していますが、ホットなトピックを続行します。</span><span class="sxs-lookup"><span data-stu-id="9132a-109">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="9132a-110">このリリースでは、NuGet UI と web サイトで非常に高速検索操作を参照してくださいを開始する必要があります。</span><span class="sxs-lookup"><span data-stu-id="9132a-110">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="9132a-111">サービスおよびこれらの操作を調整することを続行するために、サービスを使用する方法を監視しています。</span><span class="sxs-lookup"><span data-stu-id="9132a-111">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="9132a-112">重要な問題の解決</span><span class="sxs-lookup"><span data-stu-id="9132a-112">Significant Issues Resolved</span></span>

<span data-ttu-id="9132a-113">NuGet クライアントを安定化するためには、このリリースの一環として多くの問題を解決しました。</span><span class="sxs-lookup"><span data-stu-id="9132a-113">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="9132a-114">さらに重要な問題を解決のいくつかの簡単な一覧だけを次に示します。</span><span class="sxs-lookup"><span data-stu-id="9132a-114">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="9132a-115">Dnx と dnxcore を処理する ASP.NET 5 の K フレームワークの名前の変更の一環として、フレームワークのモニカーが更新されました[リンク](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="9132a-115">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="9132a-116">Visual Studio UI 内のリンクからヘルプ ドキュメントが追加されました[リンク](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="9132a-116">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="9132a-117">複雑な参照の処理の改善`.nuspec`フレームワークのコンマ区切りの参照を含む[リンク](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="9132a-117">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="9132a-118">日本語のカルチャのサポートを修正しました[リンク。](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="9132a-118">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="9132a-119">ASP.NET 5 プロジェクトで新しい v3 エンドポイントの使用を許可する更新されたクライアント[リンク](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="9132a-119">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="9132a-120">ソース コントロールにハンドルを適切に更新されたパッケージ フォルダー[リンク](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="9132a-120">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="9132a-121">サテライト パッケージのサポートを修正しました[リンク。](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="9132a-121">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="9132a-122">フレームワークに固有のコンテンツ ファイルのサポートを修正[リンク](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="9132a-122">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="9132a-123">GitHub のプレゼンスの改訂</span><span class="sxs-lookup"><span data-stu-id="9132a-123">GitHub presence overhaul</span></span>

<span data-ttu-id="9132a-124">いくつかの変更を行いました、[ソース コード リポジトリの GitHub](http://github.com/nuget/home)します。</span><span class="sxs-lookup"><span data-stu-id="9132a-124">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="9132a-125">Visual Studio の NuGet クライアント、Powershell コマンド、または、コマンド ラインで問題がある場合実行可能ファイルこれらの問題を記録してで進行状況を監視、[ホームの GitHub リポジトリの issue 一覧](http://github.com/nuget/home/issues)します。</span><span class="sxs-lookup"><span data-stu-id="9132a-125">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="9132a-126">ギャラリーでの問題を追跡します、[リポジトリの GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues)します。</span><span class="sxs-lookup"><span data-stu-id="9132a-126">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="9132a-127">お見逃しなく</span><span class="sxs-lookup"><span data-stu-id="9132a-127">Stay Tuned</span></span>

<span data-ttu-id="9132a-128">監視してください[ブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせください。</span><span class="sxs-lookup"><span data-stu-id="9132a-128">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>