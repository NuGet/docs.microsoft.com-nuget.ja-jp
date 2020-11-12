---
title: NuGet 5.8 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.8 のリリースノート。
author: dominofire
ms.author: feaguila
ms.date: 11/9/2020
ms.topic: conceptual
ms.openlocfilehash: 86e173b9d760578454df8f5f817533f64e193996
ms.sourcegitcommit: 0cc6ac680c3202d0b036c0bed7910f6709215682
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/12/2020
ms.locfileid: "94550742"
---
# <a name="nuget-58-release-notes"></a><span data-ttu-id="3b95a-103">NuGet 5.8 リリースノート</span><span class="sxs-lookup"><span data-stu-id="3b95a-103">NuGet 5.8 Release Notes</span></span>

<span data-ttu-id="3b95a-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="3b95a-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="3b95a-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="3b95a-105">NuGet version</span></span> | <span data-ttu-id="3b95a-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="3b95a-106">Available in Visual Studio version</span></span> | <span data-ttu-id="3b95a-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3b95a-107">Available in .NET SDK(s)</span></span> |
|:---|:---|:---|
| [<span data-ttu-id="3b95a-108">**5.8**</span><span class="sxs-lookup"><span data-stu-id="3b95a-108">**5.8**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="3b95a-109">Visual Studio 2019 バージョン 16.8</span><span class="sxs-lookup"><span data-stu-id="3b95a-109">Visual Studio 2019 version 16.8</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="3b95a-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="3b95a-110">[5.0](https://dotnet.microsoft.com/download/dotnet-core/5.0)<sup>1</sup></span></span> |

<span data-ttu-id="3b95a-111"><sup>1</sup> Visual Studio 2019 と .net Core ワークロードと共にインストールされる</span><span class="sxs-lookup"><span data-stu-id="3b95a-111"><sup>1</sup> Installed with Visual Studio 2019 with .NET Core workload</span></span>
  
> [!NOTE]
> <span data-ttu-id="3b95a-112">Visual Studio 16.8、MSBuild 16.8、および .NET 5.0 には NuGet.exe 5.8 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="3b95a-112">Visual Studio 16.8, MSBuild 16.8, and .NET 5.0 require NuGet.exe 5.8 or later.</span></span>


## <a name="summary-whats-new-in-58"></a><span data-ttu-id="3b95a-113">概要: 5.8 の新機能</span><span class="sxs-lookup"><span data-stu-id="3b95a-113">Summary: What's New in 5.8</span></span>
<span data-ttu-id="3b95a-114">🎉 **これは、.net 5.0 をターゲットとする NuGet パッケージの完全な作成と復元のサポートを提供するための最初のリリースです** 🎉</span><span class="sxs-lookup"><span data-stu-id="3b95a-114">🎉 **This is the first release to offer full authoring and restoring support for NuGet packages targeting .NET 5.0** 🎉</span></span>

* <span data-ttu-id="3b95a-115">パッケージマネージャー UI パッケージの詳細ペインでパッケージの脆弱性の詳細を表示する- [#9850](https://github.com/NuGet/Home/issues/9850)</span><span class="sxs-lookup"><span data-stu-id="3b95a-115">Display package vulnerability details in the Package Manager UI package details pane - [#9850](https://github.com/NuGet/Home/issues/9850)</span></span>

* <span data-ttu-id="3b95a-116">新しい [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) コマンド[#8051](https://github.com/NuGet/Home/issues/8051)で署名済みの NuGet パッケージを確認する</span><span class="sxs-lookup"><span data-stu-id="3b95a-116">Verify signed NuGet packages with the new [`dotnet nuget verify`](https://docs.microsoft.com/dotnet/core/tools/dotnet-nuget-verify) command - [#8051](https://github.com/NuGet/Home/issues/8051)</span></span>

* <span data-ttu-id="3b95a-117">[`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples)`--prerelease`プレリリースバージョンを含むパッケージの最新バージョンを追加するオプションをサポートしてい[#4699](https://github.com/NuGet/Home/issues/4699)</span><span class="sxs-lookup"><span data-stu-id="3b95a-117">[`dotnet add package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-add-package#:~:text=dotnet%20add%20package%201%20Name%202%20Synopsis%203,when%20targeting%20a%20specific%20framework.%20...%206%20Examples) supports `--prerelease` option to add the latest version of a package, including prerelease versions - [#4699](https://github.com/NuGet/Home/issues/4699)</span></span>

* <span data-ttu-id="3b95a-118">[`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search)コマンド[#9704](https://github.com/NuGet/Home/issues/9704)を使用して CLI でパッケージを検索する</span><span class="sxs-lookup"><span data-stu-id="3b95a-118">Search for packages in the CLI with [`nuget.exe search`](https://docs.microsoft.com/nuget/reference/cli-reference/cli-ref-search) command - [#9704](https://github.com/NuGet/Home/issues/9704)</span></span>

* <span data-ttu-id="3b95a-119">[`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) コマンドはオプションをサポートしてい `--verbosity` [#9600](https://github.com/NuGet/Home/issues/9600)</span><span class="sxs-lookup"><span data-stu-id="3b95a-119">[`dotnet list package`](https://docs.microsoft.com/dotnet/core/tools/dotnet-list-package) command supports `--verbosity` option - [#9600](https://github.com/NuGet/Home/issues/9600)</span></span>

* <span data-ttu-id="3b95a-120">Visual Studio での、PackageReference ベースの .csproj スタイルのプロジェクトの高速 No-Op 復元の最適化を有効にする- [#9565](https://github.com/NuGet/Home/issues/9565)</span><span class="sxs-lookup"><span data-stu-id="3b95a-120">Enable fast No-Op restore optimization for csproj-style, PackageReference-based projects in Visual Studio - [#9565](https://github.com/NuGet/Home/issues/9565)</span></span>

* <span data-ttu-id="3b95a-121">パッケージのインストールや更新などのソリューションレベルのパッケージマネージャーの UI 操作は、最大10倍の速度で実行され [#6010](https://github.com/NuGet/Home/issues/6010)</span><span class="sxs-lookup"><span data-stu-id="3b95a-121">Solution level Package Manager UI operations such as package installs and updates are up to 10x faster - [#6010](https://github.com/NuGet/Home/issues/6010)</span></span>

* <span data-ttu-id="3b95a-122">Visual Studio でのその他のいくつかの NuGet パフォーマンスの向上- [#9982](https://github.com/NuGet/Home/issues/9982)、 [#9984](https://github.com/NuGet/Home/issues/9984)、 [#10052](https://github.com/NuGet/Home/issues/10052)、 [#9903](https://github.com/NuGet/Home/issues/9903)</span><span class="sxs-lookup"><span data-stu-id="3b95a-122">Several other NuGet performance improvements in Visual Studio - [#9982](https://github.com/NuGet/Home/issues/9982), [#9984](https://github.com/NuGet/Home/issues/9984), [#10052](https://github.com/NuGet/Home/issues/10052), [#9903](https://github.com/NuGet/Home/issues/9903)</span></span>


### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="3b95a-123">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="3b95a-123">Issues fixed in this release</span></span>

<span data-ttu-id="3b95a-124">**Dcr**</span><span class="sxs-lookup"><span data-stu-id="3b95a-124">**DCRs:**</span></span>

* <span data-ttu-id="3b95a-125">.NET 5.0 TFM: フレームワークの優先順位の規則- [#9436](https://github.com/NuGet/Home/issues/9436)</span><span class="sxs-lookup"><span data-stu-id="3b95a-125">.NET 5.0 TFM: Framework Precedence Rules - [#9436](https://github.com/NuGet/Home/issues/9436)</span></span>

* <span data-ttu-id="3b95a-126">TargetFramework を解析するときに、NuGet はドットプラットフォームバージョンを推論することはできません- [#9842](https://github.com/NuGet/Home/issues/9842)</span><span class="sxs-lookup"><span data-stu-id="3b95a-126">NuGet should not infer dots platform version when parsing TargetFramework - [#9842](https://github.com/NuGet/Home/issues/9842)</span></span>

* <span data-ttu-id="3b95a-127">TargetFrameworkMoniker & Targetframeworkmoniker を使用して、個々の TFI、TFI、TFI、TFI プロパティ- [#9895](https://github.com/NuGet/Home/issues/9895)を使用するのではなく、フレームワークを推測します。</span><span class="sxs-lookup"><span data-stu-id="3b95a-127">Use TargetFrameworkMoniker & TargetPlatformMoniker to infer the frameworks instead of using individual TFI, TFV, TPI, TPV properties - [#9895](https://github.com/NuGet/Home/issues/9895)</span></span>

* <span data-ttu-id="3b95a-128">`GetReferenceNearestTargetFrameworkTask()`プラットフォーム (net 5.0-windows など) を使用したターゲットフレームワークをサポートするための更新プログラム- [#9894](https://github.com/NuGet/Home/issues/9894)</span><span class="sxs-lookup"><span data-stu-id="3b95a-128">Update `GetReferenceNearestTargetFrameworkTask()` to support target frameworks with platforms (such as net5.0-windows) - [#9894](https://github.com/NuGet/Home/issues/9894)</span></span>

* <span data-ttu-id="3b95a-129">.NET 5.0 Visual Studio Api- [#9650](https://github.com/NuGet/Home/issues/9650)</span><span class="sxs-lookup"><span data-stu-id="3b95a-129">.NET 5.0 Visual Studio APIs - [#9650](https://github.com/NuGet/Home/issues/9650)</span></span>

* <span data-ttu-id="3b95a-130">パッケージマネージャー UI: パッケージの統合または更新は、エラー (パッケージダウングレードなど) が原因でブロックされないようにする必要があります。- [#9224](https://github.com/NuGet/Home/issues/9224)</span><span class="sxs-lookup"><span data-stu-id="3b95a-130">Package Manager UI: Consolidate or Update packages operations should not be blocked due to errors (Package Downgrade, etc.) - [#9224](https://github.com/NuGet/Home/issues/9224)</span></span>

* <span data-ttu-id="3b95a-131">機能があるプロジェクトについては、NuGet の機能が淡色になります。"PackageReferences"- [#9957](https://github.com/NuGet/Home/issues/9957)</span><span class="sxs-lookup"><span data-stu-id="3b95a-131">NuGet features should light up for projects that have the capability; "PackageReferences" - [#9957](https://github.com/NuGet/Home/issues/9957)</span></span>

* <span data-ttu-id="3b95a-132">Visual Studio でメッセージの No-Op 復元を抑制する- [#6384](https://github.com/NuGet/Home/issues/6384)</span><span class="sxs-lookup"><span data-stu-id="3b95a-132">Suppress No-Op Restore messages in Visual Studio - [#6384](https://github.com/NuGet/Home/issues/6384)</span></span>

<span data-ttu-id="3b95a-133">**バグ**</span><span class="sxs-lookup"><span data-stu-id="3b95a-133">**Bugs:**</span></span>

* <span data-ttu-id="3b95a-134">OutputWindowTextWriter コンストラクターをバックグラウンドスレッドで呼び出すことはできません- [#9764](https://github.com/NuGet/Home/issues/9764)</span><span class="sxs-lookup"><span data-stu-id="3b95a-134">OutputWindowTextWriter constructor should not be called on background thread - [#9764](https://github.com/NuGet/Home/issues/9764)</span></span>

* <span data-ttu-id="3b95a-135">ビッグエンディアン Cpu で署名されたパッケージを復元する- [#9547](https://github.com/NuGet/Home/issues/9547)</span><span class="sxs-lookup"><span data-stu-id="3b95a-135">Restore signed packages on Big Endian CPUs - [#9547](https://github.com/NuGet/Home/issues/9547)</span></span>

* <span data-ttu-id="3b95a-136">OutputConsoleLogger は MEF コンストラクターで関連付けられたメソッドを呼び出すことはできません- [#9591](https://github.com/NuGet/Home/issues/9591)</span><span class="sxs-lookup"><span data-stu-id="3b95a-136">OutputConsoleLogger should not call affinitized methods in MEF constructors - [#9591](https://github.com/NuGet/Home/issues/9591)</span></span>

* <span data-ttu-id="3b95a-137">NuGet. CommandLine. Console メソッドのバグ `PrintJustified()` - [#9737](https://github.com/NuGet/Home/issues/9737)</span><span class="sxs-lookup"><span data-stu-id="3b95a-137">Bug in NuGet.CommandLine.Console `PrintJustified()` method - [#9737](https://github.com/NuGet/Home/issues/9737)</span></span>

* <span data-ttu-id="3b95a-138">不適切なバインドのためにパッケージメタデータがガベージコレクションされるときのパッケージマネージャー UI のメモリリーク [#9757](https://github.com/NuGet/Home/issues/9757)</span><span class="sxs-lookup"><span data-stu-id="3b95a-138">Package Manager UI memory leak when package metadata is garbage collected due to a bad binding - [#9757](https://github.com/NuGet/Home/issues/9757)</span></span>

* <span data-ttu-id="3b95a-139">付きパッケージマネージャー UI で packages.config 形式の署名付きパッケージをインストールすると、エラー一覧に警告は表示されません。 [#9798](https://github.com/NuGet/Home/issues/9798)</span><span class="sxs-lookup"><span data-stu-id="3b95a-139">[Signing] No warning is showed in Error List when installing a signed package with packages.config format in Package Manager UI - [#9798](https://github.com/NuGet/Home/issues/9798)</span></span>

* <span data-ttu-id="3b95a-140">XPlat にパブリック Api を含めることはできません- [#9821](https://github.com/NuGet/Home/issues/9821)</span><span class="sxs-lookup"><span data-stu-id="3b95a-140">NuGet.CommandLine.XPlat should not have public APIs - [#9821](https://github.com/NuGet/Home/issues/9821)</span></span>

* <span data-ttu-id="3b95a-141">#9822 でスレッドプールのスレッドをブロックすることによって、ソリューションの読み込み時にリソースの競合を軽減します `BlockingCollection.Take()`  -  [#9822](https://github.com/NuGet/Home/issues/9822)</span><span class="sxs-lookup"><span data-stu-id="3b95a-141">Reduce resource contention at Solution Load time caused by blocking a threaded-pool thread with `BlockingCollection.Take()` - [#9822](https://github.com/NuGet/Home/issues/9822)</span></span>

* <span data-ttu-id="3b95a-142">複数のターゲットが指定されたプロジェクトのコマンドライン復元では、NuGet は内部ビルドからターゲットフレームワーク関連情報を読み取る必要があり [#9869](https://github.com/NuGet/Home/issues/9869)</span><span class="sxs-lookup"><span data-stu-id="3b95a-142">In command line restore, with multi targeted projects, NuGet should read the target framework related information from the inner build - [#9869](https://github.com/NuGet/Home/issues/9869)</span></span>

* <span data-ttu-id="3b95a-143">TargetFrameworkInformation 項目を使用してランタイム識別子グラフを読み取ります。 [#9874](https://github.com/NuGet/Home/issues/9874)</span><span class="sxs-lookup"><span data-stu-id="3b95a-143">Read Runtime Identifier graph through TargetFrameworkInformation item - [#9874](https://github.com/NuGet/Home/issues/9874)</span></span>

* <span data-ttu-id="3b95a-144">Visual Studio と通常の MSBuild 評価の復元[#9881](https://github.com/NuGet/Home/issues/9881)と比較した場合、静的なグラフの復元は、の CrossTargeting プロパティに関して一貫性がありません</span><span class="sxs-lookup"><span data-stu-id="3b95a-144">Static graph restore is inconsistent with regards to CrossTargeting property in compared to Visual Studio and regular MSBuild evaluation restore - [#9881](https://github.com/NuGet/Home/issues/9881)</span></span>

* <span data-ttu-id="3b95a-145">複数のターゲットが指定されたプロジェクトの静的なグラフ復元では、NuGet は、内部ビルドからターゲットフレームワーク関連情報を読み取る必要があります。</span><span class="sxs-lookup"><span data-stu-id="3b95a-145">In static graph restore, with multi targeted projects, NuGet should read the target framework related information from the inner build.</span></span><span data-ttu-id="3b95a-146"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span><span class="sxs-lookup"><span data-stu-id="3b95a-146"> - [#9870](https://github.com/NuGet/Home/issues/9870)</span></span>

* <span data-ttu-id="3b95a-147">`net5.0-platform`Visual Studio でのプロジェクトの読み込みと復元を許可する- [#9863](https://github.com/NuGet/Home/issues/9863)</span><span class="sxs-lookup"><span data-stu-id="3b95a-147">Allow `net5.0-platform` projects to be loaded and restored in Visual Studio - [#9863](https://github.com/NuGet/Home/issues/9863)</span></span>

* <span data-ttu-id="3b95a-148">パッケージマネージャー UI で解決済みのバージョンを表示する- [#9826](https://github.com/NuGet/Home/issues/9826)</span><span class="sxs-lookup"><span data-stu-id="3b95a-148">Display the resolved version in the Package Manager UI - [#9826](https://github.com/NuGet/Home/issues/9826)</span></span>

* <span data-ttu-id="3b95a-149">パッケージマネージャー UI: ソリューションエクスプローラーにすべての NuGet パッケージの依存関係が表示されていません- [#9898](https://github.com/NuGet/Home/issues/9898)</span><span class="sxs-lookup"><span data-stu-id="3b95a-149">Package Manager UI: Solution Explorer is not showing all NuGet package dependencies - [#9898](https://github.com/NuGet/Home/issues/9898)</span></span>

* <span data-ttu-id="3b95a-150">SPDX ライセンスリストを更新する- [#9946](https://github.com/NuGet/Home/issues/9946)</span><span class="sxs-lookup"><span data-stu-id="3b95a-150">Update the SPDX license list - [#9946](https://github.com/NuGet/Home/issues/9946)</span></span>

* <span data-ttu-id="3b95a-151">[NuGet パッケージの管理] を開いた後、VS 2019 がクラッシュする: アイコンは[#9696](https://github.com/NuGet/Home/issues/9696) 、conversio イメージでハンドルされない例外を発生させます。</span><span class="sxs-lookup"><span data-stu-id="3b95a-151">VS 2019 crashes after opening Manage NuGet Packages: icon causes unhandled exception in image conversio - [#9696](https://github.com/NuGet/Home/issues/9696)</span></span>

* <span data-ttu-id="3b95a-152">[#9966](https://github.com/NuGet/Home/issues/9966)で Newtonsoft.Jsを除外するには、パッケージの抽出に ilmerge が必要です</span><span class="sxs-lookup"><span data-stu-id="3b95a-152">NuGet.Packaging.Extraction needs ilmerge to exclude Newtonsoft.Json - [#9966](https://github.com/NuGet/Home/issues/9966)</span></span>

* <span data-ttu-id="3b95a-153">ContinuePackingAfterGeneratingNuspec = false でのパッキングは、エラーがない場合は失敗しません- [#9786](https://github.com/NuGet/Home/issues/9786)</span><span class="sxs-lookup"><span data-stu-id="3b95a-153">Packing with ContinuePackingAfterGeneratingNuspec=false should not fail when there are no errors - [#9786](https://github.com/NuGet/Home/issues/9786)</span></span>

* <span data-ttu-id="3b95a-154">パッケージマネージャー UI: アイコンが正しく反転していません- [#10017](https://github.com/NuGet/Home/issues/10017)</span><span class="sxs-lookup"><span data-stu-id="3b95a-154">Package Manager UI: Icons aren't inverting colors properly - [#10017](https://github.com/NuGet/Home/issues/10017)</span></span>

* <span data-ttu-id="3b95a-155">復元時に最新のプロジェクトと No-Op プロジェクトのプロジェクト数が正しくない- [#10026](https://github.com/NuGet/Home/issues/10026)</span><span class="sxs-lookup"><span data-stu-id="3b95a-155">Incorrect project counts for Up-To-Date and No-Op projects at Restore - [#10026](https://github.com/NuGet/Home/issues/10026)</span></span>

* <span data-ttu-id="3b95a-156">結果を使用して `/p:RestoreUseStaticGraphEvaluation=true` 値を Null にすることはできません- [#9280](https://github.com/NuGet/Home/issues/9280)</span><span class="sxs-lookup"><span data-stu-id="3b95a-156">Using `/p:RestoreUseStaticGraphEvaluation=true` Results in Value Cannot Be Null - [#9280](https://github.com/NuGet/Home/issues/9280)</span></span>

* <span data-ttu-id="3b95a-157">`dotnet pack` WPF ライブラリプロジェクトのエイリアスを誤って使用する- [#10020](https://github.com/NuGet/Home/issues/10020)</span><span class="sxs-lookup"><span data-stu-id="3b95a-157">`dotnet pack` mistakenly uses alias for WPF Library projects - [#10020](https://github.com/NuGet/Home/issues/10020)</span></span>

* <span data-ttu-id="3b95a-158">パッケージマネージャー UI: 署名の検証に失敗した場合[#10042](https://github.com/NuGet/Home/issues/10042)の NullReferenceException</span><span class="sxs-lookup"><span data-stu-id="3b95a-158">Package Manager UI: NullReferenceException when signature validation fails - [#10042](https://github.com/NuGet/Home/issues/10042)</span></span>

* <span data-ttu-id="3b95a-159">Codespaces: `object` プロジェクトメタデータ値の型を使用しません- [#10055](https://github.com/NuGet/Home/issues/10055)</span><span class="sxs-lookup"><span data-stu-id="3b95a-159">Codespaces: do not use `object` type for project metadata values  - [#10055](https://github.com/NuGet/Home/issues/10055)</span></span>

* <span data-ttu-id="3b95a-160">Codespaces: [ツール] オプションでパッケージソースを保存すると、資格情報が上書きされ [#9711](https://github.com/NuGet/Home/issues/9711)</span><span class="sxs-lookup"><span data-stu-id="3b95a-160">Codespaces: saving package sources in tools options will overwrite credentials - [#9711](https://github.com/NuGet/Home/issues/9711)</span></span>


<span data-ttu-id="3b95a-161">**[このリリースで修正されるすべての問題の一覧-5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span><span class="sxs-lookup"><span data-stu-id="3b95a-161">**[List of all issues fixed in this release - 5.8](https://app.zenhub.com/workspaces/nuget-client-team-55aec9a240305cf007585881/reports/release?release=5f03519b777e78b4ffb2edeb)**</span></span>

<span data-ttu-id="3b95a-162">**[このリリースで修正される問題/コミットの一覧-5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span><span class="sxs-lookup"><span data-stu-id="3b95a-162">**[List of issues/commits fixed in this release - 5.8](https://github.com/NuGet/NuGet.Client/compare/5.7.0.6726...5.8.0.6930)**</span></span>

### <a name="community-contributions"></a><span data-ttu-id="3b95a-163">コミュニティからの投稿</span><span class="sxs-lookup"><span data-stu-id="3b95a-163">Community contributions</span></span>

<span data-ttu-id="3b95a-164">この NuGet のリリースに役立ったすべての共同作成者に感謝します。</span><span class="sxs-lookup"><span data-stu-id="3b95a-164">Thank you to all the contributors who helped make this NuGet release awesome!</span></span>

|<span data-ttu-id="3b95a-165">担当者</span><span class="sxs-lookup"><span data-stu-id="3b95a-165">Who</span></span>|<span data-ttu-id="3b95a-166">Pr</span><span class="sxs-lookup"><span data-stu-id="3b95a-166">PRs</span></span>|<span data-ttu-id="3b95a-167">発行</span><span class="sxs-lookup"><span data-stu-id="3b95a-167">Issues</span></span>|
|----|----|----|
[<span data-ttu-id="3b95a-168">omajid</span><span class="sxs-lookup"><span data-stu-id="3b95a-168">omajid</span></span>](https://github.com/omajid) | [<span data-ttu-id="3b95a-169">3437</span><span class="sxs-lookup"><span data-stu-id="3b95a-169">3437</span></span>](https://github.com/NuGet/NuGet.Client/pull/3437) | <span data-ttu-id="3b95a-170">エラーメッセージに誤りがあります。</span><span class="sxs-lookup"><span data-stu-id="3b95a-170">Typo in error message.</span></span> <span data-ttu-id="3b95a-171">"administrator" ではなく "管理者"- [#9662](https://github.com/NuGet/Home/issues/9662)</span><span class="sxs-lookup"><span data-stu-id="3b95a-171">"administator" instead of "administrator" - [#9662](https://github.com/NuGet/Home/issues/9662)</span></span>
[<span data-ttu-id="3b95a-172">odalet</span><span class="sxs-lookup"><span data-stu-id="3b95a-172">odalet</span></span>](https://github.com/odalet) | [<span data-ttu-id="3b95a-173">3341</span><span class="sxs-lookup"><span data-stu-id="3b95a-173">3341</span></span>](https://github.com/NuGet/NuGet.Client/pull/3341) | <span data-ttu-id="3b95a-174">無効な AssemblyInformationalVersion レポートの NuGet パックが必要です。 "- [#5548](https://github.com/NuGet/Home/issues/5548)</span><span class="sxs-lookup"><span data-stu-id="3b95a-174">NuGet Pack with invalid AssemblyInformationalVersion reports "description is required" - [#5548](https://github.com/NuGet/Home/issues/5548)</span></span>
[<span data-ttu-id="3b95a-175">campersau</span><span class="sxs-lookup"><span data-stu-id="3b95a-175">campersau</span></span>](https://github.com/campersau) | [<span data-ttu-id="3b95a-176">3501</span><span class="sxs-lookup"><span data-stu-id="3b95a-176">3501</span></span>](https://github.com/NuGet/NuGet.Client/pull/3501) | <span data-ttu-id="3b95a-177">`RepositoryMetadata.Equals()` ブランチとコミットのプロパティを考慮しない- [#9613](https://github.com/NuGet/Home/issues/9613)</span><span class="sxs-lookup"><span data-stu-id="3b95a-177">`RepositoryMetadata.Equals()` does not account for Branch and Commit properties - [#9613](https://github.com/NuGet/Home/issues/9613)</span></span>
[<span data-ttu-id="3b95a-178">Youssef1313</span><span class="sxs-lookup"><span data-stu-id="3b95a-178">Youssef1313</span></span>](https://github.com/Youssef1313) | [<span data-ttu-id="3b95a-179">3599</span><span class="sxs-lookup"><span data-stu-id="3b95a-179">3599</span></span>](https://github.com/NuGet/NuGet.Client/pull/3599) | <span data-ttu-id="3b95a-180">Visual Studio の [エラー一覧] ウィンドウで [プログラム] をクリックすると、 https://docs.microsoft.com/nuget/reference/errors-and-warnings/  -  [#9934](https://github.com/NuGet/Home/issues/9934)に変わります</span><span class="sxs-lookup"><span data-stu-id="3b95a-180">Clicking NU code in Visual Studio Error List window should go to https://docs.microsoft.com/nuget/reference/errors-and-warnings/ - [#9934](https://github.com/NuGet/Home/issues/9934)</span></span>
[<span data-ttu-id="3b95a-181">ChrisMaddock</span><span class="sxs-lookup"><span data-stu-id="3b95a-181">ChrisMaddock</span></span>](https://github.com/ChrisMaddock) | [<span data-ttu-id="3b95a-182">3624</span><span class="sxs-lookup"><span data-stu-id="3b95a-182">3624</span></span>](https://github.com/NuGet/NuGet.Client/pull/3624) | <span data-ttu-id="3b95a-183">Visual Studio のオプションを使用して新しいパッケージソースを追加するときに ' https://' を使用する- [#9974](https://github.com/NuGet/Home/issues/9974)</span><span class="sxs-lookup"><span data-stu-id="3b95a-183">Use 'https://' when adding new package source through Visual Studio options - [#9974](https://github.com/NuGet/Home/issues/9974)</span></span>
<span data-ttu-id="3b95a-184">[[& Zok]](https://github.com/Therzok)</span><span class="sxs-lookup"><span data-stu-id="3b95a-184">[Therzok](https://github.com/Therzok)</span></span> | [<span data-ttu-id="3b95a-185">3636</span><span class="sxs-lookup"><span data-stu-id="3b95a-185">3636</span></span>](https://github.com/NuGet/NuGet.Client/pull/3636) | <span data-ttu-id="3b95a-186">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio`Mono [#9989](https://github.com/NuGet/Home/issues/9989)のパフォーマンスの問題</span><span class="sxs-lookup"><span data-stu-id="3b95a-186">`RuntimeEnvironmentHelper.IsRunningOnVisualStudio` performance issue on Mono - [#9989](https://github.com/NuGet/Home/issues/9989)</span></span>
[<span data-ttu-id="3b95a-187">thomaslevesque</span><span class="sxs-lookup"><span data-stu-id="3b95a-187">thomaslevesque</span></span>](https://github.com/thomaslevesque) | [<span data-ttu-id="3b95a-188">3442</span><span class="sxs-lookup"><span data-stu-id="3b95a-188">3442</span></span>](https://github.com/NuGet/NuGet.Client/pull/3442) | <span data-ttu-id="3b95a-189">SemanticVersion クラスの TypeConverter を追加する- [#9125](https://github.com/NuGet/Home/issues/9125)</span><span class="sxs-lookup"><span data-stu-id="3b95a-189">Add a TypeConverter for the SemanticVersion class - [#9125](https://github.com/NuGet/Home/issues/9125)</span></span>


## <a name="feedback-welcome"></a><span data-ttu-id="3b95a-190">フィードバックの開始</span><span class="sxs-lookup"><span data-stu-id="3b95a-190">Feedback welcome</span></span>

<span data-ttu-id="3b95a-191">お客様のフィードバックは Microsoft にとって重要です。</span><span class="sxs-lookup"><span data-stu-id="3b95a-191">Your feedback is important to us.</span></span>  <span data-ttu-id="3b95a-192">このリリースに問題がある場合は、GitHub の [問題](https://github.com/NuGet/Home/issues) と [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) で既存の問題を確認してください。</span><span class="sxs-lookup"><span data-stu-id="3b95a-192">If there are any problems with this release, check our [GitHub Issues](https://github.com/NuGet/Home/issues) and [Visual Studio Developer Community](https://developercommunity.visualstudio.com/) for existing issues.</span></span>  <span data-ttu-id="3b95a-193">NuGet 内の新しい問題については、 [GitHub の問題](hhttps://github.com/NuGet/Home/issues/new)を報告してください。</span><span class="sxs-lookup"><span data-stu-id="3b95a-193">For new issues within NuGet, please report a [GitHub Issue](hhttps://github.com/NuGet/Home/issues/new).</span></span>
<span data-ttu-id="3b95a-194">NuGet エクスペリエンスに関する一般的な問題については、[ **ヘルプ > [問題の報告** ] の下にあるお気に入りの IDE の [ [問題点の報告](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio)] オプションを使用してお知らせください。</span><span class="sxs-lookup"><span data-stu-id="3b95a-194">For general NuGet experience issues, let us know via the [Report a Problem](https://docs.microsoft.com/visualstudio/ide/how-to-report-a-problem-with-visual-studio) option found in your favorite IDE under **Help > Report a Problem**.</span></span>
