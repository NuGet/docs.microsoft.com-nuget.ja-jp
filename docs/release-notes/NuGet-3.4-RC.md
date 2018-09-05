---
title: NuGet 3.4 RC リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.4 RC のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546755"
---
# <a name="nuget-34-rc-release-notes"></a><span data-ttu-id="b701d-103">NuGet 3.4 RC リリース ノート</span><span class="sxs-lookup"><span data-stu-id="b701d-103">NuGet 3.4-RC Release Notes</span></span>

<span data-ttu-id="b701d-104">[NuGet 3.3 のリリース ノート](../release-notes/nuget-3.3.md) | [NuGet 3.4 のリリース ノート](../release-notes/nuget-3.4.md)</span><span class="sxs-lookup"><span data-stu-id="b701d-104">[NuGet 3.3 Release Notes](../release-notes/nuget-3.3.md) | [NuGet 3.4 Release Notes](../release-notes/nuget-3.4.md)</span></span>

<span data-ttu-id="b701d-105">NuGet 3.4-RC では、2016 年 3 月 3 日 Visual Studio 2015 Update 2 RC と共にリリースされ、心でいくつかの基本思想付きでビルドされました。</span><span class="sxs-lookup"><span data-stu-id="b701d-105">NuGet 3.4-RC was released March 3, 2016 alongside the Visual Studio 2015 Update 2 RC and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="b701d-106">クロス プラットフォームのサポート</span><span class="sxs-lookup"><span data-stu-id="b701d-106">Cross-Platform support</span></span>
* <span data-ttu-id="b701d-107">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="b701d-107">Performance improvements</span></span>
* <span data-ttu-id="b701d-108">UI の軽微な改善</span><span class="sxs-lookup"><span data-stu-id="b701d-108">Minor UI improvements</span></span>

<span data-ttu-id="b701d-109">次の機能は、複数の 3.4 の最終リリースの計画と、この RC で利用できます。</span><span class="sxs-lookup"><span data-stu-id="b701d-109">The following features are available in this RC, with more planned for the 3.4 final release.</span></span>

## <a name="new-features"></a><span data-ttu-id="b701d-110">新機能</span><span class="sxs-lookup"><span data-stu-id="b701d-110">New Features</span></span>

* <span data-ttu-id="b701d-111">Gzip コンテンツ エンコード リポジトリから NuGet クライアントを今すぐサポートします。</span><span class="sxs-lookup"><span data-stu-id="b701d-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="b701d-112">Xproj プロジェクトでパッケージから Pdb のサポート</span><span class="sxs-lookup"><span data-stu-id="b701d-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="b701d-113">IOS と Android のビルド アクションで contentFiles 要素のサポート</span><span class="sxs-lookup"><span data-stu-id="b701d-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="b701d-114">Netstandard および netstandardapp フレームワーク モニカーのサポート</span><span class="sxs-lookup"><span data-stu-id="b701d-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="b701d-115">ユーザー インターフェイスの新機能</span><span class="sxs-lookup"><span data-stu-id="b701d-115">New User Interface Features</span></span>

* <span data-ttu-id="b701d-116">特に、インストールされている、更新プログラム、および統合 タブで大幅なパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="b701d-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="b701d-117">インストールし、更新プログラムのタブがアルファベット順に並べ替えるようになりました</span><span class="sxs-lookup"><span data-stu-id="b701d-117">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="b701d-118">更新を検索できるようにする更新 ボタンの追加</span><span class="sxs-lookup"><span data-stu-id="b701d-118">Added a Refresh button that allows a search to be refreshed</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="b701d-119">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="b701d-119">Updates and Improvements</span></span>

* <span data-ttu-id="b701d-120">参照されるパッケージ`project.json`浮動のあるバージョンですべてのビルドでは更新されません。</span><span class="sxs-lookup"><span data-stu-id="b701d-120">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="b701d-121">復元、クリーン、リビルド、または変更されたときにのみを更新する代わりに、`project.json`します。</span><span class="sxs-lookup"><span data-stu-id="b701d-121">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="b701d-122">nuget.org リポジトリ ソースを NuGet 構成 UI を使用すると、不要になったプロジェクト構成に求められます。</span><span class="sxs-lookup"><span data-stu-id="b701d-122">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="b701d-123">不要になった NuGet では、共有プロジェクトでパッケージを復元もロック ファイルを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="b701d-123">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="b701d-124">私たちは、ネットワーク障害を改善しました、到達できないか、応答に低速のサーバーの処理を再試行してください。</span><span class="sxs-lookup"><span data-stu-id="b701d-124">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="b701d-125">Visual Studio パッケージ マネージャー UI では、キーボードとマウスの動作が向上しました。</span><span class="sxs-lookup"><span data-stu-id="b701d-125">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="b701d-126">最新のサポート`project.json`DNX 内のスキーマ。</span><span class="sxs-lookup"><span data-stu-id="b701d-126">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="known-issues"></a><span data-ttu-id="b701d-127">既知の問題</span><span class="sxs-lookup"><span data-stu-id="b701d-127">Known Issues</span></span>

<span data-ttu-id="b701d-128">GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="b701d-128">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>