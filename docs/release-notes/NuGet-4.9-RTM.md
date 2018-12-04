---
title: NuGet 4.9 RTM リリース ノート
description: NuGet 4.9 のリリース ノートです。既知の問題、バグ修正、新機能、および DCR について示します。
author: karann-msft
ms.author: karann
ms.date: 11/20/2018
ms.topic: conceptual
ms.openlocfilehash: 3da1056f64b76f27afa662d879ef9f85868e2a07
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453774"
---
# <a name="nuget-49-release-notes"></a><span data-ttu-id="f24af-103">NuGet 4.9 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="f24af-103">NuGet 4.9 Release Notes</span></span>

<span data-ttu-id="f24af-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、NuGet 4.9.0 機能が付属しています。</span><span class="sxs-lookup"><span data-stu-id="f24af-104">[Visual Studio 2017 15.9.0 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with NuGet 4.9.0 functionality.</span></span>


<span data-ttu-id="f24af-105">また、次の同一機能のコマンド ライン バージョンが利用可能です。</span><span class="sxs-lookup"><span data-stu-id="f24af-105">Command line versions of the same functionality are also available:</span></span>
* <span data-ttu-id="f24af-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span><span class="sxs-lookup"><span data-stu-id="f24af-106">NuGet.exe 4.9.x - [nuget.org/downloads](https://nuget.org/downloads)</span></span>
* <span data-ttu-id="f24af-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span><span class="sxs-lookup"><span data-stu-id="f24af-107">dotnet.exe - [.NET Core SDK 2.1.500](https://www.microsoft.com/net/download/visual-studio-sdks)</span></span>


## <a name="summary-whats-new-in-490"></a><span data-ttu-id="f24af-108">概要: 4.9.0 の新機能</span><span class="sxs-lookup"><span data-stu-id="f24af-108">Summary: What's New in 4.9.0</span></span>

