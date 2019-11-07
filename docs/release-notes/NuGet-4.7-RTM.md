---
title: NuGet 4.7 RTM リリース ノート
description: NuGet 4.7.0 のリリース ノートです。既知の問題、バグ修正、追加機能、および DCR を含みます。
author: karann-msft
ms.author: karann
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 0c3c0380fe6efb3c58124ca5ba8bc1306a433340
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73611351"
---
# <a name="nuget-47-release-notes"></a><span data-ttu-id="0d110-103">NuGet 4.7 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="0d110-103">NuGet 4.7 Release Notes</span></span>

<span data-ttu-id="0d110-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、[NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe) が付属しています。</span><span class="sxs-lookup"><span data-stu-id="0d110-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-470"></a><span data-ttu-id="0d110-105">概要:4.7.0 の新機能</span><span class="sxs-lookup"><span data-stu-id="0d110-105">Summary: What's New in 4.7.0</span></span>

* <span data-ttu-id="0d110-106">パッケージの署名が拡張され、[リポジトリの署名付きパッケージ](https://github.com/NuGet/Home/wiki/Repository-Signatures)が有効になりました。</span><span class="sxs-lookup"><span data-stu-id="0d110-106">We have augmented package signing to enable [Repository Signed packages](https://github.com/NuGet/Home/wiki/Repository-Signatures)</span></span>

* <span data-ttu-id="0d110-107">Visual Studio Version 15.7 では、[packages.config 形式を使用する既存のプロジェクトを移行して、代わりに PackageReference を使用する](https://docs.microsoft.com/nuget/consume-packages/migrate-packages-config-to-package-reference)機能が導入されました。</span><span class="sxs-lookup"><span data-stu-id="0d110-107">With Visual Studio Version 15.7, we have introduced the capability to [migrate existing projects that use the packages.config format to use PackageReference](https://docs.microsoft.com/nuget/consume-packages/migrate-packages-config-to-package-reference) instead.</span></span>

## <a name="summary-whats-new-in-472"></a><span data-ttu-id="0d110-108">概要:4.7.2 の新機能</span><span class="sxs-lookup"><span data-stu-id="0d110-108">Summary: What's New in 4.7.2</span></span>

* <span data-ttu-id="0d110-109">セキュリティ修正プログラム: ~/.nuget 内で作成されたファイルに対するアクセス許可の範囲が広すぎる [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span><span class="sxs-lookup"><span data-stu-id="0d110-109">Security Fix: Permissions on files created inside ~/.nuget are too open [#7673](https://github.com/NuGet/Home/issues/7673) [CVE-2019-0757](https://portal.msrc.microsoft.com/en-us/security-guidance/advisory/CVE-2019-0757)</span></span>

## <a name="summary-whats-new-in-473"></a><span data-ttu-id="0d110-110">概要:4.7.3 の新機能</span><span class="sxs-lookup"><span data-stu-id="0d110-110">Summary: What's New in 4.7.3</span></span>

* <span data-ttu-id="0d110-111">セキュリティ修正プログラム: NUPKG ディレクトリより上の NUPKG 内のファイルに相対パスが含まれる場合がある [#7906](https://github.com/NuGet/Home/issues/7906)</span><span class="sxs-lookup"><span data-stu-id="0d110-111">Security Fix: Files inside of NUPKGs can have a relative path above the NUPKG directory [#7906](https://github.com/NuGet/Home/issues/7906)</span></span>

## <a name="known-issues"></a><span data-ttu-id="0d110-112">既知の問題</span><span class="sxs-lookup"><span data-stu-id="0d110-112">Known issues</span></span>

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a><span data-ttu-id="0d110-113">右クリックのコンテキスト メニューで `Migrate packages.config to PackageReference...` オプションを使用できない</span><span class="sxs-lookup"><span data-stu-id="0d110-113">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span>

#### <a name="issue"></a><span data-ttu-id="0d110-114">懸案事項</span><span class="sxs-lookup"><span data-stu-id="0d110-114">Issue</span></span>

<span data-ttu-id="0d110-115">プロジェクトを最初に開いたとき、NuGet 操作を行うまで NuGet が初期化されていない場合があります。</span><span class="sxs-lookup"><span data-stu-id="0d110-115">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="0d110-116">これにより、`packages.config` または `References` 上の右クリックのコンテキスト メニューで、移行オプションが表示されません。</span><span class="sxs-lookup"><span data-stu-id="0d110-116">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span>

#### <a name="workaround"></a><span data-ttu-id="0d110-117">回避策</span><span class="sxs-lookup"><span data-stu-id="0d110-117">Workaround</span></span>

<span data-ttu-id="0d110-118">次の NuGet アクションのいずれかを実行します。</span><span class="sxs-lookup"><span data-stu-id="0d110-118">Perform any one of the following NuGet actions:</span></span>
* <span data-ttu-id="0d110-119">パッケージ マネージャー UI を開く - `References` を右クリックし、`Manage NuGet Packages...` を選択する</span><span class="sxs-lookup"><span data-stu-id="0d110-119">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span>
* <span data-ttu-id="0d110-120">パッケージ マネージャー コンソールを開く - `Tools > NuGet Package Manager` から、`Package Manager Console` を選択する</span><span class="sxs-lookup"><span data-stu-id="0d110-120">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span>
* <span data-ttu-id="0d110-121">NuGet 復元を実行する - ソリューション エクスプローラーのソリューション ノードを右クリックし、`Restore NuGet Packages` を選択する</span><span class="sxs-lookup"><span data-stu-id="0d110-121">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span>
* <span data-ttu-id="0d110-122">NuGet 復元もトリガーするプロジェクトをビルドする</span><span class="sxs-lookup"><span data-stu-id="0d110-122">Build the project which also triggers NuGet restore</span></span>

<span data-ttu-id="0d110-123">これで、移行オプションを表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="0d110-123">You should now be able to see the migration option.</span></span> <span data-ttu-id="0d110-124">このオプションは ASP.NET と C++ のプロジェクト タイプではサポートされておらず、表示されません。</span><span class="sxs-lookup"><span data-stu-id="0d110-124">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="0d110-125">.NET Framework と NuGet での .NET Standard 2.0 の問題</span><span class="sxs-lookup"><span data-stu-id="0d110-125">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span>

<span data-ttu-id="0d110-126">.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="0d110-126">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="0d110-127">[このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="0d110-127">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="0d110-128">このリリースで修正された主な問題</span><span class="sxs-lookup"><span data-stu-id="0d110-128">Top issues fixed in this release</span></span>

### <a name="bugs"></a><span data-ttu-id="0d110-129">バグ</span><span class="sxs-lookup"><span data-stu-id="0d110-129">Bugs</span></span>

* <span data-ttu-id="0d110-130">.Net Core プロジェクト システムで、NuGet がデッドロック状態になる (新しい回帰)。</span><span class="sxs-lookup"><span data-stu-id="0d110-130">NuGet runs into a deadlock in .Net Core project system (new regression).</span></span><span data-ttu-id="0d110-131"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span><span class="sxs-lookup"><span data-stu-id="0d110-131"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span></span>
* <span data-ttu-id="0d110-132">パック: TfmSpecificPackageFile をグロビング パスと共に使用すると、PackagePath が正しく構成されない - [#6726](https://github.com/NuGet/Home/issues/6726)</span><span class="sxs-lookup"><span data-stu-id="0d110-132">Pack: PackagePath is constructed incorrectly if TfmSpecificPackageFile is used with globbing paths - [#6726](https://github.com/NuGet/Home/issues/6726)</span></span>
* <span data-ttu-id="0d110-133">パック: ispackable が明示的に設定されていない限り、Web API プロジェクトでパッケージを作成できない。</span><span class="sxs-lookup"><span data-stu-id="0d110-133">Pack: web api project cannot create package unless ispackable is explicitly set.</span></span><span data-ttu-id="0d110-134"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span><span class="sxs-lookup"><span data-stu-id="0d110-134"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span></span>
* <span data-ttu-id="0d110-135">VS UI と PMC で、新しいパッケージを表示するのに 30 分かかる (nuget.exe ではすぐに表示される) - [#6657](https://github.com/NuGet/Home/issues/6657)</span><span class="sxs-lookup"><span data-stu-id="0d110-135">VS UI and PMC take 30min to see new package (nuget.exe sees it right away) - [#6657](https://github.com/NuGet/Home/issues/6657)</span></span>
* <span data-ttu-id="0d110-136">署名: SignatureUtility.GetCertificateChain(...) ですべてのチェーンの状態がチェックされない - [#6565](https://github.com/NuGet/Home/issues/6565)</span><span class="sxs-lookup"><span data-stu-id="0d110-136">Signing:  SignatureUtility.GetCertificateChain(...) does not check all chain statuses - [#6565](https://github.com/NuGet/Home/issues/6565)</span></span>
* <span data-ttu-id="0d110-137">署名: DER GeneralizedTime 処理を向上させる - [#6564](https://github.com/NuGet/Home/issues/6564)</span><span class="sxs-lookup"><span data-stu-id="0d110-137">Signing:  improve DER GeneralizedTime handling - [#6564](https://github.com/NuGet/Home/issues/6564)</span></span>
* <span data-ttu-id="0d110-138">署名: 改ざんされたパッケージをインストールするときに、VS で NU3002 エラーが表示されない - [#6337](https://github.com/NuGet/Home/issues/6337)</span><span class="sxs-lookup"><span data-stu-id="0d110-138">Signing: VS does not show a NU3002 error when installing a tampered package - [#6337](https://github.com/NuGet/Home/issues/6337)</span></span>
* <span data-ttu-id="0d110-139">lockFile.GetLibrary では大文字と小文字が区別される - [#6500](https://github.com/NuGet/Home/issues/6500)</span><span class="sxs-lookup"><span data-stu-id="0d110-139">lockFile.GetLibrary is case sensitive - [#6500](https://github.com/NuGet/Home/issues/6500)</span></span>
* <span data-ttu-id="0d110-140">インストール/更新の復元コードと復元コードのパスが一致しない - [#3471](https://github.com/NuGet/Home/issues/3471)</span><span class="sxs-lookup"><span data-stu-id="0d110-140">Install/update restore code and Restore code paths are not consistent - [#3471](https://github.com/NuGet/Home/issues/3471)</span></span>
* <span data-ttu-id="0d110-141">ソリューション PackageManager バージョン ComboBox で、キーボードを使用して区切りを選択できる - [#2606](https://github.com/NuGet/Home/issues/2606)</span><span class="sxs-lookup"><span data-stu-id="0d110-141">Solution PackageManager Version ComboBox can select separator via keyboard - [#2606](https://github.com/NuGet/Home/issues/2606)</span></span>
* <span data-ttu-id="0d110-142">ソースのサービス インデックスを読み込めない `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException:応答状態コードが成功を示さない: 403 (禁止) - [#2530](https://github.com/NuGet/Home/issues/2530)</span><span class="sxs-lookup"><span data-stu-id="0d110-142">Unable to load the service index for source `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: Response status code does not indicate success: 403 (Forbidden) - [#2530](https://github.com/NuGet/Home/issues/2530)</span></span>

### <a name="dcrs"></a><span data-ttu-id="0d110-143">DCR</span><span class="sxs-lookup"><span data-stu-id="0d110-143">DCRs</span></span>

* <span data-ttu-id="0d110-144">X-NuGet-Session-Id ヘッダーを生成し、要求全体で関連付ける [機能提案] - [#5330](https://github.com/NuGet/Home/issues/5330)</span><span class="sxs-lookup"><span data-stu-id="0d110-144">Emit X-NuGet-Session-Id header to correlate across requests [feature proposal] - [#5330](https://github.com/NuGet/Home/issues/5330)</span></span>
* <span data-ttu-id="0d110-145">IV の API を使用して、Visual Studio 上で実行される復元操作の実行を待機するための方法を公開する。</span><span class="sxs-lookup"><span data-stu-id="0d110-145">Expose a way to wait on running restore operation running in Visual Studio via IVs apis.</span></span><span data-ttu-id="0d110-146"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span><span class="sxs-lookup"><span data-stu-id="0d110-146"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span></span>
* <span data-ttu-id="0d110-147">NuGet.exe -NoServiceEndpoint でサービス URL のサフィックスの追加を回避する - [#6586](https://github.com/NuGet/Home/issues/6586)</span><span class="sxs-lookup"><span data-stu-id="0d110-147">NuGet.exe -NoServiceEndpoint will avoid appending service url suffix - [#6586](https://github.com/NuGet/Home/issues/6586)</span></span>
* <span data-ttu-id="0d110-148">補足バージョンにコミット ハッシュを追加する - [#6492](https://github.com/NuGet/Home/issues/6492)</span><span class="sxs-lookup"><span data-stu-id="0d110-148">add commit hash to informational version - [#6492](https://github.com/NuGet/Home/issues/6492)</span></span>
* <span data-ttu-id="0d110-149">署名: リポジトリの署名/副署名の削除を可能にする - [#6646](https://github.com/NuGet/Home/issues/6646)</span><span class="sxs-lookup"><span data-stu-id="0d110-149">Signing:  enable removal of repository signature/countersignature - [#6646](https://github.com/NuGet/Home/issues/6646)</span></span>
* <span data-ttu-id="0d110-150">署名: リポジトリの署名/副署名を削除するための API - [#6589](https://github.com/NuGet/Home/issues/6589)</span><span class="sxs-lookup"><span data-stu-id="0d110-150">Signing:  API for stripping repository signature/countersignature - [#6589](https://github.com/NuGet/Home/issues/6589)</span></span>
* <span data-ttu-id="0d110-151">VS でソース情報をログに記録する - [#6527](https://github.com/NuGet/Home/issues/6527)</span><span class="sxs-lookup"><span data-stu-id="0d110-151">Log source information in VS - [#6527](https://github.com/NuGet/Home/issues/6527)</span></span>
* <span data-ttu-id="0d110-152">/tools を TFM および RID でのみフィルター処理して、設定の XML を /tools フォルダーに配置できるようにする - [#6197](https://github.com/NuGet/Home/issues/6197)</span><span class="sxs-lookup"><span data-stu-id="0d110-152">Filter /tools on only TFM and RID, so the settings XML can be put in /tools folder - [#6197](https://github.com/NuGet/Home/issues/6197)</span></span>
* <span data-ttu-id="0d110-153">パック コマンドが . で始まるファイルを除外した場合、警告する</span><span class="sxs-lookup"><span data-stu-id="0d110-153">Warn when Pack command excludes a file that starts with .</span></span><span data-ttu-id="0d110-154">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span><span class="sxs-lookup"><span data-stu-id="0d110-154">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span></span>

[<span data-ttu-id="0d110-155">このリリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="0d110-155">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
