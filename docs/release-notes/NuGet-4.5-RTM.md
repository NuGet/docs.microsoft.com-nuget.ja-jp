---
title: NuGet 4.5 RTM リリース ノート
description: NuGet 4.5 RTM の既知の問題、バグ修正、追加機能、および DCR を含む、そのリリース ノートです。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 12/4/2017
ms.topic: conceptual
ms.openlocfilehash: 1d04c508d029a6d92bbd480fe3bd7dc14727970e
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-45-rtm-release-notes"></a><span data-ttu-id="dad67-103">NuGet 4.5 RTM リリース ノート</span><span class="sxs-lookup"><span data-stu-id="dad67-103">NuGet 4.5 RTM Release Notes</span></span>

<span data-ttu-id="dad67-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、[NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe) が付属しています。</span><span class="sxs-lookup"><span data-stu-id="dad67-104">[Visual Studio 2017 15.5 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.5 RTM](https://dist.nuget.org/win-x86-commandline/v4.5.0/nuget.exe).</span></span>

## <a name="known-issues"></a><span data-ttu-id="dad67-105">既知の問題</span><span class="sxs-lookup"><span data-stu-id="dad67-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="dad67-106">.NET Framework と NuGet での .NET Standard 2.0 の問題</span><span class="sxs-lookup"><span data-stu-id="dad67-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="dad67-107">.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="dad67-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="dad67-108">[このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="dad67-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="dad67-109">NuGet パッケージ マネージャーを使用した DotNetCLITools の表示、追加、更新ができない</span><span class="sxs-lookup"><span data-stu-id="dad67-109">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="dad67-110">懸案事項</span><span class="sxs-lookup"><span data-stu-id="dad67-110">Issue</span></span>

<span data-ttu-id="dad67-111">NuGet パッケージ マネージャーが表示されず、DotNetCLITools を追加または更新できません。</span><span class="sxs-lookup"><span data-stu-id="dad67-111">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="dad67-112">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="dad67-112">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="dad67-113">回避策</span><span class="sxs-lookup"><span data-stu-id="dad67-113">Workaround</span></span>

<span data-ttu-id="dad67-114">DotNetCLIToolReferences はプロジェクト ファイルで手動編集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="dad67-114">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="dad67-115">ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になる</span><span class="sxs-lookup"><span data-stu-id="dad67-115">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="dad67-116">懸案事項</span><span class="sxs-lookup"><span data-stu-id="dad67-116">Issue</span></span>

<span data-ttu-id="dad67-117">Visual Studio では、ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になることがあります。</span><span class="sxs-lookup"><span data-stu-id="dad67-117">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="dad67-118">これは、パッケージ マネージャー形式として PackageReferences を使用しているときに発生します。</span><span class="sxs-lookup"><span data-stu-id="dad67-118">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="dad67-119">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="dad67-119">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="dad67-120">回避策</span><span class="sxs-lookup"><span data-stu-id="dad67-120">Workaround</span></span>

<span data-ttu-id="dad67-121">手動で復元します。</span><span class="sxs-lookup"><span data-stu-id="dad67-121">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="dad67-122">署名が無効なアセンブリを含む .NET Core プロジェクトのパッケージは無限の復元ループを始動させることがある</span><span class="sxs-lookup"><span data-stu-id="dad67-122">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="dad67-123">懸案事項</span><span class="sxs-lookup"><span data-stu-id="dad67-123">Issue</span></span>

