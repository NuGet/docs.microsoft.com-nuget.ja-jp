---
title: NuGet 4.4 RTM リリース ノート
description: NuGet 4.3 RTM のリリース ノートであり、既知の問題、バグ修正、追加機能、および DCR が含まれています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/14/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3e969274e69de03ca9851d31a627919dcc46bb7d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821669"
---
# <a name="nuget-44-rtm-release-notes"></a><span data-ttu-id="104fc-103">NuGet 4.4 RTM リリース ノート</span><span class="sxs-lookup"><span data-stu-id="104fc-103">NuGet 4.4 RTM Release Notes</span></span>

<span data-ttu-id="104fc-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、NuGet 4.4 RTM が付属しています。</span><span class="sxs-lookup"><span data-stu-id="104fc-104">[Visual Studio 2017 15.4 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.4 RTM.</span></span>

## <a name="known-issues"></a><span data-ttu-id="104fc-105">既知の問題</span><span class="sxs-lookup"><span data-stu-id="104fc-105">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="104fc-106">.NET Framework と NuGet での .NET Standard 2.0 の問題</span><span class="sxs-lookup"><span data-stu-id="104fc-106">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="104fc-107">.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="104fc-107">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="104fc-108">[このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="104fc-108">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

### <a name="while-using-package-manager-console-enter-key-may-not-work"></a><span data-ttu-id="104fc-109">パッケージ マネージャー コンソールの使用中、'Enter' キーが機能しない</span><span class="sxs-lookup"><span data-stu-id="104fc-109">While using Package Manager Console, 'Enter' key may not work</span></span>

#### <a name="issue"></a><span data-ttu-id="104fc-110">懸案事項</span><span class="sxs-lookup"><span data-stu-id="104fc-110">Issue</span></span>

<span data-ttu-id="104fc-111">パッケージ マネージャー コンソールで、Enter キーが機能しないことがあります。</span><span class="sxs-lookup"><span data-stu-id="104fc-111">Occasionally, the enter key does not work in the Package Manager Console.</span></span> <span data-ttu-id="104fc-112">その場合、修正プログラムで進捗状況を確認してください。再現手順について役に立つ情報があれば提供してください。</span><span class="sxs-lookup"><span data-stu-id="104fc-112">If you see this, please check out the progress on the fix, and provide any additional helpful information about your repro steps.</span></span> <span data-ttu-id="104fc-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span><span class="sxs-lookup"><span data-stu-id="104fc-113">[NuGet#4204](https://github.com/NuGet/Home/issues/4204) [NuGet#4570](https://github.com/NuGet/Home/issues/4570)</span></span>

#### <a name="workaround"></a><span data-ttu-id="104fc-114">回避策</span><span class="sxs-lookup"><span data-stu-id="104fc-114">Workaround</span></span>

<span data-ttu-id="104fc-115">ソリューションを開く前に、Visual Studio を再起動し、PMC を開いてください。</span><span class="sxs-lookup"><span data-stu-id="104fc-115">Restart Visual Studio and open the PMC before opening the solution.</span></span> <span data-ttu-id="104fc-116">または、`project.lock.json` を削除し、もう一度復元してください。</span><span class="sxs-lookup"><span data-stu-id="104fc-116">Alternatively, try deleting the `project.lock.json` and restoring again.</span></span>

### <a name="you-are-unable-to-view-add-or-update-dotnetclitools-using-nuget-package-manager"></a><span data-ttu-id="104fc-117">NuGet パッケージ マネージャーを使用した DotNetCLITools の表示、追加、更新ができない</span><span class="sxs-lookup"><span data-stu-id="104fc-117">You are unable to view, add, or update DotNetCLITools, using Nuget Package Manager</span></span>

#### <a name="issue"></a><span data-ttu-id="104fc-118">懸案事項</span><span class="sxs-lookup"><span data-stu-id="104fc-118">Issue</span></span>

