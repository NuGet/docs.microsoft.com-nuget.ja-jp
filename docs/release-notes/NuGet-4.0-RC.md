---
title: NuGet 4.0 RC リリース ノート
description: NuGet 4.0 RC のリリース ノートであり、既知の問題、バグ修正、追加機能、および DCR が含まれています。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/03/2017
ms.topic: conceptual
ms.reviewer: ananguar
ms.openlocfilehash: 8124b11d0489a2c72ffcfdde28e8528c1da1f677
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31821887"
---
# <a name="nuget-40-rc-release-notes"></a><span data-ttu-id="4be4b-103">NuGet 4.0 RC リリース ノート</span><span class="sxs-lookup"><span data-stu-id="4be4b-103">NuGet 4.0 RC Release Notes</span></span>

[<span data-ttu-id="4be4b-104">NuGet 3.5 RTM リリース ノート</span><span class="sxs-lookup"><span data-stu-id="4be4b-104">NuGet 3.5 RTM Release Notes</span></span>](../release-notes/nuget-3.5-RTM.md)

<span data-ttu-id="4be4b-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) の焦点は .NET Core シナリオのサポートを追加することです。顧客からの重要なフィードバックに対処し、さまざまなシナリオにおけるパフォーマンスを改善します。</span><span class="sxs-lookup"><span data-stu-id="4be4b-105">[NuGet 4.0 RC for Visual Studio 2017](http://blog.nuget.org/20161121/introducing-nuget4.0) is focused on adding support for .NET Core scenarios, addressing key customer feedback and improving performance in a variety of scenarios.</span></span> <span data-ttu-id="4be4b-106">このリリースでは、PackageReference のサポート、MSBuild ターゲットとしての NuGet コマンド、バックグラウンド パッケージの復元など、いくつかの改善点があります。</span><span class="sxs-lookup"><span data-stu-id="4be4b-106">This release brings several improvements like support for PackageReference, NuGet commands as MSBuild targets, background package restore, and more.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="4be4b-107">バグ修正</span><span class="sxs-lookup"><span data-stu-id="4be4b-107">Bug Fixes</span></span>

