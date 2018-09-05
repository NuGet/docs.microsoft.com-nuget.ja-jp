---
title: NuGet 3.2.1 のリリース ノート
description: などの NuGet 3.2.1 のリリース ノートには、問題、バグの修正、追加機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548191"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="086e3-103">NuGet 3.2.1 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="086e3-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="086e3-104">[NuGet 3.2 リリース ノート](../release-notes/nuget-3.2.md) | [NuGet 3.3 のリリース ノート](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="086e3-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="086e3-105">コマンドラインの NuGet 3.2.1、いくつかの最適化と 3.2 のリリースの修正、2015 年 10 月 12 日にリリースされ、はから利用可能な[dist.nuget.org](http://dist.nuget.org/index.html)します。</span><span class="sxs-lookup"><span data-stu-id="086e3-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="086e3-106">機能強化</span><span class="sxs-lookup"><span data-stu-id="086e3-106">Improvements</span></span>

* <span data-ttu-id="086e3-107">NuGet は、元の大文字小文字の区別を構成ファイルを使用するようになりました`NuGet.Config`します。</span><span class="sxs-lookup"><span data-stu-id="086e3-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="086e3-108">これは大文字のオペレーティング システムで重要な[1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="086e3-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="086e3-109">NuGet の復元は dnx プロジェクトを無視するようになりました (`*.xproj`) で処理する必要があります`dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="086e3-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="086e3-110">使用する場合は、ネットワーク使用率を最適化`index.json`登録データをパッケージ化と[1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="086e3-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="086e3-111">V2 サービスをより堅牢に処理の強化されたリソース ダウンロード[1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="086e3-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="086e3-112">修正プログラム</span><span class="sxs-lookup"><span data-stu-id="086e3-112">Fixes</span></span>

* <span data-ttu-id="086e3-113">NuGet の更新が正しく更新`.csproj` / `.vcxproj`参照[1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="086e3-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="086e3-114">ローカル .nuget フォルダーが見つかりません、SpecialFolders.UserProfile ときに作成されないようにようになりましたこと[1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="086e3-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="086e3-115">ダウンロード中に破損がローカル キャッシュ内でのパッケージの処理を改善[1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="086e3-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="086e3-116">NuGet GitHub で見つかるコマンドラインと Visual Studio の拡張機能に対処された問題の完全な一覧[3.2.1 マイルス トーン](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="086e3-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="086e3-117">既知の問題</span><span class="sxs-lookup"><span data-stu-id="086e3-117">Known Issues</span></span>

<span data-ttu-id="086e3-118">GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="086e3-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>