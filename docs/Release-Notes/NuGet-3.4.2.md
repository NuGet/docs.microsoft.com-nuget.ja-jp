---
title: "NuGet 3.4.2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: b514da09-da1f-416b-9bfc-692f08fb6957
description: "NuGet 3.4.2 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。"
keywords: "NuGet 3.4.2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6761c59b6dc85b9a8503041928c2707549006d9c
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="3ec11-104">NuGet 3.4.2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="3ec11-104">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="3ec11-105">[NuGet 3.4.1 リリース ノート](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 リリース ノート](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="3ec11-105">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="3ec11-106">NuGet 3.4.2 は 2016 年 4 月 8 日、3.4 および 3.4.1 で識別されたいくつかの問題を解決するにリリースされたリリースします。</span><span class="sxs-lookup"><span data-stu-id="3ec11-106">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="3ec11-107">nuget.exe 3.4.2 RC が利用できるようになりました</span><span class="sxs-lookup"><span data-stu-id="3ec11-107">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="3ec11-108">Nuget.exe 3.4.2 のリリース候補版をダウンロードする[ここ](https://dist.nuget.org/index.html)です。</span><span class="sxs-lookup"><span data-stu-id="3ec11-108">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="3ec11-109">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="3ec11-109">Updates and Improvements</span></span>

* <span data-ttu-id="3ec11-110">特定のシナリオ、詳細な依存関係グラフを使用してパッケージで更新プログラムが非常に長い時間がかかりし、Visual Studio のハング状態にある更新プログラムのパフォーマンスを大幅に改善おが。</span><span class="sxs-lookup"><span data-stu-id="3ec11-110">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="3ec11-111">ネットワーク トラフィックがない nuget の復元は 2.5 ~ x 3 Visual Studio 内で高速です。</span><span class="sxs-lookup"><span data-stu-id="3ec11-111">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="3ec11-112">この変更だけでなくおが問題を修正できるほか、VS UI 内の数、更新プログラムをフェッチするときに 2 回に、ネットワークにヒットされたお。</span><span class="sxs-lookup"><span data-stu-id="3ec11-112">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="3ec11-113">これが部分的に 3.4/3.4.1 の経験豊富ないくつかのタイムアウトの問題顧客を担当します。</span><span class="sxs-lookup"><span data-stu-id="3ec11-113">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="3ec11-114">No_proxy 設定のサポートが追加されました</span><span class="sxs-lookup"><span data-stu-id="3ec11-114">Added support for no_proxy setting</span></span>

##<a name="fixes"></a><span data-ttu-id="3ec11-115">修正プログラム</span><span class="sxs-lookup"><span data-stu-id="3ec11-115">Fixes</span></span>

* <span data-ttu-id="3ec11-116">Nuget.org のソースがある NuGet 設定または config で不足している 3.4.1 に更新した後、問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="3ec11-116">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="3ec11-117">問題を修正、FindPackagesById 3.4.1 で大文字と小文字の変更が Artifactory を中断します。</span><span class="sxs-lookup"><span data-stu-id="3ec11-117">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="3ec11-118">FIPS nuget.exe と NuGet の復元に失敗の原因となった問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="3ec11-118">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="3ec11-119">[無効] アイコンの URL を使用してソースを参照するときに、クラッシュを修正しました。</span><span class="sxs-lookup"><span data-stu-id="3ec11-119">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="3ec11-120">バージョンと 'すべてのソース' からエントリを結合すると問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="3ec11-120">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="3ec11-121">3.4.2 で既知の問題 Windows x86 Commandline (RC)</span><span class="sxs-lookup"><span data-stu-id="3ec11-121">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="3ec11-122">RTM に達する前に初期の次の週に、これらの問題が修正されます。</span><span class="sxs-lookup"><span data-stu-id="3ec11-122">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="3ec11-123">ソリューション ファイルがプロジェクト ファイルよりも下のフォルダー階層内に配置されている場合、ソリューションを実行している nuget の復元は失敗します。</span><span class="sxs-lookup"><span data-stu-id="3ec11-123">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="3ec11-124">V2 のフィードを使用してパッケージで nuget delete コマンドを実行は失敗します。</span><span class="sxs-lookup"><span data-stu-id="3ec11-124">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="3ec11-125">V3 フィードを使用してください。</span><span class="sxs-lookup"><span data-stu-id="3ec11-125">Use V3 feed instead.</span></span>


<span data-ttu-id="3ec11-126">、修正し、このリリースの機能強化の完全な一覧を確認して問題の一覧[ここ](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)です。</span><span class="sxs-lookup"><span data-stu-id="3ec11-126">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>