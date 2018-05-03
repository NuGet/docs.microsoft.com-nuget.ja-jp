---
title: NuGet 3.4 リリース ノート
description: NuGet 3.4 が既知の問題、バグの修正、追加された機能は、Dcr などのリリース ノートします。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 3f2a945b628022bdcc6e69a7a4b1be6c53b65626
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="03a31-103">NuGet 3.4 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="03a31-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="03a31-104">[NuGet 3.4 RC のリリース ノート](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 リリース ノート](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="03a31-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="03a31-105">NuGet 3.4 機は、Visual Studio 2015 Update 2 と Visual Studio 15 Preview リリースの一部として、2016 年 3 月 30 日がリリースされ、心にいくつかの基本思想でビルドされました。</span><span class="sxs-lookup"><span data-stu-id="03a31-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="03a31-106">クロスプラット フォーム サポート</span><span class="sxs-lookup"><span data-stu-id="03a31-106">Cross-Platform support</span></span>
* <span data-ttu-id="03a31-107">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="03a31-107">Performance improvements</span></span>
* <span data-ttu-id="03a31-108">マイナーの UI 機能強化</span><span class="sxs-lookup"><span data-stu-id="03a31-108">Minor UI improvements</span></span>

<span data-ttu-id="03a31-109">次の機能 RC で以前に追加されたと更新またはされた 3.4 のリリースでは、完了しました。</span><span class="sxs-lookup"><span data-stu-id="03a31-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="03a31-110">新機能</span><span class="sxs-lookup"><span data-stu-id="03a31-110">New Features</span></span>

* <span data-ttu-id="03a31-111">NuGet クライアント サポート gzip コンテンツ エンコード リポジトリから</span><span class="sxs-lookup"><span data-stu-id="03a31-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="03a31-112">Xproj プロジェクトでパッケージから Pdb のサポート</span><span class="sxs-lookup"><span data-stu-id="03a31-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="03a31-113">IOS および Android のビルド アクション contentFiles 要素でのサポート</span><span class="sxs-lookup"><span data-stu-id="03a31-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="03a31-114">Netstandard および netstandardapp フレームワーク モニカーのサポート</span><span class="sxs-lookup"><span data-stu-id="03a31-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="03a31-115">新しいユーザー インターフェイスの機能</span><span class="sxs-lookup"><span data-stu-id="03a31-115">New User Interface Features</span></span>

* <span data-ttu-id="03a31-116">特に、インストール、更新、および統合のタブ上の大幅なパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="03a31-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="03a31-117">集計の 'すべてのパッケージ ソース' ソースを適切な検索結果の結合を使用</span><span class="sxs-lookup"><span data-stu-id="03a31-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="03a31-118">インストールされているし、更新プログラムのタブがアルファベット順に並べ替えられました</span><span class="sxs-lookup"><span data-stu-id="03a31-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="03a31-119">更新する検索を許可する更新 ボタンの追加</span><span class="sxs-lookup"><span data-stu-id="03a31-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="03a31-120">バージョンのリストの上部にある最新のビルド オプション</span><span class="sxs-lookup"><span data-stu-id="03a31-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="03a31-121">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="03a31-121">Updates and Improvements</span></span>

