---
title: 3.5 Beta2 のリリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.5 Beta 2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 2aa92d4ef97acb2b4b70388cd4d580e7094aea45
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776387"
---
# <a name="nuget-35-beta2-release-notes"></a><span data-ttu-id="7a5f9-103">NuGet 3.5 Beta2 のリリースノート</span><span class="sxs-lookup"><span data-stu-id="7a5f9-103">NuGet 3.5 Beta2 Release Notes</span></span>

<span data-ttu-id="7a5f9-104">[NuGet 3.5-ベータリリースノート](../release-notes/nuget-3.5-Beta.md)  | [NuGet 3.5-RC リリースノート](../release-notes/nuget-3.5-RC.md)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-104">[NuGet 3.5-Beta Release Notes](../release-notes/nuget-3.5-Beta.md) | [NuGet 3.5-RC Release Notes](../release-notes/nuget-3.5-RC.md)</span></span>

<span data-ttu-id="7a5f9-105">NuGet 3.5 Beta 2 RTM は、Visual Studio 2013 と nuget.exe に2016年6月27日にリリースされました</span><span class="sxs-lookup"><span data-stu-id="7a5f9-105">NuGet 3.5 Beta 2 RTM was released June 27, 2016 for Visual Studio 2013 and nuget.exe</span></span>

