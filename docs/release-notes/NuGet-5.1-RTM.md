---
ms.openlocfilehash: 48306e77a017c11fa7dc0d695e0177edf4e79d1e
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975836"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="c08cc-101">NuGet 5.1 リリース ノート</span><span class="sxs-lookup"><span data-stu-id="c08cc-101">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="c08cc-102">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="c08cc-102">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="c08cc-103">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="c08cc-103">NuGet version</span></span> | <span data-ttu-id="c08cc-104">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="c08cc-104">Available in Visual Studio version</span></span>| <span data-ttu-id="c08cc-105">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="c08cc-105">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="c08cc-106">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="c08cc-106">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="c08cc-107">Visual Studio 2019 バージョン 16.1</span><span class="sxs-lookup"><span data-stu-id="c08cc-107">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="c08cc-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="c08cc-108">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="c08cc-109"><sup>1</sup>.NET Core ワークロードと共に Visual Studio 2019 のインストール</span><span class="sxs-lookup"><span data-stu-id="c08cc-109"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="c08cc-110"><sup>2</sup>.NET Core ワークロードと共に Visual Studio 2019 と省略可能なインストールとして利用可能</span><span class="sxs-lookup"><span data-stu-id="c08cc-110"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="c08cc-111">概要:5.1 の新機能新機能</span><span class="sxs-lookup"><span data-stu-id="c08cc-111">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="c08cc-112">適切な統合 CI/CD ワークフロー - 許可するように既に存在する場合は、パッケージのプッシュをスキップするサポート[#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="c08cc-112">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="c08cc-113">Visual Studio では、便利なリンクを今すぐでは、パッケージの nuget.org ギャラリー ページ - [# から 5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="c08cc-113">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="c08cc-114">などの新しいアセットは .NET Core 3.0 のサポート[Targeting Pack](https://github.com/dotnet/cli/issues/10006)と[ランタイム パック](https://github.com/dotnet/cli/issues/10007)</span><span class="sxs-lookup"><span data-stu-id="c08cc-114">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="c08cc-115">NuGet の pack と restore サポートを対象として、ランタイム パッケージ参照を有効にする FrameworkReferences [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="c08cc-115">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="c08cc-116">PackageDownload - でのサポート「ダウンロードのみ」パッケージ シナリオ[#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="c08cc-116">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="c08cc-117">Exlcude ランタイムと復元 (&)、検索結果からパックを対象とするグラフを使用して PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span><span class="sxs-lookup"><span data-stu-id="c08cc-117">Exlcude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="c08cc-118">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="c08cc-118">Issues fixed in this release</span></span>

<span data-ttu-id="c08cc-119">**バグ**</span><span class="sxs-lookup"><span data-stu-id="c08cc-119">**Bugs**</span></span>

* <span data-ttu-id="c08cc-120">プラグイン: 例外の詳細は、プラグインの作成 - 中に失われた[#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="c08cc-120">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="c08cc-121">排他の下限の PackageReference の範囲では、ソースのいずれかの下限の境界が存在する場合は機能しません。</span><span class="sxs-lookup"><span data-stu-id="c08cc-121">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="c08cc-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="c08cc-122"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="c08cc-123">向上 IsPackableFalseError メッセージ - [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="c08cc-123">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="c08cc-124">ロック ファイルのロックを再生成ファイル プロジェクト グラフが変更されたときにパッケージ化[#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="c08cc-124">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="c08cc-125">プロジェクト システムのバグ:自動を取得する Nuget パッケージの削除 - [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="c08cc-125">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="c08cc-126">FrameworkReference を返すためのターゲットの追加 CollectPackageDownloads および CollectPackageReferences - と同様に[#8005](https://github.com/NuGet/Home/issues/8005)</span><span class="sxs-lookup"><span data-stu-id="c08cc-126">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="c08cc-127">HTTP キャッシュ:RepositoryResources リソースは、バージョン管理された方法でキャッシュされません[#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="c08cc-127">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="c08cc-128">ログ記録: - 詳細な例外の呼び出し履歴は報告されません[#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="c08cc-128">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="c08cc-129">-HTTPS を使用するすべての NuGet Docs の Url を変更する[#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="c08cc-129">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="c08cc-130">NU3024 警告メッセージの改善[#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="c08cc-130">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="c08cc-131">ロック ファイルが更新されていないときに削除するには、packagereference [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="c08cc-131">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="c08cc-132">Nuspec - で licenseurl とライセンスの要素を検証するときに、エラー ケースの処理を向上させる[#7915](https://github.com/NuGet/Home/issues/7915)</span><span class="sxs-lookup"><span data-stu-id="c08cc-132">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="c08cc-133">タブ ヘッダーをクリック「ファイルの場所を開く」の結果エラー - PM UI の右クリック[#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="c08cc-133">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="c08cc-134">プラグイン: ログ - プラグイン プロセスの終了時に[#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="c08cc-134">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="c08cc-135">プラグイン: ログ記録の datetime 値の高い衝突率[#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="c08cc-135">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="c08cc-136">LicenseExpression - で、nuspec でが失敗した Manifest.ReadFrom [#7894](https://github.com/NuGet/Home/issues/7894)</span><span class="sxs-lookup"><span data-stu-id="c08cc-136">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="c08cc-137">RestoreLockedMode:ProjectReference がカスタム AssemblyName - プロジェクトに参照するときに予期しない NU1004 [#7889](https://github.com/NuGet/Home/issues/7889)</span><span class="sxs-lookup"><span data-stu-id="c08cc-137">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="c08cc-138">例外のプラグインの起動が失敗したときに、適切なエラー メッセージ[#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="c08cc-138">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="c08cc-139">NoOp 復元を行うときに避ける \*. obj ディレクトリ - dgspec.json 書き込み[#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="c08cc-139">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="c08cc-140">GeneratePathProperty が大文字と小文字の不一致 - でプロパティを生成に失敗する場合は true を = [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="c08cc-140">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="c08cc-141">設定: パッケージ ソース パスに無効な文字がクラッシュする - VS [#7820](https://github.com/NuGet/Home/issues/7820)</span><span class="sxs-lookup"><span data-stu-id="c08cc-141">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="c08cc-142">ロック ファイルが削除された場合の復元は、NoOp にロック ファイルを生成しません[#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="c08cc-142">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="c08cc-143">ライセンスの URL と読み取り - メタデータ エラー ライセンス原因[#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="c08cc-143">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="c08cc-144">未処理の例外で V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span><span class="sxs-lookup"><span data-stu-id="c08cc-144">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="c08cc-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="c08cc-145">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="c08cc-146">更新の署名の関連するシナリオを反映するように、エラーと警告 docs [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="c08cc-146">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="c08cc-147">アセット ファイルがプロジェクトの移動をより簡単には、有効にする相対パスを使用する必要があります[#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="c08cc-147">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="c08cc-148">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="c08cc-148">**DCRs**</span></span>

* <span data-ttu-id="c08cc-149">プラグイン: - 診断ログの記録を有効にする[#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="c08cc-149">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="c08cc-150">NetStandard 2.1 - make Tizen 6 マップ[#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="c08cc-150">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="c08cc-151">**[このリリースでは、5.1 RTM で修正されたすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="c08cc-151">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
