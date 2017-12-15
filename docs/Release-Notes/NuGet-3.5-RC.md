---
title: "3.5 RC のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 75a9b496-5762-48b6-922f-fdddf1369c45
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.5 RC のリリース ノートします。"
keywords: "NuGet 3.5 RC のリリース ノート、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 09d566de6f53bc0f0ddd8049143dc647f3075671
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
#<a name="35-rc-release-notes"></a><span data-ttu-id="6628a-104">3.5 RC のリリース ノート</span><span class="sxs-lookup"><span data-stu-id="6628a-104">3.5 RC Release Notes</span></span>

<span data-ttu-id="6628a-105">[NuGet 3.5 Beta2 リリース ノート](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM リリース ノート](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="6628a-105">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="6628a-106">3.5 インチのリリースは NuGet クライアントの品質および性能を向上させることに重点を置きます。</span><span class="sxs-lookup"><span data-stu-id="6628a-106">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="6628a-107">さらにのサポートなど、いくつかの機能が出荷された[フォールバック フォルダー](https://github.com/NuGet/Home/issues/2899)、 [PackageType](https://github.com/NuGet/Home/issues/2476)でサポート`.nuspec`などです。</span><span class="sxs-lookup"><span data-stu-id="6628a-107">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="6628a-108">懸案事項の一覧</span><span class="sxs-lookup"><span data-stu-id="6628a-108">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5 RC")

## <a name="bug-fixes"></a><span data-ttu-id="6628a-109">バグ修正</span><span class="sxs-lookup"><span data-stu-id="6628a-109">Bug Fixes</span></span>

* <span data-ttu-id="6628a-110">パッケージのインストール/復元が失敗"パッケージが複数含まれている`.nuspec`ファイルです"。</span><span class="sxs-lookup"><span data-stu-id="6628a-110">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="6628a-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="6628a-111"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="6628a-112">nuget パックを強制的に追加`.tt`ファイルをコンテンツ フォルダーの内容に関係なく[#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="6628a-112">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="6628a-113">nuget パック csproj (で`project.json`) packOptions と JSON ファイルの所有者が存在しない場合のクラッシュ[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="6628a-113">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="6628a-114">用の nuget パック`project.json`概要、作成者、所有者などのような packOptions タグは無視[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="6628a-114">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="6628a-115">出力内の依存関係が nuget パックには無視されます`.nuspec`の`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="6628a-115">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="6628a-116">ロールバックを含む複数のパッケージの更新結果が、プロジェクト、破損状態 - [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="6628a-116">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="6628a-117">Netstandard プロジェクトのいずれかの下にあるコンテンツ ファイルは追加されません[#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="6628a-117">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="6628a-118">ターゲットを .Net ライブラリをパッケージすることはできません標準正しく - [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="6628a-118">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="6628a-119">ファイルに新しいプロジェクト]-> [クラス ライブラリ (ポータブル) プロジェクトが失敗する VS2015 と Dev15 - -> [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="6628a-119">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="6628a-120">NuGet エラー - 1.0.0-* は有効なバージョン文字列ではありません[#3070。](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="6628a-120">NuGet error - 1.0.0-* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="6628a-121">表示、パッケージのインストールの動作の失敗した Find-package [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="6628a-121">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="6628a-122">エラー時"Install-package jquery.validation"dev15 -  [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="6628a-122">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="6628a-123">VS 2015 がインストールされているバージョン 3.5.0 エラーが発生した、NuGet を使用すると上の 3 を更新するときに[#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="6628a-123">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="6628a-124">パッケージ マネージャーの UI: パッケージを更新した後に新しいバージョンが表示されない- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="6628a-124">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="6628a-125">-ApiKey delete コマンド ラインでは、読み取り/に送信されない 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="6628a-125">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="6628a-126">不適切な文字列: 安定したパッケージのリリースのプレリリースの依存関係のないです。</span><span class="sxs-lookup"><span data-stu-id="6628a-126">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="6628a-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="6628a-127"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="6628a-128">PCL (net46 および windows 10) プロジェクト get NullRef 例外を作成します。</span><span class="sxs-lookup"><span data-stu-id="6628a-128">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="6628a-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="6628a-129"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="6628a-130">AllowedVersions 制約 - によってより新しいバージョンが制限されているときに、Nuget の更新プログラムは情報メッセージを提供する必要があります[#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="6628a-130">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="6628a-131">資格情報のプラグインは、エラー-1 で終了しましたエラーをダウンロードする、複数のソースの資格情報プロバイダーを使用する場合にパッケージ化/ [#2885。](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="6628a-131">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="6628a-132">nuget パック パッケージ依存関係がありません Newtonsoft.Json - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="6628a-132">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="6628a-133">Linux/MacOS + モノラル - ExecuteSynchronizedCore でバグ[#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="6628a-133">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="6628a-134">VS が repositoryPath 内の環境変数をサポートしていません (nuget.exe は) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="6628a-134">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="6628a-135">ユーザー補助の問題を修正[#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="6628a-135">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="6628a-136">ハイフンでつながれたプロファイルでポータブル フレームワークは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="6628a-136">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="6628a-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="6628a-137"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="6628a-138">NuGet パッケージ マネージャーで、詳細には適用されませんパッケージでそのオプションの一覧を明確にするため必要があります`project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="6628a-138">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="6628a-139">NuGet 3.3.0 更新で失敗 ' 追加の制約 で定義されている packages.config には、この動作ができなくなります '。</span><span class="sxs-lookup"><span data-stu-id="6628a-139">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="6628a-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="6628a-140"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="6628a-141">無効なメッセージのスローを存在しないローカル ソースからパッケージをインストールする[#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="6628a-141">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="6628a-142">「アップグレード」使用できるフィルターは、表示のバージョンの制約に違反するアップグレード[#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="6628a-142">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="6628a-143">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="6628a-143">Performance Improvements</span></span>

* <span data-ttu-id="6628a-144">パフォーマンス: 向上 ContentModel ターゲット フレームワークの解析中に[#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="6628a-144">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="6628a-145">パフォーマンス: 読み取りを回避する`runtime.json`の Rid がない復元ファイル[#3150](https://github.com/NuGet/Home/issues/3150)です。</span><span class="sxs-lookup"><span data-stu-id="6628a-145">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="6628a-146">CI のマシンでは、ASP.NET Web アプリケーションが 3 秒を 15 秒以上削減サンプルの復元します。</span><span class="sxs-lookup"><span data-stu-id="6628a-146">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="6628a-147">パフォーマンス: パッケージ マネージャー コンソール init.ps1 読み込み時[#2956](https://github.com/NuGet/Home/issues/2956)です。</span><span class="sxs-lookup"><span data-stu-id="6628a-147">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="6628a-148">場合によっては 132s から 10 件に PackageManagerConsole を開くに時間が向上しました。</span><span class="sxs-lookup"><span data-stu-id="6628a-148">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="6628a-149">NuGet の更新プログラム - ReSharper パフォーマンスの問題を解決[#3044](https://github.com/NuGet/Home/issues/3044): サンプルのプロジェクトはパッケージをインストールするのにかかる時間が 140s から 68s に短縮します。</span><span class="sxs-lookup"><span data-stu-id="6628a-149">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="6628a-150">Dcr</span><span class="sxs-lookup"><span data-stu-id="6628a-150">DCRs</span></span>

* <span data-ttu-id="6628a-151">NuGet は、ユーザーがいるベース dotnet tfm でアップグレード/インストール PCL に問題が発生の通知する必要があります[#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="6628a-151">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="6628a-152">Tfm を使用したプロジェクトの不適切なインストールまたはアップグレードに警告する ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="6628a-152">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="6628a-153">Netcoreapp11 と netstandard17 サポート - 追加[#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="6628a-153">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="6628a-154">Nuget.exe - でコンソールに NuGet 警告ヘッダーの内容を印刷[#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="6628a-154">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="6628a-155">活用 AssemblyMetadata 属性`.nuspec`トークンの置換 - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="6628a-155">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="6628a-156">ロックされているプロパティ ファイルから削除、ロックの[#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="6628a-156">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="6628a-157">シンボル パッケージのインストールでこれまで使用しないでまたは #2807 の更新</span><span class="sxs-lookup"><span data-stu-id="6628a-157">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="6628a-158">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="6628a-158">Features</span></span>

* <span data-ttu-id="6628a-159">-フォールバック パッケージ フォルダーへのサポート[#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="6628a-159">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="6628a-160">設計およびツール パッケージをサポートするには、パッケージの種類の概念を実装[#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="6628a-160">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="6628a-161">グローバル パッケージ フォルダーへのパスを取得する API [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="6628a-161">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="6628a-162">ネイティブなパッケージ更新のサポート - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="6628a-162">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
