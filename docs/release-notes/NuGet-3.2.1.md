---
title: NuGet 3.2.1 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.2.1 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776516"
---
# <a name="nuget-321-release-notes"></a><span data-ttu-id="87136-103">NuGet 3.2.1 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="87136-103">NuGet 3.2.1 Release Notes</span></span>

<span data-ttu-id="87136-104">[NuGet 3.2 リリースノート](../release-notes/nuget-3.2.md)  | [NuGet 3.3 リリースノート](../release-notes/nuget-3.3.md)</span><span class="sxs-lookup"><span data-stu-id="87136-104">[NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md) | [NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md)</span></span>

<span data-ttu-id="87136-105">コマンドラインの NuGet 3.2.1 は2015年10月12日にリリースされ、3.2 リリースのいくつかの最適化と修正が行われており、 [dist.nuget.org](http://dist.nuget.org/index.html)から入手できます。</span><span class="sxs-lookup"><span data-stu-id="87136-105">NuGet 3.2.1 for the command-line was released October 12, 2015 with a handful of optimizations and fixes for the 3.2 release and is available from [dist.nuget.org](http://dist.nuget.org/index.html).</span></span>

## <a name="improvements"></a><span data-ttu-id="87136-106">改善</span><span class="sxs-lookup"><span data-stu-id="87136-106">Improvements</span></span>

* <span data-ttu-id="87136-107">NuGet では、の元の大文字と小文字の区別に構成ファイルが使用されるようになりました `NuGet.Config` 。</span><span class="sxs-lookup"><span data-stu-id="87136-107">NuGet now uses the configuration file with the original casing of `NuGet.Config`.</span></span>  <span data-ttu-id="87136-108">これは、大文字と小文字を区別するオペレーティングシステム[1427](https://github.com/NuGet/Home/issues/1427)で重要です。</span><span class="sxs-lookup"><span data-stu-id="87136-108">This is important on case-sensitive operating systems [1427](https://github.com/NuGet/Home/issues/1427)</span></span>
* <span data-ttu-id="87136-109">NuGet の復元では、 `*.xproj` 1227 で処理する必要がある dnx プロジェクト () が無視されるようになりました `dnu` [](https://github.com/NuGet/Home/issues/1227)</span><span class="sxs-lookup"><span data-stu-id="87136-109">NuGet restore will now ignore dnx projects (`*.xproj`) that should be processed with `dnu` [1227](https://github.com/NuGet/Home/issues/1227)</span></span>
* <span data-ttu-id="87136-110">`index.json`およびパッケージ登録データ[1426](https://github.com/NuGet/Home/issues/1426)を使用する場合のネットワーク使用率の最適化</span><span class="sxs-lookup"><span data-stu-id="87136-110">Optimized network utilization when working with `index.json` and package registration data [1426](https://github.com/NuGet/Home/issues/1426)</span></span>
* <span data-ttu-id="87136-111">V2 サービス[1448](https://github.com/NuGet/Home/issues/1448)でのより堅牢なリソースダウンロード処理の向上</span><span class="sxs-lookup"><span data-stu-id="87136-111">Improved resource download handling to be more robust with v2 services [1448](https://github.com/NuGet/Home/issues/1448)</span></span>

## <a name="fixes"></a><span data-ttu-id="87136-112">修正</span><span class="sxs-lookup"><span data-stu-id="87136-112">Fixes</span></span>

* <span data-ttu-id="87136-113">NuGet 更新プログラムによる参照の更新 `.csproj` / `.vcxproj` [1483](https://github.com/NuGet/Home/issues/1483)</span><span class="sxs-lookup"><span data-stu-id="87136-113">NuGet update correctly updates `.csproj`/`.vcxproj` references [1483](https://github.com/NuGet/Home/issues/1483)</span></span>
* <span data-ttu-id="87136-114">次に、特別なフォルダーが見つからない場合に、ローカルの nuget フォルダーが作成され[1531](https://github.com/NuGet/Home/issues/1531)ないようにします。</span><span class="sxs-lookup"><span data-stu-id="87136-114">Now preventing a local .nuget folder from being created when a SpecialFolders.UserProfile cannot be located [1531](https://github.com/NuGet/Home/issues/1531)</span></span>
* <span data-ttu-id="87136-115">ダウンロード中に破損したローカルキャッシュ内のパッケージの処理の改善 [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span><span class="sxs-lookup"><span data-stu-id="87136-115">Improved handling of packages in local cache that are corrupted during download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)</span></span>

<span data-ttu-id="87136-116">コマンドラインと Visual Studio 拡張機能で解決される問題の完全な一覧については、「NuGet GitHub [3.2.1 マイルストーン](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="87136-116">A complete list of issues addressed for the command-line and Visual Studio extension can be found in the NuGet GitHub [3.2.1 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)</span></span>

## <a name="known-issues"></a><span data-ttu-id="87136-117">既知の問題</span><span class="sxs-lookup"><span data-stu-id="87136-117">Known Issues</span></span>

<span data-ttu-id="87136-118">GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="87136-118">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>