---
title: NuGet 3.4 リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.4 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 794b25e2d81d7a2c297a185bdb34a7cf68535723
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776413"
---
# <a name="nuget-34-release-notes"></a><span data-ttu-id="cb17d-103">NuGet 3.4 リリースノート</span><span class="sxs-lookup"><span data-stu-id="cb17d-103">NuGet 3.4 Release Notes</span></span>

<span data-ttu-id="cb17d-104">[NuGet 3.4-RC リリースノート](../release-notes/nuget-3.4-RC.md)  | [NuGet 3.4.1 のリリースノート](../release-notes/nuget-3.4.1.md)</span><span class="sxs-lookup"><span data-stu-id="cb17d-104">[NuGet 3.4-RC Release Notes](../release-notes/nuget-3.4-RC.md) | [NuGet 3.4.1 Release Notes](../release-notes/nuget-3.4.1.md)</span></span>

<span data-ttu-id="cb17d-105">NuGet 3.4 は、Visual Studio 2015 Update 2 および Visual Studio 15 Preview リリースの一部として2016年3月30日にリリースされ、いくつかの原則に基づいて構築されました。</span><span class="sxs-lookup"><span data-stu-id="cb17d-105">NuGet 3.4 was released March 30, 2016 as part of the Visual Studio 2015 Update 2 and Visual Studio 15 Preview Release and was built with a few tenets in minds:</span></span>

* <span data-ttu-id="cb17d-106">クロスプラットフォームサポート</span><span class="sxs-lookup"><span data-stu-id="cb17d-106">Cross-Platform support</span></span>
* <span data-ttu-id="cb17d-107">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="cb17d-107">Performance improvements</span></span>
* <span data-ttu-id="cb17d-108">UI のマイナー機能強化</span><span class="sxs-lookup"><span data-stu-id="cb17d-108">Minor UI improvements</span></span>

<span data-ttu-id="cb17d-109">RC では、次の機能が以前に追加されており、3.4 リリースで更新または完了しています。</span><span class="sxs-lookup"><span data-stu-id="cb17d-109">The following features were previously added in the RC and have been updated or completed for the 3.4 release:</span></span>

## <a name="new-features"></a><span data-ttu-id="cb17d-110">新機能</span><span class="sxs-lookup"><span data-stu-id="cb17d-110">New Features</span></span>

* <span data-ttu-id="cb17d-111">NuGet クライアントでリポジトリからの gzip コンテンツエンコードがサポートされるようになりました</span><span class="sxs-lookup"><span data-stu-id="cb17d-111">NuGet clients now support gzip content-encoding from repositories</span></span>
* <span data-ttu-id="cb17d-112">Xproj プロジェクトのパッケージからの Pdb のサポート</span><span class="sxs-lookup"><span data-stu-id="cb17d-112">Support for PDBs from packages in xproj projects</span></span>
* <span data-ttu-id="cb17d-113">ContentFiles 要素での iOS および Android ビルドアクションのサポート</span><span class="sxs-lookup"><span data-stu-id="cb17d-113">Support for iOS and Android build actions in the contentFiles element</span></span>
* <span data-ttu-id="cb17d-114">Netstandard.library と netstandardapp フレームワークのモニカーのサポート</span><span class="sxs-lookup"><span data-stu-id="cb17d-114">Support for the netstandard and netstandardapp framework monikers</span></span>

## <a name="new-user-interface-features"></a><span data-ttu-id="cb17d-115">新しいユーザーインターフェイスの機能</span><span class="sxs-lookup"><span data-stu-id="cb17d-115">New User Interface Features</span></span>

