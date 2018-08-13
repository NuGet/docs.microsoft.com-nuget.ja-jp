---
title: NuGet 4.7 RTM リリース ノート
description: NuGet 4.7.0 のリリース ノートです。既知の問題、バグ修正、追加機能、および DCR を含みます。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 5/14/2018
ms.topic: conceptual
ms.openlocfilehash: 79be74f9c54e27bf2c08e83c7adf81d1f96ce79a
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508164"
---
# <a name="nuget-47-rtm-release-notes"></a><span data-ttu-id="20e4f-103">NuGet 4.7 RTM リリース ノート</span><span class="sxs-lookup"><span data-stu-id="20e4f-103">NuGet 4.7 RTM Release Notes</span></span>

<span data-ttu-id="20e4f-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) には、[NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe) が付属しています。</span><span class="sxs-lookup"><span data-stu-id="20e4f-104">[Visual Studio 2017 15.7 RTW](https://www.visualstudio.com/news/releasenotes/vs2017-relnotes) comes with [NuGet 4.7.0](https://dist.nuget.org/win-x86-commandline/v4.7.0/nuget.exe).</span></span>

## <a name="summary-whats-new-in-this-release"></a><span data-ttu-id="20e4f-105">概要: このリリースの新機能</span><span class="sxs-lookup"><span data-stu-id="20e4f-105">Summary: What's New in this Release</span></span>

