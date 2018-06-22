---
title: NuGet 3.2.1 リリース ノート
description: NuGet 3.2.1 などのリリース ノートには、問題、バグの修正、追加された機能、および Dcr が知られています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 039fabaaacfdffd76fa88ff8183548e97cd4719b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31820145"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="59e93-103">NuGet 3.2.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="59e93-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="59e93-104">[NuGet 3.2 リリース ノート](../release-notes/nuget-3.2.md) | [NuGet 3.3 リリース ノート](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="59e93-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="59e93-105">コマンドラインの NuGet 3.2.1 リリースのほんの一部の最適化と 3.2 のリリースの修正された、2015 年 10 月 12日から[dist.nuget.org](http://dist.nuget.org/index.html)です。</span><span class="sxs-lookup"><span data-stu-id="59e93-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="59e93-106">機能強化</span><span class="sxs-lookup"><span data-stu-id="59e93-106">Improvements</span></span>

* <span data-ttu-id="59e93-107">NuGet は、元の大文字と小文字の構成ファイルを使用するようになりました`NuGet.Config`です。</span><span class="sxs-lookup"><span data-stu-id="59e93-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="59e93-108">これは、大文字小文字を区別のオペレーティング システムで重要[1427](https://github.com/NuGet/Home/issues/1427)</span><span class="sxs-lookup"><span data-stu-id="59e93-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="59e93-109">NuGet の復元は dnx プロジェクトを無視するようになりました (`*.xproj`) で処理する必要があります`dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="59e93-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="59e93-110">使用する場合は、ネットワーク使用率を最適化`index.json`登録データをパッケージ化と[1426](https://github.com/NuGet/Home/issues/1426)</span><span class="sxs-lookup"><span data-stu-id="59e93-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="59e93-111">処理 v2 サービスでより堅牢に強化されたリソースのダウンロード[1448](https://github.com/NuGet/Home/issues/1448)</span><span class="sxs-lookup"><span data-stu-id="59e93-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="59e93-112">修正プログラム</span><span class="sxs-lookup"><span data-stu-id="59e93-112">Fixes</span></span>

* <span data-ttu-id="59e93-113">NuGet の更新プログラムが正しく更新`.csproj` / `.vcxproj`参照[1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="59e93-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="59e93-114">今すぐローカル .nuget フォルダーを SpecialFolders.UserProfile が見つからないときに作成して妨げて[1531](https://github.com/NuGet/Home/issues/1531)</span><span class="sxs-lookup"><span data-stu-id="59e93-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="59e93-115">処理がダウンロード中に破損しているローカル キャッシュ内でのパッケージの強化[1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="59e93-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="59e93-116">コマンドラインと Visual Studio の拡張機能は含まれて NuGet GitHub の課題の完全な一覧[3.2.1 マイルス トーン](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="59e93-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="59e93-117">既知の問題</span><span class="sxs-lookup"><span data-stu-id="59e93-117">Known Issues</span></span>

<span data-ttu-id="59e93-118">あることができます、GitHub の問題一覧上の問題を追跡するために続行します。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="59e93-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>