---
title: "NuGet 3.2 RC のリリース ノート |Microsoft ドキュメント"
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 330577fa-7965-4433-98ad-b4b4575e1452
description: "既知の問題、バグの修正、追加された機能、および Dcr を含む NuGet 3.2 RC のリリース ノートします。"
keywords: "NuGet 3.2 RC のリリース ノート、バグの修正、既知の問題、機能、Dcr を追加します。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4b5f83f521cb326f5b3a5e6c202cdcb77acde5e2
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-32-rc-release-notes"></a><span data-ttu-id="28423-104">NuGet 3.2 RC のリリース ノートには</span><span class="sxs-lookup"><span data-stu-id="28423-104">NuGet 3.2 RC Release Notes</span></span>

<span data-ttu-id="28423-105">[NuGet 3.1.1 リリース ノート](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 リリース ノート](../release-notes/nuget-3.2.md)</span><span class="sxs-lookup"><span data-stu-id="28423-105">[NuGet 3.1.1 Release Notes](../release-notes/nuget-3.1.1.md) | [NuGet 3.2 Release Notes](../release-notes/nuget-3.2.md)</span></span>

<span data-ttu-id="28423-106">NuGet 3.2 リリース候補版がリリースされた機能強化や、3.1.1 の修正プログラムのコレクションとして、2015 年 9 月 2日をリリースします。</span><span class="sxs-lookup"><span data-stu-id="28423-106">NuGet 3.2 release candidate was released September 2, 2015 as a collection of improvements and fixes for the 3.1.1 release.</span></span>  <span data-ttu-id="28423-107">また、これらは、まず新しい dist.nuget.org リポジトリに公開されている最初のリリースです。</span><span class="sxs-lookup"><span data-stu-id="28423-107">Also, these are the first releases that are published first to the new dist.nuget.org repository.</span></span>

## <a name="new-features"></a><span data-ttu-id="28423-108">新機能</span><span class="sxs-lookup"><span data-stu-id="28423-108">New Features</span></span>

