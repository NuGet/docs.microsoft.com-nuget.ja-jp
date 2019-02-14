---
title: NuGet 5.0 preview リリース ノート
description: 既知の問題、バグの修正、新機能、および Dcr を含む NuGet 5.0 プレビューのリリース ノート。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: 5889ea52f993fa8fe841f8eb83b6da659cdede93
ms.sourcegitcommit: 1ab750ff17e55c763d646c50e7630138804ce8b8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2019
ms.locfileid: "56247660"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="ed1e8-103">NuGet 5.0 Preview リリース ノート</span><span class="sxs-lookup"><span data-stu-id="ed1e8-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="nuget-50-preview-releases"></a><span data-ttu-id="ed1e8-104">NuGet 5.0 プレビュー リリース</span><span class="sxs-lookup"><span data-stu-id="ed1e8-104">NuGet 5.0 Preview Releases</span></span>

* <span data-ttu-id="ed1e8-105">2019 年 2 月 13日 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-105">February 13, 2019 - [NuGet 5.0 Preview 3](#summary-whats-new-in-50-preview-3)</span></span>
* <span data-ttu-id="ed1e8-106">2019 年 1 月 23日 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-106">January 23, 2019 - [NuGet 5.0 Preview 2](#summary-whats-new-in-50-preview-2)</span></span>

## <a name="summary-whats-new-in-nuget-50-preview-3"></a><span data-ttu-id="ed1e8-107">概要:NuGet 5.0 Preview 3 の新機能新機能</span><span class="sxs-lookup"><span data-stu-id="ed1e8-107">Summary: What's New in NuGet 5.0 Preview 3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ed1e8-108">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="ed1e8-108">Issues fixed in this release</span></span> 

<span data-ttu-id="ed1e8-109">**バグ:**</span><span class="sxs-lookup"><span data-stu-id="ed1e8-109">**Bugs:**</span></span>

* <span data-ttu-id="ed1e8-110">nuget.exe/でしょうか。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-110">nuget.exe /?</span></span> <span data-ttu-id="ed1e8-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-111">should list correct msbuild versions - [#7794](https://github.com/NuGet/Home/issues/7794)</span></span>

* <span data-ttu-id="ed1e8-112">NuGet.targets(498,5): error :パスの一部が見つかりませんでした '/tmp/NuGetScratch - mono - [#7793。](https://github.com/NuGet/Home/issues/7793)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-112">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - on mono - [#7793](https://github.com/NuGet/Home/issues/7793)</span></span>

