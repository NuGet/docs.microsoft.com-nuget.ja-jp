---
title: NuGet のエラーと警告のリファレンス
description: 警告とエラー NuGet、さまざまな操作中に、NuGet から発行されたへの参照を完了します。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/06/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: dcff20e35adc0a3dbcc7bef482f81a937cf059c5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="e161c-103">エラーと警告</span><span class="sxs-lookup"><span data-stu-id="e161c-103">Errors and warnings</span></span>

<span data-ttu-id="e161c-104">NuGet 4.3.0+ では、このトピックで説明の番号付けはエラーと警告し、関連する問題に対処するための詳細情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="e161c-104">In NuGet 4.3.0+, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span>

<span data-ttu-id="e161c-105">エラーと警告の次のとおり、のみで使用[PackageReference ベース](../consume-packages/package-references-in-project-files.md)プロジェクトおよび NuGet 4.3.0+ です。</span><span class="sxs-lookup"><span data-stu-id="e161c-105">The errors and warnings listed here are available only with [PackageReference-based](../consume-packages/package-references-in-project-files.md) projects and NuGet 4.3.0+.</span></span> <span data-ttu-id="e161c-106">NuGet では警告を抑制するか、それらのエラーへの昇格に MSBuild プロパティも使用します。</span><span class="sxs-lookup"><span data-stu-id="e161c-106">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="e161c-107">詳細については、次を参照してください。[する方法: コンパイラの警告を抑制する状況](/visualstudio/ide/how-to-suppress-compiler-warnings)、Visual Studio のマニュアルでします。</span><span class="sxs-lookup"><span data-stu-id="e161c-107">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="e161c-108">**エラー**</span><span class="sxs-lookup"><span data-stu-id="e161c-108">**Errors**</span></span>

