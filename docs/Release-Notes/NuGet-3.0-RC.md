---
title: "NuGet 3.0 RC のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: cd0c102f-bc33-4aa2-a921-61fa21d42b28
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.0 RC のリリース ノートします。"
keywords: "NuGet 3.0 RC のリリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5d0eeae479617bc30901b599251628f72950cc67
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-30-rc-release-notes"></a><span data-ttu-id="827f0-104">NuGet 3.0 RC のリリース ノートには</span><span class="sxs-lookup"><span data-stu-id="827f0-104">NuGet 3.0 RC Release Notes</span></span>

<span data-ttu-id="827f0-105">[NuGet 3.0 Beta リリース ノート](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 リリース ノート](../release-notes/nuget-3.0-RC2.md)</span><span class="sxs-lookup"><span data-stu-id="827f0-105">[NuGet 3.0 Beta Release Notes](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md)</span></span>

<span data-ttu-id="827f0-106">NuGet 3.0 RC は、Visual Studio 2015 RC のリリースでは、2015 年 4 月 29 日にリリースされました。</span><span class="sxs-lookup"><span data-stu-id="827f0-106">NuGet 3.0 RC was released on April 29, 2015 with the Visual Studio 2015 RC release.</span></span> <span data-ttu-id="827f0-107">このリリースでは重要なバグ修正、パフォーマンスの向上、および新しいフレームワークをサポートするために更新プログラムの数。</span><span class="sxs-lookup"><span data-stu-id="827f0-107">This release has a number of important bug fixes, performance improvements and updates to support the new frameworks.</span></span>  <span data-ttu-id="827f0-108">Visual Studio 2015 のできるだけです。</span><span class="sxs-lookup"><span data-stu-id="827f0-108">It is only available for Visual Studio 2015.</span></span>

### <a name="continued-focus-on-performance"></a><span data-ttu-id="827f0-109">継続的なパフォーマンス重視</span><span class="sxs-lookup"><span data-stu-id="827f0-109">Continued Focus on Performance</span></span>

<span data-ttu-id="827f0-110">安定性と NuGet のクエリのパフォーマンスに焦点を当てたおをホット トピックし続けます。</span><span class="sxs-lookup"><span data-stu-id="827f0-110">Stability and performance of NuGet queries continue to be a hot topic that we are focusing on.</span></span>  <span data-ttu-id="827f0-111">このリリースでは、NuGet UI や web サイトでの非常に高速検索操作を参照してくださいを開始する必要があります。</span><span class="sxs-lookup"><span data-stu-id="827f0-111">With this release, you should start to see very quick search operations in the NuGet UI and website.</span></span>  <span data-ttu-id="827f0-112">サービスとこれらの操作を調整することを続行するために、サービスを使用する方法を監視しています。</span><span class="sxs-lookup"><span data-stu-id="827f0-112">We're monitoring the service and how you use the service so that we can continue to tune these operations.</span></span>

## <a name="significant-issues-resolved"></a><span data-ttu-id="827f0-113">重要な問題の解決</span><span class="sxs-lookup"><span data-stu-id="827f0-113">Significant Issues Resolved</span></span>

<span data-ttu-id="827f0-114">NuGet クライアントを安定化するために、このリリースの一部としての多くの問題を解決します。</span><span class="sxs-lookup"><span data-stu-id="827f0-114">In order to stabilize the NuGet clients, we resolved many issues as part of this release.</span></span>  <span data-ttu-id="827f0-115">いくつかの解決より重要な問題の簡単な一覧を次に示します。</span><span class="sxs-lookup"><span data-stu-id="827f0-115">Here is just a brief list of some of the more important issues resolved:</span></span>

