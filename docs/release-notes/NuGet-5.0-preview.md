---
title: NuGet 5.0 preview リリース ノート
description: 既知の問題、バグの修正、新機能、および Dcr を含む NuGet 5.0 プレビューのリリース ノート。
author: anangaur
ms.author: anangaur
ms.date: 1/25/2019
ms.topic: conceptual
ms.openlocfilehash: ed3294f88ff99d5e26f630bdbca03aa8446b6e7f
ms.sourcegitcommit: 0cb4c9853cde3647291062eadee2298dd273311e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2019
ms.locfileid: "55084938"
---
# <a name="nuget-50-preview-release-notes"></a><span data-ttu-id="7284c-103">NuGet 5.0 Preview リリース ノート</span><span class="sxs-lookup"><span data-stu-id="7284c-103">NuGet 5.0 Preview Release Notes</span></span>

## <a name="summary-whats-new-in-50-preview-2"></a><span data-ttu-id="7284c-104">概要:5.0 Preview 2 の新機能新機能</span><span class="sxs-lookup"><span data-stu-id="7284c-104">Summary: What's New in 5.0 Preview 2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="7284c-105">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="7284c-105">Issues fixed in this release</span></span>

#### <a name="bugs"></a><span data-ttu-id="7284c-106">バグ:</span><span class="sxs-lookup"><span data-stu-id="7284c-106">Bugs:</span></span>