* <span data-ttu-id="cb17d-116">インストール、更新、統合の各タブで大幅なパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="cb17d-116">Significant performance improvements especially on the Installed, Updates, and Consolidate tabs</span></span>
* <span data-ttu-id="cb17d-117">集計 ' すべてのパッケージソース ' ソースは、適切な検索結果のマージで使用できます</span><span class="sxs-lookup"><span data-stu-id="cb17d-117">Aggregate 'All Package Sources' Source is available with proper search result merging</span></span>
* <span data-ttu-id="cb17d-118">インストールおよび更新のタブがアルファベット順に並べ替えられるようになりました。</span><span class="sxs-lookup"><span data-stu-id="cb17d-118">Installed and Updates tabs are now sorted alphabetically</span></span>
* <span data-ttu-id="cb17d-119">検索を更新するための更新ボタンを追加しました</span><span class="sxs-lookup"><span data-stu-id="cb17d-119">Added a Refresh button that allows a search to be refreshed</span></span>
* <span data-ttu-id="cb17d-120">バージョン一覧の先頭にある最新のビルドオプション</span><span class="sxs-lookup"><span data-stu-id="cb17d-120">Latest Build options at the top of the Version list</span></span>

## <a name="updates-and-improvements"></a><span data-ttu-id="cb17d-121">更新プログラムと機能強化</span><span class="sxs-lookup"><span data-stu-id="cb17d-121">Updates and Improvements</span></span>

* <span data-ttu-id="cb17d-122">`project.json`浮動バージョンを持つで参照されるパッケージは、すべてのビルドで更新されません。</span><span class="sxs-lookup"><span data-stu-id="cb17d-122">Packages referenced in `project.json` that have a floating version will not update on every build.</span></span> <span data-ttu-id="cb17d-123">代わりに、復元、クリーン、リビルド、または変更を強制した場合にのみ更新され `project.json` ます。</span><span class="sxs-lookup"><span data-stu-id="cb17d-123">Instead, they will update only when forced to restore, clean, rebuild, or modify `project.json`.</span></span>
* <span data-ttu-id="cb17d-124">NuGet 構成 UI を使用する場合、nuget.org リポジトリソースはプロジェクト構成に強制されなくなりました。</span><span class="sxs-lookup"><span data-stu-id="cb17d-124">nuget.org repository sources are no longer forced into a project configuration when you use the NuGet configuration UI.</span></span>
* <span data-ttu-id="cb17d-125">NuGet では、共有プロジェクトのパッケージが復元されず、ロックファイルも書き込まれなくなりました。</span><span class="sxs-lookup"><span data-stu-id="cb17d-125">NuGet no longer restores packages in shared projects nor writes a lock file.</span></span>
* <span data-ttu-id="cb17d-126">ネットワークエラーを改善し、到達不能または応答の遅いサーバーの処理を再試行しました。</span><span class="sxs-lookup"><span data-stu-id="cb17d-126">We've improved network failure and retry handling for unreachable or slow-to-respond servers.</span></span>
* <span data-ttu-id="cb17d-127">Visual Studio パッケージマネージャーの UI では、キーボードとマウスの動作が改善されています。</span><span class="sxs-lookup"><span data-stu-id="cb17d-127">Keyboard and mouse behaviors are improved in the Visual Studio Package Manager UI.</span></span>
* <span data-ttu-id="cb17d-128">DNX の最新のスキーマがサポートされるようになりました `project.json` 。</span><span class="sxs-lookup"><span data-stu-id="cb17d-128">We now support the latest `project.json` schema in DNX.</span></span>

## <a name="breaking-changes"></a><span data-ttu-id="cb17d-129">重大な変更</span><span class="sxs-lookup"><span data-stu-id="cb17d-129">Breaking Changes</span></span>

* <span data-ttu-id="cb17d-130">パッケージのバージョン番号が *major* の形式に正規化されました。*minor*。*修正プログラム* -*プレリリース*  メジャー、マイナー、およびパッチはそれぞれ整数として扱われ、先頭のゼロは削除されます。</span><span class="sxs-lookup"><span data-stu-id="cb17d-130">Package version numbers are now normalized to the format *major*.*minor*.*patch*-*prerelease*   Each of major, minor, and patch are treated as integers and drop any leading zeroes.</span></span>  <span data-ttu-id="cb17d-131">プレリリース情報は文字列として扱われ、変更は適用されません。</span><span class="sxs-lookup"><span data-stu-id="cb17d-131">The prerelease information is treated as a string and no changes are applied to it.</span></span> <span data-ttu-id="cb17d-132">これらの数値は、NuGet クライアントによるクエリと、nuget.org サービスによって提供される検索で使用されます。</span><span class="sxs-lookup"><span data-stu-id="cb17d-132">These numbers are used in queries by the NuGet clients and the search provided by the nuget.org service.</span></span>  <span data-ttu-id="cb17d-133">詳細については、NuGet のドキュメント ( [プレリリース版](../create-packages/prerelease-packages.md)) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cb17d-133">More details can be found in the NuGet Docs under [Prerelease Versions](../create-packages/prerelease-packages.md).</span></span>

