---
title: NuGet 5.10 リリース ノート
description: 新機能、バグ修正、DCRs など、NuGet 5.10 のリリース ノート。
author: zkat
ms.author: kmarchan
ms.date: 6/11/2021
ms.topic: conceptual
ms.openlocfilehash: 666eda5803b540dc18a9310f61c92dc74ff2089e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112356499"
---
# <a name="nuget-510-release-notes"></a><span data-ttu-id="f0bd8-103">NuGet 5.10 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="f0bd8-103">NuGet 5.10 Release Notes</span></span>

<span data-ttu-id="f0bd8-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="f0bd8-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f0bd8-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="f0bd8-105">NuGet version</span></span> | <span data-ttu-id="f0bd8-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="f0bd8-106">Available in Visual Studio version</span></span> | <span data-ttu-id="f0bd8-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f0bd8-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="f0bd8-108">**5.10.0**</span><span class="sxs-lookup"><span data-stu-id="f0bd8-108">**5.10.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f0bd8-109">Visual Studio 2019 バージョン 16.10</span><span class="sxs-lookup"><span data-stu-id="f0bd8-109">Visual Studio 2019 version 16.10</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f0bd8-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f0bd8-110">[5.0.300](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="f0bd8-111"><sup>1</sup> .NET Core ワークロードVisual Studio 2019 でインストール済み</span><span class="sxs-lookup"><span data-stu-id="f0bd8-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="f0bd8-112">Visual Studio 16.10、MSBuild 16.10、および .NET 5.0.300 以降では、NuGet.exe 5.10 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-112">Visual Studio 16.10, MSBuild 16.10, and .NET 5.0.300+ requires NuGet.exe 5.10 or later.</span></span>

## <a name="summary-whats-new-in-510"></a><span data-ttu-id="f0bd8-113">概要: 5.10 の新機能</span><span class="sxs-lookup"><span data-stu-id="f0bd8-113">Summary: What's New in 5.10</span></span>

* <span data-ttu-id="f0bd8-114">署名: dotnet trusted-signers コマンドを実装する - [#8053](https://github.com/NuGet/Home/issues/8053)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-114">Signing: implement dotnet trusted-signers command - [#8053](https://github.com/NuGet/Home/issues/8053)</span></span>

* <span data-ttu-id="f0bd8-115">Linux では既定の検証を無効にし、Windows では既定[で有効にする](https://github.com/NuGet/Home/issues/10713)- #10713</span><span class="sxs-lookup"><span data-stu-id="f0bd8-115">Make default validation disabled on Linux, but enabled by default on Windows - [#10713](https://github.com/NuGet/Home/issues/10713)</span></span>

* <span data-ttu-id="f0bd8-116">.NET 5+ Linux/MAC でパッケージ署名検証用の ENV 変数を追加する - [#10742](https://github.com/NuGet/Home/issues/10742)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-116">Add an ENV Variable for Package Signing Verification on .NET 5+ Linux/MAC - [#10742](https://github.com/NuGet/Home/issues/10742)</span></span>

* <span data-ttu-id="f0bd8-117">大規模なソリューションの新しいパッケージのインストールパフォーマンスを向上させる - [#10166](https://github.com/NuGet/Home/issues/10166)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-117">Improve install new package performance for large solutions - [#10166](https://github.com/NuGet/Home/issues/10166)</span></span>

* <span data-ttu-id="f0bd8-118">`nfproj`Nuget CLI でサポートされているProjectExtensions の一覧にプロジェクトの種類を追加します。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-118">Add the project type `nfproj` to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="f0bd8-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-119"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f0bd8-120">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="f0bd8-120">Issues fixed in this release</span></span>

* <span data-ttu-id="f0bd8-121">プロジェクトを <requireLicenseAcceptance> パッキングするときに 要素を抑制[](https://github.com/NuGet/Home/issues/5133)する - #5133</span><span class="sxs-lookup"><span data-stu-id="f0bd8-121">Suppress the <requireLicenseAcceptance> element when packing a project - [#5133](https://github.com/NuGet/Home/issues/5133)</span></span>

* <span data-ttu-id="f0bd8-122">[CPVM] dotnet cli にプレビューの警告が表示される必要があります - [#10226](https://github.com/NuGet/Home/issues/10226)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-122">[CPVM] preview warning should be shown on dotnet cli - [#10226](https://github.com/NuGet/Home/issues/10226)</span></span>

* <span data-ttu-id="f0bd8-123">PMUI の背景色トークンと前景色トークンを CommonDocumentColors [-](https://github.com/NuGet/Home/issues/10608) #10608</span><span class="sxs-lookup"><span data-stu-id="f0bd8-123">Update the background and foreground color tokens of the PMUI to CommonDocumentColors - [#10608](https://github.com/NuGet/Home/issues/10608)</span></span>

* <span data-ttu-id="f0bd8-124">[バグ Bash]PM UI でタブをすばやく切り替えるときにエラー "ユーザーによって取り消された操作" が [エラー一覧] ウィンドウに表示される - [#10671](https://github.com/NuGet/Home/issues/10671)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-124">[Bug Bash] Error “operation canceled by user” show in Error List window when switching between tabs quickly in PM UI - [#10671](https://github.com/NuGet/Home/issues/10671)</span></span>

* <span data-ttu-id="f0bd8-125">PM UI: ソリューション レベルでのパッケージ インストールのパフォーマンスを向上させる - [#10210](https://github.com/NuGet/Home/issues/10210)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-125">PM UI:  Improve package installation performance on the solution level - [#10210](https://github.com/NuGet/Home/issues/10210)</span></span>

* <span data-ttu-id="f0bd8-126">GetService を NuGet.Clients のすべての場所で GetServiceAsync に置き換える - [#3784](https://github.com/NuGet/Home/issues/3784)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-126">Replace GetService with GetServiceAsync everywhere in NuGet.Clients - [#3784](https://github.com/NuGet/Home/issues/3784)</span></span>

* <span data-ttu-id="f0bd8-127">NuGet.exeパスに関するパックパフォーマンス `..` の問題 - [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-127">NuGet.exe pack performance problem with `..` relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>

* <span data-ttu-id="f0bd8-128">"nuget pack" のパフォーマンスは、ソース パスのレベルが上がって低下 [します。#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-128">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>

* <span data-ttu-id="f0bd8-129">重複するファイルを含む nuspec をパッケージ化する場合、NuGet ではエラーが発生しない。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-129">NuGet doesn't error when packaging nuspec with duplicate files.</span></span><span data-ttu-id="f0bd8-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-130"> - [#6941](https://github.com/NuGet/Home/issues/6941)</span></span>

* <span data-ttu-id="f0bd8-131">NuGet パック "指定された DateTimeOffset を Zip ファイルのタイムスタンプに変換できません" [-](https://github.com/NuGet/Home/issues/7001) #7001</span><span class="sxs-lookup"><span data-stu-id="f0bd8-131">NuGet pack "The DateTimeOffset specified cannot be converted into a Zip file timestamp" - [#7001](https://github.com/NuGet/Home/issues/7001)</span></span>

* <span data-ttu-id="f0bd8-132">パックされたパッケージのファイルのタイムスタンプは、タイムゾーンによってシフトされます[-](https://github.com/NuGet/Home/issues/7395) #7395</span><span class="sxs-lookup"><span data-stu-id="f0bd8-132">Timestamps of file of packed package is shifted by the timezone - [#7395](https://github.com/NuGet/Home/issues/7395)</span></span>

* <span data-ttu-id="f0bd8-133">NU1004 には、より多くのアクション可能な情報が含まれている必要[があります](https://github.com/NuGet/Home/issues/7696)- #7696</span><span class="sxs-lookup"><span data-stu-id="f0bd8-133">NU1004 should contain more actionable information  - [#7696](https://github.com/NuGet/Home/issues/7696)</span></span>

* <span data-ttu-id="f0bd8-134">[バグ Bash][テスト エラー]'dotnet restore --use-lock-file --locked-mode' - #8640 を実行するときに、空または形式のロック ファイル[を更新することはできません](https://github.com/NuGet/Home/issues/8640)。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-134">[Bug Bash][Test Failure] The empty/malformed lock file should not be updated when running ‘dotnet restore --use-lock-file --locked-mode’ - [#8640](https://github.com/NuGet/Home/issues/8640)</span></span>

* <span data-ttu-id="f0bd8-135">NuGetVersionRange を使用すると、論理的に正しくない範囲[](https://github.com/NuGet/Home/issues/9145)を解析#9145</span><span class="sxs-lookup"><span data-stu-id="f0bd8-135">NuGetVersionRange allows logically incorrect ranges to be parsed - [#9145](https://github.com/NuGet/Home/issues/9145)</span></span>

* <span data-ttu-id="f0bd8-136">PM UI では、選択したパッケージ ソースとホバーされたパッケージ ソースの間で識別可能な背景色[を](https://github.com/NuGet/Home/issues/9538)表示できません - #9538</span><span class="sxs-lookup"><span data-stu-id="f0bd8-136">PM UI can’t show distinguishable background color between selected and hovered package sources - [#9538](https://github.com/NuGet/Home/issues/9538)</span></span>

* <span data-ttu-id="f0bd8-137">インストールするプロジェクトを選択する場合のチェック ボックスがスクリーン リーダーによって読[](https://github.com/NuGet/Home/issues/9578)み取#9578</span><span class="sxs-lookup"><span data-stu-id="f0bd8-137">Checkbox for selecting projects to install to isn't being read by screen reader - [#9578](https://github.com/NuGet/Home/issues/9578)</span></span>

* <span data-ttu-id="f0bd8-138">詳細ペインのバージョン ドロップダウンの既定の選択は、[インストール済み]/[更新] タブで [インストール済み]/[LatestStable] である必要があります - [#9887](https://github.com/NuGet/Home/issues/9887)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-138">Details Pane Versions Dropdown default selection should be Installed/LatestStable on Installed/Updates tabs - [#9887](https://github.com/NuGet/Home/issues/9887)</span></span>

* <span data-ttu-id="f0bd8-139">一部の .NET 5 SDK レポート TargetPlatformMoniker の回避策アカウントを削除 ` ,Version= `  -  [#9913](https://github.com/NuGet/Home/issues/9913)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-139">Remove workaround account for some .NET 5 SDKs report TargetPlatformMoniker of ` ,Version= ` - [#9913](https://github.com/NuGet/Home/issues/9913)</span></span>

* <span data-ttu-id="f0bd8-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-140">dotnet nuget verify is too quiet - [#10316](https://github.com/NuGet/Home/issues/10316)</span></span>

* <span data-ttu-id="f0bd8-141">VersionRange で 1 桁の範囲を解析できない - [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-141">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>

* <span data-ttu-id="f0bd8-142">VS Solution Manager がデバッグ中に に null 例外を[スローする](https://github.com/NuGet/Home/issues/10352)- #10352</span><span class="sxs-lookup"><span data-stu-id="f0bd8-142">VS Solution manager throws null exception for during debugging - [#10352](https://github.com/NuGet/Home/issues/10352)</span></span>

* <span data-ttu-id="f0bd8-143">CLI 例外メッセージを文字列リソース ファイルに移動する - [#10392](https://github.com/NuGet/Home/issues/10392)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-143">Move CLI exception messages to String Resource files - [#10392](https://github.com/NuGet/Home/issues/10392)</span></span>

* <span data-ttu-id="f0bd8-144">使用されなコードを削除する (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-144">Remove dead code (TabItemButtonAutomationPeer) - [#10435](https://github.com/NuGet/Home/issues/10435)</span></span>

* <span data-ttu-id="f0bd8-145">更新コンテキスト メニューは、最初に選択した項目までスクロールする必要があります - [#10498](https://github.com/NuGet/Home/issues/10498)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-145">Update context menu should scroll to first selected item - [#10498](https://github.com/NuGet/Home/issues/10498)</span></span>

* <span data-ttu-id="f0bd8-146">ソリューション PMUI の詳細の横棒が重なっている - [#10533](https://github.com/NuGet/Home/issues/10533)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-146">Solution PMUI Details has overlapping horizontal bar - [#10533](https://github.com/NuGet/Home/issues/10533)</span></span>

* <span data-ttu-id="f0bd8-147">署名: 証明書の有効期限が切れ、タイムスタンプが信頼されていない場合にプライマリ署名の詳細[が表示](https://github.com/NuGet/Home/issues/10535)されない - #10535</span><span class="sxs-lookup"><span data-stu-id="f0bd8-147">Signing:  primary signature details not displayed when certificate expired and timestamp untrusted - [#10535](https://github.com/NuGet/Home/issues/10535)</span></span>

* <span data-ttu-id="f0bd8-148">有効なソースがない場合、PM UI が表示#10541 [](https://github.com/NuGet/Home/issues/10541)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-148">Having no enabled sources prevents the PM UI from showing - [#10541](https://github.com/NuGet/Home/issues/10541)</span></span>

* <span data-ttu-id="f0bd8-149">パッケージ メタデータ (詳細、非推奨) は、CodeSpaces の nuget.org からプルされない場合があります - [#10549](https://github.com/NuGet/Home/issues/10549)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-149">Package Metadata (details, deprecation) are sometimes not pulled from nuget.org in CodeSpaces - [#10549](https://github.com/NuGet/Home/issues/10549)</span></span>

* <span data-ttu-id="f0bd8-150">デバッグ セッション中に PMUI の初期化が例外で失敗する - [#10559](https://github.com/NuGet/Home/issues/10559)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-150">PMUI initialization fails with exception during debug session - [#10559](https://github.com/NuGet/Home/issues/10559)</span></span>

* <span data-ttu-id="f0bd8-151">nuget の復元により、ビッグ エンディアン システムでパッケージの整合性チェックエラーが発生する - [#10567](https://github.com/NuGet/Home/issues/10567)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-151">nuget restore results in a package integrity check failure on big endian system - [#10567](https://github.com/NuGet/Home/issues/10567)</span></span>

* <span data-ttu-id="f0bd8-152">PackagingException の代わりに FormatException が[スローされる](https://github.com/NuGet/Home/issues/10595)- #10595</span><span class="sxs-lookup"><span data-stu-id="f0bd8-152">FormatException is thrown instead of PackagingException - [#10595](https://github.com/NuGet/Home/issues/10595)</span></span>

* <span data-ttu-id="f0bd8-153">CPVM - グラフ の実行アルゴリズムでのコンカレンシーの問題 - [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-153">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>

* <span data-ttu-id="f0bd8-154">PMC PowerShell バージョンのテレメトリを追加する - [#10609](https://github.com/NuGet/Home/issues/10609)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-154">Add PMC powershell version telemetry - [#10609](https://github.com/NuGet/Home/issues/10609)</span></span>

* <span data-ttu-id="f0bd8-155">NuGetVersion の並べ替えパフォーマンスの向上 - [#10611](https://github.com/NuGet/Home/issues/10611)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-155">Improve NuGetVersion sort performance - [#10611](https://github.com/NuGet/Home/issues/10611)</span></span>

* <span data-ttu-id="f0bd8-156">信頼できる署名者の追加に一貫性のない引数があります - [#10647](https://github.com/NuGet/Home/issues/10647)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-156">Trusted-signers Add has inconsistent arguments - [#10647](https://github.com/NuGet/Home/issues/10647)</span></span>

* <span data-ttu-id="f0bd8-157">Vs2019 v16.9.0: NuGet パッケージ マネージャー のタブを "更新プログラム" から "インストール済み" に切り替えても、フレームは更新されません。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-157">Vs2019 v16.9.0: Switching tabs in NuGet Package Manager from "Updates" to "Installed" doesn't update the frame.</span></span><span data-ttu-id="f0bd8-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-158"> - [#10654](https://github.com/NuGet/Home/issues/10654)</span></span>

* <span data-ttu-id="f0bd8-159">PMUI のバージョン番号から "v" を[削除する](https://github.com/NuGet/Home/issues/10677)- #10677</span><span class="sxs-lookup"><span data-stu-id="f0bd8-159">Remove the "v" from the version number in PMUI - [#10677](https://github.com/NuGet/Home/issues/10677)</span></span>

* <span data-ttu-id="f0bd8-160">INuGetProjectService.GetInstalledPackagesAsync は、CPS プロジェクト システムの指定を受け取る前に を[スローします](https://github.com/NuGet/Home/issues/10681)- #10681</span><span class="sxs-lookup"><span data-stu-id="f0bd8-160">INuGetProjectService.GetInstalledPackagesAsync throws before receiving CPS project system nomination - [#10681](https://github.com/NuGet/Home/issues/10681)</span></span>

* <span data-ttu-id="f0bd8-161">[参照] タブの [埋め込みアイコンMicrosoft Visual Studioソースからアクセスが拒否される - [#10687](https://github.com/NuGet/Home/issues/10687)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-161">Embedded Icons cause Access Denied from source "Microsoft Visual Studio Offline Packages" on Browse tab - [#10687](https://github.com/NuGet/Home/issues/10687)</span></span>

* <span data-ttu-id="f0bd8-162">MSBuildProjectExtensionsPath が設定されていない場合に INuGetProjectService.GetInstalledPackagesAsync が[スローされる](https://github.com/NuGet/Home/issues/10739)- #10739</span><span class="sxs-lookup"><span data-stu-id="f0bd8-162">INuGetProjectService.GetInstalledPackagesAsync throws when MSBuildProjectExtensionsPath is not set - [#10739](https://github.com/NuGet/Home/issues/10739)</span></span>

* <span data-ttu-id="f0bd8-163">"dotnet nuget remove source nuget.org" が初めて動作しない[-](https://github.com/NuGet/Home/issues/10745) #10745</span><span class="sxs-lookup"><span data-stu-id="f0bd8-163">"dotnet nuget remove source nuget.org" doesn't work the first time - [#10745](https://github.com/NuGet/Home/issues/10745)</span></span>

* <span data-ttu-id="f0bd8-164">Nuget は、UI スレッドへの同期呼び出しを行う非同期メソッドでスレッドプール スレッドをブロックします [#10775。](https://github.com/NuGet/Home/issues/10775)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-164">Nuget blocks a threadpool thread in an async method making a synchronous call to the UI thread - [#10775](https://github.com/NuGet/Home/issues/10775)</span></span>

* <span data-ttu-id="f0bd8-165">ツール -> オプション -> NuGet パッケージ マネージャー文字列が切り捨てられる - [#10779](https://github.com/NuGet/Home/issues/10779)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-165">Tools -> Options -> NuGet Package Manager string is truncated - [#10779](https://github.com/NuGet/Home/issues/10779)</span></span>

* <span data-ttu-id="f0bd8-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` が実行され、パフォーマンスが低下する - [#10790](https://github.com/NuGet/Home/issues/10790)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-166">`PackageLoadContext.GetInstalledAndTransitivePackagesAsync` is dead code and hurting performance - [#10790](https://github.com/NuGet/Home/issues/10790)</span></span>

* <span data-ttu-id="f0bd8-167">NuGet SDK パッケージで埋め込みアイコンを使用する - [#10795](https://github.com/NuGet/Home/issues/10795)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-167">Use embedded icon in NuGet SDK packages - [#10795](https://github.com/NuGet/Home/issues/10795)</span></span>

* <span data-ttu-id="f0bd8-168">SPDX ライセンス の一覧を更新する - [#10806](https://github.com/NuGet/Home/issues/10806)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-168">Update the SPDX license list - [#10806](https://github.com/NuGet/Home/issues/10806)</span></span>

<span data-ttu-id="f0bd8-169">**[このリリースで修正された問題の一覧 - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span><span class="sxs-lookup"><span data-stu-id="f0bd8-169">**[List of all issues fixed in this release - 5.10](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=Z2lkOi8vcmFwdG9yL1JlbGVhc2UvNTY2MTQ)**</span></span>
  
<span data-ttu-id="f0bd8-170">**[このリリースのコミットの一覧 - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span><span class="sxs-lookup"><span data-stu-id="f0bd8-170">**[List of commits in this release - 5.10.0](https://github.com/NuGet/NuGet.Client/compare/5.9.0.7134...5.10.0.7240)**</span></span>
  
### <a name="community-contributions"></a><span data-ttu-id="f0bd8-171">コミュニティからの投稿</span><span class="sxs-lookup"><span data-stu-id="f0bd8-171">Community contributions</span></span>

<span data-ttu-id="f0bd8-172">この NuGet リリースをすばらしいものにするのに役立ったすべての共同作成者に感謝します。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-172">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="f0bd8-173">担当者</span><span class="sxs-lookup"><span data-stu-id="f0bd8-173">Who</span></span>|<span data-ttu-id="f0bd8-174">Prs</span><span class="sxs-lookup"><span data-stu-id="f0bd8-174">PRs</span></span>|<span data-ttu-id="f0bd8-175">発行</span><span class="sxs-lookup"><span data-stu-id="f0bd8-175">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="f0bd8-176">は、次の値を使用します。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-176">louis-z</span></span>](https://github.com/louis-z) | [<span data-ttu-id="f0bd8-177">3991</span><span class="sxs-lookup"><span data-stu-id="f0bd8-177">3991</span></span>](https://github.com/NuGet/NuGet.Client/pull/3991) | <span data-ttu-id="f0bd8-178">VersionRange で 1 桁の範囲を解析できない - [#10342](https://github.com/NuGet/Home/issues/10342)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-178">VersionRange cannot parse single-digit ranges - [#10342](https://github.com/NuGet/Home/issues/10342)</span></span>
[<span data-ttu-id="f0bd8-179">omajid</span><span class="sxs-lookup"><span data-stu-id="f0bd8-179">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="f0bd8-180">3860</span><span class="sxs-lookup"><span data-stu-id="f0bd8-180">3860</span></span>](https://github.com/NuGet/NuGet.Client/pull/3860) | <span data-ttu-id="f0bd8-181">NuGet.Client build.sh 破損しています - [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-181">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="f0bd8-182">Malmal4G</span><span class="sxs-lookup"><span data-stu-id="f0bd8-182">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="f0bd8-183">3623</span><span class="sxs-lookup"><span data-stu-id="f0bd8-183">3623</span></span>](https://github.com/NuGet/NuGet.Client/pull/3623) | <span data-ttu-id="f0bd8-184">NuGet.Client build.sh 破損しています - [#10139](https://github.com/NuGet/Home/issues/10139)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-184">NuGet.Client build.sh is broken - [#10139](https://github.com/NuGet/Home/issues/10139)</span></span>
[<span data-ttu-id="f0bd8-185">BlackGad</span><span class="sxs-lookup"><span data-stu-id="f0bd8-185">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="f0bd8-186">3953</span><span class="sxs-lookup"><span data-stu-id="f0bd8-186">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="f0bd8-187">"nuget pack" のパフォーマンスは、ソース パスのレベルが上がって低下 [します。#5706](https://github.com/NuGet/Home/issues/5706)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-187">The performance of "nuget pack" decreases with increasing levels in the source paths - [#5706](https://github.com/NuGet/Home/issues/5706)</span></span>
[<span data-ttu-id="f0bd8-188">BlackGad</span><span class="sxs-lookup"><span data-stu-id="f0bd8-188">BlackGad</span></span>](https://github.com/BlackGad) | [<span data-ttu-id="f0bd8-189">3953</span><span class="sxs-lookup"><span data-stu-id="f0bd8-189">3953</span></span>](https://github.com/NuGet/NuGet.Client/pull/3953) | <span data-ttu-id="f0bd8-190">NuGet.exeのパフォーマンスの問題を修正しました。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-190">NuGet.exe pack performance problem with ..</span></span> <span data-ttu-id="f0bd8-191">相対パス - [#5016](https://github.com/NuGet/Home/issues/5016)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-191">relative path - [#5016](https://github.com/NuGet/Home/issues/5016)</span></span>
[<span data-ttu-id="f0bd8-192">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="f0bd8-192">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="f0bd8-193">3940</span><span class="sxs-lookup"><span data-stu-id="f0bd8-193">3940</span></span>](https://github.com/NuGet/NuGet.Client/pull/3940) | <span data-ttu-id="f0bd8-194">CPVM - グラフ の実行アルゴリズムでのコンカレンシーの問題 - [#10598](https://github.com/NuGet/Home/issues/10598)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-194">CPVM - Concurrency issues in the graph walking algorithm - [#10598](https://github.com/NuGet/Home/issues/10598)</span></span>
[<span data-ttu-id="f0bd8-195">(1970 年 1 月 12 月</span><span class="sxs-lookup"><span data-stu-id="f0bd8-195">josesimoes</span></span>](https://github.com/josesimoes) | [<span data-ttu-id="f0bd8-196">3943</span><span class="sxs-lookup"><span data-stu-id="f0bd8-196">3943</span></span>](https://github.com/NuGet/NuGet.Client/pull/3943) | <span data-ttu-id="f0bd8-197">プロジェクトの種類 nfproj を Nuget CLI でサポートされているProjectExtensions の一覧に追加します。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-197">Add the project type nfproj to the list of supportedProjectExtensions for Nuget CLI.</span></span><span data-ttu-id="f0bd8-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span><span class="sxs-lookup"><span data-stu-id="f0bd8-198"> - [#10562](https://github.com/NuGet/Home/issues/10562)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="f0bd8-199">フィードバックへようこそ</span><span class="sxs-lookup"><span data-stu-id="f0bd8-199">Feedback welcome</span></span>

<span data-ttu-id="f0bd8-200">お客様のフィードバックは Microsoft にとって重要です。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-200">Your feedback is important to us.</span></span>  <span data-ttu-id="f0bd8-201">このリリースで問題が発生した場合は [、GitHub](https://github.com/NuGet/Home/issues) の問題と既存の問題 [Visual Studio Developer Community確認してください](https://developercommunity.visualstudio.com/) 。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-201">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="f0bd8-202">NuGet 内の新しい問題については [、GitHub の問題 を報告してください](https://github.com/NuGet/Home/issues/new)。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-202">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="f0bd8-203">NuGet エクスペリエンスに関する一般的な問題については、[](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)お気に入りの IDE の [問題の報告] オプションの [ヘルプ] の [問題の報告] >**お知らせください**。</span><span class="sxs-lookup"><span data-stu-id="f0bd8-203">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
