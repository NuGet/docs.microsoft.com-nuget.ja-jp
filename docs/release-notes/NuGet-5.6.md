---
title: NuGet 5.6 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.6 のリリースノート。
author: chgill-msft
ms.author: chgill
ms.date: 05/19/2020
ms.topic: conceptual
ms.openlocfilehash: e8d80a247da1cd18b53b35c51fb3d3dcf1cf68fa
ms.sourcegitcommit: 3529348ed394595d0fa01271486b831af9c97597
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2020
ms.locfileid: "83727807"
---
# <a name="nuget-56-release-notes"></a><span data-ttu-id="f5a66-103">NuGet 5.6 リリースノート</span><span class="sxs-lookup"><span data-stu-id="f5a66-103">NuGet 5.6 Release Notes</span></span>

<span data-ttu-id="f5a66-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="f5a66-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="f5a66-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="f5a66-105">NuGet version</span></span> | <span data-ttu-id="f5a66-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="f5a66-106">Available in Visual Studio version</span></span>| <span data-ttu-id="f5a66-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f5a66-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="f5a66-108">**5.6.0**</span><span class="sxs-lookup"><span data-stu-id="f5a66-108">**5.6.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="f5a66-109">Visual Studio 2019 バージョン 16.6</span><span class="sxs-lookup"><span data-stu-id="f5a66-109">Visual Studio 2019 version 16.6</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="f5a66-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="f5a66-110">[3.1.300](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="f5a66-111"><sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="f5a66-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-56"></a><span data-ttu-id="f5a66-112">概要: 5.6 の新機能</span><span class="sxs-lookup"><span data-stu-id="f5a66-112">Summary: What's New in 5.6</span></span>

* <span data-ttu-id="f5a66-113">フローティングバージョンでのプレリリースパッケージをサポートします。</span><span class="sxs-lookup"><span data-stu-id="f5a66-113">Support prerelease packages with floating versions.</span></span> <span data-ttu-id="f5a66-114">`Version="*-*"`、 `Version="1.*-*"` 、およびは、指定された範囲内で、プレリリースバージョンを含む最新バージョンに類似してい[#912](https://github.com/NuGet/Home/issues/912)</span><span class="sxs-lookup"><span data-stu-id="f5a66-114">`Version="*-*"`, `Version="1.*-*"`, and similar float to latest versions, including prerelease versions, within specified range  - [#912](https://github.com/NuGet/Home/issues/912)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f5a66-115">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="f5a66-115">Issues fixed in this release</span></span>

<span data-ttu-id="f5a66-116">**バグ**</span><span class="sxs-lookup"><span data-stu-id="f5a66-116">**Bugs:**</span></span>

* <span data-ttu-id="f5a66-117">`nuget push *.nupkg`snupkg が存在しない場合に失敗します- [#8148](https://github.com/NuGet/Home/issues/8148)</span><span class="sxs-lookup"><span data-stu-id="f5a66-117">`nuget push *.nupkg` fails when snupkg does not exist - [#8148](https://github.com/NuGet/Home/issues/8148)</span></span>

* <span data-ttu-id="f5a66-118">パックなど、いくつかのコードパスは、ロケールに依存しません。</span><span class="sxs-lookup"><span data-stu-id="f5a66-118">Pack, and several other code paths, fail dependent on locale.</span></span> <span data-ttu-id="f5a66-119">RegexOptions を使用します。 Regexoptions.cultureinvariant- [#8246](https://github.com/NuGet/Home/issues/8246)</span><span class="sxs-lookup"><span data-stu-id="f5a66-119">Use RegexOptions.CultureInvariant - [#8246](https://github.com/NuGet/Home/issues/8246)</span></span>

* <span data-ttu-id="f5a66-120">パフォーマンス: アンロードされたプロジェクトシナリオの DG 仕様をプレビュー復元で記述することはできません- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="f5a66-120">Perf: DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="f5a66-121">復元: ソリューションの依存関係グラフの仕様をキャッシュしてパフォーマンスを向上させる- [#9201](https://github.com/NuGet/Home/issues/9201)</span><span class="sxs-lookup"><span data-stu-id="f5a66-121">Restore: Improve performance by caching solution dependency graph spec - [#9201](https://github.com/NuGet/Home/issues/9201)</span></span>

* <span data-ttu-id="f5a66-122">Pm コンソールを使用してパッケージをインストールした後、SDK スタイルプロジェクトで PM UI が機能しない- [#9203](https://github.com/NuGet/Home/issues/9203)</span><span class="sxs-lookup"><span data-stu-id="f5a66-122">PM UI doesn't work for SDK style projects after installing a package with PM Console - [#9203](https://github.com/NuGet/Home/issues/9203)</span></span>

* <span data-ttu-id="f5a66-123">埋め込みアイコンは、ローカルパッケージフィードを含む PM UI では表示できません (/vs \- [#9225](https://github.com/NuGet/Home/issues/9225)によって異なります)</span><span class="sxs-lookup"><span data-stu-id="f5a66-123">Embedded icon can’t be shown in PM UI with local package feed - depending on / vs \ - [#9225](https://github.com/NuGet/Home/issues/9225)</span></span>

* <span data-ttu-id="f5a66-124">NuGetVersion () は解析に失敗した場合に false を返します- [#9255](https://github.com/NuGet/Home/issues/9255)</span><span class="sxs-lookup"><span data-stu-id="f5a66-124">NuGetVersion.TryParseStrict() should return false if it fails to parse - [#9255](https://github.com/NuGet/Home/issues/9255)</span></span>

* <span data-ttu-id="f5a66-125">`nuget.exe push`のヘルプでは、ソース `-source` URL ではなくソース名の使用を提案する必要があり[#9265](https://github.com/NuGet/Home/issues/9265)</span><span class="sxs-lookup"><span data-stu-id="f5a66-125">`nuget.exe push` help for `-source`, should suggest usage of source name, not source URL - [#9265](https://github.com/NuGet/Home/issues/9265)</span></span>

* <span data-ttu-id="f5a66-126">`dotnet nuget add package SourceUri`無効な既定のパッケージソース名を作成します- [#9277](https://github.com/NuGet/Home/issues/9277)</span><span class="sxs-lookup"><span data-stu-id="f5a66-126">`dotnet nuget add package SourceUri`  creates bad default package source name - [#9277](https://github.com/NuGet/Home/issues/9277)</span></span>

* <span data-ttu-id="f5a66-127">スクリーンリーダーが "検索中..." をアナウンスしないタブを切り替えるときのメッセージ- [#9307](https://github.com/NuGet/Home/issues/9307)</span><span class="sxs-lookup"><span data-stu-id="f5a66-127">Screen reader doesn't announce "Searching..." message when switching tabs - [#9307](https://github.com/NuGet/Home/issues/9307)</span></span>

* <span data-ttu-id="f5a66-128">アクセシビリティ: 暗いテーマでは、フォーカスを示す四角形の色は PM UI タブにはアクセスできません- [#9336](https://github.com/NuGet/Home/issues/9336)</span><span class="sxs-lookup"><span data-stu-id="f5a66-128">Accessibility: Focus-rectangle color is not accessible PM UI tabs in dark theme - [#9336](https://github.com/NuGet/Home/issues/9336)</span></span>

* <span data-ttu-id="f5a66-129">MSBuild 14 以下では、nuget.exe 5.5 を復元できません- [#9458](https://github.com/NuGet/Home/issues/9458)</span><span class="sxs-lookup"><span data-stu-id="f5a66-129">nuget.exe 5.5 fails to restore with MSBuild 14 or below - [#9458](https://github.com/NuGet/Home/issues/9458)</span></span>

* <span data-ttu-id="f5a66-130">メッセージの復元中にミリ秒単位の時間をログに記録しない- [#8977](https://github.com/NuGet/Home/issues/8977)</span><span class="sxs-lookup"><span data-stu-id="f5a66-130">Don't log millisecond times in restore messages - [#8977](https://github.com/NuGet/Home/issues/8977)</span></span>

* <span data-ttu-id="f5a66-131">IOutputConsole を非同期[#9268](https://github.com/NuGet/Home/issues/9268)にする</span><span class="sxs-lookup"><span data-stu-id="f5a66-131">Make IOutputConsole async - [#9268](https://github.com/NuGet/Home/issues/9268)</span></span>

* <span data-ttu-id="f5a66-132">一部の英語以外のカルチャでは、MSBuild バージョンの選択が正しく機能しません- [#9322](https://github.com/NuGet/Home/issues/9322)</span><span class="sxs-lookup"><span data-stu-id="f5a66-132">MSBuild version picking works poorly on some non-english cultures - [#9322](https://github.com/NuGet/Home/issues/9322)</span></span>

* <span data-ttu-id="f5a66-133">#9337 に既定の形式がありません `dotnet nuget list source`  -  [#9337](https://github.com/NuGet/Home/issues/9337)</span><span class="sxs-lookup"><span data-stu-id="f5a66-133">Missing format default on `dotnet nuget list source` - [#9337](https://github.com/NuGet/Home/issues/9337)</span></span>

* <span data-ttu-id="f5a66-134">Perf: RestoreOperationLogger に不要なスレッドアフィニティがあります- [#9288](https://github.com/NuGet/Home/issues/9288)</span><span class="sxs-lookup"><span data-stu-id="f5a66-134">Perf: RestoreOperationLogger has unnecessary thread affinity - [#9288](https://github.com/NuGet/Home/issues/9288)</span></span>

* <span data-ttu-id="f5a66-135">コマンドのドキュメントの自動作成 `dotnet nuget` - [#9146](https://github.com/NuGet/Home/issues/9146)</span><span class="sxs-lookup"><span data-stu-id="f5a66-135">Automated creation of docs for `dotnet nuget` commands - [#9146](https://github.com/NuGet/Home/issues/9146)</span></span>

* <span data-ttu-id="f5a66-136">既定の詳細度では、各プロジェクトの noop 復元を報告することはできません- [#8792](https://github.com/NuGet/Home/issues/8792)</span><span class="sxs-lookup"><span data-stu-id="f5a66-136">Default verbosity should not report each project's noop restore - [#8792](https://github.com/NuGet/Home/issues/8792)</span></span>

* <span data-ttu-id="f5a66-137">`-DependencyVersion`のサポートパラメーター `NuGet.exe update` は、インストールコマンド[#7694](https://github.com/NuGet/Home/issues/7694)と似ています。</span><span class="sxs-lookup"><span data-stu-id="f5a66-137">Support `-DependencyVersion` parameter for `NuGet.exe update`, similar to install command - [#7694](https://github.com/NuGet/Home/issues/7694)</span></span>


<span data-ttu-id="f5a66-138">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="f5a66-138">**DCRs:**</span></span>

* <span data-ttu-id="f5a66-139">Net 5.0 ターゲットフレームワークの初期サポートを追加する- [#9584](https://github.com/NuGet/Home/issues/9584)</span><span class="sxs-lookup"><span data-stu-id="f5a66-139">Add initial support for net5.0 target framework - [#9584](https://github.com/NuGet/Home/issues/9584)</span></span>

* <span data-ttu-id="f5a66-140">PM UI [#9278](https://github.com/NuGet/Home/issues/9278)の [更新] タブで、ID でパッケージを並べ替えます。</span><span class="sxs-lookup"><span data-stu-id="f5a66-140">Sort packages by ID in the Updates tab of the PM UI - [#9278](https://github.com/NuGet/Home/issues/9278)</span></span>


<span data-ttu-id="f5a66-141">**[このリリースで修正されるすべての問題の一覧-5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span><span class="sxs-lookup"><span data-stu-id="f5a66-141">**[List of all issues fixed in this release - 5.6](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e3b2080c4b30708e48bf9f3)**</span></span>
