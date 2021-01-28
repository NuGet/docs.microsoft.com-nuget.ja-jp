---
title: NuGet 4.3 RTM リリース ノート
description: NuGet 4.3 RTM のリリース ノートであり、既知の問題、バグ修正、追加機能、および DCR が含まれています。
author: JonDouglas
ms.author: jodou
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e9b6d15584d875f59ed64fe662944db3e37aeabb
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780174"
---
# <a name="nuget-43-release-notes"></a><span data-ttu-id="5492e-103">NuGet 4.3 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="5492e-103">NuGet 4.3 Release Notes</span></span>

<span data-ttu-id="5492e-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、.NET Standard 2.0/.NET Core 2.0 などの新しいシナリオ用のサポートを追加し、多数の品質修正を含み、パフォーマンスを改善する NuGet 4.3 RTM が付属しています。</span><span class="sxs-lookup"><span data-stu-id="5492e-104">[Visual Studio 2017 15.3 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.3 RTM which adds support for new scenarios such as .NET Standard 2.0/.NET Core 2.0, contains many quality fixes, and improves performance.</span></span> <span data-ttu-id="5492e-105">このリリースには、セマンティック バージョニング 2.0.0、NuGet の警告とエラーの MSBuild への統合などのサポートのいくつかの機能強化もあります。</span><span class="sxs-lookup"><span data-stu-id="5492e-105">This release also brings several improvements like support for Semantic Versioning 2.0.0, MSBuild integration of NuGet warnings and errors, and more.</span></span>

## <a name="summary-whats-new-in-430"></a><span data-ttu-id="5492e-106">概要:4.3.0 の新機能</span><span class="sxs-lookup"><span data-stu-id="5492e-106">Summary: What's New in 4.3.0</span></span>

## <a name="summary-whats-new-in-431"></a><span data-ttu-id="5492e-107">概要:4.3.1 の新機能</span><span class="sxs-lookup"><span data-stu-id="5492e-107">Summary: What's New in 4.3.1</span></span>

