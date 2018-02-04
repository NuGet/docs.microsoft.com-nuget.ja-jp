---
title: "NuGet 3.5 のベータ リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.5 用のリリース ノートです。"
keywords: "NuGet 3.5 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ee78ceb2ff032c05c0f8ef9a6623b94cc56ee0a9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="bb44b-104">NuGet 3.5 のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="bb44b-104">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="bb44b-105">[NuGet 3.5 RC のリリース ノート](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC のリリース ノートには](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="bb44b-105">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="bb44b-106">バグ修正</span><span class="sxs-lookup"><span data-stu-id="bb44b-106">Bug Fixes</span></span>

* <span data-ttu-id="bb44b-107">パックは、mono - に MSBuild 14.1 を使用しない[#3550](https://github.com/NuGet/Home/issues/3550)</span><span class="sxs-lookup"><span data-stu-id="bb44b-107">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="bb44b-108">更新プログラム タブは、代わりに現在インストールされているバージョンの選択を更新する最新バージョンを選択しない[#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="bb44b-108">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="bb44b-109">フィードの MyGet プライベート v2 を認証し、詳細結果 x [表示] をクリックした後のクラッシュを修正しました- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="bb44b-109">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="bb44b-110">ログ メッセージは、UI の逆の順序でのように見えて[#3446](https://github.com/NuGet/Home/issues/3446)</span><span class="sxs-lookup"><span data-stu-id="bb44b-110">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="bb44b-111">「指定されたパスの形式はサポートされていません -」をスロー v3.4.4 - Nuget 復元[#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="bb44b-111">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="bb44b-112">NuGet cmdLine 3.6 beta を認めません - Prop 構成リリースを = [#3432](https://github.com/NuGet/Home/issues/3432)</span><span class="sxs-lookup"><span data-stu-id="bb44b-112">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="bb44b-113">Nuget IKVM 低速に大規模なプロジェクトは、インストール[#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="bb44b-113">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="bb44b-114">nuget.exe 自己保持で更新自体の更新[#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="bb44b-114">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="bb44b-115">UNC 共有から 3.5 のインストール/復元が 3.4.4 - からパフォーマンス回帰[#3355](https://github.com/NuGet/Home/issues/3355)</span><span class="sxs-lookup"><span data-stu-id="bb44b-115">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="bb44b-116">エラー - net451 プロジェクトのパッケージ管理 UI から Moq をインストールするときに[#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="bb44b-116">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="bb44b-117">ソリューション レベルでのインストール タブは、パッケージのバージョンを表示しない[#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="bb44b-117">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="bb44b-118">xproj`project.json`インストール済み タブから更新プログラムを失った状態 - [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="bb44b-118">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="bb44b-119">NuGet パック`.csproj`内の空のファイルの要素を無視`.nuspec`ファイル - [#3257](https://github.com/NuGet/Home/issues/3257)</span><span class="sxs-lookup"><span data-stu-id="bb44b-119">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="bb44b-120">IIS でホストされる web サイト プロジェクト原因にはなりません復元が失敗 - [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="bb44b-120">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="bb44b-121">資格情報が v2 - v3 エンドポイントにリダイレクト時に Nuget.Config から取得されない[#3179](https://github.com/NuGet/Home/issues/3179)</span><span class="sxs-lookup"><span data-stu-id="bb44b-121">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="bb44b-122">ポータブル アセンブリ メタデータを取得するときに、アセンブリを解決するのには NuGet のパックが失敗した[#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="bb44b-122">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="bb44b-123">Nuget を見つけることができません`msbuild.exe`モノラル -  [#3085](https://github.com/NuGet/Home/issues/3085)</span><span class="sxs-lookup"><span data-stu-id="bb44b-123">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="bb44b-124">nuget.exe パックは、プレリリース版のタグ番号 - で始まるを許可しない[#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="bb44b-124">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="bb44b-125">VS2015E - で nuget パッケージのインストールが失敗した[#1298](https://github.com/NuGet/Home/issues/1298)</span><span class="sxs-lookup"><span data-stu-id="bb44b-125">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="bb44b-126">allowedVersions ソリューション レベルでない作業をフィルター処理[#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="bb44b-126">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="bb44b-127">復元にランダムに同じ項目に失敗したキーが既に追加されています。</span><span class="sxs-lookup"><span data-stu-id="bb44b-127">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="bb44b-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="bb44b-128"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="bb44b-129">Nuget.Common をインストールすることはできません`.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)</span><span class="sxs-lookup"><span data-stu-id="bb44b-129">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="bb44b-130">UI を使用して、V2 のソースを検索、FindPackagesById が各 ID - に対して 2 回呼び出されます[#2517。](https://github.com/NuGet/Home/issues/2517)</span><span class="sxs-lookup"><span data-stu-id="bb44b-130">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="bb44b-131">パッケージのプロジェクトに依存できません[#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="bb44b-131">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="bb44b-132">nuget.exe パック - 除外が記載されていますが、サポートされていません - [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="bb44b-132">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="bb44b-133">メッセージ エラーに関する問題の 'コンテンツ ファイル' セクション`.nuspec`無効です - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="bb44b-133">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="bb44b-134">パッケージ全体 2 回の認証パッケージ ソースのプッシュが常に送信[#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="bb44b-134">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="bb44b-135">について指定されていませんプロジェクトの中に nuget.exe 更新 \*.csproj を呼び出すことがないとき、 `packages.config`  -  [#1496。](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="bb44b-135">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="bb44b-136">`packages.config`5 xx 状態コード - V2 のソースからの復元を再試行しません[#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="bb44b-136">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="bb44b-137">2 つのドットでファイル src で`.nuspec`それでも - [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="bb44b-137">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="bb44b-138">暗号化に使用したフィードを無視する必要がある CoreCLR 復元[#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="bb44b-138">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="bb44b-139">nuget.exe プッシュに正しくの入力を求めていません資格情報 - 403 処理[#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="bb44b-139">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="bb44b-140">パッケージ マネージャーで NuGet の更新プログラムがからプロパティを削除、 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)</span><span class="sxs-lookup"><span data-stu-id="bb44b-140">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="bb44b-141">NuGet.PackageManagement.VisualStudio"NuGet.TeamFoundationServer14"が"NuGet.TeamFoundationServer"- に DLL の名前が変更されたことをロードしようとしました[#2857。](https://github.com/NuGet/Home/issues/2857)</span><span class="sxs-lookup"><span data-stu-id="bb44b-141">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="bb44b-142">パッケージ マネージャーの UI が新しく表示されない更新バージョン - [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="bb44b-142">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="bb44b-143">更新プログラム パッケージのパッケージ id を使用しようとしています package.version - ではなくバージョン[#2771。](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="bb44b-143">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="bb44b-144">nuget 復元 csproj は、プロジェクトは、nuget を使用していない場合、エラーを必要があります (`packages.config`または`project.json`)- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="bb44b-144">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="bb44b-145">TFS エラー"[ファイル]、ワークスペースに存在することできませんまたはへのアクセス許可がありません"中にアップグレードまたはアンインストール ソリューション/プロジェクトが TFS ソース コントロールにバインドされると[#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="bb44b-145">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="bb44b-146">更新プログラム パッケージが目標ではないパッケージの依存関係を取得しない[#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="bb44b-146">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="bb44b-147">Nuget パッケージ マネージャーの UI アクションのログ詳細レベルを設定する方法はありません[#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="bb44b-147">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="bb44b-148">nuget 構成が無効です - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="bb44b-148">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="bb44b-149">DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) は機能しません - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="bb44b-149">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="bb44b-150">nuget 3.4.3 リリースの値を取得することはできません null にする - パッケージのビルドで[#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="bb44b-150">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="bb44b-151">復元 VSTS フィード - Nuget.Config から保存された資格情報が使用されていない[#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="bb44b-151">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="bb44b-152">[dotnet 復元]--configfile は cmd dir - の代わりにプロジェクト ディレクトリに対する相対[#2639](https://github.com/NuGet/Home/issues/2639)</span><span class="sxs-lookup"><span data-stu-id="bb44b-152">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="bb44b-153">バージョンの比較コード - 内の過剰割り当て[#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="bb44b-153">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="bb44b-154">同じをインストールしようとしています nuget.exe の複数のインスタンスのパッケージ化は並列原因二重書き込み - [#2628。](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="bb44b-154">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="bb44b-155">複数プロジェクトの操作 - の依存関係情報はキャッシュされません[#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="bb44b-155">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="bb44b-156">インストールし、更新プログラムのダウンロード パッケージを最初のパッケージ フォルダーをチェックせず[#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="bb44b-156">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="bb44b-157">パッケージ ソースの一覧が空の場合は、UI を使用してパッケージのソースを追加できません (NuGet 3.4.x)- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="bb44b-157">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="bb44b-158">デザイン時のファサード - に依存しているパッケージをインストールしようとしましたエラーは誤解を招く[#2594。](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="bb44b-158">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="bb44b-159">だけ最初のソースの設定"All"PackageManager コンソールから、パッケージをインストールしようと[#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="bb44b-159">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="bb44b-160">最新のベータ版がない解凍 ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="bb44b-160">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="bb44b-161">ビルドされた自己 NuGet 3.4.1 - 起動時 VS2015 クラッシュ[#2419](https://github.com/NuGet/Home/issues/2419)</span><span class="sxs-lookup"><span data-stu-id="bb44b-161">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="bb44b-162">更新コマンドの場合は i を依頼する... - より詳細可能性があります[#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="bb44b-162">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="bb44b-163">ローカルでビルドされた VSIX は、CI ビルドとして同じ Dll とファイルが必要です。</span><span class="sxs-lookup"><span data-stu-id="bb44b-163">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="bb44b-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="bb44b-164"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="bb44b-165">ビルド - NuGet ダウン グレードの警告を修正[#2396](https://github.com/NuGet/Home/issues/2396)</span><span class="sxs-lookup"><span data-stu-id="bb44b-165">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="bb44b-166">パッケージ ソース (3 倍) の認証に失敗したがブロックされている永続 - [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="bb44b-166">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="bb44b-167">引数でフィード nuget v3.3 + からパッケージをインストールするときにパッケージの内容は正しく復元されません - NoCache パッケージが含まれている`.nupkg`ファイル - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="bb44b-167">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="bb44b-168">すべてのパッケージ ソースが見つからない、1 つのソースからパッケージを使用して Nuget のインストールが失敗した場合 - [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="bb44b-168">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="bb44b-169">[PerfWatson]UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt です。&gt;c__DisplayClass_0 +&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="bb44b-169">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="bb44b-170">1 つのソースの承認に失敗した場合は、ブロックをインストール[#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="bb44b-170">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="bb44b-171">`.nuspec`バージョン範囲は-IncludeReferencedProjects バージョン - をオーバーライドする必要があります[#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="bb44b-171">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="bb44b-172">更新プログラム パッケージ super 速度の遅い -「しようとした依存関係情報を収集する」- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="bb44b-172">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="bb44b-173">鋭いのダウン グレードの NuGet パッケージの場合にバッチ更新の依存関係 - [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="bb44b-173">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="bb44b-174">nuget.exe の更新プログラムは、アセンブリの厳密な名前およびプライベートの属性を削除します。</span><span class="sxs-lookup"><span data-stu-id="bb44b-174">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="bb44b-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="bb44b-175"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="bb44b-176">"DefaultPushSource"- の相対ファイル パス[#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="bb44b-176">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="bb44b-177">競合回避モジュール エラー メッセージを向上させる[#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="bb44b-177">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="bb44b-178">-指定したソースでないパッケージ v3 での更新プログラム パッケージが失敗した[#1013](https://github.com/NuGet/Home/issues/1013)</span><span class="sxs-lookup"><span data-stu-id="bb44b-178">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="bb44b-179">パッケージ ソースの相対パスを使用するにを使用する問題が[#865](https://github.com/NuGet/Home/issues/865)</span><span class="sxs-lookup"><span data-stu-id="bb44b-179">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="bb44b-180">NUPKG ファイルを下位バージョンの要件では、間接的な依存関係が既に存在する場合は、プロジェクトから生成された依存関係がありません[#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="bb44b-180">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="bb44b-181">対応する UI ウィンドウを閉じますプロジェクトの削除は、プロジェクトの名前を変更する名前は変更されません UI ウィンドウ。</span><span class="sxs-lookup"><span data-stu-id="bb44b-181">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="bb44b-182">注 PMC をプロジェクトの名前変更、およびプロジェクトの削除イベントのリッスン[#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="bb44b-182">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="bb44b-183">[Willow Web ワークロード]Razor v3 WSP の作成がハングする - [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="bb44b-183">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="bb44b-184">「パッケージには、複数の nuspec ファイルが含まれています」で特定のパッケージのインストール/復元が失敗します。</span><span class="sxs-lookup"><span data-stu-id="bb44b-184">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="bb44b-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="bb44b-185"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="bb44b-186">小文字の Id (& a)`packages.config`シナリオ - [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="bb44b-186">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="bb44b-187">[3.5 beta2]パッケージの復元が「レガシ」パッケージの復元に失敗した[#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="bb44b-187">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="bb44b-188">nuget パックでは、新機能に関係なくコンテンツ フォルダーを .tt ファイルを強制的に追加[#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="bb44b-188">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="bb44b-189">ASP.NET web アプリの更新プログラム パッケージには、ファイルに関連する警告が生成されますソースの構成 - [#3194。](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="bb44b-189">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="bb44b-190">nuget パック csproj (で`project.json`) packOptions と JSON ファイルの所有者が存在しない場合のクラッシュ[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="bb44b-190">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="bb44b-191">用の nuget パック`project.json`概要、作成者、所有者などのような packOptions タグは無視[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="bb44b-191">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="bb44b-192">NuGet.Packaging.PhysicalPackageFile.GetStream - を介して NullReferenceException [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="bb44b-192">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="bb44b-193">出力内の依存関係が NuGet パックには無視されます`.nuspec`の`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="bb44b-193">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="bb44b-194">ロールバックを含む複数のパッケージの更新結果が、プロジェクト、破損状態 - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="bb44b-194">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="bb44b-195">Netstandard プロジェクトのいずれかの下にあるコンテンツ ファイルは追加されません[#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="bb44b-195">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="bb44b-196">ターゲットを .Net ライブラリをパッケージすることはできません標準正しく - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="bb44b-196">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="bb44b-197">ファイルに新しいプロジェクト]-> [クラス ライブラリ (ポータブル) プロジェクトが失敗する VS2015 と Dev15 - -> [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="bb44b-197">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="bb44b-198">NuGet エラー - 1.0.0-\* は有効なバージョン文字列ではありません[#3070。](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="bb44b-198">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="bb44b-199">表示、パッケージのインストールの動作の失敗した Find-package [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="bb44b-199">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="bb44b-200">エラー時"Install-package jquery.validation"dev15 -  [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="bb44b-200">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="bb44b-201">xproj の nuget パックは既定で無効なターゲット パス - [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="bb44b-201">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="bb44b-202">VS 2015 がインストールされているバージョン 3.5.0 エラーが発生した、NuGet を使用すると上の 3 を更新するときに[#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="bb44b-202">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="bb44b-203">「Packages.config によってブロック」 `project.json` (UWP、別名のビルドと統合) プロジェクト - [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="bb44b-203">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="bb44b-204">これは、公式 preview2 ビルド preview2 003121 をビルド スクリプトがインストールされている dotnet cli を更新します。</span><span class="sxs-lookup"><span data-stu-id="bb44b-204">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="bb44b-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="bb44b-205"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="bb44b-206">パッケージ マネージャーの UI: パッケージを更新した後に新しいバージョンが表示されない- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="bb44b-206">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="bb44b-207">-ApiKey delete コマンド ラインでは、読み取り/に送信されない 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="bb44b-207">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="bb44b-208">不適切な文字列: 安定したパッケージのリリースのプレリリースの依存関係のないです。</span><span class="sxs-lookup"><span data-stu-id="bb44b-208">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="bb44b-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="bb44b-209"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="bb44b-210">OptimizedZipPackage キャッシュが空のフォルダーの[#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="bb44b-210">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="bb44b-211">PCL (net46 および windows 10) プロジェクト get NullRef 例外を作成します。</span><span class="sxs-lookup"><span data-stu-id="bb44b-211">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="bb44b-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="bb44b-212"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="bb44b-213">AllowedVersions 制約 - によってより新しいバージョンが制限されているときに、Nuget の更新プログラムは情報メッセージを提供する必要があります[#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="bb44b-213">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="bb44b-214">Nuget v3 の復元に関する問題 - [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="bb44b-214">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="bb44b-215">資格情報のプラグインは、エラー-1 で終了しましたエラーをダウンロードする、複数のソースの資格情報プロバイダーを使用する場合にパッケージ化/ [#2885。](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="bb44b-215">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="bb44b-216">`project.json`nuget の復元時に変更されました - 何も再コンパイルの原因[#2817](https://github.com/NuGet/Home/issues/2817)</span><span class="sxs-lookup"><span data-stu-id="bb44b-216">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="bb44b-217">シンボルしていないパッケージを今まででインストールまたは更新に使用される[#2807](https://github.com/NuGet/Home/issues/2807)</span><span class="sxs-lookup"><span data-stu-id="bb44b-217">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="bb44b-218">VS が repositoryPath 内の環境変数をサポートしていません (nuget.exe は) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="bb44b-218">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="bb44b-219">パッケージ マネージャー UI のラベル付けされていない Uielement をラベルにユーザー補助 - [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="bb44b-219">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="bb44b-220">ハイフンでつながれたプロファイルでポータブル フレームワークは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="bb44b-220">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="bb44b-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="bb44b-221"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="bb44b-222">NuGet パッケージ マネージャーで、詳細には適用されませんパッケージでそのオプションの一覧を明確にするため必要があります`project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="bb44b-222">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="bb44b-223">nuget.exe プッシュ/削除の API キーを使用しない[#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="bb44b-223">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="bb44b-224">ロックされているプロパティ ファイルから削除、ロックの[#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="bb44b-224">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="bb44b-225">NuGet 3.3.0 更新で失敗 ' 追加の制約 で定義されている packages.config には、この動作ができなくなります '。</span><span class="sxs-lookup"><span data-stu-id="bb44b-225">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="bb44b-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="bb44b-226"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="bb44b-227">無効なメッセージのスローを存在しないローカル ソースからパッケージをインストールする[#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="bb44b-227">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="bb44b-228">「アップグレード」使用可能なフィルターは、表示のバージョンの制約に違反するアップグレード[#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="bb44b-228">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="bb44b-229">ネイティブなパッケージを更新できません[#1291。](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="bb44b-229">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="bb44b-230">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="bb44b-230">Features</span></span>

* <span data-ttu-id="bb44b-231">追加された NuGet - によって参照に false に設定 CopyLocal をサポートして[#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="bb44b-231">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="bb44b-232">MSBuild 15 - nuget.exe サポート[#1937](https://github.com/NuGet/Home/issues/1937)</span><span class="sxs-lookup"><span data-stu-id="bb44b-232">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="bb44b-233">サポートをパックします。`csproj`</span><span class="sxs-lookup"><span data-stu-id="bb44b-233">Pack support for .`csproj`</span></span><span data-ttu-id="bb44b-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="bb44b-234"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="bb44b-235">実行されているユーザーの操作がある場合は、ユーザーの操作を無効にする- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="bb44b-235">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="bb44b-236">NuGet のサポートを追加する必要があります`runtimes/{rid}/nativeassets/{txm}/`  -  [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="bb44b-236">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="bb44b-237">NuGet で見つからない framework の互換性を追加 (既ににある 3.x) 2.x - [#2720](https://github.com/NuGet/Home/issues/2720)</span><span class="sxs-lookup"><span data-stu-id="bb44b-237">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="bb44b-238">-フォールバック パッケージ フォルダーへのサポート[#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="bb44b-238">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="bb44b-239">設計およびツール パッケージをサポートするには、パッケージの種類の概念を実装[#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="bb44b-239">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="bb44b-240">グローバルのパッケージ フォルダーへのパスを取得するために API を追加[#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="bb44b-240">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="bb44b-241">パックに SemVer 2.0.0 を有効にする[#3356](https://github.com/NuGet/Home/issues/3356)</span><span class="sxs-lookup"><span data-stu-id="bb44b-241">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="bb44b-242">DCR</span><span class="sxs-lookup"><span data-stu-id="bb44b-242">DCRs</span></span>

* <span data-ttu-id="bb44b-243">nuget.exe プッシュ タイムアウト パラメーターは機能しません - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="bb44b-243">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="bb44b-244">パッケージの説明テキストが選択可能にする必要があります[#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="bb44b-244">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="bb44b-245">生成するために nuget.exe を有効にする`.props`と`.targets`ファイル`.nuproj`プロジェクト[#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="bb44b-245">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="bb44b-246">フレームワークのインポートとを比較する API の機能を拡張する[#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="bb44b-246">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="bb44b-247">使用する場合は、依存関係のオプションを非表示に`project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="bb44b-247">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="bb44b-248">詳細な出力に nuget.exe バージョン ヘッダーを印刷[#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="bb44b-248">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="bb44b-249">NuGet は、ユーザーがいるベース dotnet tfm でアップグレード/インストール PCL に問題が発生の通知する必要があります[#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="bb44b-249">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="bb44b-250">Tfm を使用したプロジェクトの不適切なインストールまたはアップグレードに警告する ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="bb44b-250">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="bb44b-251">ReShaper と NuGet の更新のパフォーマンスの問題を修正[#3044](https://github.com/NuGet/Home/issues/3044)</span><span class="sxs-lookup"><span data-stu-id="bb44b-251">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="bb44b-252">Netcoreapp11 と netstandard17 サポート - 追加[#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="bb44b-252">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="bb44b-253">活用 AssemblyMetadata 属性`.nuspec`トークンの置換 - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="bb44b-253">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