* <span data-ttu-id="20e4f-106">パッケージの署名が拡張され、[リポジトリの署名付きパッケージ](https://github.com/NuGet/Home/wiki/Repository-Signatures)が有効になりました。</span><span class="sxs-lookup"><span data-stu-id="20e4f-106">We have augmented package signing to enable [Repository Signed packages](https://github.com/NuGet/Home/wiki/Repository-Signatures)</span></span>

* <span data-ttu-id="20e4f-107">Visual Studio Version 15.7 では、[packages.config 形式を使用する既存のプロジェクトを移行して、代わりに PackageReference を使用する](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference)機能が導入されました。</span><span class="sxs-lookup"><span data-stu-id="20e4f-107">With Visual Studio Version 15.7, we have introduced the capability to [migrate existing projects that use the packages.config format to use PackageReference](https://docs.microsoft.com/en-us/nuget/reference/migrate-packages-config-to-package-reference) instead.</span></span>

## <a name="known-issues"></a><span data-ttu-id="20e4f-108">既知の問題</span><span class="sxs-lookup"><span data-stu-id="20e4f-108">Known issues</span></span>

### <a name="the-migrate-packagesconfig-to-packagereference-option-is-not-available-in-the-right-click-context-menu"></a><span data-ttu-id="20e4f-109">右クリックのコンテキスト メニューで `Migrate packages.config to PackageReference...` オプションを使用できない</span><span class="sxs-lookup"><span data-stu-id="20e4f-109">The `Migrate packages.config to PackageReference...` option is not available in the right-click context menu</span></span>

#### <a name="issue"></a><span data-ttu-id="20e4f-110">懸案事項</span><span class="sxs-lookup"><span data-stu-id="20e4f-110">Issue</span></span>

<span data-ttu-id="20e4f-111">プロジェクトを最初に開いたとき、NuGet 操作を行うまで NuGet が初期化されていない場合があります。</span><span class="sxs-lookup"><span data-stu-id="20e4f-111">When a project is first opened, NuGet may not have initialized until a NuGet operation is performed.</span></span> <span data-ttu-id="20e4f-112">これにより、`packages.config` または `References` 上の右クリックのコンテキスト メニューで、移行オプションが表示されません。</span><span class="sxs-lookup"><span data-stu-id="20e4f-112">This causes the migration option to not show up in the right-click context menu on `packages.config` or `References`.</span></span>

#### <a name="workaround"></a><span data-ttu-id="20e4f-113">回避策</span><span class="sxs-lookup"><span data-stu-id="20e4f-113">Workaround</span></span>

<span data-ttu-id="20e4f-114">次の NuGet アクションのいずれかを実行します。</span><span class="sxs-lookup"><span data-stu-id="20e4f-114">Perform any one of the following NuGet actions:</span></span>
* <span data-ttu-id="20e4f-115">パッケージ マネージャー UI を開く - `References` を右クリックし、`Manage NuGet Packages...` を選択する</span><span class="sxs-lookup"><span data-stu-id="20e4f-115">Open the Package Manager UI - Right-click on `References` and select `Manage NuGet Packages...`</span></span>
* <span data-ttu-id="20e4f-116">パッケージ マネージャー コンソールを開く - `Tools > NuGet Package Manager` から、`Package Manager Console` を選択する</span><span class="sxs-lookup"><span data-stu-id="20e4f-116">Open the Package Manager Console - From `Tools > NuGet Package Manager`, select `Package Manager Console`</span></span>
* <span data-ttu-id="20e4f-117">NuGet 復元を実行する - ソリューション エクスプローラーのソリューション ノードを右クリックし、`Restore NuGet Packages` を選択する</span><span class="sxs-lookup"><span data-stu-id="20e4f-117">Run NuGet restore - Right-click on the solution node in the Solution Explorer and select `Restore NuGet Packages`</span></span>
* <span data-ttu-id="20e4f-118">NuGet 復元もトリガーするプロジェクトをビルドする</span><span class="sxs-lookup"><span data-stu-id="20e4f-118">Build the project which also triggers NuGet restore</span></span>

<span data-ttu-id="20e4f-119">これで、移行オプションを表示できるようになりました。</span><span class="sxs-lookup"><span data-stu-id="20e4f-119">You should now be able to see the migration option.</span></span> <span data-ttu-id="20e4f-120">このオプションは ASP.NET と C++ のプロジェクト タイプではサポートされておらず、表示されません。</span><span class="sxs-lookup"><span data-stu-id="20e4f-120">Note that this option is not supported and will not show up for ASP.NET and C++ project types.</span></span>

### <a name="issues-with-net-standard-20-with-net-framework--nuget"></a><span data-ttu-id="20e4f-121">.NET Framework と NuGet での .NET Standard 2.0 の問題</span><span class="sxs-lookup"><span data-stu-id="20e4f-121">Issues with .NET Standard 2.0 with .NET Framework & NuGet</span></span>

<span data-ttu-id="20e4f-122">.NET Standard とそのツールは、.NET Framework 4.6.1 をターゲットとするプロジェクトが、.NET Standard 2.0 以前をターゲットとする NuGet パッケージおよびプロジェクトを使用できるように設計されています。</span><span class="sxs-lookup"><span data-stu-id="20e4f-122">.NET Standard & its tooling was designed such that projects targeting .NET Framework 4.6.1 can consume NuGet packages & projects targeting .NET Standard 2.0 or earlier.</span></span> <span data-ttu-id="20e4f-123">[このドキュメント](https://github.com/dotnet/standard/issues/481)では、そのシナリオに関連する問題の概要、それらの問題を解決する計画、そのツールの今日の状態で展開できる解決策について説明します。</span><span class="sxs-lookup"><span data-stu-id="20e4f-123">[This document](https://github.com/dotnet/standard/issues/481) summarizes the issues around that scenario, the plan for addressing them, and workarounds you can deploy with today's state of the tooling.</span></span>

## <a name="top-issues-fixed-in-this-release"></a><span data-ttu-id="20e4f-124">このリリースで修正された主な問題</span><span class="sxs-lookup"><span data-stu-id="20e4f-124">Top issues fixed in this release</span></span>

### <a name="bugs"></a><span data-ttu-id="20e4f-125">バグ</span><span class="sxs-lookup"><span data-stu-id="20e4f-125">Bugs</span></span>

* <span data-ttu-id="20e4f-126">.Net Core プロジェクト システムで、NuGet がデッドロック状態になる (新しい回帰)。</span><span class="sxs-lookup"><span data-stu-id="20e4f-126">NuGet runs into a deadlock in .Net Core project system (new regression).</span></span><span data-ttu-id="20e4f-127"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span><span class="sxs-lookup"><span data-stu-id="20e4f-127"> - [#6733](https://github.com/NuGet/Home/issues/6733)</span></span>
* <span data-ttu-id="20e4f-128">パック: TfmSpecificPackageFile をグロビング パスと共に使用すると、PackagePath が正しく構成されない - [#6726](https://github.com/NuGet/Home/issues/6726)</span><span class="sxs-lookup"><span data-stu-id="20e4f-128">Pack: PackagePath is constructed incorrectly if TfmSpecificPackageFile is used with globbing paths - [#6726](https://github.com/NuGet/Home/issues/6726)</span></span>
* <span data-ttu-id="20e4f-129">パック: ispackable が明示的に設定されていない限り、Web API プロジェクトでパッケージを作成できない。</span><span class="sxs-lookup"><span data-stu-id="20e4f-129">Pack: web api project cannot create package unless ispackable is explicitly set.</span></span><span data-ttu-id="20e4f-130"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span><span class="sxs-lookup"><span data-stu-id="20e4f-130"> - [#6156](https://github.com/NuGet/Home/issues/6156)</span></span>
* <span data-ttu-id="20e4f-131">VS UI と PMC で、新しいパッケージを表示するのに 30 分かかる (nuget.exe ではすぐに表示される) - [#6657](https://github.com/NuGet/Home/issues/6657)</span><span class="sxs-lookup"><span data-stu-id="20e4f-131">VS UI and PMC take 30min to see new package (nuget.exe sees it right away) - [#6657](https://github.com/NuGet/Home/issues/6657)</span></span>
* <span data-ttu-id="20e4f-132">署名: SignatureUtility.GetCertificateChain(...) ですべてのチェーンの状態がチェックされない - [#6565](https://github.com/NuGet/Home/issues/6565)</span><span class="sxs-lookup"><span data-stu-id="20e4f-132">Signing:  SignatureUtility.GetCertificateChain(...) does not check all chain statuses - [#6565](https://github.com/NuGet/Home/issues/6565)</span></span>
* <span data-ttu-id="20e4f-133">署名: DER GeneralizedTime 処理を向上させる - [#6564](https://github.com/NuGet/Home/issues/6564)</span><span class="sxs-lookup"><span data-stu-id="20e4f-133">Signing:  improve DER GeneralizedTime handling - [#6564](https://github.com/NuGet/Home/issues/6564)</span></span>
* <span data-ttu-id="20e4f-134">署名: 改ざんされたパッケージをインストールするときに、VS で NU3002 エラーが表示されない - [#6337](https://github.com/NuGet/Home/issues/6337)</span><span class="sxs-lookup"><span data-stu-id="20e4f-134">Signing: VS does not show a NU3002 error when installing a tampered package - [#6337](https://github.com/NuGet/Home/issues/6337)</span></span>
* <span data-ttu-id="20e4f-135">lockFile.GetLibrary では大文字と小文字が区別される - [#6500](https://github.com/NuGet/Home/issues/6500)</span><span class="sxs-lookup"><span data-stu-id="20e4f-135">lockFile.GetLibrary is case sensitive - [#6500](https://github.com/NuGet/Home/issues/6500)</span></span>
* <span data-ttu-id="20e4f-136">インストール/更新の復元コードと復元コードのパスが一致しない - [#3471](https://github.com/NuGet/Home/issues/3471)</span><span class="sxs-lookup"><span data-stu-id="20e4f-136">Install/update restore code and Restore code paths are not consistent - [#3471](https://github.com/NuGet/Home/issues/3471)</span></span>
* <span data-ttu-id="20e4f-137">ソリューション PackageManager バージョン ComboBox で、キーボードを使用して区切りを選択できる - [#2606](https://github.com/NuGet/Home/issues/2606)</span><span class="sxs-lookup"><span data-stu-id="20e4f-137">Solution PackageManager Version ComboBox can select separator via keyboard - [#2606](https://github.com/NuGet/Home/issues/2606)</span></span>
* <span data-ttu-id="20e4f-138">ソース `https://www.myget.org/F/<id>` に対してサービス インデックスを読み込めない ---> System.Net.Http.HttpRequestException: 応答の状態コードは成功を示していません: 403 (禁止) - [#2530](https://github.com/NuGet/Home/issues/2530)</span><span class="sxs-lookup"><span data-stu-id="20e4f-138">Unable to load the service index for source `https://www.myget.org/F/<id>` ---> System.Net.Http.HttpRequestException: Response status code does not indicate success: 403 (Forbidden) - [#2530](https://github.com/NuGet/Home/issues/2530)</span></span>

### <a name="dcrs"></a><span data-ttu-id="20e4f-139">DCR</span><span class="sxs-lookup"><span data-stu-id="20e4f-139">DCRs</span></span>

* <span data-ttu-id="20e4f-140">X-NuGet-Session-Id ヘッダーを生成し、要求全体で関連付ける [機能提案] - [#5330](https://github.com/NuGet/Home/issues/5330)</span><span class="sxs-lookup"><span data-stu-id="20e4f-140">Emit X-NuGet-Session-Id header to correlate across requests [feature proposal] - [#5330](https://github.com/NuGet/Home/issues/5330)</span></span>
* <span data-ttu-id="20e4f-141">IV の API を使用して、Visual Studio 上で実行される復元操作の実行を待機するための方法を公開する。</span><span class="sxs-lookup"><span data-stu-id="20e4f-141">Expose a way to wait on running restore operation running in Visual Studio via IVs apis.</span></span><span data-ttu-id="20e4f-142"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span><span class="sxs-lookup"><span data-stu-id="20e4f-142"> - [#6029](https://github.com/NuGet/Home/issues/6029)</span></span>
* <span data-ttu-id="20e4f-143">NuGet.exe -NoServiceEndpoint でサービス URL のサフィックスの追加を回避する - [#6586](https://github.com/NuGet/Home/issues/6586)</span><span class="sxs-lookup"><span data-stu-id="20e4f-143">NuGet.exe -NoServiceEndpoint will avoid appending service url suffix - [#6586](https://github.com/NuGet/Home/issues/6586)</span></span>
* <span data-ttu-id="20e4f-144">補足バージョンにコミット ハッシュを追加する - [#6492](https://github.com/NuGet/Home/issues/6492)</span><span class="sxs-lookup"><span data-stu-id="20e4f-144">add commit hash to informational version - [#6492](https://github.com/NuGet/Home/issues/6492)</span></span>
* <span data-ttu-id="20e4f-145">署名: リポジトリの署名/副署名の削除を可能にする - [#6646](https://github.com/NuGet/Home/issues/6646)</span><span class="sxs-lookup"><span data-stu-id="20e4f-145">Signing:  enable removal of repository signature/countersignature - [#6646](https://github.com/NuGet/Home/issues/6646)</span></span>
* <span data-ttu-id="20e4f-146">署名: リポジトリの署名/副署名を削除するための API - [#6589](https://github.com/NuGet/Home/issues/6589)</span><span class="sxs-lookup"><span data-stu-id="20e4f-146">Signing:  API for stripping repository signature/countersignature - [#6589](https://github.com/NuGet/Home/issues/6589)</span></span>
* <span data-ttu-id="20e4f-147">VS でソース情報をログに記録する - [#6527](https://github.com/NuGet/Home/issues/6527)</span><span class="sxs-lookup"><span data-stu-id="20e4f-147">Log source information in VS - [#6527](https://github.com/NuGet/Home/issues/6527)</span></span>
* <span data-ttu-id="20e4f-148">/tools を TFM および RID でのみフィルター処理して、設定の XML を /tools フォルダーに配置できるようにする - [#6197](https://github.com/NuGet/Home/issues/6197)</span><span class="sxs-lookup"><span data-stu-id="20e4f-148">Filter /tools on only TFM and RID, so the settings XML can be put in /tools folder - [#6197](https://github.com/NuGet/Home/issues/6197)</span></span>
* <span data-ttu-id="20e4f-149">パック コマンドが . で始まるファイルを除外した場合、警告する</span><span class="sxs-lookup"><span data-stu-id="20e4f-149">Warn when Pack command excludes a file that starts with .</span></span><span data-ttu-id="20e4f-150">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span><span class="sxs-lookup"><span data-stu-id="20e4f-150">  - [#3308](https://github.com/NuGet/Home/issues/3308)</span></span>

[<span data-ttu-id="20e4f-151">このリリースで修正されたすべての問題一覧</span><span class="sxs-lookup"><span data-stu-id="20e4f-151">List of all issues fixed in this release</span></span>](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%224.7")
