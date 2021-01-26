---
title: NuGet 5.5 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.5 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2020
ms.topic: conceptual
ms.openlocfilehash: 0fde67dd03c31e986ed89f2f8627608e279ef908
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780114"
---
# <a name="nuget-55-release-notes"></a><span data-ttu-id="18cfc-103">NuGet 5.5 リリースノート</span><span class="sxs-lookup"><span data-stu-id="18cfc-103">NuGet 5.5 Release Notes</span></span>

<span data-ttu-id="18cfc-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="18cfc-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="18cfc-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="18cfc-105">NuGet version</span></span> | <span data-ttu-id="18cfc-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="18cfc-106">Available in Visual Studio version</span></span>| <span data-ttu-id="18cfc-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="18cfc-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="18cfc-108">**5.5.0**</span><span class="sxs-lookup"><span data-stu-id="18cfc-108">**5.5.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="18cfc-109">Visual Studio 2019 バージョン 16.5</span><span class="sxs-lookup"><span data-stu-id="18cfc-109">Visual Studio 2019 version 16.5</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="18cfc-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="18cfc-110">[3.1.200](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="18cfc-111"><sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="18cfc-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-55"></a><span data-ttu-id="18cfc-112">概要: 5.5 の新機能</span><span class="sxs-lookup"><span data-stu-id="18cfc-112">Summary: What's New in 5.5</span></span>