<span data-ttu-id="104fc-119">NuGet パッケージ マネージャーが表示されず、DotNetCLITools を追加または更新できません。</span><span class="sxs-lookup"><span data-stu-id="104fc-119">NuGet Package Manager does not display and does not allow add/update of DotNetCLITools.</span></span> [<span data-ttu-id="104fc-120">NuGet#4256</span><span class="sxs-lookup"><span data-stu-id="104fc-120">NuGet#4256</span></span>](https://github.com/NuGet/Home/issues/4256)

#### <a name="workaround"></a><span data-ttu-id="104fc-121">回避策</span><span class="sxs-lookup"><span data-stu-id="104fc-121">Workaround</span></span>

<span data-ttu-id="104fc-122">DotNetCLIToolReferences はプロジェクト ファイルで手動編集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="104fc-122">DotNetCLIToolReferences must be manually edited in your project file.</span></span>

### <a name="retargeting-target-framework-version-may-lead-to-incomplete-intellisense"></a><span data-ttu-id="104fc-123">ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になる</span><span class="sxs-lookup"><span data-stu-id="104fc-123">Retargeting target framework version may lead to incomplete Intellisense</span></span>

#### <a name="issue"></a><span data-ttu-id="104fc-124">懸案事項</span><span class="sxs-lookup"><span data-stu-id="104fc-124">Issue</span></span>

<span data-ttu-id="104fc-125">Visual Studio では、ターゲット フレームワーク バージョンを再ターゲットすると、IntelliSense が不完全になることがあります。</span><span class="sxs-lookup"><span data-stu-id="104fc-125">Retargeting target framework version may lead to incomplete Intellisense, in Visual Studio.</span></span> <span data-ttu-id="104fc-126">これは、パッケージ マネージャー形式として PackageReferences を使用しているときに発生します。</span><span class="sxs-lookup"><span data-stu-id="104fc-126">This happens when you are using PackageReferences as the package manager format.</span></span> [<span data-ttu-id="104fc-127">NuGet#4216</span><span class="sxs-lookup"><span data-stu-id="104fc-127">NuGet#4216</span></span>](https://github.com/NuGet/Home/issues/4216)

#### <a name="workaround"></a><span data-ttu-id="104fc-128">回避策</span><span class="sxs-lookup"><span data-stu-id="104fc-128">Workaround</span></span>

<span data-ttu-id="104fc-129">手動で復元します。</span><span class="sxs-lookup"><span data-stu-id="104fc-129">Do a manual restore.</span></span>

### <a name="a-package-in-a-net-core-project-that-contains-an-assembly-with-an-invalid-signature-can-trigger-an-infinite-restore-loop"></a><span data-ttu-id="104fc-130">署名が無効なアセンブリを含む .NET Core プロジェクトのパッケージは無限の復元ループを始動させることがある</span><span class="sxs-lookup"><span data-stu-id="104fc-130">A package in a .NET Core project that contains an assembly with an invalid signature, can trigger an infinite restore loop</span></span>

#### <a name="issue"></a><span data-ttu-id="104fc-131">懸案事項</span><span class="sxs-lookup"><span data-stu-id="104fc-131">Issue</span></span>

<span data-ttu-id="104fc-132">無効な署名付きのアセンブリを含むパッケージを使用するとき、あるいはパッケージ バージョンに 'DateTime' ティッカーが設定されているとき、パッケージの復元が無限ループで実行されることがあります (dotnet/project-system#1457)。</span><span class="sxs-lookup"><span data-stu-id="104fc-132">Occasionally, when you use a package that contains an assembly with an invalid signature or when the package version is set with 'DateTime' ticker, it causes the package auto-restore to run in an infinite loop (dotnet/project-system#1457).</span></span>

#### <a name="workaround"></a><span data-ttu-id="104fc-133">回避策</span><span class="sxs-lookup"><span data-stu-id="104fc-133">Workaround</span></span>

<span data-ttu-id="104fc-134">この問題の回避策はありません。</span><span class="sxs-lookup"><span data-stu-id="104fc-134">There is no workaround at this time.</span></span>

## <a name="issues-fixed-in-nuget-44-rtm-timeframe"></a><span data-ttu-id="104fc-135">NuGet 4.4 RTM の時間枠で修正された問題</span><span class="sxs-lookup"><span data-stu-id="104fc-135">Issues fixed in NuGet 4.4 RTM timeframe</span></span>

<span data-ttu-id="104fc-136">[NuGet 4.3 RTM のリリース ノート](../release-notes/nuget-4.3-RTM.md) - NuGet 4.3 RTM で修正されたすべての問題が掲載されています</span><span class="sxs-lookup"><span data-stu-id="104fc-136">[NuGet 4.3 RTM Release Notes](../release-notes/nuget-4.3-RTM.md) - Lists all the issues fixed for NuGet 4.3 RTM</span></span>

### <a name="features"></a><span data-ttu-id="104fc-137">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="104fc-137">Features</span></span>

- <span data-ttu-id="104fc-138">PMC および NuGet PM UI のシナリオでのライトウェイト ソリューション ロードのサポート - [#5180](https://github.com/NuGet/Home/issues/5180)</span><span class="sxs-lookup"><span data-stu-id="104fc-138">Support for Lightweight Solution Load in PMC and NuGet PM UI scenarios - [#5180](https://github.com/NuGet/Home/issues/5180)</span></span>

- <span data-ttu-id="104fc-139">MSBuild パック ターゲットには、それ自体の前にユーザー ターゲットを実行するためのパブリック フックを含める必要があります - [#5143](https://github.com/NuGet/Home/issues/5143)</span><span class="sxs-lookup"><span data-stu-id="104fc-139">The msbuild pack target should have a public hook for running user targets before itself - [#5143](https://github.com/NuGet/Home/issues/5143)</span></span>

- <span data-ttu-id="104fc-140">機能: nuget install に dependencyVersion スイッチを追加します - [#1806](https://github.com/NuGet/Home/issues/1806)</span><span class="sxs-lookup"><span data-stu-id="104fc-140">Feature: Add dependencyVersion switch to nuget install - [#1806](https://github.com/NuGet/Home/issues/1806)</span></span>

- <span data-ttu-id="104fc-141">uap10.0.TODO.0 は .NET Standard 2.0 for NuGet にマップする必要があります - [#5684](https://github.com/NuGet/Home/issues/5684)</span><span class="sxs-lookup"><span data-stu-id="104fc-141">uap10.0.TODO.0 should map to .NET Standard 2.0 for NuGet - [#5684](https://github.com/NuGet/Home/issues/5684)</span></span>

- <span data-ttu-id="104fc-142">Visual Studio Build Tools SKU と msbuild /t:restore をサポートします - [#5562](https://github.com/NuGet/Home/issues/5562)</span><span class="sxs-lookup"><span data-stu-id="104fc-142">Support Visual Studio Build Tools SKU with msbuild /t:restore - [#5562](https://github.com/NuGet/Home/issues/5562)</span></span>

- <span data-ttu-id="104fc-143">復元中、.NET Standard 2.0 用の .NET 4.6.1 のサポートが必要な場合、それがインストールされていないと、エラーを生成されます - [#5325](https://github.com/NuGet/Home/issues/5325)</span><span class="sxs-lookup"><span data-stu-id="104fc-143">During restore, generate an error if .NET 4.6.1 support for .NET Standard 2.0 is required but not installed - [#5325](https://github.com/NuGet/Home/issues/5325)</span></span>

- <span data-ttu-id="104fc-144">パッケージ ID プレフィックス予約クライアント UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span><span class="sxs-lookup"><span data-stu-id="104fc-144">Package ID prefix reservation client UI - [#5572](https://github.com/NuGet/Home/issues/5572)</span></span>

- <span data-ttu-id="104fc-145">dotnet.exe のローカライズをサポートするためにローカライズされた NuGet コンポーネントを提供します - [#4336](https://github.com/NuGet/Home/issues/4336)</span><span class="sxs-lookup"><span data-stu-id="104fc-145">deliver localized nuget components to support dotnet.exe localization - [#4336](https://github.com/NuGet/Home/issues/4336)</span></span>

### <a name="bugs"></a><span data-ttu-id="104fc-146">バグ</span><span class="sxs-lookup"><span data-stu-id="104fc-146">Bugs</span></span>

- <span data-ttu-id="104fc-147">プロジェクト パスの大文字/小文字の指定が異なると、復元において PackageReferences が失われる可能性があります - [#5855](https://github.com/NuGet/Home/issues/5855)</span><span class="sxs-lookup"><span data-stu-id="104fc-147">Different project path casings can cause restore to lose PackageReferences - [#5855](https://github.com/NuGet/Home/issues/5855)</span></span>

- <span data-ttu-id="104fc-148">警告番号を持つエラー コードがエラー範囲に移動されます - [#5824](https://github.com/NuGet/Home/issues/5824)</span><span class="sxs-lookup"><span data-stu-id="104fc-148">Move error codes with warning numbers to error range - [#5824](https://github.com/NuGet/Home/issues/5824)</span></span>

- <span data-ttu-id="104fc-149">.NET Standard バージョンがターゲット フレームワークと互換性がないことが判明すると、誤ったエラーが返されます - [#5818](https://github.com/NuGet/Home/issues/5818)</span><span class="sxs-lookup"><span data-stu-id="104fc-149">Misleading error when .NET Standard version is not known to be compatible with target framework  - [#5818](https://github.com/NuGet/Home/issues/5818)</span></span>

- <span data-ttu-id="104fc-150">テスト ファイルに混乱を招くライセンスが含まれています - [#5776](https://github.com/NuGet/Home/issues/5776)</span><span class="sxs-lookup"><span data-stu-id="104fc-150">Test files with confusing licenses - [#5776](https://github.com/NuGet/Home/issues/5776)</span></span>

- <span data-ttu-id="104fc-151">EndToEnd テスト テンプレートでライセンス ヘッダーが欠落しています - [#5774](https://github.com/NuGet/Home/issues/5774)</span><span class="sxs-lookup"><span data-stu-id="104fc-151">Missing license headers in EndToEnd test templates - [#5774](https://github.com/NuGet/Home/issues/5774)</span></span>

- <span data-ttu-id="104fc-152">packages.config restore でエラーが NU1000 として表示されます - [#5743](https://github.com/NuGet/Home/issues/5743)</span><span class="sxs-lookup"><span data-stu-id="104fc-152">packages.config restore shows errors as NU1000 - [#5743](https://github.com/NuGet/Home/issues/5743)</span></span>

- <span data-ttu-id="104fc-153">nuget.exe install には Mono に対する DisableParallelProcessing が含まれている必要があります - [#5741](https://github.com/NuGet/Home/issues/5741)</span><span class="sxs-lookup"><span data-stu-id="104fc-153">nuget.exe install should have DisableParallelProcessing on mono - [#5741](https://github.com/NuGet/Home/issues/5741)</span></span>

- <span data-ttu-id="104fc-154">nuget.exe install でキャッシュが誤って無効にされます - [#5737](https://github.com/NuGet/Home/issues/5737)</span><span class="sxs-lookup"><span data-stu-id="104fc-154">nuget.exe install incorrectly disables caching - [#5737](https://github.com/NuGet/Home/issues/5737)</span></span>

- <span data-ttu-id="104fc-155">VS: 復元が無効になっているときに packages.config の restore コマンドを実行すると、誤ったメッセージが表示されます - [#5718](https://github.com/NuGet/Home/issues/5718)</span><span class="sxs-lookup"><span data-stu-id="104fc-155">VS Running the restore command for packages.config when Restore is disabled displays incorrect message  - [#5718](https://github.com/NuGet/Home/issues/5718)</span></span>

- <span data-ttu-id="104fc-156">VS: 復元が無効になっているときに復元コマンドを実行すると、混乱を招くメッセージが表示されます - [#5659](https://github.com/NuGet/Home/issues/5659)</span><span class="sxs-lookup"><span data-stu-id="104fc-156">VS; Running the restore command when Restore is disabled displays a confusing message - [#5659](https://github.com/NuGet/Home/issues/5659)</span></span>

- <span data-ttu-id="104fc-157">バージョンのメタデータが欠落していると、GetRestoreDotnetCliToolsTask が失敗します - [#5716](https://github.com/NuGet/Home/issues/5716)</span><span class="sxs-lookup"><span data-stu-id="104fc-157">GetRestoreDotnetCliToolsTask fails when missing version metadata - [#5716](https://github.com/NuGet/Home/issues/5716)</span></span>

- <span data-ttu-id="104fc-158">dotnet</span><span class="sxs-lookup"><span data-stu-id="104fc-158">dotnet</span></span>
  - <span data-ttu-id="104fc-159">dotnetcore add package によって csproj から空の行が消去される場合があります - [#5697](https://github.com/NuGet/Home/issues/5697)</span><span class="sxs-lookup"><span data-stu-id="104fc-159">dotnetcore add package can clear empty lines from a csproj  - [#5697](https://github.com/NuGet/Home/issues/5697)</span></span>

- <span data-ttu-id="104fc-160">NuGet.Config の資格情報設定のソース名に大文字小文字の区別があります - [#5695](https://github.com/NuGet/Home/issues/5695)</span><span class="sxs-lookup"><span data-stu-id="104fc-160">Source names of credential settings in NuGet.Config are case sensitive - [#5695](https://github.com/NuGet/Home/issues/5695)</span></span>

- <span data-ttu-id="104fc-161">GeneratePackageOnBuild を有効にすることにより、パッケージの履歴全体が削除されました - [#5676](https://github.com/NuGet/Home/issues/5676)</span><span class="sxs-lookup"><span data-stu-id="104fc-161">Enabling GeneratePackageOnBuild deleted my entire history of packages - [#5676](https://github.com/NuGet/Home/issues/5676)</span></span>

- <span data-ttu-id="104fc-162">復元において、mono.cecil パッケージまたは semver パッケージが復元されません。ただし、その他のパッケージはすべて復元されます。</span><span class="sxs-lookup"><span data-stu-id="104fc-162">Restore will not restore mono.cecil or semver packages, but all other packages get restored.</span></span><span data-ttu-id="104fc-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span><span class="sxs-lookup"><span data-stu-id="104fc-163"> - [#5649](https://github.com/NuGet/Home/issues/5649)</span></span>

- <span data-ttu-id="104fc-164">エラーと警告 - ソースが使用できない状態で不適切なエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="104fc-164">Errors and Warnings - bad error when a source in unavailable.</span></span><span data-ttu-id="104fc-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span><span class="sxs-lookup"><span data-stu-id="104fc-165">  - [#5644](https://github.com/NuGet/Home/issues/5644)</span></span>

- <span data-ttu-id="104fc-166">[DesignConsistency] NuGet インストールのステータス テキストが現在のところ、ダーク テーマで適切に表示されません。</span><span class="sxs-lookup"><span data-stu-id="104fc-166">[DesignConsistency] NuGet Installation status text doesn’t look correct on dark theme currently.</span></span><span data-ttu-id="104fc-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span><span class="sxs-lookup"><span data-stu-id="104fc-167"> - [#5642](https://github.com/NuGet/Home/issues/5642)</span></span>

- <span data-ttu-id="104fc-168">ソリューションの更新/インストール時にすべてのプロジェクトについてパッケージが更新されます - [#5508](https://github.com/NuGet/Home/issues/5508)</span><span class="sxs-lookup"><span data-stu-id="104fc-168">Update packages at solution updates/installs for all the projects - [#5508](https://github.com/NuGet/Home/issues/5508)</span></span>

- <span data-ttu-id="104fc-169">dotnet</span><span class="sxs-lookup"><span data-stu-id="104fc-169">dotnet</span></span>
  - <span data-ttu-id="104fc-170">TargetFramework と TargetFrameworks によって、dotnetcore pack の動作が異なります - [#5281](https://github.com/NuGet/Home/issues/5281)</span><span class="sxs-lookup"><span data-stu-id="104fc-170">dotnetcore pack behaves differently depending on TargetFramework vs TargetFrameworks - [#5281](https://github.com/NuGet/Home/issues/5281)</span></span>

- <span data-ttu-id="104fc-171">ツール フォルダーに含まれている DLL により、警告がスローされます - [#5020](https://github.com/NuGet/Home/issues/5020)</span><span class="sxs-lookup"><span data-stu-id="104fc-171">Included DLLs inside Tools folder throw warnings - [#5020](https://github.com/NuGet/Home/issues/5020)</span></span>

- <span data-ttu-id="104fc-172">NuGet.ContentModel が文字列操作で過度のメモリを消費します - [#4714](https://github.com/NuGet/Home/issues/4714)</span><span class="sxs-lookup"><span data-stu-id="104fc-172">NuGet.ContentModel consumes too much memory for string operations - [#4714](https://github.com/NuGet/Home/issues/4714)</span></span>

- <span data-ttu-id="104fc-173">RuntimeEnvironmentHelper.IsLinux が OSX に対して true を返します - [#4648](https://github.com/NuGet/Home/issues/4648)</span><span class="sxs-lookup"><span data-stu-id="104fc-173">RuntimeEnvironmentHelper.IsLinux returns true for OSX - [#4648](https://github.com/NuGet/Home/issues/4648)</span></span>

- <span data-ttu-id="104fc-174">'dotnet pack' が obj\Debug ではなく obj の下に nuspec を配置します - [#4644](https://github.com/NuGet/Home/issues/4644)</span><span class="sxs-lookup"><span data-stu-id="104fc-174">'dotnet pack' puts nuspec under obj instead of obj\Debug - [#4644](https://github.com/NuGet/Home/issues/4644)</span></span>

- <span data-ttu-id="104fc-175">NuGet でのパッケージのアップグレードが極端に遅くなります - [#4534](https://github.com/NuGet/Home/issues/4534)</span><span class="sxs-lookup"><span data-stu-id="104fc-175">Nuget extremely slow package upgrade - [#4534](https://github.com/NuGet/Home/issues/4534)</span></span>

- <span data-ttu-id="104fc-176">LSL (ライトウェイト ソリューション復元) をオンにしていない大規模なソリューションで、CPS と Restore が同期しません - [#4307](https://github.com/NuGet/Home/issues/4307)</span><span class="sxs-lookup"><span data-stu-id="104fc-176">CPS out of sync with Restore with larger solutions that haven't turned on LSL (lightweight solution restore) - [#4307](https://github.com/NuGet/Home/issues/4307)</span></span>

- <span data-ttu-id="104fc-177">SemVer 2.0 - 指定したバージョンの NuGet パックがメタデータを無視します (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span><span class="sxs-lookup"><span data-stu-id="104fc-177">SemVer 2.0 - nuget pack with provided version ignores metadata (3.5.0-rtm-1938) - [#3643](https://github.com/NuGet/Home/issues/3643)</span></span>

- <span data-ttu-id="104fc-178">Version 番号と ExcludeVersion フラグが指定された nuget.exe (3.+) インストール パッケージがパッケージを新しいバージョンに更新しません - [#2405](https://github.com/NuGet/Home/issues/2405)</span><span class="sxs-lookup"><span data-stu-id="104fc-178">Nuget.exe (3.+) install package with Version number and ExcludeVersion flag doesn't update package to newer version - [#2405](https://github.com/NuGet/Home/issues/2405)</span></span>

- <span data-ttu-id="104fc-179">最上位のパッケージが制約に違反したときに、Project.json restore で警告が生成されます - [#2358](https://github.com/NuGet/Home/issues/2358)</span><span class="sxs-lookup"><span data-stu-id="104fc-179">Project.json restore should warn when top-level packages violate constraints - [#2358](https://github.com/NuGet/Home/issues/2358)</span></span>

- <span data-ttu-id="104fc-180">install コマンド上で -ConfigFile がカスタム構成を設定しません - [#1646](https://github.com/NuGet/Home/issues/1646)</span><span class="sxs-lookup"><span data-stu-id="104fc-180">-ConfigFile is not setting custom config on install command - [#1646](https://github.com/NuGet/Home/issues/1646)</span></span>

- <span data-ttu-id="104fc-181">nuget.exe install で '-DisableParallelProcessing' スイッチが受け入れられません - [#1556](https://github.com/NuGet/Home/issues/1556)</span><span class="sxs-lookup"><span data-stu-id="104fc-181">nuget.exe install does not honor '-DisableParallelProcessing' switch - [#1556](https://github.com/NuGet/Home/issues/1556)</span></span>

- <span data-ttu-id="104fc-182">無効にされたソースが DotNet.exe または msbuild.exe でまだ使用されています - [#5704](https://github.com/NuGet/Home/issues/5704)</span><span class="sxs-lookup"><span data-stu-id="104fc-182">Disabled sources still used by DotNet.exe or msbuild.exe - [#5704](https://github.com/NuGet/Home/issues/5704)</span></span>

- <span data-ttu-id="104fc-183">LSL シナリオでのハングアップの修正 - [#5685](https://github.com/NuGet/Home/issues/5685)</span><span class="sxs-lookup"><span data-stu-id="104fc-183">Fix hangs in LSL scenario - [#5685](https://github.com/NuGet/Home/issues/5685)</span></span>

### <a name="dcrs"></a><span data-ttu-id="104fc-184">DCR</span><span class="sxs-lookup"><span data-stu-id="104fc-184">DCRs</span></span>

- <span data-ttu-id="104fc-185">nuget.exe install による TargetFramework のサポート - [#5736](https://github.com/NuGet/Home/issues/5736)</span><span class="sxs-lookup"><span data-stu-id="104fc-185">nuget.exe install TargetFramework support - [#5736](https://github.com/NuGet/Home/issues/5736)</span></span>

- <span data-ttu-id="104fc-186">異なる msbuild タスク UserAgent 文字列の追加 (netcore 対 desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span><span class="sxs-lookup"><span data-stu-id="104fc-186">Add different msbuild task UserAgent strings (netcore vs desktop msbuild) - [#5709](https://github.com/NuGet/Home/issues/5709)</span></span>

- <span data-ttu-id="104fc-187">PackagePathResolver.GetPackageDirectoryName は仮想的なものである必要があります - [#5700](https://github.com/NuGet/Home/issues/5700)</span><span class="sxs-lookup"><span data-stu-id="104fc-187">PackagePathResolver.GetPackageDirectoryName should be virtual - [#5700](https://github.com/NuGet/Home/issues/5700)</span></span>

- <span data-ttu-id="104fc-188">[DesignConsistency] NuGet パッケージを追加したときの混乱を招くメッセージ[#5641](https://github.com/NuGet/Home/issues/5641)</span><span class="sxs-lookup"><span data-stu-id="104fc-188">[DesignConsistency] Confusing message when adding a NuGet package - [#5641](https://github.com/NuGet/Home/issues/5641)</span></span>

- <span data-ttu-id="104fc-189">[警告とエラー] NoWarn が P2P 参照を介して推移的にフローしません - [#5501](https://github.com/NuGet/Home/issues/5501)</span><span class="sxs-lookup"><span data-stu-id="104fc-189">[Warnings and errors] NoWarn does not flow transitively through P2P references - [#5501](https://github.com/NuGet/Home/issues/5501)</span></span>

- <span data-ttu-id="104fc-190">ライトウェイト ソリューション ロード: PM UI、PMC、および IV 用の Common Core - [#5057](https://github.com/NuGet/Home/issues/5057)</span><span class="sxs-lookup"><span data-stu-id="104fc-190">Lightweight Solution Load: Common Core for PM UI, PMC, and IVs- - [#5057](https://github.com/NuGet/Home/issues/5057)</span></span>

- <span data-ttu-id="104fc-191">ライトウェイト ソリューション ロード: サポート - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span><span class="sxs-lookup"><span data-stu-id="104fc-191">Lightweight Solution Load: Support - PMC - [#5053](https://github.com/NuGet/Home/issues/5053)</span></span>

- <span data-ttu-id="104fc-192">Visual Studio がトリガーする復元前の MSBuild ターゲットのサポートが追加されます - [#4781](https://github.com/NuGet/Home/issues/4781)</span><span class="sxs-lookup"><span data-stu-id="104fc-192">Add support for pre-restore MSBuild target that Visual Studio triggers - [#4781](https://github.com/NuGet/Home/issues/4781)</span></span>

- <span data-ttu-id="104fc-193">BeforeTargets を使用して参照可能な NuGet.targets にパブリック ターゲットを追加します - [#4634](https://github.com/NuGet/Home/issues/4634)</span><span class="sxs-lookup"><span data-stu-id="104fc-193">Add a public target to NuGet.targets that can be referenced using BeforeTargets - [#4634](https://github.com/NuGet/Home/issues/4634)</span></span>

- <span data-ttu-id="104fc-194">パック ターゲットがビルド アクションで contentFiles を正常に作成できません - [#4166](https://github.com/NuGet/Home/issues/4166)</span><span class="sxs-lookup"><span data-stu-id="104fc-194">Pack target can't create contentFiles with build actions correctly - [#4166](https://github.com/NuGet/Home/issues/4166)</span></span>

- <span data-ttu-id="104fc-195">RestoreOperationLogger.Do によってスレッド プール スレッドがブロックされます - [#5663](https://github.com/NuGet/Home/issues/5663)</span><span class="sxs-lookup"><span data-stu-id="104fc-195">RestoreOperationLogger.Do blocks thread pool threads - [#5663](https://github.com/NuGet/Home/issues/5663)</span></span>

### <a name="docs"></a><span data-ttu-id="104fc-196">Docs</span><span class="sxs-lookup"><span data-stu-id="104fc-196">Docs</span></span>

- <span data-ttu-id="104fc-197">Install コマンドの DependencyVersion フラグおよび Framework フラグに関するドキュメント - [#5858](https://github.com/NuGet/Home/issues/5858)</span><span class="sxs-lookup"><span data-stu-id="104fc-197">Docs for Install command DependencyVersion and Framework flags - [#5858](https://github.com/NuGet/Home/issues/5858)</span></span>

- <span data-ttu-id="104fc-198">NuGet の警告およびエラーに関するドキュメントに対する更新 - [#5857](https://github.com/NuGet/Home/issues/5857)</span><span class="sxs-lookup"><span data-stu-id="104fc-198">Update to docs on NuGet warnings and errors - [#5857](https://github.com/NuGet/Home/issues/5857)</span></span>

## <a name="links-to-github-issues-fixed-in-44-rtm"></a><span data-ttu-id="104fc-199">4.4 RTM で修正された GitHub の懸案事項へのリンク</span><span class="sxs-lookup"><span data-stu-id="104fc-199">Links to GitHub issues fixed in 4.4 RTM</span></span>

[<span data-ttu-id="104fc-200">懸案事項リスト 1</span><span class="sxs-lookup"><span data-stu-id="104fc-200">Issues List 1</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:"4.4")

[<span data-ttu-id="104fc-201">懸案事項リスト 2</span><span class="sxs-lookup"><span data-stu-id="104fc-201">Issues List 2</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F31+through+8%2F18%22)

[<span data-ttu-id="104fc-202">懸案事項リスト 3</span><span class="sxs-lookup"><span data-stu-id="104fc-202">Issues List 3</span></span>](https://github.com/NuGet/Home/issues?q=is:issue+is:closed+milestone:%224.4+-+7%2F10+through+7%2F28%22)
