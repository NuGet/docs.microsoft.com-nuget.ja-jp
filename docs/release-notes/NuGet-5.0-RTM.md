---
title: NuGet 5.0 RTM リリース ノート
description: 既知の問題、バグの修正、新機能、および Dcr を含む NuGet 5.0 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 04/02/2019
ms.topic: conceptual
ms.openlocfilehash: 5e48ff19ea5c4908d7eb0a3cb19a31b738e348eb
ms.sourcegitcommit: 8793f528a11bd8e8fb229cd12e9abba50d61e104
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/04/2019
ms.locfileid: "58921586"
---
# <a name="nuget-50-release-notes"></a><span data-ttu-id="438ae-103">NuGet 5.0 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="438ae-103">NuGet 5.0 Release Notes</span></span>

<span data-ttu-id="438ae-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="438ae-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="438ae-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="438ae-105">NuGet version</span></span> | <span data-ttu-id="438ae-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="438ae-106">Available in Visual Studio version</span></span>| <span data-ttu-id="438ae-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="438ae-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [**<span data-ttu-id="438ae-108">5.0.0</span><span class="sxs-lookup"><span data-stu-id="438ae-108">5.0.0</span></span>**](https://nuget.org/downloads) | [<span data-ttu-id="438ae-109">Visual Studio 2019 バージョン 16.0</span><span class="sxs-lookup"><span data-stu-id="438ae-109">Visual Studio 2019 version 16.0</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="438ae-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="438ae-110">[2.1.602](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.202](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="438ae-111"><sup>1</sup>.NET Core ワークロードと共に Visual Studio 2019 のインストール</span><span class="sxs-lookup"><span data-stu-id="438ae-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="438ae-112"><sup>2</sup>.NET Core ワークロードと共に Visual Studio 2019 と省略可能なインストールとして利用可能</span><span class="sxs-lookup"><span data-stu-id="438ae-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-50"></a><span data-ttu-id="438ae-113">概要:5.0 の新機能新機能</span><span class="sxs-lookup"><span data-stu-id="438ae-113">Summary: What's New in 5.0</span></span>

* <span data-ttu-id="438ae-114">復元するためのサポート[ソリューションをフィルター処理された](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019)で Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="438ae-114">Support for restoring [filtered solutions](https://docs.microsoft.com/en-us/visualstudio/ide/filtered-solutions?view=vs-2019) in Visual Studio 2019 - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>
* `BuildTransitive` <span data-ttu-id="438ae-115">フォルダーにより、パッケージをホスト プロジェクトのターゲット/プロパティを推移的に投稿する[#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="438ae-115">folder enables packages to transitively contribute targets/props to the host project - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>
* <span data-ttu-id="438ae-116">Iv api は NuGet の PackageReference シナリオのサポート強化[#7005](https://github.com/NuGet/Home/issues/7005)、 [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="438ae-116">Better support for PackageReference scenarios in NuGet IVs APIs - [#7005](https://github.com/NuGet/Home/issues/7005), [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>
* `nuget.exe pack project.json` <span data-ttu-id="438ae-117">非推奨 - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="438ae-117">has been deprecated - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
* <span data-ttu-id="438ae-118">Gen 1 の資格情報プロバイダー プラグインに置き換えられました[Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin)は間もなく非推奨 - [#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="438ae-118">Gen 1 Credential Provider plugin has been superseded by [Gen 2](https://aka.ms/nuget-cross-platform-authentication-plugin) and will soon be deprecated - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>

## <a name="issues-fixed-in-this-release"></a><span data-ttu-id="438ae-119">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="438ae-119">Issues fixed in this release</span></span>

**<span data-ttu-id="438ae-120">バグ</span><span class="sxs-lookup"><span data-stu-id="438ae-120">Bugs</span></span>**

* <span data-ttu-id="438ae-121">NoOp 復元を行うときに避ける \*. obj ディレクトリ - dgspec.json 書き込み[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="438ae-121">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="438ae-122">~/.Nuget 内で作成されたファイルに対するアクセス許可が開きすぎる[#7673](https://github.com/NuGet/Home/issues/7673)</span><span class="sxs-lookup"><span data-stu-id="438ae-122">Permissions on files created inside ~/.nuget are too open - [#7673](https://github.com/NuGet/Home/issues/7673)</span></span>

* `dotnet list package --outdated` <span data-ttu-id="438ae-123">認証 - の必要なソースを使用しない[#7605](https://github.com/NuGet/Home/issues/7605)</span><span class="sxs-lookup"><span data-stu-id="438ae-123">doesn't work with sources that need auth - [#7605](https://github.com/NuGet/Home/issues/7605)</span></span>

* <span data-ttu-id="438ae-124">NuGet.VisualStudio.IVsPackageInstaller - パッケージに含まれないプロジェクトの呼び出しを参照して常に使用 packages.config、PackageReference - に既定値が設定されている場合でも[#7005](https://github.com/NuGet/Home/issues/7005)</span><span class="sxs-lookup"><span data-stu-id="438ae-124">NuGet.VisualStudio.IVsPackageInstaller - calling on a project with no package references always uses packages.config, even if the default is set to PackageReference - [#7005](https://github.com/NuGet/Home/issues/7005)</span></span>

* <span data-ttu-id="438ae-125">PMC:更新プログラム パッケージでは、除外されるパッケージが失敗した (「できませんパッケージが見つかりません」) を再インストールします。</span><span class="sxs-lookup"><span data-stu-id="438ae-125">PMC: Update-Package reinstall fails ("Unable to find package") on delisted packages.</span></span><span data-ttu-id="438ae-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span><span class="sxs-lookup"><span data-stu-id="438ae-126"> - [#7268](https://github.com/NuGet/Home/issues/7268)</span></span>

* <span data-ttu-id="438ae-127">リポジトリと VSIX - サード パーティに関する通知を追加[#7409](https://github.com/NuGet/Home/issues/7409)</span><span class="sxs-lookup"><span data-stu-id="438ae-127">Add third party notice in our repo and VSIX - [#7409](https://github.com/NuGet/Home/issues/7409)</span></span>

* <span data-ttu-id="438ae-128">-指定されたバージョンがないときに、最新バージョンをインストールする必要があります NuGet.VisualStudio.IVsPackageInstaller.InstallPackage [#7493](https://github.com/NuGet/Home/issues/7493)</span><span class="sxs-lookup"><span data-stu-id="438ae-128">NuGet.VisualStudio.IVsPackageInstaller.InstallPackage should install latest version when no version given - [#7493](https://github.com/NuGet/Home/issues/7493)</span></span>

* <span data-ttu-id="438ae-129">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="438ae-129">--interactive support for dotnet nuget push - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

* <span data-ttu-id="438ae-130">ロック ファイルを復元する場合は、NU1603 警告が発生しないでください。</span><span class="sxs-lookup"><span data-stu-id="438ae-130">When restoring with lock file, NU1603 warning shouldn't be raised.</span></span><span data-ttu-id="438ae-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span><span class="sxs-lookup"><span data-stu-id="438ae-131"> - [#7529](https://github.com/NuGet/Home/issues/7529)</span></span>

* <span data-ttu-id="438ae-132">NuGet は、最小ログ記録 - 復元中にプロジェクト パスを印刷する必要があります[#7647](https://github.com/NuGet/Home/issues/7647)</span><span class="sxs-lookup"><span data-stu-id="438ae-132">NuGet should not print project path during restore with minimal logging - [#7647](https://github.com/NuGet/Home/issues/7647)</span></span>

* <span data-ttu-id="438ae-133">-- dotnet の対話型のサポートは、パッケージを削除する - [#7727](https://github.com/NuGet/Home/issues/7727)</span><span class="sxs-lookup"><span data-stu-id="438ae-133">--interactive support for dotnet remove package - [#7727](https://github.com/NuGet/Home/issues/7727)</span></span>

* <span data-ttu-id="438ae-134">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span><span class="sxs-lookup"><span data-stu-id="438ae-134">Add back NuGet.Packaging.Core with TypeForwardedTo attrs - [#7768](https://github.com/NuGet/Home/issues/7768)</span></span>

* <span data-ttu-id="438ae-135">plugins_cache 必要 - うまく動作するための短いパス[#7770](https://github.com/NuGet/Home/issues/7770)</span><span class="sxs-lookup"><span data-stu-id="438ae-135">plugins_cache needs shorter path to work well - [#7770](https://github.com/NuGet/Home/issues/7770)</span></span>

* <span data-ttu-id="438ae-136">ユーザーが特定の msbuild バージョン - 質問されていなかった場合、msbuild の検出パスを優先[#7786](https://github.com/NuGet/Home/issues/7786)</span><span class="sxs-lookup"><span data-stu-id="438ae-136">Prefer path for msbuild discovery if user didn't ask for specific msbuild version - [#7786](https://github.com/NuGet/Home/issues/7786)</span></span>

* `nuget.exe /?` <span data-ttu-id="438ae-137">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="438ae-137">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="438ae-138">NuGet.targets(498,5): error :パスの一部が見つかりませんでした '/tmp/NuGetScratch - mono - [#7793。](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="438ae-138">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="438ae-139">復元が不必要にマシン キャッシュ - で参照されるパッケージのすべてのバージョンの内容を列挙[#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="438ae-139">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="438ae-140">MSBuild の自動検出は 16.0 を常に選択インストール VS 2019 プレビュー - 後[#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="438ae-140">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="438ae-141">ソリューションに dotnet リスト パッケージ フレームワークの重複するエントリを出力する[#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="438ae-141">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="438ae-142">例外「空のパス名は有効な」old IVsPackageInstaller.InstallPackage を呼び出し元がプロジェクトし、パッケージ フォルダーが存在しません。</span><span class="sxs-lookup"><span data-stu-id="438ae-142">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="438ae-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="438ae-143"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="438ae-144">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="438ae-144">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

* <span data-ttu-id="438ae-145">VS 16.0 の NuGet UI には、色の問題のため、読み取り不可能なタブ[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="438ae-145">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="438ae-146">NuGet.Core & NuGet.Clients License.txt clarification on - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="438ae-146">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="438ae-147">復元は、- の種類を判断するためのグローバル パッケージ フォルダーを列挙する不必要に[#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="438ae-147">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="438ae-148">エラー一覧 ウィンドウ - にロック ファイル強制からエラーが表示されます[#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="438ae-148">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="438ae-149">NuGet.Configuration の問題を修正[#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="438ae-149">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="438ae-150">MSBuild の更新のインストールに合わせて場所 - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="438ae-150">Adapt to MSBuild updating its install location - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="438ae-151">開発の依存関係 - をする必要があります NuGet.Build.Tasks.Pack [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="438ae-151">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="438ae-152">などのパック拡張機能ポイントを追加するデバッグ シンボルの[#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="438ae-152">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* `dotnet pack` <span data-ttu-id="438ae-153">(浮動バージョンが使用されている場合も含む) の作成の nupkg で依存関係のバージョンの範囲を保持する必要があります[#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="438ae-153">should preserve dependency version range in the created nupkg (even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* `dotnet restore` <span data-ttu-id="438ae-154">ユーザー レベルの構成があります - ソースと認証済みのソースでは失敗[#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="438ae-154">fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="438ae-155">パック BuildActions - コンテンツのファイルのセットを制限せず[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="438ae-155">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="438ae-156">警告 AssetTargetFallback が成功する必要があります ProjectReference を使用してください。</span><span class="sxs-lookup"><span data-stu-id="438ae-156">Using a ProjectReference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="438ae-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="438ae-157"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="438ae-158">CPS (CommonProjectSystem) - を呼び出すときに、スレッドの問題によりデッドロック[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="438ae-158">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* `dotnet add package` <span data-ttu-id="438ae-159">ローカル設定で指定されたソースのグローバル構成から資格情報を使用しない[#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="438ae-159">doesn't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="438ae-160">MEF が非同期で呼び出されると、スレッドの問題のコード パス - [#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="438ae-160">Threading issues with MEF being called on async code paths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="438ae-161">署名: エラーが報告されずコール スタックの 2 回[#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="438ae-161">Signing: error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="438ae-162">エラー - を表示する署名証明書を信頼されていないと、署名付きパッケージをインストールする必要があります[#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="438ae-162">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="438ae-163">NuGet の復元を正しく Noop obj ディレクトリ - を共有する 2 つのプロジェクトと[#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="438ae-163">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="438ae-164">PAT では使用できません`dotnet restore`- 認証済みのフィードからパッケージを使用した linux [#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="438ae-164">Cannot use PAT with `dotnet restore` on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="438ae-165">dotnet 復元が失敗するため、無効になっているマシン ワイド フィード - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="438ae-165">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

**<span data-ttu-id="438ae-166">DCR</span><span class="sxs-lookup"><span data-stu-id="438ae-166">DCRs</span></span>**

* <span data-ttu-id="438ae-167">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span><span class="sxs-lookup"><span data-stu-id="438ae-167">Warn of future removal of "dotnet pack project.json" - [#7928](https://github.com/NuGet/Home/issues/7928)</span></span>
 
* <span data-ttu-id="438ae-168">Gen1 資格情報プラグインの非推奨の警告を追加[#7819](https://github.com/NuGet/Home/issues/7819)</span><span class="sxs-lookup"><span data-stu-id="438ae-168">Add a deprecation warning for Gen1 credential plugin - [#7819](https://github.com/NuGet/Home/issues/7819)</span></span>
 
* <span data-ttu-id="438ae-169">署名: RepositorySignatures/5.0.0 リソースを使用してすべてのパッケージのリポジトリとしてのクライアント検証を要求するリポジトリを有効になっている署名-- [#7759](https://github.com/NuGet/Home/issues/7759)</span><span class="sxs-lookup"><span data-stu-id="438ae-169">Signing: Enabled Repo to require client verification of every package as repo signed -- via RepositorySignatures/5.0.0 resource - [#7759](https://github.com/NuGet/Home/issues/7759)</span></span>

* <span data-ttu-id="438ae-170">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span><span class="sxs-lookup"><span data-stu-id="438ae-170">limit http request number per source through NuGet.Config - [#4538](https://github.com/NuGet/Home/issues/4538)</span></span>

* <span data-ttu-id="438ae-171">NuGet のために、VSIX の 16.0 ビルドのクリーンアップ) Net472 - 対象[#7143](https://github.com/NuGet/Home/issues/7143)</span><span class="sxs-lookup"><span data-stu-id="438ae-171">NuGet should target Net472 (to help Cleanup the 16.0 build of the VSIX) - [#7143](https://github.com/NuGet/Home/issues/7143)</span></span>

* <span data-ttu-id="438ae-172">PMC:Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span><span class="sxs-lookup"><span data-stu-id="438ae-172">PMC: Remove OpenPackagePage command - [#7384](https://github.com/NuGet/Home/issues/7384)</span></span>

* <span data-ttu-id="438ae-173">NetStandard 2.1 - make NetCoreApp 3.0 マップ[#7762](https://github.com/NuGet/Home/issues/7762)</span><span class="sxs-lookup"><span data-stu-id="438ae-173">Make NetCoreApp 3.0 map to NetStandard 2.1 - [#7762](https://github.com/NuGet/Home/issues/7762)</span></span>

* <span data-ttu-id="438ae-174">NuGet.\* パッケージ - に netstandard2.0 サポートを追加[#6516](https://github.com/NuGet/Home/issues/6516)</span><span class="sxs-lookup"><span data-stu-id="438ae-174">Add netstandard2.0 support to NuGet.\* packages - [#6516](https://github.com/NuGet/Home/issues/6516)</span></span>

* <span data-ttu-id="438ae-175">パッケージ作成者ビルド アセットの推移的な動作の定義を許可する[#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="438ae-175">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="438ae-176">VS 2019 ソリューション フィルター機能をサポートします。</span><span class="sxs-lookup"><span data-stu-id="438ae-176">Support VS 2019 Solution Filter feature.</span></span> <span data-ttu-id="438ae-177">また、ソリューションではなくプロジェクトまたはアンロードされたプロジェクトをサポートします。</span><span class="sxs-lookup"><span data-stu-id="438ae-177">Also supports project not in solution, or unloaded projects.</span></span> <span data-ttu-id="438ae-178">CLI または VS) (完全なソリューションを最初に復元する必要があります[#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="438ae-178">Need to restore complete solution (via CLI or VS) first - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>

* <span data-ttu-id="438ae-179">(変更) - TFM を使用して .NET 4.7.2 を必要とする NuGet 5.0 アセンブリ[#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="438ae-179">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="438ae-180">NuGetLicenseData NuGet.Packaging からパブリック型である必要があります。</span><span class="sxs-lookup"><span data-stu-id="438ae-180">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="438ae-181">Spdx から取り込まれたライセンス メタデータを更新します。</span><span class="sxs-lookup"><span data-stu-id="438ae-181">Update license metadata ingested from spdx.</span></span><span data-ttu-id="438ae-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="438ae-182"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="438ae-183">削除の設定の廃止された Api - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="438ae-183">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="438ae-184">1 システムでの回避策復元タイムアウト cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="438ae-184">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="438ae-185">NuGet.config の資格情報がある場合でも、NuGet は NTLM auth を優先 - 資格情報の認証の種類のフィルターを構成オプションを追加する[#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="438ae-185">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="438ae-186">PackageReference (一致する Packages.Config 機能) - の EmbedInteropTypes を有効にする[#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="438ae-186">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

**[<span data-ttu-id="438ae-187">このリリースでは、5.0 RTM で修正されたすべての問題の一覧</span><span class="sxs-lookup"><span data-stu-id="438ae-187">List of all issues fixed in this release - 5.0 RTM</span></span>](https://github.com/NuGet/Home/milestone/84?closed=1)**

## <a name="known-issues"></a><span data-ttu-id="438ae-188">既知の問題</span><span class="sxs-lookup"><span data-stu-id="438ae-188">Known issues</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="438ae-189">.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。</span><span class="sxs-lookup"><span data-stu-id="438ae-189">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="438ae-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="438ae-190"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
#### <a name="issue"></a><span data-ttu-id="438ae-191">懸案事項</span><span class="sxs-lookup"><span data-stu-id="438ae-191">Issue</span></span>
<span data-ttu-id="438ae-192">dotnet.exe 2.x を使って netcoreapp 1.x と netcoreapp 2.x をマルチターゲットにするプロジェクトを復元すると、そのフォールバック フォルダーがファイル フィードとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="438ae-192">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="438ae-193">つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。</span><span class="sxs-lookup"><span data-stu-id="438ae-193">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span><br>
#### <a name="workaround"></a><span data-ttu-id="438ae-194">回避策</span><span class="sxs-lookup"><span data-stu-id="438ae-194">Workaround</span></span>
<span data-ttu-id="438ae-195">フォールバックのフォルダーの使用状況を無効に設定して、 `RestoreAdditionalProjectSources` nothing に。</span><span class="sxs-lookup"><span data-stu-id="438ae-195">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing:</span></span>

`<RestoreAdditionalProjectSources></RestoreAdditionalProjectSources>`

<span data-ttu-id="438ae-196">フォールバック フォルダーから復元されるパッケージは NuGet.org からダウンロードするよう注意して使用します。</span><span class="sxs-lookup"><span data-stu-id="438ae-196">Use this with caution as packages that would be restored from the fallback folder will now be downloaded from NuGet.org.</span></span>
