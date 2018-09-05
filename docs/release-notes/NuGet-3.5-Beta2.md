---
title: 3.5 beta 2 リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.5 Beta 2 のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b47939e2fafc11823c41a849b3c58bbf0800ada
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551992"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="c2733-103">NuGet 3.5 beta 2 リリース ノートします。</span><span class="sxs-lookup"><span data-stu-id="c2733-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="c2733-104">[NuGet 3.5 のベータ リリース ノート](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5 RC リリース ノート](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="c2733-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="c2733-105">用と nuget.exe の Visual Studio 2013、2016 年 6 月 27 日にリリースされた NuGet 3.5 Beta 2 の RTM</span><span class="sxs-lookup"><span data-stu-id="c2733-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="c2733-106">完全な変更ログ</span><span class="sxs-lookup"><span data-stu-id="c2733-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="c2733-107">懸案事項リスト</span><span class="sxs-lookup"><span data-stu-id="c2733-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="c2733-108">バグ修正</span><span class="sxs-lookup"><span data-stu-id="c2733-108">Bug Fixes</span></span>

* <span data-ttu-id="c2733-109">更新されたエラー メッセージの認証されたフィード - .NET Core でのパスワード decrpytion のサポートの不足を[#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="c2733-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="c2733-110">パッケージ マネージャー コンソール Get-パッケージが失敗する場合は、.NET Core プロジェクトを開く - [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="c2733-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="c2733-111">NuGet push コマンドで 403 が不適切に処理を修正[#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="c2733-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="c2733-112">DisableSourceControlIntegration が設定されている場合は、TFS ソース管理にバインドされているソリューション内のパッケージのアンインストールで問題を修正する true - [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="c2733-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="c2733-113">アカウントのターゲット以外パッケージ - を考慮するパッケージの更新の修正[#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="c2733-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="c2733-114">MSBuild の詳細レベルを使用して UI アクションの Nuget パッケージ マネージャーのログ レベルを設定する[#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="c2733-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="c2733-115">NuGet の構成の修正プログラムは、web サイト プロジェクトの VS 2015 VSIX (v3.4.3) - で無効なエラー [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="c2733-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="c2733-116">パックに関する問題を修正`.csproj`コンテンツ ファイルが含まれています - とき[#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="c2733-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="c2733-117">DefaultPushSource `NuGetDefaults.Config` (`ProgramData\NuGet`) が動作しない - [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="c2733-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="c2733-118">値をパッケージの作成時に null にすることはできません - Nuget 3.4.3 リリースで問題を解決[#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="c2733-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="c2733-119">復元は Nuget.Config から保存された資格情報を使用して VSTS フィード - [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="c2733-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="c2733-120">パフォーマンス - 内のバージョンの比較コード修正の過剰な割り当て - [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="c2733-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="c2733-121">Nuget.exe の複数のインスタンスが、並列 - 同じパッケージをインストールしようとしています問題を修正[#2628。](https://github.com/NuGet/Home/issues/2628)</span><span class="sxs-lookup"><span data-stu-id="c2733-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="c2733-122">パフォーマンスのマルチ プロジェクトの操作の依存関係情報をキャッシュ - [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="c2733-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="c2733-123">問題を修正するソースのリストが空の場合に、パッケージ ソースというが設定から追加する場所[#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="c2733-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="c2733-124">デザイン時のファサードに依存するパッケージをインストールするときに、誤解を招きやすいエラーを修正する[#2594](https://github.com/NuGet/Home/issues/2594)</span><span class="sxs-lookup"><span data-stu-id="c2733-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="c2733-125">のみ最初のソース -"All"の設定で PackageManager コンソールからパッケージをインストールしようと[#2557](https://github.com/NuGet/Home/issues/2557)</span><span class="sxs-lookup"><span data-stu-id="c2733-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="c2733-126">書き込み時間が、将来の (Mono) - ファイルのパッケージに関する問題を解決[#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="c2733-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="c2733-127">障害が発生した検索のプロジェクトで update コマンドの場合に表示される例外[#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="c2733-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="c2733-128">引数でフィードから nuget v3.3 以降、パッケージをインストールするときにパッケージのコンテンツは正しく復元されません、パッケージが含まれている場合 - NoCache`.nupkg`ファイル - [#2354](https://github.com/NuGet/Home/issues/2354)</span><span class="sxs-lookup"><span data-stu-id="c2733-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="c2733-129">パッケージに問題を修正プログラムが - 1 つのソースからパッケージが見つからない場合に、(すべてのソース) をインストール[#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="c2733-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="c2733-130">1 つのソース - 承認に失敗した場合は、ブロックをインストール[#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="c2733-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="c2733-131">`.nuspec` バージョン範囲は-IncludeReferencedProjects バージョン - をオーバーライドする必要があります[#1983](https://github.com/NuGet/Home/issues/1983)</span><span class="sxs-lookup"><span data-stu-id="c2733-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="c2733-132">NuGet 3.3.0 更新が失敗 '... 制約で定義されている packages.config には、この動作ができなくなります '。</span><span class="sxs-lookup"><span data-stu-id="c2733-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="c2733-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="c2733-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="c2733-134">nuget.exe の更新プログラムは、アセンブリの厳密な名前とプライベートの属性を削除します。</span><span class="sxs-lookup"><span data-stu-id="c2733-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="c2733-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="c2733-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="c2733-136">"DefaultPushSource"- の相対ファイル パスの問題が修正[#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="c2733-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="c2733-137">更新競合回避モジュールのエラー メッセージの改善[#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="c2733-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="c2733-138">機能および動作変更</span><span class="sxs-lookup"><span data-stu-id="c2733-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="c2733-139">nuget.exe プッシュのタイムアウト パラメーターは機能しません - [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="c2733-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="c2733-140">nuget.exe の復元を生成しない`.props`と`.targets`ファイル`.nuproj`プロジェクト (v3.4.3.855 の回帰) - [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="c2733-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="c2733-141">機能拡張 API フレームワークの imports とを比較する必要がある[#2633](https://github.com/NuGet/Home/issues/2633)</span><span class="sxs-lookup"><span data-stu-id="c2733-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="c2733-142">使用する場合は、依存関係のオプションを非表示に`project.json`  -  [#2486](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="c2733-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="c2733-143">詳細な出力 - で nuget.exe のバージョン ヘッダーを印刷[#1887](https://github.com/NuGet/Home/issues/1887)</span><span class="sxs-lookup"><span data-stu-id="c2733-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="c2733-144">NuGet は、{rid}/runtimes//nativeassets/{txm} のサポートを追加する必要があります、- [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="c2733-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>