* <span data-ttu-id="f24af-109">署名: ClientPolicies において、NuGet.Config に記載されている信頼された作成者とリポジトリのセットの使用を要求することを可能にする - [#6961](https://github.com/NuGet/Home/issues/6961)</span><span class="sxs-lookup"><span data-stu-id="f24af-109">Signing: Enable ClientPolicies to require use of a set of Trusted Authors and Repositories listed in NuGet.Config - [#6961](https://github.com/NuGet/Home/issues/6961)</span></span>

* <span data-ttu-id="f24af-110">パックにシンボルを含める ".snupkg" ファイルの作成 -- シンボル サーバーの snupkg ファイルを受け入れるための nuget プロトコルを把握できるようプッシュを強化する - [#6878](https://github.com/NuGet/Home/issues/6878)</span><span class="sxs-lookup"><span data-stu-id="f24af-110">create ".snupkg" files to contain symbols in pack -- enhance push to understand nuget protocol to accept snupkg files for symbol server - [#6878](https://github.com/NuGet/Home/issues/6878)</span></span>

* <span data-ttu-id="f24af-111">NuGet 資格情報プラグイン V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span><span class="sxs-lookup"><span data-stu-id="f24af-111">NuGet credential plugin V2 - [#6642](https://github.com/NuGet/Home/issues/6642)</span></span>

* <span data-ttu-id="f24af-112">自己完結型の NuGet パッケージ - ライセンス - [#4628](https://github.com/NuGet/Home/issues/4628)</span><span class="sxs-lookup"><span data-stu-id="f24af-112">Self-Contained NuGet Packages - License - [#4628](https://github.com/NuGet/Home/issues/4628)</span></span>

* <span data-ttu-id="f24af-113">PackageReference 上の "GeneratePathProperty" オプトイン メタデータで、"Foo.Bar\1.0\" ディレクトリにパッケージごとの MSBuild プロパティを生成することを可能にする - [#6949](https://github.com/NuGet/Home/issues/6949)</span><span class="sxs-lookup"><span data-stu-id="f24af-113">Enable opt-in "GeneratePathProperty" metadata on a PackageReference to generate a per package MSBuild property to "Foo.Bar\1.0\" directory - [#6949](https://github.com/NuGet/Home/issues/6949)</span></span>

* <span data-ttu-id="f24af-114">NuGet の操作での顧客の成功を改善する - [#7108](https://github.com/NuGet/Home/issues/7108)</span><span class="sxs-lookup"><span data-stu-id="f24af-114">Improve customer success with NuGet operations - [#7108](https://github.com/NuGet/Home/issues/7108)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f24af-115">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="f24af-115">Issues fixed in this release</span></span>

* <span data-ttu-id="f24af-116">PackageExtraction によって発生した、(WarnAsErrors を介して) エラーに昇格された警告は、抽出されたパッケージを抜けるべきではない - [#7445](https://github.com/NuGet/Home/issues/7445)</span><span class="sxs-lookup"><span data-stu-id="f24af-116">Warnings elevated to errors (via WarnAsErrors) raised by PackageExtraction should never leave extracted package around - [#7445](https://github.com/NuGet/Home/issues/7445)</span></span>

* <span data-ttu-id="f24af-117">不正に署名されたパッケージは、最終的にグローバル パッケージ フォルダーに含まれるべきではない - [#7423](https://github.com/NuGet/Home/issues/7423)</span><span class="sxs-lookup"><span data-stu-id="f24af-117">Badly signed packages should not end up in the global packages folder - [#7423](https://github.com/NuGet/Home/issues/7423)</span></span>

* <span data-ttu-id="f24af-118">バインド リダイレクトの生成でファサード アセンブリがスキップされるべきではない - [#7393](https://github.com/NuGet/Home/issues/7393)</span><span class="sxs-lookup"><span data-stu-id="f24af-118">binding redirect generation should not skip facade assemblies - [#7393](https://github.com/NuGet/Home/issues/7393)</span></span>

* <span data-ttu-id="f24af-119">VersionRange Equals で浮動小数の範囲が比較されない - [#7324](https://github.com/NuGet/Home/issues/7324)</span><span class="sxs-lookup"><span data-stu-id="f24af-119">VersionRange Equals doesn't compare floating ranges - [#7324](https://github.com/NuGet/Home/issues/7324)</span></span>

* <span data-ttu-id="f24af-120">復元: 新しい .NET Core 2.1 の HTTP スタックを使う際のパフォーマンスの低下 - [#7314](https://github.com/NuGet/Home/issues/7314)</span><span class="sxs-lookup"><span data-stu-id="f24af-120">Restore:  performance regression using new .NET Core 2.1 HTTP stack - [#7314](https://github.com/NuGet/Home/issues/7314)</span></span>

* <span data-ttu-id="f24af-121">パッケージの更新で PackageReference の PrivateAssets が変更されるべきではない - [#7285](https://github.com/NuGet/Home/issues/7285)</span><span class="sxs-lookup"><span data-stu-id="f24af-121">Update of a Package should not modify PrivateAssets of a PackageReference - [#7285](https://github.com/NuGet/Home/issues/7285)</span></span>

* <span data-ttu-id="f24af-122">署名: パッケージに含まれるパッケージ エントリが多すぎる (> 65534) 場合は、署名を失敗させる必要がある - [#7248](https://github.com/NuGet/Home/issues/7248)</span><span class="sxs-lookup"><span data-stu-id="f24af-122">Signing:  signing should fail if a package has too many package entries (>65534) - [#7248](https://github.com/NuGet/Home/issues/7248)</span></span>

* <span data-ttu-id="f24af-123">"dotnet nuget push" コードパスで新しい資格情報プロバイダーをサポートする必要がある - [#7233](https://github.com/NuGet/Home/issues/7233)</span><span class="sxs-lookup"><span data-stu-id="f24af-123">"dotnet nuget push" codepath should support the new credential provider - [#7233](https://github.com/NuGet/Home/issues/7233)</span></span>

* <span data-ttu-id="f24af-124">インバリアント カルチャを使ったプラグインの実行をサポートする (docker で起こるように) - [#7223](https://github.com/NuGet/Home/issues/7223)</span><span class="sxs-lookup"><span data-stu-id="f24af-124">Support executing plugins with invariant culture (as happens in docker) - [#7223](https://github.com/NuGet/Home/issues/7223)</span></span>

* <span data-ttu-id="f24af-125">nuget ソースの追加で NuGet.config から資格情報を削除するべきではない - [#7200](https://github.com/NuGet/Home/issues/7200)</span><span class="sxs-lookup"><span data-stu-id="f24af-125">nuget sources add should not delete credentials from NuGet.config - [#7200](https://github.com/NuGet/Home/issues/7200)</span></span>

* <span data-ttu-id="f24af-126">devDependency PackageReference のインストールの規定値を excludeassets=compile にする必要がある - [#7084](https://github.com/NuGet/Home/issues/7084)</span><span class="sxs-lookup"><span data-stu-id="f24af-126">installing a devDependency PackageReference should default to excludeassets=compile - [#7084](https://github.com/NuGet/Home/issues/7084)</span></span>

* <span data-ttu-id="f24af-127">migrator オプションを修正してすべてのプロジェクトに対して表示させ、プロジェクトに互換性がない場合はエラーを表示させる - [#6958](https://github.com/NuGet/Home/issues/6958)</span><span class="sxs-lookup"><span data-stu-id="f24af-127">fix migrator option to be displayed for all projects and show error if project is incompatible - [#6958](https://github.com/NuGet/Home/issues/6958)</span></span>

* <span data-ttu-id="f24af-128">"dotnet add package" では、それが資産ファイルに対して実行する復元をコミットする必要がある - [#6928](https://github.com/NuGet/Home/issues/6928)</span><span class="sxs-lookup"><span data-stu-id="f24af-128">"dotnet add package" should commit the restore it performs to the assets file - [#6928](https://github.com/NuGet/Home/issues/6928)</span></span>

* <span data-ttu-id="f24af-129">署名: 署名に関連するエラー メッセージを改善する - [#6906](https://github.com/NuGet/Home/issues/6906)</span><span class="sxs-lookup"><span data-stu-id="f24af-129">Signing:  improve signing related error messages - [#6906](https://github.com/NuGet/Home/issues/6906)</span></span>

* <span data-ttu-id="f24af-130">[テスト失敗] [zh-TW] パッケージ マネージャー コンソールで文字列 "Package Manager Console" がローカライズされない - [#6381](https://github.com/NuGet/Home/issues/6381)</span><span class="sxs-lookup"><span data-stu-id="f24af-130">[Test Failure][zh-TW]String "Package Manager Console" doesn't localize on Package Manager Console  - [#6381](https://github.com/NuGet/Home/issues/6381)</span></span>

* <span data-ttu-id="f24af-131">VS 内で、"プロジェクト情報が見つかりません" というエラー メッセージをもう少し具体的にする必要がある - [#5350](https://github.com/NuGet/Home/issues/5350)</span><span class="sxs-lookup"><span data-stu-id="f24af-131">Error message around "Unable to find project information" should be a little more specific inside VS - [#5350](https://github.com/NuGet/Home/issues/5350)</span></span>

* <span data-ttu-id="f24af-132">nuget パックの nuspec バージョンのタグを誤って使ったときのエラー メッセージが役に立たない - [#2714](https://github.com/NuGet/Home/issues/2714)</span><span class="sxs-lookup"><span data-stu-id="f24af-132">Unhelpful error message when incorrectly using nuspec version tag of nuget pack - [#2714](https://github.com/NuGet/Home/issues/2714)</span></span>

* <span data-ttu-id="f24af-133">DCR - 署名: NuGet プロトコルをサポートする: RepositorySignatures/4.9.0 リソース - [#7421](https://github.com/NuGet/Home/issues/7421)</span><span class="sxs-lookup"><span data-stu-id="f24af-133">DCR - Signing:  support NuGet protocol: RepositorySignatures/4.9.0 resource - [#7421](https://github.com/NuGet/Home/issues/7421)</span></span>

* <span data-ttu-id="f24af-134">DCR - .nupkg.metadata ファイルがパッケージの抽出中に作成されるようになった - "content-hash" を含む - [#7283](https://github.com/NuGet/Home/issues/7283)</span><span class="sxs-lookup"><span data-stu-id="f24af-134">DCR - .nupkg.metadata file will now be created during package extraction - contains "content-hash" - [#7283](https://github.com/NuGet/Home/issues/7283)</span></span>

* <span data-ttu-id="f24af-135">DCR - Mono での実行中にプラグインの authenticode 検証をスキップする - [#7222](https://github.com/NuGet/Home/issues/7222)</span><span class="sxs-lookup"><span data-stu-id="f24af-135">DCR - Skip authenticode verification for plugins while executing on Mono - [#7222](https://github.com/NuGet/Home/issues/7222)</span></span>

[<span data-ttu-id="f24af-136">この 4.9.0 リリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="f24af-136">List of all issues fixed in this release 4.9.0</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9") <br>

## <a name="summary-whats-new-in-491"></a><span data-ttu-id="f24af-137">概要: 4.9.1 の新機能</span><span class="sxs-lookup"><span data-stu-id="f24af-137">Summary: What's New in 4.9.1</span></span>

* <span data-ttu-id="f24af-138">新しいコマンド trusted-signers を介して nuget.config への書き込みの読み取りのサポートを追加する - [#7480](https://github.com/NuGet/Home/issues/7480)</span><span class="sxs-lookup"><span data-stu-id="f24af-138">Add support for reading a writing to the nuget.config via a new command trusted-signers - [#7480](https://github.com/NuGet/Home/issues/7480)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="f24af-139">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="f24af-139">Issues fixed in this release</span></span>

* <span data-ttu-id="f24af-140">ライセンスのリンクの生成を修正 - [#7515](https://github.com/NuGet/Home/issues/7515)</span><span class="sxs-lookup"><span data-stu-id="f24af-140">Fix license link generation - [#7515](https://github.com/NuGet/Home/issues/7515)</span></span>

* <span data-ttu-id="f24af-141">署名の検証に対するエラー コードの回帰 - [#7492](https://github.com/NuGet/Home/issues/7492)</span><span class="sxs-lookup"><span data-stu-id="f24af-141">Error codes regression for validating signatures - [#7492](https://github.com/NuGet/Home/issues/7492)</span></span>

* <span data-ttu-id="f24af-142">NuGet.Build.Tasks.Pack パッケージにライセンス情報がない - [#7379](https://github.com/NuGet/Home/issues/7379)</span><span class="sxs-lookup"><span data-stu-id="f24af-142">NuGet.Build.Tasks.Pack package does not have license information - [#7379](https://github.com/NuGet/Home/issues/7379)</span></span>

[<span data-ttu-id="f24af-143">この 4.9.1 リリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="f24af-143">List of all issues fixed in this release 4.9.1</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.9.1")

## <a name="known-issues"></a><span data-ttu-id="f24af-144">既知の問題</span><span class="sxs-lookup"><span data-stu-id="f24af-144">Known issues</span></span>

### <a name="dotnetexenugetexe-doesnt-use-credentials-when-source-name-contains-a-whitespace---7517httpsgithubcomnugethomeissues7517"></a><span data-ttu-id="f24af-145">ソース名に空白文字が含まれていると、dotnet.exe/nuget.exe で資格情報が使用されない - [#7517](https://github.com/NuGet/Home/issues/7517)</span><span class="sxs-lookup"><span data-stu-id="f24af-145">dotnet.exe/nuget.exe doesn't use credentials when source name contains a whitespace - [#7517](https://github.com/NuGet/Home/issues/7517)</span></span>

#### <a name="issue"></a><span data-ttu-id="f24af-146">懸案事項</span><span class="sxs-lookup"><span data-stu-id="f24af-146">Issue</span></span>
<span data-ttu-id="f24af-147">ソース名に空白文字が含まれていると、nuget.exe によって `The ' ' character, hexadecimal value 0x20, cannot be included in a name.` のようなエラーがスローされます。</span><span class="sxs-lookup"><span data-stu-id="f24af-147">When there is a whitespace in the source name, nuget.exe throws an error like `The ' ' character, hexadecimal value 0x20, cannot be included in a name.`</span></span>

#### <a name="workaround"></a><span data-ttu-id="f24af-148">回避策</span><span class="sxs-lookup"><span data-stu-id="f24af-148">Workaround</span></span>
<span data-ttu-id="f24af-149">空白文字を含めないようにソースの名前を変更します。</span><span class="sxs-lookup"><span data-stu-id="f24af-149">Change the name of the source to not contain a whitespace.</span></span>

### <a name="dotnet-nuget-push---interactive-gives-an-error-on-mac---7519httpsgithubcomnugethomeissues7519"></a><span data-ttu-id="f24af-150">dotnet nuget push --interactive が Mac 上でエラーになる。</span><span class="sxs-lookup"><span data-stu-id="f24af-150">dotnet nuget push --interactive gives an error on Mac.</span></span><span data-ttu-id="f24af-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span><span class="sxs-lookup"><span data-stu-id="f24af-151"> - [#7519](https://github.com/NuGet/Home/issues/7519)</span></span>

#### <a name="issue"></a><span data-ttu-id="f24af-152">懸案事項</span><span class="sxs-lookup"><span data-stu-id="f24af-152">Issue</span></span>
<span data-ttu-id="f24af-153">`--interactive` 引数が dotnet CLI によって転送されていないため、エラー `error: Missing value for option 'interactive'` が発生します</span><span class="sxs-lookup"><span data-stu-id="f24af-153">The `--interactive` argument is not being forwarded by the dotnet cli and results in the error `error: Missing value for option 'interactive'`</span></span>

#### <a name="workaround"></a><span data-ttu-id="f24af-154">回避策</span><span class="sxs-lookup"><span data-stu-id="f24af-154">Workaround</span></span>
<span data-ttu-id="f24af-155">`dotnet restore --interactive` のように、対話型のオプションを使ってその他の任意の dotnet コマンドを実行し、認証します。</span><span class="sxs-lookup"><span data-stu-id="f24af-155">Run any other dotnet command with the interactive option such as `dotnet restore --interactive` and authenticate.</span></span> <span data-ttu-id="f24af-156">そうすると、認証が資格情報プロバイダーによってキャッシュされる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="f24af-156">The authentication then might be cached by the credential provider.</span></span> <span data-ttu-id="f24af-157">その後、`dotnet nuget push` を実行します。</span><span class="sxs-lookup"><span data-stu-id="f24af-157">Then run `dotnet nuget push`.</span></span>

### <a name="licenseacceptancewindow-and-licensefilewindow-accessibility-issues---7452httpsgithubcomnugethomeissues7452"></a><span data-ttu-id="f24af-158">LicenseAcceptanceWindow と LicenseFileWindow のアクセシビリティの問題 - [#7452](https://github.com/NuGet/Home/issues/7452)</span><span class="sxs-lookup"><span data-stu-id="f24af-158">LicenseAcceptanceWindow and LicenseFileWindow Accessibility issues - [#7452](https://github.com/NuGet/Home/issues/7452)</span></span>

#### <a name="issue"></a><span data-ttu-id="f24af-159">懸案事項</span><span class="sxs-lookup"><span data-stu-id="f24af-159">Issue</span></span>
<span data-ttu-id="f24af-160">ライセンスの同意ウィンドウおよびライセンス ファイル ウィンドウについて、キーボード ナビゲーションと、スクリーン リーダーおよび JAWS を使ったナレーションに関するアクセシビリティの問題があります。</span><span class="sxs-lookup"><span data-stu-id="f24af-160">The license acceptance window and license file window have accessibility issues with keyboard navigation and narration with screen reader and JAWS.</span></span>

#### <a name="workaround"></a><span data-ttu-id="f24af-161">回避策</span><span class="sxs-lookup"><span data-stu-id="f24af-161">Workaround</span></span>
<span data-ttu-id="f24af-162">回避策はありません。</span><span class="sxs-lookup"><span data-stu-id="f24af-162">No workaround.</span></span>

### <a name="packages-in-fallbackfolders-installed-by-net-core-sdk-are-custom-installed-and-fail-signature-validation---7414httpsgithubcomnugethomeissues7414"></a><span data-ttu-id="f24af-163">.NET Core SDK によってインストールされる FallbackFolders 内のパッケージがカスタム インストールされ、署名の検証に失敗する。</span><span class="sxs-lookup"><span data-stu-id="f24af-163">Packages in FallbackFolders installed by .NET Core SDK are custom installed, and fail signature validation.</span></span><span data-ttu-id="f24af-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span><span class="sxs-lookup"><span data-stu-id="f24af-164"> - [#7414](https://github.com/NuGet/Home/issues/7414)</span></span>

#### <a name="issue"></a><span data-ttu-id="f24af-165">懸案事項</span><span class="sxs-lookup"><span data-stu-id="f24af-165">Issue</span></span>
<span data-ttu-id="f24af-166">dotnet.exe 2.x を使って netcoreapp 1.x と netcoreapp 2.x をマルチターゲットにするプロジェクトを復元すると、そのフォールバック フォルダーがファイル フィードとして扱われます。</span><span class="sxs-lookup"><span data-stu-id="f24af-166">When using dotnet.exe 2.x to restore a project that multi-targets netcoreapp 1.x and netcoreapp 2.x, the fallback folder is treated as a file feed.</span></span> <span data-ttu-id="f24af-167">つまり、復元するときに、NuGet ではフォールバック フォルダーからパッケージを選択し、それをグローバル パッケージ フォルダーにインストールしようと試み、通常の署名の検証を行って、失敗します。</span><span class="sxs-lookup"><span data-stu-id="f24af-167">This means, when restoring, NuGet will pick the package from the fallback folder and try to install it into the global packages folder and do the usual signing validation which fails.</span></span>

#### <a name="workaround"></a><span data-ttu-id="f24af-168">回避策</span><span class="sxs-lookup"><span data-stu-id="f24af-168">Workaround</span></span>
<span data-ttu-id="f24af-169">`RestoreAdditionalProjectSources` に何も設定しないことで、フォールバック フォルダーの使用を無効にします。</span><span class="sxs-lookup"><span data-stu-id="f24af-169">Disable the usage of the fallback folder by setting the `RestoreAdditionalProjectSources` to nothing.</span></span> <span data-ttu-id="f24af-170">`<RestoreAdditionalProjectSources/>` これは慎重に使う必要があります。フォールバック フォルダーから復元されていたはずの多くのパッケージが、NuGet.org からダウンロードされることになるためです。</span><span class="sxs-lookup"><span data-stu-id="f24af-170">`<RestoreAdditionalProjectSources/>` Use this with caution as it will cause a lot of packages to be downloaded from NuGet.org which otherwise would be have been restored from the fallback folder.</span></span>
