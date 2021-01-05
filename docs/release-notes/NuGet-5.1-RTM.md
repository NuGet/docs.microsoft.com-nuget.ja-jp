---
title: NuGet 5.1 RTM リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.1 のリリースノート。
author: karann-msft
ms.author: karann
ms.date: 05/21/2019
ms.topic: conceptual
ms.openlocfilehash: 2a94360dc375ba90b90c1045f4acbcfca81fea5b
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699866"
---
# <a name="nuget-51-release-notes"></a><span data-ttu-id="a01ad-103">NuGet 5.1 リリースノート</span><span class="sxs-lookup"><span data-stu-id="a01ad-103">NuGet 5.1 Release Notes</span></span>

<span data-ttu-id="a01ad-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="a01ad-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="a01ad-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="a01ad-105">NuGet version</span></span> | <span data-ttu-id="a01ad-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="a01ad-106">Available in Visual Studio version</span></span>| <span data-ttu-id="a01ad-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="a01ad-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="a01ad-108">**5.1.0**</span><span class="sxs-lookup"><span data-stu-id="a01ad-108">**5.1.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="a01ad-109">Visual Studio 2019 バージョン 16.1</span><span class="sxs-lookup"><span data-stu-id="a01ad-109">Visual Studio 2019 version 16.1</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="a01ad-110">[2.1.70 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>、 [2.2.30 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span><span class="sxs-lookup"><span data-stu-id="a01ad-110">[2.1.70X](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.30X](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup></span></span> |

<span data-ttu-id="a01ad-111"><sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="a01ad-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span> 

<span data-ttu-id="a01ad-112"><sup>2</sup>.NET Core ワークロードを含む Visual Studio 2019 を使用したオプションのインストールとして利用可能</span><span class="sxs-lookup"><span data-stu-id="a01ad-112"><sup>2</sup>Available as an optional install with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-51"></a><span data-ttu-id="a01ad-113">概要: 5.1 の新機能</span><span class="sxs-lookup"><span data-stu-id="a01ad-113">Summary: What's New in 5.1</span></span>

* <span data-ttu-id="a01ad-114">CI/CD ワークフローとの統合を強化するために既に存在する場合は、パッケージプッシュをスキップできるようになります。 [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span><span class="sxs-lookup"><span data-stu-id="a01ad-114">Support to skip a package push if it already exists to allow for better integration with CI/CD workflows - [#1630](https://github.com/NuGet/Home/issues/1630#issuecomment-483461100)</span></span>

* <span data-ttu-id="a01ad-115">Visual Studio で、パッケージの nuget.org ギャラリーページへの便利なリンクが提供されるようになりました [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span><span class="sxs-lookup"><span data-stu-id="a01ad-115">Visual Studio now provides a convenient link to the the package's nuget.org gallery page - [#5299](https://github.com/NuGet/Home/issues/5299#issuecomment-494458510)</span></span>

* <span data-ttu-id="a01ad-116">[ターゲットパック](https://github.com/dotnet/cli/issues/10006)や[ランタイムパック](https://github.com/dotnet/cli/issues/10007)など、新しい .net Core 3.0 資産のサポート</span><span class="sxs-lookup"><span data-stu-id="a01ad-116">Support for new .NET Core 3.0 assets such as [Targeting Packs](https://github.com/dotnet/cli/issues/10006) and [Runtime Packs](https://github.com/dotnet/cli/issues/10007)</span></span>
  * <span data-ttu-id="a01ad-117">ターゲットおよびランタイムパッケージの参照を有効にするための FrameworkReferences の NuGet パックと復元のサポート- [#7342](https://github.com/NuGet/Home/issues/7342)</span><span class="sxs-lookup"><span data-stu-id="a01ad-117">NuGet pack and restore support for FrameworkReferences to enable targeting and runtime package references - [#7342](https://github.com/NuGet/Home/issues/7342)</span></span>
  * <span data-ttu-id="a01ad-118">PackageDownload を使用した "ダウンロードのみ" パッケージのシナリオをサポートする- [#7339](https://github.com/NuGet/Home/issues/7339)</span><span class="sxs-lookup"><span data-stu-id="a01ad-118">Support "download only" package scenario with PackageDownload - [#7339](https://github.com/NuGet/Home/issues/7339)</span></span>
  * <span data-ttu-id="a01ad-119">検索結果からランタイムとターゲットパックを除外し & PackageType- [#7337](https://github.com/NuGet/Home/issues/7337)を使用してグラフを復元する</span><span class="sxs-lookup"><span data-stu-id="a01ad-119">Exclude runtime and targeting packs from search results & restore graph using PackageType - [#7337](https://github.com/NuGet/Home/issues/7337)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="a01ad-120">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="a01ad-120">Issues fixed in this release</span></span>

<span data-ttu-id="a01ad-121">**バグ**</span><span class="sxs-lookup"><span data-stu-id="a01ad-121">**Bugs**</span></span>

* <span data-ttu-id="a01ad-122">プラグイン: プラグインの作成中に例外の詳細が失われました- [#8057](https://github.com/NuGet/Home/issues/8057)</span><span class="sxs-lookup"><span data-stu-id="a01ad-122">Plugins:  exception details lost during plugin creation - [#8057](https://github.com/NuGet/Home/issues/8057)</span></span>

* <span data-ttu-id="a01ad-123">排他的下限を持つ PackageReference range は、いずれかのソースに下限が存在する場合は機能しません。</span><span class="sxs-lookup"><span data-stu-id="a01ad-123">PackageReference range with exclusive lower bound does not work if the lower bound is present on one of the sources.</span></span><span data-ttu-id="a01ad-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span><span class="sxs-lookup"><span data-stu-id="a01ad-124"> - [#8054](https://github.com/NuGet/Home/issues/8054)</span></span>

* <span data-ttu-id="a01ad-125">Ispackablefalse エラーメッセージの改善- [#8021](https://github.com/NuGet/Home/issues/8021)</span><span class="sxs-lookup"><span data-stu-id="a01ad-125">Improve IsPackableFalseError message - [#8021](https://github.com/NuGet/Home/issues/8021)</span></span>

* <span data-ttu-id="a01ad-126">パッケージロックファイル-プロジェクトグラフが変更したときにロックファイルを再生成する- [#8019](https://github.com/NuGet/Home/issues/8019)</span><span class="sxs-lookup"><span data-stu-id="a01ad-126">Packages Lock File - regenerate lock file when project graph changes - [#8019](https://github.com/NuGet/Home/issues/8019)</span></span>

* <span data-ttu-id="a01ad-127">ProjectSystem のバグ: Nuget パッケージの自動削除の取得- [#8017](https://github.com/NuGet/Home/issues/8017)</span><span class="sxs-lookup"><span data-stu-id="a01ad-127">ProjectSystem bug: Nuget Packages getting auto removed - [#8017](https://github.com/NuGet/Home/issues/8017)</span></span>

* <span data-ttu-id="a01ad-128">CollectPackageDownloads および[#8005](https://github.com/NuGet/Home/issues/8005) CollectPackageReferences と同様の frameworkreference を返すターゲットを追加します。</span><span class="sxs-lookup"><span data-stu-id="a01ad-128">Add a target for returning the FrameworkReference similar to CollectPackageDownloads and CollectPackageReferences - [#8005](https://github.com/NuGet/Home/issues/8005)</span></span>

* <span data-ttu-id="a01ad-129">HTTP キャッシュ: RepositoryResources リソースはバージョン管理された方法でキャッシュされていません- [#7997](https://github.com/NuGet/Home/issues/7997)</span><span class="sxs-lookup"><span data-stu-id="a01ad-129">HTTP cache:  RepositoryResources resource is not cached in a versioned way - [#7997](https://github.com/NuGet/Home/issues/7997)</span></span>

* <span data-ttu-id="a01ad-130">ログ: 例外呼び出し履歴は詳細な詳細度で報告されません- [#7955](https://github.com/NuGet/Home/issues/7955)</span><span class="sxs-lookup"><span data-stu-id="a01ad-130">Logging:  exception callstacks are not reported with detailed verbosity - [#7955](https://github.com/NuGet/Home/issues/7955)</span></span>

* <span data-ttu-id="a01ad-131">HTTPS を使用するようにすべての NuGet Docs Url を変更する [#7950](https://github.com/NuGet/Home/issues/7950)</span><span class="sxs-lookup"><span data-stu-id="a01ad-131">Change all NuGet Docs URLs to use HTTPS - [#7950](https://github.com/NuGet/Home/issues/7950)</span></span>

* <span data-ttu-id="a01ad-132">NU3024 の警告メッセージの改善- [#7933](https://github.com/NuGet/Home/issues/7933)</span><span class="sxs-lookup"><span data-stu-id="a01ad-132">Improve NU3024 warning message - [#7933](https://github.com/NuGet/Home/issues/7933)</span></span>

* <span data-ttu-id="a01ad-133">packagereference が削除されたときにロックファイルが更新されない- [#7930](https://github.com/NuGet/Home/issues/7930)</span><span class="sxs-lookup"><span data-stu-id="a01ad-133">lock file not updating when packagereference removed - [#7930](https://github.com/NuGet/Home/issues/7930)</span></span>

* <span data-ttu-id="a01ad-134">[#7915](https://github.com/NuGet/Home/issues/7915) nuspec で licenseurl と license 要素を検証するときのエラーケースの処理を改善する</span><span class="sxs-lookup"><span data-stu-id="a01ad-134">Improve the error case handling when validating licenseurl and license element in nuspec - [#7915](https://github.com/NuGet/Home/issues/7915)</span></span>

* <span data-ttu-id="a01ad-135">PM UI-タブヘッダーを右クリックし、[ファイルの場所を開く] をクリックすると、エラー [#7913](https://github.com/NuGet/Home/issues/7913)</span><span class="sxs-lookup"><span data-stu-id="a01ad-135">PM UI - right click on tab header and clicking "Open file location" results in error - [#7913](https://github.com/NuGet/Home/issues/7913)</span></span>

* <span data-ttu-id="a01ad-136">プラグイン: プラグインプロセスが終了したときにログを記録する- [#7907](https://github.com/NuGet/Home/issues/7907)</span><span class="sxs-lookup"><span data-stu-id="a01ad-136">Plugins:  log when plugin process exits - [#7907](https://github.com/NuGet/Home/issues/7907)</span></span>

* <span data-ttu-id="a01ad-137">プラグイン: ログに記録される datetime 値の競合率が高い- [#7899](https://github.com/NuGet/Home/issues/7899)</span><span class="sxs-lookup"><span data-stu-id="a01ad-137">Plugins:  high collision rate in logging datetime values - [#7899](https://github.com/NuGet/Home/issues/7899)</span></span>

* <span data-ttu-id="a01ad-138">LicenseExpression Expression で nuspec を使用すると、すべての[](https://github.com/NuGet/Home/issues/7894)で失敗します。</span><span class="sxs-lookup"><span data-stu-id="a01ad-138">Manifest.ReadFrom fails on any nuspec with LicenseExpression - [#7894](https://github.com/NuGet/Home/issues/7894)</span></span>

* <span data-ttu-id="a01ad-139">RestoreLockedMode: ProjectReference がカスタム AssemblyName [#7889](https://github.com/NuGet/Home/issues/7889)を持つプロジェクトを参照しているときに、予期しない NU1004 があります</span><span class="sxs-lookup"><span data-stu-id="a01ad-139">RestoreLockedMode: Unexpected NU1004 when ProjectReference refers to a project with custom AssemblyName - [#7889](https://github.com/NuGet/Home/issues/7889)</span></span>

* <span data-ttu-id="a01ad-140">プラグインの起動が例外で失敗した場合のエラーメッセージの改善- [#7857](https://github.com/NuGet/Home/issues/7857)</span><span class="sxs-lookup"><span data-stu-id="a01ad-140">Better error message when the plugin startup fails with an exception - [#7857](https://github.com/NuGet/Home/issues/7857)</span></span>

* <span data-ttu-id="a01ad-141">NoOp 復元を実行する場合は、obj ディレクトリへの書き込み時に \* .dgspec.jsを避ける- [#7854](https://github.com/NuGet/Home/issues/7854)</span><span class="sxs-lookup"><span data-stu-id="a01ad-141">When doing a NoOp restore, avoid \*.dgspec.json write in obj directory - [#7854](https://github.com/NuGet/Home/issues/7854)</span></span>

* <span data-ttu-id="a01ad-142">GeneratePathProperty = true は、ケースが一致しない場合にプロパティを生成できません- [#7843](https://github.com/NuGet/Home/issues/7843)</span><span class="sxs-lookup"><span data-stu-id="a01ad-142">GeneratePathProperty=true fails to generate property on case mismatch - [#7843](https://github.com/NuGet/Home/issues/7843)</span></span>

* <span data-ttu-id="a01ad-143">設定: パッケージソースパスに無効な文字があると、VS- [#7820](https://github.com/NuGet/Home/issues/7820)がクラッシュする可能性があります</span><span class="sxs-lookup"><span data-stu-id="a01ad-143">Settings:  illegal character in package source path can crash VS - [#7820](https://github.com/NuGet/Home/issues/7820)</span></span>

* <span data-ttu-id="a01ad-144">ロックファイルが削除された場合、restore では、NoOp でロックファイルが生成されません- [#7807](https://github.com/NuGet/Home/issues/7807)</span><span class="sxs-lookup"><span data-stu-id="a01ad-144">If lock file is deleted, restore does not generate lock file on NoOp  - [#7807](https://github.com/NuGet/Home/issues/7807)</span></span>

* <span data-ttu-id="a01ad-145">ライセンス URL とライセンスにより、メタデータで読み取りエラーが発生する- [#7547](https://github.com/NuGet/Home/issues/7547)</span><span class="sxs-lookup"><span data-stu-id="a01ad-145">License URL and license causes read error with Metadata - [#7547](https://github.com/NuGet/Home/issues/7547)</span></span>

* <span data-ttu-id="a01ad-146">[#7523](https://github.com/NuGet/Home/issues/7523) V2FeedParser でのハンドルされない例外</span><span class="sxs-lookup"><span data-stu-id="a01ad-146">Unhandled exceptions in V2FeedParser - [#7523](https://github.com/NuGet/Home/issues/7523)</span></span>

* <span data-ttu-id="a01ad-147">無効な引数の終了コード0が返さ nuget.exe- [#7178](https://github.com/NuGet/Home/issues/7178)</span><span class="sxs-lookup"><span data-stu-id="a01ad-147">nuget.exe returns exit code zero for invalid arguments - [#7178](https://github.com/NuGet/Home/issues/7178)</span></span>

* <span data-ttu-id="a01ad-148">署名関連のシナリオを反映するようにエラーと警告ドキュメントを更新する- [#6498](https://github.com/NuGet/Home/issues/6498)</span><span class="sxs-lookup"><span data-stu-id="a01ad-148">Update Errors and warning docs to reflect signing related scenarios - [#6498](https://github.com/NuGet/Home/issues/6498)</span></span>

* <span data-ttu-id="a01ad-149">アセットファイルは、相対パスを使用して、より簡単にプロジェクトを移動できるようにする必要があり [#4582](https://github.com/NuGet/Home/issues/4582)</span><span class="sxs-lookup"><span data-stu-id="a01ad-149">Assets file should use relative paths to enable moving projects more easily - [#4582](https://github.com/NuGet/Home/issues/4582)</span></span>

<span data-ttu-id="a01ad-150">**DCR**</span><span class="sxs-lookup"><span data-stu-id="a01ad-150">**DCRs**</span></span>

* <span data-ttu-id="a01ad-151">プラグイン: 診断ログを有効にする- [#7859](https://github.com/NuGet/Home/issues/7859)</span><span class="sxs-lookup"><span data-stu-id="a01ad-151">Plugins:  enable diagnostic logging - [#7859](https://github.com/NuGet/Home/issues/7859)</span></span>

* <span data-ttu-id="a01ad-152">Tizen 6 を NetStandard 2.1 にマップする- [#7773](https://github.com/NuGet/Home/issues/7773)</span><span class="sxs-lookup"><span data-stu-id="a01ad-152">Make Tizen 6 map to NetStandard 2.1 - [#7773](https://github.com/NuGet/Home/issues/7773)</span></span>

<span data-ttu-id="a01ad-153">**[このリリース-5.1 RTM で修正されるすべての問題の一覧](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span><span class="sxs-lookup"><span data-stu-id="a01ad-153">**[List of all issues fixed in this release - 5.1 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.1")**</span></span>
