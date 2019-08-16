---
title: NuGet 5.2 RTM リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.2 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: f94bd8ddb8fac8bf47c2826bf5b417595b0efa8b
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68471185"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="00f2b-103">NuGet 5.2 リリースノート</span><span class="sxs-lookup"><span data-stu-id="00f2b-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="00f2b-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="00f2b-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="00f2b-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="00f2b-105">NuGet version</span></span> | <span data-ttu-id="00f2b-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="00f2b-106">Available in Visual Studio version</span></span>| <span data-ttu-id="00f2b-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="00f2b-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="00f2b-108">**5.2.0 以降**</span><span class="sxs-lookup"><span data-stu-id="00f2b-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="00f2b-109">Visual Studio 2019 バージョン16.2</span><span class="sxs-lookup"><span data-stu-id="00f2b-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="00f2b-110">[2.1.80 X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.40 X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="00f2b-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="00f2b-111"><sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="00f2b-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="00f2b-112"><sup>2</sup>.NET Core ワークロードを含む Visual Studio 2019 を使用したオプションのインストールとして利用可能</span><span class="sxs-lookup"><span data-stu-id="00f2b-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="00f2b-113">概要:5.2 の新機能</span><span class="sxs-lookup"><span data-stu-id="00f2b-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="00f2b-114">Linux & Mac [#7341](https://github.com/NuGet/Home/issues/7341)でのパスの問題により、NuGet 操作エラーが発生する可能性のある重大なバグを修正しました</span><span class="sxs-lookup"><span data-stu-id="00f2b-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="00f2b-115">Visual Studio の NuGet パッケージマネージャー UI を使用したパッケージの参照時の UI の応答性の向上 (低速なソースの場合は特に顕著)- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="00f2b-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="00f2b-116">ロックファイル ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) および認証プラグイン ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271](https://github.com/NuGet/Home/issues/8271)、[#8269](https://github.com/NuGet/Home/issues/8269)、[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)、[#7845](https://github.com/NuGet/Home/issues/7845)) に対する信頼性の高い修正プログラム</span><span class="sxs-lookup"><span data-stu-id="00f2b-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="00f2b-117">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="00f2b-117">Issues fixed in this release</span></span>

<span data-ttu-id="00f2b-118">**バグ**</span><span class="sxs-lookup"><span data-stu-id="00f2b-118">**Bugs**</span></span>

* <span data-ttu-id="00f2b-119">Perfパッケージマネージャーコンソール:UI 遅延更新 "Default project" combobox selected value- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="00f2b-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="00f2b-120">PerfPM UI [#8039](https://github.com/NuGet/Home/issues/8039)のパフォーマンスの向上</span><span class="sxs-lookup"><span data-stu-id="00f2b-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="00f2b-121">Perf[#6824](https://github.com/NuGet/Home/issues/6824) PMC で既定のプロジェクトを読み取るときの UI 遅延</span><span class="sxs-lookup"><span data-stu-id="00f2b-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="00f2b-122">Perf: [vsfeedback] ローカルパッケージソースに対して NuGet 更新タブがフリーズする- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="00f2b-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="00f2b-123">済みプラグインの起動または終了に失敗した場合、NuGet は完全なハンドシェイクのタイムアウトを待機し[#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="00f2b-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="00f2b-124">プラグイン: プラグイン起動エラーの diagnosability の改善- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="00f2b-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="00f2b-125">済み組み込みプラグインの nuget.exe 検出に関する問題- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="00f2b-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="00f2b-126">プラグイン: キャッシュファイルが読み取り専用ではない[#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="00f2b-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="00f2b-127">済み"タスクが取り消されました。"</span><span class="sxs-lookup"><span data-stu-id="00f2b-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="00f2b-128">復元中に認証プラグインでエラーが発生した[#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="00f2b-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="00f2b-129">プラグインキャッシュが linux プラットフォームで断続的に検出されない- [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="00f2b-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="00f2b-130">LockFile: ATF では、ターゲットフレームワークの等価性の[#8187](https://github.com/NuGet/Home/issues/8187)チェックが無効なため、FALSE の NU1004 があります</span><span class="sxs-lookup"><span data-stu-id="00f2b-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="00f2b-131">LockFile: '--locked-mode ' 復元フラグは、ロックファイルが空であるか、形式が正しくない場合には尊重されません[#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="00f2b-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="00f2b-132">LockFile:パッケージでカスタムアセンブリ名を持つ小文字のプロジェクトをロックする (ファイル[#8114](https://github.com/NuGet/Home/issues/8114)をロックする)</span><span class="sxs-lookup"><span data-stu-id="00f2b-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="00f2b-133">LockFile:プロジェクト参照の小文字をロックファイルに使用する- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="00f2b-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="00f2b-134">復元: 改ざんされた署名されたパッケージをインストールすると、複数のインストールが失敗する (出力が繰り返されます)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="00f2b-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="00f2b-135">VS: ソリューションユーザーオプションが NuGet の更新後に逆シリアル化に失敗する- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="00f2b-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="00f2b-136">UnitTest プロジェクトの dotnet-package はエラーを返します- [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="00f2b-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="00f2b-137">VS インストーラーの NuGet パッケージグループを作成する-VSIX セットアップの問題を修正する- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="00f2b-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="00f2b-138">GeneratePackageOnBuild で NoBuild を設定することはできません。</span><span class="sxs-lookup"><span data-stu-id="00f2b-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="00f2b-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="00f2b-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="00f2b-140">Nuspec ファイルに明示的なアセンブリ参照[#7638](https://github.com/NuGet/Home/issues/7638)要素が含まれている場合、新しいオプション "-packageformat snupkg" によってエラーが生成されます。</span><span class="sxs-lookup"><span data-stu-id="00f2b-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="00f2b-141">NuGet.targets(498,5): error :パス '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)の一部が見つかりませんでした</span><span class="sxs-lookup"><span data-stu-id="00f2b-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="00f2b-142">**DCR:**</span><span class="sxs-lookup"><span data-stu-id="00f2b-142">**DCR:**</span></span>

* <span data-ttu-id="00f2b-143">PackageDownload がサポートされていることを示す msbuild プロパティを追加します- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="00f2b-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="00f2b-144">FrameworkReference: FrameworkReference による依存関係フローを抑制します。 PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="00f2b-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="00f2b-145">パッケージ[#7351](https://github.com/NuGet/Home/issues/7351)の外部でランタイムを指定するための機構</span><span class="sxs-lookup"><span data-stu-id="00f2b-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="00f2b-146">**[このリリース-5.2 RTM で修正されるすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="00f2b-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


