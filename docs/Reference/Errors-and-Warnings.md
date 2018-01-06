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
ms.openlocfilehash: 53fccbb86f2920d870b5383070d043e25045a626
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="errors-and-warnings"></a><span data-ttu-id="c57c4-104">エラーと警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-104">Errors and warnings</span></span>

<span data-ttu-id="c57c4-105">4.3.0、NuGet では、このトピックで説明の番号付けはエラーと警告し、関連する問題に対処するための詳細情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-105">In NuGet 4.3.0, errors and warnings are numbered as described in this topic and provide detailed information to help you address the issues involved.</span></span> 

<span data-ttu-id="c57c4-106">エラーと警告の次のとおり、のみで使用[PackageReference ベース](../Consume-Packages/Package-References-in-Project-Files.md)プロジェクトおよび NuGet 4.3.0 です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-106">The errors and warnings listed here are available only with [PackageReference-based](../Consume-Packages/Package-References-in-Project-Files.md) projects and NuGet 4.3.0.</span></span> <span data-ttu-id="c57c4-107">NuGet では警告を抑制するか、それらのエラーへの昇格に MSBuild プロパティも使用します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-107">NuGet also honors MSBuild properties to suppress warnings or elevate them to errors.</span></span> <span data-ttu-id="c57c4-108">詳細については、次を参照してください。[する方法: コンパイラの警告を抑制する状況](/visualstudio/ide/how-to-suppress-compiler-warnings)、Visual Studio のマニュアルでします。</span><span class="sxs-lookup"><span data-stu-id="c57c4-108">For more information, see [How to: Suppress Compiler Warnings](/visualstudio/ide/how-to-suppress-compiler-warnings) in the Visual Studio documentation.</span></span>

<span data-ttu-id="c57c4-109">**エラー**</span><span class="sxs-lookup"><span data-stu-id="c57c4-109">**Errors**</span></span>