## <a name="known-issues"></a><span data-ttu-id="cb17d-134">既知の問題</span><span class="sxs-lookup"><span data-stu-id="cb17d-134">Known Issues</span></span>

* <span data-ttu-id="cb17d-135">**問題:** 次のシナリオでは、Windows 10 バージョン1511ユーザーが Visual Studio で Powershell を使用して問題を発生させるか、Visual Studio をクラッシュさせる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="cb17d-135">**Issue:** Windows 10 v1511 users may experience issues or even a Visual Studio crash with Powershell in Visual Studio in the following scenarios:</span></span>
    * <span data-ttu-id="cb17d-136">install.ps1/uninstall.ps1 スクリプトを含むパッケージのインストール/アンインストール</span><span class="sxs-lookup"><span data-stu-id="cb17d-136">Installing / Uninstalling packages that have install.ps1 / uninstall.ps1 scripts</span></span>
    * <span data-ttu-id="cb17d-137">init.ps1 スクリプトを含むプロジェクトの読み込み (EntityFramework など)</span><span class="sxs-lookup"><span data-stu-id="cb17d-137">Loading projects that have an init.ps1 script (like EntityFramework)</span></span>
    * <span data-ttu-id="cb17d-138">Web コンテンツの発行</span><span class="sxs-lookup"><span data-stu-id="cb17d-138">Publishing web content</span></span>

* <span data-ttu-id="cb17d-139">**回避策:** Windows 10 のインストールに最新のパッチが適用されていることを確認してください。2016年1月 (KB 3124263) 以降の更新プログラムが適用されます。</span><span class="sxs-lookup"><span data-stu-id="cb17d-139">**Workaround:** Ensure that your Windows 10 install has the latest patches applied, expecially the January 2016 (KB 3124263) or a later update.</span></span>  <span data-ttu-id="cb17d-140">詳細については、 [GitHub の問題](http://github.com/nuget/home/issues/1638)を参照してください #1638</span><span class="sxs-lookup"><span data-stu-id="cb17d-140">More details are available on [GitHub issue #1638](http://github.com/nuget/home/issues/1638)</span></span>

* <span data-ttu-id="cb17d-141">**問題:** NuGet v2 プロトコル リダイレクトが壊れています。</span><span class="sxs-lookup"><span data-stu-id="cb17d-141">**Issue:** NuGet v2 protocol redirects are broken.</span></span>
<span data-ttu-id="cb17d-142">要求を代替ホストにリダイレクトするカスタム NuGet リポジトリが、リダイレクト要求を行いません。</span><span class="sxs-lookup"><span data-stu-id="cb17d-142">Custom NuGet repositories that redirect requests to an alternative host do not honor the redirect request.</span></span>
* <span data-ttu-id="cb17d-143">**回避策:**  この問題を回避するには、リダイレクトされたサーバーの場所を指すように [設定] でパッケージリポジトリの URI を構成します。</span><span class="sxs-lookup"><span data-stu-id="cb17d-143">**Workaround:**  To work around this issue, configure the package repository URI in settings to point to the redirected server location.</span></span>
<span data-ttu-id="cb17d-144">詳細については、「 [GitHub プル要求 #387](https://github.com/NuGet/NuGet.Client/pull/387)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cb17d-144">For more information, see [GitHub pull request #387](https://github.com/NuGet/NuGet.Client/pull/387).</span></span>

<span data-ttu-id="cb17d-145">GitHub の問題の一覧に関する問題は、引き続き次の場所にあります。 [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="cb17d-145">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>