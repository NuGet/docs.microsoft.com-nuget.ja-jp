---
title: NuGet 3.4.2 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780248"
---
# <a name="nuget-342-release-notes"></a><span data-ttu-id="a7ee0-103">NuGet 3.4.2 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="a7ee0-103">NuGet 3.4.2 Release Notes</span></span>

<span data-ttu-id="a7ee0-104">[NuGet 3.4.1 のリリースノート](../release-notes/nuget-3.4.1.md)  | [NuGet 3.4.3 のリリースノート](../release-notes/nuget-3.4.3.md)</span><span class="sxs-lookup"><span data-stu-id="a7ee0-104">[NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3 Release Notes](../release-notes/nuget-3.4.3.md)</span></span>

<span data-ttu-id="a7ee0-105">2016年4月8日にリリースされた NuGet 3.4.2 は、3.4 および3.4.1 リリースで特定されたいくつかの問題に対処しています。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-105">NuGet 3.4.2 was released on April 8, 2016 to address several issues that were identified in the 3.4 and 3.4.1 release.</span></span>

## <a name="nugetexe-342-rc-is-now-available"></a><span data-ttu-id="a7ee0-106">nuget.exe 3.4.2 RC を使用できるようになりました</span><span class="sxs-lookup"><span data-stu-id="a7ee0-106">nuget.exe 3.4.2 RC is now available</span></span>

<span data-ttu-id="a7ee0-107">nuget.exe 3.4.2 のリリース候補は [こちら](https://dist.nuget.org/index.html)からダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-107">You can download the release candidate of nuget.exe 3.4.2 [here](https://dist.nuget.org/index.html).</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="a7ee0-108">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="a7ee0-108">Updates and Improvements</span></span>

* <span data-ttu-id="a7ee0-109">特定のシナリオにおける更新のパフォーマンスが大幅に改善されました。深い依存関係グラフを含むパッケージの更新には、非常に長い時間がかかり、Visual Studio がハングしました。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-109">We have significantly improved the performance of updates in a specific scenario, where updates on packages with deep dependency graphs took a really long time and hung Visual Studio.</span></span>
* <span data-ttu-id="a7ee0-110">ネットワークトラフィックのない nuget の復元は、Visual Studio 内で 2.5 x ~ 3 倍高速になります。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-110">nuget restore without network traffic is 2.5x – 3x faster within Visual Studio.</span></span>
* <span data-ttu-id="a7ee0-111">この変更に加えて、VS UI で更新数をフェッチするときに2回ネットワークに到達したという問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-111">In addition to this change, we have fixed an issue where we were hitting the network twice when fetching the update count in the VS UI.</span></span> <span data-ttu-id="a7ee0-112">これは、3.4/3.4.1 で発生したいくつかのタイムアウト問題を部分的に担当していました。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-112">This was partially responsible for some timeout issues customers experienced in 3.4/3.4.1.</span></span>
* <span data-ttu-id="a7ee0-113">No_proxy 設定のサポートを追加しました</span><span class="sxs-lookup"><span data-stu-id="a7ee0-113">Added support for no_proxy setting</span></span>

## <a name="fixes"></a><span data-ttu-id="a7ee0-114">修正</span><span class="sxs-lookup"><span data-stu-id="a7ee0-114">Fixes</span></span>

* <span data-ttu-id="a7ee0-115">3.4.1 に更新した後、nuget.org source が NuGet の設定または config にない問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-115">Fixed an issue where nuget.org source was missing in NuGet settings or config after updating to 3.4.1.</span></span>
* <span data-ttu-id="a7ee0-116">3.4.1 で FindPackagesById の大文字と小文字の変更が発生した場合の問題を修正します。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-116">Fixed an issue where a casing change to FindPackagesById in 3.4.1 breaks Artifactory.</span></span>
* <span data-ttu-id="a7ee0-117">nuget.exe による NuGet の復元でエラーが発生した FIPS の問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-117">Corrected an issue with FIPS that caused failures with NuGet restore with nuget.exe.</span></span>
* <span data-ttu-id="a7ee0-118">無効なアイコンの URL を使用してソースを参照するときのクラッシュを修正します。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-118">Fixed a crash when browsing sources with invalid icon URL.</span></span>
* <span data-ttu-id="a7ee0-119">' すべてのソース ' からのバージョンとエントリのマージに関する問題を修正しています。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-119">Fixed issues with merging versions and entries from 'All Sources'.</span></span>

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a><span data-ttu-id="a7ee0-120">3.4.2 Windows x86 コマンドライン (RC) の既知の問題</span><span class="sxs-lookup"><span data-stu-id="a7ee0-120">Known Issues in 3.4.2 Windows x86 Commandline (RC)</span></span>

<span data-ttu-id="a7ee0-121">これらの問題は、RTM に達する前に、次の週の前に修正されます。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-121">These issues will be fixed early next week before we hit RTM.</span></span>

*  <span data-ttu-id="a7ee0-122">ソリューションファイルがプロジェクトファイルよりも下位のフォルダー階層に配置されている場合、ソリューションで nuget の復元を実行することはできません。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-122">Running nuget restore on a solution will fail if the solution file is placed in a lower folder hierarchy than the project files.</span></span>
*  <span data-ttu-id="a7ee0-123">V2 フィードを使用してパッケージで nuget delete コマンドを実行すると、失敗します。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-123">Running nuget delete command on a package using the V2 feed will fail.</span></span> <span data-ttu-id="a7ee0-124">代わりに V3 フィードを使用します。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-124">Use V3 feed instead.</span></span>


<span data-ttu-id="a7ee0-125">このリリースの修正プログラムと機能強化の完全な一覧については、 [ここ](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)で問題の一覧を確認してください。</span><span class="sxs-lookup"><span data-stu-id="a7ee0-125">For the complete list of fixes and improvements in this release, check out the list of issues [here](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).</span></span>