---
title: NuGet 5.9 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.9 のリリースノート。
author: erdembayar
ms.author: eryondon
ms.date: 3/11/2021
ms.topic: conceptual
ms.openlocfilehash: 24933ebb51851da2583b03e7fd3e55fade5e8a18
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859529"
---
# <a name="nuget-59-release-notes"></a><span data-ttu-id="8c93a-103">NuGet 5.9 リリースノート</span><span class="sxs-lookup"><span data-stu-id="8c93a-103">NuGet 5.9 Release Notes</span></span>

<span data-ttu-id="8c93a-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="8c93a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="8c93a-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="8c93a-105">NuGet version</span></span> | <span data-ttu-id="8c93a-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="8c93a-106">Available in Visual Studio version</span></span> | <span data-ttu-id="8c93a-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8c93a-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="8c93a-108">**5.9**</span><span class="sxs-lookup"><span data-stu-id="8c93a-108">**5.9**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="8c93a-109">Visual Studio 2019 バージョン16.9</span><span class="sxs-lookup"><span data-stu-id="8c93a-109">Visual Studio 2019 version 16.9</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="8c93a-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="8c93a-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="8c93a-111"><sup>1</sup> Visual Studio 2019 と .net Core ワークロードと共にインストールされる</span><span class="sxs-lookup"><span data-stu-id="8c93a-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="8c93a-112">Visual Studio 16.9、MSBuild 16.9、および .NET 5.0.3 + には NuGet.exe 5.9 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="8c93a-112">Visual Studio 16.9, MSBuild 16.9, and .NET 5.0.3+ requires NuGet.exe 5.9 or later.</span></span>

## <a name="summary-whats-new-in-59"></a><span data-ttu-id="8c93a-113">概要: 5.9 の新機能</span><span class="sxs-lookup"><span data-stu-id="8c93a-113">Summary: What's New in 5.9</span></span>

