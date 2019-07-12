---
title: NuGet 5.1 RTM リリース ノート
description: 新機能、バグの修正、および Dcr を含む NuGet 5.1 リリース ノート。
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 384145947b19af6577dc1255985df1a361c72bb5
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842578"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="9ebf3-103">NuGet 5.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="9ebf3-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="9ebf3-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="9ebf3-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="9ebf3-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="9ebf3-105">NuGet version</span></span> | <span data-ttu-id="9ebf3-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="9ebf3-106">Available in Visual Studio version</span></span>| <span data-ttu-id="9ebf3-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9ebf3-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="9ebf3-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="9ebf3-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="9ebf3-109">Visual Studio 2019 バージョン 16.1</span><span class="sxs-lookup"><span data-stu-id="9ebf3-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="9ebf3-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="9ebf3-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="9ebf3-111"><sup>1</sup>.NET Core ワークロードと共に Visual Studio 2019 のインストール</span><span class="sxs-lookup"><span data-stu-id="9ebf3-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="9ebf3-112"><sup>2</sup>.NET Core ワークロードと共に Visual Studio 2019 と省略可能なインストールとして利用可能</span><span class="sxs-lookup"><span data-stu-id="9ebf3-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="9ebf3-113">概要:5.1 の新機能新機能</span><span class="sxs-lookup"><span data-stu-id="9ebf3-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="9ebf3-114">適切な統合 CI/CD ワークフロー - 許可するように既に存在する場合は、パッケージのプッシュをスキップするサポート[#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="9ebf3-115">Visual Studio では、便利なリンクを今すぐでは、パッケージの nuget.org ギャラリー ページ - [# から 5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="9ebf3-116">などの新しいアセットは .NET Core 3.0 のサポート[Targeting Pack](https://github.com/dotnet/cli/issues/10006)と[ランタイム パック](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="9ebf3-117">NuGet の pack と restore サポートを対象として、ランタイム パッケージ参照を有効にする FrameworkReferences [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="9ebf3-118">PackageDownload - でのサポート「ダウンロードのみ」パッケージ シナリオ[#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="9ebf3-119">Exlcude ランタイムと復元 (&)、検索結果からパックを対象とするグラフを使用して PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-119">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="9ebf3-120">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="9ebf3-120">Issues fixed in this release</span></span>

<span data-ttu-id="9ebf3-121">**バグ**</span><span class="sxs-lookup"><span data-stu-id="9ebf3-121">**Bugs**</span></span>

* <span data-ttu-id="9ebf3-122">プラグイン: 例外の詳細は、プラグインの作成 - 中に失われた[#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="9ebf3-123">排他の下限の PackageReference の範囲では、ソースのいずれかの下限の境界が存在する場合は機能しません。</span><span class="sxs-lookup"><span data-stu-id="9ebf3-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="9ebf3-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="9ebf3-125">向上 IsPackableFalseError メッセージ - [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="9ebf3-126">ロック ファイルのロックを再生成ファイル プロジェクト グラフが変更されたときにパッケージ化[#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="9ebf3-127">プロジェクト システムのバグ:自動を取得する Nuget パッケージの削除 - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="9ebf3-128">FrameworkReference を返すためのターゲットの追加 CollectPackageDownloads および CollectPackageReferences - と同様に[#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="9ebf3-129">HTTP キャッシュ:RepositoryResources リソースは、バージョン管理された方法でキャッシュされません[#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="9ebf3-130">ログ記録: - 詳細な例外の呼び出し履歴は報告されません[#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="9ebf3-131">-HTTPS を使用するすべての NuGet Docs の Url を変更する[#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="9ebf3-132">NU3024 警告メッセージの改善[#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="9ebf3-133">ロック ファイルが更新されていないときに削除するには、packagereference [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="9ebf3-134">Nuspec - で licenseurl とライセンスの要素を検証するときに、エラー ケースの処理を向上させる[#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="9ebf3-135">タブ ヘッダーをクリック「ファイルの場所を開く」の結果エラー - PM UI の右クリック[#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="9ebf3-136">プラグイン: ログ - プラグイン プロセスの終了時に[#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="9ebf3-137">プラグイン: ログ記録の datetime 値の高い衝突率[#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="9ebf3-138">LicenseExpression - で、nuspec でが失敗した Manifest.ReadFrom [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="9ebf3-139">RestoreLockedMode:ProjectReference がカスタム AssemblyName - プロジェクトに参照するときに予期しない NU1004 [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="9ebf3-140">例外のプラグインの起動が失敗したときに、適切なエラー メッセージ[#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="9ebf3-141">NoOp 復元を行うときに避ける \*. obj ディレクトリ - dgspec.json 書き込み[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="9ebf3-142">GeneratePathProperty が大文字と小文字の不一致 - でプロパティを生成に失敗する場合は true を = [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="9ebf3-143">設定: パッケージ ソース パスに無効な文字がクラッシュする - VS [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="9ebf3-144">ロック ファイルが削除された場合の復元は、NoOp にロック ファイルを生成しません[#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="9ebf3-145">ライセンスの URL と読み取り - メタデータ エラー ライセンス原因[#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="9ebf3-146">未処理の例外で V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="9ebf3-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="9ebf3-148">更新の署名の関連するシナリオを反映するように、エラーと警告 docs [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="9ebf3-149">アセット ファイルがプロジェクトの移動をより簡単には、有効にする相対パスを使用する必要があります[#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="9ebf3-150">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="9ebf3-150">**DCRs**</span></span>

* <span data-ttu-id="9ebf3-151">プラグイン: - 診断ログの記録を有効にする[#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="9ebf3-152">NetStandard 2.1 - make Tizen 6 マップ[#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="9ebf3-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="9ebf3-153">**[このリリースでは、5.1 RTM で修正されたすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="9ebf3-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