* <span data-ttu-id="ed1e8-113">復元が不必要にマシン キャッシュ - で参照されるパッケージのすべてのバージョンの内容を列挙[#7639](https://github.com/NuGet/Home/issues/7639)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-113">restore unnecessarily enumerates the contents of all versions of referenced package in the machine cache - [#7639](https://github.com/NuGet/Home/issues/7639)</span></span>

* <span data-ttu-id="ed1e8-114">MSBuild の自動検出は 16.0 を常に選択インストール VS 2019 プレビュー - 後[#7621](https://github.com/NuGet/Home/issues/7621)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-114">MSBuild auto-detection always selects 16.0 after installing VS 2019 Preview - [#7621](https://github.com/NuGet/Home/issues/7621)</span></span>

* <span data-ttu-id="ed1e8-115">ソリューションに dotnet リスト パッケージ フレームワークの重複するエントリを出力する[#7607](https://github.com/NuGet/Home/issues/7607)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-115">dotnet list package on a solution outputs duplicate entries for framework - [#7607](https://github.com/NuGet/Home/issues/7607)</span></span>

* <span data-ttu-id="ed1e8-116">例外「空のパス名は有効な」old IVsPackageInstaller.InstallPackage を呼び出し元がプロジェクトし、パッケージ フォルダーが存在しません。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-116">Exception "Empty path name is not legal" when calling IVsPackageInstaller.InstallPackage on old projects and packages folder does not exist.</span></span><span data-ttu-id="ed1e8-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-117"> - [#5936](https://github.com/NuGet/Home/issues/5936)</span></span>

* <span data-ttu-id="ed1e8-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-118">msbuild /t:restore minimal verbosity should be more minimal - [#4695](https://github.com/NuGet/Home/issues/4695)</span></span>

<span data-ttu-id="ed1e8-119">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="ed1e8-119">**DCRs**</span></span>

* <span data-ttu-id="ed1e8-120">パッケージ作成者ビルド アセットの推移的な動作の定義を許可する[#6091](https://github.com/NuGet/Home/issues/6091)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-120">Allow package authors to define build assets transitive behavior - [#6091](https://github.com/NuGet/Home/issues/6091)</span></span>

* <span data-ttu-id="ed1e8-121">プロジェクトは、ソリューションの一部でないか、アンロードされますが復元された以前の場合は成功を VS での復元を有効にする[#5820](https://github.com/NuGet/Home/issues/5820)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-121">Enable restore in VS to succeed if a project is not part of solution or is not loaded, but has previously been restored - [#5820](https://github.com/NuGet/Home/issues/5820)</span></span>


## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="ed1e8-122">概要:5.0 Preview 2 の新機能新機能</span><span class="sxs-lookup"><span data-stu-id="ed1e8-122">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="ed1e8-123">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="ed1e8-123">Issues fixed in this release</span></span>

<span data-ttu-id="ed1e8-124">**バグ:**</span><span class="sxs-lookup"><span data-stu-id="ed1e8-124">**Bugs:**</span></span>

* <span data-ttu-id="ed1e8-125">VS 16.0 の NuGet UI には、色の問題のため、読み取り不可能なタブ[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-125">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="ed1e8-126">NuGet.Core & NuGet.Clients License.txt clarification on - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-126">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="ed1e8-127">復元は、- の種類を判断するためのグローバル パッケージ フォルダーを列挙する不必要に[#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-127">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="ed1e8-128">エラー一覧 ウィンドウ - にロック ファイル強制からエラーが表示されます[#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-128">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="ed1e8-129">NuGet.Configuration の問題を修正[#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-129">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="ed1e8-130">MSBuild の更新に合わせてそれはのインストール場所。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-130">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="ed1e8-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-131">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="ed1e8-132">開発の依存関係 - をする必要があります NuGet.Build.Tasks.Pack [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-132">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="ed1e8-133">などのパック拡張機能ポイントを追加するデバッグ シンボルの[#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-133">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="ed1e8-134">dotnet pack には、作成した nupkg で依存関係のバージョンの範囲を保持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-134">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="ed1e8-135">(浮動バージョンが使用されている場合も含む) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-135">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="ed1e8-136">ユーザー レベルの構成には、ソースもがある場合、認証済みのソースで dotnet 復元が失敗した[#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-136">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="ed1e8-137">パック BuildActions - コンテンツのファイルのセットを制限せず[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-137">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="ed1e8-138">警告 AssetTargetFallback が成功する必要があります projectreference を使用してください。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-138">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="ed1e8-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-139"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="ed1e8-140">CPS (CommonProjectSystem) - を呼び出すときに、スレッドの問題によりデッドロック[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-140">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="ed1e8-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-141">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="ed1e8-142">スレッド処理の MEF される問題非同期コードパス - で呼び出される[#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-142">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="ed1e8-143">署名: エラーが報告されずコール スタックの 2 回[#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-143">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="ed1e8-144">エラー - を表示する署名証明書を信頼されていないと、署名付きパッケージをインストールする必要があります[#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-144">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="ed1e8-145">NuGet の復元を正しく Noop obj ディレクトリ - を共有する 2 つのプロジェクトと[#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-145">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="ed1e8-146">-認証済みのフィードからパッケージを使用した Linux での dotnet restore で PAT を使用することはできません[#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-146">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="ed1e8-147">dotnet 復元が失敗するため、無効になっているマシン ワイド フィード - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-147">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

<span data-ttu-id="ed1e8-148">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="ed1e8-148">**DCRs**</span></span>

* <span data-ttu-id="ed1e8-149">(変更) - TFM を使用して .NET 4.7.2 を必要とする NuGet 5.0 アセンブリ[#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-149">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="ed1e8-150">NuGetLicenseData NuGet.Packaging からパブリック型である必要があります。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-150">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="ed1e8-151">Spdx から取り込まれたライセンス メタデータを更新します。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-151">Update license metadata ingested from spdx.</span></span><span data-ttu-id="ed1e8-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-152"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="ed1e8-153">削除の設定の廃止された Api - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-153">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="ed1e8-154">1 システムでの回避策復元タイムアウト cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-154">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="ed1e8-155">NuGet.config の資格情報がある場合でも、NuGet は NTLM auth を優先 - 資格情報の認証の種類のフィルターを構成オプションを追加する[#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-155">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="ed1e8-156">PackageReference (一致する Packages.Config 機能) - の EmbedInteropTypes を有効にする[#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-156">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="ed1e8-157">このリリース 5.0.0-preview2 で修正されたすべての問題の一覧</span><span class="sxs-lookup"><span data-stu-id="ed1e8-157">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

### <a name="known-issues"></a><span data-ttu-id="ed1e8-158">既知の問題</span><span class="sxs-lookup"><span data-stu-id="ed1e8-158">Known issues</span></span>

#### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="ed1e8-159">dotnet nuget push --interactive が Mac 上でエラーになる。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-159">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="ed1e8-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-160"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>
<span data-ttu-id="ed1e8-161">**問題**、`--interactive`引数は dotnet cli を使用して転送されていませんが、エラーが発生`error: Missing value for option 'interactive'` 
**回避策**などの対話型のオプションを使用して、他のdotnetコマンドを実行`dotnet restore --interactive`および認証します。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-161">**Issue** The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`
**Workaround** Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="ed1e8-162">そうすると、認証が資格情報プロバイダーによってキャッシュされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-162">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="ed1e8-163">その後、`dotnet nuget push` を実行します。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-163">Then run `dotnet nuget push`.</span></span>

#### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="ed1e8-164">.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-164">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="ed1e8-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="ed1e8-165"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>
<span data-ttu-id="ed1e8-166">**問題**dotnet.exe を使用するときにそのマルチ ターゲット netcoreapp プロジェクトを復元する 2.x 1.x と netcoreapp 2.x、フォールバックのフォルダーはフィード ファイルとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-166">**Issue** When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="ed1e8-167">つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>
<span data-ttu-id="ed1e8-168">**回避策**フォールバック フォルダーの使用状況を無効に設定して、 `RestoreAdditionalProjectSources` nothing にします。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-168">**Workaround** Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="ed1e8-169">`<RestoreAdditionalProjectSources/>` これは慎重に使う必要があります。フォールバック フォルダーから復元されていたはずの多くのパッケージが、NuGet.org からダウンロードされることになるためです。</span><span class="sxs-lookup"><span data-stu-id="ed1e8-169">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
