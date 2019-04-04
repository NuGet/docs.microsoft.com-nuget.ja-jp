---
title: NuGet 3.4 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.4 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551192"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="d89cc-103">NuGet 3.4 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="d89cc-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="d89cc-104">[NuGet 3.4 RC リリース ノート](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 リリース ノート](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="d89cc-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="d89cc-105">NuGet 3.4 では、Visual Studio 2015 Update 2 と Visual Studio 15 Preview リリースの一部として、2016 年 3 月 30 日にリリースされ、心でいくつかの基本思想付きでビルドされました。</span><span class="sxs-lookup"><span data-stu-id="d89cc-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="d89cc-106">クロス プラットフォームのサポート</span><span class="sxs-lookup"><span data-stu-id="d89cc-106">Cross-Platform support</span></span>
* <span data-ttu-id="d89cc-107">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="d89cc-107">Performance improvements</span></span>
* <span data-ttu-id="d89cc-108">UI の軽微な改善</span><span class="sxs-lookup"><span data-stu-id="d89cc-108">Minor UI improvements</span></span>

<span data-ttu-id="d89cc-109">次の機能、RC で以前に追加されたと更新または 3.4 のリリースが完了しました。</span><span class="sxs-lookup"><span data-stu-id="d89cc-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="d89cc-110">新機能</span><span class="sxs-lookup"><span data-stu-id="d89cc-110">New Features</span></span>

* <span data-ttu-id="d89cc-111">Gzip コンテンツ エンコード リポジトリから NuGet クライアントを今すぐサポートします。</span><span class="sxs-lookup"><span data-stu-id="d89cc-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="d89cc-112">Xproj プロジェクトでパッケージから Pdb のサポート</span><span class="sxs-lookup"><span data-stu-id="d89cc-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="d89cc-113">IOS と Android のビルド アクションで contentFiles 要素のサポート</span><span class="sxs-lookup"><span data-stu-id="d89cc-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="d89cc-114">Netstandard および netstandardapp フレームワーク モニカーのサポート</span><span class="sxs-lookup"><span data-stu-id="d89cc-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="d89cc-115">ユーザー インターフェイスの新機能</span><span class="sxs-lookup"><span data-stu-id="d89cc-115">New User Interface Features</span></span>

* <span data-ttu-id="d89cc-116">特に、インストールされている、更新プログラム、および統合 タブで大幅なパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="d89cc-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="d89cc-117">集計の 'すべてのパッケージ ソース' のソースが適切な検索結果のマージに使用</span><span class="sxs-lookup"><span data-stu-id="d89cc-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="d89cc-118">インストールし、更新プログラムのタブがアルファベット順に並べ替えるようになりました</span><span class="sxs-lookup"><span data-stu-id="d89cc-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="d89cc-119">更新を検索できるようにする更新 ボタンの追加</span><span class="sxs-lookup"><span data-stu-id="d89cc-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="d89cc-120">バージョンの一覧の上部にある最新のビルド オプション</span><span class="sxs-lookup"><span data-stu-id="d89cc-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="d89cc-121">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="d89cc-121">Updates and Improvements</span></span>

* <span data-ttu-id="d89cc-122">参照されるパッケージ`project.json`浮動のあるバージョンですべてのビルドでは更新されません。</span><span class="sxs-lookup"><span data-stu-id="d89cc-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="d89cc-123">復元、クリーン、リビルド、または変更されたときにのみを更新する代わりに、`project.json`します。</span><span class="sxs-lookup"><span data-stu-id="d89cc-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="d89cc-124">nuget.org リポジトリ ソースを NuGet 構成 UI を使用すると、不要になったプロジェクト構成に求められます。</span><span class="sxs-lookup"><span data-stu-id="d89cc-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="d89cc-125">不要になった NuGet では、共有プロジェクトでパッケージを復元もロック ファイルを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="d89cc-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="d89cc-126">私たちは、ネットワーク障害を改善しました、到達できないか、応答に低速のサーバーの処理を再試行してください。</span><span class="sxs-lookup"><span data-stu-id="d89cc-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="d89cc-127">Visual Studio パッケージ マネージャー UI では、キーボードとマウスの動作が向上しました。</span><span class="sxs-lookup"><span data-stu-id="d89cc-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="d89cc-128">最新のサポート`project.json`DNX 内のスキーマ。</span><span class="sxs-lookup"><span data-stu-id="d89cc-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="d89cc-129">互換性に影響する変更点</span><span class="sxs-lookup"><span data-stu-id="d89cc-129">Breaking Changes</span></span>

* <span data-ttu-id="d89cc-130">パッケージのバージョン番号が、形式に正規化されるようになりました*メジャー*.*マイナー*.*パッチ*-*プレリリース*それぞれのメジャー、マイナー、および修正プログラムは整数として扱われ、先頭に 0 を削除します。</span><span class="sxs-lookup"><span data-stu-id="d89cc-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="d89cc-131">プレリリース情報は、文字列として扱うし、して変更は適用されません。</span><span class="sxs-lookup"><span data-stu-id="d89cc-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="d89cc-132">これらの数値は、NuGet クライアントと、nuget.org のサービスによって提供される検索でクエリで使用されます。</span><span class="sxs-lookup"><span data-stu-id="d89cc-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="d89cc-133">詳細については、NuGet Docs で参照できます[プレリリース バージョン](../create-packages/prerelease-packages.md)します。</span><span class="sxs-lookup"><span data-stu-id="d89cc-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="d89cc-134">既知の問題</span><span class="sxs-lookup"><span data-stu-id="d89cc-134">Known Issues</span></span>

* <span data-ttu-id="d89cc-135">**問題:** 問題も Visual Studio のクラッシュなど Visual Studio で Powershell を使用した次のシナリオで Windows 10 v1511 ユーザーが発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d89cc-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="d89cc-136">インストール/install.ps1 のパッケージをアンインストール/uninstall.ps1 スクリプト</span><span class="sxs-lookup"><span data-stu-id="d89cc-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="d89cc-137">Init.ps1 スクリプトを (EntityFramework) のようなプロジェクトの読み込み</span><span class="sxs-lookup"><span data-stu-id="d89cc-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="d89cc-138">Web コンテンツの発行</span><span class="sxs-lookup"><span data-stu-id="d89cc-138">Publishing web content</span></span>

* <span data-ttu-id="d89cc-139">**回避策:** Windows 10 のインストールが最新のパッチ適用、expecially (KB 情報 3124263) 2016 年 1 月、または以降の更新プログラムがあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="d89cc-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="d89cc-140">詳細についてで使用できる[GitHub 問題 #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="d89cc-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="d89cc-141">**問題:** NuGet v2 プロトコル リダイレクトが壊れています。</span><span class="sxs-lookup"><span data-stu-id="d89cc-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="d89cc-142">要求を代替ホストにリダイレクトするカスタム NuGet リポジトリが、リダイレクト要求を行いません。</span><span class="sxs-lookup"><span data-stu-id="d89cc-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="d89cc-143">**回避策:** この問題を回避するには、リダイレクトされたサーバーの場所を指す設定でパッケージ リポジトリ URI を構成します。</span><span class="sxs-lookup"><span data-stu-id="d89cc-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="d89cc-144">詳細については、[GitHub プル要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d89cc-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="d89cc-145">GitHub の問題一覧上の問題を追跡するために引き続き。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="d89cc-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>