* <span data-ttu-id="827f0-116">Dnx および dnxcore を処理する更新されたフレームワーク モニカーの ASP.NET 5 K、フレームワークの名前の変更の一環として、[リンク](https://github.com/NuGet/Home/issues/215)</span><span class="sxs-lookup"><span data-stu-id="827f0-116">As part of the rename of the K framework for ASP.NET 5, framework monikers have been updated to handle dnx and dnxcore [link](https://github.com/NuGet/Home/issues/215)</span></span>
* <span data-ttu-id="827f0-117">Visual Studio UI 内のリンクからヘルプ ドキュメントを追加[リンク](https://github.com/NuGet/Home/issues/232)</span><span class="sxs-lookup"><span data-stu-id="827f0-117">Added help documentation from links in the Visual Studio UI [link](https://github.com/NuGet/Home/issues/232)</span></span>
* <span data-ttu-id="827f0-118">複雑な参照の処理の改善`.nuspec`カンマ区切りのフレームワーク参照を含む[リンク](https://github.com/NuGet/Home/issues/276)</span><span class="sxs-lookup"><span data-stu-id="827f0-118">Better handling of complex references in `.nuspec` with comma-delimited framework references [link](https://github.com/NuGet/Home/issues/276)</span></span>
* <span data-ttu-id="827f0-119">日本語のカルチャのサポートを固定[リンク](https://github.com/NuGet/Home/issues/253)</span><span class="sxs-lookup"><span data-stu-id="827f0-119">Fixed support for Japanese cultures [link](https://github.com/NuGet/Home/issues/253)</span></span>
* <span data-ttu-id="827f0-120">ASP.NET 5 プロジェクトの新しい v3 エンドポイントの使用を許可する更新されたクライアント[リンク](https://github.com/NuGet/Home/issues/219)</span><span class="sxs-lookup"><span data-stu-id="827f0-120">Updated client to allow ASP.NET 5 projects to use new v3 endpoints [link](https://github.com/NuGet/Home/issues/219)</span></span>
* <span data-ttu-id="827f0-121">ソース コントロールのハンドルをより効率的に更新されたパッケージ フォルダー[リンク](https://github.com/NuGet/Home/issues/56)</span><span class="sxs-lookup"><span data-stu-id="827f0-121">Updated to better handle packages folder with source control [link](https://github.com/NuGet/Home/issues/56)</span></span>
* <span data-ttu-id="827f0-122">サテライトのパッケージのサポートを固定[リンク](https://github.com/NuGet/Home/issues/17)</span><span class="sxs-lookup"><span data-stu-id="827f0-122">Fixed support for satellite packages [link](https://github.com/NuGet/Home/issues/17)</span></span>
* <span data-ttu-id="827f0-123">フレームワーク固有のコンテンツ ファイルのサポートを修正[リンク](https://github.com/NuGet/Home/issues/18)</span><span class="sxs-lookup"><span data-stu-id="827f0-123">Corrected support for framework-specific content files [link](https://github.com/NuGet/Home/issues/18)</span></span>

## <a name="github-presence-overhaul"></a><span data-ttu-id="827f0-124">GitHub プレゼンスの修理</span><span class="sxs-lookup"><span data-stu-id="827f0-124">GitHub presence overhaul</span></span>

<span data-ttu-id="827f0-125">いくつかの変更を加えられた、 [GitHub でコード リポジトリのソース](http://github.com/nuget/home)です。</span><span class="sxs-lookup"><span data-stu-id="827f0-125">We've made some changes to our [source code repositories on GitHub](http://github.com/nuget/home).</span></span>  <span data-ttu-id="827f0-126">NuGet の Visual Studio クライアント、Powershell コマンドまたはコマンドラインで問題があれば実行可能それらの問題をログおよび監視できますその進行状況で、[ホームの GitHub リポジトリの問題一覧](http://github.com/nuget/home/issues)です。</span><span class="sxs-lookup"><span data-stu-id="827f0-126">If you have any issues with the NuGet Visual Studio client, the Powershell commands, or the command-line executable you can log those issues and monitor their progress on our [GitHub Home repository issues list](http://github.com/nuget/home/issues).</span></span>  <span data-ttu-id="827f0-127">ギャラリー内の問題を追跡して、 [GitHub NuGetGallery リポジトリ](http://github.com/nuget/NuGetGallery/issues)です。</span><span class="sxs-lookup"><span data-stu-id="827f0-127">We are tracking issues for the gallery in our [GitHub NuGetGallery repository](http://github.com/nuget/NuGetGallery/issues).</span></span>


## <a name="stay-tuned"></a><span data-ttu-id="827f0-128">待ち</span><span class="sxs-lookup"><span data-stu-id="827f0-128">Stay Tuned</span></span>

<span data-ttu-id="827f0-129">くださいに注意[私たちのブログ](http://blog.nuget.org)の詳細の進行状況と NuGet 3.0 のお知らせください。</span><span class="sxs-lookup"><span data-stu-id="827f0-129">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements for NuGet 3.0!</span></span>