[<span data-ttu-id="7a5f9-106">完全な Changelog</span><span class="sxs-lookup"><span data-stu-id="7a5f9-106">Full Changelog</span></span>](https://github.com/NuGet/NuGet.Client/compare/release-3.5.0-beta...release-3.5.0-beta2)

[<span data-ttu-id="7a5f9-107">懸案事項リスト</span><span class="sxs-lookup"><span data-stu-id="7a5f9-107">Issues List</span></span>](https://github.com/Nuget/Home/issues?q=is%3Aissue+milestone%3A%223.5+Beta2%22+is%3Aclosed)

## <a name="bug-fixes"></a><span data-ttu-id="7a5f9-108">バグの修正</span><span class="sxs-lookup"><span data-stu-id="7a5f9-108">Bug Fixes</span></span>

* <span data-ttu-id="7a5f9-109">認証されたフィード用の .NET Core でのパスワード decrpytion のサポート不足に関するエラーメッセージを更新しました- [#2942](https://github.com/NuGet/Home/issues/2942)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-109">Updated error message to lack of support for password decrpytion in .NET Core for authenticated feeds  - [#2942](https://github.com/NuGet/Home/issues/2942)</span></span>

* <span data-ttu-id="7a5f9-110">.NET Core プロジェクトが開いている場合、パッケージマネージャーコンソール Get-Package が失敗する [#2932](https://github.com/NuGet/Home/issues/2932)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-110">Package Manager Console Get-Package fails if .NET Core project is open - [#2932](https://github.com/NuGet/Home/issues/2932)</span></span>

* <span data-ttu-id="7a5f9-111">NuGet push コマンドでの403の不適切な処理を修正し [#2910](https://github.com/NuGet/Home/issues/2910)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-111">Fix incorrect handling of 403 in NuGet push command [#2910](https://github.com/NuGet/Home/issues/2910)</span></span>

* <span data-ttu-id="7a5f9-112">DisableSourceControlIntegration が true に設定されている場合に TFS ソース管理にバインドされているソリューションでのパッケージのアンインストールに関する問題を修正しました- [#2739](https://github.com/NuGet/Home/issues/2739)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-112">Fix issues in uninstalling packages in a solution bound to TFS source control when disableSourceControlIntegration is set to true - [#2739](https://github.com/NuGet/Home/issues/2739)</span></span>

* <span data-ttu-id="7a5f9-113">対象外のパッケージを考慮するようにパッケージの更新を修正する- [#2724](https://github.com/NuGet/Home/issues/2724)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-113">Fix package update to take into account non-target packages - [#2724](https://github.com/NuGet/Home/issues/2724)</span></span>

* <span data-ttu-id="7a5f9-114">MSBuild の詳細レベルを使用して Nuget パッケージマネージャーの UI 操作のロガーレベルを設定する- [#2705](https://github.com/NuGet/Home/issues/2705)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-114">Use MSBuild verbosity level to set logger level for Nuget package manager UI actions - [#2705](https://github.com/NuGet/Home/issues/2705)</span></span>

* <span data-ttu-id="7a5f9-115">Web サイトプロジェクトの NuGet 構成が無効であることを修正するエラー-VS 2015 VSIX (v 3.4.3)- [#2667](https://github.com/NuGet/Home/issues/2667)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-115">Fix NuGet configuration is invalid error in WebSite projects - VS 2015 VSIX (v3.4.3) - [#2667](https://github.com/NuGet/Home/issues/2667)</span></span>

* <span data-ttu-id="7a5f9-116">コンテンツファイルが含まれている場合のパックの問題を修正 `.csproj` する- [#2658](https://github.com/NuGet/Home/issues/2658)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-116">Fix pack issues from `.csproj` when content files are included - [#2658](https://github.com/NuGet/Home/issues/2658)</span></span>

* <span data-ttu-id="7a5f9-117">() の DefaultPushSource `NuGetDefaults.Config` `ProgramData\NuGet` が動作しません [#2653](https://github.com/NuGet/Home/issues/2653)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-117">DefaultPushSource in `NuGetDefaults.Config` (`ProgramData\NuGet`) doesn't work - [#2653](https://github.com/NuGet/Home/issues/2653)</span></span>

* <span data-ttu-id="7a5f9-118">Nuget 3.4.3 のリリースで問題を修正する-パッケージの作成時に値を null にすることはできません- [#2648](https://github.com/NuGet/Home/issues/2648)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-118">Fix issue in Nuget 3.4.3 release - Value cannot be null on package creation - [#2648](https://github.com/NuGet/Home/issues/2648)</span></span>

* <span data-ttu-id="7a5f9-119">復元では、VSTS フィードの Nuget.Config から格納された資格情報を使用します。 [#2647](https://github.com/NuGet/Home/issues/2647)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-119">Restore uses stored credentials from Nuget.Config for VSTS feeds - [#2647](https://github.com/NuGet/Home/issues/2647)</span></span>

* <span data-ttu-id="7a5f9-120">パフォーマンス-バージョン comparsion で過剰な割り当てを修正するコード- [#2632](https://github.com/NuGet/Home/issues/2632)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-120">Performance - Fix excessive allocations in version comparsion code - [#2632](https://github.com/NuGet/Home/issues/2632)</span></span>

* <span data-ttu-id="7a5f9-121">nuget.exe の複数のインスタンスが並列[#2628](https://github.com/NuGet/Home/issues/2628)で同じパッケージをインストールしようとしたときに発生する問題を修正します。</span><span class="sxs-lookup"><span data-stu-id="7a5f9-121">Fix issues when multiple instances of nuget.exe tries to install the same package in parallel - [#2628](https://github.com/NuGet/Home/issues/2628)</span></span>

* <span data-ttu-id="7a5f9-122">パフォーマンス-複数プロジェクトの操作の依存関係情報をキャッシュする- [#2619](https://github.com/NuGet/Home/issues/2619)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-122">Performance - Cache dependency information for multi-project operations - [#2619](https://github.com/NuGet/Home/issues/2619)</span></span>

* <span data-ttu-id="7a5f9-123">ソースリストが空のときにパッケージソースを設定から追加できない問題を修正しました- [#2617](https://github.com/NuGet/Home/issues/2617)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-123">Fix issue where package sources cannnot be added from settings when source list is empty - [#2617](https://github.com/NuGet/Home/issues/2617)</span></span>

* <span data-ttu-id="7a5f9-124">デザイン時のファサードに依存するパッケージをインストールしようとすると[#2594](https://github.com/NuGet/Home/issues/2594) 、誤解を招くエラーを修正する</span><span class="sxs-lookup"><span data-stu-id="7a5f9-124">Fix Misleading error when attempting to install package that depends on design-time facades - [#2594](https://github.com/NuGet/Home/issues/2594)</span></span>

* <span data-ttu-id="7a5f9-125">"All" に設定して、パッケージを "All" に設定してパッケージをインストールすると、最初のソース[#2557](https://github.com/NuGet/Home/issues/2557)のみが試行される</span><span class="sxs-lookup"><span data-stu-id="7a5f9-125">Installing a package from PackageManager console with setting "All" tries only first source - [#2557](https://github.com/NuGet/Home/issues/2557)</span></span>

* <span data-ttu-id="7a5f9-126">将来 (Mono) で書き込み時間があるファイルを含むパッケージに関する問題を修正しました- [#2518](https://github.com/NuGet/Home/issues/2518)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-126">Fix issues with packages that have files with write times in the future (Mono) - [#2518](https://github.com/NuGet/Home/issues/2518)</span></span>

* <span data-ttu-id="7a5f9-127">Update コマンドでプロジェクトの検索エラーが発生したときに例外を表示する- [#2418](https://github.com/NuGet/Home/issues/2418)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-127">Display exception when there is a failure finding projects in update command - [#2418](https://github.com/NuGet/Home/issues/2418)</span></span>

* <span data-ttu-id="7a5f9-128">パッケージに `.nupkg` [#2354](https://github.com/NuGet/Home/issues/2354)ファイルが含まれている場合、NoCache という引数を使用して nuget v 3.3 + フィードからパッケージをインストールすると、パッケージコンテンツが正しく復元されない</span><span class="sxs-lookup"><span data-stu-id="7a5f9-128">Package content is not restored correctly when installing a package from a nuget v3.3+ feed with the argument -NoCache when the package contains `.nupkg` files - [#2354](https://github.com/NuGet/Home/issues/2354)</span></span>

* <span data-ttu-id="7a5f9-129">1つのソースからパッケージが欠落している場合に、パッケージのインストール (すべてのソース) の問題を修正しました。 [#2322](https://github.com/NuGet/Home/issues/2322)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-129">Fix issue with package install (All Sources) when package is missing from 1 source - [#2322](https://github.com/NuGet/Home/issues/2322)</span></span>

* <span data-ttu-id="7a5f9-130">1つのソースが承認に失敗した場合のインストールブロック- [#2034](https://github.com/NuGet/Home/issues/2034)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-130">Install blocks if a single source fails authorization - [#2034](https://github.com/NuGet/Home/issues/2034)</span></span>

* <span data-ttu-id="7a5f9-131">`.nuspec`バージョン範囲は IncludeReferencedProjects バージョン- [#1983](https://github.com/NuGet/Home/issues/1983)をオーバーライドする必要があります</span><span class="sxs-lookup"><span data-stu-id="7a5f9-131">`.nuspec` version range should override -IncludeReferencedProjects version - [#1983](https://github.com/NuGet/Home/issues/1983)</span></span>

* <span data-ttu-id="7a5f9-132">NuGet 3.3.0 の更新が ' 追加の制約で失敗しました...packages.config で定義されているため、この操作を実行できません。 '</span><span class="sxs-lookup"><span data-stu-id="7a5f9-132">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="7a5f9-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-133"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="7a5f9-134">nuget.exe の更新では、アセンブリの厳密な名前とプライベート属性が削除されます。</span><span class="sxs-lookup"><span data-stu-id="7a5f9-134">nuget.exe update drops the assembly strong name and Private attribute.</span></span><span data-ttu-id="7a5f9-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-135"> - [#1778](https://github.com/NuGet/Home/issues/1778)</span></span>

* <span data-ttu-id="7a5f9-136">"DefaultPushSource" の相対ファイルパスの問題を修正します- [#1746](https://github.com/NuGet/Home/issues/1746)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-136">Fix issues with relative file path for "DefaultPushSource" - [#1746](https://github.com/NuGet/Home/issues/1746)</span></span>

* <span data-ttu-id="7a5f9-137">更新リゾルバーのエラーメッセージの改善- [#1373](https://github.com/NuGet/Home/issues/1373)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-137">Improve Update resolver failure messages - [#1373](https://github.com/NuGet/Home/issues/1373)</span></span>

## <a name="features-and-behavior-changes"></a><span data-ttu-id="7a5f9-138">機能と動作の変更</span><span class="sxs-lookup"><span data-stu-id="7a5f9-138">Features and Behavior Changes</span></span>

* <span data-ttu-id="7a5f9-139">nuget.exe のプッシュタイムアウトパラメーターが機能しません- [#2785](https://github.com/NuGet/Home/issues/2785)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-139">nuget.exe push - timeout parameter doesn't work  - [#2785](https://github.com/NuGet/Home/issues/2785)</span></span>

* <span data-ttu-id="7a5f9-140">nuget.exe の復元で `.props` は、プロジェクトのファイルとファイルが生成されません `.targets` `.nuproj` (3.4.3.855 での回帰)- [#2711](https://github.com/NuGet/Home/issues/2711)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-140">nuget.exe restore doesn't produce `.props` and `.targets` files for `.nuproj` projects (regression in v3.4.3.855) - [#2711](https://github.com/NuGet/Home/issues/2711)</span></span>

* <span data-ttu-id="7a5f9-141">フレームワークとインポート[#2633](https://github.com/NuGet/Home/issues/2633)を比較するには、機能拡張 API が必要です</span><span class="sxs-lookup"><span data-stu-id="7a5f9-141">Need extensibility API to compare frameworks with imports - [#2633](https://github.com/NuGet/Home/issues/2633)</span></span>

* <span data-ttu-id="7a5f9-142">#2486 の使用時に依存関係オプションを非表示にする `project.json`  -  [](https://github.com/NuGet/Home/issues/2486)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-142">Hide dependency options when using `project.json` - [#2486](https://github.com/NuGet/Home/issues/2486)</span></span>

* <span data-ttu-id="7a5f9-143">詳細な出力[#1887](https://github.com/NuGet/Home/issues/1887)に nuget.exe バージョンヘッダーを出力する</span><span class="sxs-lookup"><span data-stu-id="7a5f9-143">Print out nuget.exe version header in detailed output - [#1887](https://github.com/NuGet/Home/issues/1887)</span></span>

* <span data-ttu-id="7a5f9-144">NuGet は/runtimes/{rid}/nativeassets/{txm}/のサポートを追加する必要があり [#2782](https://github.com/NuGet/Home/issues/2782)</span><span class="sxs-lookup"><span data-stu-id="7a5f9-144">NuGet should add support for /runtimes/{rid}/nativeassets/{txm}/ - [#2782](https://github.com/NuGet/Home/issues/2782)</span></span>