* <span data-ttu-id="18cfc-113">Visual Studio の NuGet パッケージマネージャー UI のアクセシビリティとスクリーンリーダーエクスペリエンスが向上しました。</span><span class="sxs-lookup"><span data-stu-id="18cfc-113">Improved accessibility and screen reader experience for the NuGet package manager UI in Visual Studio</span></span>
    * <span data-ttu-id="18cfc-114">スクリーンリーダーエクスペリエンスでのアクセシビリティの問題、ショートカットテキストがない、インストールされたテキストボックスのアクセス可能な名前などが含まれている、- [#9059](https://github.com/NuGet/Home/issues/9059)</span><span class="sxs-lookup"><span data-stu-id="18cfc-114">Accessibility issues in Screen Reader experiences, missing altText and accessible name for Installed textbox, etc., - [#9059](https://github.com/NuGet/Home/issues/9059)</span></span>
    * <span data-ttu-id="18cfc-115">パッケージ一覧のスクリーンリーダーエクスペリエンスに関するアクセシビリティの問題- [#9077](https://github.com/NuGet/Home/issues/9077)</span><span class="sxs-lookup"><span data-stu-id="18cfc-115">Accessibility issues in Screen Reader experiences in Packages List - [#9077](https://github.com/NuGet/Home/issues/9077)</span></span>
    * <span data-ttu-id="18cfc-116">"参照"、"インストール"、"更新" タブに関連するスクリーンリーダーエクスペリエンスのアクセシビリティに関する問題- [#9078](https://github.com/NuGet/Home/issues/9078)</span><span class="sxs-lookup"><span data-stu-id="18cfc-116">Accessibility issues in Screen Reader experiences related to "browse","install","update" Tabs - [#9078](https://github.com/NuGet/Home/issues/9078)</span></span>
    * <span data-ttu-id="18cfc-117">ナレーターは、"Blank"、"No Dependencies" "、" nuget.exe "、" MIT "のリンクラベルを発表しません [#9157](https://github.com/NuGet/Home/issues/9157)</span><span class="sxs-lookup"><span data-stu-id="18cfc-117">Narrator does not announce "Blank","No Dependencies","nuget.org","MIT" link label [#9157](https://github.com/NuGet/Home/issues/9157)</span></span>

* <span data-ttu-id="18cfc-118">ローカルフィードでホストされているパッケージのための、Visual Studio パッケージマネージャー UI での自己完結型アイコンの表示のサポート- [#8189](https://github.com/NuGet/Home/issues/8189)</span><span class="sxs-lookup"><span data-stu-id="18cfc-118">Support for surfacing self-contained icons in Visual Studio package manager UI for packages hosted on local feeds - [#8189](https://github.com/NuGet/Home/issues/8189)</span></span>

* <span data-ttu-id="18cfc-119">`RestoreUseStaticGraphEvaluation`MSBuild スタティック Graph api を呼び出して評価を高速化する、を使用した非 op 復元パフォーマンスの大幅な向上- [8791](https://github.com/NuGet/Home/issues/8791)</span><span class="sxs-lookup"><span data-stu-id="18cfc-119">Significantly improved no-op restore performance using `RestoreUseStaticGraphEvaluation` which speeds up evaluations by calling MSBuild Static Graph APIs - [8791](https://github.com/NuGet/Home/issues/8791)</span></span>

* <span data-ttu-id="18cfc-120">クロスプラットフォーム認証プラグインでの dotnet.exe の信頼性の向上</span><span class="sxs-lookup"><span data-stu-id="18cfc-120">Improved dotnet.exe reliability with cross-platform authentication plugins</span></span>
    * <span data-ttu-id="18cfc-121">[#7842](https://github.com/NuGet/Home/issues/7842) TaskCanceledException で失敗 dotnet restore</span><span class="sxs-lookup"><span data-stu-id="18cfc-121">dotnet restore failing with TaskCanceledException - [#7842](https://github.com/NuGet/Home/issues/7842)</span></span>
    * <span data-ttu-id="18cfc-122">プラグイン: "タスクが取り消されました"-これにより、ADO 認証に問題があります。</span><span class="sxs-lookup"><span data-stu-id="18cfc-122">Plugin:  "A task was cancelled" - problem with ADO authentication due to this.</span></span><span data-ttu-id="18cfc-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span><span class="sxs-lookup"><span data-stu-id="18cfc-123"> - [#8528](https://github.com/NuGet/Home/issues/8528)</span></span>

* <span data-ttu-id="18cfc-124">`dotnet nuget <add|remove|update|disable|enable|list> source`コマンド[#4126](https://github.com/NuGet/Home/issues/4126)の追加</span><span class="sxs-lookup"><span data-stu-id="18cfc-124">add `dotnet nuget <add|remove|update|disable|enable|list> source` command - [#4126](https://github.com/NuGet/Home/issues/4126)</span></span>

* <span data-ttu-id="18cfc-125">`--skip-duplicate`Dotnet nuget プッシュ[#8778](https://github.com/NuGet/Home/issues/8778)の使用に関するサポート</span><span class="sxs-lookup"><span data-stu-id="18cfc-125">Suport for `--skip-duplicate`  using dotnet nuget push - [#8778](https://github.com/NuGet/Home/issues/8778)</span></span>

* <span data-ttu-id="18cfc-126">`packages.config`Msbuild/restore を使用したサポート- [#8506](https://github.com/NuGet/Home/issues/8506)</span><span class="sxs-lookup"><span data-stu-id="18cfc-126">Support `packages.config` with msbuild /restore - [#8506](https://github.com/NuGet/Home/issues/8506)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="18cfc-127">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="18cfc-127">Issues fixed in this release</span></span>

<span data-ttu-id="18cfc-128">**バグ**</span><span class="sxs-lookup"><span data-stu-id="18cfc-128">**Bugs**</span></span>

* <span data-ttu-id="18cfc-129">V3 Api を使用した Self-Updater の再作業- [#4197](https://github.com/NuGet/Home/issues/4197)</span><span class="sxs-lookup"><span data-stu-id="18cfc-129">Rework Self-Updater with V3 Apis - [#4197](https://github.com/NuGet/Home/issues/4197)</span></span>

* <span data-ttu-id="18cfc-130">パッケージの依存関係のバージョンが ' \* ' に設定されている場合、パッケージの依存関係のバージョンが正しくありません- [#6697](https://github.com/NuGet/Home/issues/6697)</span><span class="sxs-lookup"><span data-stu-id="18cfc-130">Wrong package dependency version If package dependency version is set to '\*' - [#6697](https://github.com/NuGet/Home/issues/6697)</span></span>

* <span data-ttu-id="18cfc-131">ErrorUnsafePackageEntry エラーメッセージが問題の原因を指していません- [#7505](https://github.com/NuGet/Home/issues/7505)</span><span class="sxs-lookup"><span data-stu-id="18cfc-131">ErrorUnsafePackageEntry error message is not pointing to source of problem - [#7505](https://github.com/NuGet/Home/issues/7505)</span></span>

* <span data-ttu-id="18cfc-132">"\*" シナリオでは、ロックファイルは受け入れられません- [#8073](https://github.com/NuGet/Home/issues/8073)</span><span class="sxs-lookup"><span data-stu-id="18cfc-132">Lock file is not honored in "\*" scenarios  - [#8073](https://github.com/NuGet/Home/issues/8073)</span></span>

* <span data-ttu-id="18cfc-133">PackageReference (MSBuild/Dotnet/VS restore do) を使用している場合、NuGet.exe はパッケージの最新バージョンに解決されません。- [#8432](https://github.com/NuGet/Home/issues/8432)</span><span class="sxs-lookup"><span data-stu-id="18cfc-133">NuGet.exe does not resolve to the latest version of a package when using \* in PackageReference (MSBuild/Dotnet/VS restore do) - [#8432](https://github.com/NuGet/Home/issues/8432)</span></span>

* <span data-ttu-id="18cfc-134">dotnet list パッケージとマルチターゲット化 WPF プロジェクト- [#8463](https://github.com/NuGet/Home/issues/8463)</span><span class="sxs-lookup"><span data-stu-id="18cfc-134">dotnet list package with multi targeting WPF project - [#8463](https://github.com/NuGet/Home/issues/8463)</span></span>

* <span data-ttu-id="18cfc-135">ConcurrencyUtilities の向上 (CPU 使用率の削減)- [#8653](https://github.com/NuGet/Home/issues/8653)</span><span class="sxs-lookup"><span data-stu-id="18cfc-135">Improve ConcurrencyUtilities (reduce CPU usage) - [#8653](https://github.com/NuGet/Home/issues/8653)</span></span>

* <span data-ttu-id="18cfc-136">アンロードされたプロジェクトシナリオの DG 仕様は、プレビュー復元では記述できません- [#8793](https://github.com/NuGet/Home/issues/8793)</span><span class="sxs-lookup"><span data-stu-id="18cfc-136">DG Spec for unloaded project scenarios should not be written in preview restores - [#8793](https://github.com/NuGet/Home/issues/8793)</span></span>

* <span data-ttu-id="18cfc-137">Visual Studio NuGet パッケージ (RestoreManagerPackage) は、ソリューションビルドイベントに対して自動読み込みを行う必要があります- [#8796](https://github.com/NuGet/Home/issues/8796)</span><span class="sxs-lookup"><span data-stu-id="18cfc-137">The Visual Studio NuGet packages (RestoreManagerPackage) needs to auto load on solution build events - [#8796](https://github.com/NuGet/Home/issues/8796)</span></span>

* <span data-ttu-id="18cfc-138">.Vssettings 初期化- [#8842](https://github.com/NuGet/Home/issues/8842)のデッドロック</span><span class="sxs-lookup"><span data-stu-id="18cfc-138">Deadlock in VSSettings init - [#8842](https://github.com/NuGet/Home/issues/8842)</span></span>

* <span data-ttu-id="18cfc-139">プロジェクトがソリューションフォルダーに配置されている場合、VisualStudio ツールボックスは NuGet パッケージから設定されません- [#8868](https://github.com/NuGet/Home/issues/8868)</span><span class="sxs-lookup"><span data-stu-id="18cfc-139">VisualStudio ToolBox is not populated from a NuGet package if a project is placed in a solution folder - [#8868](https://github.com/NuGet/Home/issues/8868)</span></span>

* <span data-ttu-id="18cfc-140">VS: ソリューションの復元永続的が競合状態によって失敗する- [#8881](https://github.com/NuGet/Home/issues/8881)</span><span class="sxs-lookup"><span data-stu-id="18cfc-140">VS:  solution restore perpetually fails due to race condition - [#8881](https://github.com/NuGet/Home/issues/8881)</span></span>

* <span data-ttu-id="18cfc-141">[インストール済み] タブおよび [検索] の定数 "読み込み中"</span><span class="sxs-lookup"><span data-stu-id="18cfc-141">Constant "loading.." on installed tab, and "searching</span></span> <term><span data-ttu-id="18cfc-142">[更新] タブの [ [#8890](https://github.com/NuGet/Home/issues/8890)</span><span class="sxs-lookup"><span data-stu-id="18cfc-142">.." on updates tab - [#8890](https://github.com/NuGet/Home/issues/8890)</span></span>

* <span data-ttu-id="18cfc-143">キャッシュの有効期限が切れた後、VS PM UI に埋め込みアイコンがない- [#9069](https://github.com/NuGet/Home/issues/9069)</span><span class="sxs-lookup"><span data-stu-id="18cfc-143">Missing Embedded Icons in VS PM UI after cache expires - [#9069](https://github.com/NuGet/Home/issues/9069)</span></span>

* <span data-ttu-id="18cfc-144">アドイン UI の起動 [#9112](https://github.com/NuGet/Home/issues/9112)</span><span class="sxs-lookup"><span data-stu-id="18cfc-144">FireAndForget PM UI startup - [#9112](https://github.com/NuGet/Home/issues/9112)</span></span>

* <span data-ttu-id="18cfc-145">Restore: IncludeExcludeFiles. Equals (...) の実装が正しくありません- [#9167](https://github.com/NuGet/Home/issues/9167)</span><span class="sxs-lookup"><span data-stu-id="18cfc-145">Restore: IncludeExcludeFiles.Equals(...) implementation is incorrect - [#9167](https://github.com/NuGet/Home/issues/9167)</span></span>

* <span data-ttu-id="18cfc-146">復元: PackageSpec () は、等しくない複製を作成し [#9211](https://github.com/NuGet/Home/issues/9211)</span><span class="sxs-lookup"><span data-stu-id="18cfc-146">Restore: PackageSpec.Clone() creates unequal clone - [#9211](https://github.com/NuGet/Home/issues/9211)</span></span>

* <span data-ttu-id="18cfc-147">[ビルドがエラーで終了した場合は常にエラー一覧を表示する] がオンになっていない場合に表示されるエラー一覧 [#8190](https://github.com/NuGet/Home/issues/8190)</span><span class="sxs-lookup"><span data-stu-id="18cfc-147">Error list shown although "Always show Error List if build finishes with errors" is not checked - [#8190](https://github.com/NuGet/Home/issues/8190)</span></span>

* <span data-ttu-id="18cfc-148">静的なグラフの復元では、空の SolutionPath を渡すことはできません- [#9061](https://github.com/NuGet/Home/issues/9061)</span><span class="sxs-lookup"><span data-stu-id="18cfc-148">Static Graph restore should not pass empty SolutionPath - [#9061](https://github.com/NuGet/Home/issues/9061)</span></span>

* <span data-ttu-id="18cfc-149">復元: 各プロジェクトのクロージャが4回[#9042](https://github.com/NuGet/Home/issues/9042)に計算されます。</span><span class="sxs-lookup"><span data-stu-id="18cfc-149">Restore: closure computed for each project 4 times - [#9042](https://github.com/NuGet/Home/issues/9042)</span></span>

* <span data-ttu-id="18cfc-150">復元: DependencyGraphSpec. Load (...) は JObject- [#9040](https://github.com/NuGet/Home/issues/9040)を必要としません</span><span class="sxs-lookup"><span data-stu-id="18cfc-150">Restore: DependencyGraphSpec.Load(...) does not need JObject - [#9040](https://github.com/NuGet/Home/issues/9040)</span></span>

* <span data-ttu-id="18cfc-151">復元: 大きなオブジェクトヒープ (LOH) で作成された大きな文字列- [#9031](https://github.com/NuGet/Home/issues/9031)</span><span class="sxs-lookup"><span data-stu-id="18cfc-151">Restore: large strings created on large object heap (LOH) - [#9031](https://github.com/NuGet/Home/issues/9031)</span></span>

* <span data-ttu-id="18cfc-152">新しい mono のカスタム nuget.exe が MSBuild SDK リゾルバー- [8848](https://github.com/NuGet/Home/issues/8848)のために壊れている可能性があります</span><span class="sxs-lookup"><span data-stu-id="18cfc-152">Custom nuget.exe on newer mono might break due to the MSBuild SDK Resolver - [8848](https://github.com/NuGet/Home/issues/8848)</span></span>

* <span data-ttu-id="18cfc-153">で nuget.dgspec.jsが "別のプロセスで使用されています"- [8692](https://github.com/NuGet/Home/issues/8692)の場合に復元が失敗する</span><span class="sxs-lookup"><span data-stu-id="18cfc-153">restore fails when nuget.dgspec.json is "used by another process" - [8692](https://github.com/NuGet/Home/issues/8692)</span></span>

<span data-ttu-id="18cfc-154">**DCR**</span><span class="sxs-lookup"><span data-stu-id="18cfc-154">**DCRs**</span></span>

* <span data-ttu-id="18cfc-155">_GetRestoreProjectStyle のロジックはタスクの[#8804](https://github.com/NuGet/Home/issues/8804)である必要があります。</span><span class="sxs-lookup"><span data-stu-id="18cfc-155">Logic in _GetRestoreProjectStyle should be in a task - [#8804](https://github.com/NuGet/Home/issues/8804)</span></span>

* <span data-ttu-id="18cfc-156">[インストールされているタブに既定で非推奨情報を追加する]- [#8541](https://github.com/NuGet/Home/issues/8541)</span><span class="sxs-lookup"><span data-stu-id="18cfc-156">Add deprecation information by default on the installed tab - [#8541](https://github.com/NuGet/Home/issues/8541)</span></span>

<span data-ttu-id="18cfc-157">**[このリリースで修正されるすべての問題の一覧-5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span><span class="sxs-lookup"><span data-stu-id="18cfc-157">**[List of all issues fixed in this release - 5.5](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5e0e5fbd021f7aa0ec95db18)**</span></span>
