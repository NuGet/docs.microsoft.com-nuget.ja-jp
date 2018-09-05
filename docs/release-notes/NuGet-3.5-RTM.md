---
title: NuGet 3.5 のベータ版のリリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.5 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: d8df2cb51ddcc03fb3922d9e9def17b39fccc661
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550685"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="b1f69-103">NuGet 3.5 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="b1f69-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="b1f69-104">[NuGet 3.5 RC リリース ノート](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC リリース ノート](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="b1f69-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="b1f69-105">バグ修正</span><span class="sxs-lookup"><span data-stu-id="b1f69-105">Bug Fixes</span></span>

* <span data-ttu-id="b1f69-106">パックは、mono で MSBuild 14.1 を使用しない[#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="b1f69-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="b1f69-107">更新プログラム タブは、代わりに現在インストールされているバージョンの選択を更新する利用可能な最新のバージョンを選択しない[#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="b1f69-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="b1f69-108">MyGet フィード プライベート v2 を認証し、"x は詳細の表示 をクリックするとクラッシュを修正しました- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="b1f69-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="b1f69-109">ログ メッセージは、UI - 逆の順序であると思われる[#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="b1f69-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="b1f69-110">「指定されたパスの形式はサポートされていません -」v3.4.4 - Nuget の復元をスローします[#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="b1f69-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="b1f69-111">NuGet コマンドライン 3.6 ベータ版を考慮しません - Prop 構成リリース - = [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="b1f69-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="b1f69-112">大規模なプロジェクトのインストール、Nuget IKVM 低速[#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="b1f69-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="b1f69-113">nuget.exe 自己保持で更新自体の更新プログラム[#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="b1f69-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="b1f69-114">UNC 共有から 3.5 のインストール/復元が 3.4.4 - からパフォーマンス回帰[#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="b1f69-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="b1f69-115">エラー - net451 プロジェクトのパッケージ管理 UI から Moq をインストールするときに[#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="b1f69-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="b1f69-116">ソリューション レベルでは、[インストール] タブは、パッケージのバージョンを表示しない[#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="b1f69-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="b1f69-117">xproj`project.json`インストール済み タブから更新プログラムが状態を失う[#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="b1f69-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="b1f69-118">NuGet パックを`.csproj`内の空のファイルの要素を無視`.nuspec`ファイル - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="b1f69-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="b1f69-119">IIS でホストされる web サイト プロジェクトには、復元が失敗にする必要がありますされません[#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="b1f69-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="b1f69-120">資格情報のない v2 - v3 エンドポイントにリダイレクトすると、Nuget.Config から取得[#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="b1f69-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="b1f69-121">NuGet の pack が失敗するポータブル アセンブリ メタデータを取得するときに、アセンブリを解決するのには[#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="b1f69-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="b1f69-122">Nuget で見つけることができません`msbuild.exe`mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="b1f69-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="b1f69-123">nuget.exe パックは、その最初の数値のプレリリース タグを許可しない[#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="b1f69-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="b1f69-124">VS2015E - で nuget パッケージのインストールが失敗する[#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="b1f69-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="b1f69-125">allowedVersions フィルター ソリューション レベルで作業しない[#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="b1f69-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="b1f69-126">復元に同じ項目をランダムに失敗したキーが既に追加されています。</span><span class="sxs-lookup"><span data-stu-id="b1f69-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="b1f69-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="b1f69-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="b1f69-128">Nuget.Common でをインストールすることはできません`.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="b1f69-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="b1f69-129">UI を使用して、V2 ソースを検索する、FindPackagesById が各 ID - に対して 2 回呼び出されます[#2517。](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="b1f69-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="b1f69-130">パッケージがプロジェクト - に依存できない[#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="b1f69-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="b1f69-131">nuget.exe パック - 除外が記載されていますが、サポートされていません - [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="b1f69-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="b1f69-132">メッセージ エラーに関する問題の 'contentFiles' セクション`.nuspec`が無効です - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="b1f69-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="b1f69-133">パッケージ全体 2 回認証パッケージ ソースのプッシュが常に送信[#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="b1f69-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="b1f69-134">プロジェクトの中に update \*.csproj の nuget.exe を呼び出すことがあるない場合に情報が指定されません、 `packages.config`  -  [#1496](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="b1f69-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="b1f69-135">`packages.config` 復元が V2 ソース - から 5 xx ステータス コードに再試行しない[#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="b1f69-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="b1f69-136">2 つのドットでファイル src で`.nuspec`が動作しない - [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="b1f69-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="b1f69-137">暗号化 - を使用したフィードを無視する必要がある CoreCLR 復元[#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="b1f69-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="b1f69-138">nuget.exe プッシュ - 正しくない資格情報を求める - 403 処理[#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="b1f69-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="b1f69-139">パッケージ マネージャーで NuGet の更新プログラムからプロパティが削除、 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="b1f69-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="b1f69-140">"NuGet.TeamFoundationServer14"が"NuGet.TeamFoundationServer"- に DLL の名前が変更されたことをロードしようとしている NuGet.PackageManagement.VisualStudio [#2857](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="b1f69-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="b1f69-141">パッケージ マネージャーの UI が新しく表示されない更新バージョン - [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="b1f69-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="b1f69-142">更新プログラム パッケージの id を使用しようとしています package.version - ではなくバージョン[#2771。](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="b1f69-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="b1f69-143">プロジェクトで nuget を使用していない場合、nuget 復元 csproj がエラー (`packages.config`または`project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="b1f69-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="b1f69-144">TFS エラー"[ファイル] ワークスペースに存在できないまたはへのアクセス許可がありません"中にアップグレードまたはアンインストールを TFS ソース管理のソリューション/プロジェクトがバインドされる[#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="b1f69-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="b1f69-145">更新プログラム パッケージは、- 非対象のパッケージの依存関係を取得しない[#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="b1f69-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="b1f69-146">Nuget パッケージ マネージャー UI の操作でのログの詳細レベルを設定する方法はありません[#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="b1f69-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="b1f69-147">nuget の構成が無効です - VS 2015 の VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="b1f69-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="b1f69-148">DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) が動作しない - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="b1f69-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="b1f69-149">nuget 3.4.3 リリース - をパッケージのビルドを null にする値を取得することはできません[#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="b1f69-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="b1f69-150">VSTS フィードの場合に、復元で Nuget.Config から保存された資格情報が使用されていない[#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="b1f69-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="b1f69-151">cmd dir - ではなくプロジェクト ディレクトリに対する相対パス [dotnet restore]--configfile です[#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="b1f69-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="b1f69-152">バージョンの比較コード - で過剰な割り当て[#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="b1f69-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="b1f69-153">同じをインストールしようとしています nuget.exe の複数のインスタンスのパッケージ化は並列原因二重書き込み - [#2628。](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="b1f69-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="b1f69-154">複数プロジェクトの操作 - の依存関係情報がキャッシュされない[#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="b1f69-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="b1f69-155">インストールし、最初のパッケージ フォルダーをチェックせず、ダウンロード パッケージを更新[#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="b1f69-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="b1f69-156">パッケージ ソースの一覧が空の場合は、UI を使用してパッケージ ソースを追加できません (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="b1f69-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="b1f69-157">デザイン時のファサードに依存するパッケージをインストールするときにエラーは誤解を招く[#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="b1f69-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="b1f69-158">のみ最初のソース -"All"の設定で PackageManager コンソールからパッケージをインストールしようと[#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="b1f69-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="b1f69-159">最新のベータ版を解凍できません - ModernHttpClient [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="b1f69-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="b1f69-160">自作 nuget 3.4.1 - 起動時にクラッシュを VS2015 [#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="b1f69-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="b1f69-161">Update コマンドを i を依頼するいかがの場合、少し冗長になる可能性があります[#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="b1f69-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="b1f69-162">ローカルでビルドされた VSIX は、CI ビルドとして同じ Dll およびファイルが必要です。</span><span class="sxs-lookup"><span data-stu-id="b1f69-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="b1f69-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="b1f69-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="b1f69-164">-ビルドで NuGet のダウン グレードの警告を修正[#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="b1f69-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="b1f69-165">永久にブロックされます (3 回) のパッケージ ソースを認証に失敗した[#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="b1f69-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="b1f69-166">引数でフィードから nuget v3.3 以降、パッケージをインストールするときにパッケージのコンテンツは正しく復元されません、パッケージが含まれている場合 - NoCache`.nupkg`ファイル - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="b1f69-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="b1f69-167">すべてのパッケージ ソースが、1 つのソースから不足しているパッケージで Nuget のインストールが失敗する - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="b1f69-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="b1f69-168">[PerfWatson]UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="b1f69-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="b1f69-169">1 つのソース - 承認に失敗した場合は、ブロックをインストール[#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="b1f69-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="b1f69-170">`.nuspec` バージョン範囲は-IncludeReferencedProjects バージョン - をオーバーライドする必要があります[#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="b1f69-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="b1f69-171">更新プログラム パッケージが、「しようとすると依存関係情報を収集する」- 低速 super [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="b1f69-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="b1f69-172">ステルス ダウン グレードの NuGet パッケージの場合にバッチ更新の依存関係 - [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="b1f69-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="b1f69-173">nuget.exe の更新プログラムは、アセンブリの厳密な名前とプライベートの属性を削除します。</span><span class="sxs-lookup"><span data-stu-id="b1f69-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="b1f69-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="b1f69-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="b1f69-175">相対ファイル パスの"DefaultPushSource"- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="b1f69-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="b1f69-176">競合回避モジュールのエラー メッセージを向上させる[#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="b1f69-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="b1f69-177">v3 での更新プログラムのパッケージが失敗する - 指定したソースではなくパッケージを使用した[#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="b1f69-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="b1f69-178">パッケージ ソースの相対パスを使用するには - を使用する問題が[#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="b1f69-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="b1f69-179">NUPKG ファイルに低いバージョンの要件では、間接的な依存関係が既に存在する場合は、プロジェクトから生成された依存関係がありません[#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="b1f69-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="b1f69-180">プロジェクトを削除する対応する UI ウィンドウを閉じます。 は、プロジェクトの名前変更は、UI ウィンドウを変更できません。</span><span class="sxs-lookup"><span data-stu-id="b1f69-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="b1f69-181">PMC をプロジェクトの名前変更、およびプロジェクトの削除イベントのリッスン注[#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="b1f69-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="b1f69-182">[Willow Web ワークロード]Razor v3 WSP の作成がハングする - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="b1f69-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="b1f69-183">特定のパッケージのインストール/復元は、「パッケージには、複数の nuspec ファイルが含まれています」。</span><span class="sxs-lookup"><span data-stu-id="b1f69-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="b1f69-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="b1f69-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="b1f69-185">小文字の Id (& a)`packages.config`シナリオ - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="b1f69-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="b1f69-186">[3.5 beta 2]パッケージの復元が失敗する -「レガシ」のパッケージを復元する[#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="b1f69-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="b1f69-187">nuget の pack が強制的に .tt ファイルを何であってもコンテンツのフォルダーに追加[#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="b1f69-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="b1f69-188">ASP.NET web アプリの更新プログラムのパッケージ ファイルに関連する警告が生成されますソース - [#3194。](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="b1f69-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="b1f69-189">nuget パック csproj (で`project.json`) packOptions と JSON ファイルの所有者がない場合のクラッシュ[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="b1f69-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="b1f69-190">用の nuget パック`project.json`概要、作成者、所有者などのような packOptions タグは無視[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="b1f69-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="b1f69-191">NuGet.Packaging.PhysicalPackageFile.GetStream - 経由で NullReferenceException [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="b1f69-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="b1f69-192">出力内の依存関係を無視する NuGet の pack`.nuspec`の`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="b1f69-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="b1f69-193">プロジェクトの破損した状態のままロールバックを含む複数のパッケージを更新[#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="b1f69-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="b1f69-194">いずれかの ContentFiles は netstandard プロジェクトには追加されません[#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="b1f69-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="b1f69-195">.Net をターゲットとするライブラリをパッケージ化できません標準- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="b1f69-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="b1f69-196">ファイルに新しいプロジェクト]-> [VS2015 で Dev15 - クラス ライブラリ (ポータブル) プロジェクトの失敗]-> [ [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="b1f69-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="b1f69-197">NuGet エラー - 1.0.0-\* が有効なバージョン文字列のではない[#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="b1f69-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="b1f69-198">表示が、インストール パッケージの機能の検索パッケージが失敗する[#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="b1f69-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="b1f69-199">エラー時に - dev15 で"Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="b1f69-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="b1f69-200">xproj の nuget パックは既定で無効なターゲット パス - [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="b1f69-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="b1f69-201">VS 2015 がインストールされている 3 バージョン 3.5.0 のエラーが発生した、NuGet を使用して VS を更新するときに[#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="b1f69-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="b1f69-202">「Packages.config によってブロック」 `project.json` (UWP、別名、ビルドの統合) プロジェクト - [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="b1f69-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="b1f69-203">これは公式 preview2 ビルド preview2 003121 にビルド スクリプトによってインストールされている dotnet cli を更新します。</span><span class="sxs-lookup"><span data-stu-id="b1f69-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="b1f69-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="b1f69-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="b1f69-205">パッケージ マネージャー UI: パッケージの更新後に新しいバージョンが表示されません- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="b1f69-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="b1f69-206">-Apikey コマンド行の削除が読み取り/で送信されない 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="b1f69-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="b1f69-207">文字列が正しくありません。 プレリリースの依存関係のパッケージの安定したリリースはありません。</span><span class="sxs-lookup"><span data-stu-id="b1f69-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="b1f69-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="b1f69-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="b1f69-209">OptimizedZipPackage キャッシュが空のフォルダー - [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="b1f69-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="b1f69-210">PCL (net46 および windows 10) プロジェクト get NullRef 例外を作成します。</span><span class="sxs-lookup"><span data-stu-id="b1f69-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="b1f69-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="b1f69-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="b1f69-212">AllowedVersions 制約 - によって新しいバージョンが制限されていると、Nuget の更新プログラムは情報メッセージを提供する必要があります[#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="b1f69-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="b1f69-213">Nuget v3 の復元に関する問題 - [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="b1f69-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="b1f69-214">資格情報プラグインが-1 のエラーで終了しました]、[複数のソースの資格情報プロバイダーを使用する場合にパッケージをダウンロード中にエラー [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="b1f69-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="b1f69-215">`project.json` nuget の復元が再コンパイル時に何も変更されました - [#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="b1f69-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="b1f69-216">シンボル パッケージがこれまでがないインストールまたは更新 - で使用される[#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="b1f69-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="b1f69-217">VS が repositoryPath 内の環境変数をサポートしていません (nuget.exe が) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="b1f69-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="b1f69-218">パッケージ マネージャー UI でラベル付けされていない Uielement をラベルには、ユーザー補助 - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="b1f69-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="b1f69-219">ハイフンでつながれたプロファイルを使用した移植可能なフレームワークは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="b1f69-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="b1f69-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="b1f69-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="b1f69-221">NuGet パッケージ マネージャーで、そのオプションの一覧でパッケージの詳細には適用されませんを明確にするため必要があります`project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="b1f69-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="b1f69-222">nuget.exe プッシュ/削除は、API キー - を使用しない[#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="b1f69-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="b1f69-223">ロックされているプロパティはロック ファイルから削除[#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="b1f69-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="b1f69-224">NuGet 3.3.0 更新が失敗 '... 制約で定義されている packages.config には、この動作ができなくなります '。</span><span class="sxs-lookup"><span data-stu-id="b1f69-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="b1f69-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="b1f69-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="b1f69-226">無効なメッセージがスローされますが存在しないローカル ソースからパッケージをインストールする[#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="b1f69-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="b1f69-227">「アップグレード可能」フィルターはバージョン制約に違反するアップグレードでは、表示[#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="b1f69-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="b1f69-228">-ネイティブのパッケージを更新できません[#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="b1f69-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="b1f69-229">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="b1f69-229">Features</span></span>

* <span data-ttu-id="b1f69-230">NuGet - によって追加された参照を false に設定 CopyLocal をサポートして[#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="b1f69-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="b1f69-231">MSBuild 15 - nuget.exe サポート[#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="b1f69-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="b1f69-232">パックのサポート。`csproj`</span><span class="sxs-lookup"><span data-stu-id="b1f69-232">Pack support for .`csproj`</span></span><span data-ttu-id="b1f69-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="b1f69-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="b1f69-234">実行されているユーザーの操作がある場合は、ユーザーの操作を無効にする- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="b1f69-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="b1f69-235">NuGet のサポートを追加する必要があります`runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="b1f69-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="b1f69-236">NuGet で不足しているフレームワークの互換性を追加 (これは 3.x で、既に) 2.x - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="b1f69-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="b1f69-237">フォールバックのパッケージ フォルダー - サポート[#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="b1f69-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="b1f69-238">設計および実装ツール パッケージをサポートするには、パッケージの種類の概念[#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="b1f69-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="b1f69-239">グローバル パッケージ フォルダーのパスを取得するための API を追加[#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="b1f69-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="b1f69-240">パックには、SemVer 2.0.0 を有効にする[#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="b1f69-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="b1f69-241">DCR</span><span class="sxs-lookup"><span data-stu-id="b1f69-241">DCRs</span></span>

* <span data-ttu-id="b1f69-242">nuget.exe プッシュのタイムアウト パラメーターは機能しません - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="b1f69-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="b1f69-243">パッケージの説明テキストが選択できる - [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="b1f69-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="b1f69-244">生成するために nuget.exe を有効にする`.props`と`.targets`ファイル`.nuproj`プロジェクト[#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="b1f69-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="b1f69-245">機能拡張フレームワークの imports とを比較する API を追加[#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="b1f69-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="b1f69-246">使用する場合は、依存関係のオプションを非表示に`project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="b1f69-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="b1f69-247">詳細な出力 - で nuget.exe のバージョン ヘッダーを印刷[#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="b1f69-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="b1f69-248">NuGet は、ベース dotnet tfm でアップグレード/インストール PCL の問題が生じたり - ユーザーに通知する必要があります[#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="b1f69-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="b1f69-249">Tfm を使用したプロジェクトの不適切なインストールまたはアップグレードを警告する ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="b1f69-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="b1f69-250">ReShaper と NuGet の更新 - パフォーマンスの問題を修正[#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="b1f69-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="b1f69-251">追加 netcoreapp11 と netstandard17 サポート - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="b1f69-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="b1f69-252">利用して AssemblyMetadata 属性`.nuspec`トークンの置換 - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="b1f69-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
