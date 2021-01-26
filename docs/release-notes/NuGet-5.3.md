---
title: NuGet 5.3 リリースノート
description: 新機能、バグ修正、および DCRs を含む NuGet 5.3 のリリースノート。
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 009a219139a767ee6453305be68ccce478b0ec75
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780125"
---
# <a name="nuget-53-release-notes"></a><span data-ttu-id="82bd7-103">NuGet 5.3 リリースノート</span><span class="sxs-lookup"><span data-stu-id="82bd7-103">NuGet 5.3 Release Notes</span></span>

<span data-ttu-id="82bd7-104">NuGet 配布の種類:</span><span class="sxs-lookup"><span data-stu-id="82bd7-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="82bd7-105">NuGet のバージョン</span><span class="sxs-lookup"><span data-stu-id="82bd7-105">NuGet version</span></span> | <span data-ttu-id="82bd7-106">利用可能な Visual Studio バージョン</span><span class="sxs-lookup"><span data-stu-id="82bd7-106">Available in Visual Studio version</span></span>| <span data-ttu-id="82bd7-107">利用可能な .NET SDK</span><span class="sxs-lookup"><span data-stu-id="82bd7-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="82bd7-108">**以降**</span><span class="sxs-lookup"><span data-stu-id="82bd7-108">**5.3.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="82bd7-109">Visual Studio 2019 バージョン 16.3</span><span class="sxs-lookup"><span data-stu-id="82bd7-109">Visual Studio 2019 version 16.3</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="82bd7-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="82bd7-110">[3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup></span></span> |
| [<span data-ttu-id="82bd7-111">**5.3.1**</span><span class="sxs-lookup"><span data-stu-id="82bd7-111">**5.3.1**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="82bd7-112">Visual Studio 2019 バージョン16.3.6</span><span class="sxs-lookup"><span data-stu-id="82bd7-112">Visual Studio 2019 version 16.3.6</span></span>](https://visualstudio.microsoft.com/downloads/) | [<span data-ttu-id="82bd7-113">将来のバージョン: 3.0.101</span><span class="sxs-lookup"><span data-stu-id="82bd7-113">Future version: 3.0.101</span></span>](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<span data-ttu-id="82bd7-114"><sup>1</sup>.NET Core ワークロードを含む Visual Studio 2019 と共にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="82bd7-114"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-53"></a><span data-ttu-id="82bd7-115">概要: 5.3 の新機能</span><span class="sxs-lookup"><span data-stu-id="82bd7-115">Summary: What's New in 5.3</span></span>

* <span data-ttu-id="82bd7-116">パッケージアイコンは、外部 URL を必要とするのではなく、[パッケージに埋め込むことができ](../reference/msbuild-targets.md#packing-an-icon-image-file)ます。</span><span class="sxs-lookup"><span data-stu-id="82bd7-116">[Package Icon can be embedded in the package](../reference/msbuild-targets.md#packing-an-icon-image-file), instead of needing an external URL.</span></span><span data-ttu-id="82bd7-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span><span class="sxs-lookup"><span data-stu-id="82bd7-117"> - [#352](https://github.com/NuGet/Home/issues/352)</span></span>

* <span data-ttu-id="82bd7-118">Packages.Config [#7281](https://github.com/NuGet/Home/issues/7281)に対する SHA の追跡と強制によるセキュリティ強化</span><span class="sxs-lookup"><span data-stu-id="82bd7-118">Improved security with SHA tracking and enforcement for Packages.Config - [#7281](https://github.com/NuGet/Home/issues/7281)</span></span>

* <span data-ttu-id="82bd7-119">廃止された、または従来の NuGet パッケージの廃止を有効にする[#2867](https://github.com/NuGet/Home/issues/2867)  |  [ブログの投稿](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/)  |  [ドキュメント](../nuget-org/deprecate-packages.md)</span><span class="sxs-lookup"><span data-stu-id="82bd7-119">Enable deprecation of obsolete/legacy NuGet Packages [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog post](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [Docs](../nuget-org/deprecate-packages.md)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="82bd7-120">このリリースで修正された問題</span><span class="sxs-lookup"><span data-stu-id="82bd7-120">Issues fixed in this release</span></span>

<span data-ttu-id="82bd7-121">**バグ**</span><span class="sxs-lookup"><span data-stu-id="82bd7-121">**Bugs**</span></span>

* <span data-ttu-id="82bd7-122">3.0.100 preview9 SDK で生成された NuGet パッケージは、2.2 SDK ユーザーが使用することはできません...タイムゾーンに応じて [#8603](https://github.com/NuGet/Home/issues/8603)</span><span class="sxs-lookup"><span data-stu-id="82bd7-122">NuGet packages produced with 3.0.100-preview9 SDK cannot be used by 2.2 SDK users...depending on your timezone [#8603](https://github.com/NuGet/Home/issues/8603)</span></span>

* <span data-ttu-id="82bd7-123">引用符 "パス内の文字が原因で、パスに無効な文字が含まれる" というエラーが発生する `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span><span class="sxs-lookup"><span data-stu-id="82bd7-123">Quote " characters in PATH cause "Illegal characters in path" failure in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)</span></span>

* <span data-ttu-id="82bd7-124">VS: アセンブリが完全に ngen されていません。 [#8513](https://github.com/NuGet/Home/issues/8513)</span><span class="sxs-lookup"><span data-stu-id="82bd7-124">VS: assemblies are fully ngen-ed not partially ngen-ed - [#8513](https://github.com/NuGet/Home/issues/8513)</span></span>

* <span data-ttu-id="82bd7-125">メモリ使用量の削減 (イベントからのサブスクリプションの解除)- [#8471](https://github.com/NuGet/Home/issues/8471)</span><span class="sxs-lookup"><span data-stu-id="82bd7-125">Reduce memory usage (unsubscribe from events) - [#8471](https://github.com/NuGet/Home/issues/8471)</span></span>

* <span data-ttu-id="82bd7-126">"Error_UnableToFindProjectInfo" メッセージは、文法が正しくありません- [#8441](https://github.com/NuGet/Home/issues/8441)</span><span class="sxs-lookup"><span data-stu-id="82bd7-126">"Error_UnableToFindProjectInfo" message is not grammatically correct - [#8441](https://github.com/NuGet/Home/issues/8441)</span></span>

* <span data-ttu-id="82bd7-127">NU1403 の改善-すべてのパッケージを検証し、予期される/実際の sha 値を含めます- [#8424](https://github.com/NuGet/Home/issues/8424)</span><span class="sxs-lookup"><span data-stu-id="82bd7-127">NU1403 improvements - validate all packages, include the expected/actual sha values - [#8424](https://github.com/NuGet/Home/issues/8424)</span></span>

* <span data-ttu-id="82bd7-128">#8401 内の複数の列挙型 `NuGetPackageManager.PreviewUpdatePackagesAsync`  -  [](https://github.com/NuGet/Home/issues/8401)</span><span class="sxs-lookup"><span data-stu-id="82bd7-128">Multiple enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)</span></span>

* <span data-ttu-id="82bd7-129">PluginProcess の "パブリック > 内部" の変更を元に戻す- [#8390](https://github.com/NuGet/Home/issues/8390)</span><span class="sxs-lookup"><span data-stu-id="82bd7-129">Revert "public -> internal" change in PluginProcess - [#8390](https://github.com/NuGet/Home/issues/8390)</span></span>

* <span data-ttu-id="82bd7-130">IVsPackageSourceProvider (...) の例外動作が正しく定義されていません- [#8383](https://github.com/NuGet/Home/issues/8383)</span><span class="sxs-lookup"><span data-stu-id="82bd7-130">IVsPackageSourceProvider.GetSources(…) has ill-defined exception behavior - [#8383](https://github.com/NuGet/Home/issues/8383)</span></span>

* <span data-ttu-id="82bd7-131">PluginManager コンストラクターを再度公開する- [#8379](https://github.com/NuGet/Home/issues/8379)</span><span class="sxs-lookup"><span data-stu-id="82bd7-131">Make PluginManager constructor public again - [#8379](https://github.com/NuGet/Home/issues/8379)</span></span>

* <span data-ttu-id="82bd7-132">PM UI [#8369](https://github.com/NuGet/Home/issues/8369)のリフレッシュレートを追跡するためのメトリック</span><span class="sxs-lookup"><span data-stu-id="82bd7-132">Metrics to track the refresh rate of the PM UI - [#8369](https://github.com/NuGet/Home/issues/8369)</span></span>

* <span data-ttu-id="82bd7-133">パッケージマネージャー UI を使用したインストール時の UI 更新の数を減らす- [#8358](https://github.com/NuGet/Home/issues/8358)</span><span class="sxs-lookup"><span data-stu-id="82bd7-133">Decrease the number of UI refreshes when installing through the Package Manager UI - [#8358](https://github.com/NuGet/Home/issues/8358)</span></span>

* <span data-ttu-id="82bd7-134">テレメトリ: datetime 値はカルチャ固有の形式を使用する- [#8351](https://github.com/NuGet/Home/issues/8351)</span><span class="sxs-lookup"><span data-stu-id="82bd7-134">Telemetry:  datetime values use culture-specific formats - [#8351](https://github.com/NuGet/Home/issues/8351)</span></span>

* <span data-ttu-id="82bd7-135">パッケージマネージャー UI の [参照] タブで UI の更新を減らす #6570- [#8339](https://github.com/NuGet/Home/issues/8339)</span><span class="sxs-lookup"><span data-stu-id="82bd7-135">Reduce UI refreshes in browse tab of Package Manager UI #6570 - [#8339](https://github.com/NuGet/Home/issues/8339)</span></span>

* <span data-ttu-id="82bd7-136">[テストの失敗]"構成ファイルを解析できません" というメッセージが2回表示され [#8320](https://github.com/NuGet/Home/issues/8320)</span><span class="sxs-lookup"><span data-stu-id="82bd7-136">[Test Failure] “Unable to parse config file” will prompt twice - [#8320](https://github.com/NuGet/Home/issues/8320)</span></span>

* <span data-ttu-id="82bd7-137">お客様の修正プログラムについて説明する適切なドキュメントページで、NU5037 エラーを発生させます (パッケージに必要な nuspec ファイルがありません)- [#8291](https://github.com/NuGet/Home/issues/8291)</span><span class="sxs-lookup"><span data-stu-id="82bd7-137">Raise NU5037 error with good doc page that explains customer fixes (The package is missing the required nuspec file) - [#8291](https://github.com/NuGet/Home/issues/8291)</span></span>

* <span data-ttu-id="82bd7-138">プロジェクトの RuntimeIdentifier が変更されると、ロックモードの復元が失敗する- [#8260](https://github.com/NuGet/Home/issues/8260)</span><span class="sxs-lookup"><span data-stu-id="82bd7-138">Locked-mode restore fails when a project's RuntimeIdentifier is changed - [#8260](https://github.com/NuGet/Home/issues/8260)</span></span>

* <span data-ttu-id="82bd7-139">VS レイジー [#8156](https://github.com/NuGet/Home/issues/8156)で設定を読み取ります。</span><span class="sxs-lookup"><span data-stu-id="82bd7-139">Make the Settings reading in VS lazy - [#8156](https://github.com/NuGet/Home/issues/8156)</span></span>

* <span data-ttu-id="82bd7-140">の回帰では、 `Nuget sources add` "the ': ' 文字、16進数値 0x3A, を名前に含めることはできません" エラー- [#7948](https://github.com/NuGet/Home/issues/7948)</span><span class="sxs-lookup"><span data-stu-id="82bd7-140">Regression in `Nuget sources add` causes "The ':' character, hexadecimal value 0x3A, cannot be included in a name" errors - [#7948](https://github.com/NuGet/Home/issues/7948)</span></span>

* <span data-ttu-id="82bd7-141">NuGet プラグイン資格情報プロバイダー-プロセスウィンドウを非表示にする- [#7511](https://github.com/NuGet/Home/issues/7511)</span><span class="sxs-lookup"><span data-stu-id="82bd7-141">NuGet plugin credential providers - hide the process window - [#7511](https://github.com/NuGet/Home/issues/7511)</span></span>

* <span data-ttu-id="82bd7-142">強制 PackagePathResolver は絶対パス [#7349](https://github.com/NuGet/Home/issues/7349)</span><span class="sxs-lookup"><span data-stu-id="82bd7-142">Enforce PackagePathResolver is an absolute path - [#7349](https://github.com/NuGet/Home/issues/7349)</span></span>

* <span data-ttu-id="82bd7-143">パッケージマネージャー UI の [インストール] タブと [更新] タブで UI の更新を減らす- [#6570](https://github.com/NuGet/Home/issues/6570)</span><span class="sxs-lookup"><span data-stu-id="82bd7-143">Reduce UI refreshes in install and update tabs of Package Manager UI - [#6570](https://github.com/NuGet/Home/issues/6570)</span></span>

<span data-ttu-id="82bd7-144">**DCR**</span><span class="sxs-lookup"><span data-stu-id="82bd7-144">**DCR:**</span></span>

* <span data-ttu-id="82bd7-145">NetStandard 2.1- [#8368](https://github.com/NuGet/Home/issues/8368)にマップするように Xamarin フレームワークを更新する</span><span class="sxs-lookup"><span data-stu-id="82bd7-145">Update Xamarin frameworks to map to NetStandard 2.1 - [#8368](https://github.com/NuGet/Home/issues/8368)</span></span>

* <span data-ttu-id="82bd7-146">パッケージマネージャーの [プレビューウィンドウ] の内容をインストール/更新用にコピーできるようにします。 [#8324](https://github.com/NuGet/Home/issues/8324)</span><span class="sxs-lookup"><span data-stu-id="82bd7-146">Enable copying the contents of package manager "preview window" for install/update - [#8324](https://github.com/NuGet/Home/issues/8324)</span></span>

* <span data-ttu-id="82bd7-147">[Proj ファイルの復元を有効にする]- [#8212](https://github.com/NuGet/Home/issues/8212)</span><span class="sxs-lookup"><span data-stu-id="82bd7-147">Enable restore on .proj files - [#8212](https://github.com/NuGet/Home/issues/8212)</span></span>

* <span data-ttu-id="82bd7-148">同時 `NUGET_NETFX_PLUGIN_PATHS` `NUGET_NETCORE_PLUGIN_PATHS` に両方の構成をサポートすると共に [#8151](https://github.com/NuGet/Home/issues/8151)</span><span class="sxs-lookup"><span data-stu-id="82bd7-148">Introduce `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` to support configuration of both at same time - [#8151](https://github.com/NuGet/Home/issues/8151)</span></span>

* <span data-ttu-id="82bd7-149">バージョン属性を使用して PackageDownload の複数のバージョンを有効にする- [#8074](https://github.com/NuGet/Home/issues/8074)</span><span class="sxs-lookup"><span data-stu-id="82bd7-149">Enable multiple versions for a PackageDownload via Version attribute - [#8074](https://github.com/NuGet/Home/issues/8074)</span></span>

* <span data-ttu-id="82bd7-150">-SolutionDirectory オプションと-PackageDirectory オプションを nuget.exe pack- [#7163](https://github.com/NuGet/Home/issues/7163)に追加する</span><span class="sxs-lookup"><span data-stu-id="82bd7-150">Add -SolutionDirectory and -PackageDirectory options to nuget.exe pack - [#7163](https://github.com/NuGet/Home/issues/7163)</span></span>

<span data-ttu-id="82bd7-151">**[このリリースで修正されるすべての問題の一覧-5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span><span class="sxs-lookup"><span data-stu-id="82bd7-151">**[List of all issues fixed in this release - 5.3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**</span></span>

## <a name="summary-whats-new-in-531"></a><span data-ttu-id="82bd7-152">概要: 5.3.1 の新機能</span><span class="sxs-lookup"><span data-stu-id="82bd7-152">Summary: What's New in 5.3.1</span></span>

* <span data-ttu-id="82bd7-153">プラグイン: タスクが取り消されました-キャンセルしてプラグインのインスタンス化に影響を与えることはできません- [#8648](https://github.com/NuGet/Home/issues/8648)</span><span class="sxs-lookup"><span data-stu-id="82bd7-153">Plugin: A task was canceled - don't let cancellations affect plugin instantiation - [#8648](https://github.com/NuGet/Home/issues/8648)</span></span>

* <span data-ttu-id="82bd7-154">1つのプロセスで (資格情報プロバイダーが使用されている場合) 復元タスクを2回安全に実行することはできません- [#8688](https://github.com/NuGet/Home/issues/8688)</span><span class="sxs-lookup"><span data-stu-id="82bd7-154">Restore Task cannot be safely run twice in one process (when Credential providers are used) - [#8688](https://github.com/NuGet/Home/issues/8688)</span></span>