| <span data-ttu-id="e161c-109">グループ化</span><span class="sxs-lookup"><span data-stu-id="e161c-109">Group</span></span> | <span data-ttu-id="e161c-110">エラー番号</span><span class="sxs-lookup"><span data-stu-id="e161c-110">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="e161c-111">無効な入力エラー</span><span class="sxs-lookup"><span data-stu-id="e161c-111">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="e161c-112">[NU1001](#nu1001)、 [NU1002](#nu1002)、 [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="e161c-112">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="e161c-113">パッケージとプロジェクトの不足エラー</span><span class="sxs-lookup"><span data-stu-id="e161c-113">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="e161c-114">[NU1100](#nu1100)、 [NU1101](#nu1101)、 [NU1102](#nu1102)、 [NU1103](#nu1103)、 [NU1104](#nu1104)、 [NU1105](#nu1105)、 [NU1106](#nu1106)、 [NU1107](#nu1107) (NU1607 以前) [NU1108](#nu1108) (NU1606 以前)</span><span class="sxs-lookup"><span data-stu-id="e161c-114">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="e161c-115">互換性に関するエラー</span><span class="sxs-lookup"><span data-stu-id="e161c-115">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="e161c-116">[NU1201](#nu1201)、 [NU1202](#nu1202)、 [NU1203](#nu1203)、 [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="e161c-116">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="e161c-117">**警告**</span><span class="sxs-lookup"><span data-stu-id="e161c-117">**Warnings**</span></span>

| <span data-ttu-id="e161c-118">グループ化</span><span class="sxs-lookup"><span data-stu-id="e161c-118">Group</span></span> | <span data-ttu-id="e161c-119">警告番号</span><span class="sxs-lookup"><span data-stu-id="e161c-119">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="e161c-120">無効な入力の警告</span><span class="sxs-lookup"><span data-stu-id="e161c-120">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="e161c-121">[NU1501](#nu1501)、 [NU1502](#nu1502)、 [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="e161c-121">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="e161c-122">予期しないパッケージのバージョンの警告</span><span class="sxs-lookup"><span data-stu-id="e161c-122">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="e161c-123">[NU1601](#nu1601)、 [NU1602](#nu1602)、 [NU1603](#nu1603)、 [NU1604](#nu1604)、 [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="e161c-123">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="e161c-124">競合回避モジュールの競合の警告</span><span class="sxs-lookup"><span data-stu-id="e161c-124">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="e161c-125">NU1608</span><span class="sxs-lookup"><span data-stu-id="e161c-125">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="e161c-126">パッケージのフォールバック警告</span><span class="sxs-lookup"><span data-stu-id="e161c-126">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="e161c-127">NU1701</span><span class="sxs-lookup"><span data-stu-id="e161c-127">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="e161c-128">フィードの警告</span><span class="sxs-lookup"><span data-stu-id="e161c-128">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="e161c-129">NU1801</span><span class="sxs-lookup"><span data-stu-id="e161c-129">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="e161c-130">NuGet の内部エラーと警告</span><span class="sxs-lookup"><span data-stu-id="e161c-130">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="e161c-131">[NU1000](#nu1000)、 [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="e161c-131">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |
| [<span data-ttu-id="e161c-132">署名付きパッケージ (作成および検証)</span><span class="sxs-lookup"><span data-stu-id="e161c-132">Signed packages (creation and verification)</span></span>](#signed-packages-creation-and-verification)| <span data-ttu-id="e161c-133">[NU3000](#nu3000)、 [NU3001](#nu3001)、 [NU3002](#nu3002)、 [NU3004](#nu3004)、 [NU3008](#nu3008)、 [NU3018](#nu3018)、 [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="e161c-133">[NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="e161c-134">無効な入力エラー</span><span class="sxs-lookup"><span data-stu-id="e161c-134">Invalid input errors</span></span>

<span data-ttu-id="e161c-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="e161c-135">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="e161c-136">NU1001</span><span class="sxs-lookup"><span data-stu-id="e161c-136">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-137">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-137">**Issue**</span></span> | <span data-ttu-id="e161c-138">プロジェクトには、1 つまたは複数のフレームワークが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="e161c-138">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="e161c-139">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-139">**Example message**</span></span> | <span data-ttu-id="e161c-140">*プロジェクト projA では、どのターゲット フレームワーク c:\tmp\projA.csproj で指定されていません*</span><span class="sxs-lookup"><span data-stu-id="e161c-140">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |
| <span data-ttu-id="e161c-141">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-141">**Solution**</span></span> | <span data-ttu-id="e161c-142">追加、`TargetFramework`または`TargetFrameworks`プロパティを指定したプロジェクト ファイルです。</span><span class="sxs-lookup"><span data-stu-id="e161c-142">Add a `TargetFramework` or `TargetFrameworks` property to the specified project file.</span></span> |

### <a name="nu1002"></a><span data-ttu-id="e161c-143">NU1002</span><span class="sxs-lookup"><span data-stu-id="e161c-143">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-144">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-144">**Issue**</span></span> | <span data-ttu-id="e161c-145">入力とクリア キーワードの組み合わせが無効です。</span><span class="sxs-lookup"><span data-stu-id="e161c-145">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="e161c-146">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-146">**Example message**</span></span> | <span data-ttu-id="e161c-147">*'CLEAR' では使用できませんの他の値と共に*</span><span class="sxs-lookup"><span data-stu-id="e161c-147">*'CLEAR' cannot be used in conjunction with other values*</span></span> |
| <span data-ttu-id="e161c-148">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-148">**Solution**</span></span> | <span data-ttu-id="e161c-149">クリアを単独で使用し、その他のすべての入力を省略します。</span><span class="sxs-lookup"><span data-stu-id="e161c-149">Use CLEAR by itself and omit all other inputs.</span></span> |

### <a name="nu1003"></a><span data-ttu-id="e161c-150">NU1003</span><span class="sxs-lookup"><span data-stu-id="e161c-150">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-151">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-151">**Issue**</span></span> | <span data-ttu-id="e161c-152">`PackageTargetFallback` および`AssetTargetFallback`資産を選択するための動作の違いを提供し、一緒に使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="e161c-152">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="e161c-153">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-153">**Example message**</span></span> | <span data-ttu-id="e161c-154">*PackageTargetFallback と AssetTargetFallback に使用することはできません。プロジェクトの環境から PackageTargetFallback(deprecated) 参照を削除します。*</span><span class="sxs-lookup"><span data-stu-id="e161c-154">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |
| <span data-ttu-id="e161c-155">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-155">**Solution**</span></span> | <span data-ttu-id="e161c-156">削除、非推奨`PackageTargetFallback`プロジェクトからの要素。</span><span class="sxs-lookup"><span data-stu-id="e161c-156">Remove the deprecated `PackageTargetFallback` element from the project.</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="e161c-157">パッケージとプロジェクトの不足エラー</span><span class="sxs-lookup"><span data-stu-id="e161c-157">Missing package and project errors</span></span>

<span data-ttu-id="e161c-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="e161c-158">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="e161c-159">NU1100</span><span class="sxs-lookup"><span data-stu-id="e161c-159">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-160">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-160">**Issue**</span></span> | <span data-ttu-id="e161c-161">依存関係グループを解決できません。</span><span class="sxs-lookup"><span data-stu-id="e161c-161">A dependency group not be resolved.</span></span> <span data-ttu-id="e161c-162">これは、パッケージまたはプロジェクトではない型での一般的な問題です。</span><span class="sxs-lookup"><span data-stu-id="e161c-162">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="e161c-163">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-163">**Example message**</span></span> | <span data-ttu-id="e161c-164">*Net45 を System.Missing を解決できません。*</span><span class="sxs-lookup"><span data-stu-id="e161c-164">*Unable to resolve System.Missing for net45*</span></span> |
| <span data-ttu-id="e161c-165">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-165">**Solution**</span></span> | <span data-ttu-id="e161c-166">プロジェクト ファイルを開き、その依存関係の一覧を確認します。</span><span class="sxs-lookup"><span data-stu-id="e161c-166">Open the project file and examine the list of its dependencies.</span></span> <span data-ttu-id="e161c-167">それぞれの依存関係を使用しているパッケージ ソースに存在して、パッケージがプロジェクトのターゲット フレームワークをサポートしていることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="e161c-167">Check that each dependency exists on the package sources you're using, and that the package supports the project's target framework.</span></span> |

### <a name="nu1101"></a><span data-ttu-id="e161c-168">NU1101</span><span class="sxs-lookup"><span data-stu-id="e161c-168">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-169">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-169">**Issue**</span></span> | <span data-ttu-id="e161c-170">パッケージのソースに見つかりません。</span><span class="sxs-lookup"><span data-stu-id="e161c-170">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="e161c-171">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-171">**Example message**</span></span> | <span data-ttu-id="e161c-172">*パッケージ System.Missing が見つかりません。ソースでは、この id を持つパッケージが存在しません: dotnet コア、dotnet roslyn、nuget.org*</span><span class="sxs-lookup"><span data-stu-id="e161c-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |
| <span data-ttu-id="e161c-173">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-173">**Solution**</span></span> | <span data-ttu-id="e161c-174">正しいパッケージ id とバージョン番号を使用していることを確認する Visual Studio でプロジェクトの依存関係を確認します。</span><span class="sxs-lookup"><span data-stu-id="e161c-174">Examine the project's dependencies in Visual Studio to be sure you're using the correct package identifier and version number.</span></span> <span data-ttu-id="e161c-175">確認することも、[の NuGet 構成](../consume-packages/Configuring-NuGet-Behavior.md)パッケージ ソースを識別することです。</span><span class="sxs-lookup"><span data-stu-id="e161c-175">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="e161c-176">されているパッケージを使用する場合[セマンティック バージョニング 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200)を使用していることを確認してください、 [V3 フィード](https://api.nuget.org/v3/index.json)で、[の NuGet 構成](../consume-packages/Configuring-NuGet-Behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="e161c-176">If you use packages that have [Semantic Versioning 2.0.0](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#semantic-versioning-200), please make sure that you are using the [V3 feed](https://api.nuget.org/v3/index.json) in the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> |

### <a name="nu1102"></a><span data-ttu-id="e161c-177">NU1102</span><span class="sxs-lookup"><span data-stu-id="e161c-177">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-178">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-178">**Issue**</span></span> | <span data-ttu-id="e161c-179">パッケージ識別子が見つかりましたが、ソースのいずれかで指定した依存関係の範囲内のバージョンが見つかりません。</span><span class="sxs-lookup"><span data-stu-id="e161c-179">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> <span data-ttu-id="e161c-180">パッケージとユーザーではなく、範囲を指定する場合があります。</span><span class="sxs-lookup"><span data-stu-id="e161c-180">The range might be specified by a package and not the user.</span></span> |
| <span data-ttu-id="e161c-181">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-181">**Example message**</span></span> | <span data-ttu-id="e161c-182">*NuGet.Versioning バージョンでパッケージを見つけることができません (> = 9.0.1)<br/> -nuget.org で見つかった 30 版 [バージョンに最も近い: 4.0.0]<br/> -dotnet buildtools で見つかった 10 バージョン [バージョンに最も近い: 4.0.0-rc-2129]<br/> -9 の検出NuGetVolatile のバージョン [バージョンに最も近い: 3.0.0-beta-00032]<br/> -0 のバージョンを記載 dotnet コア<br/>-dotnet roslyn で 0 バージョンを検出*</span><span class="sxs-lookup"><span data-stu-id="e161c-182">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="e161c-183">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-183">**Solution**</span></span> | <span data-ttu-id="e161c-184">パッケージのバージョンを解決するプロジェクト ファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="e161c-184">Edit the project file to correct the package version.</span></span> <span data-ttu-id="e161c-185">確認することも、[の NuGet 構成](../consume-packages/Configuring-NuGet-Behavior.md)パッケージ ソースを識別することです。</span><span class="sxs-lookup"><span data-stu-id="e161c-185">Also check that the [NuGet configuration](../consume-packages/Configuring-NuGet-Behavior.md) identifies the package sources your expect to be using.</span></span> <span data-ttu-id="e161c-186">このパッケージがプロジェクトで直接参照されている場合、requeted バージョンを変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e161c-186">You may need to change the requeted version if this package is referenced by the project directly.</span></span> |

### <a name="nu1103"></a><span data-ttu-id="e161c-187">NU1103</span><span class="sxs-lookup"><span data-stu-id="e161c-187">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-188">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-188">**Issue**</span></span> | <span data-ttu-id="e161c-189">プロジェクトの依存関係の範囲、安定したバージョンの指定が、その範囲に安定したバージョンが見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="e161c-189">The project specified a stable version for the dependency range, but no stable versions were found in that range.</span></span> <span data-ttu-id="e161c-190">プレリリース版は見つかりましたが、許可されていません。</span><span class="sxs-lookup"><span data-stu-id="e161c-190">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="e161c-191">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-191">**Example message**</span></span> | <span data-ttu-id="e161c-192">*バージョンと安定したパッケージ NuGet.Versioning を見つけることができません (> = 3.0.0)<br/> -dotnet buildtools で見つかった 10 バージョン [バージョンに最も近い: 4.0.0-rc-2129]<br/> -NuGetVolatile で見つかった 9 版 [バージョンに最も近い: 3.0.0-beta-00032]<br/> -0 のバージョンを記載 dotnet コア<br/>-dotnet roslyn で 0 バージョンが見つかりません*</span><span class="sxs-lookup"><span data-stu-id="e161c-192">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |
| <span data-ttu-id="e161c-193">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-193">**Solution**</span></span> |  <span data-ttu-id="e161c-194">プレリリース版を含めるようにプロジェクト ファイルのバージョンの範囲を編集します。</span><span class="sxs-lookup"><span data-stu-id="e161c-194">Edit the version range in the project file to include pre-release versions.</span></span> <span data-ttu-id="e161c-195">参照してください[パッケージのバージョン管理](../reference/Package-Versioning.md)です。</span><span class="sxs-lookup"><span data-stu-id="e161c-195">See [Package versioning](../reference/Package-Versioning.md).</span></span> |

### <a name="nu1104"></a><span data-ttu-id="e161c-196">NU1104</span><span class="sxs-lookup"><span data-stu-id="e161c-196">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-197">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-197">**Issue**</span></span> | <span data-ttu-id="e161c-198">ProjectReference は、存在しないファイルを指します。</span><span class="sxs-lookup"><span data-stu-id="e161c-198">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="e161c-199">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-199">**Example message**</span></span> | <span data-ttu-id="e161c-200">*プロジェクト参照では、'c:\a.csproj' は存在しません。プロジェクトへの参照が有効であると、プロジェクト ファイルが存在することを確認してください。*</span><span class="sxs-lookup"><span data-stu-id="e161c-200">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |
| <span data-ttu-id="e161c-201">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-201">**Solution**</span></span> | <span data-ttu-id="e161c-202">か、参照先のプロジェクトへのパスを修正するか、参照を削除するプロジェクト ファイルを編集する必要がなくなった場合。</span><span class="sxs-lookup"><span data-stu-id="e161c-202">Edit the project file to either correct the path to the referenced project or to remove the reference altogether if it's no longer needed.</span></span> |

### <a name="nu1105"></a><span data-ttu-id="e161c-203">NU1105</span><span class="sxs-lookup"><span data-stu-id="e161c-203">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-204">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-204">**Issue**</span></span> | <span data-ttu-id="e161c-205">プロジェクト ファイルが存在しますが、その復元に関する情報が指定されていません。</span><span class="sxs-lookup"><span data-stu-id="e161c-205">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="e161c-206">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-206">**Example message**</span></span> | <span data-ttu-id="e161c-207">*'C:\a.csproj' のプロジェクト情報を読み取れません。プロジェクト ファイルには、復元に必要なターゲットを無効または不足している可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="e161c-207">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="e161c-208">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-208">**Solution**</span></span> | <span data-ttu-id="e161c-209">Visual Studio で、エラーに、プロジェクトにプロジェクトの再読み込みする場合に、読み込まれているがある可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e161c-209">In Visual Studio, the error could mean that the project is unloaded, in which case reload the project.</span></span> <span data-ttu-id="e161c-210">コマンドラインからこのまたはことを意味、ファイルが壊れていることが含まれていないカスタム"インポート"の後に、プロジェクトを読み込むへの復元に必要なターゲットです。</span><span class="sxs-lookup"><span data-stu-id="e161c-210">From the command line this could mean that the file is corrupt or that it doesn't contain the custom "after imports" target needed for restore to read the project.</span></span> <span data-ttu-id="e161c-211">プロジェクト ファイルが有効であり"インポート"の後にターゲットを含むことを確認してください。</span><span class="sxs-lookup"><span data-stu-id="e161c-211">Check that the project file is valid and contains an "after imports" target.</span></span> |

### <a name="nu1106"></a><span data-ttu-id="e161c-212">NU1106</span><span class="sxs-lookup"><span data-stu-id="e161c-212">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-213">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-213">**Issue**</span></span> | <span data-ttu-id="e161c-214">依存関係の制約を解決することはできません。</span><span class="sxs-lookup"><span data-stu-id="e161c-214">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="e161c-215">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-215">**Example message**</span></span> | <span data-ttu-id="e161c-216">*{Id} の矛盾する要求を満たすことができません: {競合パス} フレームワーク: {ターゲット グラフ}*</span><span class="sxs-lookup"><span data-stu-id="e161c-216">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |
| <span data-ttu-id="e161c-217">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-217">**Solution**</span></span> | <span data-ttu-id="e161c-218">正確なバージョンではなく、依存関係の制約のない複数の範囲を指定するプロジェクト ファイルを編集します。</span><span class="sxs-lookup"><span data-stu-id="e161c-218">Edit the project file to specify more open-ended ranges for the dependency rather than an exact version.</span></span> |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="e161c-219">NU1107 (NU1607 以前)</span><span class="sxs-lookup"><span data-stu-id="e161c-219">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-220">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-220">**Issue**</span></span> | <span data-ttu-id="e161c-221">パッケージ間で依存関係の制約を解決できません。</span><span class="sxs-lookup"><span data-stu-id="e161c-221">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="e161c-222">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-222">**Example message**</span></span> | <span data-ttu-id="e161c-223">*バージョンの競合の NuGet.Versioning が検出されました。この問題を解決するのには、プロジェクトから直接パッケージを参照します。<br/>NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="e161c-223">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |
| <span data-ttu-id="e161c-224">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-224">**Solution**</span></span> | <span data-ttu-id="e161c-225">正確なバージョンに依存関係の制約を含むパッケージでは、他のパッケージを必要な場合は、バージョンを増やすには許可されません。</span><span class="sxs-lookup"><span data-stu-id="e161c-225">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> <span data-ttu-id="e161c-226">必要な正しいバージョンを直接 (プロジェクト ファイル) 内のプロジェクトへの参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="e161c-226">Add a reference to the project directly (in the project file) with the exact version required.</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="e161c-227">NU1108 (NU1606 以前)</span><span class="sxs-lookup"><span data-stu-id="e161c-227">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-228">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-228">**Issue**</span></span> | <span data-ttu-id="e161c-229">循環する依存関係が検出されました。</span><span class="sxs-lookup"><span data-stu-id="e161c-229">A circular dependency was detected.</span></span> |
| <span data-ttu-id="e161c-230">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-230">**Example message**</span></span> | <span data-ttu-id="e161c-231">*サイクルが検出されました: A が B]-> [A]-> [*</span><span class="sxs-lookup"><span data-stu-id="e161c-231">*Cycle detected: A -> B -> A*</span></span> |
| <span data-ttu-id="e161c-232">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-232">**Solution**</span></span> | <span data-ttu-id="e161c-233">パッケージが正しく作成されていません。バグを修正するパッケージの所有者に問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="e161c-233">The package is authored incorrectly; contact the package owner to correct the bug.</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="e161c-234">互換性に関するエラー</span><span class="sxs-lookup"><span data-stu-id="e161c-234">Compatibility errors</span></span>

<span data-ttu-id="e161c-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="e161c-235">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="e161c-236">NU1201</span><span class="sxs-lookup"><span data-stu-id="e161c-236">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-237">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-237">**Issue**</span></span> | <span data-ttu-id="e161c-238">依存関係プロジェクトには、現在のプロジェクトと互換性のあるフレームワークが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="e161c-238">A dependency project doesn't contain a framework compatible with the current project.</span></span> <span data-ttu-id="e161c-239">通常、プロジェクトのターゲット フレームワークは、プロジェクトが使用より高いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="e161c-239">Typically, the project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="e161c-240">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-240">**Example message**</span></span> | <span data-ttu-id="e161c-241">*プロジェクト ServerWeb は netstandard1.3 と互換性がありません (です。NETStandard, Version = v1.3)。プロジェクトの ServerWeb サポート:<br/> -netstandard1.6 (です。NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (です。NETCoreApp, Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="e161c-241">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |
| <span data-ttu-id="e161c-242">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-242">**Solution**</span></span> | <span data-ttu-id="e161c-243">プロジェクトのターゲット フレームワークを使用するプロジェクトよりも等しいまたはそれ以前のバージョンに変更します。</span><span class="sxs-lookup"><span data-stu-id="e161c-243">Change the project's target framework to an equal or lower version than the consuming project.</span></span> |

### <a name="nu1202"></a><span data-ttu-id="e161c-244">NU1202</span><span class="sxs-lookup"><span data-stu-id="e161c-244">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-245">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-245">**Issue**</span></span> | <span data-ttu-id="e161c-246">依存関係パッケージには、プロジェクトと互換性のある任意のアセットが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="e161c-246">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="e161c-247">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-247">**Example message**</span></span> | <span data-ttu-id="e161c-248">*パッケージ System.ComponentModel.EventBasedAsync 4.0.11 は netstandard1.3 と互換性がありません (です。NETStandard, Version = v1.3)。System.ComponentModel.EventBasedAsync 4.0.11 サポートをパッケージ化:<br/> -monoandroid10 (MonoAndroid、バージョン = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (です。NETFramework, Version = v4.5)<br/> -netcore50 (です。NETCore, Version = v5.0)<br/> -netstandard1.0 (です。NETStandard, Version = v1.0)<br/> -portable net45 + win8 + wp8 + wpa81 (です。NETPortable、バージョン v0.0、プロファイルを = = Profile259)<br/> -win8 (Windows、バージョン = バージョン 8.0)<br/> -wp8 (WindowsPhone, Version = バージョン 8.0)<br/> -wpa81 (WindowsPhoneApp、バージョン = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="e161c-248">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|
| <span data-ttu-id="e161c-249">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-249">**Solution**</span></span> | <span data-ttu-id="e161c-250">パッケージをサポートするには、プロジェクトのターゲット フレームワークを変更します。</span><span class="sxs-lookup"><span data-stu-id="e161c-250">Change the project's target framework to one that the package supports.</span></span> |

### <a name="nu1203"></a><span data-ttu-id="e161c-251">NU1203</span><span class="sxs-lookup"><span data-stu-id="e161c-251">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-252">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-252">**Issue**</span></span> | <span data-ttu-id="e161c-253">パッケージがプロジェクトをサポートしない`RuntimeIdentifier`です。</span><span class="sxs-lookup"><span data-stu-id="e161c-253">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="e161c-254">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-254">**Example message**</span></span> | <span data-ttu-id="e161c-255">*System.Example 1.0.0 a.dll のコンパイル時参照アセンブリ net461、上には互換性のあるランタイム アセンブリが存在しません。*</span><span class="sxs-lookup"><span data-stu-id="e161c-255">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |
| <span data-ttu-id="e161c-256">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-256">**Solution**</span></span> | <span data-ttu-id="e161c-257">変更、`RuntimeIdentifier`必要に応じて、プロジェクトで使用される値。</span><span class="sxs-lookup"><span data-stu-id="e161c-257">Change the `RuntimeIdentifier` values used in the project as needed.</span></span> |

### <a name="nu1401"></a><span data-ttu-id="e161c-258">NU1401</span><span class="sxs-lookup"><span data-stu-id="e161c-258">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-259">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-259">**Issue**</span></span> | <span data-ttu-id="e161c-260">パッケージには、機能、または NuGet のインストールされているバージョンでサポートされていないフレームワークが必要です。</span><span class="sxs-lookup"><span data-stu-id="e161c-260">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="e161c-261">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-261">**Example message**</span></span> | <span data-ttu-id="e161c-262">*'NuGet.Versioning' パッケージは NuGet クライアント バージョン '5.0.0' を必要以上に設定するが現在の NuGet バージョンは '4.3.0' です。*</span><span class="sxs-lookup"><span data-stu-id="e161c-262">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'.*</span></span> |
| <span data-ttu-id="e161c-263">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-263">**Solution**</span></span> | <span data-ttu-id="e161c-264">新しいバージョンの NuGet をインストールします。</span><span class="sxs-lookup"><span data-stu-id="e161c-264">Install a newer version of NuGet.</span></span> <span data-ttu-id="e161c-265">参照してください[NuGet のインストールのクライアント ツール](../install-nuget-client-tools.md)です。</span><span class="sxs-lookup"><span data-stu-id="e161c-265">See [Installing NuGet client tools](../install-nuget-client-tools.md).</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="e161c-266">無効な入力の警告</span><span class="sxs-lookup"><span data-stu-id="e161c-266">Invalid input warnings</span></span>

<span data-ttu-id="e161c-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="e161c-267">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="e161c-268">NU1501</span><span class="sxs-lookup"><span data-stu-id="e161c-268">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-269">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-269">**Issue**</span></span> | <span data-ttu-id="e161c-270">操作しようとして、プロジェクトの復元に見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="e161c-270">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="e161c-271">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-271">**Example message**</span></span> | <span data-ttu-id="e161c-272">*フォルダー 'c:\projects\a' に復元するプロジェクトが含まれていません。*</span><span class="sxs-lookup"><span data-stu-id="e161c-272">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |
| <span data-ttu-id="e161c-273">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-273">**Solution**</span></span> | <span data-ttu-id="e161c-274">プロジェクトを含むフォルダーには、nuget の復元を実行します。</span><span class="sxs-lookup"><span data-stu-id="e161c-274">Run nuget restore in a folder that contains a project.</span></span> |

### <a name="nu1502"></a><span data-ttu-id="e161c-275">NU1502</span><span class="sxs-lookup"><span data-stu-id="e161c-275">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-276">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-276">**Issue**</span></span> | <span data-ttu-id="e161c-277">`RuntimeSupports` 無効なプロファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="e161c-277">`RuntimeSupports` contains an invalid profile.</span></span> <span data-ttu-id="e161c-278">通常、サポートしているプロファイルに見つからなかった、`runtime.json`現在の依存関係パッケージからファイル。</span><span class="sxs-lookup"><span data-stu-id="e161c-278">Typically, the supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span>|
| <span data-ttu-id="e161c-279">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-279">**Example message**</span></span> | <span data-ttu-id="e161c-280">*不明な互換性プロファイル: aaa*</span><span class="sxs-lookup"><span data-stu-id="e161c-280">*Unknown Compatibility Profile: aaa*</span></span> |
| <span data-ttu-id="e161c-281">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-281">**Solution**</span></span> | <span data-ttu-id="e161c-282">チェック、`RuntimeSupports`プロジェクト内の値。</span><span class="sxs-lookup"><span data-stu-id="e161c-282">Check the `RuntimeSupports` value in your project.</span></span> |

### <a name="nu1503"></a><span data-ttu-id="e161c-283">NU1503</span><span class="sxs-lookup"><span data-stu-id="e161c-283">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-284">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-284">**Issue**</span></span> | <span data-ttu-id="e161c-285">依存関係プロジェクトでは、NuGet の復元のターゲットをインポートしません。</span><span class="sxs-lookup"><span data-stu-id="e161c-285">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="e161c-286">NU1105 に似ていますが、ここで、プロジェクトがスキップされた、すべての復元が失敗の原因ではなく無視します。</span><span class="sxs-lookup"><span data-stu-id="e161c-286">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="e161c-287">複雑なソリューションでもある復元をサポートしない可能性があるプロジェクトの他の種類。</span><span class="sxs-lookup"><span data-stu-id="e161c-287">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="e161c-288">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-288">**Example message**</span></span> | <span data-ttu-id="e161c-289">*プロジェクト 'c:\a.csproj' の復元をスキップしています。プロジェクト ファイルには、復元に必要なターゲットを無効または不足している可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="e161c-289">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |
| <span data-ttu-id="e161c-290">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-290">**Solution**</span></span> | <span data-ttu-id="e161c-291">プロジェクトの復元は自動的にインポートする共通のプロパティ/ターゲットはインポートしない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="e161c-291">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="e161c-292">プロジェクトを復元する必要がある場合は無視できます。</span><span class="sxs-lookup"><span data-stu-id="e161c-292">If the project doesn't need to be restored this can be ignored.</span></span> <span data-ttu-id="e161c-293">それ以外の場合、復元のターゲットを追加する影響を受けるプロジェクトを編集します。</span><span class="sxs-lookup"><span data-stu-id="e161c-293">Otherwise, edit the affected project to add targets for restore.</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="e161c-294">予期しないパッケージのバージョンの警告</span><span class="sxs-lookup"><span data-stu-id="e161c-294">Unexpected package version warnings</span></span>

<span data-ttu-id="e161c-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="e161c-295">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="e161c-296">NU1601</span><span class="sxs-lookup"><span data-stu-id="e161c-296">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-297">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-297">**Issue**</span></span> | <span data-ttu-id="e161c-298">直接プロジェクトの依存関係が、指定したプロジェクトより新しいバージョンに高くなります。</span><span class="sxs-lookup"><span data-stu-id="e161c-298">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="e161c-299">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-299">**Example message**</span></span> | <span data-ttu-id="e161c-300">*指定された依存関係が NuGet.Versioning (> = 3.5.0) NuGet.Versioning 4.0.0 で終了しましたが、します。*</span><span class="sxs-lookup"><span data-stu-id="e161c-300">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |
| <span data-ttu-id="e161c-301">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-301">**Solution**</span></span> | <span data-ttu-id="e161c-302">プロジェクト内の依存関係を適切なバージョンに更新します。</span><span class="sxs-lookup"><span data-stu-id="e161c-302">Update the dependency in the project to an appropriate version.</span></span> |

### <a name="nu1602"></a><span data-ttu-id="e161c-303">NU1602</span><span class="sxs-lookup"><span data-stu-id="e161c-303">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-304">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-304">**Issue**</span></span> | <span data-ttu-id="e161c-305">パッケージの依存関係には、下限値がありません。</span><span class="sxs-lookup"><span data-stu-id="e161c-305">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="e161c-306">これは、検索への復元を許可しない、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="e161c-306">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="e161c-307">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="e161c-307">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="e161c-308">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="e161c-308">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="e161c-309">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-309">**Example message**</span></span> | <span data-ttu-id="e161c-310">*NuGet.Packaging 4.0.0 では、依存 NuGet.Versioning (> 3.5.0) のため、下限は提供されません。3.6.0 のおおよその最適な一致が解決されました。*</span><span class="sxs-lookup"><span data-stu-id="e161c-310">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |
| <span data-ttu-id="e161c-311">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-311">**Solution**</span></span> | <span data-ttu-id="e161c-312">これは通常、パッケージ作成エラーです。</span><span class="sxs-lookup"><span data-stu-id="e161c-312">This is usually a package authoring error.</span></span> <span data-ttu-id="e161c-313">この問題を解決するのには、パッケージの作成者に問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="e161c-313">Contact the package author to resolve the issue.</span></span> |

### <a name="nu1603"></a><span data-ttu-id="e161c-314">NU1603</span><span class="sxs-lookup"><span data-stu-id="e161c-314">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-315">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-315">**Issue**</span></span> | <span data-ttu-id="e161c-316">パッケージの依存関係は、バージョンが見つかりませんでしたを指定します。</span><span class="sxs-lookup"><span data-stu-id="e161c-316">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="e161c-317">通常、パッケージ ソースでは、予想される下限バージョンは含まれません。</span><span class="sxs-lookup"><span data-stu-id="e161c-317">Typically, the package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="e161c-318">以降のバージョンは、に対して、パッケージが作成されたものと異なるを代わりに、使用されました。</span><span class="sxs-lookup"><span data-stu-id="e161c-318">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="e161c-319">つまり、復元が見つかりませんでした、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="e161c-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="e161c-320">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="e161c-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="e161c-321">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="e161c-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="e161c-322">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-322">**Example message**</span></span> | <span data-ttu-id="e161c-323">NuGet.Packaging 4.0.0 NuGet.Versioning によって異なります (> = 4.0.0) が、4.0.0 が見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="e161c-323">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="e161c-324">5.0.0 以降のおおよその最適な一致が解決されました。</span><span class="sxs-lookup"><span data-stu-id="e161c-324">An approximate best match of 5.0.0 was resolved.</span></span> |
| <span data-ttu-id="e161c-325">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-325">**Solution**</span></span> | <span data-ttu-id="e161c-326">期待どおりパッケージがリリースされていない場合、パッケージの作成エラーでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="e161c-326">If the package expected has not been released then this may be a package authoring error.</span></span> <span data-ttu-id="e161c-327">この問題を解決するのには、パッケージの作成者に問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="e161c-327">Contact the package author to resolve the issue.</span></span> <span data-ttu-id="e161c-328">パッケージがリリースされている場合、上にある使用可能なパッケージ ソースを使用しているを調べます。</span><span class="sxs-lookup"><span data-stu-id="e161c-328">If the package has been released, then check that it's available on the package sources you're using.</span></span> <span data-ttu-id="e161c-329">プライベートのソースを使用する場合は、そのフィードのパッケージを更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="e161c-329">If using a private source, you may need to update the package on that feed.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="e161c-330">NU1604</span><span class="sxs-lookup"><span data-stu-id="e161c-330">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-331">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-331">**Issue**</span></span> | <span data-ttu-id="e161c-332">プロジェクトの依存関係、下限が定義されません。</span><span class="sxs-lookup"><span data-stu-id="e161c-332">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="e161c-333">つまり、復元が見つかりませんでした、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="e161c-333">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="e161c-334">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="e161c-334">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="e161c-335">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="e161c-335">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="e161c-336">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-336">**Example message**</span></span> | <span data-ttu-id="e161c-337">*プロジェクトの依存関係 NuGet.Versioning (< = 9.0.0) doe が包括的の下限値が含まれていません。結果の整合性の復元に依存関係のバージョンに下限の境界を含めます。*</span><span class="sxs-lookup"><span data-stu-id="e161c-337">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |
| <span data-ttu-id="e161c-338">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-338">**Solution**</span></span> | <span data-ttu-id="e161c-339">プロジェクトの更新`PackageReference``Version`属性を下限の境界が含まれます。</span><span class="sxs-lookup"><span data-stu-id="e161c-339">Update the project's `PackageReference` `Version` attribute to include a lower bound.</span></span> |

### <a name="nu1605"></a><span data-ttu-id="e161c-340">NU1605</span><span class="sxs-lookup"><span data-stu-id="e161c-340">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-341">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-341">**Issue**</span></span> | <span data-ttu-id="e161c-342">依存関係パッケージには、パッケージの復元が最終的により高いバージョンでバージョン制約が指定されています。</span><span class="sxs-lookup"><span data-stu-id="e161c-342">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> <span data-ttu-id="e161c-343">"Wins"最も近いルール パッケージを解決するときに、原因は、グラフ内の最も近いパッケージが離れているパッケージをオーバーライドして可能性がありますされています。</span><span class="sxs-lookup"><span data-stu-id="e161c-343">That is, because of the "nearest wins" rule when resolving packages, a nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="e161c-344">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-344">**Example message**</span></span> | <span data-ttu-id="e161c-345">*パッケージのダウン グレードが検出されました: 3.5.0 に 4.0.0 から NuGet.Versioning です。異なるバージョンを選択するプロジェクトから直接パッケージを参照します。<br/>NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="e161c-345">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |
| <span data-ttu-id="e161c-346">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-346">**Solution**</span></span> | <span data-ttu-id="e161c-347">新しいバージョンを使用するパッケージのためのプロジェクトへの直接参照を追加します。</span><span class="sxs-lookup"><span data-stu-id="e161c-347">Add a direct reference to the project for the higher version of the package that you want to use.</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="e161c-348">競合回避モジュールの競合の警告</span><span class="sxs-lookup"><span data-stu-id="e161c-348">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="e161c-349">NU1608</span><span class="sxs-lookup"><span data-stu-id="e161c-349">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-350">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-350">**Issue**</span></span> | <span data-ttu-id="e161c-351">解決済みのパッケージは、依存関係の制約によりより高い。</span><span class="sxs-lookup"><span data-stu-id="e161c-351">A resolved package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="e161c-352">これは、プロジェクトを直接参照されているパッケージに他のパッケージからの依存関係の制約がよりも優先されることを意味します。</span><span class="sxs-lookup"><span data-stu-id="e161c-352">This means that a package referenced directly by a project overrides dependency constraints from other packages.</span></span>|
| <span data-ttu-id="e161c-353">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-353">**Example message**</span></span> | <span data-ttu-id="e161c-354">*依存関係の制約の外部で検出されたパッケージのバージョン: x 1.0.0 y (1.0.0 =) が必要ですが、バージョン y 2.0.0 が解決されました。*</span><span class="sxs-lookup"><span data-stu-id="e161c-354">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |
| <span data-ttu-id="e161c-355">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-355">**Solution**</span></span> | <span data-ttu-id="e161c-356">これが意図的ないくつかの場合と、警告を抑制することができます。</span><span class="sxs-lookup"><span data-stu-id="e161c-356">In some cases this is intentional and the warning can be suppressed.</span></span> <span data-ttu-id="e161c-357">それ以外の場合、そのバージョンの制約を拡大するために、パッケージへのプロジェクトの参照を変更します。</span><span class="sxs-lookup"><span data-stu-id="e161c-357">Otherwise, change the project's reference to the package to widen its version constraints.</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="e161c-358">パッケージのフォールバック警告</span><span class="sxs-lookup"><span data-stu-id="e161c-358">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="e161c-359">NU1701</span><span class="sxs-lookup"><span data-stu-id="e161c-359">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-360">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-360">**Issue**</span></span> | <span data-ttu-id="e161c-361">`PackageTargetFallback` / `AssetTargetFallback` パッケージからのアセットの選択に使用されました。</span><span class="sxs-lookup"><span data-stu-id="e161c-361">`PackageTargetFallback` / `AssetTargetFallback` was used to select assets from a package.</span></span> <span data-ttu-id="e161c-362">この警告は、ユーザーに、資産が 100% の互換性がある可能性がありますされないことを通知を使用できます。</span><span class="sxs-lookup"><span data-stu-id="e161c-362">The warning let users know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="e161c-363">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-363">**Example message**</span></span> | <span data-ttu-id="e161c-364">*使用して 'portable net45 + win8' 代わりにプロジェクトのターゲット フレームワーク 'netstandard1.5' パッケージ 'NuGet.Versioning' が復元されました。このパッケージは、プロジェクトを完全に互換性がない可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="e161c-364">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |
| <span data-ttu-id="e161c-365">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-365">**Solution**</span></span> | <span data-ttu-id="e161c-366">パッケージをサポートするには、プロジェクトのターゲット フレームワークを変更します。</span><span class="sxs-lookup"><span data-stu-id="e161c-366">Change the project's target framework to one that the package supports.</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="e161c-367">フィードの警告</span><span class="sxs-lookup"><span data-stu-id="e161c-367">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="e161c-368">NU1801</span><span class="sxs-lookup"><span data-stu-id="e161c-368">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-369">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-369">**Issue**</span></span> | <span data-ttu-id="e161c-370">フィードを読み取る際にエラーが発生したときに`IgnoreFailedSources`が設定されて true の場合、致命的でない警告に変換することをします。</span><span class="sxs-lookup"><span data-stu-id="e161c-370">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="e161c-371">これにより、すべてのメッセージが含まれがジェネリックです。</span><span class="sxs-lookup"><span data-stu-id="e161c-371">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="e161c-372">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-372">**Example message**</span></span> | <span data-ttu-id="e161c-373">N/A</span><span class="sxs-lookup"><span data-stu-id="e161c-373">n/a</span></span> |
| <span data-ttu-id="e161c-374">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-374">**Solution**</span></span> | <span data-ttu-id="e161c-375">有効なソースを指定する構成を編集します。</span><span class="sxs-lookup"><span data-stu-id="e161c-375">Edit your configuration to specify valid sources.</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="e161c-376">NuGet の内部エラーと警告</span><span class="sxs-lookup"><span data-stu-id="e161c-376">NuGet internal errors and warnings</span></span>

<span data-ttu-id="e161c-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="e161c-377">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="e161c-378">NU1000</span><span class="sxs-lookup"><span data-stu-id="e161c-378">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-379">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-379">**Issue**</span></span> | <span data-ttu-id="e161c-380">NuGet から以外の特定の内部エラー。</span><span class="sxs-lookup"><span data-stu-id="e161c-380">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="e161c-381">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-381">**Solution**</span></span> | <span data-ttu-id="e161c-382">詳細については、ログを確認します。</span><span class="sxs-lookup"><span data-stu-id="e161c-382">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="e161c-383">NU1500</span><span class="sxs-lookup"><span data-stu-id="e161c-383">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-384">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-384">**Issue**</span></span> | <span data-ttu-id="e161c-385">NuGet による非特定内部警告します。</span><span class="sxs-lookup"><span data-stu-id="e161c-385">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="e161c-386">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-386">**Solution**</span></span> | <span data-ttu-id="e161c-387">詳細については、ログを確認します。</span><span class="sxs-lookup"><span data-stu-id="e161c-387">Check the logs for more information</span></span> |

## <a name="signed-packages-creation-and-verification"></a><span data-ttu-id="e161c-388">署名付きパッケージ (作成および検証)</span><span class="sxs-lookup"><span data-stu-id="e161c-388">Signed packages (creation and verification)</span></span>

<span data-ttu-id="e161c-389">*NuGet 4.6.0+*</span><span class="sxs-lookup"><span data-stu-id="e161c-389">*NuGet 4.6.0+*</span></span>

<span data-ttu-id="e161c-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span><span class="sxs-lookup"><span data-stu-id="e161c-390">[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)</span></span>

### <a name="nu3000"></a><span data-ttu-id="e161c-391">NU3000</span><span class="sxs-lookup"><span data-stu-id="e161c-391">NU3000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-392">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-392">**Issue**</span></span> | <span data-ttu-id="e161c-393">特定できないエラーは、パッケージの署名に関連して、パッケージの検証を署名します。</span><span class="sxs-lookup"><span data-stu-id="e161c-393">A non-specific error related to package signing and signed package verification.</span></span> |
| <span data-ttu-id="e161c-394">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-394">**Solution**</span></span> | <span data-ttu-id="e161c-395">詳細については、ログを確認してください。</span><span class="sxs-lookup"><span data-stu-id="e161c-395">Check the logs for more information.</span></span> |

### <a name="nu3001"></a><span data-ttu-id="e161c-396">NU3001</span><span class="sxs-lookup"><span data-stu-id="e161c-396">NU3001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-397">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-397">**Issue**</span></span> | <span data-ttu-id="e161c-398">いずれかに無効な引数、[コマンドをサインイン](../tools/cli-ref-sign.md)または[コマンドを確認してください](../tools/cli-ref-verify.md)です。</span><span class="sxs-lookup"><span data-stu-id="e161c-398">Invalid arguments to either the [sign command](../tools/cli-ref-sign.md) or the [verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="e161c-399">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-399">**Solution**</span></span> | <span data-ttu-id="e161c-400">確認し、指定された引数を修正します。</span><span class="sxs-lookup"><span data-stu-id="e161c-400">Check and correct the arguments provided.</span></span> |

### <a name="nu3002"></a><span data-ttu-id="e161c-401">NU3002</span><span class="sxs-lookup"><span data-stu-id="e161c-401">NU3002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-402">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-402">**Issue**</span></span> | <span data-ttu-id="e161c-403">`-Timestamper`とオプションが指定されなかった、 [nuget 記号コマンド](../tools/cli-ref-sign.md)です。</span><span class="sxs-lookup"><span data-stu-id="e161c-403">The `-Timestamper` option was not specified with the [nuget sign command](../tools/cli-ref-sign.md).</span></span> |
| <span data-ttu-id="e161c-404">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-404">**Example message**</span></span> | <span data-ttu-id="e161c-405">*'-Timestamper' オプションが指定されていません。署名されたパッケージには、タイムスタンプはできません。*</span><span class="sxs-lookup"><span data-stu-id="e161c-405">*The '-Timestamper' option was not provided. The signed package will not be timestamped.*</span></span> |
| <span data-ttu-id="e161c-406">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-406">**Solution**</span></span> | <span data-ttu-id="e161c-407">指定して、`-Timestamper`オプションは`nuget sign`します。</span><span class="sxs-lookup"><span data-stu-id="e161c-407">Specify the `-Timestamper` option with `nuget sign`.</span></span> |

### <a name="nu3004"></a><span data-ttu-id="e161c-408">NU3004</span><span class="sxs-lookup"><span data-stu-id="e161c-408">NU3004</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-409">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-409">**Issue**</span></span> | <span data-ttu-id="e161c-410">署名されていないパッケージに指定された、 [nuget コマンドを確認してください](../tools/cli-ref-verify.md)です。</span><span class="sxs-lookup"><span data-stu-id="e161c-410">An unsigned package was provided to the [nuget verify command](../tools/cli-ref-verify.md).</span></span> |
| <span data-ttu-id="e161c-411">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-411">**Solution**</span></span> | <span data-ttu-id="e161c-412">実行`nuget verify`署名付きパッケージとします。</span><span class="sxs-lookup"><span data-stu-id="e161c-412">Run `nuget verify` with a signed package.</span></span> <span data-ttu-id="e161c-413">参照してください[パッケージに署名](../create-packages/Sign-a-Package.md)です。</span><span class="sxs-lookup"><span data-stu-id="e161c-413">See [Sign a package](../create-packages/Sign-a-Package.md).</span></span> |

### <a name="nu3008"></a><span data-ttu-id="e161c-414">NU3008</span><span class="sxs-lookup"><span data-stu-id="e161c-414">NU3008</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-415">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-415">**Issue**</span></span> | <span data-ttu-id="e161c-416">パッケージの整合性チェックに失敗しました、署名されているため、署名付きパッケージ改ざんされたことを意味します。</span><span class="sxs-lookup"><span data-stu-id="e161c-416">The package integrity check failed, meaning that a signed package was tampered with since being signed.</span></span> |
| <span data-ttu-id="e161c-417">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-417">**Solution**</span></span> | <span data-ttu-id="e161c-418">ウイルス対策ソフトウェアを使用してコンピューターをスキャンします。</span><span class="sxs-lookup"><span data-stu-id="e161c-418">Scan your computer with anti-virus software.</span></span> <span data-ttu-id="e161c-419">コンピューターからパッケージを削除して、再インストールし、および、操作を再試行します。</span><span class="sxs-lookup"><span data-stu-id="e161c-419">Then remove the package from the computer, reinstall it, and try the operation again.</span></span> <span data-ttu-id="e161c-420">問題が解決しない場合は、パッケージ ソースの所有者とパッケージの所有者に問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="e161c-420">If the problem persists, contact the owner of the package source and the package owner.</span></span> |

### <a name="nu3018"></a><span data-ttu-id="e161c-421">NU3018</span><span class="sxs-lookup"><span data-stu-id="e161c-421">NU3018</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-422">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-422">**Issue**</span></span> | <span data-ttu-id="e161c-423">プライマリ署名の証明書チェーンの構築が失敗しました。</span><span class="sxs-lookup"><span data-stu-id="e161c-423">Certificate chain building failed for the primary signature.</span></span> <span data-ttu-id="e161c-424">プライマリ署名証明書は失効済みで、信頼されていないか、証明書の失効情報は使用できません。</span><span class="sxs-lookup"><span data-stu-id="e161c-424">The primary signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="e161c-425">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-425">**Example message**</span></span> | <span data-ttu-id="e161c-426">*警告: NU3018: 失効関数は、証明書の失効を確認できませんでした。*</span><span class="sxs-lookup"><span data-stu-id="e161c-426">*WARNING: NU3018: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="e161c-427">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-427">**Solution**</span></span> | <span data-ttu-id="e161c-428">信頼できる、有効な証明書を使用します。</span><span class="sxs-lookup"><span data-stu-id="e161c-428">Use a trusted and valid certificate.</span></span> <span data-ttu-id="e161c-429">インターネット接続を確認します。</span><span class="sxs-lookup"><span data-stu-id="e161c-429">Check internet connectivity.</span></span> |

### <a name="nu3028"></a><span data-ttu-id="e161c-430">NU3028</span><span class="sxs-lookup"><span data-stu-id="e161c-430">NU3028</span></span>

| | |
| --- | --- |
| <span data-ttu-id="e161c-431">**問題点**</span><span class="sxs-lookup"><span data-stu-id="e161c-431">**Issue**</span></span> | <span data-ttu-id="e161c-432">タイムスタンプの署名の証明書チェーンの構築が失敗しました。</span><span class="sxs-lookup"><span data-stu-id="e161c-432">Certificate chain building failed for the timestamp signature.</span></span> <span data-ttu-id="e161c-433">タイムスタンプの署名証明書は失効済みで、信頼されていないか、証明書の失効情報は使用できません。</span><span class="sxs-lookup"><span data-stu-id="e161c-433">The timestamp signing certificate is untrusted, revoked, or revocation information for the certificate is unavailable.</span></span> |
| <span data-ttu-id="e161c-434">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="e161c-434">**Example message**</span></span> | <span data-ttu-id="e161c-435">*警告: NU3028: 失効関数は、証明書の失効を確認できませんでした。*</span><span class="sxs-lookup"><span data-stu-id="e161c-435">*WARNING: NU3028: The revocation function was unable to check revocation for the certificate.*</span></span> |
| <span data-ttu-id="e161c-436">**解決方法**</span><span class="sxs-lookup"><span data-stu-id="e161c-436">**Solution**</span></span> | <span data-ttu-id="e161c-437">信頼できる、有効な証明書を使用します。</span><span class="sxs-lookup"><span data-stu-id="e161c-437">Use a trusted and valid certificate.</span></span> <span data-ttu-id="e161c-438">インターネット接続を確認します。</span><span class="sxs-lookup"><span data-stu-id="e161c-438">Check internet connectivity.</span></span> |
