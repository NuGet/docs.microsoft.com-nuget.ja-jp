---
title: "NuGet の復元エラーと警告のリファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "警告とパッケージの復元時に NuGet から発行されたエラーの完全なリファレンス"
keywords: "NuGet のエラー、NuGet の警告、診断"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29eb72cbb6c095cd3aeb524fd8b28416ec5dc798
ms.sourcegitcommit: 6ccb963e065680ab2e7df1d8dd5492897fd56b04
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="c997c-104">エラーと警告</span><span class="sxs-lookup"><span data-stu-id="c997c-104">Errors and warnings</span></span>

<span data-ttu-id="c997c-105">4.3.0、NuGet では、このトピックで説明の番号付けはエラーと警告し、関連する問題に対処するための詳細情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="c997c-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="c997c-106">エラーと警告の次のとおり、のみで使用[PackageReference ベース](../Consume-Packages/Package-References-in-Project-Files.md)プロジェクトおよび NuGet 4.3.0 です。</span><span class="sxs-lookup"><span data-stu-id="c997c-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="c997c-107">NuGet では警告を抑制するか、それらのエラーへの昇格に MSBuild プロパティも使用します。</span><span class="sxs-lookup"><span data-stu-id="c997c-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="c997c-108">詳細については、次を参照してください。[する方法: コンパイラの警告を抑制する状況](/visualstudio/ide/how-to-suppress-compiler-warnings)、Visual Studio のマニュアルでします。</span><span class="sxs-lookup"><span data-stu-id="c997c-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="c997c-109">**エラー**</span><span class="sxs-lookup"><span data-stu-id="c997c-109">**Errors**</span></span>

