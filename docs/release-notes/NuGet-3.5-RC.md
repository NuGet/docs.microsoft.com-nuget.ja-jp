---
title: 3.5 RC リリース ノート
description: 既知の問題、バグの修正、追加機能、および Dcr を含む NuGet 3.5 RC のリリース ノート。
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 52c443ecd79c9108203f5a3c327078ce9e28b95b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548539"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="ef0af-103">NuGet 3.5 RC リリース ノートします。</span><span class="sxs-lookup"><span data-stu-id="ef0af-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="ef0af-104">[NuGet 3.5 beta 2 リリース ノート](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM リリース ノート](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="ef0af-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="ef0af-105">3.5 のリリースは NuGet クライアントの品質およびパフォーマンスの向上に重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="ef0af-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="ef0af-106">さらになどのサポートのいくつかの機能が出荷された[Fallback フォルダー](https://github.com/NuGet/Home/issues/2899)、 [PackageType](https://github.com/NuGet/Home/issues/2476)サポート`.nuspec`など。</span><span class="sxs-lookup"><span data-stu-id="ef0af-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="ef0af-107">懸案事項リスト</span><span class="sxs-lookup"><span data-stu-id="ef0af-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="ef0af-108">バグ修正</span><span class="sxs-lookup"><span data-stu-id="ef0af-108">Bug Fixes</span></span>

* <span data-ttu-id="ef0af-109">パッケージのインストール/復元が失敗した"パッケージが複数含まれている`.nuspec`ファイル"。</span><span class="sxs-lookup"><span data-stu-id="ef0af-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="ef0af-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="ef0af-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="ef0af-111">nuget パックを強制的に追加します`.tt`- 何であってもコンテンツのフォルダーにファイルを[#3203](https://github.com/NuGet/Home/issues/3203)</span><span class="sxs-lookup"><span data-stu-id="ef0af-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="ef0af-112">nuget パック csproj (で`project.json`) packOptions と JSON ファイルの所有者がない場合のクラッシュ[#3180](https://github.com/NuGet/Home/issues/3180)</span><span class="sxs-lookup"><span data-stu-id="ef0af-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="ef0af-113">用の nuget パック`project.json`概要、作成者、所有者などのような packOptions タグは無視[#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="ef0af-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="ef0af-114">出力内の依存関係を無視する nuget の pack`.nuspec`の`project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)</span><span class="sxs-lookup"><span data-stu-id="ef0af-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="ef0af-115">プロジェクトの破損した状態のままロールバックを含む複数のパッケージを更新[#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="ef0af-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="ef0af-116">いずれかの ContentFiles は netstandard プロジェクトには追加されません[#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="ef0af-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="ef0af-117">.Net をターゲットとするライブラリをパッケージ化できません標準- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="ef0af-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="ef0af-118">ファイルに新しいプロジェクト]-> [VS2015 で Dev15 - クラス ライブラリ (ポータブル) プロジェクトの失敗]-> [ [#3094](https://github.com/NuGet/Home/issues/3094)</span><span class="sxs-lookup"><span data-stu-id="ef0af-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="ef0af-119">NuGet エラー - 1.0.0-\* が有効なバージョン文字列のではない[#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="ef0af-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="ef0af-120">表示が、インストール パッケージの機能の検索パッケージが失敗する[#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="ef0af-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="ef0af-121">エラー時に - dev15 で"Install-package jquery.validation" [#3061](https://github.com/NuGet/Home/issues/3061)</span><span class="sxs-lookup"><span data-stu-id="ef0af-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="ef0af-122">VS 2015 がインストールされている 3 バージョン 3.5.0 のエラーが発生した、NuGet を使用して VS を更新するときに[#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="ef0af-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="ef0af-123">パッケージ マネージャー UI: パッケージの更新後に新しいバージョンが表示されません- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="ef0af-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="ef0af-124">-Apikey コマンド行の削除が読み取り/で送信されない 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="ef0af-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="ef0af-125">文字列が正しくありません。 プレリリースの依存関係のパッケージの安定したリリースはありません。</span><span class="sxs-lookup"><span data-stu-id="ef0af-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="ef0af-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="ef0af-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="ef0af-127">PCL (net46 および windows 10) プロジェクト get NullRef 例外を作成します。</span><span class="sxs-lookup"><span data-stu-id="ef0af-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="ef0af-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="ef0af-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="ef0af-129">AllowedVersions 制約 - によって新しいバージョンが制限されていると、Nuget の更新プログラムは情報メッセージを提供する必要があります[#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="ef0af-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="ef0af-130">資格情報プラグインが-1 のエラーで終了しました]、[複数のソースの資格情報プロバイダーを使用する場合にパッケージをダウンロード中にエラー [#2885](https://github.com/NuGet/Home/issues/2885)</span><span class="sxs-lookup"><span data-stu-id="ef0af-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="ef0af-131">nuget パック - 不足している Newtonsoft.Json パッケージの依存関係 - [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="ef0af-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="ef0af-132">ExecuteSynchronizedCore Linux/macos + - Mono 上でバグ[#2860](https://github.com/NuGet/Home/issues/2860)</span><span class="sxs-lookup"><span data-stu-id="ef0af-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="ef0af-133">VS が repositoryPath 内の環境変数をサポートしていません (nuget.exe が) - [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="ef0af-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="ef0af-134">アクセシビリティの問題を修正[#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="ef0af-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="ef0af-135">ハイフンでつながれたプロファイルを使用した移植可能なフレームワークは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="ef0af-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="ef0af-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="ef0af-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="ef0af-137">NuGet パッケージ マネージャーで、そのオプションの一覧でパッケージの詳細には適用されませんを明確にするため必要があります`project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="ef0af-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="ef0af-138">NuGet 3.3.0 更新が失敗 '... 制約で定義されている packages.config には、この動作ができなくなります '。</span><span class="sxs-lookup"><span data-stu-id="ef0af-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="ef0af-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="ef0af-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="ef0af-140">無効なメッセージがスローされますが存在しないローカル ソースからパッケージをインストールする[#1674](https://github.com/NuGet/Home/issues/1674)</span><span class="sxs-lookup"><span data-stu-id="ef0af-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="ef0af-141">「少ないアップグレード」フィルターはバージョン制約に違反するアップグレードでは、表示[#1094](https://github.com/NuGet/Home/issues/1094)</span><span class="sxs-lookup"><span data-stu-id="ef0af-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="ef0af-142">パフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="ef0af-142">Performance Improvements</span></span>

* <span data-ttu-id="ef0af-143">: パフォーマンス contentmodel はターゲット フレームワークの解析のを向上させる[#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="ef0af-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="ef0af-144">パフォーマンス: 読み取りを回避する`runtime.json`の Rid がない復元ファイル[#3150](https://github.com/NuGet/Home/issues/3150)します。</span><span class="sxs-lookup"><span data-stu-id="ef0af-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="ef0af-145">CI マシンでの ASP.NET Web アプリケーションが 3 秒を 15 秒から短縮サンプルを復元します。</span><span class="sxs-lookup"><span data-stu-id="ef0af-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="ef0af-146">パフォーマンス: パッケージ マネージャー コンソール init.ps1 読み込み時間[#2956](https://github.com/NuGet/Home/issues/2956)します。</span><span class="sxs-lookup"><span data-stu-id="ef0af-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="ef0af-147">よって 132s から 10 件に PackageManagerConsole を開こうとする時間が向上しました。</span><span class="sxs-lookup"><span data-stu-id="ef0af-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="ef0af-148">NuGet の更新 - ReSharper パフォーマンスの問題を解決[#3044](https://github.com/NuGet/Home/issues/3044): サンプル プロジェクトはパッケージのインストールにかかる時間が 140s から 68s に縮小します。</span><span class="sxs-lookup"><span data-stu-id="ef0af-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="ef0af-149">DCR</span><span class="sxs-lookup"><span data-stu-id="ef0af-149">DCRs</span></span>

* <span data-ttu-id="ef0af-150">NuGet は、ベース dotnet tfm でアップグレード/インストール PCL の問題が生じたり - ユーザーに通知する必要があります[#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="ef0af-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="ef0af-151">Tfm を使用したプロジェクトの不適切なインストールまたはアップグレードを警告する ="dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="ef0af-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="ef0af-152">追加 netcoreapp11 と netstandard17 サポート - [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="ef0af-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="ef0af-153">Nuget.exe - で、コンソールへの NuGet 警告ヘッダーの内容を印刷[#2934](https://github.com/NuGet/Home/issues/2934)</span><span class="sxs-lookup"><span data-stu-id="ef0af-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="ef0af-154">利用して AssemblyMetadata 属性`.nuspec`トークンの置換 - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="ef0af-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="ef0af-155">ロックされているプロパティはロック ファイルから削除[#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="ef0af-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="ef0af-156">シンボル パッケージはこれまで使用できませんのインストールまたは #2807 の更新</span><span class="sxs-lookup"><span data-stu-id="ef0af-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="ef0af-157">フィーチャー</span><span class="sxs-lookup"><span data-stu-id="ef0af-157">Features</span></span>

* <span data-ttu-id="ef0af-158">フォールバックのパッケージ フォルダー - サポート[#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="ef0af-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="ef0af-159">設計および実装ツール パッケージをサポートするには、パッケージの種類の概念[#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="ef0af-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="ef0af-160">API へのグローバル パッケージ フォルダーのパスを取得する[#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="ef0af-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="ef0af-161">ネイティブ パッケージの更新のサポート - [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="ef0af-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