| <span data-ttu-id="c57c4-110">グループ化</span><span class="sxs-lookup"><span data-stu-id="c57c4-110">Group</span></span> | <span data-ttu-id="c57c4-111">エラー番号</span><span class="sxs-lookup"><span data-stu-id="c57c4-111">Error Numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="c57c4-112">無効な入力エラー</span><span class="sxs-lookup"><span data-stu-id="c57c4-112">Invalid input errors</span></span>](#invalid-input-errors) | <span data-ttu-id="c57c4-113">[NU1001](#nu1001)、 [NU1002](#nu1002)、 [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="c57c4-113">[NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003)</span></span> |
| [<span data-ttu-id="c57c4-114">パッケージとプロジェクトの不足エラー</span><span class="sxs-lookup"><span data-stu-id="c57c4-114">Missing package and project errors</span></span>](#missing-package-and-project-errors) | <span data-ttu-id="c57c4-115">[NU1100](#nu1100)、 [NU1101](#nu1101)、 [NU1102](#nu1102)、 [NU1103](#nu1103)、 [NU1104](#nu1104)、 [NU1105](#nu1105)、 [NU1106](#nu1106)、 [NU1107](#nu1107) (NU1607 以前) [NU1108](#nu1107) (NU1606 以前)</span><span class="sxs-lookup"><span data-stu-id="c57c4-115">[NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1107) (previously NU1606)</span></span> |
| [<span data-ttu-id="c57c4-116">互換性に関するエラー</span><span class="sxs-lookup"><span data-stu-id="c57c4-116">Compatibility errors</span></span>](#compatibility-errors) | <span data-ttu-id="c57c4-117">[NU1201](#nu1201)、 [NU1202](#nu1202)、 [NU1203](#nu1203)、 [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="c57c4-117">[NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401)</span></span> |

<span data-ttu-id="c57c4-118">**警告**</span><span class="sxs-lookup"><span data-stu-id="c57c4-118">**Warnings**</span></span>

| <span data-ttu-id="c57c4-119">グループ化</span><span class="sxs-lookup"><span data-stu-id="c57c4-119">Group</span></span> | <span data-ttu-id="c57c4-120">警告番号</span><span class="sxs-lookup"><span data-stu-id="c57c4-120">Warning numbers</span></span> |
| --- | --- |
| [<span data-ttu-id="c57c4-121">無効な入力の警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-121">Invalid input warnings</span></span>](#invalid-input-warnings) | <span data-ttu-id="c57c4-122">[NU1501](#nu1501)、 [NU1502](#nu1502)、 [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="c57c4-122">[NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503)</span></span> |
| [<span data-ttu-id="c57c4-123">予期しないパッケージのバージョンの警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-123">Unexpected package version warnings</span></span>](#unexpected-package-version-warnings) | <span data-ttu-id="c57c4-124">[NU1601](#nu1601)、 [NU1602](#nu1602)、 [NU1603](#nu1603)、 [NU1604](#nu1604)、 [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="c57c4-124">[NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605)</span></span> |
| [<span data-ttu-id="c57c4-125">競合回避モジュールの競合の警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-125">Resolver conflict warnings</span></span>](#resolver-conflict-warnings) | [<span data-ttu-id="c57c4-126">NU1608</span><span class="sxs-lookup"><span data-stu-id="c57c4-126">NU1608</span></span>](#nu1608) |
| [<span data-ttu-id="c57c4-127">パッケージのフォールバック警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-127">Package fallback warnings</span></span>](#package-fallback-warnings) | [<span data-ttu-id="c57c4-128">NU1701</span><span class="sxs-lookup"><span data-stu-id="c57c4-128">NU1701</span></span>](#nu1701) |
| [<span data-ttu-id="c57c4-129">フィードの警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-129">Feed warnings</span></span>](#feed-warnings) | [<span data-ttu-id="c57c4-130">NU1801</span><span class="sxs-lookup"><span data-stu-id="c57c4-130">NU1801</span></span>](#nu1801) |
| [<span data-ttu-id="c57c4-131">NuGet の内部エラーと警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-131">NuGet internal errors and warnings</span></span>](#nuget-internal-errors-and-warnings) | <span data-ttu-id="c57c4-132">[NU1000](#nu1000)、 [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="c57c4-132">[NU1000](#nu1000), [NU1500](#nu1500)</span></span> |

## <a name="invalid-input-errors"></a><span data-ttu-id="c57c4-133">無効な入力エラー</span><span class="sxs-lookup"><span data-stu-id="c57c4-133">Invalid input errors</span></span>

<span data-ttu-id="c57c4-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span><span class="sxs-lookup"><span data-stu-id="c57c4-134">[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)</span></span>

### <a name="nu1001"></a><span data-ttu-id="c57c4-135">NU1001</span><span class="sxs-lookup"><span data-stu-id="c57c4-135">NU1001</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-136">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-136">**Issue**</span></span> | <span data-ttu-id="c57c4-137">プロジェクトには、1 つまたは複数のフレームワークが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-137">The project doesn't contain one or more frameworks.</span></span> |
| <span data-ttu-id="c57c4-138">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-138">**Common causes**</span></span> | <span data-ttu-id="c57c4-139">プロジェクトが含まれていない、`TargetFramework`または`TargetFrameworks`プロパティです。</span><span class="sxs-lookup"><span data-stu-id="c57c4-139">The project doesn't contain a `TargetFramework` or `TargetFrameworks` property.</span></span> |
| <span data-ttu-id="c57c4-140">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-140">**Example message**</span></span> | <span data-ttu-id="c57c4-141">*プロジェクト projA では、どのターゲット フレームワーク c:\tmp\projA.csproj で指定されていません*</span><span class="sxs-lookup"><span data-stu-id="c57c4-141">*The project projA does not specify any target frameworks in c:\tmp\projA.csproj*</span></span> |

### <a name="nu1002"></a><span data-ttu-id="c57c4-142">NU1002</span><span class="sxs-lookup"><span data-stu-id="c57c4-142">NU1002</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-143">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-143">**Issue**</span></span> | <span data-ttu-id="c57c4-144">入力とクリア キーワードの組み合わせが無効です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-144">Invalid combination of inputs along with a CLEAR keyword.</span></span> |
| <span data-ttu-id="c57c4-145">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-145">**Common causes**</span></span> | <span data-ttu-id="c57c4-146">クリアを他の入力で組み合わせることはできません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-146">CLEAR may not be combined with other inputs.</span></span> |
| <span data-ttu-id="c57c4-147">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-147">**Example message**</span></span> | <span data-ttu-id="c57c4-148">*'CLEAR' では使用できませんの他の値と共に*</span><span class="sxs-lookup"><span data-stu-id="c57c4-148">*'CLEAR' cannot be used in conjunction with other values*</span></span> |

### <a name="nu1003"></a><span data-ttu-id="c57c4-149">NU1003</span><span class="sxs-lookup"><span data-stu-id="c57c4-149">NU1003</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-150">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-150">**Issue**</span></span> | <span data-ttu-id="c57c4-151">`PackageTargetFallback`および`AssetTargetFallback`資産を選択するための動作の違いを提供し、一緒に使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-151">`PackageTargetFallback` and `AssetTargetFallback` provide different behavior for selecting assets and cannot be used together.</span></span> |
| <span data-ttu-id="c57c4-152">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-152">**Common causes**</span></span> | <span data-ttu-id="c57c4-153">両方`PackageTargetFallback`と`AssetTargetFallback`プロジェクト内に存在します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-153">Both `PackageTargetFallback` and `AssetTargetFallback` exist in the project.</span></span> |
| <span data-ttu-id="c57c4-154">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-154">**Example message**</span></span> | <span data-ttu-id="c57c4-155">*PackageTargetFallback と AssetTargetFallback に使用することはできません。プロジェクトの環境から PackageTargetFallback(deprecated) 参照を削除します。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-155">*PackageTargetFallback and AssetTargetFallback cannot be used together. Remove PackageTargetFallback(deprecated) references from the project environment.*</span></span> |

## <a name="missing-package-and-project-errors"></a><span data-ttu-id="c57c4-156">パッケージとプロジェクトの不足エラー</span><span class="sxs-lookup"><span data-stu-id="c57c4-156">Missing package and project errors</span></span>

<span data-ttu-id="c57c4-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104)  |  [NU1105](#nu1105) | [NU1106](#nu1106)</span><span class="sxs-lookup"><span data-stu-id="c57c4-157">[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)</span></span>

### <a name="nu1100"></a><span data-ttu-id="c57c4-158">NU1100</span><span class="sxs-lookup"><span data-stu-id="c57c4-158">NU1100</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-159">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-159">**Issue**</span></span> | <span data-ttu-id="c57c4-160">依存関係グループを解決できません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-160">A dependency group not be resolved.</span></span> <span data-ttu-id="c57c4-161">これは、パッケージまたはプロジェクトではない型での一般的な問題です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-161">This is a generic issue for types that are not packages or projects.</span></span> |
| <span data-ttu-id="c57c4-162">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-162">**Common causes**</span></span> | <span data-ttu-id="c57c4-163">プロジェクトには、存在しないアイテムへの依存関係が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c57c4-163">The project contains a dependency on an item that doesn't exist.</span></span> |
| <span data-ttu-id="c57c4-164">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-164">**Example message**</span></span> | <span data-ttu-id="c57c4-165">*Net45 を System.Missing を解決できません。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-165">*Unable to resolve System.Missing for net45*</span></span> |

### <a name="nu1101"></a><span data-ttu-id="c57c4-166">NU1101</span><span class="sxs-lookup"><span data-stu-id="c57c4-166">NU1101</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-167">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-167">**Issue**</span></span> | <span data-ttu-id="c57c4-168">パッケージのソースに見つかりません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-168">The package cannot be found on any sources.</span></span> |
| <span data-ttu-id="c57c4-169">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-169">**Common causes**</span></span> | <span data-ttu-id="c57c4-170">適切なパッケージ ソースが見つからないか、パッケージの識別子が正しくありません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-170">The correct package source is missing or the package identifier is incorrect.</span></span> |
| <span data-ttu-id="c57c4-171">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-171">**Example message**</span></span> | <span data-ttu-id="c57c4-172">*パッケージ System.Missing が見つかりません。ソースでは、この id を持つパッケージが存在しません: dotnet コア、dotnet roslyn、nuget.org*</span><span class="sxs-lookup"><span data-stu-id="c57c4-172">*Unable to find package System.Missing. No packages exist with this id in source(s): dotnet-core, dotnet-roslyn, nuget.org*</span></span> |

### <a name="nu1102"></a><span data-ttu-id="c57c4-173">NU1102</span><span class="sxs-lookup"><span data-stu-id="c57c4-173">NU1102</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-174">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-174">**Issue**</span></span> | <span data-ttu-id="c57c4-175">パッケージ識別子が見つかりましたが、ソースのいずれかで指定した依存関係の範囲内のバージョンが見つかりません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-175">The package identifier is found but a version within the specified dependency range cannot be found on any of the sources.</span></span> |
| <span data-ttu-id="c57c4-176">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-176">**Common causes**</span></span> | <span data-ttu-id="c57c4-177">適切なパッケージ ソースが見つからないか、依存関係の範囲が正しくありません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-177">The correct package source is missing or the dependency range is incorrect.</span></span> <span data-ttu-id="c57c4-178">パッケージとユーザーではなく、範囲を指定する場合があります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-178">The range might be specified by a package and not the user.</span></span> <span data-ttu-id="c57c4-179">ユーザーは、このパッケージがプロジェクトで直接参照されている場合に使用可能なバージョンに切り替える必要があります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-179">The user may need to switch to an available version if this package is referenced by the project directly.</span></span> |
| <span data-ttu-id="c57c4-180">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-180">**Example message**</span></span> | <span data-ttu-id="c57c4-181">*NuGet.Versioning バージョンでパッケージを見つけることができません (> = 9.0.1)<br/> -nuget.org で見つかった 30 版 [バージョンに最も近い: 4.0.0]<br/> -dotnet buildtools で見つかった 10 バージョン [バージョンに最も近い: 4.0.0-rc-2129]<br/> -9 の検出NuGetVolatile のバージョン [バージョンに最も近い: 3.0.0-beta-00032]<br/> -0 のバージョンを記載 dotnet コア<br/>-dotnet roslyn で 0 バージョンを検出*</span><span class="sxs-lookup"><span data-stu-id="c57c4-181">*Unable to find package NuGet.Versioning with version (>= 9.0.1)<br/>  - Found 30 version(s) in nuget.org [ Nearest version: 4.0.0 ]<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1103"></a><span data-ttu-id="c57c4-182">NU1103</span><span class="sxs-lookup"><span data-stu-id="c57c4-182">NU1103</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-183">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-183">**Issue**</span></span> | <span data-ttu-id="c57c4-184">依存関係の範囲内で安定したバージョンが見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="c57c4-184">No stable versions were found in the dependency range.</span></span> <span data-ttu-id="c57c4-185">プレリリース版は見つかりましたが、許可されていません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-185">Pre-release versions were found but are not allowed.</span></span> |
| <span data-ttu-id="c57c4-186">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-186">**Common causes**</span></span> | <span data-ttu-id="c57c4-187">プロジェクトでは、依存関係の範囲の安定したバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-187">The project specified a stable version for the dependency range.</span></span> <span data-ttu-id="c57c4-188">ユーザーは、プレリリース版を含むバージョンの範囲を変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-188">Users need to change the version range to include pre-release versions.</span></span> |
| <span data-ttu-id="c57c4-189">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-189">**Example message**</span></span> | <span data-ttu-id="c57c4-190">*バージョンと安定したパッケージ NuGet.Versioning を見つけることができません (> = 3.0.0)<br/> -dotnet buildtools で見つかった 10 バージョン [バージョンに最も近い: 4.0.0-rc-2129]<br/> -NuGetVolatile で見つかった 9 版 [バージョンに最も近い: 3.0.0-beta-00032]<br/> -0 のバージョンを記載 dotnet コア<br/>-dotnet roslyn で 0 バージョンが見つかりません*</span><span class="sxs-lookup"><span data-stu-id="c57c4-190">*Unable to find a stable package NuGet.Versioning with version (>= 3.0.0)<br/>  - Found 10 version(s) in dotnet-buildtools [ Nearest version: 4.0.0-rc-2129 ]<br/>  - Found 9 version(s) in NuGetVolatile [ Nearest version: 3.0.0-beta-00032 ]<br/>  - Found 0 version(s) in dotnet-core<br/>  - Found 0 version(s) in dotnet-roslyn*</span></span> |

### <a name="nu1104"></a><span data-ttu-id="c57c4-191">NU1104</span><span class="sxs-lookup"><span data-stu-id="c57c4-191">NU1104</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-192">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-192">**Issue**</span></span> | <span data-ttu-id="c57c4-193">ProjectReference は、存在しないファイルを指します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-193">A ProjectReference points to a file that doesn't exist.</span></span> |
| <span data-ttu-id="c57c4-194">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-194">**Common causes**</span></span> | <span data-ttu-id="c57c4-195">プロジェクト ファイルがディスクから不足しているか、参照が正しくありません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-195">The project file is missing from disk or the reference is incorrect.</span></span> |
| <span data-ttu-id="c57c4-196">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-196">**Example message**</span></span> | <span data-ttu-id="c57c4-197">*プロジェクト参照では、'c:\a.csproj' は存在しません。プロジェクトへの参照が有効であると、プロジェクト ファイルが存在することを確認してください。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-197">*Project reference does not exist 'c:\a.csproj'. Check that the project reference is valid and that the project file exists.*</span></span> |

### <a name="nu1105"></a><span data-ttu-id="c57c4-198">NU1105</span><span class="sxs-lookup"><span data-stu-id="c57c4-198">NU1105</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-199">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-199">**Issue**</span></span> | <span data-ttu-id="c57c4-200">プロジェクト ファイルが存在しますが、その復元に関する情報が指定されていません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-200">The project file exists but no restore information was provided for it.</span></span> |
| <span data-ttu-id="c57c4-201">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-201">**Common causes**</span></span> | <span data-ttu-id="c57c4-202">Visual Studio でプロジェクトが読み込まれているこの可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-202">In Visual Studio this could mean that the project is unloaded.</span></span> <span data-ttu-id="c57c4-203">コマンド ラインからは、ファイルが破損しているか、ことが含まれていないカスタム プロジェクトを読み込むへの復元に必要な imports ターゲットの後にこの可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-203">From the command line this could mean that the file is corrupt or that it doesn't contain the custom after imports target needed for restore to read the project.</span></span> |
| <span data-ttu-id="c57c4-204">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-204">**Example message**</span></span> | <span data-ttu-id="c57c4-205">*'C:\a.csproj' のプロジェクト情報を読み取れません。プロジェクト ファイルには、復元に必要なターゲットを無効または不足している可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-205">*Unable to read project information for 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

### <a name="nu1106"></a><span data-ttu-id="c57c4-206">NU1106</span><span class="sxs-lookup"><span data-stu-id="c57c4-206">NU1106</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-207">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-207">**Issue**</span></span> | <span data-ttu-id="c57c4-208">依存関係の制約を解決することはできません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-208">Dependency constraints cannot be resolved.</span></span> |
| <span data-ttu-id="c57c4-209">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-209">**Common causes**</span></span> | <span data-ttu-id="c57c4-210">パッケージには、正確なバージョンの大まかな範囲ではなくパッケージへの依存関係が含まれます。</span><span class="sxs-lookup"><span data-stu-id="c57c4-210">Packages contain dependency on exact versions of a package instead of open-ended ranges.</span></span> |
| <span data-ttu-id="c57c4-211">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-211">**Example message**</span></span> | <span data-ttu-id="c57c4-212">*{Id} の矛盾する要求を満たすことができません: {競合パス} フレームワーク: {ターゲット グラフ}*</span><span class="sxs-lookup"><span data-stu-id="c57c4-212">*Unable to satisfy conflicting requests for {id}: {conflict path} Framework: {target graph}*</span></span> |

<span data-ttu-id="c57c4-213">< a name ="NU1107 ></a></span><span class="sxs-lookup"><span data-stu-id="c57c4-213"><a name="NU1107></a></span></span>

### <a name="nu1107-previously-nu1607"></a><span data-ttu-id="c57c4-214">NU1107 (NU1607 以前)</span><span class="sxs-lookup"><span data-stu-id="c57c4-214">NU1107 (Previously NU1607)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-215">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-215">**Issue**</span></span> | <span data-ttu-id="c57c4-216">パッケージ間で依存関係の制約を解決できません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-216">Unable to resolve dependency constraints between packages.</span></span> |
| <span data-ttu-id="c57c4-217">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-217">**Common causes**</span></span> | <span data-ttu-id="c57c4-218">正確なバージョンに依存関係の制約を含むパッケージでは、他のパッケージを必要な場合は、バージョンを増やすには許可されません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-218">Packages with dependency constraints on exact versions do not allow other packages to increase the version if needed.</span></span> |
| <span data-ttu-id="c57c4-219">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-219">**Example message**</span></span> | <span data-ttu-id="c57c4-220">*バージョンの競合の NuGet.Versioning が検出されました。この問題を解決するのには、プロジェクトから直接パッケージを参照します。<br/>NuGet.Packaging 3.5.0 NuGet.Versioning (= 3.5.0)]-> [<br/> NuGet.Configuration 4.0.0 NuGet.Versioning (= 4.0.0)]-> [*</span><span class="sxs-lookup"><span data-stu-id="c57c4-220">*Version conflict detected for NuGet.Versioning. Reference the package directly from the project to resolve this issue.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)*</span></span> |

<span data-ttu-id="c57c4-221">< a name ="NU1108 ></a></span><span class="sxs-lookup"><span data-stu-id="c57c4-221"><a name="NU1108></a></span></span>

### <a name="nu1108-previously-nu1606"></a><span data-ttu-id="c57c4-222">NU1108 (NU1606 以前)</span><span class="sxs-lookup"><span data-stu-id="c57c4-222">NU1108 (Previously NU1606)</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-223">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-223">**Issue**</span></span> | <span data-ttu-id="c57c4-224">循環する依存関係が検出されました。</span><span class="sxs-lookup"><span data-stu-id="c57c4-224">A circular dependency was detected.</span></span> |
| <span data-ttu-id="c57c4-225">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-225">**Common causes**</span></span> | <span data-ttu-id="c57c4-226">パッケージが正しく作成されていません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-226">A package is authored incorrectly.</span></span> |
| <span data-ttu-id="c57c4-227">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-227">**Example message**</span></span> | <span data-ttu-id="c57c4-228">*サイクルが検出されました: A が B]-> [A]-> [*</span><span class="sxs-lookup"><span data-stu-id="c57c4-228">*Cycle detected: A -> B -> A*</span></span> |

## <a name="compatibility-errors"></a><span data-ttu-id="c57c4-229">互換性に関するエラー</span><span class="sxs-lookup"><span data-stu-id="c57c4-229">Compatibility errors</span></span>

<span data-ttu-id="c57c4-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span><span class="sxs-lookup"><span data-stu-id="c57c4-230">[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)</span></span>

### <a name="nu1201"></a><span data-ttu-id="c57c4-231">NU1201</span><span class="sxs-lookup"><span data-stu-id="c57c4-231">NU1201</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-232">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-232">**Issue**</span></span> | <span data-ttu-id="c57c4-233">依存関係プロジェクトには、現在のプロジェクトと互換性のあるフレームワークが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-233">A dependency project doesn't contain a framework compatible with the current project.</span></span> |
| <span data-ttu-id="c57c4-234">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-234">**Common causes**</span></span> | <span data-ttu-id="c57c4-235">プロジェクトのターゲット フレームワークは、プロジェクトが使用より高いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="c57c4-235">The project's target framework is a higher version than the consuming project.</span></span> |
| <span data-ttu-id="c57c4-236">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-236">**Example message**</span></span> | <span data-ttu-id="c57c4-237">*プロジェクト ServerWeb は netstandard1.3 と互換性がありません (です。NETStandard, Version = v1.3)。プロジェクトの ServerWeb サポート:<br/> -netstandard1.6 (です。NETStandard, Version = v1.6)<br/> -netcoreapp1.0 (です。NETCoreApp, Version = v1.0)*</span><span class="sxs-lookup"><span data-stu-id="c57c4-237">*Project ServerWeb is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Project ServerWeb supports:<br/>  - netstandard1.6 (.NETStandard,Version=v1.6)<br/>  - netcoreapp1.0 (.NETCoreApp,Version=v1.0)*</span></span> |

### <a name="nu1202"></a><span data-ttu-id="c57c4-238">NU1202</span><span class="sxs-lookup"><span data-stu-id="c57c4-238">NU1202</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-239">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-239">**Issue**</span></span> | <span data-ttu-id="c57c4-240">依存関係パッケージには、プロジェクトと互換性のある任意のアセットが含まれていません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-240">A dependency package doesn't contain any assets compatible with the project.</span></span> |
| <span data-ttu-id="c57c4-241">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-241">**Common causes**</span></span> | <span data-ttu-id="c57c4-242">パッケージには、プロジェクトのターゲット フレームワークをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-242">The package doesn't support the project's target framework.</span></span> |
| <span data-ttu-id="c57c4-243">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-243">**Example message**</span></span> | <span data-ttu-id="c57c4-244">*パッケージ System.ComponentModel.EventBasedAsync 4.0.11 は netstandard1.3 と互換性がありません (です。NETStandard, Version = v1.3)。System.ComponentModel.EventBasedAsync 4.0.11 サポートをパッケージ化:<br/> -monoandroid10 (MonoAndroid、バージョン = v1.0)<br/> -monotouch10 (MonoTouch, Version = v1.0)<br/> -net45 (です。NETFramework, Version = v4.5)<br/> -netcore50 (です。NETCore, Version = v5.0)<br/> -netstandard1.0 (です。NETStandard, Version = v1.0)<br/> -portable net45 + win8 + wp8 + wpa81 (です。NETPortable、バージョン v0.0、プロファイルを = = Profile259)<br/> -win8 (Windows、バージョン = バージョン 8.0)<br/> -wp8 (WindowsPhone, Version = バージョン 8.0)<br/> -wpa81 (WindowsPhoneApp、バージョン = v8.1)<br/> -xamarinios10 (Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span><span class="sxs-lookup"><span data-stu-id="c57c4-244">*Package System.ComponentModel.EventBasedAsync 4.0.11 is not compatible with netstandard1.3 (.NETStandard,Version=v1.3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*</span></span>|

### <a name="nu1203"></a><span data-ttu-id="c57c4-245">NU1203</span><span class="sxs-lookup"><span data-stu-id="c57c4-245">NU1203</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-246">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-246">**Issue**</span></span> | <span data-ttu-id="c57c4-247">パッケージがプロジェクトをサポートしない`RuntimeIdentifier`です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-247">The package doesn't support the project's `RuntimeIdentifier`.</span></span> |
| <span data-ttu-id="c57c4-248">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-248">**Common causes**</span></span> | <span data-ttu-id="c57c4-249">現在をサポートしていないパッケージ`RuntimeIdentifier`です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-249">The package doesn't support the current `RuntimeIdentifier`.</span></span> <span data-ttu-id="c57c4-250">変更、`RuntimeIdentifier`必要な場合は、プロジェクトで使用される値。</span><span class="sxs-lookup"><span data-stu-id="c57c4-250">Change the `RuntimeIdentifier` values used in the project if needed.</span></span> |
| <span data-ttu-id="c57c4-251">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-251">**Example message**</span></span> | <span data-ttu-id="c57c4-252">*System.Example 1.0.0 a.dll のコンパイル時参照アセンブリ net461、上には互換性のあるランタイム アセンブリが存在しません。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-252">*System.Example 1.0.0 provides a compile-time reference assembly for a.dll on net461, but there is no compatible run-time assembly.*</span></span> |

### <a name="nu1401"></a><span data-ttu-id="c57c4-253">NU1401</span><span class="sxs-lookup"><span data-stu-id="c57c4-253">NU1401</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-254">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-254">**Issue**</span></span> | <span data-ttu-id="c57c4-255">パッケージには、機能、または NuGet のインストールされているバージョンでサポートされていないフレームワークが必要です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-255">The package requires features or frameworks not currently supported by the installed version of NuGet.</span></span> |
| <span data-ttu-id="c57c4-256">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-256">**Common causes**</span></span> | <span data-ttu-id="c57c4-257">問題を解決する NuGet をアップグレードします。</span><span class="sxs-lookup"><span data-stu-id="c57c4-257">Upgrade NuGet to fix the issue.</span></span> |
| <span data-ttu-id="c57c4-258">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-258">**Example message**</span></span> | <span data-ttu-id="c57c4-259">*'NuGet.Versioning' パッケージは NuGet クライアント バージョン '5.0.0' を必要以上に設定するが現在の NuGet バージョンは '4.3.0' です。NuGet をアップグレードするには、http://docs.nuget.org/consume/installing-nuget を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-259">*The 'NuGet.Versioning' package requires NuGet client version '5.0.0' or above, but the current NuGet version is '4.3.0'. To upgrade NuGet, please go to http://docs.nuget.org/consume/installing-nuget.*</span></span> |

## <a name="invalid-input-warnings"></a><span data-ttu-id="c57c4-260">無効な入力の警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-260">Invalid input warnings</span></span>

<span data-ttu-id="c57c4-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span><span class="sxs-lookup"><span data-stu-id="c57c4-261">[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)</span></span>

### <a name="nu1501"></a><span data-ttu-id="c57c4-262">NU1501</span><span class="sxs-lookup"><span data-stu-id="c57c4-262">NU1501</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-263">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-263">**Issue**</span></span> | <span data-ttu-id="c57c4-264">操作しようとして、プロジェクトの復元に見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="c57c4-264">The project restore is attempting to operate on was not found.</span></span> |
| <span data-ttu-id="c57c4-265">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-265">**Common causes**</span></span> | <span data-ttu-id="c57c4-266">プロジェクトがありません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-266">The project is missing.</span></span> |
| <span data-ttu-id="c57c4-267">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-267">**Example message**</span></span> | <span data-ttu-id="c57c4-268">*フォルダー 'c:\projects\a' に復元するプロジェクトが含まれていません。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-268">*The folder 'c:\projects\a' does not contain a project to restore.*</span></span> |

### <a name="nu1502"></a><span data-ttu-id="c57c4-269">NU1502</span><span class="sxs-lookup"><span data-stu-id="c57c4-269">NU1502</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-270">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-270">**Issue**</span></span> | <span data-ttu-id="c57c4-271">`RuntimeSupports`無効なプロファイルが含まれています。</span><span class="sxs-lookup"><span data-stu-id="c57c4-271">`RuntimeSupports` contains an invalid profile.</span></span> |
| <span data-ttu-id="c57c4-272">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-272">**Common causes**</span></span> | <span data-ttu-id="c57c4-273">サポートしているプロファイルが見つかりません、`runtime.json`現在の依存関係パッケージからファイル。</span><span class="sxs-lookup"><span data-stu-id="c57c4-273">The supports profile was not found in a `runtime.json` file from the current dependency packages.</span></span> |
| <span data-ttu-id="c57c4-274">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-274">**Example message**</span></span> | <span data-ttu-id="c57c4-275">*不明な互換性プロファイル: aaa*</span><span class="sxs-lookup"><span data-stu-id="c57c4-275">*Unknown Compatibility Profile: aaa*</span></span> |

### <a name="nu1503"></a><span data-ttu-id="c57c4-276">NU1503</span><span class="sxs-lookup"><span data-stu-id="c57c4-276">NU1503</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-277">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-277">**Issue**</span></span> | <span data-ttu-id="c57c4-278">依存関係プロジェクトでは、NuGet の復元のターゲットをインポートしません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-278">A dependency project doesn't import NuGet's restore targets.</span></span> <span data-ttu-id="c57c4-279">NU1105 に似ていますが、ここで、プロジェクトがスキップされた、すべての復元が失敗の原因ではなく無視します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-279">This is similar to NU1105 but here the project is skipped and ignored instead of causing all of restore to fail.</span></span> <span data-ttu-id="c57c4-280">複雑なソリューションでもある復元をサポートしない可能性があるプロジェクトの他の種類。</span><span class="sxs-lookup"><span data-stu-id="c57c4-280">In complex solutions there are often other types of projects that may not support restore.</span></span> |
| <span data-ttu-id="c57c4-281">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-281">**Common causes**</span></span> | <span data-ttu-id="c57c4-282">プロジェクトの復元は自動的にインポートする共通のプロパティ/ターゲットはインポートしない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-282">This can happen for projects that do not import common props/targets which automatically import restore.</span></span> <span data-ttu-id="c57c4-283">プロジェクトを復元する必要がある場合は無視できます。</span><span class="sxs-lookup"><span data-stu-id="c57c4-283">If the project doesn't need to be restored this can be ignored.</span></span> |
| <span data-ttu-id="c57c4-284">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-284">**Example message**</span></span> | <span data-ttu-id="c57c4-285">*プロジェクト 'c:\a.csproj' の復元をスキップしています。プロジェクト ファイルには、復元に必要なターゲットを無効または不足している可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-285">*Skipping restore for project 'c:\a.csproj'. The project file may be invalid or missing targets required for restore.*</span></span> |

## <a name="unexpected-package-version-warnings"></a><span data-ttu-id="c57c4-286">予期しないパッケージのバージョンの警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-286">Unexpected package version warnings</span></span>

<span data-ttu-id="c57c4-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span><span class="sxs-lookup"><span data-stu-id="c57c4-287">[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)</span></span>

### <a name="nu1601"></a><span data-ttu-id="c57c4-288">NU1601</span><span class="sxs-lookup"><span data-stu-id="c57c4-288">NU1601</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-289">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-289">**Issue**</span></span> | <span data-ttu-id="c57c4-290">直接プロジェクトの依存関係が、指定したプロジェクトより新しいバージョンに高くなります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-290">A direct project dependency was bumped to a higher version than the project specified.</span></span> |
| <span data-ttu-id="c57c4-291">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-291">**Common causes**</span></span> | <span data-ttu-id="c57c4-292">別の依存関係パッケージより新しいバージョンを必要し、パッケージを高きます。</span><span class="sxs-lookup"><span data-stu-id="c57c4-292">Another dependency package required a higher version and bumped the package up.</span></span> |
| <span data-ttu-id="c57c4-293">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-293">**Example message**</span></span> | <span data-ttu-id="c57c4-294">*指定された依存関係が NuGet.Versioning (> = 3.5.0) NuGet.Versioning 4.0.0 で終了しましたが、します。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-294">*Dependency specified was NuGet.Versioning (>= 3.5.0) but ended up with NuGet.Versioning 4.0.0.*</span></span> |

### <a name="nu1602"></a><span data-ttu-id="c57c4-295">NU1602</span><span class="sxs-lookup"><span data-stu-id="c57c4-295">NU1602</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-296">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-296">**Issue**</span></span> | <span data-ttu-id="c57c4-297">パッケージの依存関係には、下限値がありません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-297">A package dependency is missing a lower bound.</span></span> <span data-ttu-id="c57c4-298">これは、検索への復元を許可しない、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-298">This doesn't allow restore to find the *best match*.</span></span> <span data-ttu-id="c57c4-299">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-299">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c57c4-300">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-300">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c57c4-301">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-301">**Common causes**</span></span> | <span data-ttu-id="c57c4-302">これは通常、パッケージ作成エラーです。</span><span class="sxs-lookup"><span data-stu-id="c57c4-302">This is usually a package authoring error.</span></span> |
| <span data-ttu-id="c57c4-303">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-303">**Example message**</span></span> | <span data-ttu-id="c57c4-304">*NuGet.Packaging 4.0.0 では、依存 NuGet.Versioning (> 3.5.0) のため、下限は提供されません。3.6.0 のおおよその最適な一致が解決されました。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-304">*NuGet.Packaging 4.0.0 does not provide an inclusive lower bound for dependency NuGet.Versioning (> 3.5.0). An approximate best match of 3.6.0 was resolved.*</span></span> |

### <a name="nu1603"></a><span data-ttu-id="c57c4-305">NU1603</span><span class="sxs-lookup"><span data-stu-id="c57c4-305">NU1603</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-306">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-306">**Issue**</span></span> | <span data-ttu-id="c57c4-307">パッケージの依存関係は、バージョンが見つかりませんでしたを指定します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-307">A package dependency specified a version that could not be found.</span></span> <span data-ttu-id="c57c4-308">以降のバージョンは、に対して、パッケージが作成されたものと異なるを代わりに、使用されました。</span><span class="sxs-lookup"><span data-stu-id="c57c4-308">A higher version was used instead, which differs from what the package was authored against.</span></span><br/><br/><span data-ttu-id="c57c4-309">つまり、復元が見つかりませんでした、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-309">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="c57c4-310">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-310">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c57c4-311">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-311">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c57c4-312">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-312">**Common causes**</span></span> | <span data-ttu-id="c57c4-313">パッケージ ソースでは、予想される下限バージョンは含まれません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-313">The package sources do not contain the expected lower bound version.</span></span> <span data-ttu-id="c57c4-314">期待どおりパッケージがリリースされていない場合、パッケージの作成エラーでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-314">If the package expected has not been released then this may be a package authoring error.</span></span> |
| <span data-ttu-id="c57c4-315">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-315">**Example message**</span></span> | <span data-ttu-id="c57c4-316">NuGet.Packaging 4.0.0 NuGet.Versioning によって異なります (> = 4.0.0) が、4.0.0 が見つかりませんでした。</span><span class="sxs-lookup"><span data-stu-id="c57c4-316">NuGet.Packaging 4.0.0 depends on NuGet.Versioning (>= 4.0.0) but 4.0.0 was not found.</span></span> <span data-ttu-id="c57c4-317">5.0.0 以降のおおよその最適な一致が解決されました。</span><span class="sxs-lookup"><span data-stu-id="c57c4-317">An approximate best match of 5.0.0 was resolved.</span></span> |

### <a name="nu1604"></a><span data-ttu-id="c57c4-318">NU1604</span><span class="sxs-lookup"><span data-stu-id="c57c4-318">NU1604</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-319">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-319">**Issue**</span></span> | <span data-ttu-id="c57c4-320">プロジェクトの依存関係、下限が定義されません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-320">A project dependency doesn't define a lower bound.</span></span><br/><br/><span data-ttu-id="c57c4-321">つまり、復元が見つかりませんでした、*最適一致*です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-321">This means that restore did not find the *best match*.</span></span> <span data-ttu-id="c57c4-322">各復元は、使用できる、古いバージョンを検索しようとするは下位変化します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-322">Each restore will float downwards trying to find a lower version that can be used.</span></span> <span data-ttu-id="c57c4-323">これは、その復元が毎回ユーザー パッケージ フォルダーに既に存在するパッケージを使用する代わりにすべてのソースを確認するオンラインになることを意味します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-323">This means that restore goes online to check all sources each time instead of using the packages that already exist in the user package folder.</span></span> |
| <span data-ttu-id="c57c4-324">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-324">**Common causes**</span></span> | <span data-ttu-id="c57c4-325">プロジェクトの*PackageReference* *バージョン*属性は、下限の境界を含むように更新する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-325">The project's *PackageReference* *Version* attribute should be updated to include a lower bound.</span></span> |
| <span data-ttu-id="c57c4-326">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-326">**Example message**</span></span> | <span data-ttu-id="c57c4-327">*プロジェクトの依存関係 NuGet.Versioning (< = 9.0.0) doe が包括的の下限値が含まれていません。結果の整合性の復元に依存関係のバージョンに下限の境界を含めます。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-327">*Project dependency NuGet.Versioning (<= 9.0.0) doe not contain an inclusive lower bound. Include a lower bound in the dependency version to ensure consistent restore results.*</span></span> |

### <a name="nu1605"></a><span data-ttu-id="c57c4-328">NU1605</span><span class="sxs-lookup"><span data-stu-id="c57c4-328">NU1605</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-329">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-329">**Issue**</span></span> | <span data-ttu-id="c57c4-330">依存関係パッケージには、パッケージの復元が最終的により高いバージョンでバージョン制約が指定されています。</span><span class="sxs-lookup"><span data-stu-id="c57c4-330">A dependency package specified a version constraint on a higher version of a package than restore ultimately resolved.</span></span> |
| <span data-ttu-id="c57c4-331">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-331">**Common causes**</span></span> | <span data-ttu-id="c57c4-332">パッケージを解決するときに最も近いが優先されます。</span><span class="sxs-lookup"><span data-stu-id="c57c4-332">Nearest wins when resolving packages.</span></span> <span data-ttu-id="c57c4-333">グラフ内の最も近いパッケージには、離れた場所にあるパッケージがオーバーライドされている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c57c4-333">A nearer package in the graph may have overridden a distant package.</span></span> |
| <span data-ttu-id="c57c4-334">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-334">**Example message**</span></span> | <span data-ttu-id="c57c4-335">*パッケージのダウン グレードが検出されました: 3.5.0 に 4.0.0 から NuGet.Versioning です。異なるバージョンを選択するプロジェクトから直接パッケージを参照します。<br/>NuGet.Packaging 3.5.0 NuGet.Versioning 3.5.0]-> [<br/> NuGet.Commands 4.0.0 NuGet.Configuration]-> [4.0.0 NuGet.Versioning 4.0.0]-> [*</span><span class="sxs-lookup"><span data-stu-id="c57c4-335">*Detected package downgrade: NuGet.Versioning from 4.0.0 to 3.5.0. Reference the package directly from the project to select a different version.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0*</span></span> |

## <a name="resolver-conflict-warnings"></a><span data-ttu-id="c57c4-336">競合回避モジュールの競合の警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-336">Resolver conflict warnings</span></span>

[<span data-ttu-id="c57c4-337">NU1608</span><span class="sxs-lookup"><span data-stu-id="c57c4-337">NU1608</span></span>](#nu1608)

### <a name="nu1608"></a><span data-ttu-id="c57c4-338">NU1608</span><span class="sxs-lookup"><span data-stu-id="c57c4-338">NU1608</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-339">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-339">**Issue**</span></span> | <span data-ttu-id="c57c4-340">解決パッケージは、依存関係の制約によりより高い。</span><span class="sxs-lookup"><span data-stu-id="c57c4-340">A resolve package is higher than a dependency constraint allows.</span></span> <span data-ttu-id="c57c4-341">これが意図的ないくつかの場合と、警告を抑制することができます。</span><span class="sxs-lookup"><span data-stu-id="c57c4-341">In some cases this is intentional and the warning can be suppressed.</span></span> |
| <span data-ttu-id="c57c4-342">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-342">**Common causes**</span></span> | <span data-ttu-id="c57c4-343">プロジェクトを直接参照されているパッケージには、他のパッケージからの依存関係の制約がよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="c57c4-343">A package referenced directly by a project will override dependency constraints from other packages.</span></span>   |
| <span data-ttu-id="c57c4-344">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-344">**Example message**</span></span> | <span data-ttu-id="c57c4-345">*依存関係の制約の外部で検出されたパッケージのバージョン: x 1.0.0 y (1.0.0 =) が必要ですが、バージョン y 2.0.0 が解決されました。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-345">*Detected package version outside of dependency constraint: x 1.0.0 requires y (= 1.0.0) but version y 2.0.0 was resolved.*</span></span> |

## <a name="package-fallback-warnings"></a><span data-ttu-id="c57c4-346">パッケージのフォールバック警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-346">Package fallback warnings</span></span>

[<span data-ttu-id="c57c4-347">NU1701</span><span class="sxs-lookup"><span data-stu-id="c57c4-347">NU1701</span></span>](#nu1701)

### <a name="nu1701"></a><span data-ttu-id="c57c4-348">NU1701</span><span class="sxs-lookup"><span data-stu-id="c57c4-348">NU1701</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-349">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-349">**Issue**</span></span> | <span data-ttu-id="c57c4-350">*PackageTargetFallback/AssetTargetFallback*パッケージから資産を選択するために使用されました。</span><span class="sxs-lookup"><span data-stu-id="c57c4-350">*PackageTargetFallback/AssetTargetFallback* was used to select assets from a package.</span></span> <span data-ttu-id="c57c4-351">これは、ユーザーに、資産が 100% の互換性がある可能性がありますされないことを通知する警告です。</span><span class="sxs-lookup"><span data-stu-id="c57c4-351">This is a warning to let the user know that the assets may not be 100% compatible.</span></span> |
| <span data-ttu-id="c57c4-352">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-352">**Common causes**</span></span> | <span data-ttu-id="c57c4-353">パッケージには、プロジェクトのフレームワークをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-353">The package doesn't support the project framework.</span></span> |
| <span data-ttu-id="c57c4-354">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-354">**Example message**</span></span> | <span data-ttu-id="c57c4-355">*使用して 'portable net45 + win8' 代わりにプロジェクトのターゲット フレームワーク 'netstandard1.5' パッケージ 'NuGet.Versioning' が復元されました。このパッケージは、プロジェクトを完全に互換性がない可能性があります。*</span><span class="sxs-lookup"><span data-stu-id="c57c4-355">*Package 'NuGet.Versioning' was restored using 'portable-net45+win8' instead the project target framework 'netstandard1.5'. This package may not be fully compatible with your project.*</span></span> |

## <a name="feed-warnings"></a><span data-ttu-id="c57c4-356">フィードの警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-356">Feed warnings</span></span>

[<span data-ttu-id="c57c4-357">NU1801</span><span class="sxs-lookup"><span data-stu-id="c57c4-357">NU1801</span></span>](#nu1801)

### <a name="nu1801"></a><span data-ttu-id="c57c4-358">NU1801</span><span class="sxs-lookup"><span data-stu-id="c57c4-358">NU1801</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-359">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-359">**Issue**</span></span> | <span data-ttu-id="c57c4-360">フィードを読み取る際にエラーが発生したときに`IgnoreFailedSources`が設定されて true の場合、致命的でない警告に変換することをします。</span><span class="sxs-lookup"><span data-stu-id="c57c4-360">An error occurred when reading the feed when `IgnoreFailedSources` is set to true, converting it to a non-fatal warning.</span></span> <span data-ttu-id="c57c4-361">これにより、すべてのメッセージが含まれがジェネリックです。</span><span class="sxs-lookup"><span data-stu-id="c57c4-361">This could contain any message and is generic.</span></span> |
| <span data-ttu-id="c57c4-362">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-362">**Common causes**</span></span> | <span data-ttu-id="c57c4-363">ソースが正しくありません。</span><span class="sxs-lookup"><span data-stu-id="c57c4-363">The source is invalid.</span></span> |
| <span data-ttu-id="c57c4-364">**メッセージの例**</span><span class="sxs-lookup"><span data-stu-id="c57c4-364">**Example message**</span></span> | <span data-ttu-id="c57c4-365">N/A</span><span class="sxs-lookup"><span data-stu-id="c57c4-365">n/a</span></span> |

## <a name="nuget-internal-errors-and-warnings"></a><span data-ttu-id="c57c4-366">NuGet の内部エラーと警告</span><span class="sxs-lookup"><span data-stu-id="c57c4-366">NuGet internal errors and warnings</span></span>

<span data-ttu-id="c57c4-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span><span class="sxs-lookup"><span data-stu-id="c57c4-367">[NU1000](#nu1000) | [NU1500](#nu1500)</span></span>

### <a name="nu1000"></a><span data-ttu-id="c57c4-368">NU1000</span><span class="sxs-lookup"><span data-stu-id="c57c4-368">NU1000</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-369">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-369">**Issue**</span></span> | <span data-ttu-id="c57c4-370">NuGet から以外の特定の内部エラー。</span><span class="sxs-lookup"><span data-stu-id="c57c4-370">A non specific internal error from NuGet.</span></span> |
| <span data-ttu-id="c57c4-371">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-371">**Common causes**</span></span> | <span data-ttu-id="c57c4-372">詳細については、ログを確認します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-372">Check the logs for more information</span></span> |

### <a name="nu1500"></a><span data-ttu-id="c57c4-373">NU1500</span><span class="sxs-lookup"><span data-stu-id="c57c4-373">NU1500</span></span>

| | |
| --- | --- |
| <span data-ttu-id="c57c4-374">**問題点**</span><span class="sxs-lookup"><span data-stu-id="c57c4-374">**Issue**</span></span> | <span data-ttu-id="c57c4-375">NuGet による非特定内部警告します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-375">A non specific internal warning from NuGet.</span></span> |
| <span data-ttu-id="c57c4-376">**一般的な原因**</span><span class="sxs-lookup"><span data-stu-id="c57c4-376">**Common causes**</span></span> | <span data-ttu-id="c57c4-377">詳細については、ログを確認します。</span><span class="sxs-lookup"><span data-stu-id="c57c4-377">Check the logs for more information</span></span> |