- <span data-ttu-id="4be4b-108">`dotnet pack --version-suffix foo` の動作変更  -  [#3838](https://github.com/NuGet/Home/issues/3838)</span><span class="sxs-lookup"><span data-stu-id="4be4b-108">Behavioral changes in `dotnet pack --version-suffix foo` - [#3838](https://github.com/NuGet/Home/issues/3838)</span></span>

- <span data-ttu-id="4be4b-109">vs "15" コンピューターでのみ、nuget.exe 復元が失敗する - [#3834](https://github.com/NuGet/Home/issues/3834)</span><span class="sxs-lookup"><span data-stu-id="4be4b-109">nuget.exe restore on vs "15" machine only fails - [#3834](https://github.com/NuGet/Home/issues/3834)</span></span>

- <span data-ttu-id="4be4b-110">.NETCore ファイルの新しいプロジェクトが復元中ビルドを阻む - [#3780](https://github.com/NuGet/Home/issues/3780)</span><span class="sxs-lookup"><span data-stu-id="4be4b-110">.NETCore file new project should block the build during restore - [#3780](https://github.com/NuGet/Home/issues/3780)</span></span>

- <span data-ttu-id="4be4b-111">VS2015 から VS "15" へ移行した ASP.NET Core Web アプリを復元できない。</span><span class="sxs-lookup"><span data-stu-id="4be4b-111">ASP.NET Core web app, migrated from VS2015 to VS "15", unable to restore.</span></span><span data-ttu-id="4be4b-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span><span class="sxs-lookup"><span data-stu-id="4be4b-112"> - [#3773](https://github.com/NuGet/Home/issues/3773)</span></span>

- <span data-ttu-id="4be4b-113">[テスト不合格] パッケージ ‘jQuery 検証’ を PM UI でアンインストールできない - [#3755](https://github.com/NuGet/Home/issues/3755)</span><span class="sxs-lookup"><span data-stu-id="4be4b-113">[Test Failure]Package ‘jQuery Validation’ can’t be uninstalled by PM UI - [#3755](https://github.com/NuGet/Home/issues/3755)</span></span>

- <span data-ttu-id="4be4b-114">パッケージを UWP `project.json` にインストールするとき、親プロジェクトも復元されなければならない - [#3731](https://github.com/NuGet/Home/issues/3731)</span><span class="sxs-lookup"><span data-stu-id="4be4b-114">When a package is installed to UWP `project.json`, parent projects should also be restored - [#3731](https://github.com/NuGet/Home/issues/3731)</span></span>

- <span data-ttu-id="4be4b-115">詳細度を通常ではなく高にしてパッケージ ソースをログに記録するように NuGet ターゲットを変更する - [#3719](https://github.com/NuGet/Home/issues/3719)</span><span class="sxs-lookup"><span data-stu-id="4be4b-115">Modify the NuGet targets to log the package sources as High verbosity instead of Normal - [#3719](https://github.com/NuGet/Home/issues/3719)</span></span>

- <span data-ttu-id="4be4b-116">dotnet</span><span class="sxs-lookup"><span data-stu-id="4be4b-116">dotnet</span></span>
  - <span data-ttu-id="4be4b-117">dotnetcore pack3 には既定で XML ドキュメントを含める必要がある - [#3698](https://github.com/NuGet/Home/issues/3698)</span><span class="sxs-lookup"><span data-stu-id="4be4b-117">dotnetcore pack3 should include XML documentation by default - [#3698](https://github.com/NuGet/Home/issues/3698)</span></span>

- <span data-ttu-id="4be4b-118">パッケージなしのソースが最初で、すべてのソースが選択されているとき、UI から一括更新できない - [#3696](https://github.com/NuGet/Home/issues/3696)</span><span class="sxs-lookup"><span data-stu-id="4be4b-118">Batch update fails from UI when source without the package is first and All source is selected - [#3696](https://github.com/NuGet/Home/issues/3696)</span></span>

- <span data-ttu-id="4be4b-119">Nuget パック コマンドにすべてのファイルが含まれない - [#3678](https://github.com/NuGet/Home/issues/3678)</span><span class="sxs-lookup"><span data-stu-id="4be4b-119">Nuget pack command does not include all files - [#3678](https://github.com/NuGet/Home/issues/3678)</span></span>

- <span data-ttu-id="4be4b-120">OOM 問題 - [#3661](https://github.com/NuGet/Home/issues/3661)</span><span class="sxs-lookup"><span data-stu-id="4be4b-120">OOM issue - [#3661](https://github.com/NuGet/Home/issues/3661)</span></span>

- <span data-ttu-id="4be4b-121">アセット ファイルの ProjectFileDependencyGroups セクションでプロジェクトにライブラリ名を使用する必要がある - [#3611](https://github.com/NuGet/Home/issues/3611)</span><span class="sxs-lookup"><span data-stu-id="4be4b-121">ProjectFileDependencyGroups section of the assets file should use library names for projects - [#3611](https://github.com/NuGet/Home/issues/3611)</span></span>

- <span data-ttu-id="4be4b-122">"dotnet restore" と再帰するディレクトリ - [#3517](https://github.com/NuGet/Home/issues/3517)</span><span class="sxs-lookup"><span data-stu-id="4be4b-122">"dotnet restore" and recursing directories - [#3517](https://github.com/NuGet/Home/issues/3517)</span></span>

- <span data-ttu-id="4be4b-123">Restore3 の問題がエラーではなく警告としてログに記録される - [#3503](https://github.com/NuGet/Home/issues/3503)</span><span class="sxs-lookup"><span data-stu-id="4be4b-123">Restore3 failures are logged as warnings instead of errors - [#3503](https://github.com/NuGet/Home/issues/3503)</span></span>

- <span data-ttu-id="4be4b-124">TFS 問題: "ワークスペースで [ファイル] が見つからないか、それにアクセスする許可がない" - [#2805](https://github.com/NuGet/Home/issues/2805)</span><span class="sxs-lookup"><span data-stu-id="4be4b-124">TFS issue: "[file]not be found in your workspace, or you do not have permission to access it" - [#2805](https://github.com/NuGet/Home/issues/2805)</span></span>

- <span data-ttu-id="4be4b-125">vs クイック起動検索ボックスに "nuget <packagename>" と入力すると、"nuget " プレフィックスが維持される - [#2719](https://github.com/NuGet/Home/issues/2719)</span><span class="sxs-lookup"><span data-stu-id="4be4b-125">Typing "nuget <packagename>" in vs quicklaunch search box keeps "nuget " prefix - [#2719](https://github.com/NuGet/Home/issues/2719)</span></span>

- <span data-ttu-id="4be4b-126">System.Xml.XmlException: Core Properties パートのルート要素を認識できない。</span><span class="sxs-lookup"><span data-stu-id="4be4b-126">System.Xml.XmlException: Unrecognized root element in Core Properties part.</span></span> <span data-ttu-id="4be4b-127">ライン 2、位置 2。</span><span class="sxs-lookup"><span data-stu-id="4be4b-127">Line 2, position 2.</span></span><span data-ttu-id="4be4b-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span><span class="sxs-lookup"><span data-stu-id="4be4b-128"> - [#2718](https://github.com/NuGet/Home/issues/2718)</span></span>

- <span data-ttu-id="4be4b-129">テキスト フィールドの &lt; または &gt; をエスケープ処理すると、`.nuspec` がビルドされなくなる - [#2651](https://github.com/NuGet/Home/issues/2651)</span><span class="sxs-lookup"><span data-stu-id="4be4b-129">`.nuspec` with escaped &lt; or &gt; in text fields no longer builds - [#2651](https://github.com/NuGet/Home/issues/2651)</span></span>

- <span data-ttu-id="4be4b-130">nuget.exe 削除で資格情報が求められない (非対話モードで) - [#2626](https://github.com/NuGet/Home/issues/2626)</span><span class="sxs-lookup"><span data-stu-id="4be4b-130">nuget.exe delete won't prompt for credentials (it's in non-interactive mode) - [#2626](https://github.com/NuGet/Home/issues/2626)</span></span>

- <span data-ttu-id="4be4b-131">nuget.exe 削除でローカル ソースの API キーに関して、意味がない場合にも警告される - [#2625](https://github.com/NuGet/Home/issues/2625)</span><span class="sxs-lookup"><span data-stu-id="4be4b-131">nuget.exe delete warns about API Key for local sources, even though it makes no sense - [#2625](https://github.com/NuGet/Home/issues/2625)</span></span>

- <span data-ttu-id="4be4b-132">EF プリパッケージのインストール時、エラー処理が望ましくない - [#2566](https://github.com/NuGet/Home/issues/2566)</span><span class="sxs-lookup"><span data-stu-id="4be4b-132">Error experience poor when installing EF -pre package - [#2566](https://github.com/NuGet/Home/issues/2566)</span></span>

- <span data-ttu-id="4be4b-133">パッケージ マネージャーで選択を変更後、Visual Studio がクラッシュ - [#2551](https://github.com/NuGet/Home/issues/2551)</span><span class="sxs-lookup"><span data-stu-id="4be4b-133">Visual Studio crashed attempting after changing selection in Package Manager - [#2551](https://github.com/NuGet/Home/issues/2551)</span></span>

- <span data-ttu-id="4be4b-134">dotnet</span><span class="sxs-lookup"><span data-stu-id="4be4b-134">dotnet</span></span>
  - <span data-ttu-id="4be4b-135">浮動バージョンが使用されているとき、フラット リストのローカル リポジトリで、dotnetcore 復元が小文字と大文字を区別して ID を参照する - [#2516](https://github.com/NuGet/Home/issues/2516)</span><span class="sxs-lookup"><span data-stu-id="4be4b-135">dotnetcore restore performs case sensitive Id lookups on flat-list local repositories when floating versions are used - [#2516](https://github.com/NuGet/Home/issues/2516)</span></span>

- <span data-ttu-id="4be4b-136">V2 フィードで nuget.exe 削除が壊れる - [#2509](https://github.com/NuGet/Home/issues/2509)</span><span class="sxs-lookup"><span data-stu-id="4be4b-136">nuget.exe delete is broken for V2 feed - [#2509](https://github.com/NuGet/Home/issues/2509)</span></span>

- <span data-ttu-id="4be4b-137">nuget.exe プッシュのタイムアウトでエラー メッセージの改善が必要 - [#2503](https://github.com/NuGet/Home/issues/2503)</span><span class="sxs-lookup"><span data-stu-id="4be4b-137">nuget.exe push timeout needs a better error message - [#2503](https://github.com/NuGet/Home/issues/2503)</span></span>

- <span data-ttu-id="4be4b-138">適切なインポートなしのツール復元が警告なく失敗する。</span><span class="sxs-lookup"><span data-stu-id="4be4b-138">Tool restore without proper imports silently fails.</span></span><span data-ttu-id="4be4b-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span><span class="sxs-lookup"><span data-stu-id="4be4b-139"> - [#2462](https://github.com/NuGet/Home/issues/2462)</span></span>

- <span data-ttu-id="4be4b-140">nuget.org からインストールするときでも、プライベート フィードがあると、NuGet が資格情報の入力を求める - [#2346](https://github.com/NuGet/Home/issues/2346)</span><span class="sxs-lookup"><span data-stu-id="4be4b-140">NuGet prompts to enter credentials when there is a private feed even when installing from nuget.org - [#2346](https://github.com/NuGet/Home/issues/2346)</span></span>

- <span data-ttu-id="4be4b-141">ApplicationInsights 2.0 パッケージが一覧にあるが、存在しない - [#2317](https://github.com/NuGet/Home/issues/2317)</span><span class="sxs-lookup"><span data-stu-id="4be4b-141">ApplicationInsights 2.0 package is listed but doesn't exist yet - [#2317](https://github.com/NuGet/Home/issues/2317)</span></span>

- <span data-ttu-id="4be4b-142">VS "15" プレビュー 5 ブランチの UIDelay - [#3500](https://github.com/NuGet/Home/issues/3500)</span><span class="sxs-lookup"><span data-stu-id="4be4b-142">UIDelay in VS "15" preview 5 branch - [#3500](https://github.com/NuGet/Home/issues/3500)</span></span>

- <span data-ttu-id="4be4b-143">UWP のビルド中、復元に対して最初の OnBuild イベントがない - [#3489](https://github.com/NuGet/Home/issues/3489)</span><span class="sxs-lookup"><span data-stu-id="4be4b-143">First OnBuild event is missed for Restore during Build for UWP - [#3489](https://github.com/NuGet/Home/issues/3489)</span></span>

- <span data-ttu-id="4be4b-144">PowerShell 5 で EntityFramework のインストールが中断される</span><span class="sxs-lookup"><span data-stu-id="4be4b-144">PowerShell5 breaks EntityFramework install?</span></span><span data-ttu-id="4be4b-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span><span class="sxs-lookup"><span data-stu-id="4be4b-145"> - [#3312](https://github.com/NuGet/Home/issues/3312)</span></span>

- <span data-ttu-id="4be4b-146">詳細なログ記録にソースを追加 (3.5 で考慮) - [#3294](https://github.com/NuGet/Home/issues/3294)</span><span class="sxs-lookup"><span data-stu-id="4be4b-146">Add source to detailed logging (consider for 3.5) - [#3294](https://github.com/NuGet/Home/issues/3294)</span></span>

- <span data-ttu-id="4be4b-147">NoCache パラメーターが nuget クライアント バージョン 3.4+ で無視される - [#3074](https://github.com/NuGet/Home/issues/3074)</span><span class="sxs-lookup"><span data-stu-id="4be4b-147">NoCache parameter not honored in nuget client version 3.4+ - [#3074](https://github.com/NuGet/Home/issues/3074)</span></span>

- <span data-ttu-id="4be4b-148">資格情報プロバイダーが VS に読み込まれないとき、NuGet が中断されない - [#2422](https://github.com/NuGet/Home/issues/2422)</span><span class="sxs-lookup"><span data-stu-id="4be4b-148">When a credential provider fails to load in VS, don't break NuGet - [#2422](https://github.com/NuGet/Home/issues/2422)</span></span>

## <a name="features"></a><span data-ttu-id="4be4b-149">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="4be4b-149">Features</span></span>

- <span data-ttu-id="4be4b-150">x86 を実行するように CI を設定する - [#3868](https://github.com/NuGet/Home/issues/3868)</span><span class="sxs-lookup"><span data-stu-id="4be4b-150">Set up CI to run x86 - [#3868](https://github.com/NuGet/Home/issues/3868)</span></span>

- <span data-ttu-id="4be4b-151">自動復元 3/3: 非ブロッキング UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span><span class="sxs-lookup"><span data-stu-id="4be4b-151">Auto Restore 3/3: non blocking UI - [#3658](https://github.com/NuGet/Home/issues/3658)</span></span>

- <span data-ttu-id="4be4b-152">自動復元 2/3: 指名時のバックグラウンド復元 - [#3657](https://github.com/NuGet/Home/issues/3657)</span><span class="sxs-lookup"><span data-stu-id="4be4b-152">Auto Restore 2/3: background restore on nomination - [#3657](https://github.com/NuGet/Home/issues/3657)</span></span>

- <span data-ttu-id="4be4b-153">ビルド動作に一致するようにプロジェクト参照を復元 (再帰) - [#3615](https://github.com/NuGet/Home/issues/3615)</span><span class="sxs-lookup"><span data-stu-id="4be4b-153">Restore project refs to match build behavior (recurse) - [#3615](https://github.com/NuGet/Home/issues/3615)</span></span>

- <span data-ttu-id="4be4b-154">VS "15" で DPL サポート - ミニバー - [#3614](https://github.com/NuGet/Home/issues/3614)</span><span class="sxs-lookup"><span data-stu-id="4be4b-154">DPL support in VS "15" - minbar - [#3614](https://github.com/NuGet/Home/issues/3614)</span></span>

- <span data-ttu-id="4be4b-155">設定ファイルをプログラム ファイルに移動 - [#3613](https://github.com/NuGet/Home/issues/3613)</span><span class="sxs-lookup"><span data-stu-id="4be4b-155">Move settings file to Program Files - [#3613](https://github.com/NuGet/Home/issues/3613)</span></span>

- <span data-ttu-id="4be4b-156">生成された復元 props と targets に複数のバージョン対応が必要 - [#3496](https://github.com/NuGet/Home/issues/3496)</span><span class="sxs-lookup"><span data-stu-id="4be4b-156">Generated restore props and targets need cross-targeting participation support - [#3496](https://github.com/NuGet/Home/issues/3496)</span></span>

- <span data-ttu-id="4be4b-157">PackageTargetFallback の NuGet 復元サポート (以前のインポート) - [#3494](https://github.com/NuGet/Home/issues/3494)</span><span class="sxs-lookup"><span data-stu-id="4be4b-157">NuGet Restore support for PackageTargetFallback (f.k.a Imports) - [#3494](https://github.com/NuGet/Home/issues/3494)</span></span>

- <span data-ttu-id="4be4b-158">ToolsRef 実装 - [#3472](https://github.com/NuGet/Home/issues/3472)</span><span class="sxs-lookup"><span data-stu-id="4be4b-158">ToolsRef implementation - [#3472](https://github.com/NuGet/Home/issues/3472)</span></span>

- <span data-ttu-id="4be4b-159">RID の Restore3 - [#3465](https://github.com/NuGet/Home/issues/3465)</span><span class="sxs-lookup"><span data-stu-id="4be4b-159">Restore3 for a RID - [#3465](https://github.com/NuGet/Home/issues/3465)</span></span>

- <span data-ttu-id="4be4b-160">NuGet UI で PackageRefs の追加、削除、更新に対応 - [#3457](https://github.com/NuGet/Home/issues/3457)</span><span class="sxs-lookup"><span data-stu-id="4be4b-160">NuGet UI to support Add/Remove/Update of PackageRefs - [#3457](https://github.com/NuGet/Home/issues/3457)</span></span>

- <span data-ttu-id="4be4b-161">自動復元 1/3: プロジェクト復元情報のキャッシュによる指定 API の実装 - [#3456](https://github.com/NuGet/Home/issues/3456)</span><span class="sxs-lookup"><span data-stu-id="4be4b-161">Auto Restore 1/3: Implemenation of Nomination API via Caching Project Restore Info - [#3456](https://github.com/NuGet/Home/issues/3456)</span></span>

- <span data-ttu-id="4be4b-162">[0] NuGet 復元タスクとターゲット - [#2994](https://github.com/NuGet/Home/issues/2994)</span><span class="sxs-lookup"><span data-stu-id="4be4b-162">[0] NuGet Restore Task & Targets - [#2994](https://github.com/NuGet/Home/issues/2994)</span></span>

- <span data-ttu-id="4be4b-163">[1] MSBuild のソリューションレベル復元を有効にする - [#2993](https://github.com/NuGet/Home/issues/2993)</span><span class="sxs-lookup"><span data-stu-id="4be4b-163">[1] Enable Solution level restore in MSBuild - [#2993](https://github.com/NuGet/Home/issues/2993)</span></span>

- <span data-ttu-id="4be4b-164">Visual Studio で資格情報プロバイダーのパブリック拡張をサポート - [#2909](https://github.com/NuGet/Home/issues/2909)</span><span class="sxs-lookup"><span data-stu-id="4be4b-164">Support credential provider public extensibility in Visual Studio - [#2909](https://github.com/NuGet/Home/issues/2909)</span></span>

- <span data-ttu-id="4be4b-165">再帰的 nuget 復元 - [#2533](https://github.com/NuGet/Home/issues/2533)</span><span class="sxs-lookup"><span data-stu-id="4be4b-165">Recursive nuget restore - [#2533](https://github.com/NuGet/Home/issues/2533)</span></span>

- <span data-ttu-id="4be4b-166">dev15 で Microsoft.TeamFoundation.Client を読み込めず、VS "15" プレビューに関して、Microsoft.TeamFoundation.Client バージョンを 15.0 に更新する必要がある - [#2392](https://github.com/NuGet/Home/issues/2392)</span><span class="sxs-lookup"><span data-stu-id="4be4b-166">Can't load Microsoft.TeamFoundation.Client on dev15, need to update Microsoft.TeamFoundation.Client version to 15.0 for VS "15" Preview - [#2392](https://github.com/NuGet/Home/issues/2392)</span></span>

- <span data-ttu-id="4be4b-167">VS "15" プレビューで C++ UWP プロジェクトに C++ パッケージをインストールできない - [#2369](https://github.com/NuGet/Home/issues/2369)</span><span class="sxs-lookup"><span data-stu-id="4be4b-167">Unable to install C++ package to C++ UWP project in VS "15" Preview - [#2369](https://github.com/NuGet/Home/issues/2369)</span></span>

- <span data-ttu-id="4be4b-168">Nupkg で \buildCrossTargeting\ フォルダーをサポートする必要あり - また、"複数バージョン対応の" MSBuild スコープに `.targets` / `.props` をインポートする必要あり。</span><span class="sxs-lookup"><span data-stu-id="4be4b-168">Nupkg needs to support \buildCrossTargeting\ folder - and import `.targets` / `.props` for "crosstargeting" MSBuild scope.</span></span><span data-ttu-id="4be4b-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span><span class="sxs-lookup"><span data-stu-id="4be4b-169"> - [#3499](https://github.com/NuGet/Home/issues/3499)</span></span>

- <span data-ttu-id="4be4b-170">ToolsReference デザイン - [#3462](https://github.com/NuGet/Home/issues/3462)</span><span class="sxs-lookup"><span data-stu-id="4be4b-170">ToolsReference Design - [#3462](https://github.com/NuGet/Home/issues/3462)</span></span>

- <span data-ttu-id="4be4b-171">`.csproj` で復元と PackageReferences をサポートするように NuGet UI を修正  -  [#3455](https://github.com/NuGet/Home/issues/3455)</span><span class="sxs-lookup"><span data-stu-id="4be4b-171">Fix NuGet UI to support restore w/ PackageReferences in `.csproj` - [#3455](https://github.com/NuGet/Home/issues/3455)</span></span>

- <span data-ttu-id="4be4b-172">VS パッケージ マネージャー設定にキャッシュ消去ボタンを追加 - [#3289](https://github.com/NuGet/Home/issues/3289)</span><span class="sxs-lookup"><span data-stu-id="4be4b-172">Adding clear cache button to VS package manager settings - [#3289](https://github.com/NuGet/Home/issues/3289)</span></span>

## <a name="dcrs"></a><span data-ttu-id="4be4b-173">DCR</span><span class="sxs-lookup"><span data-stu-id="4be4b-173">DCRs</span></span>

- <span data-ttu-id="4be4b-174">自動復元中、ソリューション復元を防ぐ必要あり。</span><span class="sxs-lookup"><span data-stu-id="4be4b-174">Solution Restore should be blocked while auto restore is happening.</span></span><span data-ttu-id="4be4b-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span><span class="sxs-lookup"><span data-stu-id="4be4b-175"> - [#3797](https://github.com/NuGet/Home/issues/3797)</span></span>

- <span data-ttu-id="4be4b-176">NuGet パッケージ マネージャー UI からの NetCore インストールで、パッケージがサポートしているものではなく、すべての TFM にインストールされる - [#3721](https://github.com/NuGet/Home/issues/3721)</span><span class="sxs-lookup"><span data-stu-id="4be4b-176">NetCore install from NuGet Package Manager UI installs to every TFM , instead of ones that the package supports - [#3721](https://github.com/NuGet/Home/issues/3721)</span></span>

- <span data-ttu-id="4be4b-177">復元を指定する API で DotNetCliToolsReferences もサポートする必要あり。</span><span class="sxs-lookup"><span data-stu-id="4be4b-177">Restore nominator API needs to support DotNetCliToolsReferences too.</span></span><span data-ttu-id="4be4b-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span><span class="sxs-lookup"><span data-stu-id="4be4b-178"> - [#3702](https://github.com/NuGet/Home/issues/3702)</span></span>

- <span data-ttu-id="4be4b-179">VS "15" vsix をシステム コンポーネントとしてマークする - [#3700](https://github.com/NuGet/Home/issues/3700)</span><span class="sxs-lookup"><span data-stu-id="4be4b-179">Mark our VS "15" vsix as a systemcomponent - [#3700](https://github.com/NuGet/Home/issues/3700)</span></span>

- <span data-ttu-id="4be4b-180">参照元 MS.VS.Services.Client から MS.VS.Services.Client.Interactive に移行する - [#3670](https://github.com/NuGet/Home/issues/3670)</span><span class="sxs-lookup"><span data-stu-id="4be4b-180">Migrate from referencing MS.VS.Services.Client to MS.VS.Services.Client.Interactive - [#3670](https://github.com/NuGet/Home/issues/3670)</span></span>

- <span data-ttu-id="4be4b-181">$(RestoreLegacyPackagesDirectory) は復元時、プロジェクト レベルで適用される必要あり - [#3618](https://github.com/NuGet/Home/issues/3618)</span><span class="sxs-lookup"><span data-stu-id="4be4b-181">$(RestoreLegacyPackagesDirectory) should be respected at a project level by restore - [#3618](https://github.com/NuGet/Home/issues/3618)</span></span>

- <span data-ttu-id="4be4b-182">シングル TargetFramework のプロジェクトに復元するとき、props を条件にするべきではない - [#3588](https://github.com/NuGet/Home/issues/3588)</span><span class="sxs-lookup"><span data-stu-id="4be4b-182">Restore to project with single TargetFramework must not condition props - [#3588](https://github.com/NuGet/Home/issues/3588)</span></span>

- <span data-ttu-id="4be4b-183">dotnet</span><span class="sxs-lookup"><span data-stu-id="4be4b-183">dotnet</span></span>
  - <span data-ttu-id="4be4b-184">dotnetcore restore3 foo.csproj は projectref 依存関係に従い、それらも復元する必要あり。</span><span class="sxs-lookup"><span data-stu-id="4be4b-184">dotnetcore restore3 foo.csproj should follow projectref dependencies, and restore those too.</span></span> <span data-ttu-id="4be4b-185">ビルドのように。</span><span class="sxs-lookup"><span data-stu-id="4be4b-185">Like build.</span></span><span data-ttu-id="4be4b-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span><span class="sxs-lookup"><span data-stu-id="4be4b-186"> - [#3577](https://github.com/NuGet/Home/issues/3577)</span></span>

- <span data-ttu-id="4be4b-187">"type": "platform" 依存関係が "type" として表現される: ロック ファイルの "package" - [#2695](https://github.com/NuGet/Home/issues/2695)</span><span class="sxs-lookup"><span data-stu-id="4be4b-187">"type": "platform" Dependencies represented as "type":"package" in lock file - [#2695](https://github.com/NuGet/Home/issues/2695)</span></span>

- <span data-ttu-id="4be4b-188">nuget.exe 詳細モードでダウンロード URL を表示する必要がある - [#2629](https://github.com/NuGet/Home/issues/2629)</span><span class="sxs-lookup"><span data-stu-id="4be4b-188">nuget.exe Verbose mode should show the download url - [#2629](https://github.com/NuGet/Home/issues/2629)</span></span>

- <span data-ttu-id="4be4b-189">NuGet xplat を Microsoft.NetCore.App と netcoreapp1.0 に移動する - [#2483](https://github.com/NuGet/Home/issues/2483)</span><span class="sxs-lookup"><span data-stu-id="4be4b-189">Move NuGet xplat to Microsoft.NetCore.App and netcoreapp1.0 - [#2483](https://github.com/NuGet/Home/issues/2483)</span></span>

- <span data-ttu-id="4be4b-190">プッシュ - コマンド ラインからプッシュするとき、シンボル サーバーを上書きできなければならない - [#2348](https://github.com/NuGet/Home/issues/2348)</span><span class="sxs-lookup"><span data-stu-id="4be4b-190">Push - It should be possible to override the symbol server when pushing from the command line - [#2348](https://github.com/NuGet/Home/issues/2348)</span></span>

- <span data-ttu-id="4be4b-191">グローバル パッケージ パスを見つけるためにコードを連結する - [#2296](https://github.com/NuGet/Home/issues/2296)</span><span class="sxs-lookup"><span data-stu-id="4be4b-191">Consolidate code for finding the global packages path - [#2296](https://github.com/NuGet/Home/issues/2296)</span></span>

- <span data-ttu-id="4be4b-192">suppressParent よりもよい名前が必要 - [#2196](https://github.com/NuGet/Home/issues/2196)</span><span class="sxs-lookup"><span data-stu-id="4be4b-192">Need a better name than suppressParent - [#2196](https://github.com/NuGet/Home/issues/2196)</span></span>

- <span data-ttu-id="4be4b-193">MSBuild プロジェクトに使用する `project.json` 依存関係名を決定する - [#1914](https://github.com/NuGet/Home/issues/1914)</span><span class="sxs-lookup"><span data-stu-id="4be4b-193">Determine `project.json` dependency name to use for MSBuild projects - [#1914](https://github.com/NuGet/Home/issues/1914)</span></span>

- <span data-ttu-id="4be4b-194">SemVer 2.0.0 サポートを NuGet.Core に追加 - [#3383](https://github.com/NuGet/Home/issues/3383)</span><span class="sxs-lookup"><span data-stu-id="4be4b-194">Add SemVer 2.0.0 support to NuGet.Core - [#3383](https://github.com/NuGet/Home/issues/3383)</span></span>

- <span data-ttu-id="4be4b-195">推移的依存関係 NuPkgs と `.targets` を MSBuild で利用できるようにする - [#3342](https://github.com/NuGet/Home/issues/3342)</span><span class="sxs-lookup"><span data-stu-id="4be4b-195">Allow transitive dependency NuPkgs with `.targets` to be available in MSBuild - [#3342](https://github.com/NuGet/Home/issues/3342)</span></span>

- <span data-ttu-id="4be4b-196">コマンドラインからの NuGet 復元が VS より大幅に遅い - [#3330](https://github.com/NuGet/Home/issues/3330)</span><span class="sxs-lookup"><span data-stu-id="4be4b-196">NuGet restore from the commandline is significantly slower than VS - [#3330](https://github.com/NuGet/Home/issues/3330)</span></span>

- <span data-ttu-id="4be4b-197">パッケージ ID とバージョン比較で大文字と小文字を区別するようにする - [#2522](https://github.com/NuGet/Home/issues/2522)</span><span class="sxs-lookup"><span data-stu-id="4be4b-197">Make package ID and version comparison case insensitive - [#2522](https://github.com/NuGet/Home/issues/2522)</span></span>

- <span data-ttu-id="4be4b-198">NoCache オプションが `packages.config` ベースの復元/インストールで機能しない (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span><span class="sxs-lookup"><span data-stu-id="4be4b-198">NoCache option does not work for `packages.config` based restore/install (GlobalPackagesFolder) - [#1406](https://github.com/NuGet/Home/issues/1406)</span></span>

- <span data-ttu-id="4be4b-199">FindPackageByIdResource リソースに既定のキャッシュ コンテキストとロガーが必要 - [#1357](https://github.com/NuGet/Home/issues/1357)</span><span class="sxs-lookup"><span data-stu-id="4be4b-199">FindPackageByIdResource resources needs a default cache context and logger - [#1357](https://github.com/NuGet/Home/issues/1357)</span></span>