* <span data-ttu-id="8c93a-114">事前に選択されたパッケージを使用してパッケージマネージャーの UI を起動し、パッケージの依存関係の [更新] コンテキストメニュー項目を追加 [#10378](https://github.com/NuGet/Home/issues/10378)</span><span class="sxs-lookup"><span data-stu-id="8c93a-114">Add "Update" context menu item for package dependencies that launches Package Manager UI with preselected packages to update - [#10378](https://github.com/NuGet/Home/issues/10378)</span></span>

    ![パッケージの "更新" エクスペリエンスを右クリックします。](media/releasenotes-59-update.png)

* <span data-ttu-id="8c93a-116">ソリューションレベルパッケージマネージャー UI の [プロジェクト] リストの [バージョン] 列に、要求されたバージョン (フローティングバージョンまたはバージョン範囲の要求を含む) を表示し [#9827](https://github.com/NuGet/Home/issues/9827)</span><span class="sxs-lookup"><span data-stu-id="8c93a-116">Show the requested version (including floating version or version range request) in the "Version" column of the project list in the solution level Package Manager UI - [#9827](https://github.com/NuGet/Home/issues/9827)</span></span>

    ![ソリューションレベルのパッケージマネージャー UI で要求されたバージョン](media/releasenotes-59-requested-version.png)

* <span data-ttu-id="8c93a-118">パッケージマネージャー UI の IntelliCode パッケージの提案 A/B テスト[#10053](https://github.com/NuGet/Home/issues/10053)としてリリース</span><span class="sxs-lookup"><span data-stu-id="8c93a-118">IntelliCode package suggestions in the Package Manager UI Browse tab released as an A/B test - [#10053](https://github.com/NuGet/Home/issues/10053)</span></span>

* <span data-ttu-id="8c93a-119">`.nupkg.metadata`インストールソースを含むようにファイルを拡張する- [#10354](https://github.com/NuGet/Home/issues/10354)</span><span class="sxs-lookup"><span data-stu-id="8c93a-119">Extend the `.nupkg.metadata` file to include the installation source - [#10354](https://github.com/NuGet/Home/issues/10354)</span></span>

* <span data-ttu-id="8c93a-120">パックタスクの実行中に特定の TFMs のビルド出力を除外する新しい msbuild プロパティを導入する- [#10396](https://github.com/NuGet/Home/issues/10396)</span><span class="sxs-lookup"><span data-stu-id="8c93a-120">Introduce a new msbuild property to exclude build output for specific TFMs during pack task - [#10396](https://github.com/NuGet/Home/issues/10396)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="8c93a-121">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="8c93a-121">Issues fixed in this release</span></span>

<span data-ttu-id="8c93a-122">**DCRs (デザイン変更要求):**</span><span class="sxs-lookup"><span data-stu-id="8c93a-122">**DCRs(Design Change Request):**</span></span>

* <span data-ttu-id="8c93a-123">最新のパッケージバージョンがインストールされている場合、下位アイコンアイコンは直観的ではありません。</span><span class="sxs-lookup"><span data-stu-id="8c93a-123">The down icon icon when the latest package version is installed is not intuitive.</span></span> <span data-ttu-id="8c93a-124">以前の緑のティックは完全に [#9789](https://github.com/NuGet/Home/issues/9789)</span><span class="sxs-lookup"><span data-stu-id="8c93a-124">The old green tick was perfect - [#9789](https://github.com/NuGet/Home/issues/9789)</span></span>

* <span data-ttu-id="8c93a-125">Nuget デバッグの詳細度は、パッケージの送信元- [#3055](https://github.com/NuGet/Home/issues/3055)</span><span class="sxs-lookup"><span data-stu-id="8c93a-125">Nuget Debug verbosity should say where a package came from - [#3055](https://github.com/NuGet/Home/issues/3055)</span></span>

* <span data-ttu-id="8c93a-126">NuGet パックでは、バージョン番号にドットが含まれている誤った省略をキャッチする必要があり [#9215](https://github.com/NuGet/Home/issues/9215)</span><span class="sxs-lookup"><span data-stu-id="8c93a-126">NuGet pack should catch incorrect omitting of the dot in version numbers - [#9215](https://github.com/NuGet/Home/issues/9215)</span></span>

* <span data-ttu-id="8c93a-127">[CPVM]中央推移的な依存関係のピン留めを無効にする- [#10132](https://github.com/NuGet/Home/issues/10132)</span><span class="sxs-lookup"><span data-stu-id="8c93a-127">[CPVM] Disable pinning of the central transitive dependencies  - [#10132](https://github.com/NuGet/Home/issues/10132)</span></span>

* <span data-ttu-id="8c93a-128">net5 TFM: TFM- [#9441](https://github.com/NuGet/Home/issues/9441)がない場合にエラーを生成する</span><span class="sxs-lookup"><span data-stu-id="8c93a-128">net5 TFM: produce error when missing TPV - [#9441](https://github.com/NuGet/Home/issues/9441)</span></span>

* <span data-ttu-id="8c93a-129">復元ログ中にパッケージ contenthash をログに記録する (抽出中)- [#10384](https://github.com/NuGet/Home/issues/10384)</span><span class="sxs-lookup"><span data-stu-id="8c93a-129">Log package contenthash during restore logging (during extraction) - [#10384](https://github.com/NuGet/Home/issues/10384)</span></span>

* <span data-ttu-id="8c93a-130">ソリューションオープン[#9986](https://github.com/NuGet/Home/issues/9986)で復元を呼び出す従来の PR プロジェクトの事前登録メカニズムを実装する</span><span class="sxs-lookup"><span data-stu-id="8c93a-130">Implement a pre-registration mechanism for legacy PR projects that call restore at solution open - [#9986](https://github.com/NuGet/Home/issues/9986)</span></span>

* <span data-ttu-id="8c93a-131">パッケージマネージャーで複数のソースが選択されている場合は、NuGet パッケージレコメンダーを使用する必要があります- [#10433](https://github.com/NuGet/Home/issues/10433)</span><span class="sxs-lookup"><span data-stu-id="8c93a-131">NuGet package recommender should work when more than one source is selected in package manager - [#10433](https://github.com/NuGet/Home/issues/10433)</span></span>

* <span data-ttu-id="8c93a-132">通常の詳細度で復元する場合は、パッケージの復元元のソースをログに記録し [#10461](https://github.com/NuGet/Home/issues/10461)</span><span class="sxs-lookup"><span data-stu-id="8c93a-132">When restoring at normal verbosity, log which source a package is being restored from - [#10461](https://github.com/NuGet/Home/issues/10461)</span></span>

<span data-ttu-id="8c93a-133">**バグ**</span><span class="sxs-lookup"><span data-stu-id="8c93a-133">**Bugs:**</span></span>

* <span data-ttu-id="8c93a-134">INuGetPackageFileService-Codespaces とスタンドアロン[#10151](https://github.com/NuGet/Home/issues/10151)のイメージと埋め込みライセンスを取得します。</span><span class="sxs-lookup"><span data-stu-id="8c93a-134">INuGetPackageFileService - Fetch Images and embedded licenses for Codespaces-connected and standalone - [#10151](https://github.com/NuGet/Home/issues/10151)</span></span>

* <span data-ttu-id="8c93a-135">VS OE: IProjectMetadataContextInfo にフォーマッタがありません- [#10079](https://github.com/NuGet/Home/issues/10079)</span><span class="sxs-lookup"><span data-stu-id="8c93a-135">VS OE:  IProjectMetadataContextInfo missing formatter - [#10079](https://github.com/NuGet/Home/issues/10079)</span></span>

* <span data-ttu-id="8c93a-136">[CPVM-Perf][#10002](https://github.com/NuGet/Home/issues/10002) centralTransitiveDependencyGroups に書き込まれる情報を減らします。</span><span class="sxs-lookup"><span data-stu-id="8c93a-136">[CPVM-Perf] Reduce the information written to centralTransitiveDependencyGroups - [#10002](https://github.com/NuGet/Home/issues/10002)</span></span>

* <span data-ttu-id="8c93a-137">プロジェクトが読み込まれなかったことが原因でスローされる復元操作は `NoOp` 、テレメトリ- [#9985](https://github.com/NuGet/Home/issues/9985)として報告されます。</span><span class="sxs-lookup"><span data-stu-id="8c93a-137">Restore operations that throw due to a project not being loaded are reported as `NoOp` in telemetry - [#9985](https://github.com/NuGet/Home/issues/9985)</span></span>

* <span data-ttu-id="8c93a-138">特定のカラーパレットを持つアイコンにより、PM UI がクラッシュし [#10037](https://github.com/NuGet/Home/issues/10037)</span><span class="sxs-lookup"><span data-stu-id="8c93a-138">Icons with certain color pallets causes PM UI to crash VS - [#10037](https://github.com/NuGet/Home/issues/10037)</span></span>

* <span data-ttu-id="8c93a-139">[CPVM-Perf]CPVM 情報を追加するときに PackageSpec clone を減らす- [#10003](https://github.com/NuGet/Home/issues/10003)</span><span class="sxs-lookup"><span data-stu-id="8c93a-139">[CPVM-Perf] Reduce the PackageSpec clone when adding the CPVM information  - [#10003](https://github.com/NuGet/Home/issues/10003)</span></span>

* <span data-ttu-id="8c93a-140">PM UI-asyncify アイコン読み込み- [#10009](https://github.com/NuGet/Home/issues/10009)</span><span class="sxs-lookup"><span data-stu-id="8c93a-140">PM UI - asyncify icon loading - [#10009](https://github.com/NuGet/Home/issues/10009)</span></span>

* <span data-ttu-id="8c93a-141">PM UI でアイコンの Url を読み込むときの UI の遅延 [#8505](https://github.com/NuGet/Home/issues/8505)</span><span class="sxs-lookup"><span data-stu-id="8c93a-141">UI delay when loading icon URLs in PM UI - [#8505](https://github.com/NuGet/Home/issues/8505)</span></span>

* <span data-ttu-id="8c93a-142">BitmapSource と WPF UI スレッドでのスレッドアフィニティ- [#9161](https://github.com/NuGet/Home/issues/9161)</span><span class="sxs-lookup"><span data-stu-id="8c93a-142">Thread affinity in BitmapSource and WPF UI threads - [#9161](https://github.com/NuGet/Home/issues/9161)</span></span>

* <span data-ttu-id="8c93a-143">Packastool が[targetframework](https://github.com/NuGet/Home/issues/10097) framework NU5128 の場合の警告の警告</span><span class="sxs-lookup"><span data-stu-id="8c93a-143">Warning for warning NU5128 when packastool with targetframework alias - [#10097](https://github.com/NuGet/Home/issues/10097)</span></span>

* <span data-ttu-id="8c93a-144">カスタマイズされたビルドでの OutputPath logic in Pack ターゲットは正常に機能しません- [#9234](https://github.com/NuGet/Home/issues/9234)</span><span class="sxs-lookup"><span data-stu-id="8c93a-144">OutputPath logic in Pack targets in a customized build doesn't work properly - [#9234](https://github.com/NuGet/Home/issues/9234)</span></span>

* <span data-ttu-id="8c93a-145">VS OE: クライアント[#10141](https://github.com/NuGet/Home/issues/10141)での IServiceBroker インスタンスのキャッシュ</span><span class="sxs-lookup"><span data-stu-id="8c93a-145">VS OE:  cache IServiceBroker instance on client - [#10141](https://github.com/NuGet/Home/issues/10141)</span></span>

* <span data-ttu-id="8c93a-146">PM UI からのアンインストールの NuGetProjectActions を作成する並列操作- [#9956](https://github.com/NuGet/Home/issues/9956)</span><span class="sxs-lookup"><span data-stu-id="8c93a-146">Make creating NuGetProjectActions for uninstall  from PM UI a parallel operation - [#9956](https://github.com/NuGet/Home/issues/9956)</span></span>

* <span data-ttu-id="8c93a-147">パフォーマンス: 従来のプロジェクトおよび PR 以外のプロジェクトのために、Uide を使用して Get/Async を縮小する方法については、 [#9953](https://github.com/NuGet/Home/issues/9953)</span><span class="sxs-lookup"><span data-stu-id="8c93a-147">Performance: Reduce UIDelays in GetPackageSpecsAsync for Legacy projects and non PR projects - [#9953](https://github.com/NuGet/Home/issues/9953)</span></span>

* <span data-ttu-id="8c93a-148">``dotnet nuget push *.nupkg``複数のファイル[#4393](https://github.com/NuGet/Home/issues/4393)をプッシュしません。</span><span class="sxs-lookup"><span data-stu-id="8c93a-148">``dotnet nuget push *.nupkg`` doesn't push more than one file - [#4393](https://github.com/NuGet/Home/issues/4393)</span></span>

* <span data-ttu-id="8c93a-149">リダイレクトされると、出力は macOS で80文字でラップされ [#10198](https://github.com/NuGet/Home/issues/10198)</span><span class="sxs-lookup"><span data-stu-id="8c93a-149">Output is wrapped at 80 characters on macOS when redirected - [#10198](https://github.com/NuGet/Home/issues/10198)</span></span>

* <span data-ttu-id="8c93a-150">-Source #9406 で復元が失敗する <Relative Path>  -  [](https://github.com/NuGet/Home/issues/9406)</span><span class="sxs-lookup"><span data-stu-id="8c93a-150">Restore fails with -Source <Relative Path> - [#9406](https://github.com/NuGet/Home/issues/9406)</span></span>

* <span data-ttu-id="8c93a-151">netcoreapp 5.0-windows はラウンドトリップせず、プラットフォーム情報を解析しません- [#10177](https://github.com/NuGet/Home/issues/10177)</span><span class="sxs-lookup"><span data-stu-id="8c93a-151">netcoreapp5.0-windows does not round trip and does not parse platform information - [#10177](https://github.com/NuGet/Home/issues/10177)</span></span>

* <span data-ttu-id="8c93a-152">カスタム CPS プロジェクトを復元するには、AssemblyReferences プロジェクト機能が必要です。</span><span class="sxs-lookup"><span data-stu-id="8c93a-152">Custom CPS projects require AssemblyReferences project capability in order to restore.</span></span><span data-ttu-id="8c93a-153"> - [#8071](https://github.com/NuGet/Home/issues/8071)</span><span class="sxs-lookup"><span data-stu-id="8c93a-153"> - [#8071](https://github.com/NuGet/Home/issues/8071)</span></span>

* <span data-ttu-id="8c93a-154">ライセンスとアイコンファイルの存在チェックでは、常に大文字と小文字を区別する比較を使用する必要があり [#9817](https://github.com/NuGet/Home/issues/9817)</span><span class="sxs-lookup"><span data-stu-id="8c93a-154">License and icon file existence check should always use a case-sensitive comparison - [#9817](https://github.com/NuGet/Home/issues/9817)</span></span>

* <span data-ttu-id="8c93a-155">DotnetCLiToolReference の復元では、no op プロジェクトの数/uptodateprojectscount- [#10038](https://github.com/NuGet/Home/issues/10038)</span><span class="sxs-lookup"><span data-stu-id="8c93a-155">DotnetCLiToolReference restores make it difficult to reason about no-op projects count/uptodateprojectscount - [#10038](https://github.com/NuGet/Home/issues/10038)</span></span>

* <span data-ttu-id="8c93a-156">ダークテーマで [NuGet パッケージマネージャーの形式を選択] ダイアログボックスを使用して移動するときに、パッケージ形式のダッシュラインボックスを表示するのは困難です。 [#9729](https://github.com/NuGet/Home/issues/9729)</span><span class="sxs-lookup"><span data-stu-id="8c93a-156">Hard to see the dash-line box of package format when navigating by tab through the “Choose NuGet Package Manager Format” dialog in Dark theme - [#9729](https://github.com/NuGet/Home/issues/9729)</span></span>

* <span data-ttu-id="8c93a-157">#10314 からの推移的なフレームワーク参照を除外する `CollectFrameworkReferences`  -  [](https://github.com/NuGet/Home/issues/10314)</span><span class="sxs-lookup"><span data-stu-id="8c93a-157">Exclude transitive framework references from `CollectFrameworkReferences` - [#10314](https://github.com/NuGet/Home/issues/10314)</span></span>

* <span data-ttu-id="8c93a-158">比較子の静的プロパティはべき等 [#10339](https://github.com/NuGet/Home/issues/10339)</span><span class="sxs-lookup"><span data-stu-id="8c93a-158">Comparer static properties should be idempotent  - [#10339](https://github.com/NuGet/Home/issues/10339)</span></span>

* <span data-ttu-id="8c93a-159">内部コントラクトアセンブリの読み込みの解決 (RPS の修正または例外の取得)- [#9919](https://github.com/NuGet/Home/issues/9919)</span><span class="sxs-lookup"><span data-stu-id="8c93a-159">resolve internal contracts assembly loading (fix RPS or get exception) - [#9919](https://github.com/NuGet/Home/issues/9919)</span></span>

* <span data-ttu-id="8c93a-160">GetService を GetServiceAsync に置き換え、パート 1- [#10362](https://github.com/NuGet/Home/issues/10362)</span><span class="sxs-lookup"><span data-stu-id="8c93a-160">Replace GetService with GetServiceAsync in NuGet.Clients, Part 1 - [#10362](https://github.com/NuGet/Home/issues/10362)</span></span>

* <span data-ttu-id="8c93a-161">インストールされていないパッケージをインストールすることはできません- [#7466](https://github.com/NuGet/Home/issues/7466)</span><span class="sxs-lookup"><span data-stu-id="8c93a-161">CLI installs should not install unlisted packages - [#7466](https://github.com/NuGet/Home/issues/7466)</span></span>

* <span data-ttu-id="8c93a-162">静的 msbuild グラフ復元- [#10335](https://github.com/NuGet/Home/issues/10335) MSBuildStartupDirectory に関する必要なログ記録の解除</span><span class="sxs-lookup"><span data-stu-id="8c93a-162">Static msbuild graph restore - unnnecessary logging about MSBuildStartupDirectory - [#10335](https://github.com/NuGet/Home/issues/10335)</span></span>

* <span data-ttu-id="8c93a-163">PrivateAssets とマークされている ProjectReferences のプロジェクトの依存関係は、[最新の情報に更新するまでロックファイルに含めないでください。 [#8565](https://github.com/NuGet/Home/issues/8565)</span><span class="sxs-lookup"><span data-stu-id="8c93a-163">Project Dependencies of ProjectReferences marked as PrivateAssets should not be included in the lock file up to date check - [#8565](https://github.com/NuGet/Home/issues/8565)</span></span>

* <span data-ttu-id="8c93a-164">無効なデータを含む SDK プロジェクトは、VS- [#10406](https://github.com/NuGet/Home/issues/10406)に復元エラーが表示されない</span><span class="sxs-lookup"><span data-stu-id="8c93a-164">SDK projects with bad data not showing restore errors in VS - [#10406](https://github.com/NuGet/Home/issues/10406)</span></span>

* <span data-ttu-id="8c93a-165">NU1004 と netstandard2 プロジェクトが混在しているソリューションを[#9623](https://github.com/NuGet/Home/issues/9623) LockedMode を使用して cmd 行から復元する場合の</span><span class="sxs-lookup"><span data-stu-id="8c93a-165">NU1004 when restoring a solution that has mixed Legacy and netstandard2 projects from cmd line with LockedMode - [#9623](https://github.com/NuGet/Home/issues/9623)</span></span>

* <span data-ttu-id="8c93a-166">パッケージには、依存関係パッケージを通じて現在のプロジェクトのパッケージに取り込まれたコンテンツが含まれます (SDK ベースのプロジェクトのみ)- [#8867](https://github.com/NuGet/Home/issues/8867)</span><span class="sxs-lookup"><span data-stu-id="8c93a-166">Pack includes content brought in through dependency packages into the current project's package (SDK based projects only) - [#8867](https://github.com/NuGet/Home/issues/8867)</span></span>

* <span data-ttu-id="8c93a-167">NuGet の VS 機能拡張 API エラーのテレメトリを追加する- [#10062](https://github.com/NuGet/Home/issues/10062)</span><span class="sxs-lookup"><span data-stu-id="8c93a-167">Add telemetry for NuGet's VS extensibility API faults - [#10062](https://github.com/NuGet/Home/issues/10062)</span></span>

* <span data-ttu-id="8c93a-168">デバッグ機能を向上させるために、静的なグラフの復元で GenerateRestoreGraphFile を追加します。</span><span class="sxs-lookup"><span data-stu-id="8c93a-168">Add GenerateRestoreGraphFile in static graph restore to improve debugability.</span></span><span data-ttu-id="8c93a-169">  - [#10365](https://github.com/NuGet/Home/issues/10365)</span><span class="sxs-lookup"><span data-stu-id="8c93a-169">  - [#10365](https://github.com/NuGet/Home/issues/10365)</span></span>

* <span data-ttu-id="8c93a-170">NuGet パッケージマネージャーを開くことができません- [#10336](https://github.com/NuGet/Home/issues/10336)</span><span class="sxs-lookup"><span data-stu-id="8c93a-170">Cannot open the NuGet Package manager - [#10336](https://github.com/NuGet/Home/issues/10336)</span></span>

* <span data-ttu-id="8c93a-171">NVDA/ナレーターは、"Apache-2.0" リンク[#10425](https://github.com/NuGet/Home/issues/10425)の "ライセンス" ラベルを読み取っていません</span><span class="sxs-lookup"><span data-stu-id="8c93a-171">NVDA/Narrator is not reading "License" label for "Apache-2.0" link - [#10425](https://github.com/NuGet/Home/issues/10425)</span></span>

* <span data-ttu-id="8c93a-172">最新のステータスバーメッセージは、VS [#9402](https://github.com/NuGet/Home/issues/9402)では十分ではありません</span><span class="sxs-lookup"><span data-stu-id="8c93a-172">The up to date status bar message is not great in VS - [#9402](https://github.com/NuGet/Home/issues/9402)</span></span>

* <span data-ttu-id="8c93a-173">の packages.config package.lock.jsは不適切なターゲットフレームワークを使用して [#10257](https://github.com/NuGet/Home/issues/10257)</span><span class="sxs-lookup"><span data-stu-id="8c93a-173">packages.config package.lock.json uses an incorrect target framework - [#10257](https://github.com/NuGet/Home/issues/10257)</span></span>

* <span data-ttu-id="8c93a-174">Codespaces: #10439 からテレメトリを修正します https://github.com/NuGet/NuGet.Client/pull/3786  -  [](https://github.com/NuGet/Home/issues/10439)</span><span class="sxs-lookup"><span data-stu-id="8c93a-174">Codespaces:  fix telemetry from https://github.com/NuGet/NuGet.Client/pull/3786 - [#10439](https://github.com/NuGet/Home/issues/10439)</span></span>

* <span data-ttu-id="8c93a-175">"RestoreLockedMode"- [#8973](https://github.com/NuGet/Home/issues/8973)を有効にした後にソリューションをビルドすると、エラー NU1004 が消えます</span><span class="sxs-lookup"><span data-stu-id="8c93a-175">Error NU1004 disappears when building solution after enabling “RestoreLockedMode” - [#8973](https://github.com/NuGet/Home/issues/8973)</span></span>

* <span data-ttu-id="8c93a-176">逆方向の PMUI を使用して tab キーを移動すると、前方の方向がミラー化され [#10234](https://github.com/NuGet/Home/issues/10234)</span><span class="sxs-lookup"><span data-stu-id="8c93a-176">Tabbing through PMUI in the reverse should mirror forward direction - [#10234](https://github.com/NuGet/Home/issues/10234)</span></span>

* <span data-ttu-id="8c93a-177">実験用インスタンスで PMUI をデバッグすると、SolutionView から ProjectView [#10416](https://github.com/NuGet/Home/issues/10416)に InvalidCastException がスローされることがある</span><span class="sxs-lookup"><span data-stu-id="8c93a-177">Debugging PMUI in Experimental Instance sometimes throws InvalidCastException from SolutionView to ProjectView - [#10416](https://github.com/NuGet/Home/issues/10416)</span></span>

* <span data-ttu-id="8c93a-178">既定のバージョンは、[参照] タブで非推奨のパッケージをクリックすると null になり [#10380](https://github.com/NuGet/Home/issues/10380)</span><span class="sxs-lookup"><span data-stu-id="8c93a-178">The default version is null after clicking a deprecated package in Browse tab - [#10380](https://github.com/NuGet/Home/issues/10380)</span></span>

* <span data-ttu-id="8c93a-179">Visual Studio の NuGet マネージャーは、フォーカスが再度表示されたときに再読み込みを行い [#4176](https://github.com/NuGet/Home/issues/4176)</span><span class="sxs-lookup"><span data-stu-id="8c93a-179">The NuGet manager in Visual Studio reloads when focus is regained - [#4176](https://github.com/NuGet/Home/issues/4176)</span></span>

* <span data-ttu-id="8c93a-180">IPackageSourceProvider2 と関連する型の削除- [#10098](https://github.com/NuGet/Home/issues/10098)</span><span class="sxs-lookup"><span data-stu-id="8c93a-180">Remove IPackageSourceProvider2 and related types - [#10098](https://github.com/NuGet/Home/issues/10098)</span></span>

* <span data-ttu-id="8c93a-181">パッケージ ' NameOfPackage ' は、プロジェクト内の ' all ' フレームワークと互換性がありません- [#5127](https://github.com/NuGet/Home/issues/5127)</span><span class="sxs-lookup"><span data-stu-id="8c93a-181">Package 'NameOfPackage' is incompatible with 'all' frameworks in project - [#5127](https://github.com/NuGet/Home/issues/5127)</span></span>

* <span data-ttu-id="8c93a-182">CreateVersionsAsync が不要な NuGetVersion を比較する- [#10436](https://github.com/NuGet/Home/issues/10436)</span><span class="sxs-lookup"><span data-stu-id="8c93a-182">CreateVersionsAsync does unnecessary NuGetVersion Compares - [#10436](https://github.com/NuGet/Home/issues/10436)</span></span>

* <span data-ttu-id="8c93a-183">NuGet。クライアントは ManagedImageMonikers と KnownMonikers を使用して置き換える必要があります- [#9977](https://github.com/NuGet/Home/issues/9977)</span><span class="sxs-lookup"><span data-stu-id="8c93a-183">NuGet.Client should replace using of ManagedImageMonikers with KnownMonikers - [#9977](https://github.com/NuGet/Home/issues/9977)</span></span>

* <span data-ttu-id="8c93a-184">非推奨のアイコンは、[参照] タブで非推奨のパッケージのバージョンと重複しています- [#10452](https://github.com/NuGet/Home/issues/10452)</span><span class="sxs-lookup"><span data-stu-id="8c93a-184">The deprecated icon overlaps with the version of the deprecated package in Browse tab - [#10452](https://github.com/NuGet/Home/issues/10452)</span></span>

* <span data-ttu-id="8c93a-185">PackageReference NU1604 のエラー処理は VS とコマンドラインで異なります (Restore & Package Manager UI)- [#9289](https://github.com/NuGet/Home/issues/9289)</span><span class="sxs-lookup"><span data-stu-id="8c93a-185">PackageReference NU1604 error handling is different across VS and command line (Restore & Package Manager UI) - [#9289](https://github.com/NuGet/Home/issues/9289)</span></span>

* <span data-ttu-id="8c93a-186">Codespaces: 必要なフォーマッタが登録されていません- [#10467](https://github.com/NuGet/Home/issues/10467)</span><span class="sxs-lookup"><span data-stu-id="8c93a-186">Codespaces:  necessary formatters not registered - [#10467](https://github.com/NuGet/Home/issues/10467)</span></span>

* <span data-ttu-id="8c93a-187">Net45 からターゲットフレームワークとしてを削除します[#10470](https://github.com/NuGet/Home/issues/10470) 。</span><span class="sxs-lookup"><span data-stu-id="8c93a-187">Remove net45 as as a target framework from NuGet.Frameworks - [#10470](https://github.com/NuGet/Home/issues/10470)</span></span>

* <span data-ttu-id="8c93a-188">実装-新しいテレメトリを追加して、PMC と Powershell の使用状況に関連するイベントを追跡します。</span><span class="sxs-lookup"><span data-stu-id="8c93a-188">Implementation - Add new telemetries to track events related to PMC and Powershell usage.</span></span><span data-ttu-id="8c93a-189"> - [#10142](https://github.com/NuGet/Home/issues/10142)</span><span class="sxs-lookup"><span data-stu-id="8c93a-189"> - [#10142](https://github.com/NuGet/Home/issues/10142)</span></span>

* <span data-ttu-id="8c93a-190">パッケージマネージャー UI で更新できるパッケージが複数ある場合、[変更のプレビュー] ウィンドウに表示されるパッケージは1つだけです [#10483](https://github.com/NuGet/Home/issues/10483)</span><span class="sxs-lookup"><span data-stu-id="8c93a-190">Only one package shows in the Preview Changes window when there are multiple packages available to update in the Package Manager UI - [#10483](https://github.com/NuGet/Home/issues/10483)</span></span>

* <span data-ttu-id="8c93a-191">複数の対象を持つプロジェクトをパッキングする場合は、空の frameworkReferences グループを生成する必要があり [#10218](https://github.com/NuGet/Home/issues/10218)</span><span class="sxs-lookup"><span data-stu-id="8c93a-191">Empty frameworkReferences groups should be generated when packing multitargeted projects - [#10218](https://github.com/NuGet/Home/issues/10218)</span></span>

* <span data-ttu-id="8c93a-192">[更新] タブでパッケージのチェックボックスが表示されるのは、青い/Blue (エクストラコントラスト)/明るいテーマを使用してタブ間を移動するときに、ダッシュラインボックスを使用することです。 [#8963](https://github.com/NuGet/Home/issues/8963)</span><span class="sxs-lookup"><span data-stu-id="8c93a-192">Hard to see the check-box of package in ‘Updates’ Tab is focused with a dash-line box when navigating through Tab in Blue/Blue (Extra Contrast)/Light themes - [#8963](https://github.com/NuGet/Home/issues/8963)</span></span>

* <span data-ttu-id="8c93a-193">[更新] タブのチェックボックスは、スクリーンリーダーでは適切に機能しません- [#10449](https://github.com/NuGet/Home/issues/10449)</span><span class="sxs-lookup"><span data-stu-id="8c93a-193">Updates Tab checkboxes do not work well with screen-readers - [#10449](https://github.com/NuGet/Home/issues/10449)</span></span>

* <span data-ttu-id="8c93a-194">PMUI で更新すると、オブジェクト参照がオブジェクトのインスタンスに設定されません- [#9882](https://github.com/NuGet/Home/issues/9882)</span><span class="sxs-lookup"><span data-stu-id="8c93a-194">Updating in PMUI causes Object reference not set to an instance of an object - [#9882](https://github.com/NuGet/Home/issues/9882)</span></span>

* <span data-ttu-id="8c93a-195">実装-新しいテレメトリを追加して、PMC と Powershell の使用状況に関連するイベントを追跡します。</span><span class="sxs-lookup"><span data-stu-id="8c93a-195">Implementation - Add new telemetries to track events related to PMC and Powershell usage follow up.</span></span><span data-ttu-id="8c93a-196"> - [#10478](https://github.com/NuGet/Home/issues/10478)</span><span class="sxs-lookup"><span data-stu-id="8c93a-196"> - [#10478](https://github.com/NuGet/Home/issues/10478)</span></span>

* <span data-ttu-id="8c93a-197">[#10480](https://github.com/NuGet/Home/issues/10480) V2FeedPackageInfo でのコピー/貼り付けエラー</span><span class="sxs-lookup"><span data-stu-id="8c93a-197">Copy-paste error in V2FeedPackageInfo - [#10480](https://github.com/NuGet/Home/issues/10480)</span></span>

* <span data-ttu-id="8c93a-198">NuGetPackageFileService fix-を使用して破棄可能な memorystream を使用する- [#10503](https://github.com/NuGet/Home/issues/10503)</span><span class="sxs-lookup"><span data-stu-id="8c93a-198">NuGetPackageFileService fix - use using for disposable memorystream - [#10503](https://github.com/NuGet/Home/issues/10503)</span></span>


<span data-ttu-id="8c93a-199">**[このリリースで修正されるすべての問題の一覧-5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**</span><span class="sxs-lookup"><span data-stu-id="8c93a-199">**[List of all issues fixed in this release - 5.9.0](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f6be8c10485c0236b7ef889)**</span></span>

<span data-ttu-id="8c93a-200">**[このリリースのコミットの一覧-5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**</span><span class="sxs-lookup"><span data-stu-id="8c93a-200">**[List of commits in this release - 5.9.0](https://github.com/NuGet/NuGet.Client/compare/5.8.1.7021...5.9.0.7134)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="8c93a-201">コミュニティからの投稿</span><span class="sxs-lookup"><span data-stu-id="8c93a-201">Community contributions</span></span>

<span data-ttu-id="8c93a-202">この NuGet のリリースに役立ったすべての共同作成者に感謝します。</span><span class="sxs-lookup"><span data-stu-id="8c93a-202">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="8c93a-203">担当者</span><span class="sxs-lookup"><span data-stu-id="8c93a-203">Who</span></span>|<span data-ttu-id="8c93a-204">Pr</span><span class="sxs-lookup"><span data-stu-id="8c93a-204">PRs</span></span>|<span data-ttu-id="8c93a-205">発行</span><span class="sxs-lookup"><span data-stu-id="8c93a-205">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="8c93a-206">omajid</span><span class="sxs-lookup"><span data-stu-id="8c93a-206">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="8c93a-207">3865</span><span class="sxs-lookup"><span data-stu-id="8c93a-207">3865</span></span>](https://github.com/NuGet/NuGet.Client/pull/3865) | <span data-ttu-id="8c93a-208">[#10480](https://github.com/NuGet/Home/issues/10480) V2FeedPackageInfo でのコピー/貼り付けエラー</span><span class="sxs-lookup"><span data-stu-id="8c93a-208">Copy-paste error in V2FeedPackageInfo - [#10480](https://github.com/NuGet/Home/issues/10480)</span></span>
[<span data-ttu-id="8c93a-209">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="8c93a-209">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="8c93a-210">3812</span><span class="sxs-lookup"><span data-stu-id="8c93a-210">3812</span></span>](https://github.com/NuGet/NuGet.Client/pull/3812) | <span data-ttu-id="8c93a-211">PrivateAssets = "All" 属性でパッケージが参照されているケースのテストがありません- [#10397](https://github.com/NuGet/Home/issues/10397)</span><span class="sxs-lookup"><span data-stu-id="8c93a-211">Missing tests for the case where packages are referenced with PrivateAssets="All" attribute - [#10397](https://github.com/NuGet/Home/issues/10397)</span></span>
[<span data-ttu-id="8c93a-212">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="8c93a-212">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="8c93a-213">3739</span><span class="sxs-lookup"><span data-stu-id="8c93a-213">3739</span></span>](https://github.com/NuGet/NuGet.Client/pull/3739) | <span data-ttu-id="8c93a-214">複数のパッケージをプッシュするためのサポートを追加する- [#4393](https://github.com/NuGet/Home/issues/4393)</span><span class="sxs-lookup"><span data-stu-id="8c93a-214">Adding support for pushing multiple packages - [#4393](https://github.com/NuGet/Home/issues/4393)</span></span>
[<span data-ttu-id="8c93a-215">marcin-krystianc</span><span class="sxs-lookup"><span data-stu-id="8c93a-215">marcin-krystianc</span></span>](https://github.com/marcin-krystianc) | [<span data-ttu-id="8c93a-216">3723</span><span class="sxs-lookup"><span data-stu-id="8c93a-216">3723</span></span>](https://github.com/NuGet/NuGet.Client/pull/3723) | <span data-ttu-id="8c93a-217">アセンブリの署名が無効になっていると、NuGet ライブラリのビルドが破損する- [#10173](https://github.com/NuGet/Home/issues/10173)</span><span class="sxs-lookup"><span data-stu-id="8c93a-217">Build of NuGet libraries is broken when assembly signing is disabled - [#10173](https://github.com/NuGet/Home/issues/10173)</span></span>
[<span data-ttu-id="8c93a-218">kant2002</span><span class="sxs-lookup"><span data-stu-id="8c93a-218">kant2002</span></span>](https://github.com/kant2002) | [<span data-ttu-id="8c93a-219">3807</span><span class="sxs-lookup"><span data-stu-id="8c93a-219">3807</span></span>](https://github.com/NuGet/NuGet.Client/pull/3807) | <span data-ttu-id="8c93a-220">貢献するドキュメントをクリーンアップする- [#10399](https://github.com/NuGet/Home/issues/10399)</span><span class="sxs-lookup"><span data-stu-id="8c93a-220">Clean-up the contributing docs - [#10399](https://github.com/NuGet/Home/issues/10399)</span></span>
[<span data-ttu-id="8c93a-221">PathogenDavid</span><span class="sxs-lookup"><span data-stu-id="8c93a-221">PathogenDavid</span></span>](https://github.com/PathogenDavid) | [<span data-ttu-id="8c93a-222">3754</span><span class="sxs-lookup"><span data-stu-id="8c93a-222">3754</span></span>](https://github.com/NuGet/NuGet.Client/pull/3754) | <span data-ttu-id="8c93a-223">ライセンスとアイコンファイルの存在チェックでは、常に大文字と小文字を区別する比較を使用する必要があり [#9817](https://github.com/NuGet/Home/issues/9817)</span><span class="sxs-lookup"><span data-stu-id="8c93a-223">License and icon file existence check should always use a case-sensitive comparison - [#9817](https://github.com/NuGet/Home/issues/9817)</span></span>
[<span data-ttu-id="8c93a-224">campersau</span><span class="sxs-lookup"><span data-stu-id="8c93a-224">campersau</span></span>](https://github.com/campersau) | [<span data-ttu-id="8c93a-225">3677</span><span class="sxs-lookup"><span data-stu-id="8c93a-225">3677</span></span>](https://github.com/NuGet/NuGet.Client/pull/3677) | <span data-ttu-id="8c93a-226">DecodePixelWidth を使用するときに IgnoreColorProfile を使用して WPF の問題を回避するには[#10037](https://github.com/NuGet/Home/issues/10037) 、BitmapCreateOptions. を使用します。</span><span class="sxs-lookup"><span data-stu-id="8c93a-226">Use BitmapCreateOptions.IgnoreColorProfile to workaround WPF issue when using DecodePixelWidth - [#10037](https://github.com/NuGet/Home/issues/10037)</span></span>
[<span data-ttu-id="8c93a-227">bjorkstromm</span><span class="sxs-lookup"><span data-stu-id="8c93a-227">bjorkstromm</span></span>](https://github.com/bjorkstromm) | [<span data-ttu-id="8c93a-228">3697</span><span class="sxs-lookup"><span data-stu-id="8c93a-228">3697</span></span>](https://github.com/NuGet/NuGet.Client/pull/3697) | <span data-ttu-id="8c93a-229">Windows SDK 10 リンクが NuGet で破損しています。クライアント貢献ガイド- [#10099](https://github.com/NuGet/Home/issues/10099)</span><span class="sxs-lookup"><span data-stu-id="8c93a-229">Windows SDK 10 link is broken in NuGet.Client Contribution guide - [#10099](https://github.com/NuGet/Home/issues/10099)</span></span>
[<span data-ttu-id="8c93a-230">bjorkstromm</span><span class="sxs-lookup"><span data-stu-id="8c93a-230">bjorkstromm</span></span>](https://github.com/bjorkstromm) | [<span data-ttu-id="8c93a-231">3696</span><span class="sxs-lookup"><span data-stu-id="8c93a-231">3696</span></span>](https://github.com/NuGet/NuGet.Client/pull/3696) | <span data-ttu-id="8c93a-232">NuGet で相対リンクが破損しています。クライアントデバッグガイド- [#10100](https://github.com/NuGet/Home/issues/10100)</span><span class="sxs-lookup"><span data-stu-id="8c93a-232">Relative links are broken in NuGet.Client debugging guide - [#10100](https://github.com/NuGet/Home/issues/10100)</span></span>
[<span data-ttu-id="8c93a-233">Nirmal4G</span><span class="sxs-lookup"><span data-stu-id="8c93a-233">Nirmal4G</span></span>](https://github.com/Nirmal4G) | [<span data-ttu-id="8c93a-234">3637</span><span class="sxs-lookup"><span data-stu-id="8c93a-234">3637</span></span>](https://github.com/NuGet/NuGet.Client/pull/3637) | <span data-ttu-id="8c93a-235">テストフィクスチャと関連コードの向上- [#9996](https://github.com/NuGet/Home/issues/9996)</span><span class="sxs-lookup"><span data-stu-id="8c93a-235">Improve test fixtures and related code - [#9996](https://github.com/NuGet/Home/issues/9996)</span></span>
[<span data-ttu-id="8c93a-236">rolfbjarne</span><span class="sxs-lookup"><span data-stu-id="8c93a-236">rolfbjarne</span></span>](https://github.com/rolfbjarne) | [<span data-ttu-id="8c93a-237">3743</span><span class="sxs-lookup"><span data-stu-id="8c93a-237">3743</span></span>](https://github.com/NuGet/NuGet.Client/pull/3743) | <span data-ttu-id="8c93a-238">リダイレクトされると、出力は macOS で80文字でラップされ [#10198](https://github.com/NuGet/Home/issues/10198)</span><span class="sxs-lookup"><span data-stu-id="8c93a-238">Output is wrapped at 80 characters on macOS when redirected - [#10198](https://github.com/NuGet/Home/issues/10198)</span></span>
[<span data-ttu-id="8c93a-239">xen2</span><span class="sxs-lookup"><span data-stu-id="8c93a-239">xen2</span></span>](https://github.com/xen2) | [<span data-ttu-id="8c93a-240">2861</span><span class="sxs-lookup"><span data-stu-id="8c93a-240">2861</span></span>](https://github.com/NuGet/NuGet.Client/pull/2861) | <span data-ttu-id="8c93a-241">Nuget.exe を .NET Standard パッケージとして使用できるようにする- [#6150](https://github.com/NuGet/Home/issues/6150)</span><span class="sxs-lookup"><span data-stu-id="8c93a-241">Make NuGet.PackageManagement available as a .NET Standard package - [#6150](https://github.com/NuGet/Home/issues/6150)</span></span>
[<span data-ttu-id="8c93a-242">Anipik</span><span class="sxs-lookup"><span data-stu-id="8c93a-242">Anipik</span></span>](https://github.com/Anipik) | [<span data-ttu-id="8c93a-243">3810</span><span class="sxs-lookup"><span data-stu-id="8c93a-243">3810</span></span>](https://github.com/NuGet/NuGet.Client/pull/3810) | <span data-ttu-id="8c93a-244">パックタスクの実行中に特定の tfm のビルド出力を除外する新しい msbuild プロパティを導入する- [#10396](https://github.com/NuGet/Home/issues/10396)</span><span class="sxs-lookup"><span data-stu-id="8c93a-244">Introduce a new msbuild property to exclude build output for specific tfms during pack task - [#10396](https://github.com/NuGet/Home/issues/10396)</span></span>

## <a name="feedback-welcome"></a><span data-ttu-id="8c93a-245">フィードバックの開始</span><span class="sxs-lookup"><span data-stu-id="8c93a-245">Feedback welcome</span></span>

<span data-ttu-id="8c93a-246">お客様のフィードバックは Microsoft にとって重要です。</span><span class="sxs-lookup"><span data-stu-id="8c93a-246">Your feedback is important to us.</span></span>  <span data-ttu-id="8c93a-247">このリリースに問題がある場合は、GitHub の [問題](https://github.com/NuGet/Home/issues) と [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) で既存の問題を確認してください。</span><span class="sxs-lookup"><span data-stu-id="8c93a-247">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="8c93a-248">NuGet 内の新しい問題については、 [GitHub の問題](https://github.com/NuGet/Home/issues/new)を報告してください。</span><span class="sxs-lookup"><span data-stu-id="8c93a-248">For new issues within NuGet, please report a [GitHub Issue](https://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="8c93a-249">NuGet エクスペリエンスに関する一般的な問題については、[**ヘルプ > [問題の報告**] の下にあるお気に入りの IDE の [[問題点の報告](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] オプションを使用してお知らせください。</span><span class="sxs-lookup"><span data-stu-id="8c93a-249">For general NuGet experience issues, let us know via the [Report a Problem](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
