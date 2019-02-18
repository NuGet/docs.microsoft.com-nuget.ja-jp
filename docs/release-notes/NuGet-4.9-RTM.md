---
title: NuGet 4.9 RTM リリース ノート
description: NuGet 4.9 のリリース ノートです。既知の問題、バグ修正、新機能、および DCR について示します。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: aa9bf87504477506dbb1e9ac10d5c1d5841c224f
ms.sourcegitcommit: 885973352d31808e3ddbb45da6d6e54d1e4fca9d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/13/2019
ms.locfileid: "56224945"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="01785-103">NuGet 4.9 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="01785-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="01785-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="01785-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="01785-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="01785-105">NuGet version</span></span> | <span data-ttu-id="01785-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="01785-106">Available in Visual Studio version</span></span>| <span data-ttu-id="01785-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="01785-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="01785-108">**4.9.0**</span><span class="sxs-lookup"><span data-stu-id="01785-108">**4.9.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="01785-109">Visual Studio 2017 バージョン 15.9.0</span><span class="sxs-lookup"><span data-stu-id="01785-109">Visual Studio 2017 version 15.9.0</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="01785-110">2.1.500、2.2.100</span><span class="sxs-lookup"><span data-stu-id="01785-110">2.1.500, 2.2.100</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="01785-111">**4.9.1**</span><span class="sxs-lookup"><span data-stu-id="01785-111">**4.9.1**</span></span>](https://nuget.org/downloads) | <span data-ttu-id="01785-112">N/A</span><span class="sxs-lookup"><span data-stu-id="01785-112">n/a</span></span> | <span data-ttu-id="01785-113">N/A</span><span class="sxs-lookup"><span data-stu-id="01785-113">n/a</span></span> |
| [<span data-ttu-id="01785-114">**4.9.2**</span><span class="sxs-lookup"><span data-stu-id="01785-114">**4.9.2**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="01785-115">Visual Studio 2017 バージョン 15.9.4</span><span class="sxs-lookup"><span data-stu-id="01785-115">Visual Studio 2017 version 15.9.4</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="01785-116">2.1.502、2.2.101</span><span class="sxs-lookup"><span data-stu-id="01785-116">2.1.502, 2.2.101</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |
| [<span data-ttu-id="01785-117">**4.9.3**</span><span class="sxs-lookup"><span data-stu-id="01785-117">**4.9.3**</span></span>](https://nuget.org/downloads) |[<span data-ttu-id="01785-118">Visual Studio 2017 バージョン 15.9.6</span><span class="sxs-lookup"><span data-stu-id="01785-118">Visual Studio 2017 version 15.9.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="01785-119">2.1.504, 2.2.104</span><span class="sxs-lookup"><span data-stu-id="01785-119">2.1.504, 2.2.104</span></span>](https://www.microsoft.com/net/download/visual-studio-sdks) |


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="01785-120">概要:4.9.0 の新機能</span><span class="sxs-lookup"><span data-stu-id="01785-120">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="01785-121">署名: ClientPolicies において、NuGet.Config に記載されている信頼された作成者とリポジトリのセットの使用を要求することを可能にする - [#6961](https://github.com/NuGet/Home/issues/6961)、[ブログ記事](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span><span class="sxs-lookup"><span data-stu-id="01785-121">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961), [blog post](https://blog.nuget.org/20181205/Lock-down-your-dependencies-using-configurable-trust-policies.html)</span></span>

* <span data-ttu-id="01785-122">パックにシンボルを含める ".snupkg" ファイルの作成 -- シンボル サーバーの snupkg ファイルを受け入れるための nuget プロトコルを把握できるようプッシュを強化する - [#6878](https://github.com/NuGet/Home/issues/6878)、[ブログ記事](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span><span class="sxs-lookup"><span data-stu-id="01785-122">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878), [blog post](https://blog.nuget.org/20181116/Improved-debugging-experience-with-the-NuGet-org-symbol-server-and-snupkg.html)</span></span>

* <span data-ttu-id="01785-123">NuGet 資格情報プラグイン V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="01785-123">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="01785-124">自己完結型の NuGet パッケージ - ライセンス - [#4628](https://github.com/NuGet/Home/issues/4628)、[お知らせ](https://github.com/NuGet/Announcements/issues/32)</span><span class="sxs-lookup"><span data-stu-id="01785-124">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628), [announcement](https://github.com/NuGet/Announcements/issues/32)</span></span>

* <span data-ttu-id="01785-125">PackageReference 上の "GeneratePathProperty" オプトイン メタデータで、"Foo.Bar\1.0\" ディレクトリにパッケージごとの MSBuild プロパティを生成することを可能にする - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="01785-125">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="01785-126">NuGet の操作での顧客の成功を改善する - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="01785-126">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

* <span data-ttu-id="01785-127">ロック ファイルを使った反復可能なパッケージの復元を可能にする - [#5602](https://github.com/NuGet/Home/issues/5602)、[お知らせ](https://github.com/NuGet/Announcements/issues/28)、[ブログ記事](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span><span class="sxs-lookup"><span data-stu-id="01785-127">Enable repeatable package restores using a lock file - [#5602](https://github.com/NuGet/Home/issues/5602), [announcement](https://github.com/NuGet/Announcements/issues/28), [blog post](https://blog.nuget.org/20181217/Enable-repeatable-package-restores-using-a-lock-file.html)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01785-128">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="01785-128">Issues fixed in this release</span></span>

* <span data-ttu-id="01785-129">PackageExtraction によって発生した、(WarnAsErrors を介して) エラーに昇格された警告は、抽出されたパッケージを抜けるべきではない - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="01785-129">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="01785-130">不正に署名されたパッケージは、最終的にグローバル パッケージ フォルダーに含まれるべきではない - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="01785-130">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="01785-131">バインド リダイレクトの生成でファサード アセンブリがスキップされるべきではない - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="01785-131">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="01785-132">VersionRange Equals で浮動小数の範囲が比較されない - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="01785-132">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="01785-133">復元: 新しい .NET Core 2.1 の HTTP スタックを使う際のパフォーマンスの低下 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="01785-133">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="01785-134">パッケージの更新で PackageReference の PrivateAssets が変更されるべきではない - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="01785-134">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="01785-135">署名: パッケージに含まれるパッケージ エントリが多すぎる (> 65534) 場合は、署名を失敗させる必要がある - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="01785-135">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="01785-136">"dotnet nuget push" コードパスで新しい資格情報プロバイダーをサポートする必要がある - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="01785-136">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="01785-137">インバリアント カルチャを使ったプラグインの実行をサポートする (docker で起こるように) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="01785-137">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="01785-138">nuget ソースの追加で NuGet.config から資格情報を削除するべきではない - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="01785-138">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="01785-139">devDependency PackageReference のインストールの規定値を excludeassets=compile にする必要がある - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="01785-139">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="01785-140">migrator オプションを修正してすべてのプロジェクトに対して表示させ、プロジェクトに互換性がない場合はエラーを表示させる - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="01785-140">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="01785-141">"dotnet add package" では、それが資産ファイルに対して実行する復元をコミットする必要がある - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="01785-141">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="01785-142">署名: 署名に関連するエラー メッセージを改善する - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="01785-142">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="01785-143">[テスト失敗] [zh-TW] パッケージ マネージャー コンソールで文字列 "Package Manager Console" がローカライズされない - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="01785-143">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="01785-144">VS 内で、"プロジェクト情報が見つかりません" というエラー メッセージをもう少し具体的にする必要がある - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="01785-144">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="01785-145">nuget パックの nuspec バージョンのタグを誤って使ったときのエラー メッセージが役に立たない - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="01785-145">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="01785-146">DCR - 署名: NuGet プロトコルのサポート: RepositorySignatures/4.9.0 リソース - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="01785-146">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="01785-147">DCR - .nupkg.metadata ファイルがパッケージの抽出中に作成されるようになった - "content-hash" を含む - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="01785-147">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="01785-148">DCR - Mono での実行中にプラグインの authenticode 検証をスキップする - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="01785-148">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="01785-149">この 4.9.0 リリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="01785-149">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="01785-150">概要:4.9.1 の新機能</span><span class="sxs-lookup"><span data-stu-id="01785-150">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="01785-151">新しいコマンド trusted-signers を介して nuget.config への書き込みの読み取りのサポートを追加する - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="01785-151">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01785-152">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="01785-152">Issues fixed in this release</span></span>

* <span data-ttu-id="01785-153">ライセンスのリンクの生成を修正 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="01785-153">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="01785-154">署名の検証に対するエラー コードの回帰 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="01785-154">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="01785-155">NuGet.Build.Tasks.Pack パッケージにライセンス情報がない - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="01785-155">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="01785-156">この 4.9.1 リリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="01785-156">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="summary-whats-new-in-492"></a><span data-ttu-id="01785-157">概要:4.9.2 の新機能</span><span class="sxs-lookup"><span data-stu-id="01785-157">Summary: What's New in 4.9.2</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01785-158">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="01785-158">Issues fixed in this release</span></span>

* <span data-ttu-id="01785-159">ソース名に空白文字が含まれていると、VS/dotnet.exe/nuget.exe/msbuild.exe で資格情報が使用されない - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="01785-159">VS/dotnet.exe/nuget.exe/msbuild.exe restore doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

* <span data-ttu-id="01785-160">LicenseAcceptanceWindow と LicenseFileWindow のアクセシビリティの問題 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="01785-160">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

* <span data-ttu-id="01785-161">DateTimeConverter の DateTime.Parse の FormatException の修正 - [#7539](https://github.com/NuGet/Home/issues/7539)</span><span class="sxs-lookup"><span data-stu-id="01785-161">Fix FormatException in DateTime.Parse from DateTimeConverter - [#7539](https://github.com/NuGet/Home/issues/7539)</span></span>

[<span data-ttu-id="01785-162">この 4.9.2 リリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="01785-162">List of all issues fixed in this release 4.9.2</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.2")

## <a name="summary-whats-new-in-493"></a><span data-ttu-id="01785-163">概要:4.9.3 の新機能</span><span class="sxs-lookup"><span data-stu-id="01785-163">Summary: What's New in 4.9.3</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="01785-164">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="01785-164">Issues fixed in this release</span></span>
#### <a name="repeatable-package-restores-using-a-lock-file-issues"></a><span data-ttu-id="01785-165">"ロック ファイルを使った反復可能なパッケージの復元" に関する問題</span><span class="sxs-lookup"><span data-stu-id="01785-165">"Repeatable Package Restores Using a Lock File" Issues</span></span>

* <span data-ttu-id="01785-166">以前にキャッシュされたパッケージに対して、ハッシュとして動作していないロック モードが正しく計算されない - [#7682](https://github.com/NuGet/Home/issues/7682)</span><span class="sxs-lookup"><span data-stu-id="01785-166">Locked mode not working as hash is calculated incorrectly for previously cached packages - [#7682](https://github.com/NuGet/Home/issues/7682)</span></span>

* <span data-ttu-id="01785-167">復元が `packages.lock.json` ファイル内で定義されているものと別のバージョンに解決される - [#7667](https://github.com/NuGet/Home/issues/7667)</span><span class="sxs-lookup"><span data-stu-id="01785-167">Restore resolves to a different version than defined in `packages.lock.json` file - [#7667](https://github.com/NuGet/Home/issues/7667)</span></span>

* <span data-ttu-id="01785-168">ProjectReferences が関係していると '--locked-mode / RestoreLockedMode' で実際には発生していない復元の失敗が発生する - [#7646](https://github.com/NuGet/Home/issues/7646)</span><span class="sxs-lookup"><span data-stu-id="01785-168">'--locked-mode / RestoreLockedMode' causes spurious Restore failures when ProjectReferences are involved - [#7646](https://github.com/NuGet/Home/issues/7646)</span></span>

* <span data-ttu-id="01785-169">MSBuild SDK リゾルバーは SDK パッケージの SHA を検証しようとするが、packages.lock.json を使うと復元に失敗する - [#7599](https://github.com/NuGet/Home/issues/7599)</span><span class="sxs-lookup"><span data-stu-id="01785-169">MSBuild SDK resolver tries to validate SHA for a SDK package which fails restore when using packages.lock.json - [#7599](https://github.com/NuGet/Home/issues/7599)</span></span>

#### <a name="lock-down-your-dependencies-using-configurable-trust-policies-issues"></a><span data-ttu-id="01785-170">"構成可能な信頼ポリシーを使った依存関係のロックダウン" に関する問題</span><span class="sxs-lookup"><span data-stu-id="01785-170">"Lock Down Your Dependencies Using Configurable Trust Policies" Issues</span></span>
* <span data-ttu-id="01785-171">署名済みパッケージがサポートされていない間は dotnet.exe で trusted-signers を評価すべきではない - [#7574](https://github.com/NuGet/Home/issues/7574)</span><span class="sxs-lookup"><span data-stu-id="01785-171">dotnet.exe should not evaluate trusted-signers while signed packages are not supported - [#7574](https://github.com/NuGet/Home/issues/7574)</span></span>

* <span data-ttu-id="01785-172">構成ファイル内での trustedSigners の順序が信頼評価に影響を与える - [#7572](https://github.com/NuGet/Home/issues/7572)</span><span class="sxs-lookup"><span data-stu-id="01785-172">Order of trustedSigners in config file affects trust evaluation - [#7572](https://github.com/NuGet/Home/issues/7572)</span></span>

* <span data-ttu-id="01785-173">ISettings を実装できない [信頼ポリシー機能をサポートするための API の設定のリファクタリングによって発生] - [#7614](https://github.com/NuGet/Home/issues/7614)</span><span class="sxs-lookup"><span data-stu-id="01785-173">Can't implement ISettings [Caused by refactoring of settings APIs to support Trust Policies feature] - [#7614](https://github.com/NuGet/Home/issues/7614)</span></span>

#### <a name="improved-debugging-experience-issues"></a><span data-ttu-id="01785-174">"デバッグ エクスペリエンスの向上" に関する問題</span><span class="sxs-lookup"><span data-stu-id="01785-174">"Improved Debugging Experience" Issues</span></span>

* <span data-ttu-id="01785-175">.NET Core グローバル ツールのシンボル パッケージを発行できない - [#7632](https://github.com/NuGet/Home/issues/7632)</span><span class="sxs-lookup"><span data-stu-id="01785-175">Cannot publish symbol package for .NET Core Global Tool - [#7632](https://github.com/NuGet/Home/issues/7632)</span></span>

#### <a name="self-contained-nuget-packages---license-issues"></a><span data-ttu-id="01785-176">"自己完結型の NuGet パッケージ - ライセンス" に関する問題</span><span class="sxs-lookup"><span data-stu-id="01785-176">"Self-Contained NuGet Packages - License" Issues</span></span>

* <span data-ttu-id="01785-177">埋め込みライセンス ファイルを使うとシンボル .snupkg パッケージのビルド中にエラーが発生する - [#7591](https://github.com/NuGet/Home/issues/7591)</span><span class="sxs-lookup"><span data-stu-id="01785-177">Error building symbol .snupkg package when using embedded license file - [#7591](https://github.com/NuGet/Home/issues/7591)</span></span>

[<span data-ttu-id="01785-178">この 4.9.3 リリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="01785-178">List of all issues fixed in this release 4.9.3</span></span>](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.3")
## <a name="known-issues"></a><span data-ttu-id="01785-179">既知の問題</span><span class="sxs-lookup"><span data-stu-id="01785-179">Known issues</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="01785-180">dotnet nuget push --interactive が Mac 上でエラーになる。</span><span class="sxs-lookup"><span data-stu-id="01785-180">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="01785-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="01785-181"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="01785-182">懸案事項</span><span class="sxs-lookup"><span data-stu-id="01785-182">Issue</span></span>
<span data-ttu-id="01785-183">`--interactive` 引数が dotnet CLI によって転送されていないため、エラー `error: Missing value for option 'interactive'` が発生します</span><span class="sxs-lookup"><span data-stu-id="01785-183">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="01785-184">回避策</span><span class="sxs-lookup"><span data-stu-id="01785-184">Workaround</span></span>
<span data-ttu-id="01785-185">`dotnet restore --interactive` のように、対話型のオプションを使ってその他の任意の dotnet コマンドを実行し、認証します。</span><span class="sxs-lookup"><span data-stu-id="01785-185">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="01785-186">そうすると、認証が資格情報プロバイダーによってキャッシュされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="01785-186">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="01785-187">その後、`dotnet nuget push` を実行します。</span><span class="sxs-lookup"><span data-stu-id="01785-187">Then run `dotnet nuget push`.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="01785-188">.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。</span><span class="sxs-lookup"><span data-stu-id="01785-188">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="01785-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="01785-189"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="01785-190">懸案事項</span><span class="sxs-lookup"><span data-stu-id="01785-190">Issue</span></span>
<span data-ttu-id="01785-191">dotnet.exe 2.x を使って netcoreapp 1.x と netcoreapp 2.x をマルチターゲットにするプロジェクトを復元すると、そのフォールバック フォルダーがファイル フィードとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="01785-191">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="01785-192">つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。</span><span class="sxs-lookup"><span data-stu-id="01785-192">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="01785-193">回避策</span><span class="sxs-lookup"><span data-stu-id="01785-193">Workaround</span></span>
<span data-ttu-id="01785-194">`RestoreAdditionalProjectSources` に何も設定しないことで、フォールバック フォルダーの使用を無効にします。</span><span class="sxs-lookup"><span data-stu-id="01785-194">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="01785-195">`<RestoreAdditionalProjectSources/>` これは慎重に使う必要があります。フォールバック フォルダーから復元されていたはずの多くのパッケージが、NuGet.org からダウンロードされることになるためです。</span><span class="sxs-lookup"><span data-stu-id="01785-195">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