| <span data-ttu-id="c997c-110">グループ化</span><span class="sxs-lookup"><span data-stu-id="c997c-110">Group</span></span> | <span data-ttu-id="c997c-111">エラー番号</span><span class="sxs-lookup"><span data-stu-id="c997c-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="c997c-112">無効な入力エラー</span><span class="sxs-lookup"><span data-stu-id="c997c-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="c997c-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="c997c-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="c997c-114">パッケージとプロジェクトの不足エラー</span><span class="sxs-lookup"><span data-stu-id="c997c-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="c997c-115">[NU1100](#nu1100)、 [NU1101](#nu1101)、 [NU1102](#nu1102)、 [NU1103](#nu1103)、 [NU1104](#nu1104)、 [NU1105](#nu1105)、 [NU1106](#nu1106)、 [NU1107](#nu1107) (NU1607 以前) [NU1108](#nu1108) (NU1606 以前)</span><span class="sxs-lookup"><span data-stu-id="c997c-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606)</span></span> |
| [<span data-ttu-id="c997c-116">互換性に関するエラー</span><span class="sxs-lookup"><span data-stu-id="c997c-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="c997c-117">[NU1201](#nu1201)、 [NU1202](#nu1202)、 [NU1203](#nu1203)、 [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="c997c-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="c997c-118">**警告**</span><span class="sxs-lookup"><span data-stu-id="c997c-118">**Warnings**</span></span>

| <span data-ttu-id="c997c-119">グループ化</span><span class="sxs-lookup"><span data-stu-id="c997c-119">Group</span></span> | <span data-ttu-id="c997c-120">警告番号</span><span class="sxs-lookup"><span data-stu-id="c997c-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="c997c-121">無効な入力の警告</span><span class="sxs-lookup"><span data-stu-id="c997c-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="c997c-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="c997c-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="c997c-123">予期しないパッケージのバージョンの警告</span><span class="sxs-lookup"><span data-stu-id="c997c-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="c997c-124">[NU1601](#nu1601)、 [NU1602](#nu1602)、 [NU1603](#nu1603)、 [NU1604](#nu1604)、 [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="c997c-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="c997c-125">競合回避モジュールの競合の警告</span><span class="sxs-lookup"><span data-stu-id="c997c-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="c997c-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="c997c-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="c997c-127">パッケージのフォールバック警告</span><span class="sxs-lookup"><span data-stu-id="c997c-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="c997c-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="c997c-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="c997c-129">フィードの警告</span><span class="sxs-lookup"><span data-stu-id="c997c-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="c997c-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="c997c-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="c997c-131">NuGet の内部エラーと警告</span><span class="sxs-lookup"><span data-stu-id="c997c-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="c997c-132">[NU1000](#nu1000), [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="c997c-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="c997c-133">無効な入力エラー</span><span class="sxs-lookup"><span data-stu-id="c997c-133">Invalid input errors</span></span>

<span data-ttu-id="c997c-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="c997c-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="c997c-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="c997c-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-136">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-136">**Issue**</span></span> | <span data-ttu-id="c997c-137">プロジェクトには、1 つまたは複数のフレームワークが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c997c-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="c997c-138">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-138">**Common causes**</span></span> | <span data-ttu-id="c997c-139">プロジェクトが含まれていない、`TargetFramework`または`TargetFrameworks`プロパティです。</span><span class="sxs-lookup"><span data-stu-id="c997c-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="c997c-140">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-140">**Example message**</span></span> | <span data-ttu-id="c997c-141">*プロジェクト projA では、どのターゲット フレームワーク c:\tmp\projA.csproj で指定されていません*</span><span class="sxs-lookup"><span data-stu-id="c997c-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="c997c-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="c997c-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-143">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-143">**Issue**</span></span> | <span data-ttu-id="c997c-144">入力とクリア キーワードの組み合わせが無効です。</span><span class="sxs-lookup"><span data-stu-id="c997c-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="c997c-145">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-145">**Common causes**</span></span> | <span data-ttu-id="c997c-146">クリアを他の入力で組み合わせることはできません。</span><span class="sxs-lookup"><span data-stu-id="c997c-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="c997c-147">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-147">**Example message**</span></span> | <span data-ttu-id="c997c-148">*'CLEAR' では使用できませんの他の値と共に*</span><span class="sxs-lookup"><span data-stu-id="c997c-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="c997c-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="c997c-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-150">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-150">**Issue**</span></span> | <span data-ttu-id="c997c-151">`PackageTargetFallback`および`AssetTargetFallback`資産を選択するための動作の違いを提供し、一緒に使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="c997c-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="c997c-152">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-152">**Common causes**</span></span> | <span data-ttu-id="c997c-153">両方`PackageTargetFallback`と`AssetTargetFallback`プロジェクト内に存在します。</span><span class="sxs-lookup"><span data-stu-id="c997c-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="c997c-154">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-154">**Example message**</span></span> | <span data-ttu-id="c997c-155">*PackageTargetFallback と AssetTargetFallback に使用することはできません。プロジェクトの環境から PackageTargetFallback(deprecated) 参照を削除します。*</span><span class="sxs-lookup"><span data-stu-id="c997c-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="c997c-156">パッケージとプロジェクトの不足エラー</span><span class="sxs-lookup"><span data-stu-id="c997c-156">Missing package and project errors</span></span>

<span data-ttu-id="c997c-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="c997c-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="c997c-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="c997c-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-159">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-159">**Issue**</span></span> | <span data-ttu-id="c997c-160">依存関係グループを解決できません。</span><span class="sxs-lookup"><span data-stu-id="c997c-160">A dependency group not be resolved.</span></span> <span data-ttu-id="c997c-161">これは、パッケージまたはプロジェクトではない型での一般的な問題です。</span><span class="sxs-lookup"><span data-stu-id="c997c-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="c997c-162">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-162">**Common causes**</span></span> | <span data-ttu-id="c997c-163">プロジェクトには、存在しないアイテムへの依存関係が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c997c-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="c997c-164">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-164">**Example message**</span></span> | <span data-ttu-id="c997c-165">*Net45 を System.Missing を解決できません。*</span><span class="sxs-lookup"><span data-stu-id="c997c-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="c997c-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="c997c-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-167">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-167">**Issue**</span></span> | <span data-ttu-id="c997c-168">パッケージのソースに見つかりません。</span><span class="sxs-lookup"><span data-stu-id="c997c-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="c997c-169">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-169">**Common causes**</span></span> | <span data-ttu-id="c997c-170">適切なパッケージ ソースが見つからないか、パッケージの識別子が正しくありません。</span><span class="sxs-lookup"><span data-stu-id="c997c-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="c997c-171">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-171">**Example message**</span></span> | <span data-ttu-id="c997c-172">*パッケージ System.Missing が見つかりません。ソースでは、この id を持つパッケージが存在しません: dotnet コア、dotnet roslyn、nuget.org*</span><span class="sxs-lookup"><span data-stu-id="c997c-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="c997c-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="c997c-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-174">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-174">**Issue**</span></span> | <span data-ttu-id="c997c-175">パッケージ識別子が見つかりましたが、ソースのいずれかで指定した依存関係の範囲内のバージョンが見つかりません。</span><span class="sxs-lookup"><span data-stu-id="c997c-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="c997c-176">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-176">**Common causes**</span></span> | <span data-ttu-id="c997c-177">適切なパッケージ ソースが見つからないか、依存関係の範囲が正しくありません。</span><span class="sxs-lookup"><span data-stu-id="c997c-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="c997c-178">パッケージとユーザーではなく、範囲を指定する場合があります。</span><span class="sxs-lookup"><span data-stu-id="c997c-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="c997c-179">ユーザーは、このパッケージがプロジェクトで直接参照されている場合に使用可能なバージョンに切り替える必要があります。</span><span class="sxs-lookup"><span data-stu-id="c997c-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="c997c-180">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-180">**Example message**</span></span> | <span data-ttu-id="c997c-181">*NuGet.Versioning バージョンでパッケージを見つけることができません (> = 9.0.1)<br/> -nuget.org で見つかった 30 版 [バージョンに最も近い: 4.0.0]<br/> -dotnet buildtools で見つかった 10 バージョン [バージョンに最も近い: 4.0.0-rc-2129]<br/> -9 の検出NuGetVolatile のバージョン [バージョンに最も近い: 3.0.0-beta-00032]<br/> -0 のバージョンを記載 dotnet コア<br/>-dotnet roslyn で 0 バージョンを検出*</span><span class="sxs-lookup"><span data-stu-id="c997c-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="c997c-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="c997c-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-183">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-183">**Issue**</span></span> | <span data-ttu-id="c997c-184">依存関係の範囲内で安定したバージョンが見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="c997c-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="c997c-185">プレリリース版は見つかりましたが、許可されていません。</span><span class="sxs-lookup"><span data-stu-id="c997c-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="c997c-186">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-186">**Common causes**</span></span> | <span data-ttu-id="c997c-187">プロジェクトでは、依存関係の範囲の安定したバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="c997c-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="c997c-188">ユーザーは、プレリリース版を含むバージョンの範囲を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c997c-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="c997c-189">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-189">**Example message**</span></span> | <span data-ttu-id="c997c-190">*バージョンと安定したパッケージ NuGet.Versioning を見つけることができません (> = 3.0.0)<br/> -dotnet buildtools で見つかった 10 バージョン [バージョンに最も近い: 4.0.0-rc-2129]<br/> -NuGetVolatile で見つかった 9 版 [バージョンに最も近い: 3.0.0-beta-00032]<br/> -0 のバージョンを記載 dotnet コア<br/>-dotnet roslyn で 0 バージョンが見つかりません*</span><span class="sxs-lookup"><span data-stu-id="c997c-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="c997c-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="c997c-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-192">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-192">**Issue**</span></span> | <span data-ttu-id="c997c-193">ProjectReference は、存在しないファイルを指します。</span><span class="sxs-lookup"><span data-stu-id="c997c-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="c997c-194">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-194">**Common causes**</span></span> | <span data-ttu-id="c997c-195">プロジェクト ファイルがディスクから不足しているか、参照が正しくありません。</span><span class="sxs-lookup"><span data-stu-id="c997c-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="c997c-196">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-196">**Example message**</span></span> | <span data-ttu-id="c997c-197">*プロジェクト参照では、'c:\a.csproj' は存在しません。プロジェクトへの参照が有効であると、プロジェクト ファイルが存在することを確認してください。*</span><span class="sxs-lookup"><span data-stu-id="c997c-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="c997c-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="c997c-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-199">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-199">**Issue**</span></span> | <span data-ttu-id="c997c-200">プロジェクト ファイルが存在しますが、その復元に関する情報が指定されていません。</span><span class="sxs-lookup"><span data-stu-id="c997c-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="c997c-201">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-201">**Common causes**</span></span> | <span data-ttu-id="c997c-202">Visual Studio でプロジェクトが読み込まれているこの可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c997c-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="c997c-203">コマンド ラインからは、ファイルが破損しているか、ことが含まれていないカスタム プロジェクトを読み込むへの復元に必要な imports ターゲットの後にこの可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c997c-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="c997c-204">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-204">**Example message**</span></span> | <span data-ttu-id="c997c-205">*'C:\a.csproj' のプロジェクト情報を読み取れません。プロジェクト ファイルには、復元に必要なターゲットを無効または不足している可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="c997c-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="c997c-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="c997c-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-207">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-207">**Issue**</span></span> | <span data-ttu-id="c997c-208">依存関係の制約を解決することはできません。</span><span class="sxs-lookup"><span data-stu-id="c997c-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="c997c-209">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-209">**Common causes**</span></span> | <span data-ttu-id="c997c-210">パッケージには、正確なバージョンの大まかな範囲ではなくパッケージへの依存関係が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c997c-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="c997c-211">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-211">**Example message**</span></span> | <span data-ttu-id="c997c-212">*{Id} の矛盾する要求を満たすことができません: {競合パス} フレームワーク: {ターゲット グラフ}*</span><span class="sxs-lookup"><span data-stu-id="c997c-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="c997c-213">NU1107 (NU1607 以前)</span><span class="sxs-lookup"><span data-stu-id="c997c-213">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-214">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-214">**Issue**</span></span> | <span data-ttu-id="c997c-215">パッケージ間で依存関係の制約を解決できません。</span><span class="sxs-lookup"><span data-stu-id="c997c-215">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="c997c-216">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-216">**Common causes**</span></span> | <span data-ttu-id="c997c-217">正確なバージョンに依存関係の制約を含むパッケージでは、他のパッケージを必要な場合は、バージョンを増やすには許可されません。</span><span class="sxs-lookup"><span data-stu-id="c997c-217">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="c997c-218">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-218">**Example message**</span></span> | <span data-ttu-id="c997c-219">*バージョンの競合の NuGet.Versioning が検出されました。この問題を解決するのには、プロジェクトから直接パッケージを参照します。<br/>NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span><span class="sxs-lookup"><span data-stu-id="c997c-219">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="c997c-220">NU1108 (NU1606 以前)</span><span class="sxs-lookup"><span data-stu-id="c997c-220">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-221">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-221">**Issue**</span></span> | <span data-ttu-id="c997c-222">循環する依存関係が検出されました。</span><span class="sxs-lookup"><span data-stu-id="c997c-222">A circular dependency was detected.</span></span> |
| <span data-ttu-id="c997c-223">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-223">**Common causes**</span></span> | <span data-ttu-id="c997c-224">パッケージが正しく作成されていません。</span><span class="sxs-lookup"><span data-stu-id="c997c-224">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="c997c-225">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-225">**Example message**</span></span> | <span data-ttu-id="c997c-226">*サイクルが検出されました: A が B]-> [A]-> [*</span><span class="sxs-lookup"><span data-stu-id="c997c-226">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="c997c-227">互換性に関するエラー</span><span class="sxs-lookup"><span data-stu-id="c997c-227">Compatibility errors</span></span>

<span data-ttu-id="c997c-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="c997c-228">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="c997c-229">NU1201</span><span class="sxs-lookup"><span data-stu-id="c997c-229">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-230">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-230">**Issue**</span></span> | <span data-ttu-id="c997c-231">依存関係プロジェクトには、現在のプロジェクトと互換性のあるフレームワークが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c997c-231">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="c997c-232">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-232">**Common causes**</span></span> | <span data-ttu-id="c997c-233">プロジェクトのターゲット フレームワークは、プロジェクトが使用より高いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="c997c-233">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="c997c-234">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-234">**Example message**</span></span> | <span data-ttu-id="c997c-235">*プロジェクト ServerWeb は netstandard1.3 と互換性がありません (です。NETStandard, Version = v1.3)。プロジェクトの ServerWeb サポート:<br/> -netstandard1.6 (です。NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (です。NETCoreApp, Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="c997c-235">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="c997c-236">NU1202</span><span class="sxs-lookup"><span data-stu-id="c997c-236">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-237">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-237">**Issue**</span></span> | <span data-ttu-id="c997c-238">依存関係パッケージには、プロジェクトと互換性のある任意のアセットが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c997c-238">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="c997c-239">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-239">**Common causes**</span></span> | <span data-ttu-id="c997c-240">パッケージには、プロジェクトのターゲット フレームワークをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="c997c-240">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="c997c-241">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-241">**Example message**</span></span> | <span data-ttu-id="c997c-242">*パッケージ System.ComponentModel.EventBasedAsync 4.0.11 は netstandard1.3 と互換性がありません (です。NETStandard, Version = v1.3)。System.ComponentModel.EventBasedAsync 4.0.11 サポートをパッケージ化:<br/> -monoandroid10 (MonoAndroid、バージョン = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (です。NETFramework, Version = v4.5)<br/> -netcore50 (です。NETCore, Version = v5.0)<br/> -netstandard1.0 (です。NETStandard, Version = v1.0)<br/> -portable net45 + win8 + wp8 + wpa81 (です。NETPortable、バージョン v0.0、プロファイルを = = Profile259)<br/> -win8 (Windows、バージョン = バージョン 8.0)<br/> -wp8 (WindowsPhone, Version = バージョン 8.0)<br/> -wpa81 (WindowsPhoneApp、バージョン = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="c997c-242">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="c997c-243">NU1203</span><span class="sxs-lookup"><span data-stu-id="c997c-243">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-244">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-244">**Issue**</span></span> | <span data-ttu-id="c997c-245">パッケージがプロジェクトをサポートしない`RuntimeIdentifier`です。</span><span class="sxs-lookup"><span data-stu-id="c997c-245">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="c997c-246">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-246">**Common causes**</span></span> | <span data-ttu-id="c997c-247">現在をサポートしていないパッケージ`RuntimeIdentifier`です。</span><span class="sxs-lookup"><span data-stu-id="c997c-247">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="c997c-248">変更、`RuntimeIdentifier`必要な場合は、プロジェクトで使用される値。</span><span class="sxs-lookup"><span data-stu-id="c997c-248">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="c997c-249">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-249">**Example message**</span></span> | <span data-ttu-id="c997c-250">*System.Example 1.0.0 a.dll のコンパイル時参照アセンブリ net461、上には互換性のあるランタイム アセンブリが存在しません。*</span><span class="sxs-lookup"><span data-stu-id="c997c-250">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="c997c-251">NU1401</span><span class="sxs-lookup"><span data-stu-id="c997c-251">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-252">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-252">**Issue**</span></span> | <span data-ttu-id="c997c-253">パッケージには、機能、または NuGet のインストールされているバージョンでサポートされていないフレームワークが必要です。</span><span class="sxs-lookup"><span data-stu-id="c997c-253">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="c997c-254">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-254">**Common causes**</span></span> | <span data-ttu-id="c997c-255">問題を解決する NuGet をアップグレードします。</span><span class="sxs-lookup"><span data-stu-id="c997c-255">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="c997c-256">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-256">**Example message**</span></span> | <span data-ttu-id="c997c-257">*'NuGet.Versioning' パッケージは NuGet クライアント バージョン '5.0.0' を必要以上に設定するが現在の NuGet バージョンは '4.3.0' です。NuGet をアップグレードするには、http://docs.nuget.org/consume/installing-nuget を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="c997c-257">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="c997c-258">無効な入力の警告</span><span class="sxs-lookup"><span data-stu-id="c997c-258">Invalid input warnings</span></span>

<span data-ttu-id="c997c-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="c997c-259">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="c997c-260">NU1501</span><span class="sxs-lookup"><span data-stu-id="c997c-260">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-261">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-261">**Issue**</span></span> | <span data-ttu-id="c997c-262">操作しようとして、プロジェクトの復元に見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="c997c-262">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="c997c-263">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-263">**Common causes**</span></span> | <span data-ttu-id="c997c-264">プロジェクトがありません。</span><span class="sxs-lookup"><span data-stu-id="c997c-264">The project is missing.</span></span> |
| <span data-ttu-id="c997c-265">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-265">**Example message**</span></span> | <span data-ttu-id="c997c-266">*フォルダー 'c:\projects\a' に復元するプロジェクトが含まれていません。*</span><span class="sxs-lookup"><span data-stu-id="c997c-266">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="c997c-267">NU1502</span><span class="sxs-lookup"><span data-stu-id="c997c-267">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-268">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-268">**Issue**</span></span> | <span data-ttu-id="c997c-269">`RuntimeSupports`無効なプロファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c997c-269">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="c997c-270">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-270">**Common causes**</span></span> | <span data-ttu-id="c997c-271">サポートしているプロファイルが見つかりません、`runtime.json`現在の依存関係パッケージからファイル。</span><span class="sxs-lookup"><span data-stu-id="c997c-271">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="c997c-272">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-272">**Example message**</span></span> | <span data-ttu-id="c997c-273">*不明な互換性プロファイル: aaa*</span><span class="sxs-lookup"><span data-stu-id="c997c-273">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="c997c-274">NU1503</span><span class="sxs-lookup"><span data-stu-id="c997c-274">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-275">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-275">**Issue**</span></span> | <span data-ttu-id="c997c-276">依存関係プロジェクトでは、NuGet の復元のターゲットをインポートしません。</span><span class="sxs-lookup"><span data-stu-id="c997c-276">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="c997c-277">NU1105 に似ていますが、ここで、プロジェクトがスキップされた、すべての復元が失敗の原因ではなく無視します。</span><span class="sxs-lookup"><span data-stu-id="c997c-277">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="c997c-278">複雑なソリューションでもある復元をサポートしない可能性があるプロジェクトの他の種類。</span><span class="sxs-lookup"><span data-stu-id="c997c-278">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="c997c-279">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-279">**Common causes**</span></span> | <span data-ttu-id="c997c-280">プロジェクトの復元は自動的にインポートする共通のプロパティ/ターゲットはインポートしない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c997c-280">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="c997c-281">プロジェクトを復元する必要がある場合は無視できます。</span><span class="sxs-lookup"><span data-stu-id="c997c-281">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="c997c-282">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-282">**Example message**</span></span> | <span data-ttu-id="c997c-283">*プロジェクト 'c:\a.csproj' の復元をスキップしています。プロジェクト ファイルには、復元に必要なターゲットを無効または不足している可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="c997c-283">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="c997c-284">予期しないパッケージのバージョンの警告</span><span class="sxs-lookup"><span data-stu-id="c997c-284">Unexpected package version warnings</span></span>

<span data-ttu-id="c997c-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="c997c-285">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="c997c-286">NU1601</span><span class="sxs-lookup"><span data-stu-id="c997c-286">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-287">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-287">**Issue**</span></span> | <span data-ttu-id="c997c-288">直接プロジェクトの依存関係が、指定したプロジェクトより新しいバージョンに高くなります。</span><span class="sxs-lookup"><span data-stu-id="c997c-288">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="c997c-289">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-289">**Common causes**</span></span> | <span data-ttu-id="c997c-290">別の依存関係パッケージより新しいバージョンを必要し、パッケージを高きます。</span><span class="sxs-lookup"><span data-stu-id="c997c-290">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="c997c-291">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-291">**Example message**</span></span> | <span data-ttu-id="c997c-292">*指定された依存関係が NuGet.Versioning (> = 3.5.0) NuGet.Versioning 4.0.0 で終了しましたが、します。*</span><span class="sxs-lookup"><span data-stu-id="c997c-292">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="c997c-293">NU1602</span><span class="sxs-lookup"><span data-stu-id="c997c-293">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-294">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-294">**Issue**</span></span> | <span data-ttu-id="c997c-295">パッケージの依存関係には、下限値がありません。</span><span class="sxs-lookup"><span data-stu-id="c997c-295">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="c997c-296">これは、検索への復元を許可しない、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="c997c-296">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="c997c-297">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="c997c-297">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c997c-298">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="c997c-298">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c997c-299">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-299">**Common causes**</span></span> | <span data-ttu-id="c997c-300">これは通常、パッケージ作成エラーです。</span><span class="sxs-lookup"><span data-stu-id="c997c-300">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="c997c-301">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-301">**Example message**</span></span> | <span data-ttu-id="c997c-302">*NuGet.Packaging 4.0.0 では、依存 NuGet.Versioning (> 3.5.0) のため、下限は提供されません。3.6.0 のおおよその最適な一致が解決されました。*</span><span class="sxs-lookup"><span data-stu-id="c997c-302">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="c997c-303">NU1603</span><span class="sxs-lookup"><span data-stu-id="c997c-303">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-304">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-304">**Issue**</span></span> | <span data-ttu-id="c997c-305">パッケージの依存関係は、バージョンが見つかりませんでしたを指定します。</span><span class="sxs-lookup"><span data-stu-id="c997c-305">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="c997c-306">以降のバージョンは、に対して、パッケージが作成されたものと異なるを代わりに、使用されました。</span><span class="sxs-lookup"><span data-stu-id="c997c-306">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="c997c-307">つまり、復元が見つかりませんでした、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="c997c-307">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="c997c-308">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="c997c-308">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c997c-309">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="c997c-309">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c997c-310">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-310">**Common causes**</span></span> | <span data-ttu-id="c997c-311">パッケージ ソースでは、予想される下限バージョンは含まれません。</span><span class="sxs-lookup"><span data-stu-id="c997c-311">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="c997c-312">期待どおりパッケージがリリースされていない場合、パッケージの作成エラーでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="c997c-312">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="c997c-313">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-313">**Example message**</span></span> | <span data-ttu-id="c997c-314">NuGet.Packaging 4.0.0 NuGet.Versioning によって異なります (> = 4.0.0) が、4.0.0 が見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="c997c-314">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="c997c-315">5.0.0 以降のおおよその最適な一致が解決されました。</span><span class="sxs-lookup"><span data-stu-id="c997c-315">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="c997c-316">NU1604</span><span class="sxs-lookup"><span data-stu-id="c997c-316">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-317">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-317">**Issue**</span></span> | <span data-ttu-id="c997c-318">プロジェクトの依存関係、下限が定義されません。</span><span class="sxs-lookup"><span data-stu-id="c997c-318">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="c997c-319">つまり、復元が見つかりませんでした、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="c997c-319">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="c997c-320">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="c997c-320">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c997c-321">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="c997c-321">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c997c-322">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-322">**Common causes**</span></span> | <span data-ttu-id="c997c-323">プロジェクトの*PackageReference* *バージョン*属性は、下限の境界を含むように更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c997c-323">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="c997c-324">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-324">**Example message**</span></span> | <span data-ttu-id="c997c-325">*プロジェクトの依存関係 NuGet.Versioning (< = 9.0.0) doe が包括的の下限値が含まれていません。結果の整合性の復元に依存関係のバージョンに下限の境界を含めます。*</span><span class="sxs-lookup"><span data-stu-id="c997c-325">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="c997c-326">NU1605</span><span class="sxs-lookup"><span data-stu-id="c997c-326">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-327">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-327">**Issue**</span></span> | <span data-ttu-id="c997c-328">依存関係パッケージには、パッケージの復元が最終的により高いバージョンでバージョン制約が指定されています。</span><span class="sxs-lookup"><span data-stu-id="c997c-328">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="c997c-329">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-329">**Common causes**</span></span> | <span data-ttu-id="c997c-330">パッケージを解決するときに最も近いが優先されます。</span><span class="sxs-lookup"><span data-stu-id="c997c-330">Nearest wins when resolving packages.</span></span> <span data-ttu-id="c997c-331">グラフ内の最も近いパッケージには、離れた場所にあるパッケージがオーバーライドされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c997c-331">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="c997c-332">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-332">**Example message**</span></span> | <span data-ttu-id="c997c-333">*パッケージのダウン グレードが検出されました: 3.5.0 に 4.0.0 から NuGet.Versioning です。異なるバージョンを選択するプロジェクトから直接パッケージを参照します。<br/>NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span><span class="sxs-lookup"><span data-stu-id="c997c-333">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="c997c-334">競合回避モジュールの競合の警告</span><span class="sxs-lookup"><span data-stu-id="c997c-334">Resolver conflict warnings</span></span>

### <a name="nu1608"></a><span data-ttu-id="c997c-335">NU1608</span><span class="sxs-lookup"><span data-stu-id="c997c-335">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-336">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-336">**Issue**</span></span> | <span data-ttu-id="c997c-337">解決パッケージは、依存関係の制約によりより高い。</span><span class="sxs-lookup"><span data-stu-id="c997c-337">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="c997c-338">これが意図的ないくつかの場合と、警告を抑制することができます。</span><span class="sxs-lookup"><span data-stu-id="c997c-338">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="c997c-339">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-339">**Common causes**</span></span> | <span data-ttu-id="c997c-340">プロジェクトを直接参照されているパッケージには、他のパッケージからの依存関係の制約がよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="c997c-340">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="c997c-341">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-341">**Example message**</span></span> | <span data-ttu-id="c997c-342">*依存関係の制約の外部で検出されたパッケージのバージョン: x 1.0.0 y (1.0.0 =) が必要ですが、バージョン y 2.0.0 が解決されました。*</span><span class="sxs-lookup"><span data-stu-id="c997c-342">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="c997c-343">パッケージのフォールバック警告</span><span class="sxs-lookup"><span data-stu-id="c997c-343">Package fallback warnings</span></span>

### <a name="nu1701"></a><span data-ttu-id="c997c-344">NU1701</span><span class="sxs-lookup"><span data-stu-id="c997c-344">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-345">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-345">**Issue**</span></span> | <span data-ttu-id="c997c-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span><span class="sxs-lookup"><span data-stu-id="c997c-346">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="c997c-347">これは、ユーザーに、資産が 100% の互換性がある可能性がありますされないことを通知する警告です。</span><span class="sxs-lookup"><span data-stu-id="c997c-347">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="c997c-348">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-348">**Common causes**</span></span> | <span data-ttu-id="c997c-349">パッケージには、プロジェクトのフレームワークをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="c997c-349">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="c997c-350">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-350">**Example message**</span></span> | <span data-ttu-id="c997c-351">*使用して 'portable net45 + win8' 代わりにプロジェクトのターゲット フレームワーク 'netstandard1.5' パッケージ 'NuGet.Versioning' が復元されました。このパッケージは、プロジェクトを完全に互換性がない可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="c997c-351">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="c997c-352">フィードの警告</span><span class="sxs-lookup"><span data-stu-id="c997c-352">Feed warnings</span></span>

### <a name="nu1801"></a><span data-ttu-id="c997c-353">NU1801</span><span class="sxs-lookup"><span data-stu-id="c997c-353">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-354">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-354">**Issue**</span></span> | <span data-ttu-id="c997c-355">フィードを読み取る際にエラーが発生したときに`IgnoreFailedSources`が設定されて true の場合、致命的でない警告に変換することをします。</span><span class="sxs-lookup"><span data-stu-id="c997c-355">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="c997c-356">これにより、すべてのメッセージが含まれがジェネリックです。</span><span class="sxs-lookup"><span data-stu-id="c997c-356">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="c997c-357">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-357">**Common causes**</span></span> | <span data-ttu-id="c997c-358">ソースが正しくありません。</span><span class="sxs-lookup"><span data-stu-id="c997c-358">The source is invalid.</span></span> |
| <span data-ttu-id="c997c-359">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c997c-359">**Example message**</span></span> | <span data-ttu-id="c997c-360">N/A</span><span class="sxs-lookup"><span data-stu-id="c997c-360">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="c997c-361">NuGet の内部エラーと警告</span><span class="sxs-lookup"><span data-stu-id="c997c-361">NuGet internal errors and warnings</span></span>

<span data-ttu-id="c997c-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="c997c-362">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="c997c-363">NU1000</span><span class="sxs-lookup"><span data-stu-id="c997c-363">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-364">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-364">**Issue**</span></span> | <span data-ttu-id="c997c-365">NuGet から以外の特定の内部エラー。</span><span class="sxs-lookup"><span data-stu-id="c997c-365">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="c997c-366">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-366">**Common causes**</span></span> | <span data-ttu-id="c997c-367">詳細については、ログを確認します。</span><span class="sxs-lookup"><span data-stu-id="c997c-367">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="c997c-368">NU1500</span><span class="sxs-lookup"><span data-stu-id="c997c-368">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c997c-369">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c997c-369">**Issue**</span></span> | <span data-ttu-id="c997c-370">NuGet による非特定内部警告します。</span><span class="sxs-lookup"><span data-stu-id="c997c-370">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="c997c-371">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c997c-371">**Common causes**</span></span> | <span data-ttu-id="c997c-372">詳細については、ログを確認します。</span><span class="sxs-lookup"><span data-stu-id="c997c-372">Check the logs for more information</span></span> |