* <span data-ttu-id="03a31-122">パッケージで参照されている`project.json`浮動があるすべてのビルドでバージョンは更新されません。</span><span class="sxs-lookup"><span data-stu-id="03a31-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="03a31-123">強制復元、クリーン、再構築、または変更する場合にのみを更新する代わりに、`project.json`です。</span><span class="sxs-lookup"><span data-stu-id="03a31-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="03a31-124">nuget.org のリポジトリ ソースを NuGet 構成 UI を使用するときに、不要になったプロジェクト構成に求められます。</span><span class="sxs-lookup"><span data-stu-id="03a31-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="03a31-125">不要になった NuGet は、共有プロジェクトでパッケージを復元も、ロック ファイルを書き込みます。</span><span class="sxs-lookup"><span data-stu-id="03a31-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="03a31-126">ネットワーク障害を改良しましたし、到達できないか、応答に低速のサーバーの処理を再試行してください。</span><span class="sxs-lookup"><span data-stu-id="03a31-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="03a31-127">Visual Studio のパッケージ マネージャーの UI では、キーボードとマウスの動作が強化されています。</span><span class="sxs-lookup"><span data-stu-id="03a31-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="03a31-128">最新のサポート`project.json`DNX 内のスキーマです。</span><span class="sxs-lookup"><span data-stu-id="03a31-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="03a31-129">互換性に影響する変更点</span><span class="sxs-lookup"><span data-stu-id="03a31-129">Breaking Changes</span></span>

* <span data-ttu-id="03a31-130">パッケージのバージョン番号が、形式に正規化されたようになりました*メジャー*.*マイナー*.*修正プログラム*-*プレリリース*のメジャー、マイナー、し、修正プログラムは整数として扱われ、すべて先頭に 0 を削除します。</span><span class="sxs-lookup"><span data-stu-id="03a31-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="03a31-131">プレリリース情報が文字列として扱われに変更は適用されません。</span><span class="sxs-lookup"><span data-stu-id="03a31-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="03a31-132">これらの番号は、NuGet クライアントおよび nuget.org サービスによって指定された検索クエリで使用されます。</span><span class="sxs-lookup"><span data-stu-id="03a31-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="03a31-133">詳細については、NuGet のドキュメントを参照できます[プレリリース バージョン](../create-packages/prerelease-packages.md)します。</span><span class="sxs-lookup"><span data-stu-id="03a31-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="03a31-134">既知の問題</span><span class="sxs-lookup"><span data-stu-id="03a31-134">Known Issues</span></span>

* <span data-ttu-id="03a31-135">**問題点:** v1511 ユーザーの Windows 10 の問題またはでも Visual Studio でクラッシュが Visual Studio での Powershell で、次のシナリオが適用される場合があります。</span><span class="sxs-lookup"><span data-stu-id="03a31-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="03a31-136">インストール/install.ps1 をされているパッケージをアンインストールする/uninstall.ps1 スクリプト</span><span class="sxs-lookup"><span data-stu-id="03a31-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="03a31-137">Init.ps1 スクリプト (EntityFramework) のように既にあるプロジェクトの読み込み</span><span class="sxs-lookup"><span data-stu-id="03a31-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="03a31-138">Web コンテンツの発行</span><span class="sxs-lookup"><span data-stu-id="03a31-138">Publishing web content</span></span>

* <span data-ttu-id="03a31-139">**回避策:** Windows 10 のインストールが最新のパッチが適用されて、expecially (KB 情報 3124263) 2016 年 1 月、または以降の更新プログラムがあることを確認します。</span><span class="sxs-lookup"><span data-stu-id="03a31-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="03a31-140">詳細についてで使用できる[GitHub 問題 #1638](http://github.com/nuget/home/issues/1638)</span><span class="sxs-lookup"><span data-stu-id="03a31-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="03a31-141">**問題:** NuGet v2 プロトコル リダイレクトが壊れています。</span><span class="sxs-lookup"><span data-stu-id="03a31-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="03a31-142">要求を代替ホストにリダイレクトするカスタム NuGet リポジトリが、リダイレクト要求を行いません。</span><span class="sxs-lookup"><span data-stu-id="03a31-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="03a31-143">**回避策:** この問題を回避するには、リダイレクトされたサーバーの場所を指す設定でパッケージ リポジトリの URI を構成します。</span><span class="sxs-lookup"><span data-stu-id="03a31-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="03a31-144">詳細については、次を参照してください。 [GitHub プル要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)です。</span><span class="sxs-lookup"><span data-stu-id="03a31-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="03a31-145">あることができます、GitHub の問題一覧上の問題を追跡するために続行します。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="03a31-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>