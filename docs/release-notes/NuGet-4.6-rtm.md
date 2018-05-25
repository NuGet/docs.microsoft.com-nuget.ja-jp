---
title: NuGet 4.6 RTM リリース ノート
description: NuGet 4.6.0 のリリース ノートであり、既知の問題、バグ修正、追加機能、および DCR が含まれています。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 3/7/2018
ms.topic: conceptual
ms.openlocfilehash: 11e604ad9a28ac2b22880a13ef9d8b41d8c09507
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2018
---
# <a name="nuget-46-rtm-release-notes"></a><span data-ttu-id="380a4-103">NuGet 4.6 RTM リリース ノート</span><span class="sxs-lookup"><span data-stu-id="380a4-103">NuGet 4.6 RTM Release Notes</span></span>

<span data-ttu-id="380a4-104">[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、[NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe) が付属しています。</span><span class="sxs-lookup"><span data-stu-id="380a4-104">[Visual Studio 2017 15.6 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.6.0](https://dist.nuget.org/win-x86-commandline/v4.6.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-this-release"></a><span data-ttu-id="380a4-105">概要: このリリースの新機能</span><span class="sxs-lookup"><span data-stu-id="380a4-105">Summary: What's New in this Release</span></span>

* <span data-ttu-id="380a4-106">[パッケージの署名](../create-packages/sign-a-package.md)のサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="380a4-106">We have added support for [signing packages](../create-packages/sign-a-package.md).</span></span>
* <span data-ttu-id="380a4-107">Visual Studio 2017 と nuget.exe では、[署名済みパッケージ](../reference/signed-packages-reference.md)について、パッケージをインストール、復元する前にパッケージの整合性を検証できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="380a4-107">Visual Studio 2017 and nuget.exe now verifies package integrity before installing, restoring packages for [signed packages](../reference/signed-packages-reference.md).</span></span>
* <span data-ttu-id="380a4-108">連続する復元のパフォーマンスが向上しました。</span><span class="sxs-lookup"><span data-stu-id="380a4-108">We have improved performance of successive restores.</span></span>

## <a name="known-issues"></a><span data-ttu-id="380a4-109">既知の問題</span><span class="sxs-lookup"><span data-stu-id="380a4-109">Known issues</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="380a4-110">.NET Framework と NuGet での .NET Standard 2.0 の問題</span><span class="sxs-lookup"><span data-stu-id="380a4-110">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span> 

<span data-ttu-id="380a4-111">.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="380a4-111">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="380a4-112">[このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="380a4-112">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="380a4-113">このリリースで修正された主な問題</span><span class="sxs-lookup"><span data-stu-id="380a4-113">Top issues fixed in this release</span></span>

<span data-ttu-id="380a4-114">**パフォーマンスの改善**</span><span class="sxs-lookup"><span data-stu-id="380a4-114">**Performance fixes**</span></span>

* <span data-ttu-id="380a4-115">変更がない場合に資産ファイルを書き込まない - [#6491](https://github.com/NuGet/Home/issues/6491)</span><span class="sxs-lookup"><span data-stu-id="380a4-115">Don't write asset files when there is no change - [#6491](https://github.com/NuGet/Home/issues/6491)</span></span>
* <span data-ttu-id="380a4-116">子プロジェクトの TFM が親プロジェクトの TFM と一致しない場合、復元によって追加の MSBuild 評価が発生する - [#6311](https://github.com/NuGet/Home/issues/6311)</span><span class="sxs-lookup"><span data-stu-id="380a4-116">Restore causes extra MSBuild evaluations when child projects' TFM do not match with the parent project's - [#6311](https://github.com/NuGet/Home/issues/6311)</span></span>
* <span data-ttu-id="380a4-117">依存関係グラフ仕様の作成を最適化することで NoOp 復元のパフォーマンスを向上する - [#6252](https://github.com/NuGet/Home/issues/6252)</span><span class="sxs-lookup"><span data-stu-id="380a4-117">Improve NoOp restore perf by optimizing dependency graph spec creation - [#6252](https://github.com/NuGet/Home/issues/6252)</span></span>

<span data-ttu-id="380a4-118">**バグ**</span><span class="sxs-lookup"><span data-stu-id="380a4-118">**Bugs**</span></span>

* <span data-ttu-id="380a4-119">ローカル フォルダーにプッシュすると、nupkg がロックされたままになる - [#6325](https://github.com/NuGet/Home/issues/6325)</span><span class="sxs-lookup"><span data-stu-id="380a4-119">Push to local folder leaves nupkg locked - [#6325](https://github.com/NuGet/Home/issues/6325)</span></span>
* <span data-ttu-id="380a4-120">NuGet プラグインの実装: 複数の問題 - [#6149](https://github.com/NuGet/Home/issues/6149)</span><span class="sxs-lookup"><span data-stu-id="380a4-120">NuGet Plugin implementation:  multiple issues - [#6149](https://github.com/NuGet/Home/issues/6149)</span></span>
* <span data-ttu-id="380a4-121">UIHang - VSSolutionManager の MEF の初期化からクエリ サービス呼び出しを削除する - [#6110](https://github.com/NuGet/Home/issues/6110)</span><span class="sxs-lookup"><span data-stu-id="380a4-121">UIHang - Remove query service call from MEF initialization in VSSolutionManager - [#6110](https://github.com/NuGet/Home/issues/6110)</span></span>
* <span data-ttu-id="380a4-122">取り消されたパッケージ ダウンロード タスクのエラー報告の例外 - [#6096](https://github.com/NuGet/Home/issues/6096)</span><span class="sxs-lookup"><span data-stu-id="380a4-122">Error reporting exception for cancelled package download task - [#6096](https://github.com/NuGet/Home/issues/6096)</span></span>
* <span data-ttu-id="380a4-123">NuGet.exe がアセンブリ名の '+' を '%2B' に置換する - [#5956](https://github.com/NuGet/Home/issues/5956)</span><span class="sxs-lookup"><span data-stu-id="380a4-123">NuGet.exe replaces '+' with '%2B' in assembly name - [#5956](https://github.com/NuGet/Home/issues/5956)</span></span>
* <span data-ttu-id="380a4-124">F1 キーを押しても PM UI とコンソールの正しいヘルプ ページが表示されない - [#5912](https://github.com/NuGet/Home/issues/5912)</span><span class="sxs-lookup"><span data-stu-id="380a4-124">Fn+F1 does not take to the right help page for PM UI and Console - [#5912](https://github.com/NuGet/Home/issues/5912)</span></span>
* <span data-ttu-id="380a4-125">特定の状況下で VS NuGet が絶対パスをプロジェクト ファイルに書き込む - [#5888](https://github.com/NuGet/Home/issues/5888)</span><span class="sxs-lookup"><span data-stu-id="380a4-125">VS NuGet writes absolute paths into project files under specific circumstances - [#5888](https://github.com/NuGet/Home/issues/5888)</span></span>
* <span data-ttu-id="380a4-126">4.3 の回帰を修正 - 変換で contentfile 内のプレースホルダー $product$ と $AssemblyGuid$ が置換されない - [#5880](https://github.com/NuGet/Home/issues/5880)</span><span class="sxs-lookup"><span data-stu-id="380a4-126">Fix 4.3 regression - Placeholders $product$ and $AssemblyGuid$ not replaced in contentfile through transformation - [#5880](https://github.com/NuGet/Home/issues/5880)</span></span>
* <span data-ttu-id="380a4-127">ソースが複数ある dotnet restore がクラッシュする - [#5817](https://github.com/NuGet/Home/issues/5817)</span><span class="sxs-lookup"><span data-stu-id="380a4-127">dotnet restore with multiple sources crashes - [#5817](https://github.com/NuGet/Home/issues/5817)</span></span>
* <span data-ttu-id="380a4-128">git のバージョン管理を使用するにはパックでプロジェクトのバージョンを再評価する必要がある - [#4790](https://github.com/NuGet/Home/issues/4790)</span><span class="sxs-lookup"><span data-stu-id="380a4-128">Pack should re-evaluate project versions to allow git versioning - [#4790](https://github.com/NuGet/Home/issues/4790)</span></span>
* <span data-ttu-id="380a4-129">互換性のないパッケージをインストールした場合のわかりづらいエラーを改善 - [#4555](https://github.com/NuGet/Home/issues/4555)</span><span class="sxs-lookup"><span data-stu-id="380a4-129">Improve hard to understand errors when you install an incompatible package - [#4555](https://github.com/NuGet/Home/issues/4555)</span></span>
* <span data-ttu-id="380a4-130">TemplateWizard のオプションで、パッケージを PackageReferences としてインストールする必要がある - [#4549](https://github.com/NuGet/Home/issues/4549)</span><span class="sxs-lookup"><span data-stu-id="380a4-130">TemplateWizard needs option to install packages as PackageReferences - [#4549](https://github.com/NuGet/Home/issues/4549)</span></span>
* <span data-ttu-id="380a4-131">MSBuild.exe が開発者コマンド プロンプト以外から実行された場合にパッケージ配信されたプロパティ ファイルが無視される - [#4530](https://github.com/NuGet/Home/issues/4530)</span><span class="sxs-lookup"><span data-stu-id="380a4-131">Package-delivered props files ignored when MSBuild.exe is run from outside a Developer Command Prompt - [#4530](https://github.com/NuGet/Home/issues/4530)</span></span>
* <span data-ttu-id="380a4-132">プロジェクトに適用されない .NET Standard ライブラリを参照する場合のわかりづらいエラー メッセージを修正 - [#4423](https://github.com/NuGet/Home/issues/4423)</span><span class="sxs-lookup"><span data-stu-id="380a4-132">Fix poor error message when referencing .NET Standard Library that is not applicable to project - [#4423](https://github.com/NuGet/Home/issues/4423)</span></span>
* <span data-ttu-id="380a4-133">ポータブル プロファイルをターゲットとするパッケージの dotnet add package が失敗し、ほとんどガイダンスが表示されない - [#4349](https://github.com/NuGet/Home/issues/4349)</span><span class="sxs-lookup"><span data-stu-id="380a4-133">dotnet add package fails for package targeting portable profile with little guidance - [#4349](https://github.com/NuGet/Home/issues/4349)</span></span>
* <span data-ttu-id="380a4-134">dotnet pack - ProjectReference にバージョンのサフィックスがない - [#4337](https://github.com/NuGet/Home/issues/4337)</span><span class="sxs-lookup"><span data-stu-id="380a4-134">dotnet pack - version suffix missing from ProjectReference - [#4337](https://github.com/NuGet/Home/issues/4337)</span></span>
* <span data-ttu-id="380a4-135">.NET Core テンプレートのビルド エラーと VS のクラッシュ - [#3973](https://github.com/NuGet/Home/issues/3973)</span><span class="sxs-lookup"><span data-stu-id="380a4-135">Build errors and VS crash with .NET Core template - [#3973](https://github.com/NuGet/Home/issues/3973)</span></span>
* <span data-ttu-id="380a4-136">ソースの https:\* のサービス インデックスを読み込むことができない - [#3681](https://github.com/NuGet/Home/issues/3681)</span><span class="sxs-lookup"><span data-stu-id="380a4-136">Unable to load the service index for source https:\* - [#3681](https://github.com/NuGet/Home/issues/3681)</span></span>
* <span data-ttu-id="380a4-137">nuget.exe list -allversions が動作しない - [#3441](https://github.com/NuGet/Home/issues/3441)</span><span class="sxs-lookup"><span data-stu-id="380a4-137">nuget.exe list -allversions doesn't work - [#3441](https://github.com/NuGet/Home/issues/3441)</span></span>
* <span data-ttu-id="380a4-138">誤解を招く依存関係解決のエラー メッセージ - [#2984](https://github.com/NuGet/Home/issues/2984)</span><span class="sxs-lookup"><span data-stu-id="380a4-138">Misleading dependency resolution error message - [#2984](https://github.com/NuGet/Home/issues/2984)</span></span>
* <span data-ttu-id="380a4-139">nuget.exe の復元で .msbuildproj の .props および .targets ファイルが生成されない (v3.3.0-3.4.4 アップグレードの回帰) - [#2921](https://github.com/NuGet/Home/issues/2921)</span><span class="sxs-lookup"><span data-stu-id="380a4-139">nuget.exe restore doesn't produce .props and .targets files for .msbuildproj (regression in v3.3.0-3.4.4 upgrade) - [#2921](https://github.com/NuGet/Home/issues/2921)</span></span>
* <span data-ttu-id="380a4-140">XAML ファイルを開いた状態で NuGet パッケージを更新するときに UI に遅延が生じる - [#2878](https://github.com/NuGet/Home/issues/2878)</span><span class="sxs-lookup"><span data-stu-id="380a4-140">UI delay when updating a NuGet package with XAML file open - [#2878](https://github.com/NuGet/Home/issues/2878)</span></span>
* <span data-ttu-id="380a4-141">パスに不適切な文字があると、IIS の WebSite プロジェクトが失敗する - [#2798](https://github.com/NuGet/Home/issues/2798)</span><span class="sxs-lookup"><span data-stu-id="380a4-141">WebSite project from IIS fails with illegal characters in path - [#2798](https://github.com/NuGet/Home/issues/2798)</span></span>
* <span data-ttu-id="380a4-142">CentOS 上で nuget add がハングする - [#2708](https://github.com/NuGet/Home/issues/2708)</span><span class="sxs-lookup"><span data-stu-id="380a4-142">Nuget add hangs on CentOS - [#2708](https://github.com/NuGet/Home/issues/2708)</span></span>
* <span data-ttu-id="380a4-143">json.net の場合、packagesavemode -nupkg を使用した復元が失敗する - [#2706](https://github.com/NuGet/Home/issues/2706)</span><span class="sxs-lookup"><span data-stu-id="380a4-143">Restore with packagesavemode -nupkg fails for json.net - [#2706](https://github.com/NuGet/Home/issues/2706)</span></span>
* <span data-ttu-id="380a4-144">restore コマンドの vs 出力ウィンドウでパッケージ マネージャー フィルターを使用できない - [#2704](https://github.com/NuGet/Home/issues/2704)</span><span class="sxs-lookup"><span data-stu-id="380a4-144">Package Manager filter not available in vs output window for restore command - [#2704](https://github.com/NuGet/Home/issues/2704)</span></span>

[<span data-ttu-id="380a4-145">このリリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="380a4-145">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.6")