* <span data-ttu-id="28423-109">同じフォルダーに存在するプロジェクトを異なるようになりましたが`project.json`ファイルをフォルダーの各プロジェクトに固有です。</span><span class="sxs-lookup"><span data-stu-id="28423-109">Projects that live in the same folder can now have different `project.json` files in that folder specific to each project.</span></span>  <span data-ttu-id="28423-110">各プロジェクトの名前、`project.json`ファイル`{ProjectName}.project.json`NuGet を正しく参照してプロジェクトごとにそのコンテンツを適切に使用するとします。</span><span class="sxs-lookup"><span data-stu-id="28423-110">For each project, name the `project.json` file `{ProjectName}.project.json` and NuGet will properly reference and use that content for each project appropriately.</span></span>  <span data-ttu-id="28423-111">新しい機能をサポートしているこの[1102](https://github.com/NuGet/Home/issues/1102)</span><span class="sxs-lookup"><span data-stu-id="28423-111">This supports a new feature  [1102](https://github.com/NuGet/Home/issues/1102)</span></span>
* <span data-ttu-id="28423-112">`NuGet.Config`では、相対パス - として globalPackagesFolder [1062](https://github.com/NuGet/Home/issues/1062)</span><span class="sxs-lookup"><span data-stu-id="28423-112">`NuGet.Config` now supports a globalPackagesFolder as a relative path - [1062](https://github.com/NuGet/Home/issues/1062)</span></span>

## <a name="command-line-updates"></a><span data-ttu-id="28423-113">更新プログラムのコマンドライン</span><span class="sxs-lookup"><span data-stu-id="28423-113">Command-line updates</span></span>

<span data-ttu-id="28423-114">これは、NuGet v3 のサーバーをサポートする nuget.exe クライアントの最初のバージョンで管理されているプロジェクトのパッケージを復元する、`project.json`ファイル。</span><span class="sxs-lookup"><span data-stu-id="28423-114">This is the first version of the nuget.exe client that supports the NuGet v3 servers and restoring packages for projects managed with a `project.json` file.</span></span>

#### <a name="there-were-a-number-of-authenticated-feed-issues-that-were-addressed-in-this-release-to-improve-interactions-with-the-client"></a><span data-ttu-id="28423-115">さまざまなクライアントとのやり取りを向上させるためには、このリリースで解決された認証済みのフィードの問題が発生しました。</span><span class="sxs-lookup"><span data-stu-id="28423-115">There were a number of authenticated feed issues that were addressed in this release to improve interactions with the client.</span></span>

* <span data-ttu-id="28423-116">インストールの復元の相互作用 - 認証されたフィードには、最初の要求の資格情報の送信だけ/ [1300](https://github.com/NuGet/Home/issues/1300)、 [456](https://github.com/NuGet/Home/issues/456)</span><span class="sxs-lookup"><span data-stu-id="28423-116">Install / restore interactions only submit credentials for the initial request to the authenticated feed - [1300](https://github.com/NuGet/Home/issues/1300), [456](https://github.com/NuGet/Home/issues/456)</span></span>
* <span data-ttu-id="28423-117">Push コマンドからの構成 - 資格情報が解決しない[1248](https://github.com/NuGet/Home/issues/1248)</span><span class="sxs-lookup"><span data-stu-id="28423-117">Push command does not resolve credentials from configuration - [1248](https://github.com/NuGet/Home/issues/1248)</span></span>
* <span data-ttu-id="28423-118">ユーザー エージェントとヘッダーが NuGet リポジトリが統計情報の追跡のために送信されるようになりました[929](https://github.com/NuGet/Home/issues/929)</span><span class="sxs-lookup"><span data-stu-id="28423-118">User agent and headers are now submitted to NuGet repositories to help with statistics tracking - [929](https://github.com/NuGet/Home/issues/929)</span></span>

#### <a name="we-made-a-number-of-improvements-to-better-handle-network-failures-while-attempting-to-work-with-a-remote-nuget-repository"></a><span data-ttu-id="28423-119">多数の NuGet リポジトリをリモートで作業しようとしています。 ネットワーク障害を適切に処理する機能強化を行いました。</span><span class="sxs-lookup"><span data-stu-id="28423-119">We made a number of improvements to better handle network failures while attempting to work with a remote NuGet repository:</span></span>

* <span data-ttu-id="28423-120">-リモートのフィードに接続できない場合に、エラー メッセージが改善[1238](https://github.com/NuGet/Home/issues/1238)</span><span class="sxs-lookup"><span data-stu-id="28423-120">Improved error messages when unable to connect to remote feeds - [1238](https://github.com/NuGet/Home/issues/1238)</span></span>
* <span data-ttu-id="28423-121">正常時に返される 1、エラー状態が発生した - NuGet 復元コマンドを修正[1186](https://github.com/NuGet/Home/issues/1186)</span><span class="sxs-lookup"><span data-stu-id="28423-121">Corrected NuGet restore command to properly return a 1 when an error condition occurs - [1186](https://github.com/NuGet/Home/issues/1186)</span></span>
* <span data-ttu-id="28423-122">今すぐネットワーク接続の再試行すべて 200 ミリ秒の場合は HTTP 5xx エラー: 5 回試行の最大の[1120](https://github.com/NuGet/Home/issues/1120)</span><span class="sxs-lookup"><span data-stu-id="28423-122">Now retrying network connections every 200ms for a maximum of 5 attempts in the case of HTTP 5xx failures - [1120](https://github.com/NuGet/Home/issues/1120)</span></span>
* <span data-ttu-id="28423-123">Push コマンドの中にサーバーのリダイレクト応答の処理強化[1051](https://github.com/NuGet/Home/issues/1051)</span><span class="sxs-lookup"><span data-stu-id="28423-123">Improved handling of server redirect responses during a push command - [1051](https://github.com/NuGet/Home/issues/1051)</span></span>
* <span data-ttu-id="28423-124">`nuget install -source`では、URL またはリポジトリ名の引数として無効です Nuget.Config を[1046。](https://github.com/NuGet/Home/issues/1046)</span><span class="sxs-lookup"><span data-stu-id="28423-124">`nuget install -source` now supports either URL or repository name from Nuget.Config as an argument - [1046](https://github.com/NuGet/Home/issues/1046)</span></span>
* <span data-ttu-id="28423-125">いないに配置されていたリポジトリの復元中に足りないパッケージが警告ではなくエラーとして報告されるようになりました[1038](https://github.com/NuGet/Home/issues/1038)</span><span class="sxs-lookup"><span data-stu-id="28423-125">Missing packages that were not located on a repository during a restore are now reported as errors instead of warnings [1038](https://github.com/NuGet/Home/issues/1038)</span></span>
* <span data-ttu-id="28423-126">Unix または Linux のシナリオ - \r\n の multipartwebrequest 処理を修正[776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="28423-126">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>

#### <a name="there-are-a-number-of-fixes-to-issues-with-various-commands"></a><span data-ttu-id="28423-127">さまざまなコマンドに関する問題の修正プログラムの数があります。</span><span class="sxs-lookup"><span data-stu-id="28423-127">There are a number of fixes to issues with various commands:</span></span>

* <span data-ttu-id="28423-128">Push コマンドが、パッケージ ソースの構成 - に対して put コマンドの前に、の取得を行いません[1237](https://github.com/NuGet/Home/issues/1237)</span><span class="sxs-lookup"><span data-stu-id="28423-128">Push command no longer does a GET before a PUT against a package source - [1237](https://github.com/NuGet/Home/issues/1237)</span></span>
* <span data-ttu-id="28423-129">一覧のコマンドは、バージョン番号を不要になった繰り返されます[1185](https://github.com/NuGet/Home/issues/1185)</span><span class="sxs-lookup"><span data-stu-id="28423-129">List command no longer repeats version numbers - [1185](https://github.com/NuGet/Home/issues/1185)</span></span>
* <span data-ttu-id="28423-130">パック-ビルド引数を持つようになりました正しくサポートする c# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span><span class="sxs-lookup"><span data-stu-id="28423-130">Pack with the -build argument now properly supports C# 6.0 - [1107](https://github.com/NuGet/Home/issues/1107)</span></span>
* <span data-ttu-id="28423-131">Visual Studio 2015 - で修正された問題の f# プロジェクトをパックしていますがビルドされた[1048](https://github.com/NuGet/Home/issues/1048)</span><span class="sxs-lookup"><span data-stu-id="28423-131">Corrected issues attempting to pack an F# project built with Visual Studio 2015 - [1048](https://github.com/NuGet/Home/issues/1048)</span></span>
* <span data-ttu-id="28423-132">パッケージは既に存在 - したときに、今すぐいいえ ops を復元[1040](https://github.com/NuGet/Home/issues/1040)</span><span class="sxs-lookup"><span data-stu-id="28423-132">Restore now no-ops when packages already exist - [1040](https://github.com/NuGet/Home/issues/1040)</span></span>
* <span data-ttu-id="28423-133">強化されたエラー メッセージ`packages.config`ファイル形式が正しくありません - [1034](https://github.com/NuGet/Home/issues/1034)</span><span class="sxs-lookup"><span data-stu-id="28423-133">Improved error messages when `packages.config` file is malformed - [1034](https://github.com/NuGet/Home/issues/1034)</span></span>
* <span data-ttu-id="28423-134">復元コマンドでの修正`-SolutionDirectory`- の相対パスを使用するスイッチ[992](https://github.com/NuGet/Home/issues/992)</span><span class="sxs-lookup"><span data-stu-id="28423-134">Corrected restore command with `-SolutionDirectory` switch to work with relative paths - [992](https://github.com/NuGet/Home/issues/992)</span></span>
* <span data-ttu-id="28423-135">ソリューション全体の更新プログラム - をサポートするために更新されたコマンドの向上[924](https://github.com/NuGet/Home/issues/924)</span><span class="sxs-lookup"><span data-stu-id="28423-135">Improved Updated command to support solution-wide update - [924](https://github.com/NuGet/Home/issues/924)</span></span>

<span data-ttu-id="28423-136">このリリースで解決される問題の完全な一覧は含まれて NuGet GitHub[コマンド ライン マイルス トーン](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate)です。</span><span class="sxs-lookup"><span data-stu-id="28423-136">A complete list of issues addressed in this release can be found in the NuGet GitHub [Command-Line milestone](https://github.com/nuget/home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.2.0-commandline+is%3Aclosed+-label%3AClosedAs%3ADuplicate).</span></span>

## <a name="visual-studio-extension-updates"></a><span data-ttu-id="28423-137">Visual Studio 拡張機能の更新</span><span class="sxs-lookup"><span data-stu-id="28423-137">Visual Studio extension updates</span></span>

### <a name="new-features-in-visual-studio"></a><span data-ttu-id="28423-138">Visual Studio での新機能</span><span class="sxs-lookup"><span data-stu-id="28423-138">New Features in Visual Studio</span></span>

* <span data-ttu-id="28423-139">により、パッケージを復元する際に、ソリューションをビルドするソリューション ノードで、ソリューション エクスプ ローラーに追加された新しいコンテキスト メニュー項目 ([1274](https://github.com/NuGet/Home/issues/1274))。</span><span class="sxs-lookup"><span data-stu-id="28423-139">A new context menu item was added to the Solution Explorer on the solution node that allows packages to be restored without building the solution ([1274](https://github.com/NuGet/Home/issues/1274)).</span></span>

![新しいコンテキスト メニュー項目の 'パッケージを復元'](./media/NuGet-3.2/newContextMenu.png)

### <a name="updates-and-fixes-in-visual-studio"></a><span data-ttu-id="28423-141">更新し、Visual Studio での修正</span><span class="sxs-lookup"><span data-stu-id="28423-141">Updates and Fixes in Visual Studio</span></span>

#### <a name="the-fixes-for-authenticated-feeds-were-rolled-up-and-addressed-in-the-extension-as-well--the-following-authentication-items-were-also-addressed-in-the-extension"></a><span data-ttu-id="28423-142">認証されたフィードに対する修正プログラム ロールアップし、拡張機能でアドレス指定されます。</span><span class="sxs-lookup"><span data-stu-id="28423-142">The fixes for authenticated feeds were rolled up and addressed in the extension as well.</span></span>  <span data-ttu-id="28423-143">拡張機能に、以下の認証は行われても。</span><span class="sxs-lookup"><span data-stu-id="28423-143">The following authentication items were also addressed in the extension:</span></span>

* <span data-ttu-id="28423-144">これで、フィードを正しく認証 NuGet v3 を正しく処理の代わりに v2 認証フィード - として[1216](https://github.com/NuGet/Home/issues/1216)</span><span class="sxs-lookup"><span data-stu-id="28423-144">Now correctly treating NuGet v3 authenticated feeds properly, instead of as v2 authenticated feeds - [1216](https://github.com/NuGet/Home/issues/1216)</span></span>
* <span data-ttu-id="28423-145">認証の資格情報を使用するプロジェクトで修正された要求`project.json`v2 フィード - との通信および[1082](https://github.com/NuGet/Home/issues/1082)</span><span class="sxs-lookup"><span data-stu-id="28423-145">Corrected request for authentication credentials in projects using `project.json` and communicating with v2 feeds - [1082](https://github.com/NuGet/Home/issues/1082)</span></span>

#### <a name="network-connectivity-had-affected-the-user-interface-in-visual-studio-and-we-addressed-this-with-the-following-fixes"></a><span data-ttu-id="28423-146">ネットワーク接続には、Visual Studio で、ユーザー インターフェイスが影響を受けるし、次の修正プログラムとこれに対処し。</span><span class="sxs-lookup"><span data-stu-id="28423-146">Network connectivity had affected the user interface in Visual Studio, and we addressed this with the following fixes:</span></span>

* <span data-ttu-id="28423-147">パッケージのバージョンでのローカル キャッシュの保守性の向上[1096](https://github.com/NuGet/Home/issues/1096)</span><span class="sxs-lookup"><span data-stu-id="28423-147">Improved the maintenance of the local cache of package versions - [1096](https://github.com/NuGet/Home/issues/1096)</span></span>
* <span data-ttu-id="28423-148">フィードを不要になったしようとすると v2 フィード - として扱うことを示す v3 に接続するときにエラーの動作を変更[1253](https://github.com/NuGet/Home/issues/1253)</span><span class="sxs-lookup"><span data-stu-id="28423-148">Changed the failure behavior when connecting to a v3 feed to no longer attempt to treat it as a v2 feed - [1253](https://github.com/NuGet/Home/issues/1253)</span></span>
* <span data-ttu-id="28423-149">複数のパッケージ ソースのパッケージをインストールするときに、インストールの失敗を防ぐようになりました[1183](https://github.com/NuGet/Home/issues/1183)</span><span class="sxs-lookup"><span data-stu-id="28423-149">Now preventing install failures when installing a package with multiple package sources - [1183](https://github.com/NuGet/Home/issues/1183)</span></span>

<span data-ttu-id="28423-150">おには、ビルド操作との対話の処理が向上しました。</span><span class="sxs-lookup"><span data-stu-id="28423-150">We improved handling of interactions with build operations:</span></span>

* <span data-ttu-id="28423-151">1 つのプロジェクトが失敗した場合 - のパッケージを復元する場合は、プロジェクトをビルドを続行するようになりました[1169](https://github.com/NuGet/Home/issues/1169)</span><span class="sxs-lookup"><span data-stu-id="28423-151">Now continuing to build projects if restoring packages for a single project fails - [1169](https://github.com/NuGet/Home/issues/1169)</span></span>
* <span data-ttu-id="28423-152">ソリューションの再構築 - 強制的に、ソリューション内の別のプロジェクトが依存するプロジェクトにパッケージをインストールする[981](https://github.com/NuGet/Home/issues/981)</span><span class="sxs-lookup"><span data-stu-id="28423-152">Installing a package into a project that is depended on by another project in the solution forces a solution rebuild - [981](https://github.com/NuGet/Home/issues/981)</span></span>
* <span data-ttu-id="28423-153">-プロジェクトへの変更を正しくロールバックに失敗したパッケージのインストールを修正[1265](https://github.com/NuGet/Home/issues/1265)</span><span class="sxs-lookup"><span data-stu-id="28423-153">Corrected failed package installs to properly rollback changes to a project - [1265](https://github.com/NuGet/Home/issues/1265)</span></span>
* <span data-ttu-id="28423-154">不注意による削除の修正、`developmentDependency`属性内のパッケージで`packages.config`  -  [1263](https://github.com/NuGet/Home/issues/1263)</span><span class="sxs-lookup"><span data-stu-id="28423-154">Corrected inadvertent removal of the `developmentDependency` attribute on a package in `packages.config` - [1263](https://github.com/NuGet/Home/issues/1263)</span></span>
* <span data-ttu-id="28423-155">呼び出す`install.ps1`ある適切な`$package.AssemblyReferences`に渡されたオブジェクト[1245](https://github.com/NuGet/Home/issues/1245)</span><span class="sxs-lookup"><span data-stu-id="28423-155">Calls to `install.ps1` now have a proper `$package.AssemblyReferences` object passed - [1245](https://github.com/NuGet/Home/issues/1245)</span></span>
* <span data-ttu-id="28423-156">プロジェクトが、正常な状態の間を UWP プロジェクトでパッケージのアンインストールを妨げなく[1128](https://github.com/NuGet/Home/issues/1128)</span><span class="sxs-lookup"><span data-stu-id="28423-156">No longer preventing uninstalls of packages in UWP projects while the project is in a bad state - [1128](https://github.com/NuGet/Home/issues/1128)</span></span>
* <span data-ttu-id="28423-157">ソリューションが混在している`packages.config`と`project.json`せず、2 番目のプロジェクトが正しくビルドようになりましたビルド操作 - [1122](https://github.com/NuGet/Home/issues/1122)</span><span class="sxs-lookup"><span data-stu-id="28423-157">Solutions containing a mix of `packages.config` and `project.json` projects are now properly built without requiring a second build operation - [1122](https://github.com/NuGet/Home/issues/1122)</span></span>
* <span data-ttu-id="28423-158">リンクまたは別のフォルダーに配置された場合、app.config ファイルを正しく検索[1111](https://github.com/NuGet/Home/issues/1111)、 [894](https://github.com/NuGet/Home/issues/894)</span><span class="sxs-lookup"><span data-stu-id="28423-158">Properly locating app.config files if they are linked or located in a different folder - [1111](https://github.com/NuGet/Home/issues/1111), [894](https://github.com/NuGet/Home/issues/894)</span></span>
* <span data-ttu-id="28423-159">UWP プロジェクトが一覧にないパッケージをインストールできるよう[1109](https://github.com/NuGet/Home/issues/1109)</span><span class="sxs-lookup"><span data-stu-id="28423-159">UWP projects can now install unlisted packages - [1109](https://github.com/NuGet/Home/issues/1109)</span></span>
* <span data-ttu-id="28423-160">パッケージの復元は今すぐ、ソリューションが許可されません - 保存された状態で[1081](https://github.com/NuGet/Home/issues/1081)</span><span class="sxs-lookup"><span data-stu-id="28423-160">Package restore is now allowed while a solution is not in a saved state - [1081](https://github.com/NuGet/Home/issues/1081)</span></span>


<span data-ttu-id="28423-161">ファイルが修正された構成への更新を処理します。</span><span class="sxs-lookup"><span data-stu-id="28423-161">Handling updates to configuration files were corrected:</span></span>

* <span data-ttu-id="28423-162">パッケージの後続のビルドを上から配信されなくターゲット ファイルを削除する、`project.json`マネージ プロジェクトに[1288](https://github.com/NuGet/Home/issues/1288)</span><span class="sxs-lookup"><span data-stu-id="28423-162">No longer removing a targets file delivered from a package on subsequent builds of a `project.json` managed project - [1288](https://github.com/NuGet/Home/issues/1288)</span></span>
* <span data-ttu-id="28423-163">不要になった - ASP.NET 5 ソリューションのビルド中に Nuget.Config ファイルの変更[1201](https://github.com/NuGet/Home/issues/1201)</span><span class="sxs-lookup"><span data-stu-id="28423-163">No longer modifying Nuget.Config files during ASP.NET 5 solution build - [1201](https://github.com/NuGet/Home/issues/1201)</span></span>
* <span data-ttu-id="28423-164">パッケージの更新プログラムの中にバージョン制約を許可される変更されなく[1130](https://github.com/NuGet/Home/issues/1130)</span><span class="sxs-lookup"><span data-stu-id="28423-164">No longer changing allowed versions constraint during package update - [1130](https://github.com/NuGet/Home/issues/1130)</span></span>
* <span data-ttu-id="28423-165">ロック ファイル今すぐロックされたままのビルド時に[1127](https://github.com/NuGet/Home/issues/1127)</span><span class="sxs-lookup"><span data-stu-id="28423-165">Lock files now remain locked during build - [1127](https://github.com/NuGet/Home/issues/1127)</span></span>
* <span data-ttu-id="28423-166">今すぐ変更`packages.config`いない更新プログラムの中に書き換えたと[585](https://github.com/NuGet/Home/issues/585)</span><span class="sxs-lookup"><span data-stu-id="28423-166">Now modifying `packages.config` and not rewriting it during updates - [585](https://github.com/NuGet/Home/issues/585)</span></span>


<span data-ttu-id="28423-167">ソース管理の TFS とのやり取りが改善されます。</span><span class="sxs-lookup"><span data-stu-id="28423-167">Interactions with TFS source control are improved:</span></span>

* <span data-ttu-id="28423-168">不要になった - TFS にバインドされているパッケージのインストールが失敗している[番号 1164](https://github.com/NuGet/Home/issues/1164)、 [980](https://github.com/NuGet/Home/issues/980)</span><span class="sxs-lookup"><span data-stu-id="28423-168">No longer failing installs for packages that are bound to TFS - [1164](https://github.com/NuGet/Home/issues/1164), [980](https://github.com/NuGet/Home/issues/980)</span></span>
* <span data-ttu-id="28423-169">TFS 2013 の統合に使用できるように修正された NuGet ユーザー インターフェイス[1071](https://github.com/NuGet/Home/issues/1071)</span><span class="sxs-lookup"><span data-stu-id="28423-169">Corrected NuGet user interface to allow TFS 2013 integration - [1071](https://github.com/NuGet/Home/issues/1071)</span></span>
* <span data-ttu-id="28423-170">正しくパッケージ フォルダーに由来する復元パッケージへの参照を修正[1004](https://github.com/NuGet/Home/issues/1004)</span><span class="sxs-lookup"><span data-stu-id="28423-170">Corrected references to packages restored to properly come from a packages folder - [1004](https://github.com/NuGet/Home/issues/1004)</span></span>

<span data-ttu-id="28423-171">最後に、私たちも向上してこれらの項目。</span><span class="sxs-lookup"><span data-stu-id="28423-171">Finally, we also improved these items:</span></span>

* <span data-ttu-id="28423-172">ログ メッセージの詳細度が小さくなります`project.json`マネージ プロジェクトに[1163](https://github.com/NuGet/Home/issues/1163)</span><span class="sxs-lookup"><span data-stu-id="28423-172">Verbosity of log messages reduced for `project.json` managed projects - [1163](https://github.com/NuGet/Home/issues/1163)</span></span>
* <span data-ttu-id="28423-173">これで、正しくインストールされているバージョンのパッケージ、ユーザー インターフェイスで表示・ [1061](https://github.com/NuGet/Home/issues/1061)</span><span class="sxs-lookup"><span data-stu-id="28423-173">Now properly displaying the installed version of a package in the user interface - [1061](https://github.com/NuGet/Home/issues/1061)</span></span>


<span data-ttu-id="28423-174">Visual Studio 拡張機能は含まれて NuGet GitHub の課題の完全な一覧[3.2 マイルス トーン](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span><span class="sxs-lookup"><span data-stu-id="28423-174">A complete list of issues addressed for the Visual Studio extension can be found in the NuGet GitHub [3.2 milestone](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+-label%3AClosedAs%3ADuplicate+milestone%3A3.2)</span></span>

## <a name="known-issues"></a><span data-ttu-id="28423-175">既知の問題</span><span class="sxs-lookup"><span data-stu-id="28423-175">Known Issues</span></span>

<span data-ttu-id="28423-176">あることができます、GitHub の問題一覧上の問題を追跡するために続行: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span><span class="sxs-lookup"><span data-stu-id="28423-176">We continue to track issues on our GitHub issues list which can be found at: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)</span></span>