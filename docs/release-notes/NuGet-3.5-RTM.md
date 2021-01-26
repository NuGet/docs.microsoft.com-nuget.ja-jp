---
title: NuGet 3.5 RTM リリース ノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 158373fb62f57fe6947fb863a1eef8122399959a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776355"
---
# <a name="nuget-35-release-notes"></a><span data-ttu-id="a7978-103">NuGet 3.5 リリースノート</span><span class="sxs-lookup"><span data-stu-id="a7978-103">NuGet 3.5 Release Notes</span></span>

<span data-ttu-id="a7978-104">[NuGet 3.5-RC リリースノート](../release-notes/nuget-3.5-RC.md)  | [NuGet 4.0 RC リリースノート](../release-notes/nuget-4.0-RC.md)</span><span class="sxs-lookup"><span data-stu-id="a7978-104">[NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md) | [NuGet 4.0 RC Release Notes](../release-notes/nuget-4.0-RC.md)</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="a7978-105">バグの修正</span><span class="sxs-lookup"><span data-stu-id="a7978-105">Bug Fixes</span></span>

* <span data-ttu-id="a7978-106">パッケージが mono [#3550](https://github.com/NuGet/Home/issues/3550)で MSBuild 14.1 を使用していない</span><span class="sxs-lookup"><span data-stu-id="a7978-106">Pack doesn't use MSBuild 14.1 on mono - [#3550](https://github.com/NuGet/Home/issues/3550)</span></span>

* <span data-ttu-id="a7978-107">[更新] タブでは、更新に使用できる最新のバージョンが選択されていません。現在インストールされているバージョンを選択し [#3498](https://github.com/NuGet/Home/issues/3498)</span><span class="sxs-lookup"><span data-stu-id="a7978-107">Update tab doesn't select the latest available version to update instead select current installed version - [#3498](https://github.com/NuGet/Home/issues/3498)</span></span>

* <span data-ttu-id="a7978-108">プライベート v2 MyGet feed を認証し、[その他の結果を表示] をクリックした後にクラッシュを修正する- [#3469](https://github.com/NuGet/Home/issues/3469)</span><span class="sxs-lookup"><span data-stu-id="a7978-108">Fix Crash after authenticating a private v2 MyGet feed and clicking "Show x more results" - [#3469](https://github.com/NuGet/Home/issues/3469)</span></span>

* <span data-ttu-id="a7978-109">ログメッセージは、UI [#3446](https://github.com/NuGet/Home/issues/3446)の逆の順序であるように見えます。</span><span class="sxs-lookup"><span data-stu-id="a7978-109">Log messages seem to be in reverse order for UI - [#3446](https://github.com/NuGet/Home/issues/3446)</span></span>

* <span data-ttu-id="a7978-110">v 3.4.4-Nuget の復元で "指定されたパスの形式はサポートされていません"- [#3442](https://github.com/NuGet/Home/issues/3442)</span><span class="sxs-lookup"><span data-stu-id="a7978-110">v3.4.4 - Nuget restore throws "The given path's format is not supported" - [#3442](https://github.com/NuGet/Home/issues/3442)</span></span>

* <span data-ttu-id="a7978-111">NuGet cmdLine 3.6 beta は、Prop Configuration = Release- [#3432](https://github.com/NuGet/Home/issues/3432)を優先しません</span><span class="sxs-lookup"><span data-stu-id="a7978-111">NuGet cmdLine 3.6 beta does not honor -Prop Configuration = Release - [#3432](https://github.com/NuGet/Home/issues/3432)</span></span>

* <span data-ttu-id="a7978-112">大規模なプロジェクトでの Nuget IKVM の遅いインストール- [#3428](https://github.com/NuGet/Home/issues/3428)</span><span class="sxs-lookup"><span data-stu-id="a7978-112">Nuget IKVM slow install on large project - [#3428](https://github.com/NuGet/Home/issues/3428)</span></span>

* <span data-ttu-id="a7978-113">nuget.exe 更新プログラム-自己更新 (自己更新)- [#3395](https://github.com/NuGet/Home/issues/3395)</span><span class="sxs-lookup"><span data-stu-id="a7978-113">nuget.exe Update -Self keeps on updating itself - [#3395](https://github.com/NuGet/Home/issues/3395)</span></span>

* <span data-ttu-id="a7978-114">3.5 UNC 共有からのインストール/復元は[#3355](https://github.com/NuGet/Home/issues/3355) 3.4.4 からのパフォーマンスの回帰を持つ</span><span class="sxs-lookup"><span data-stu-id="a7978-114">3.5 install/restore from UNC share has performance Regression from 3.4.4 - [#3355](https://github.com/NuGet/Home/issues/3355)</span></span>

* <span data-ttu-id="a7978-115">Net451 プロジェクトのパッケージ管理 UI から Moq をインストールするときにエラーが発生する- [#3349](https://github.com/NuGet/Home/issues/3349)</span><span class="sxs-lookup"><span data-stu-id="a7978-115">Error when installing Moq from the Package management UI for a net451 project - [#3349](https://github.com/NuGet/Home/issues/3349)</span></span>

* <span data-ttu-id="a7978-116">ソリューションレベルの [インストール] タブにパッケージのバージョンが表示されない- [#3339](https://github.com/NuGet/Home/issues/3339)</span><span class="sxs-lookup"><span data-stu-id="a7978-116">Install tab at solution level doesn't show package's version - [#3339](https://github.com/NuGet/Home/issues/3339)</span></span>

* <span data-ttu-id="a7978-117">xproj `project.json` 更新プログラムがインストールされたタブから状態が失われる- [#3303](https://github.com/NuGet/Home/issues/3303)</span><span class="sxs-lookup"><span data-stu-id="a7978-117">xproj `project.json` update from Installed tab loses state - [#3303](https://github.com/NuGet/Home/issues/3303)</span></span>

* <span data-ttu-id="a7978-118">の NuGet パック `.csproj` は `.nuspec` 、ファイル[#3257](https://github.com/NuGet/Home/issues/3257)内の空のファイル要素を無視します</span><span class="sxs-lookup"><span data-stu-id="a7978-118">NuGet pack on `.csproj` ignores empty files element in `.nuspec` file - [#3257](https://github.com/NuGet/Home/issues/3257)</span></span>

* <span data-ttu-id="a7978-119">IIS でホストされている web サイトプロジェクトで復元が失敗することはありません- [#3235](https://github.com/NuGet/Home/issues/3235)</span><span class="sxs-lookup"><span data-stu-id="a7978-119">Website projects hosted in IIS should not cause restore to fail - [#3235](https://github.com/NuGet/Home/issues/3235)</span></span>

* <span data-ttu-id="a7978-120">V3 エンドポイントが v2- [#3179](https://github.com/NuGet/Home/issues/3179)にリダイレクトされると、Nuget.Config から資格情報が取得されない</span><span class="sxs-lookup"><span data-stu-id="a7978-120">Credentials not retrieved from Nuget.Config when v3 endpoint redirects to v2 - [#3179](https://github.com/NuGet/Home/issues/3179)</span></span>

* <span data-ttu-id="a7978-121">ポータブルアセンブリメタデータを取得するときに NuGet パックがアセンブリを解決できない- [#3128](https://github.com/NuGet/Home/issues/3128)</span><span class="sxs-lookup"><span data-stu-id="a7978-121">NuGet pack fails to resolve assembly when retrieving portable assembly metadata - [#3128](https://github.com/NuGet/Home/issues/3128)</span></span>

* <span data-ttu-id="a7978-122">Nuget `msbuild.exe` が Mono [#3085](https://github.com/NuGet/Home/issues/3085)で見つかりません</span><span class="sxs-lookup"><span data-stu-id="a7978-122">Nuget can't find `msbuild.exe` on Mono - [#3085](https://github.com/NuGet/Home/issues/3085)</span></span>

* <span data-ttu-id="a7978-123">nuget.exe パックでは、番号で始まるプレリリースタグを許可しません- [#1743](https://github.com/NuGet/Home/issues/1743)</span><span class="sxs-lookup"><span data-stu-id="a7978-123">nuget.exe pack doesn't allow a pre-release tag which begins with numbers - [#1743](https://github.com/NuGet/Home/issues/1743)</span></span>

* <span data-ttu-id="a7978-124">[#1298](https://github.com/NuGet/Home/issues/1298) VS2015E で nuget パッケージのインストールが失敗する</span><span class="sxs-lookup"><span data-stu-id="a7978-124">nuget package install fails on VS2015E - [#1298](https://github.com/NuGet/Home/issues/1298)</span></span>

* <span data-ttu-id="a7978-125">allowedVersions フィルターがソリューションレベルで機能していません- [#333](https://github.com/NuGet/Home/issues/333)</span><span class="sxs-lookup"><span data-stu-id="a7978-125">allowedVersions filter not working at solution level - [#333](https://github.com/NuGet/Home/issues/333)</span></span>

* <span data-ttu-id="a7978-126">同じキーを持つ項目が既に追加されているため、復元はランダムに失敗します。</span><span class="sxs-lookup"><span data-stu-id="a7978-126">Restore randomly fails with An item with the same key has already been added.</span></span><span data-ttu-id="a7978-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span><span class="sxs-lookup"><span data-stu-id="a7978-127"> - [#2646](https://github.com/NuGet/Home/issues/2646)</span></span>

* <span data-ttu-id="a7978-128">Nuget をインストールできません。 `.csproj`  -  [#2635](https://github.com/NuGet/Home/issues/2635)に共通</span><span class="sxs-lookup"><span data-stu-id="a7978-128">Cannot install Nuget.Common in `.csproj` - [#2635](https://github.com/NuGet/Home/issues/2635)</span></span>

* <span data-ttu-id="a7978-129">UI を使用して V2 ソースを検索する場合、FindPackagesById は各[#2517](https://github.com/NuGet/Home/issues/2517) ID に対して2回呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="a7978-129">When using the UI to search a V2 source, FindPackagesById is called twice for each ID - [#2517](https://github.com/NuGet/Home/issues/2517)</span></span>

* <span data-ttu-id="a7978-130">パッケージはプロジェクトに依存できません- [#2490](https://github.com/NuGet/Home/issues/2490)</span><span class="sxs-lookup"><span data-stu-id="a7978-130">Packages cannot depend on projects - [#2490](https://github.com/NuGet/Home/issues/2490)</span></span>

* <span data-ttu-id="a7978-131">nuget.exe pack-Exclude はドキュメントに記載されていますが、サポートされていません- [#2284](https://github.com/NuGet/Home/issues/2284)</span><span class="sxs-lookup"><span data-stu-id="a7978-131">nuget.exe pack -Exclude is documented but not supported - [#2284](https://github.com/NuGet/Home/issues/2284)</span></span>

* <span data-ttu-id="a7978-132">の ' contentFiles ' セクションが無効な場合のエラーメッセージに関する問題 `.nuspec` - [#1686](https://github.com/NuGet/Home/issues/1686)</span><span class="sxs-lookup"><span data-stu-id="a7978-132">Issues with error messages when 'contentFiles' section of `.nuspec` is invalid - [#1686](https://github.com/NuGet/Home/issues/1686)</span></span>

* <span data-ttu-id="a7978-133">プッシュは、常にパッケージ全体を、認証されたパッケージソースと共に2回送信します- [#1501](https://github.com/NuGet/Home/issues/1501)</span><span class="sxs-lookup"><span data-stu-id="a7978-133">Push always sends entire package twice with authenticated package sources - [#1501](https://github.com/NuGet/Home/issues/1501)</span></span>

* <span data-ttu-id="a7978-134">プロジェクトに #1496 がないときに nuget.exe update \* .csproj を呼び出すときに情報が指定されませんでした `packages.config`  -  [](https://github.com/NuGet/Home/issues/1496)</span><span class="sxs-lookup"><span data-stu-id="a7978-134">No information was given when calling nuget.exe update \*.csproj while the project does not have a `packages.config` - [#1496](https://github.com/NuGet/Home/issues/1496)</span></span>

* <span data-ttu-id="a7978-135">`packages.config` 復元では、V2 ソースからの5xx 状態コードでは再試行されません- [#1217](https://github.com/NuGet/Home/issues/1217)</span><span class="sxs-lookup"><span data-stu-id="a7978-135">`packages.config` restore does not retry on 5xx status codes from V2 sources - [#1217](https://github.com/NuGet/Home/issues/1217)</span></span>

* <span data-ttu-id="a7978-136">のファイル src の2つのドット `.nuspec` が機能しません- [#2947](https://github.com/NuGet/Home/issues/2947)</span><span class="sxs-lookup"><span data-stu-id="a7978-136">Double dot in file src in `.nuspec` doesn't work - [#2947](https://github.com/NuGet/Home/issues/2947)</span></span>

* <span data-ttu-id="a7978-137">CoreCLR 復元では、暗号化を使用したフィードを無視する必要があり [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="a7978-137">CoreCLR restore needs to ignore feeds with encryption - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="a7978-138">nuget.exe push 403 処理-資格情報の入力を誤って要求しています- [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="a7978-138">nuget.exe push 403 handling - Incorrectly prompting for credentials - [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="a7978-139">パッケージマネージャーを使用した NuGet の更新では、 `project.json`  -  [#2888](https://github.com/NuGet/Home/issues/2888)からプロパティを削除します</span><span class="sxs-lookup"><span data-stu-id="a7978-139">NuGet update through package manager removes properties from the `project.json` - [#2888](https://github.com/NuGet/Home/issues/2888)</span></span>

* <span data-ttu-id="a7978-140">VisualStudio は "TeamFoundationServer14" の読み込みを試行しますが、その DLL 名は "NuGet. Teamfound Ationserver"- [#2857](https://github.com/NuGet/Home/issues/2857)に変更されました</span><span class="sxs-lookup"><span data-stu-id="a7978-140">NuGet.PackageManagement.VisualStudio try to load "NuGet.TeamFoundationServer14", but that DLL name changed to "NuGet.TeamFoundationServer" - [#2857](https://github.com/NuGet/Home/issues/2857)</span></span>

* <span data-ttu-id="a7978-141">パッケージマネージャー UI に新しく更新されたバージョンが表示されない- [#2828](https://github.com/NuGet/Home/issues/2828)</span><span class="sxs-lookup"><span data-stu-id="a7978-141">Package manager UI doesn't show newly updated version - [#2828](https://github.com/NuGet/Home/issues/2828)</span></span>

* <span data-ttu-id="a7978-142">packageid の代わりにを使用しようとしているパッケージのバージョン- [#2771](https://github.com/NuGet/Home/issues/2771)</span><span class="sxs-lookup"><span data-stu-id="a7978-142">update-package trying to use packageid,version instead of package.version - [#2771](https://github.com/NuGet/Home/issues/2771)</span></span>

* <span data-ttu-id="a7978-143">プロジェクトが nuget (または) を使用していない場合は、nuget の restore .csproj がエラーになります ( `packages.config` または `project.json` )- [#2766](https://github.com/NuGet/Home/issues/2766)</span><span class="sxs-lookup"><span data-stu-id="a7978-143">nuget restore csproj should error if the project isn't using nuget (`packages.config` or `project.json`) - [#2766](https://github.com/NuGet/Home/issues/2766)</span></span>

* <span data-ttu-id="a7978-144">Tfs エラー "[ファイル] がワークスペースに見つかりません。または、ソリューション/プロジェクトが TFS ソース管理にバインドされている場合、アップグレードまたはアンインストール中に、このファイルにアクセスするためのアクセス許可がありません- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="a7978-144">TFS Error "[file]not be found in your workspace, or you do not have permission to access it"  during upgrade or uninstall when solution/project is bound to TFS source control - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="a7978-145">更新プログラムパッケージは、ターゲットでないパッケージの依存関係を取得しません- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="a7978-145">update package doesn't get dependencies for non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="a7978-146">Nuget パッケージマネージャーの UI 操作のログの詳細レベルを設定する方法はありません- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="a7978-146">There is no way to set logs verbosity level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="a7978-147">nuget の構成が無効です-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="a7978-147">nuget configuration is invalid - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="a7978-148">() の DefaultPushSource `NuGetDefaults.Config` `ProgramData\NuGet` が動作しません [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="a7978-148">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="a7978-149">nuget 3.4.3 のリリース-パッケージビルドで値を null にすることはできません- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="a7978-149">nuget 3.4.3 release -  getting Value cannot be null on package build - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="a7978-150">復元では、VSTS フィードの Nuget.Config から保存された資格情報が使用されていません- [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="a7978-150">restore is not using stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="a7978-151">[dotnet restore]--configfile は、cmd dir- [#2639](https://github.com/NuGet/Home/issues/2639)の代わりにプロジェクトディレクトリを基準としています</span><span class="sxs-lookup"><span data-stu-id="a7978-151">[dotnet restore] --configfile is relative to project dir instead of the cmd dir - [#2639](https://github.com/NuGet/Home/issues/2639)</span></span>

* <span data-ttu-id="a7978-152">バージョン comparsion の過剰な割り当て (コード[#2632](https://github.com/NuGet/Home/issues/2632) )</span><span class="sxs-lookup"><span data-stu-id="a7978-152">Excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="a7978-153">同じパッケージを並行してインストールしようとしている nuget.exe の複数のインスタンスによって、ダブル書き込みが [#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="a7978-153">Multiple instances of nuget.exe trying to install the same package in parallel causes a double write - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="a7978-154">複数プロジェクトの操作の依存関係情報はキャッシュされていません- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="a7978-154">Dependency information is not cached for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="a7978-155">パッケージフォルダーを最初にチェックせずに、ダウンロードパッケージをインストールおよび更新する [#2618](https://github.com/NuGet/Home/issues/2618)</span><span class="sxs-lookup"><span data-stu-id="a7978-155">Install and update download packages without checking the packages folder first - [#2618](https://github.com/NuGet/Home/issues/2618)</span></span>

* <span data-ttu-id="a7978-156">パッケージソースリストが空の場合、UI (NuGet 3.4. x) を介してパッケージソースを追加することはできません- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="a7978-156">If package source list is empty, cannot add package source via UI (NuGet 3.4.x) - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="a7978-157">デザイン時のファサードに依存するパッケージをインストールしようとすると[#2594](https://github.com/NuGet/Home/issues/2594) 、誤解を招くエラーが発生する</span><span class="sxs-lookup"><span data-stu-id="a7978-157">Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="a7978-158">"All" に設定して、パッケージを "All" に設定してパッケージをインストールすると、最初のソース[#2557](https://github.com/NuGet/Home/issues/2557)のみが試行される</span><span class="sxs-lookup"><span data-stu-id="a7978-158">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="a7978-159">ModernHttpClient を解凍していない最新[#2518](https://github.com/NuGet/Home/issues/2518)のベータ版</span><span class="sxs-lookup"><span data-stu-id="a7978-159">Latest beta not unzipping ModernHttpClient - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="a7978-160">自己ビルド型の NuGet [#2419](https://github.com/NuGet/Home/issues/2419) 3.4.1 を使用した起動時の VS2015 クラッシュ</span><span class="sxs-lookup"><span data-stu-id="a7978-160">VS2015 crash at startup with self-built NuGet 3.4.1 - [#2419](https://github.com/NuGet/Home/issues/2419)</span></span>

* <span data-ttu-id="a7978-161">Update コマンドを実行するように要求すると、さらに詳細な情報が表示される場合があります...- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="a7978-161">Update command might be a bit more verbose if i ask it to be so... - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="a7978-162">ローカルでビルドされた VSIX は、CI ビルドと同じ Dll およびファイルを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="a7978-162">VSIX built locally should have the same DLLs and files as the CI build.</span></span><span data-ttu-id="a7978-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span><span class="sxs-lookup"><span data-stu-id="a7978-163"> - [#2401](https://github.com/NuGet/Home/issues/2401)</span></span>

* <span data-ttu-id="a7978-164">ビルド[#2396](https://github.com/NuGet/Home/issues/2396)で NuGet ダウングレードの警告を修正する</span><span class="sxs-lookup"><span data-stu-id="a7978-164">Fix NuGet downgrade warnings in the build - [#2396](https://github.com/NuGet/Home/issues/2396)</span></span>

* <span data-ttu-id="a7978-165">パッケージソース (3 回) の認証に失敗すると、無期限にブロックされ [#2362](https://github.com/NuGet/Home/issues/2362)</span><span class="sxs-lookup"><span data-stu-id="a7978-165">Failing to authenticate package source (3 times) is blocked forever - [#2362](https://github.com/NuGet/Home/issues/2362)</span></span>

* <span data-ttu-id="a7978-166">パッケージに `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354)ファイルが含まれている場合、NoCache という引数を使用して nuget v 3.3 + フィードからパッケージをインストールすると、パッケージコンテンツが正しく復元されない</span><span class="sxs-lookup"><span data-stu-id="a7978-166">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="a7978-167">すべてのパッケージソースと共に Nuget をインストールしますが、1つのソースからのパッケージが見つからない場合は、 [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="a7978-167">Nuget Install with All Package Sources, but package missing from 1 source, fails - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="a7978-168">[PerfWatson]Uide のレイアウト: nuget.packagemanagement.visualstudio.dll!VisualStudio. VSMSBuildNuGetProjectSystem + \* lt; &gt;c__DisplayClass_0 + &lt; &lt; addreference &gt; b__ &gt; d. MoveNext- [#2285](https://github.com/NuGet/Home/issues/2285)</span><span class="sxs-lookup"><span data-stu-id="a7978-168">[PerfWatson] UIDelay: nuget.packagemanagement.visualstudio.dll!NuGet.PackageManagement.VisualStudio.VSMSBuildNuGetProjectSystem+\*lt;&gt;c__DisplayClass_0+&lt;&lt;AddReference&gt;b__&gt;d.MoveNext - [#2285](https://github.com/NuGet/Home/issues/2285)</span></span>

* <span data-ttu-id="a7978-169">1つのソースが承認に失敗した場合のインストールブロック- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="a7978-169">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="a7978-170">`.nuspec`バージョン範囲は IncludeReferencedProjects バージョン- [#1983](https://github.com/NuGet/Home/issues/1983)をオーバーライドする必要があります</span><span class="sxs-lookup"><span data-stu-id="a7978-170">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="a7978-171">Update-Package super 低速-"依存関係情報を収集しようとしています"- [#1909](https://github.com/NuGet/Home/issues/1909)</span><span class="sxs-lookup"><span data-stu-id="a7978-171">Update-Package super slow - "Attempting to gather dependencies information" - [#1909](https://github.com/NuGet/Home/issues/1909)</span></span>

* <span data-ttu-id="a7978-172">依存関係をバッチ更新するときの NuGet ステルスダウンパッケージパッケージ- [#1903](https://github.com/NuGet/Home/issues/1903)</span><span class="sxs-lookup"><span data-stu-id="a7978-172">NuGet stealth downgrades package when batch updating its dependencies - [#1903](https://github.com/NuGet/Home/issues/1903)</span></span>

* <span data-ttu-id="a7978-173">nuget.exe の更新では、アセンブリの厳密な名前とプライベート属性が削除されます。</span><span class="sxs-lookup"><span data-stu-id="a7978-173">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="a7978-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="a7978-174"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="a7978-175">"DefaultPushSource" の相対ファイルパス- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="a7978-175">Relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="a7978-176">競合回避モジュールのエラーメッセージの改善- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="a7978-176">Improve resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

* <span data-ttu-id="a7978-177">v3 の更新パッケージが、指定されたソース[#1013](https://github.com/NuGet/Home/issues/1013)にないパッケージで失敗する</span><span class="sxs-lookup"><span data-stu-id="a7978-177">update-package in v3 fails with packages not in the specified source - [#1013](https://github.com/NuGet/Home/issues/1013)</span></span>

* <span data-ttu-id="a7978-178">パッケージソースに相対パスを使用すると、- [#865](https://github.com/NuGet/Home/issues/865)を使用すると問題が発生する</span><span class="sxs-lookup"><span data-stu-id="a7978-178">Using relative paths for package sources is problematic to use - [#865](https://github.com/NuGet/Home/issues/865)</span></span>

* <span data-ttu-id="a7978-179">古いバージョンの要件を持つ間接的な依存関係が既に存在する場合、プロジェクトから生成された依存関係が見つからない- [#759](https://github.com/NuGet/Home/issues/759)</span><span class="sxs-lookup"><span data-stu-id="a7978-179">Missing dependency in NUPKG-file generated from project if indirect dependency already exists with a lower version requirement - [#759](https://github.com/NuGet/Home/issues/759)</span></span>

* <span data-ttu-id="a7978-180">プロジェクトを削除すると、対応する UI ウィンドウが閉じますが、プロジェクトの名前を変更しても UI ウィンドウの名前は変更されません。</span><span class="sxs-lookup"><span data-stu-id="a7978-180">Deleting a project closes corresponding UI window, but, renaming a project does not rename the UI window.</span></span> <span data-ttu-id="a7978-181">PMC がプロジェクトの名前変更とプロジェクト削除イベントをリッスンすることに注意してください- [#670](https://github.com/NuGet/Home/issues/670)</span><span class="sxs-lookup"><span data-stu-id="a7978-181">Note that PMC listens to project rename and project remove events - [#670](https://github.com/NuGet/Home/issues/670)</span></span>

* <span data-ttu-id="a7978-182">[Willow Web ワークロード]Razor v3 WSP ハングの作成- [#3241](https://github.com/NuGet/Home/issues/3241)</span><span class="sxs-lookup"><span data-stu-id="a7978-182">[Willow Web Workload] Creating Razor v3 WSP hangs - [#3241](https://github.com/NuGet/Home/issues/3241)</span></span>

* <span data-ttu-id="a7978-183">特定のパッケージのインストール/復元が失敗し、"パッケージに複数の nuspec ファイルが含まれています。" というエラーが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a7978-183">Install/restore of a particular package fails with "Package contains multiple nuspec files."</span></span><span data-ttu-id="a7978-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="a7978-184"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="a7978-185">小文字の Id & `packages.config` シナリオ- [#3209](https://github.com/NuGet/Home/issues/3209)</span><span class="sxs-lookup"><span data-stu-id="a7978-185">Lowercase IDs & `packages.config` scenarios - [#3209](https://github.com/NuGet/Home/issues/3209)</span></span>

* <span data-ttu-id="a7978-186">[3.5-beta2]パッケージの復元で "従来の" パッケージの復元に失敗する- [#3208](https://github.com/NuGet/Home/issues/3208)</span><span class="sxs-lookup"><span data-stu-id="a7978-186">[3.5-beta2] Package restore fails to restore "legacy" packages - [#3208](https://github.com/NuGet/Home/issues/3208)</span></span>

* <span data-ttu-id="a7978-187">nuget パックによって、 [#3203](https://github.com/NuGet/Home/issues/3203)に関係なく、コンテンツフォルダーに .tt ファイルが強制的に追加される</span><span class="sxs-lookup"><span data-stu-id="a7978-187">nuget pack forcefully adds .tt files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="a7978-188">ASP.NET web アプリの更新プログラムパッケージによって、ファイルに関連する警告が生成されます: ソース- [#3194](https://github.com/NuGet/Home/issues/3194)</span><span class="sxs-lookup"><span data-stu-id="a7978-188">update-package of ASP.NET web app generates warning related to file: source - [#3194](https://github.com/NuGet/Home/issues/3194)</span></span>

* <span data-ttu-id="a7978-189">`project.json`JSON ファイル内に packOptions と owner がない場合[#3180](https://github.com/NuGet/Home/issues/3180) 、nuget pack .csproj (を含む) がクラッシュする</span><span class="sxs-lookup"><span data-stu-id="a7978-189">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="a7978-190">の nuget パックでは `project.json` 、summary、authors、owners などの packOptions タグが無視されます。 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="a7978-190">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="a7978-191">NullReferenceException を使用して、System.resources.resourcemanager.getstream- [#3160](https://github.com/NuGet/Home/issues/3160)</span><span class="sxs-lookup"><span data-stu-id="a7978-191">NullReferenceException via NuGet.Packaging.PhysicalPackageFile.GetStream - [#3160](https://github.com/NuGet/Home/issues/3160)</span></span>

* <span data-ttu-id="a7978-192">NuGet パック `.nuspec` は `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)の出力の依存関係を無視します</span><span class="sxs-lookup"><span data-stu-id="a7978-192">NuGet pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="a7978-193">ロールバックを使用して複数のパッケージを更新すると、プロジェクトが破損した状態のままになります- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="a7978-193">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="a7978-194">Netstandard.library プロジェクトでは、ContentFiles は追加されません- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="a7978-194">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="a7978-195">.Net Standard をターゲットとするライブラリをパッケージ化できません- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="a7978-195">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="a7978-196">ファイル > 新しいプロジェクト-> クラスライブラリ (ポータブル) プロジェクトが VS2015 と[#3094](https://github.com/NuGet/Home/issues/3094) Dev15 で失敗する</span><span class="sxs-lookup"><span data-stu-id="a7978-196">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="a7978-197">nuGet エラー-1.0.0-\* は有効なバージョン文字列ではありません- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="a7978-197">nuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="a7978-198">Find-Package を表示できませんが、Install-Package 動作 [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="a7978-198">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="a7978-199">Dev15 で "パッケージのインストール-検証" を行うとエラー [#3061](https://github.com/NuGet/Home/issues/3061)が発生する</span><span class="sxs-lookup"><span data-stu-id="a7978-199">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="a7978-200">xproj の nuget パックは、既定で無効なターゲットパスを示しています- [#3060](https://github.com/NuGet/Home/issues/3060)</span><span class="sxs-lookup"><span data-stu-id="a7978-200">nuget pack of xproj is defaulting to invalid target path - [#3060](https://github.com/NuGet/Home/issues/3060)</span></span>

* <span data-ttu-id="a7978-201">NuGet バージョンを使用する VS で VS 2015 update 3 をインストールすると3.5.0 エラーが発生する- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="a7978-201">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="a7978-202">「 `project.json` (UWP、a. k. a build integrated) プロジェクト」の「packages.config によってブロックされました」- [#3046](https://github.com/NuGet/Home/issues/3046)</span><span class="sxs-lookup"><span data-stu-id="a7978-202">"Blocked by packages.config" in `project.json` (UWP, a.k.a build integrated) project - [#3046](https://github.com/NuGet/Home/issues/3046)</span></span>

* <span data-ttu-id="a7978-203">ビルドスクリプトによってインストールされた dotnet cli を preview2-003121) に更新します。これは、公式の preview2 ビルドです。</span><span class="sxs-lookup"><span data-stu-id="a7978-203">update dotnet cli installed by build script to preview2-003121, which is the official preview2 build.</span></span><span data-ttu-id="a7978-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span><span class="sxs-lookup"><span data-stu-id="a7978-204"> - [#3045](https://github.com/NuGet/Home/issues/3045)</span></span>

* <span data-ttu-id="a7978-205">パッケージマネージャー UI: パッケージを更新した後、新しいバージョンは表示されません- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="a7978-205">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="a7978-206">-Delete コマンドラインの ApiKey は3.5.0 で読み取り/送信されません- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="a7978-206">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="a7978-207">文字列が正しくありません: パッケージの安定したリリースでは、プレリリースの依存関係を設定することはできません。</span><span class="sxs-lookup"><span data-stu-id="a7978-207">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="a7978-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="a7978-208"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="a7978-209">OptimizedZipPackage cache が空のフォルダーを残す- [#3029](https://github.com/NuGet/Home/issues/3029)</span><span class="sxs-lookup"><span data-stu-id="a7978-209">OptimizedZipPackage cache leaves empty folders - [#3029](https://github.com/NuGet/Home/issues/3029)</span></span>

* <span data-ttu-id="a7978-210">PCL (net46 および windows 10) プロジェクトを作成すると、NullRef 例外が生成されます。</span><span class="sxs-lookup"><span data-stu-id="a7978-210">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="a7978-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="a7978-211"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="a7978-212">新しいバージョンが allowedVersions 制約によって制限されている場合、Nuget 更新プログラムは情報メッセージを提供する必要があり [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="a7978-212">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="a7978-213">Nuget v3 の復元に関する問題- [#2891](https://github.com/NuGet/Home/issues/2891)</span><span class="sxs-lookup"><span data-stu-id="a7978-213">Nuget v3 restore issues - [#2891](https://github.com/NuGet/Home/issues/2891)</span></span>

* <span data-ttu-id="a7978-214">複数の[#2885](https://github.com/NuGet/Home/issues/2885)ソースで資格情報プロバイダーを使用しているときに、資格情報プラグインがエラーで終了しました-1/エラーが発生したパッケージのダウンロード中</span><span class="sxs-lookup"><span data-stu-id="a7978-214">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="a7978-215">`project.json`何も変更されなかった場合に、nuget の復元によって再コンパイル[#2817](https://github.com/NuGet/Home/issues/2817)が行われる</span><span class="sxs-lookup"><span data-stu-id="a7978-215">`project.json` nuget restore causes recompilation when nothing changed - [#2817](https://github.com/NuGet/Home/issues/2817)</span></span>

* <span data-ttu-id="a7978-216">シンボルパッケージは、インストールまたは更新[#2807](https://github.com/NuGet/Home/issues/2807)では使用しないでください</span><span class="sxs-lookup"><span data-stu-id="a7978-216">Symbols packages should not ever be used in install or update - [#2807](https://github.com/NuGet/Home/issues/2807)</span></span>

* <span data-ttu-id="a7978-217">VS は repositoryPath の環境変数をサポートしていません (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="a7978-217">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="a7978-218">パッケージマネージャー UI でラベル付けされていない UIElements にアクセシビリティ対応のラベルを付けます- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="a7978-218">Label the unlabeled UIElements in Package Manager UI for accessibility - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="a7978-219">ハイフネーションされたプロファイルを含むポータブルフレームワークは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="a7978-219">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="a7978-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="a7978-220"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="a7978-221">NuGet パッケージマネージャーは、[パッケージの詳細] のオプション一覧が適用されないことを明確にする必要があり `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="a7978-221">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="a7978-222">プッシュ/削除 nuget.exe は API キーを使用しません- [#2627](https://github.com/NuGet/Home/issues/2627)</span><span class="sxs-lookup"><span data-stu-id="a7978-222">nuget.exe push/delete won't use API Key  - [#2627](https://github.com/NuGet/Home/issues/2627)</span></span>

* <span data-ttu-id="a7978-223">ロックファイルからロックされたプロパティを削除し [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="a7978-223">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="a7978-224">NuGet 3.3.0 の更新が ' 追加の制約で失敗しました...packages.config で定義されているため、この操作を実行できません。 '</span><span class="sxs-lookup"><span data-stu-id="a7978-224">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="a7978-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="a7978-225"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="a7978-226">存在しないローカルソースからパッケージをインストールすると、偽のメッセージ[#1674](https://github.com/NuGet/Home/issues/1674)がスローされる</span><span class="sxs-lookup"><span data-stu-id="a7978-226">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="a7978-227">[使用可能なアップグレード] フィルターにより、バージョンの制約に違反するアップグレードが表示されます- [#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="a7978-227">"Upgrade available" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

* <span data-ttu-id="a7978-228">ネイティブパッケージを更新できません- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="a7978-228">Unable to update native packages - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>


## <a name="features"></a><span data-ttu-id="a7978-229">特徴</span><span class="sxs-lookup"><span data-stu-id="a7978-229">Features</span></span>

* <span data-ttu-id="a7978-230">NuGet によって追加された参照に対して CopyLocal を false に設定することをサポートする [#329](https://github.com/NuGet/Home/issues/329)</span><span class="sxs-lookup"><span data-stu-id="a7978-230">Support setting CopyLocal to false on references added by NuGet - [#329](https://github.com/NuGet/Home/issues/329)</span></span>

* <span data-ttu-id="a7978-231">MSBuild 15 [#1937](https://github.com/NuGet/Home/issues/1937)の nuget.exe サポート</span><span class="sxs-lookup"><span data-stu-id="a7978-231">nuget.exe support for MSBuild 15 - [#1937](https://github.com/NuGet/Home/issues/1937)</span></span>

* <span data-ttu-id="a7978-232">のパックサポート。`csproj`</span><span class="sxs-lookup"><span data-stu-id="a7978-232">Pack support for .`csproj`</span></span><span data-ttu-id="a7978-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span><span class="sxs-lookup"><span data-stu-id="a7978-233"> + `project.json` - [#1689](https://github.com/NuGet/Home/issues/1689)</span></span>

* <span data-ttu-id="a7978-234">ユーザー操作が実行されているときにユーザー操作を無効にする- [#1440](https://github.com/NuGet/Home/issues/1440)</span><span class="sxs-lookup"><span data-stu-id="a7978-234">Disable user action when there are user actions being executed - [#1440](https://github.com/NuGet/Home/issues/1440)</span></span>

* <span data-ttu-id="a7978-235">NuGet は #2782 のサポートを追加する必要があります `runtimes/{rid}/nativeassets/{txm}/`  -  [](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="a7978-235">NuGet should add support for `runtimes/{rid}/nativeassets/{txm}/` - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>

* <span data-ttu-id="a7978-236">NuGet 2.x (既に 3. x に存在する) で[#2720](https://github.com/NuGet/Home/issues/2720) 、互換性のフレームワークを追加します。</span><span class="sxs-lookup"><span data-stu-id="a7978-236">Add framework compatibilities missing in NuGet 2.x (which are already in 3.x) - [#2720](https://github.com/NuGet/Home/issues/2720)</span></span>

* <span data-ttu-id="a7978-237">フォールバックパッケージフォルダーのサポート- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="a7978-237">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="a7978-238">ツールパッケージをサポートするためのパッケージの種類の概念を設計および実装する- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="a7978-238">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="a7978-239">API を追加して、グローバルパッケージフォルダーへのパスを取得します- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="a7978-239">Add an API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="a7978-240">パック[#3356](https://github.com/NuGet/Home/issues/3356)で semver 2.0.0 を有効にする</span><span class="sxs-lookup"><span data-stu-id="a7978-240">Enable SemVer 2.0.0 in pack - [#3356](https://github.com/NuGet/Home/issues/3356)</span></span>

## <a name="dcrs"></a><span data-ttu-id="a7978-241">DCR</span><span class="sxs-lookup"><span data-stu-id="a7978-241">DCRs</span></span>

* <span data-ttu-id="a7978-242">nuget.exe のプッシュタイムアウトパラメーターが機能しません- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="a7978-242">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="a7978-243">パッケージの説明テキストは選択可能である必要があります- [#1769](https://github.com/NuGet/Home/issues/1769)</span><span class="sxs-lookup"><span data-stu-id="a7978-243">Package Description text should be selectable - [#1769](https://github.com/NuGet/Home/issues/1769)</span></span>

* <span data-ttu-id="a7978-244">`.props` `.targets` プロジェクトのファイルとファイルを生成するための nuget.exe を有効に `.nuproj` [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="a7978-244">Enable nuget.exe to produce `.props` and `.targets` files for `.nuproj` projects [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="a7978-245">拡張 API を追加して、フレームワークとインポート[#2633](https://github.com/NuGet/Home/issues/2633)を比較する</span><span class="sxs-lookup"><span data-stu-id="a7978-245">Add extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="a7978-246">#2486 の使用時に依存関係オプションを非表示にする `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="a7978-246">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="a7978-247">詳細な出力[#1887](https://github.com/NuGet/Home/issues/1887)に nuget.exe バージョンヘッダーを出力する</span><span class="sxs-lookup"><span data-stu-id="a7978-247">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="a7978-248">NuGet では、dotnet tfm ベースの PCL でのアップグレードまたはインストールによって問題が発生する可能性があることをユーザーに知らせる必要があり [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="a7978-248">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="a7978-249">[プロジェクトに対して無効なインストール/アップグレードを警告する]: "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="a7978-249">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="a7978-250">ReShaper と NuGet の更新プログラム[#3044](https://github.com/NuGet/Home/issues/3044)のパフォーマンスの問題を修正します。</span><span class="sxs-lookup"><span data-stu-id="a7978-250">Fix performance issues with ReShaper and NuGet for Update - [#3044](https://github.com/NuGet/Home/issues/3044)</span></span>

* <span data-ttu-id="a7978-251">Netcoreapp11 と netstandard17 のサポートを追加する- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="a7978-251">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="a7978-252">トークンの置換に AssemblyMetadata 属性を利用する `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="a7978-252">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>
