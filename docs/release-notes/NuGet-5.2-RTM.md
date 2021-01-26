---
title: NuGet 5.2 RTM リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.2 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776212"
---
# <a name="nuget-52-release-notes"></a><span data-ttu-id="d214e-103">NuGet 5.2 リリースノート</span><span class="sxs-lookup"><span data-stu-id="d214e-103">NuGet 5.2 Release Notes</span></span>

<span data-ttu-id="d214e-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="d214e-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="d214e-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="d214e-105">NuGet version</span></span> | <span data-ttu-id="d214e-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="d214e-106">Available in Visual Studio version</span></span>| <span data-ttu-id="d214e-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="d214e-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="d214e-108">**5.2.0 以降**</span><span class="sxs-lookup"><span data-stu-id="d214e-108">**5.2.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="d214e-109">Visual Studio 2019 バージョン 16.2</span><span class="sxs-lookup"><span data-stu-id="d214e-109">Visual Studio 2019 version 16.2</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="d214e-110">[2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="d214e-110">[2.1.80X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="d214e-111"><sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="d214e-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="d214e-112"><sup>2</sup>.NET Core ワークロードを含む Visual Studio 2019 を使用したオプションのインストールとして利用可能</span><span class="sxs-lookup"><span data-stu-id="d214e-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-52"></a><span data-ttu-id="d214e-113">概要: 5.2 の新機能</span><span class="sxs-lookup"><span data-stu-id="d214e-113">Summary: What's New in 5.2</span></span>

* <span data-ttu-id="d214e-114">Linux & Mac [#7341](https://github.com/NuGet/Home/issues/7341)でのパスの問題により、NuGet 操作エラーが発生する可能性のある重大なバグを修正しました</span><span class="sxs-lookup"><span data-stu-id="d214e-114">Fixed a critical bug that caused occasional NuGet operation failures due to path issues on Linux & Mac - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

* <span data-ttu-id="d214e-115">Visual Studio の NuGet パッケージマネージャー UI を使用したパッケージの参照時の UI の応答性の向上 (低速なソースの場合は特に顕著)- [#8039](https://github.com/NuGet/Home/issues/8039)</span><span class="sxs-lookup"><span data-stu-id="d214e-115">Improved UI responsiveness when browsing packages using the NuGet package manager UI in Visual Studio especially noticeable for slow sources - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="d214e-116">ロックファイル ([#8187](https://github.com/NuGet/Home/issues/8187)、[#8160](https://github.com/NuGet/Home/issues/8160)、[#8114](https://github.com/NuGet/Home/issues/8114)、[#7840](https://github.com/NuGet/Home/issues/7840)) および認証プラグイン ([#8300](https://github.com/NuGet/Home/issues/8300)、[#8271、#8269](https://github.com/NuGet/Home/issues/8271)[、](https://github.com/NuGet/Home/issues/8269)[#8210](https://github.com/NuGet/Home/issues/8210)、[#8198](https://github.com/NuGet/Home/issues/8198)、[#7845](https://github.com/NuGet/Home/issues/7845)) に対する信頼性の高い修正プログラム</span><span class="sxs-lookup"><span data-stu-id="d214e-116">Tons of reliability fixes for lock file ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) and authentication plugin ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="d214e-117">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="d214e-117">Issues fixed in this release</span></span>

<span data-ttu-id="d214e-118">**バグ**</span><span class="sxs-lookup"><span data-stu-id="d214e-118">**Bugs**</span></span>

* <span data-ttu-id="d214e-119">パフォーマンス: パッケージマネージャーコンソール: UI 遅延更新 "Default project" combobox selected value- [#8235](https://github.com/NuGet/Home/issues/8235)</span><span class="sxs-lookup"><span data-stu-id="d214e-119">Perf: Package Manager Console:  UI delay updating "Default project" combobox selected value - [#8235](https://github.com/NuGet/Home/issues/8235)</span></span>

* <span data-ttu-id="d214e-120">パフォーマンス: PM UI [#8039](https://github.com/NuGet/Home/issues/8039)のパフォーマンスが向上しました。</span><span class="sxs-lookup"><span data-stu-id="d214e-120">Perf: Performance improvements in the PM UI - [#8039](https://github.com/NuGet/Home/issues/8039)</span></span>

* <span data-ttu-id="d214e-121">Perf: [#6824](https://github.com/NuGet/Home/issues/6824) PMC で既定のプロジェクトを読み取るときの UI 遅延</span><span class="sxs-lookup"><span data-stu-id="d214e-121">Perf: UI Delay when reading Default Project in PMC - [#6824](https://github.com/NuGet/Home/issues/6824)</span></span>

* <span data-ttu-id="d214e-122">Perf: [vsfeedback] ローカルパッケージソースに対して NuGet 更新タブがフリーズする- [#6470](https://github.com/NuGet/Home/issues/6470)</span><span class="sxs-lookup"><span data-stu-id="d214e-122">Perf: [vsfeedback] NuGet Update tab freezes for a local package source - [#6470](https://github.com/NuGet/Home/issues/6470)</span></span>

* <span data-ttu-id="d214e-123">プラグイン: プラグインの起動または終了に失敗した場合、NuGet は完全なハンドシェイクのタイムアウトを待機し [#8300](https://github.com/NuGet/Home/issues/8300)</span><span class="sxs-lookup"><span data-stu-id="d214e-123">Plugins:  NuGet waits full handshake timeout if plugin fails to launch or terminates early - [#8300](https://github.com/NuGet/Home/issues/8300)</span></span>

* <span data-ttu-id="d214e-124">プラグイン: プラグイン起動エラーの diagnosability の改善- [#8271](https://github.com/NuGet/Home/issues/8271)</span><span class="sxs-lookup"><span data-stu-id="d214e-124">Plugins:  improve diagnosability of plugin launch failure - [#8271](https://github.com/NuGet/Home/issues/8271)</span></span>

* <span data-ttu-id="d214e-125">プラグイン: 組み込みプラグインの nuget.exe 検出に関する問題- [#8269](https://github.com/NuGet/Home/issues/8269)</span><span class="sxs-lookup"><span data-stu-id="d214e-125">Plugins: Issue with nuget.exe discovery of built in plugins - [#8269](https://github.com/NuGet/Home/issues/8269)</span></span>

* <span data-ttu-id="d214e-126">プラグイン: キャッシュファイルが読み取り専用ではない [#8210](https://github.com/NuGet/Home/issues/8210)</span><span class="sxs-lookup"><span data-stu-id="d214e-126">Plugins:  cache file is never read - [#8210](https://github.com/NuGet/Home/issues/8210)</span></span>

* <span data-ttu-id="d214e-127">プラグイン: "タスクが取り消されました。"</span><span class="sxs-lookup"><span data-stu-id="d214e-127">Plugins:  "A task was canceled."</span></span> <span data-ttu-id="d214e-128">復元中に認証プラグインでエラーが発生した [#8198](https://github.com/NuGet/Home/issues/8198)</span><span class="sxs-lookup"><span data-stu-id="d214e-128">errors with authentication plugin during restore - [#8198](https://github.com/NuGet/Home/issues/8198)</span></span>

* <span data-ttu-id="d214e-129">プラグインキャッシュが linux プラットフォームで断続的に検出されない- [#7845](https://github.com/NuGet/Home/issues/7845)</span><span class="sxs-lookup"><span data-stu-id="d214e-129">Plugins cache not discoverable intermittently on linux platforms - [#7845](https://github.com/NuGet/Home/issues/7845)</span></span>

* <span data-ttu-id="d214e-130">LockFile: ATF では、ターゲットフレームワークの等価性の[#8187](https://github.com/NuGet/Home/issues/8187)チェックが無効なため、FALSE の NU1004 があります</span><span class="sxs-lookup"><span data-stu-id="d214e-130">LockFile: with ATF, it has false NU1004 due to a bad target framework equality check - [#8187](https://github.com/NuGet/Home/issues/8187)</span></span>

* <span data-ttu-id="d214e-131">LockFile: '--locked-mode ' 復元フラグは、ロックファイルが空であるか、形式が正しくない場合には尊重されません [#8160](https://github.com/NuGet/Home/issues/8160)</span><span class="sxs-lookup"><span data-stu-id="d214e-131">LockFile: '--locked-mode' restore flag not respected if lock file is empty or malformed - [#8160](https://github.com/NuGet/Home/issues/8160)</span></span>

* <span data-ttu-id="d214e-132">LockFile: パッケージのロックファイル[#8114](https://github.com/NuGet/Home/issues/8114)で、カスタムアセンブリ名を持つ小文字のプロジェクトは使用しないでください</span><span class="sxs-lookup"><span data-stu-id="d214e-132">LockFile: Don't lowercase projects with custom assembly names in packages lock file - [#8114](https://github.com/NuGet/Home/issues/8114)</span></span>

* <span data-ttu-id="d214e-133">LockFile: プロジェクト参照の小文字をロックファイルに設定する- [#7840](https://github.com/NuGet/Home/issues/7840)</span><span class="sxs-lookup"><span data-stu-id="d214e-133">LockFile: Make project reference lower case in lock file  - [#7840](https://github.com/NuGet/Home/issues/7840)</span></span>

* <span data-ttu-id="d214e-134">復元: 改ざんされた署名されたパッケージをインストールすると、複数のインストールが失敗する (出力が繰り返されます)- [#8175](https://github.com/NuGet/Home/issues/8175)</span><span class="sxs-lookup"><span data-stu-id="d214e-134">Restore:  installing a tampered signed package results in multiple failed install attempts (with repeated output) - [#8175](https://github.com/NuGet/Home/issues/8175)</span></span>

* <span data-ttu-id="d214e-135">VS: ソリューションユーザーオプションが NuGet の更新後に逆シリアル化に失敗する- [#8166](https://github.com/NuGet/Home/issues/8166)</span><span class="sxs-lookup"><span data-stu-id="d214e-135">VS: solution user options fail to deserialize after NuGet update - [#8166](https://github.com/NuGet/Home/issues/8166)</span></span>

* <span data-ttu-id="d214e-136">UnitTest プロジェクトの dotnet-package はエラーを返します- [#8154](https://github.com/NuGet/Home/issues/8154)</span><span class="sxs-lookup"><span data-stu-id="d214e-136">dotnet-list-package in a UnitTest project returns an error - [#8154](https://github.com/NuGet/Home/issues/8154)</span></span>

* <span data-ttu-id="d214e-137">VS インストーラーの NuGet パッケージグループを作成する-VSIX セットアップの問題を修正する- [#8033](https://github.com/NuGet/Home/issues/8033)</span><span class="sxs-lookup"><span data-stu-id="d214e-137">Create NuGet package group for VS installer - fixing some VSIX setup problems - [#8033](https://github.com/NuGet/Home/issues/8033)</span></span>

* <span data-ttu-id="d214e-138">GeneratePackageOnBuild で NoBuild を設定することはできません。</span><span class="sxs-lookup"><span data-stu-id="d214e-138">GeneratePackageOnBuild should not set NoBuild.</span></span><span data-ttu-id="d214e-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span><span class="sxs-lookup"><span data-stu-id="d214e-139"> - [#7801](https://github.com/NuGet/Home/issues/7801)</span></span>

* <span data-ttu-id="d214e-140">Nuspec ファイルに明示的なアセンブリ参照[#7638](https://github.com/NuGet/Home/issues/7638)要素が含まれている場合、新しいオプション "-packageformat snupkg" によってエラーが生成されます。</span><span class="sxs-lookup"><span data-stu-id="d214e-140">The new option "-SymbolPackageFormat snupkg" generates an error when the .nuspec file contains an explicit assembly reference element - [#7638](https://github.com/NuGet/Home/issues/7638)</span></span>

* <span data-ttu-id="d214e-141">Nuget.exe (498, 5): エラー: パス '/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341)の一部が見つかりませんでした</span><span class="sxs-lookup"><span data-stu-id="d214e-141">NuGet.targets(498,5): error : Could not find a part of the path '/tmp/NuGetScratch - [#7341](https://github.com/NuGet/Home/issues/7341)</span></span>

<span data-ttu-id="d214e-142">**DCR**</span><span class="sxs-lookup"><span data-stu-id="d214e-142">**DCR:**</span></span>

* <span data-ttu-id="d214e-143">PackageDownload がサポートされていることを示す msbuild プロパティを追加します- [#8106](https://github.com/NuGet/Home/issues/8106)</span><span class="sxs-lookup"><span data-stu-id="d214e-143">Add an msbuild property that indicates that PackageDownload is supported - [#8106](https://github.com/NuGet/Home/issues/8106)</span></span>

* <span data-ttu-id="d214e-144">FrameworkReference: FrameworkReference による依存関係フローを抑制します。 PrivateAssets- [#7988](https://github.com/NuGet/Home/issues/7988)</span><span class="sxs-lookup"><span data-stu-id="d214e-144">FrameworkReference suppress dependency flow via FrameworkReference.PrivateAssets - [#7988](https://github.com/NuGet/Home/issues/7988)</span></span>

* <span data-ttu-id="d214e-145">パッケージ[#7351](https://github.com/NuGet/Home/issues/7351)の外部で runtime.jsを提供するメカニズム</span><span class="sxs-lookup"><span data-stu-id="d214e-145">Mechanism for supplying runtime.json outside of a package - [#7351](https://github.com/NuGet/Home/issues/7351)</span></span>

<span data-ttu-id="d214e-146">**[このリリース-5.2 RTM で修正されるすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span><span class="sxs-lookup"><span data-stu-id="d214e-146">**[List of all issues fixed in this release - 5.2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**</span></span>


