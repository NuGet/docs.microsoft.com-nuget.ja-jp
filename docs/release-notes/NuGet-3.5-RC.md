---
title: 3.5 RC リリースノート
description: 既知の問題、バグ修正、追加された機能、および DCRs を含む NuGet 3.5 RC のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 04ec402df5ff993b405bb710abf26e1cdc850703
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780206"
---
# <a name="nuget-35-rc-release-notes"></a><span data-ttu-id="a243e-103">NuGet 3.5 RC リリースノート</span><span class="sxs-lookup"><span data-stu-id="a243e-103">NuGet 3.5 RC Release Notes</span></span>

<span data-ttu-id="a243e-104">[NuGet 3.5-Beta2 リリースノート](../release-notes/nuget-3.5-Beta2.md)  | [NuGet 3.5-RTM リリースノート](../release-notes/nuget-3.5-RTM.md)</span><span class="sxs-lookup"><span data-stu-id="a243e-104">[NuGet 3.5-Beta2 Release Notes](../release-notes/nuget-3.5-Beta2.md) | [NuGet 3.5-RTM Release Notes](../release-notes/nuget-3.5-RTM.md)</span></span>

<span data-ttu-id="a243e-105">3.5 リリースは、NuGet クライアントの品質とパフォーマンスを向上させることに重点を置いています。</span><span class="sxs-lookup"><span data-stu-id="a243e-105">3.5 release is focused on improving quality and performance of NuGet clients.</span></span> <span data-ttu-id="a243e-106">さらに、 [フォールバックフォルダー](https://github.com/NuGet/Home/issues/2899)のサポート、およびでの [packagetype](https://github.com/NuGet/Home/issues/2476) のサポートなど、いくつかの機能を提供してい `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="a243e-106">In addition, we have shipped a few features like support for [Fallback folders](https://github.com/NuGet/Home/issues/2899), [PackageType](https://github.com/NuGet/Home/issues/2476) support in `.nuspec` and more.</span></span>

[<span data-ttu-id="a243e-107">懸案事項リスト</span><span class="sxs-lookup"><span data-stu-id="a243e-107">Issues List</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%223.5%20RC")

## <a name="bug-fixes"></a><span data-ttu-id="a243e-108">バグの修正</span><span class="sxs-lookup"><span data-stu-id="a243e-108">Bug Fixes</span></span>

* <span data-ttu-id="a243e-109">パッケージのインストール/復元が失敗し、"パッケージに複数のファイルが含まれています。" というエラーが表示さ `.nuspec` れます。</span><span class="sxs-lookup"><span data-stu-id="a243e-109">Install/restore of a package fails with "Package contains multiple `.nuspec` files."</span></span><span data-ttu-id="a243e-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span><span class="sxs-lookup"><span data-stu-id="a243e-110"> - [#3231](https://github.com/NuGet/Home/issues/3231)</span></span>

* <span data-ttu-id="a243e-111">nuget パック `.tt` は、 [#3203](https://github.com/NuGet/Home/issues/3203)に関係なく、ファイルをコンテンツフォルダーに強制的に追加します。</span><span class="sxs-lookup"><span data-stu-id="a243e-111">nuget pack forcefully adds `.tt` files to content folder no matter what - [#3203](https://github.com/NuGet/Home/issues/3203)</span></span>

* <span data-ttu-id="a243e-112">`project.json`JSON ファイル内に packOptions と owner がない場合[#3180](https://github.com/NuGet/Home/issues/3180) 、nuget pack .csproj (を含む) がクラッシュする</span><span class="sxs-lookup"><span data-stu-id="a243e-112">nuget pack csproj (with `project.json`) crashes if there are no packOptions and owner in JSON file - [#3180](https://github.com/NuGet/Home/issues/3180)</span></span>

* <span data-ttu-id="a243e-113">の nuget パックでは `project.json` 、summary、authors、owners などの packOptions タグが無視されます。 [#3161](https://github.com/NuGet/Home/issues/3161)</span><span class="sxs-lookup"><span data-stu-id="a243e-113">nuget pack for `project.json` ignores packOptions tags like summary, authors , owners etc - [#3161](https://github.com/NuGet/Home/issues/3161)</span></span>

* <span data-ttu-id="a243e-114">nuget パック `.nuspec` は `project.json`  -  [#3145](https://github.com/NuGet/Home/issues/3145)の出力の依存関係を無視します</span><span class="sxs-lookup"><span data-stu-id="a243e-114">nuget pack ignores dependencies in output `.nuspec` for `project.json` - [#3145](https://github.com/NuGet/Home/issues/3145)</span></span>

* <span data-ttu-id="a243e-115">ロールバックを使用して複数のパッケージを更新すると、プロジェクトが破損した状態のままになります- [#3139](https://github.com/NuGet/Home/issues/3139)</span><span class="sxs-lookup"><span data-stu-id="a243e-115">Updating multiple packages with rollback leaves the project in a broken state - [#3139](https://github.com/NuGet/Home/issues/3139)</span></span>

* <span data-ttu-id="a243e-116">Netstandard.library プロジェクトでは、ContentFiles は追加されません- [#3118](https://github.com/NuGet/Home/issues/3118)</span><span class="sxs-lookup"><span data-stu-id="a243e-116">ContentFiles under any are not added for netstandard projects - [#3118](https://github.com/NuGet/Home/issues/3118)</span></span>

* <span data-ttu-id="a243e-117">.Net Standard をターゲットとするライブラリをパッケージ化できません- [#3108](https://github.com/NuGet/Home/issues/3108)</span><span class="sxs-lookup"><span data-stu-id="a243e-117">Cannot package library targeting .Net Standard correctly - [#3108](https://github.com/NuGet/Home/issues/3108)</span></span>

* <span data-ttu-id="a243e-118">ファイル > 新しいプロジェクト-> クラスライブラリ (ポータブル) プロジェクトが VS2015 と[#3094](https://github.com/NuGet/Home/issues/3094) Dev15 で失敗する</span><span class="sxs-lookup"><span data-stu-id="a243e-118">File -> New Project -> Class Library (Portable) project fails in VS2015 and Dev15 - [#3094](https://github.com/NuGet/Home/issues/3094)</span></span>

* <span data-ttu-id="a243e-119">NuGet エラー-1.0.0-\* は有効なバージョン文字列ではありません- [#3070](https://github.com/NuGet/Home/issues/3070)</span><span class="sxs-lookup"><span data-stu-id="a243e-119">NuGet error - 1.0.0-\* is not a valid version string - [#3070](https://github.com/NuGet/Home/issues/3070)</span></span>

* <span data-ttu-id="a243e-120">Find-Package を表示できませんが、Install-Package 動作 [#3068](https://github.com/NuGet/Home/issues/3068)</span><span class="sxs-lookup"><span data-stu-id="a243e-120">Find-Package fails to display but Install-Package works - [#3068](https://github.com/NuGet/Home/issues/3068)</span></span>

* <span data-ttu-id="a243e-121">Dev15 で "パッケージのインストール-検証" を行うとエラー [#3061](https://github.com/NuGet/Home/issues/3061)が発生する</span><span class="sxs-lookup"><span data-stu-id="a243e-121">Error when "Install-Package jquery.validation" on dev15 - [#3061](https://github.com/NuGet/Home/issues/3061)</span></span>

* <span data-ttu-id="a243e-122">NuGet バージョンを使用する VS で VS 2015 update 3 をインストールすると3.5.0 エラーが発生する- [#3053](https://github.com/NuGet/Home/issues/3053)</span><span class="sxs-lookup"><span data-stu-id="a243e-122">When installed VS 2015 update 3 on a VS that uses NuGet version 3.5.0 error occurs - [#3053](https://github.com/NuGet/Home/issues/3053)</span></span>

* <span data-ttu-id="a243e-123">パッケージマネージャー UI: パッケージを更新した後、新しいバージョンは表示されません- [#3041](https://github.com/NuGet/Home/issues/3041)</span><span class="sxs-lookup"><span data-stu-id="a243e-123">Package manager UI: Doesn't display new version after updating a package - [#3041](https://github.com/NuGet/Home/issues/3041)</span></span>

* <span data-ttu-id="a243e-124">-Delete コマンドラインの ApiKey は3.5.0 で読み取り/送信されません- [#3037](https://github.com/NuGet/Home/issues/3037)</span><span class="sxs-lookup"><span data-stu-id="a243e-124">-ApiKey on delete command line is not read/sent in 3.5.0-beta - [#3037](https://github.com/NuGet/Home/issues/3037)</span></span>

* <span data-ttu-id="a243e-125">文字列が正しくありません: パッケージの安定したリリースでは、プレリリースの依存関係を設定することはできません。</span><span class="sxs-lookup"><span data-stu-id="a243e-125">Incorrect string: A stable release of a package should not have on a prerelease dependency.</span></span><span data-ttu-id="a243e-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span><span class="sxs-lookup"><span data-stu-id="a243e-126"> - [#3030](https://github.com/NuGet/Home/issues/3030)</span></span>

* <span data-ttu-id="a243e-127">PCL (net46 および windows 10) プロジェクトを作成すると、NullRef 例外が生成されます。</span><span class="sxs-lookup"><span data-stu-id="a243e-127">Creating PCL (net46 and windows 10) project get NullRef exception.</span></span><span data-ttu-id="a243e-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span><span class="sxs-lookup"><span data-stu-id="a243e-128"> - [#3014](https://github.com/NuGet/Home/issues/3014)</span></span>

* <span data-ttu-id="a243e-129">新しいバージョンが allowedVersions 制約によって制限されている場合、Nuget 更新プログラムは情報メッセージを提供する必要があり [#3013](https://github.com/NuGet/Home/issues/3013)</span><span class="sxs-lookup"><span data-stu-id="a243e-129">Nuget update should provide informative message when a higher version is restricted by allowedVersions constraint - [#3013](https://github.com/NuGet/Home/issues/3013)</span></span>

* <span data-ttu-id="a243e-130">複数の[#2885](https://github.com/NuGet/Home/issues/2885)ソースで資格情報プロバイダーを使用しているときに、資格情報プラグインがエラーで終了しました-1/エラーが発生したパッケージのダウンロード中</span><span class="sxs-lookup"><span data-stu-id="a243e-130">Credential plugin exited with error -1 / error downloading package when using credential providers with multiple sources - [#2885](https://github.com/NuGet/Home/issues/2885)</span></span>

* <span data-ttu-id="a243e-131">nuget pack-パッケージの依存関係に Newtonsoft.Jsがありません- [#2876](https://github.com/NuGet/Home/issues/2876)</span><span class="sxs-lookup"><span data-stu-id="a243e-131">nuget pack - Missing Newtonsoft.Json package dependency - [#2876](https://github.com/NuGet/Home/issues/2876)</span></span>

* <span data-ttu-id="a243e-132">Linux/MacOS + Mono [#2860](https://github.com/NuGet/Home/issues/2860)での ExecuteSynchronizedCore のバグ</span><span class="sxs-lookup"><span data-stu-id="a243e-132">Bug in ExecuteSynchronizedCore on Linux/MacOS + Mono - [#2860](https://github.com/NuGet/Home/issues/2860)</span></span>

* <span data-ttu-id="a243e-133">VS は repositoryPath の環境変数をサポートしていません (nuget.exe)- [#2763](https://github.com/NuGet/Home/issues/2763)</span><span class="sxs-lookup"><span data-stu-id="a243e-133">VS doesn't support environment variables in repositoryPath (nuget.exe does) - [#2763](https://github.com/NuGet/Home/issues/2763)</span></span>

* <span data-ttu-id="a243e-134">アクセシビリティの問題を修正する- [#2745](https://github.com/NuGet/Home/issues/2745)</span><span class="sxs-lookup"><span data-stu-id="a243e-134">Fix Accessibility Issues - [#2745](https://github.com/NuGet/Home/issues/2745)</span></span>

* <span data-ttu-id="a243e-135">ハイフネーションされたプロファイルを含むポータブルフレームワークは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="a243e-135">Portable frameworks with hyphenated profiles are rejected.</span></span><span data-ttu-id="a243e-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span><span class="sxs-lookup"><span data-stu-id="a243e-136"> - [#2734](https://github.com/NuGet/Home/issues/2734)</span></span>

* <span data-ttu-id="a243e-137">NuGet パッケージマネージャーは、[パッケージの詳細] のオプション一覧が適用されないことを明確にする必要があり `project.json`  -  [#2665](https://github.com/NuGet/Home/issues/2665)</span><span class="sxs-lookup"><span data-stu-id="a243e-137">NuGet package manager should make it clear that options list in packages detail does not apply to `project.json` - [#2665](https://github.com/NuGet/Home/issues/2665)</span></span>

* <span data-ttu-id="a243e-138">NuGet 3.3.0 の更新が ' 追加の制約で失敗しました...packages.config で定義されているため、この操作を実行できません。 '</span><span class="sxs-lookup"><span data-stu-id="a243e-138">NuGet 3.3.0 update fails with 'An additional constraint ... defined in packages.config prevents this operation.'</span></span><span data-ttu-id="a243e-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span><span class="sxs-lookup"><span data-stu-id="a243e-139"> - [#1816](https://github.com/NuGet/Home/issues/1816)</span></span>

* <span data-ttu-id="a243e-140">存在しないローカルソースからパッケージをインストールすると、偽のメッセージ[#1674](https://github.com/NuGet/Home/issues/1674)がスローされる</span><span class="sxs-lookup"><span data-stu-id="a243e-140">Installing package from a local source that doesn't exist throws a bogus message - [#1674](https://github.com/NuGet/Home/issues/1674)</span></span>

* <span data-ttu-id="a243e-141">"Upgrade v)" フィルターに[#1094](https://github.com/NuGet/Home/issues/1094)より、バージョンの制約に違反するアップグレードが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a243e-141">"Upgrade vailable" filter shows upgrades that violate the version constraint - [#1094](https://github.com/NuGet/Home/issues/1094)</span></span>

## <a name="performance-improvements"></a><span data-ttu-id="a243e-142">パフォーマンスの強化</span><span class="sxs-lookup"><span data-stu-id="a243e-142">Performance Improvements</span></span>

* <span data-ttu-id="a243e-143">パフォーマンス: ContentModel ターゲットフレームワークの解析の向上- [#3162](https://github.com/NuGet/Home/issues/3162)</span><span class="sxs-lookup"><span data-stu-id="a243e-143">Performance: Improve ContentModel target framework parsing - [#3162](https://github.com/NuGet/Home/issues/3162)</span></span>

* <span data-ttu-id="a243e-144">パフォーマンス: `runtime.json` rid [#3150](https://github.com/NuGet/Home/issues/3150)を持たない復元用のファイルを読み取らないようにします。</span><span class="sxs-lookup"><span data-stu-id="a243e-144">Performance: Avoid reading `runtime.json` files for restores that do not have RIDs [#3150](https://github.com/NuGet/Home/issues/3150).</span></span> <span data-ttu-id="a243e-145">CI マシンでは、サンプル ASP.NET Web アプリケーションの復元が15秒から3秒に短縮されました。</span><span class="sxs-lookup"><span data-stu-id="a243e-145">On CI machines, restore of a sample ASP.NET Web Application reduced from over 15 secs to 3 secs.</span></span>

* <span data-ttu-id="a243e-146">パフォーマンス: パッケージマネージャーコンソール init.ps1 読み込み時間 [#2956](https://github.com/NuGet/Home/issues/2956)です。</span><span class="sxs-lookup"><span data-stu-id="a243e-146">Performance: Package Manager Console init.ps1 load time [#2956](https://github.com/NuGet/Home/issues/2956).</span></span> <span data-ttu-id="a243e-147">場合によっては、132s から 10 PackageManagerConsole までの時間が短縮されます。</span><span class="sxs-lookup"><span data-stu-id="a243e-147">Time to open PackageManagerConsole improved in some cases from 132s to 10s.</span></span>

* <span data-ttu-id="a243e-148">NuGet 更新プログラム [#3044](https://github.com/NuGet/Home/issues/3044)でのパフォーマンスに関する問題の解決: サンプルプロジェクトでは、パッケージのインストールに要した時間が14秒から1分に短縮されました。</span><span class="sxs-lookup"><span data-stu-id="a243e-148">Solve ReSharper performance issues in NuGet Update - [#3044](https://github.com/NuGet/Home/issues/3044): On a sample project, time taken to install packages reduced from 140s to 68s.</span></span>

## <a name="dcrs"></a><span data-ttu-id="a243e-149">DCR</span><span class="sxs-lookup"><span data-stu-id="a243e-149">DCRs</span></span>

* <span data-ttu-id="a243e-150">NuGet では、dotnet tfm ベースの PCL でのアップグレードまたはインストールによって問題が発生する可能性があることをユーザーに知らせる必要があり [#3138](https://github.com/NuGet/Home/issues/3138)</span><span class="sxs-lookup"><span data-stu-id="a243e-150">NuGet needs to let users know that upgrading/installing in a dotnet tfm based PCL could cause issues - [#3138](https://github.com/NuGet/Home/issues/3138)</span></span>

* <span data-ttu-id="a243e-151">[プロジェクトに対して無効なインストール/アップグレードを警告する]: "dotnet"- [#3137](https://github.com/NuGet/Home/issues/3137)</span><span class="sxs-lookup"><span data-stu-id="a243e-151">Warn bad install/upgrade for project w/ tfm="dotnet" - [#3137](https://github.com/NuGet/Home/issues/3137)</span></span>

* <span data-ttu-id="a243e-152">Netcoreapp11 と netstandard17 のサポートを追加する- [#2998](https://github.com/NuGet/Home/issues/2998)</span><span class="sxs-lookup"><span data-stu-id="a243e-152">Add netcoreapp11 and netstandard17 support - [#2998](https://github.com/NuGet/Home/issues/2998)</span></span>

* <span data-ttu-id="a243e-153">nuget.exe [#2934](https://github.com/NuGet/Home/issues/2934)で NuGet-Warning ヘッダーの内容をコンソールに出力する</span><span class="sxs-lookup"><span data-stu-id="a243e-153">Print NuGet-Warning header contents to console in nuget.exe - [#2934](https://github.com/NuGet/Home/issues/2934)</span></span>

* <span data-ttu-id="a243e-154">トークンの置換に AssemblyMetadata 属性を利用する `.nuspec` - [#2851](https://github.com/NuGet/Home/issues/2851)</span><span class="sxs-lookup"><span data-stu-id="a243e-154">Leverage AssemblyMetadata attribute for `.nuspec` token replacements - [#2851](https://github.com/NuGet/Home/issues/2851)</span></span>

* <span data-ttu-id="a243e-155">ロックファイルからロックされたプロパティを削除し [#2379](https://github.com/NuGet/Home/issues/2379)</span><span class="sxs-lookup"><span data-stu-id="a243e-155">Remove the locked property from the lock file - [#2379](https://github.com/NuGet/Home/issues/2379)</span></span>

* <span data-ttu-id="a243e-156">シンボルパッケージは、インストールまたは更新では使用しないでください #2807</span><span class="sxs-lookup"><span data-stu-id="a243e-156">Symbol packages should not ever be used in install or update #2807</span></span>

## <a name="features"></a><span data-ttu-id="a243e-157">特徴</span><span class="sxs-lookup"><span data-stu-id="a243e-157">Features</span></span>

* <span data-ttu-id="a243e-158">フォールバックパッケージフォルダーのサポート- [#2899](https://github.com/NuGet/Home/issues/2899)</span><span class="sxs-lookup"><span data-stu-id="a243e-158">Support for fallback package folders - [#2899](https://github.com/NuGet/Home/issues/2899)</span></span>

* <span data-ttu-id="a243e-159">ツールパッケージをサポートするためのパッケージの種類の概念を設計および実装する- [#2476](https://github.com/NuGet/Home/issues/2476)</span><span class="sxs-lookup"><span data-stu-id="a243e-159">Design and implement a notion of package type to support tool packages - [#2476](https://github.com/NuGet/Home/issues/2476)</span></span>

* <span data-ttu-id="a243e-160">グローバルパッケージフォルダーへのパスを取得するための API- [#2403](https://github.com/NuGet/Home/issues/2403)</span><span class="sxs-lookup"><span data-stu-id="a243e-160">API to get the path to the global packages folder - [#2403](https://github.com/NuGet/Home/issues/2403)</span></span>

* <span data-ttu-id="a243e-161">ネイティブパッケージの更新サポート- [#1291](https://github.com/NuGet/Home/issues/1291)</span><span class="sxs-lookup"><span data-stu-id="a243e-161">Native packages update support - [#1291](https://github.com/NuGet/Home/issues/1291)</span></span>