<span data-ttu-id="dad67-124">無効なアセンブリを含むパッケージを使用するとき、あるいはパッケージ バージョンに 'DateTime' ティッカーが設定されているとき、パッケージ復元が無限ループになることがあります ([dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457))。</span><span class="sxs-lookup"><span data-stu-id="dad67-124">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop [dotnet/project-system#1457](https://github.com/dotnet/project-system/issues/1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="dad67-125">回避策</span><span class="sxs-lookup"><span data-stu-id="dad67-125">Workaround</span></span>

<span data-ttu-id="dad67-126">この問題の回避策はありません。</span><span class="sxs-lookup"><span data-stu-id="dad67-126">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-45-rtm-timeframe"></a><span data-ttu-id="dad67-127">NuGet 4.5 RTM の時間枠で修正された問題</span><span class="sxs-lookup"><span data-stu-id="dad67-127">Issues fixed in NuGet 4.5 RTM timeframe</span></span>

<span data-ttu-id="dad67-128">NuGet 4.4 RTM で修正された問題については、[NuGet 4.4 RTM のリリース ノート](../release-notes/nuget-4.4-RTM.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dad67-128">For issues fixed in NuGet 4.4 RTM, please refer to [NuGet 4.4 RTM Release Notes](../release-notes/nuget-4.4-RTM.md)</span></span> 

### <a name="features"></a><span data-ttu-id="dad67-129">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="dad67-129">Features</span></span>

- <span data-ttu-id="dad67-130">シンボル パッケージの自動プッシュを無効にする - [#6113](https://github.com/NuGet/Home/issues/6113)</span><span class="sxs-lookup"><span data-stu-id="dad67-130">Disable auto-push of symbols package - [#6113](https://github.com/NuGet/Home/issues/6113)</span></span>

### <a name="bugs"></a><span data-ttu-id="dad67-131">バグ</span><span class="sxs-lookup"><span data-stu-id="dad67-131">Bugs</span></span>

- <span data-ttu-id="dad67-132">15.5p1 での[回帰]: Portable0.0 がスキップされる - [#6105](https://github.com/NuGet/Home/issues/6105)</span><span class="sxs-lookup"><span data-stu-id="dad67-132">[Regression] in 15.5p1: Portable0.0 is skipped - [#6105](https://github.com/NuGet/Home/issues/6105)</span></span>
- <span data-ttu-id="dad67-133">復元後パッケージのアセットが見つからない - [#5995](https://github.com/NuGet/Home/issues/5995)</span><span class="sxs-lookup"><span data-stu-id="dad67-133">Assets from packages are missing after restore - [#5995](https://github.com/NuGet/Home/issues/5995)</span></span>
- <span data-ttu-id="dad67-134">スペースを含む URI でプラグイン資格情報プロバイダーが動作しない - [#5982](https://github.com/NuGet/Home/issues/5982)</span><span class="sxs-lookup"><span data-stu-id="dad67-134">Plugin credential providers do not work with URIs containing spaces - [#5982](https://github.com/NuGet/Home/issues/5982)</span></span>
- <span data-ttu-id="dad67-135">パッケージの復元に失敗した場合、最小の詳細がオンであっても、エラーは出力に印字される必要がある - [#5658](https://github.com/NuGet/Home/issues/5658)</span><span class="sxs-lookup"><span data-stu-id="dad67-135">If package failed to restore, error should be printed in the output even with Minimal verbosity ON - [#5658](https://github.com/NuGet/Home/issues/5658)</span></span>
- <span data-ttu-id="dad67-136">dotnet</span><span class="sxs-lookup"><span data-stu-id="dad67-136">dotnet</span></span>
  - <span data-ttu-id="dad67-137">ソリューション レベルでの dotnetcore restore が ReferenceOutputAssembly が false の ProjectReference に従わず、ビルドがランダムに失敗する - [#5490](https://github.com/NuGet/Home/issues/5490)</span><span class="sxs-lookup"><span data-stu-id="dad67-137">dotnetcore restore at solution-level doesn't follow ProjectReference with ReferenceOutputAssembly of false leading to random build failures - [#5490](https://github.com/NuGet/Home/issues/5490)</span></span>
- <span data-ttu-id="dad67-138">オブジェクト メソッドで PMC のオートコンプリートが正しく動作しない - [#4800](https://github.com/NuGet/Home/issues/4800)</span><span class="sxs-lookup"><span data-stu-id="dad67-138">Auto-complete in PMC works incorrectly with object methods - [#4800](https://github.com/NuGet/Home/issues/4800)</span></span>
- <span data-ttu-id="dad67-139">Visual Studio 2015 ツールセットで nuget.exe の復元が失敗する - [#4713](https://github.com/NuGet/Home/issues/4713)</span><span class="sxs-lookup"><span data-stu-id="dad67-139">nuget.exe restore fails with Visual Studio 2015 toolset - [#4713](https://github.com/NuGet/Home/issues/4713)</span></span>
- <span data-ttu-id="dad67-140">vs2017 で perf - pmc をインスタンス化するにはコストがかかる - [#4205](https://github.com/NuGet/Home/issues/4205)</span><span class="sxs-lookup"><span data-stu-id="dad67-140">perf - pmc is expensive to instantiate in vs2017 - [#4205](https://github.com/NuGet/Home/issues/4205)</span></span>
- <span data-ttu-id="dad67-141">低速接続で依存関係の情報を早く入手できない - [#4089](https://github.com/NuGet/Home/issues/4089)</span><span class="sxs-lookup"><span data-stu-id="dad67-141">Slow to get dependency information on slow connection - [#4089](https://github.com/NuGet/Home/issues/4089)</span></span>
- <span data-ttu-id="dad67-142">複数のパッケージで同じ依存関係を共有する場合、uninstall-package で -RemoveDependencies を使用すると失敗する - [#4026](https://github.com/NuGet/Home/issues/4026)</span><span class="sxs-lookup"><span data-stu-id="dad67-142">uninstall-package w/ -RemoveDependencies will fail if multiple packages share a common dependency - [#4026](https://github.com/NuGet/Home/issues/4026)</span></span>
- <span data-ttu-id="dad67-143">発行用に NuGet.Core.nupkg を最終処理する - [#3581](https://github.com/NuGet/Home/issues/3581)</span><span class="sxs-lookup"><span data-stu-id="dad67-143">Finalize NuGet.Core.nupkg for publishing - [#3581](https://github.com/NuGet/Home/issues/3581)</span></span>
- <span data-ttu-id="dad67-144">-IncludeProjectReferences が csproj と project.json 用に使用される場合、NuGet パックは依存関係 ID をディレクトリ名から解決する - [#3566](https://github.com/NuGet/Home/issues/3566)</span><span class="sxs-lookup"><span data-stu-id="dad67-144">NuGet pack resolves dependency ID from directory name when -IncludeProjectReferences is used for csproj + project.json - [#3566](https://github.com/NuGet/Home/issues/3566)</span></span>
- <span data-ttu-id="dad67-145">'NuGet.ProxyCache' 用のタイプ初期化子が例外をスロー - [#3144](https://github.com/NuGet/Home/issues/3144)</span><span class="sxs-lookup"><span data-stu-id="dad67-145">The type initializer for 'NuGet.ProxyCache' threw an exception - [#3144](https://github.com/NuGet/Home/issues/3144)</span></span>
- <span data-ttu-id="dad67-146">kudu での nuget のパフォーマンスの復元の問題 - [#3087](https://github.com/NuGet/Home/issues/3087)</span><span class="sxs-lookup"><span data-stu-id="dad67-146">nuget restore performance issue with kudu - [#3087](https://github.com/NuGet/Home/issues/3087)</span></span>
- <span data-ttu-id="dad67-147">検索が登録 BLOB よりも前の場合、UI クライアントでエラーまたは警告が表示されない - [#2149](https://github.com/NuGet/Home/issues/2149)</span><span class="sxs-lookup"><span data-stu-id="dad67-147">UI Client fails to show any error or warning when search is ahead of registration blobs - [#2149](https://github.com/NuGet/Home/issues/2149)</span></span>
- <span data-ttu-id="dad67-148">Get-Packages -Updates により不正なクエリが生成される - [#2135](https://github.com/NuGet/Home/issues/2135)</span><span class="sxs-lookup"><span data-stu-id="dad67-148">Get-Packages -Updates generates an incorrect query - [#2135](https://github.com/NuGet/Home/issues/2135)</span></span>

## <a name="links-to-github-issues-fixed-in-45-rtm"></a><span data-ttu-id="dad67-149">4.5 RTM で修正された GitHub の懸案事項へのリンク</span><span class="sxs-lookup"><span data-stu-id="dad67-149">Links to GitHub issues fixed in 4.5 RTM</span></span>

[<span data-ttu-id="dad67-150">懸案事項リスト</span><span class="sxs-lookup"><span data-stu-id="dad67-150">Issues list</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A4.5+is%3Aclosed)
