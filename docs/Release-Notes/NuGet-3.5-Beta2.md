---
title: "3.5 Beta2 リリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b76064f-0607-438a-bbf8-dd862690f48e
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.5 Beta 2 をリリース ノートです。"
keywords: "NuGet 3.5 Beta 2 リリース ノートについては、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6dd388e52308d2f3cd32d4d6c66c2868f0ae2a41
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="35-beta2-release-notes"></a><span data-ttu-id="6dc07-104">3.5 Beta2 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="6dc07-104">3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="6dc07-105">[NuGet 3.5 ベータ リリース ノート](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC のリリース ノート](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="6dc07-105">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="6dc07-106">Visual Studio 2013 と nuget.exe 用、2016 年 6 月 27 日にリリースされた NuGet 3.5 Beta 2 RTM</span><span class="sxs-lookup"><span data-stu-id="6dc07-106">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="6dc07-107">すべての変更ログ</span><span class="sxs-lookup"><span data-stu-id="6dc07-107">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="6dc07-108">懸案事項の一覧</span><span class="sxs-lookup"><span data-stu-id="6dc07-108">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

# <a name="notable-changes"></a><span data-ttu-id="6dc07-109">主な変更点</span><span class="sxs-lookup"><span data-stu-id="6dc07-109">Notable Changes</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6dc07-110">バグ修正</span><span class="sxs-lookup"><span data-stu-id="6dc07-110">Bug Fixes</span></span>

* <span data-ttu-id="6dc07-111">最新のエラー メッセージの認証されたフィードは、.NET Core でのパスワード decrpytion のサポートの不足が[#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="6dc07-111">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="6dc07-112">パッケージ マネージャー コンソール Get-パッケージが失敗する .NET Core プロジェクトを開く - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="6dc07-112">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="6dc07-113">NuGet プッシュ コマンドで 403 が不適切に処理を修正[#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="6dc07-113">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="6dc07-114">DisableSourceControlIntegration が設定されている場合は、TFS ソース管理にバインドされているソリューション内のパッケージのアンインストールで問題を修正 true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="6dc07-114">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="6dc07-115">アカウントのターゲットではないパッケージ - を考慮するパッケージの更新の修正[#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="6dc07-115">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="6dc07-116">レベルを設定するロガー Nuget パッケージ マネージャーの UI アクションの MSBuild の詳細レベルを使用して[#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="6dc07-116">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="6dc07-117">修正プログラムの NuGet 構成が無効な web サイト プロジェクトの VS 2015 VSIX (v3.4.3) - エラー [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="6dc07-117">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="6dc07-118">パックに関する問題を修正`.csproj`コンテンツ ファイルが含まれています - とき[#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="6dc07-118">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="6dc07-119">DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) は機能しません - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="6dc07-119">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="6dc07-120">値をパッケージの作成時に null にすることはできません - Nuget 3.4.3 リリースで問題を解決[#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="6dc07-120">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="6dc07-121">復元は Nuget.Config から保存された資格情報を使用して VSTS フィード - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="6dc07-121">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="6dc07-122">パフォーマンス - バージョンの比較コード内の修正プログラムの過剰な割り当て - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="6dc07-122">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="6dc07-123">Nuget.exe の複数のインスタンスが並列 - 同じパッケージをインストールしようとするときの問題を修正[#2628](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="6dc07-123">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="6dc07-124">パフォーマンス - 複数のプロジェクトの操作の依存関係情報をキャッシュ - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="6dc07-124">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="6dc07-125">問題を修正パッケージのソースは追加設定から基になるリストが空のときに、 [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="6dc07-125">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="6dc07-126">デザイン時のファサード - に依存しているパッケージをインストールしようとするときは、誤解を招きやすいエラーを修正する[#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="6dc07-126">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="6dc07-127">だけ最初のソースの設定"All"PackageManager コンソールから、パッケージをインストールしようと[#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="6dc07-127">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="6dc07-128">(モノラル) - 書き込みの際、将来にファイルがパッケージの問題が修正[#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="6dc07-128">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="6dc07-129">障害が発生、検索するプロジェクトの更新のコマンドでは、例外を表示[#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="6dc07-129">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="6dc07-130">引数でフィード nuget v3.3 + からパッケージをインストールするときにパッケージの内容は正しく復元されません - NoCache パッケージが含まれている`.nupkg`ファイル - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="6dc07-130">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="6dc07-131">-1 つのソースからパッケージが見つからない場合に、パッケージに問題を修正プログラムが (すべてのソース) をインストール[#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="6dc07-131">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="6dc07-132">1 つのソースの承認に失敗した場合は、ブロックをインストール[#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="6dc07-132">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="6dc07-133">`.nuspec`バージョン範囲は-IncludeReferencedProjects バージョン - をオーバーライドする必要があります[#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="6dc07-133">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="6dc07-134">NuGet 3.3.0 更新で失敗 ' 追加の制約 で定義されている packages.config には、この動作ができなくなります '。</span><span class="sxs-lookup"><span data-stu-id="6dc07-134">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="6dc07-135"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="6dc07-135"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="6dc07-136">nuget.exe の更新プログラムは、アセンブリの厳密な名前およびプライベートの属性を削除します。</span><span class="sxs-lookup"><span data-stu-id="6dc07-136">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="6dc07-137"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="6dc07-137"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="6dc07-138">"DefaultPushSource"- の相対ファイル パスの問題が修正[#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="6dc07-138">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="6dc07-139">更新の競合回避モジュール エラー メッセージを向上させる[#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="6dc07-139">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="6dc07-140">機能および動作変更</span><span class="sxs-lookup"><span data-stu-id="6dc07-140">Features and Behavior Changes</span></span>

* <span data-ttu-id="6dc07-141">nuget.exe プッシュ タイムアウト パラメーターは機能しません - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="6dc07-141">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="6dc07-142">nuget.exe restore を生成しない`.props`と`.targets`ファイル`.nuproj`プロジェクト (v3.4.3.855 の回帰) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="6dc07-142">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="6dc07-143">機能拡張 API フレームワークでのインポートとを比較する必要がある[#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="6dc07-143">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="6dc07-144">使用する場合は、依存関係のオプションを非表示に`project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="6dc07-144">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="6dc07-145">詳細な出力に nuget.exe バージョン ヘッダーを印刷[#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="6dc07-145">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="6dc07-146">NuGet は、{rid}/runtimes//nativeassets/{txm} のサポートを追加する必要があります/- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="6dc07-146">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>