* <span data-ttu-id="7284c-107">VS 16.0 の NuGet UI には、色の問題のため、読み取り不可能なタブ[#7735](https://github.com/NuGet/Home/issues/7735)</span><span class="sxs-lookup"><span data-stu-id="7284c-107">VS 16.0's NuGet UI has unreadable tabs due to color problems - [#7735](https://github.com/NuGet/Home/issues/7735)</span></span>

* <span data-ttu-id="7284c-108">NuGet.Core & NuGet.Clients License.txt clarification on - [#7629](https://github.com/NuGet/Home/issues/7629)</span><span class="sxs-lookup"><span data-stu-id="7284c-108">NuGet.Core & NuGet.Clients License.txt clarification - [#7629](https://github.com/NuGet/Home/issues/7629)</span></span>

* <span data-ttu-id="7284c-109">復元は、- の種類を判断するためのグローバル パッケージ フォルダーを列挙する不必要に[#7596](https://github.com/NuGet/Home/issues/7596)</span><span class="sxs-lookup"><span data-stu-id="7284c-109">Restore unnecessarily enumerates global package folder in attempt to determine type - [#7596](https://github.com/NuGet/Home/issues/7596)</span></span>

* <span data-ttu-id="7284c-110">エラー一覧 ウィンドウ - にロック ファイル強制からエラーが表示されます[#7429](https://github.com/NuGet/Home/issues/7429)</span><span class="sxs-lookup"><span data-stu-id="7284c-110">Errors from lock file enforcement should show up in Error List Window - [#7429](https://github.com/NuGet/Home/issues/7429)</span></span>

* <span data-ttu-id="7284c-111">NuGet.Configuration の問題を修正[#7326](https://github.com/NuGet/Home/issues/7326)</span><span class="sxs-lookup"><span data-stu-id="7284c-111">Fix NuGet.Configuration issues - [#7326](https://github.com/NuGet/Home/issues/7326)</span></span>

* <span data-ttu-id="7284c-112">MSBuild の更新に合わせてそれはのインストール場所。</span><span class="sxs-lookup"><span data-stu-id="7284c-112">Adapt to MSBuild updating it's install location.</span></span><span data-ttu-id="7284c-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span><span class="sxs-lookup"><span data-stu-id="7284c-113">  - [#7325](https://github.com/NuGet/Home/issues/7325)</span></span>

* <span data-ttu-id="7284c-114">開発の依存関係 - をする必要があります NuGet.Build.Tasks.Pack [#7249](https://github.com/NuGet/Home/issues/7249)</span><span class="sxs-lookup"><span data-stu-id="7284c-114">NuGet.Build.Tasks.Pack should be a development dependency - [#7249](https://github.com/NuGet/Home/issues/7249)</span></span>

* <span data-ttu-id="7284c-115">などのパック拡張機能ポイントを追加するデバッグ シンボルの[#7234](https://github.com/NuGet/Home/issues/7234)</span><span class="sxs-lookup"><span data-stu-id="7284c-115">Add pack extension point for including debug symbols - [#7234](https://github.com/NuGet/Home/issues/7234)</span></span>

* <span data-ttu-id="7284c-116">dotnet pack には、作成した nupkg で依存関係のバージョンの範囲を保持する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7284c-116">dotnet pack should preserve dependency version range in the created nupkg.</span></span> <span data-ttu-id="7284c-117">(浮動バージョンが使用されている場合も含む) - [#7232](https://github.com/NuGet/Home/issues/7232)</span><span class="sxs-lookup"><span data-stu-id="7284c-117">(even if floating version is used) - [#7232](https://github.com/NuGet/Home/issues/7232)</span></span>

* <span data-ttu-id="7284c-118">ユーザー レベルの構成には、ソースもがある場合、認証済みのソースで dotnet 復元が失敗した[#7209](https://github.com/NuGet/Home/issues/7209)</span><span class="sxs-lookup"><span data-stu-id="7284c-118">dotnet restore fails on authenticated source when user-level config also has source - [#7209](https://github.com/NuGet/Home/issues/7209)</span></span>

* <span data-ttu-id="7284c-119">パック BuildActions - コンテンツのファイルのセットを制限せず[#7155](https://github.com/NuGet/Home/issues/7155)</span><span class="sxs-lookup"><span data-stu-id="7284c-119">Pack should not restrict the set of BuildActions for content files - [#7155](https://github.com/NuGet/Home/issues/7155)</span></span>

* <span data-ttu-id="7284c-120">警告 AssetTargetFallback が成功する必要があります projectreference を使用してください。</span><span class="sxs-lookup"><span data-stu-id="7284c-120">Using a projectreference which requires AssetTargetFallback to succeed, should warn.</span></span><span data-ttu-id="7284c-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span><span class="sxs-lookup"><span data-stu-id="7284c-121"> - [#7137](https://github.com/NuGet/Home/issues/7137)</span></span>

* <span data-ttu-id="7284c-122">CPS (CommonProjectSystem) - を呼び出すときに、スレッドの問題によりデッドロック[#7103](https://github.com/NuGet/Home/issues/7103)</span><span class="sxs-lookup"><span data-stu-id="7284c-122">Deadlock due to threading issues when calling into CPS (CommonProjectSystem) - [#7103](https://github.com/NuGet/Home/issues/7103)</span></span>

* <span data-ttu-id="7284c-123">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span><span class="sxs-lookup"><span data-stu-id="7284c-123">dotnet add package won't use credentials from global config for a source specified in local config - [#6935](https://github.com/NuGet/Home/issues/6935)</span></span>

* <span data-ttu-id="7284c-124">スレッド処理の MEF される問題非同期コードパス - で呼び出される[#6771](https://github.com/NuGet/Home/issues/6771)</span><span class="sxs-lookup"><span data-stu-id="7284c-124">Threading issues with MEF being called on async codepaths - [#6771](https://github.com/NuGet/Home/issues/6771)</span></span>

* <span data-ttu-id="7284c-125">署名: エラーが報告されずコール スタックの 2 回[#6455](https://github.com/NuGet/Home/issues/6455)</span><span class="sxs-lookup"><span data-stu-id="7284c-125">Signing:  error reported twice and without call stack - [#6455](https://github.com/NuGet/Home/issues/6455)</span></span>

* <span data-ttu-id="7284c-126">エラー - を表示する署名証明書を信頼されていないと、署名付きパッケージをインストールする必要があります[#6318](https://github.com/NuGet/Home/issues/6318)</span><span class="sxs-lookup"><span data-stu-id="7284c-126">Installing a signed package with untrusted signing certificate should show error - [#6318](https://github.com/NuGet/Home/issues/6318)</span></span>

* <span data-ttu-id="7284c-127">NuGet の復元を正しく Noop obj ディレクトリ - を共有する 2 つのプロジェクトと[#6114](https://github.com/NuGet/Home/issues/6114)</span><span class="sxs-lookup"><span data-stu-id="7284c-127">NuGet restore improperly NoOps when 2 projects are sharing obj directory - [#6114](https://github.com/NuGet/Home/issues/6114)</span></span>

* <span data-ttu-id="7284c-128">-認証済みのフィードからパッケージを使用した Linux での dotnet restore で PAT を使用することはできません[#5651](https://github.com/NuGet/Home/issues/5651)</span><span class="sxs-lookup"><span data-stu-id="7284c-128">Cannot use PAT with dotnet restore on Linux with packages from authenticated feed - [#5651](https://github.com/NuGet/Home/issues/5651)</span></span>

* <span data-ttu-id="7284c-129">dotnet 復元が失敗するため、無効になっているマシン ワイド フィード - [#5410](https://github.com/NuGet/Home/issues/5410)</span><span class="sxs-lookup"><span data-stu-id="7284c-129">dotnet restore fails due to disabled machine wide feed - [#5410](https://github.com/NuGet/Home/issues/5410)</span></span>

#### <a name="dcrs"></a><span data-ttu-id="7284c-130">DCR</span><span class="sxs-lookup"><span data-stu-id="7284c-130">DCRs</span></span>

* <span data-ttu-id="7284c-131">(変更) - TFM を使用して .NET 4.7.2 を必要とする NuGet 5.0 アセンブリ[#7510](https://github.com/NuGet/Home/issues/7510)</span><span class="sxs-lookup"><span data-stu-id="7284c-131">NuGet 5.0 assemblies to require .NET 4.7.2 (via TFM change) - [#7510](https://github.com/NuGet/Home/issues/7510)</span></span>

* <span data-ttu-id="7284c-132">NuGetLicenseData NuGet.Packaging からパブリック型である必要があります。</span><span class="sxs-lookup"><span data-stu-id="7284c-132">NuGetLicenseData from NuGet.Packaging should be a public type.</span></span> <span data-ttu-id="7284c-133">Spdx から取り込まれたライセンス メタデータを更新します。</span><span class="sxs-lookup"><span data-stu-id="7284c-133">Update license metadata ingested from spdx.</span></span><span data-ttu-id="7284c-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span><span class="sxs-lookup"><span data-stu-id="7284c-134"> - [#7471](https://github.com/NuGet/Home/issues/7471)</span></span>

* <span data-ttu-id="7284c-135">削除の設定の廃止された Api - [#7294](https://github.com/NuGet/Home/issues/7294)</span><span class="sxs-lookup"><span data-stu-id="7284c-135">Remove obsolete Settings APIs - [#7294](https://github.com/NuGet/Home/issues/7294)</span></span>

* <span data-ttu-id="7284c-136">1 システムでの回避策復元タイムアウト cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span><span class="sxs-lookup"><span data-stu-id="7284c-136">Workaround restore timeouts on systems with 1 cpu - [#6742](https://github.com/NuGet/Home/issues/6742)</span></span>

* <span data-ttu-id="7284c-137">NuGet.config の資格情報がある場合でも、NuGet は NTLM auth を優先 - 資格情報の認証の種類のフィルターを構成オプションを追加する[#5286](https://github.com/NuGet/Home/issues/5286)</span><span class="sxs-lookup"><span data-stu-id="7284c-137">NuGet prefers NTLM auth even if there are credentials in NuGet.config - add config option to filter auth types for credentials - [#5286](https://github.com/NuGet/Home/issues/5286)</span></span>

* <span data-ttu-id="7284c-138">PackageReference (一致する Packages.Config 機能) - の EmbedInteropTypes を有効にする[#2365](https://github.com/NuGet/Home/issues/2365)</span><span class="sxs-lookup"><span data-stu-id="7284c-138">Enable EmbedInteropTypes for PackageReference (matching Packages.Config capability) - [#2365](https://github.com/NuGet/Home/issues/2365)</span></span>

[<span data-ttu-id="7284c-139">このリリース 5.0.0-preview2 で修正されたすべての問題の一覧</span><span class="sxs-lookup"><span data-stu-id="7284c-139">List of all issues fixed in this release 5.0.0-preview2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")


## <a name="known-issues"></a><span data-ttu-id="7284c-140">既知の問題</span><span class="sxs-lookup"><span data-stu-id="7284c-140">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="7284c-141">dotnet nuget push --interactive が Mac 上でエラーになる。</span><span class="sxs-lookup"><span data-stu-id="7284c-141">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="7284c-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="7284c-142"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="7284c-143">懸案事項</span><span class="sxs-lookup"><span data-stu-id="7284c-143">Issue</span></span>
<span data-ttu-id="7284c-144">`--interactive` 引数が dotnet CLI によって転送されていないため、エラー `error: Missing value for option 'interactive'` が発生します</span><span class="sxs-lookup"><span data-stu-id="7284c-144">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="7284c-145">回避策</span><span class="sxs-lookup"><span data-stu-id="7284c-145">Workaround</span></span>
<span data-ttu-id="7284c-146">`dotnet restore --interactive` のように、対話型のオプションを使ってその他の任意の dotnet コマンドを実行し、認証します。</span><span class="sxs-lookup"><span data-stu-id="7284c-146">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="7284c-147">そうすると、認証が資格情報プロバイダーによってキャッシュされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7284c-147">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="7284c-148">その後、`dotnet nuget push` を実行します。</span><span class="sxs-lookup"><span data-stu-id="7284c-148">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="7284c-149">.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。</span><span class="sxs-lookup"><span data-stu-id="7284c-149">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="7284c-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="7284c-150"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="7284c-151">懸案事項</span><span class="sxs-lookup"><span data-stu-id="7284c-151">Issue</span></span>
<span data-ttu-id="7284c-152">dotnet.exe 2.x を使って netcoreapp 1.x と netcoreapp 2.x をマルチターゲットにするプロジェクトを復元すると、そのフォールバック フォルダーがファイル フィードとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="7284c-152">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="7284c-153">つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。</span><span class="sxs-lookup"><span data-stu-id="7284c-153">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="7284c-154">回避策</span><span class="sxs-lookup"><span data-stu-id="7284c-154">Workaround</span></span>
<span data-ttu-id="7284c-155">`RestoreAdditionalProjectSources` に何も設定しないことで、フォールバック フォルダーの使用を無効にします。</span><span class="sxs-lookup"><span data-stu-id="7284c-155">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="7284c-156">`<RestoreAdditionalProjectSources/>` これは慎重に使う必要があります。フォールバック フォルダーから復元されていたはずの多くのパッケージが、NuGet.org からダウンロードされることになるためです。</span><span class="sxs-lookup"><span data-stu-id="7284c-156">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
