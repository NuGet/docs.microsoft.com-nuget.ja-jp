---
title: NuGet 5.0 RTM リリースノート
description: 既知の問題、バグ修正、新機能、および DCRs を含む NuGet 5.0 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: e4a6be7fb26e3cc4bd297eaf02999f6ac1389b77
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236803"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="a2c7a-103">NuGet 5.0 リリースノート</span><span class="sxs-lookup"><span data-stu-id="a2c7a-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="a2c7a-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="a2c7a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a2c7a-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="a2c7a-105">NuGet version</span></span> | <span data-ttu-id="a2c7a-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="a2c7a-106">Available in Visual Studio version</span></span>| <span data-ttu-id="a2c7a-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a2c7a-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="a2c7a-108">**5.0.0**</span><span class="sxs-lookup"><span data-stu-id="a2c7a-108">**5.0.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a2c7a-109">Visual Studio 2019 バージョン 16.0</span><span class="sxs-lookup"><span data-stu-id="a2c7a-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a2c7a-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a2c7a-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |
| [<span data-ttu-id="a2c7a-111">**5.0.2**</span><span class="sxs-lookup"><span data-stu-id="a2c7a-111">**5.0.2**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a2c7a-112">Visual Studio 2019 バージョン16.0.4</span><span class="sxs-lookup"><span data-stu-id="a2c7a-112">Visual Studio 2019 version 16.0.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a2c7a-113">[2.1.60 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.20 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a2c7a-113">[2.1.60X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.20X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="a2c7a-114"><sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="a2c7a-115"><sup>2</sup>.NET Core ワークロードを含む Visual Studio 2019 を使用したオプションのインストールとして利用可能</span><span class="sxs-lookup"><span data-stu-id="a2c7a-115"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="a2c7a-116">概要: 5.0 の新機能</span><span class="sxs-lookup"><span data-stu-id="a2c7a-116">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="a2c7a-117">Visual Studio 2019 での [フィルター選択](/visualstudio/ide/filtered-solutions?view=vs-2019) されたソリューションの復元のサポート- [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-117">Support for restoring [filtered solutions](/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* <span data-ttu-id="a2c7a-118">`BuildTransitive` フォルダーを使用すると、パッケージのターゲット/プロパティをホストプロジェクトに推移的に投稿でき [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-118">`BuildTransitive` folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="a2c7a-119">NuGet Iv Api での PackageReference シナリオのサポートの向上- [#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-119">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* <span data-ttu-id="a2c7a-120">`nuget.exe pack project.json` は非推奨とされました- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-120">`nuget.exe pack project.json` has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="a2c7a-121">Gen 1 Credential Provider プラグインは [gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) に置き換えられており、まもなく非推奨となりました- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-121">Gen 1 Credential Provider plugin has been superseded by [Gen 2](../reference/extensibility/nuget-cross-platform-authentication-plugin.md) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a2c7a-122">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="a2c7a-122">Issues fixed in this release</span></span>

<span data-ttu-id="a2c7a-123">**バグ**</span><span class="sxs-lookup"><span data-stu-id="a2c7a-123">**Bugs**</span></span>

* <span data-ttu-id="a2c7a-124">NoOp 復元を実行する場合は、obj ディレクトリへの書き込み時に \* .dgspec.jsを避ける- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-124">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="a2c7a-125">~/.Nuget の内部で作成されたファイルのアクセス許可がオープン [#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-125">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* <span data-ttu-id="a2c7a-126">`dotnet list package --outdated` 認証を必要とするソースでは機能しません。 [#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-126">`dotnet list package --outdated` doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="a2c7a-127">VisualStudio IVsPackageInstaller-既定値が[#7005](https://github.com/NuGet/Home/issues/7005) PackageReference に設定されている場合でも、パッケージ参照のないプロジェクトでを呼び出すと、常に packages.config が使用されます。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-127">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="a2c7a-128">PMC: Update-Package の再インストールが、delisted パッケージで失敗します ("パッケージが見つかりません")。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-128">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="a2c7a-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-129"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="a2c7a-130">リポジトリと VSIX [#7409](https://github.com/NuGet/Home/issues/7409)にサードパーティの通知を追加する</span><span class="sxs-lookup"><span data-stu-id="a2c7a-130">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="a2c7a-131">VisualStudio のバージョンが指定されていない場合、IVsPackageInstaller は最新バージョンをインストールする必要があり [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-131">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="a2c7a-132">--dotnet nuget プッシュ[#7519](https://github.com/NuGet/Home/issues/7519)の対話形式のサポート</span><span class="sxs-lookup"><span data-stu-id="a2c7a-132">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="a2c7a-133">ロックファイルを使用して復元する場合、NU1603 warning を発生させることはできません。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-133">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="a2c7a-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-134"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="a2c7a-135">NuGet では、最小ログ記録を使用して復元中にプロジェクトパスを印刷しないようにする必要があり [#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-135">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="a2c7a-136">--dotnet remove パッケージ[#7727](https://github.com/NuGet/Home/issues/7727)の対話型サポート</span><span class="sxs-lookup"><span data-stu-id="a2c7a-136">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="a2c7a-137">TypeForwardedTo [#7768](https://github.com/NuGet/Home/issues/7768) attrs を使用してを追加します。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-137">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="a2c7a-138">plugins_cache が正常に機能するためには、短いパスが必要です。 [#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-138">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="a2c7a-139">ユーザーが特定の msbuild バージョンを要求しなかった場合に、msbuild 検出のパスを優先する- [#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-139">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* <span data-ttu-id="a2c7a-140">`nuget.exe /?` 正しい msbuild バージョンを一覧表示する必要があります- [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-140">`nuget.exe /?` should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="a2c7a-141">Nuget.exe (498, 5): エラー: パス '/tmp/NuGetScratch ' の一部が見つかりませんでした- [#7793](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="a2c7a-142">復元では、コンピューターキャッシュ内の参照されているパッケージのすべてのバージョンのコンテンツを不要に列挙します- [#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-142">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="a2c7a-143">VS 2019 Preview- [#7621](https://github.com/NuGet/Home/issues/7621)をインストールした後、MSBuild の自動検出では常に16.0 が選択されます。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-143">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="a2c7a-144">ソリューションの dotnet list パッケージは、フレームワーク[#7607](https://github.com/NuGet/Home/issues/7607)の重複したエントリを出力します</span><span class="sxs-lookup"><span data-stu-id="a2c7a-144">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="a2c7a-145">例外 "空のパス名は無効です" は、古いプロジェクトとパッケージフォルダーで IVsPackageInstaller を呼び出すと存在しません。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-145">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="a2c7a-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-146"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="a2c7a-147">msbuild/t: 最小の復元の詳細は、より少なくする必要があり [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-147">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="a2c7a-148">色の問題により、VS 16.0 の NuGet UI にタブが読み取られない- [#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-148">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="a2c7a-149">Nuget. Core & License.txt の説明- [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-149">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="a2c7a-150">型[#7596](https://github.com/NuGet/Home/issues/7596)を特定するために、不要な復元のグローバルパッケージフォルダーを復元します</span><span class="sxs-lookup"><span data-stu-id="a2c7a-150">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="a2c7a-151">ロックファイルの適用からのエラーはエラー一覧ウィンドウに表示される必要があります- [#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-151">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="a2c7a-152">NuGet.Configuration の問題を修正する- [#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-152">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="a2c7a-153">MSBuild に適合するインストール場所の更新- [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-153">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="a2c7a-154">Nuget.exe は開発の依存関係である必要があります- [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-154">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="a2c7a-155">デバッグシンボルを含むようにパック拡張ポイントを追加する- [#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-155">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="a2c7a-156">`dotnet pack` は、(浮動バージョンが使用されている場合でも) 作成された nupkg の依存関係バージョンの範囲を保持する必要があります。- [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-156">`dotnet pack` should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="a2c7a-157">`dotnet restore`ユーザーレベルの構成もソース[#7209](https://github.com/NuGet/Home/issues/7209)を持っている場合、認証されたソースで失敗する</span><span class="sxs-lookup"><span data-stu-id="a2c7a-157">`dotnet restore` fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="a2c7a-158">パックでは、コンテンツファイルに対する BuildActions のセットを制限しないでください。 [#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-158">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="a2c7a-159">AssetTargetFallback を成功させる必要がある ProjectReference を使用すると、警告が通知されます。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-159">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="a2c7a-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-160"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="a2c7a-161">CPS (CommonProjectSystem) の呼び出し時にスレッド処理の問題が原因でデッドロックが発生する- [#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-161">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="a2c7a-162">`dotnet add package` ローカル構成で指定されたソースのグローバル構成の資格情報を使用しません- [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-162">`dotnet add package` doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="a2c7a-163">非同期コードパスで MEF が呼び出されているスレッド処理の問題- [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-163">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="a2c7a-164">署名: エラーは呼び出し履歴を使用せずに2回報告されました- [#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-164">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="a2c7a-165">信頼されていない署名証明書を含む署名済みパッケージをインストールすると、エラー [#6318](https://github.com/NuGet/Home/issues/6318)が表示される</span><span class="sxs-lookup"><span data-stu-id="a2c7a-165">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="a2c7a-166">2つのプロジェクトが obj ディレクトリを共有している場合、NuGet の復元に誤りがありません- [#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-166">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="a2c7a-167">`dotnet restore`認証済みフィードからのパッケージを使用して Linux 上で PAT を使用することはできません- [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-167">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="a2c7a-168">コンピューター全体のフィード[#5410](https://github.com/NuGet/Home/issues/5410)が無効になっているため dotnet restore が失敗する</span><span class="sxs-lookup"><span data-stu-id="a2c7a-168">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="a2c7a-169">**DCR**</span><span class="sxs-lookup"><span data-stu-id="a2c7a-169">**DCRs**</span></span>

* <span data-ttu-id="a2c7a-170">"Dotnet pack project.json" が今後削除されることを警告する- [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-170">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="a2c7a-171">Gen1 credential プラグインの非推奨の警告を追加する- [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-171">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="a2c7a-172">署名: 有効にされたリポジトリは、署名されたリポジトリとしてのすべてのパッケージのクライアント検証を必要とします--via RepositorySignatures/5.0.0 リソース- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-172">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="a2c7a-173">NuGet.Config- [#4538](https://github.com/NuGet/Home/issues/4538)を使用して、ソースごとの http 要求番号を制限する</span><span class="sxs-lookup"><span data-stu-id="a2c7a-173">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="a2c7a-174">NuGet は Net472 をターゲットにする必要があります (VSIX の16.0 ビルドのクリーンアップに役立ちます)- [#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-174">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="a2c7a-175">PMC: OpenPackagePage コマンド[#7384](https://github.com/NuGet/Home/issues/7384)の削除</span><span class="sxs-lookup"><span data-stu-id="a2c7a-175">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="a2c7a-176">NetCoreApp 3.0 を NetStandard 2.1 にマップする- [#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-176">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="a2c7a-177">NuGet. \* パッケージに netstandard 2.0 サポートを追加する- [#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-177">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="a2c7a-178">パッケージ作成者がビルドアセットを定義できるようにする推移的な動作- [#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-178">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="a2c7a-179">VS 2019 ソリューションフィルター機能をサポートします。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-179">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="a2c7a-180">では、プロジェクトがソリューションに含まれていないか、プロジェクトがアンロードされています。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-180">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="a2c7a-181">最初の[#5820](https://github.com/NuGet/Home/issues/5820) (CLI または VS を使用) で完全なソリューションを復元する必要がある</span><span class="sxs-lookup"><span data-stu-id="a2c7a-181">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="a2c7a-182">.NET 4.7.2 を必要とする NuGet 5.0 アセンブリ (TFM change を使用)- [#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-182">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="a2c7a-183">NuGetLicenseData からのパッケージはパブリック型である必要があります。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-183">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="a2c7a-184">Spdx からライセンスメタデータ取り込まれたを更新します。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-184">Update license metadata ingested from spdx.</span></span><span data-ttu-id="a2c7a-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-185"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="a2c7a-186">古い設定の Api を削除する- [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-186">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="a2c7a-187">1 cpu- [#6742](https://github.com/NuGet/Home/issues/6742)のシステムでの復元タイムアウトの回避</span><span class="sxs-lookup"><span data-stu-id="a2c7a-187">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="a2c7a-188">NuGet.config-[構成の追加] オプションで資格情報がある場合でも、NuGet は NTLM 認証を優先します。資格情報の認証の種類をフィルター処理するには [#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-188">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="a2c7a-189">PackageReference の EmbedInteropTypes を有効にする (一致する Packages.Config 機能)- [#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-189">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

<span data-ttu-id="a2c7a-190">**[このリリース-5.0 RTM で修正されるすべての問題の一覧](https://github.com/NuGet/Home/milestone/84?closed=1)**</span><span class="sxs-lookup"><span data-stu-id="a2c7a-190">**[List of all issues fixed in this release - 5.0 RTM](https://github.com/NuGet/Home/milestone/84?closed=1)**</span></span>

## <a name="summary-whats-new-in-502"></a><span data-ttu-id="a2c7a-191">概要: 5.0.2 の新機能</span><span class="sxs-lookup"><span data-stu-id="a2c7a-191">Summary: What's New in 5.0.2</span></span>

* <span data-ttu-id="a2c7a-192">セキュリティ (dotnet.exe または mono.exe 経由で実行する場合)-obj フォルダーは正しいアクセス許可で作成する必要があり [#7908](https://github.com/NuGet/Home/issues/7908)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-192">Security (when run via dotnet.exe or mono.exe) - The obj folder should be created with correct permissions [#7908](https://github.com/NuGet/Home/issues/7908)</span></span>

* <span data-ttu-id="a2c7a-193">Mono/MacOS での nuget.exe の復元がカスタム nuget.config と `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)で失敗する</span><span class="sxs-lookup"><span data-stu-id="a2c7a-193">nuget.exe restore on mono/MacOS fails with custom nuget.config and `PackageSignatureValidity: False` [#8011](https://github.com/NuGet/Home/issues/8011)</span></span>


## <a name="known-issues"></a><span data-ttu-id="a2c7a-194">既知の問題</span><span class="sxs-lookup"><span data-stu-id="a2c7a-194">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414"></a><span data-ttu-id="a2c7a-195">.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-195">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="a2c7a-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="a2c7a-196"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="a2c7a-197">問題</span><span class="sxs-lookup"><span data-stu-id="a2c7a-197">Issue</span></span>
<span data-ttu-id="a2c7a-198">dotnet.exe 2.x を使って netcoreapp 1.x と netcoreapp 2.x をマルチターゲットにするプロジェクトを復元すると、そのフォールバック フォルダーがファイル フィードとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-198">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="a2c7a-199">つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-199">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="a2c7a-200">回避策</span><span class="sxs-lookup"><span data-stu-id="a2c7a-200">Workaround</span></span>
<span data-ttu-id="a2c7a-201">を nothing に設定することにより、フォールバックフォルダーの使用を無効にし `RestoreAdditionalProjectSources` ます。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-201">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="a2c7a-202">フォールバックフォルダーから復元されるパッケージは NuGet.org からダウンロードされるので、これは注意して使用してください。</span><span class="sxs-lookup"><span data-stu-id="a2c7a-202">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>