* <span data-ttu-id="5492e-108">セキュリティ修正プログラム: ~/.nuget 内で作成されたファイルに対するアクセス許可の範囲が広すぎる [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="5492e-108">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>
* <span data-ttu-id="5492e-109">セキュリティ修正プログラム: NUPKG ディレクトリより上の NUPKG 内のファイルに相対パスが含まれる場合がある [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="5492e-109">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="5492e-110">既知の問題</span><span class="sxs-lookup"><span data-stu-id="5492e-110">Known issues</span></span>

### <a name="nuget-restore-may-treat-disabled-package-sources-as-enabled-in-some-cases"></a><span data-ttu-id="5492e-111">NuGet の復元で無効になっているパッケージ ソースが有効として扱われることがある</span><span class="sxs-lookup"><span data-stu-id="5492e-111">NuGet restore may treat disabled package sources as enabled in some cases</span></span>

#### <a name="issue"></a><span data-ttu-id="5492e-112">懸案事項</span><span class="sxs-lookup"><span data-stu-id="5492e-112">Issue</span></span>

<span data-ttu-id="5492e-113">次の復元コマンド ライン手法を使うと、無効になっているパッケージ ソースが有効として処理されます。</span><span class="sxs-lookup"><span data-stu-id="5492e-113">The following restore command-line techniques treat disabled packages sources as enabled.</span></span> [<span data-ttu-id="5492e-114">NuGet#5704</span><span class="sxs-lookup"><span data-stu-id="5492e-114">NuGet#5704</span></span>](https://github.com/NuGet/Home/issues/5704)
- `msbuild /t:restore`
- <span data-ttu-id="5492e-115">`dotnet restore` (VS または NetCore SDK 2.0.0 に付属する dotnet.exe を使用)</span><span class="sxs-lookup"><span data-stu-id="5492e-115">`dotnet restore` (either with dotnet.exe that ships with VS, or the one that comes with NetCore SDK 2.0.0)</span></span>

#### <a name="workaround"></a><span data-ttu-id="5492e-116">回避策</span><span class="sxs-lookup"><span data-stu-id="5492e-116">Workaround</span></span>

1. <span data-ttu-id="5492e-117">Visual Studio (2017 15.3 以降) または NuGet.exe (v4.3.0 以降) を使います。</span><span class="sxs-lookup"><span data-stu-id="5492e-117">Use Visual Studio (2017 15.3 or later) or NuGet.exe (v4.3.0 or later)</span></span>
1. <span data-ttu-id="5492e-118">無効なソースを削除し、引き続き msbuild または dotnet.exe を使います。</span><span class="sxs-lookup"><span data-stu-id="5492e-118">Delete your disabled source and continue to use msbuild or dotnet.exe.</span></span>
1. <span data-ttu-id="5492e-119">ソリューションの場合、NuGet.config で "Clear" を使った後、そのソリューションに必要なソースを定義できます。</span><span class="sxs-lookup"><span data-stu-id="5492e-119">For your solution, you could use "Clear" in NuGet.config and then define the sources necessary for that solution.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="5492e-120">パッケージ マネージャー コンソールの使用中、'Enter' キーが機能しない</span><span class="sxs-lookup"><span data-stu-id="5492e-120">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="5492e-121">懸案事項</span><span class="sxs-lookup"><span data-stu-id="5492e-121">Issue</span></span>

<span data-ttu-id="5492e-122">パッケージ マネージャー コンソールで、Enter キーが機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="5492e-122">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="5492e-123">その場合、修正プログラムで進捗状況を確認してください。再現手順について役に立つ情報があれば提供してください。</span><span class="sxs-lookup"><span data-stu-id="5492e-123">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="5492e-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="5492e-124">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="5492e-125">回避策</span><span class="sxs-lookup"><span data-stu-id="5492e-125">Workaround</span></span>

<span data-ttu-id="5492e-126">ソリューションを開く前に、Visual Studio を再起動し、PMC を開いてください。</span><span class="sxs-lookup"><span data-stu-id="5492e-126">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="5492e-127">または、`project.lock.json` を削除し、もう一度復元してください。</span><span class="sxs-lookup"><span data-stu-id="5492e-127">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="5492e-128">NuGet パッケージ マネージャーを使用した DotNetCLITools の表示、追加、更新ができない</span><span class="sxs-lookup"><span data-stu-id="5492e-128">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="5492e-129">懸案事項</span><span class="sxs-lookup"><span data-stu-id="5492e-129">Issue</span></span>

<span data-ttu-id="5492e-130">NuGet パッケージ マネージャーが表示されず、DotNetCLITools を追加または更新できません。</span><span class="sxs-lookup"><span data-stu-id="5492e-130">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="5492e-131">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="5492e-131">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="5492e-132">回避策</span><span class="sxs-lookup"><span data-stu-id="5492e-132">Workaround</span></span>

<span data-ttu-id="5492e-133">DotNetCLIToolReferences はプロジェクト ファイルで手動編集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5492e-133">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="5492e-134">ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になる</span><span class="sxs-lookup"><span data-stu-id="5492e-134">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="5492e-135">懸案事項</span><span class="sxs-lookup"><span data-stu-id="5492e-135">Issue</span></span>

<span data-ttu-id="5492e-136">Visual Studio では、ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になることがあります。</span><span class="sxs-lookup"><span data-stu-id="5492e-136">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="5492e-137">これは、パッケージ マネージャー形式として PackageReferences を使用しているときに発生します。</span><span class="sxs-lookup"><span data-stu-id="5492e-137">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="5492e-138">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="5492e-138">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="5492e-139">回避策</span><span class="sxs-lookup"><span data-stu-id="5492e-139">Workaround</span></span>

<span data-ttu-id="5492e-140">手動で復元します。</span><span class="sxs-lookup"><span data-stu-id="5492e-140">Do a manual restore.</span></span>

## <a name="issues-fixed-in-nuget-43-rtm-timeframe"></a><span data-ttu-id="5492e-141">NuGet 4.3 RTM の時間枠で修正された問題</span><span class="sxs-lookup"><span data-stu-id="5492e-141">Issues fixed in NuGet 4.3 RTM timeframe</span></span>

<span data-ttu-id="5492e-142">[NuGet 4.0 RTM のリリースノート](../release-notes/nuget-4.0-RTM.md) - NuGet 4.0 RTM で修正されたすべての問題が掲載されています</span><span class="sxs-lookup"><span data-stu-id="5492e-142">[NuGet 4.0 RTM Release Notes](../release-notes/nuget-4.0-RTM.md) - Lists all the issues fixed for NuGet 4.0 RTM</span></span>

### <a name="features"></a><span data-ttu-id="5492e-143">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="5492e-143">Features</span></span>

- <span data-ttu-id="5492e-144">NuGet の復元のパフォーマンスの向上: コマンドラインからの復元と VS でのよりスマートな NoOp の実装 - [#5080](https://github.com/NuGet/Home/issues/5080)</span><span class="sxs-lookup"><span data-stu-id="5492e-144">Improve NuGet Restore Perf - Implement smarter NoOp for command line restores and VS - [#5080](https://github.com/NuGet/Home/issues/5080)</span></span>

- <span data-ttu-id="5492e-145">.NET Core 2.0: VS/Dotnet CLI で既存の NuGet 機能を使用開始する必要がある: FallBack フォルダー - [#4939](https://github.com/NuGet/Home/issues/4939)</span><span class="sxs-lookup"><span data-stu-id="5492e-145">NET Core 2.0: VS/Dotnet CLI should start using existing NuGet functionality: FallBack folders - [#4939](https://github.com/NuGet/Home/issues/4939)</span></span>

- <span data-ttu-id="5492e-146">.NET Core 2.0: 特定の復元の警告をユーザーが無視 (またはエラーを昇格) できるようにする - [#4898](https://github.com/NuGet/Home/issues/4898)</span><span class="sxs-lookup"><span data-stu-id="5492e-146">NET Core 2.0: Enable users to ignore specific restore warnings (or elevate to error) - [#4898](https://github.com/NuGet/Home/issues/4898)</span></span>

- <span data-ttu-id="5492e-147">.NET Core 2.0: CLI のローカライズ アセンブリ - [#4896](https://github.com/NuGet/Home/issues/4896)</span><span class="sxs-lookup"><span data-stu-id="5492e-147">NET Core 2.0: CLI localized assemblies - [#4896](https://github.com/NuGet/Home/issues/4896)</span></span>

- <span data-ttu-id="5492e-148">NET Core 2.0: アセット ファイルへのすべての警告/エラーの登録 (PackageTargetFallback を含む) - [#4895](https://github.com/NuGet/Home/issues/4895)</span><span class="sxs-lookup"><span data-stu-id="5492e-148">NET Core 2.0: register all warnings/errors to assets file (including PackageTargetFallback) - [#4895](https://github.com/NuGet/Home/issues/4895)</span></span>

- <span data-ttu-id="5492e-149">TFM のサポートの有効化: NetStandard2.0、Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span><span class="sxs-lookup"><span data-stu-id="5492e-149">Enable TFM support: NetStandard2.0, Tizen - [#4892](https://github.com/NuGet/Home/issues/4892)</span></span>

- <span data-ttu-id="5492e-150">NuGet.Core および NuGet.Client プロジェクト (そして結果として DLL) の数の削減 - [#2446](https://github.com/NuGet/Home/issues/2446)</span><span class="sxs-lookup"><span data-stu-id="5492e-150">Reduce the number of NuGet.Core and NuGet.Client projects (and thus DLLs) - [#2446](https://github.com/NuGet/Home/issues/2446)</span></span>

- <span data-ttu-id="5492e-151">nuget 警告をエラーとしてマークする機能の追加 - [#2395](https://github.com/NuGet/Home/issues/2395)</span><span class="sxs-lookup"><span data-stu-id="5492e-151">Add ability to mark nuget warnings as errors - [#2395](https://github.com/NuGet/Home/issues/2395)</span></span>

### <a name="bugs"></a><span data-ttu-id="5492e-152">バグ</span><span class="sxs-lookup"><span data-stu-id="5492e-152">Bugs</span></span>

- <span data-ttu-id="5492e-153">"PackTask" タスクで "DevelopmentDependency" パラメーターで失敗する msbuild /t:pack はサポートされない - [#5584](https://github.com/NuGet/Home/issues/5584)</span><span class="sxs-lookup"><span data-stu-id="5492e-153">msbuild /t:pack fails with The "DevelopmentDependency" parameter is not supported by the "PackTask" task - [#5584](https://github.com/NuGet/Home/issues/5584)</span></span>

- <span data-ttu-id="5492e-154">PackagePath の最後に Windows ディレクトリの区切り記号を追加しないと、コンテンツ ファイルのディレクトリ構造がフラット化する - [#4795](https://github.com/NuGet/Home/issues/4795)</span><span class="sxs-lookup"><span data-stu-id="5492e-154">Directory structure for content files flattened if not adding Windows directory separator at the end of PackagePath - [#4795](https://github.com/NuGet/Home/issues/4795)</span></span>

- <span data-ttu-id="5492e-155">netcore プロジェクトでは developmentDependency としての設定がサポートされない - [#4694](https://github.com/NuGet/Home/issues/4694)</span><span class="sxs-lookup"><span data-stu-id="5492e-155">netcore projects don't support setting as developmentDependency - [#4694](https://github.com/NuGet/Home/issues/4694)</span></span>

- <span data-ttu-id="5492e-156">UI スレッドをブロックし VS をデッドロックさせた RestoreManagerPackage が同期的に読み込まれる - [#4679](https://github.com/NuGet/Home/issues/4679)</span><span class="sxs-lookup"><span data-stu-id="5492e-156">RestoreManagerPackage being loaded synchronously which blocked UI thread and deadlocked VS - [#4679](https://github.com/NuGet/Home/issues/4679)</span></span>

- <span data-ttu-id="5492e-157">dotnet</span><span class="sxs-lookup"><span data-stu-id="5492e-157">dotnet</span></span>
  - <span data-ttu-id="5492e-158">dotnetcore Restore (そのため msbuild /t:restore) はソリューションで明示的なプロジェクト依存関係があるプロジェクトをスキップする [#4578](https://github.com/NuGet/Home/issues/4578)</span><span class="sxs-lookup"><span data-stu-id="5492e-158">dotnetcore Restore (& therefore msbuild /t:restore) skips projects with an explicit solution project dependency [#4578](https://github.com/NuGet/Home/issues/4578)</span></span>

- <span data-ttu-id="5492e-159">ソリューションに、大文字と小文字が異なる、同じプロジェクトを参照するプロジェクトへの参照がある場合、復元ができない場合があります。</span><span class="sxs-lookup"><span data-stu-id="5492e-159">If your solution has projectreferences that refer to the same project, with different casing, restore may not work.</span></span> <span data-ttu-id="5492e-160">これは、別の相対パスで、大文字と小文字に違いがない場合にも影響します - [#4574](https://github.com/NuGet/Home/issues/4574)</span><span class="sxs-lookup"><span data-stu-id="5492e-160">This also affects different relative paths, without a difference in casing - [#4574](https://github.com/NuGet/Home/issues/4574)</span></span>

- <span data-ttu-id="5492e-161">NuGet パッケージから復元した実行可能ファイルが .NET Core 2.0 で実行できない - [#4424](https://github.com/NuGet/Home/issues/4424)</span><span class="sxs-lookup"><span data-stu-id="5492e-161">Executables restored from NuGet packages are no longer executable with .NET Core 2.0 - [#4424](https://github.com/NuGet/Home/issues/4424)</span></span>

- <span data-ttu-id="5492e-162">ソリューション ファイルの解析時に、NuGet.exe が例外の詳細を受け取る - [#4411](https://github.com/NuGet/Home/issues/4411)</span><span class="sxs-lookup"><span data-stu-id="5492e-162">NuGet.exe swallows details of exception when parsing solution file - [#4411](https://github.com/NuGet/Home/issues/4411)</span></span>

- <span data-ttu-id="5492e-163">Windows で ContentTargetFolders に '/' で終わるパスが含まれている場合、パックがコンテンツ ファイルを不正な場所に配置する - [#4407](https://github.com/NuGet/Home/issues/4407)</span><span class="sxs-lookup"><span data-stu-id="5492e-163">Pack puts content files in wrong location if ContentTargetFolders contains a path that ends with '/' on Windows - [#4407](https://github.com/NuGet/Home/issues/4407)</span></span>

- <span data-ttu-id="5492e-164">netcoreapp1.1 をターゲットとするツール パッケージ用に DotNetCliToolReference を復元できない - [#4396](https://github.com/NuGet/Home/issues/4396)</span><span class="sxs-lookup"><span data-stu-id="5492e-164">Can't restore a DotNetCliToolReference for a tools package that targets netcoreapp1.1 - [#4396](https://github.com/NuGet/Home/issues/4396)</span></span>

- <span data-ttu-id="5492e-165">Nuget 更新 CLI が古いパッケージ バージョンの状態をプロジェクト ファイルに残す (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span><span class="sxs-lookup"><span data-stu-id="5492e-165">Nuget update CLI leaves the old package version condition in project file (C++) - [#2449](https://github.com/NuGet/Home/issues/2449)</span></span>

### <a name="dcrs"></a><span data-ttu-id="5492e-166">DCR</span><span class="sxs-lookup"><span data-stu-id="5492e-166">DCRs</span></span>

- <span data-ttu-id="5492e-167">CPS 候補からの DotnetCliToolTargetFramework の読み取り - [#5397](https://github.com/NuGet/Home/issues/5397)</span><span class="sxs-lookup"><span data-stu-id="5492e-167">Read DotnetCliToolTargetFramework from CPS nomation - [#5397](https://github.com/NuGet/Home/issues/5397)</span></span>

- <span data-ttu-id="5492e-168">TPMinV チェックは pj スタイル UWP 用に動作する必要がある - [#4763](https://github.com/NuGet/Home/issues/4763)</span><span class="sxs-lookup"><span data-stu-id="5492e-168">TPMinV check should work for pj style UWP - [#4763](https://github.com/NuGet/Home/issues/4763)</span></span>

- <span data-ttu-id="5492e-169">AutoReferenced パッケージ用の UI の説明の向上 - [#4471](https://github.com/NuGet/Home/issues/4471)</span><span class="sxs-lookup"><span data-stu-id="5492e-169">Improve UI description for AutoReferenced packages - [#4471](https://github.com/NuGet/Home/issues/4471)</span></span>

- <span data-ttu-id="5492e-170">NuGet の復元は、ランタイム セクションからコンパイル アセットを選択しています。</span><span class="sxs-lookup"><span data-stu-id="5492e-170">NuGet restore is selecting compile assets from runtime section.</span></span><span data-ttu-id="5492e-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span><span class="sxs-lookup"><span data-stu-id="5492e-171"> - [#4207](https://github.com/NuGet/Home/issues/4207)</span></span>

- <span data-ttu-id="5492e-172">ロック ファイルに依存関係の診断を入れる - [#1599](https://github.com/NuGet/Home/issues/1599)</span><span class="sxs-lookup"><span data-stu-id="5492e-172">Put dependency diagnostics in the lock file - [#1599](https://github.com/NuGet/Home/issues/1599)</span></span>

## <a name="links-to-github-issues-fixed-in-43-rtm"></a><span data-ttu-id="5492e-173">4\.3 RTM で修正された GitHub の懸案事項へのリンク</span><span class="sxs-lookup"><span data-stu-id="5492e-173">Links to GitHub issues fixed in 4.3 RTM</span></span>

[<span data-ttu-id="5492e-174">懸案事項リスト</span><span class="sxs-lookup"><span data-stu-id="5492e-174">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.3")
