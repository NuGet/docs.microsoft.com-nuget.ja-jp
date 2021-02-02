---
title: NuGet パッケージ バージョンのリファレンス
description: NuGet パッケージが依存する他のパッケージのバージョン番号と範囲を指定する方法と、依存関係をインストールする方法について詳しく説明します。
author: JonDouglas
ms.author: jodou
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 5ba7860fae1037c0c0eb4c55d2df12d98b1d77cf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775115"
---
# <a name="package-versioning"></a><span data-ttu-id="b3020-103">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="b3020-103">Package versioning</span></span>

<span data-ttu-id="b3020-104">特定のパッケージは、常にパッケージ識別子と正確なバージョン番号を使用して参照されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="b3020-105">たとえば、nuget.org の [Entity Framework](https://www.nuget.org/packages/EntityFramework/) には、バージョン *4.1.10311* からバージョン *6.1.3* (最新の安定したリリース) までの数十の特定のパッケージと、*6.2.0-beta1* のようなさまざまなプレリリース バージョンがあります。</span><span class="sxs-lookup"><span data-stu-id="b3020-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="b3020-106">パッケージの作成時に、オプションのプレリリース テキスト サフィックスを使用して特定のバージョン番号を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="b3020-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="b3020-107">一方、パッケージを使用するときには、正確なバージョン番号または許容されるバージョンの範囲のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b3020-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="b3020-108">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="b3020-108">In this topic:</span></span>

- <span data-ttu-id="b3020-109">プレリリース サフィックスを含む[バージョンの基本](#version-basics)。</span><span class="sxs-lookup"><span data-stu-id="b3020-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="b3020-110">バージョン範囲</span><span class="sxs-lookup"><span data-stu-id="b3020-110">Version ranges</span></span>](#version-ranges)
- [<span data-ttu-id="b3020-111">正規化されたバージョン番号</span><span class="sxs-lookup"><span data-stu-id="b3020-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="b3020-112">バージョンの基本</span><span class="sxs-lookup"><span data-stu-id="b3020-112">Version basics</span></span>

<span data-ttu-id="b3020-113">特定のバージョン番号は、*Major.Minor.Patch[-Suffix]* という形式になっています。ここで、各構成要素には次の意味があります。</span><span class="sxs-lookup"><span data-stu-id="b3020-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="b3020-114">*Major*:互換性に影響する変更</span><span class="sxs-lookup"><span data-stu-id="b3020-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="b3020-115">*Minor*: 新機能、ただし下位互換性あり</span><span class="sxs-lookup"><span data-stu-id="b3020-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="b3020-116">*Patch*: 下位互換性のバグ修正のみ</span><span class="sxs-lookup"><span data-stu-id="b3020-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="b3020-117">*-Suffix* (省略可能): ハイフンに続けて、プレリリース バージョンを示す文字列 ([セマンティック バージョニングまたは SemVer 1.0 規約](https://semver.org/spec/v1.0.0.html)に従う)。</span><span class="sxs-lookup"><span data-stu-id="b3020-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](https://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="b3020-118">**例:**</span><span class="sxs-lookup"><span data-stu-id="b3020-118">**Examples:**</span></span>

```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="b3020-119">nuget.org では、正確なバージョン番号がないパッケージのアップロードがすべて拒否されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="b3020-120">バージョンは、`.nuspec` 内またはパッケージの作成に使用されるプロジェクト ファイル内で指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b3020-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="b3020-121">プレリリース バージョン</span><span class="sxs-lookup"><span data-stu-id="b3020-121">Pre-release versions</span></span>

<span data-ttu-id="b3020-122">技術的に言えば、パッケージの作成者は、任意の文字列をサフィックスとして使用してプレリリース バージョンを示すことができます。これは、NuGet ではそのようなバージョンがプレリリースとして扱われ、他の解釈は行われないためです。</span><span class="sxs-lookup"><span data-stu-id="b3020-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="b3020-123">つまり、NuGet では、関係する UI に完全なバージョン文字列が表示され、サフィックスの意味の解釈はコンシューマーに委ねられます。</span><span class="sxs-lookup"><span data-stu-id="b3020-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="b3020-124">つまり、パッケージ開発者は一般に、認識されている名前付け規則に従います。</span><span class="sxs-lookup"><span data-stu-id="b3020-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="b3020-125">`-alpha`:アルファ リリース。一般的に、進行中の製品または実験に使用されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="b3020-126">`-beta`: ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b3020-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="b3020-127">`-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。</span><span class="sxs-lookup"><span data-stu-id="b3020-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="b3020-128">NuGet 4.3.0 以降では、*1.0.1-build.23* のように、ドット表記のプレリリース番号をサポートする [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html) がサポートされます。</span><span class="sxs-lookup"><span data-stu-id="b3020-128">NuGet 4.3.0+ supports [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="b3020-129">ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b3020-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="b3020-130">*1.0.1-build23* のような形式を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b3020-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="b3020-131">パッケージ参照を解決するときに、複数のパッケージ バージョンのサフィックスだけが異なる場合、NuGet ではサフィックスのないバージョンが最初に選択され、プレリリース バージョンにアルファベットの逆順の優先順位が適用されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="b3020-132">たとえば、以下のバージョンは、示されているとおりの順序で選択されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-132">For example, the following versions would be chosen in the exact order shown:</span></span>

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a><span data-ttu-id="b3020-133">セマンティック バージョニング 2.0.0</span><span class="sxs-lookup"><span data-stu-id="b3020-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="b3020-134">NuGet 4.3.0 以降と Visual Studio 2017 バージョン 15.3 以降では、NuGet によって[セマンティック バージョニング 2.0.0](https://semver.org/spec/v2.0.0.html) がサポートされます。</span><span class="sxs-lookup"><span data-stu-id="b3020-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](https://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="b3020-135">SemVer v2.0.0 の特定のセマンティクスは、以前のクライアントではサポートされません。</span><span class="sxs-lookup"><span data-stu-id="b3020-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="b3020-136">NuGet では、次のいずれかの文が真の場合に、パッケージ バージョンが SemVer v2.0.0 に固有であると見なされます。</span><span class="sxs-lookup"><span data-stu-id="b3020-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="b3020-137">プレリリース ラベルがドットで区切られている (例: *1.0.0-alpha.1*)</span><span class="sxs-lookup"><span data-stu-id="b3020-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="b3020-138">バージョンにビルド メタデータが含まれている (例: *1.0.0+githash*)</span><span class="sxs-lookup"><span data-stu-id="b3020-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="b3020-139">nuget.org では、次のいずれかの文が真の場合に、パッケージが SemVer v2.0.0 パッケージとして定義されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="b3020-140">パッケージの独自のバージョンが上で定義されている SemVer v2.0.0 に準拠しているが、SemVer v1.0.0 には準拠していない。</span><span class="sxs-lookup"><span data-stu-id="b3020-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="b3020-141">パッケージの依存関係のバージョン範囲のいずれかの最小または最大バージョンが上で定義されている SemVer v2.0.0 に準拠しているが、SemVer v1.0.0 には準拠していない (例: *[1.0.0-alpha.1, )* )。</span><span class="sxs-lookup"><span data-stu-id="b3020-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="b3020-142">SemVer v2.0.0 固有のパッケージを nuget.org にアップロードした場合、パッケージは以前のクライアントでは非表示になり、以下の NuGet クライアントでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="b3020-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="b3020-143">NuGet 4.3.0 以降</span><span class="sxs-lookup"><span data-stu-id="b3020-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="b3020-144">Visual Studio 2017 バージョン 15.3 以降</span><span class="sxs-lookup"><span data-stu-id="b3020-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="b3020-145">Visual Studio 2015 と [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="b3020-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="b3020-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="b3020-146">dotnet</span></span>
  - <span data-ttu-id="b3020-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="b3020-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="b3020-148">サード パーティ製クライアント:</span><span class="sxs-lookup"><span data-stu-id="b3020-148">Third-party clients:</span></span>

- <span data-ttu-id="b3020-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="b3020-149">JetBrains Rider</span></span>
- <span data-ttu-id="b3020-150">Paket バージョン 5.0 以降</span><span class="sxs-lookup"><span data-stu-id="b3020-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a><span data-ttu-id="b3020-151">バージョン範囲</span><span class="sxs-lookup"><span data-stu-id="b3020-151">Version ranges</span></span>

<span data-ttu-id="b3020-152">パッケージの依存関係を参照する場合、以下にまとめるように、NuGet ではバージョン範囲を指定するために間隔表記の使用がサポートされます。</span><span class="sxs-lookup"><span data-stu-id="b3020-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="b3020-153">Notation</span><span class="sxs-lookup"><span data-stu-id="b3020-153">Notation</span></span> | <span data-ttu-id="b3020-154">適用されるルール</span><span class="sxs-lookup"><span data-stu-id="b3020-154">Applied rule</span></span> | <span data-ttu-id="b3020-155">説明</span><span class="sxs-lookup"><span data-stu-id="b3020-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="b3020-156">1</span><span class="sxs-lookup"><span data-stu-id="b3020-156">1.0</span></span> | <span data-ttu-id="b3020-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-157">x ≥ 1.0</span></span> | <span data-ttu-id="b3020-158">最小バージョン (示されている値を含む)</span><span class="sxs-lookup"><span data-stu-id="b3020-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="b3020-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="b3020-159">(1.0,)</span></span> | <span data-ttu-id="b3020-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-160">x > 1.0</span></span> | <span data-ttu-id="b3020-161">最小バージョン (示されている値を含まない)</span><span class="sxs-lookup"><span data-stu-id="b3020-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="b3020-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="b3020-162">[1.0]</span></span> | <span data-ttu-id="b3020-163">x == 1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-163">x == 1.0</span></span> | <span data-ttu-id="b3020-164">正確なバージョンの一致</span><span class="sxs-lookup"><span data-stu-id="b3020-164">Exact version match</span></span> |
| <span data-ttu-id="b3020-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="b3020-165">(,1.0]</span></span> | <span data-ttu-id="b3020-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-166">x ≤ 1.0</span></span> | <span data-ttu-id="b3020-167">最大バージョン (示されている値を含む)</span><span class="sxs-lookup"><span data-stu-id="b3020-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="b3020-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="b3020-168">(,1.0)</span></span> | <span data-ttu-id="b3020-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-169">x < 1.0</span></span> | <span data-ttu-id="b3020-170">最大バージョン (示されている値を含まない)</span><span class="sxs-lookup"><span data-stu-id="b3020-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="b3020-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="b3020-171">[1.0,2.0]</span></span> | <span data-ttu-id="b3020-172">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="b3020-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="b3020-173">正確な範囲 (示されている値を含む)</span><span class="sxs-lookup"><span data-stu-id="b3020-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="b3020-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b3020-174">(1.0,2.0)</span></span> | <span data-ttu-id="b3020-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b3020-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="b3020-176">正確な範囲 (示されている値を含まない)</span><span class="sxs-lookup"><span data-stu-id="b3020-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="b3020-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b3020-177">[1.0,2.0)</span></span> | <span data-ttu-id="b3020-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b3020-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="b3020-179">示されている値を含む最小バージョンと示されている値を含まない最大バージョンの組み合わせ</span><span class="sxs-lookup"><span data-stu-id="b3020-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="b3020-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="b3020-180">(1.0)</span></span>    | <span data-ttu-id="b3020-181">無効な</span><span class="sxs-lookup"><span data-stu-id="b3020-181">invalid</span></span> | <span data-ttu-id="b3020-182">無効な</span><span class="sxs-lookup"><span data-stu-id="b3020-182">invalid</span></span> |

<span data-ttu-id="b3020-183">PackageReference 形式を使用する場合、NuGet では、番号の Major、Minor、Patch、およびプレリリース サフィックス部分に浮動小数点表記 \* を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b3020-183">When using the PackageReference format, NuGet also supports using a floating notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="b3020-184">`packages.config` 形式では、浮動小数点バージョンはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b3020-184">Floating versions are not supported with the `packages.config` format.</span></span> <span data-ttu-id="b3020-185">浮動バージョンを指定した場合、バージョンの説明に一致する既存の最高バージョンに解決されるというルールになります。</span><span class="sxs-lookup"><span data-stu-id="b3020-185">When a floating version is specified, the rule is to resolve to the highest existent version that matches the version description.</span></span> <span data-ttu-id="b3020-186">次に、浮動バージョンと解決の例を示します。</span><span class="sxs-lookup"><span data-stu-id="b3020-186">Examples of floating versions and the resolutions are below.</span></span>

> [!Note]
> <span data-ttu-id="b3020-187">PackageReference のバージョン範囲には、プレリリース バージョンが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b3020-187">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="b3020-188">仕様により、浮動バージョンでは、オプトインしない限りプレリリース バージョンは解決されません。</span><span class="sxs-lookup"><span data-stu-id="b3020-188">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="b3020-189">関連する機能要求の状態については、[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297) に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="b3020-189">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="b3020-190">例</span><span class="sxs-lookup"><span data-stu-id="b3020-190">Examples</span></span>

<span data-ttu-id="b3020-191">プロジェクト ファイル、`packages.config` ファイル、`.nuspec` ファイル内では、パッケージの依存関係のバージョンまたはバージョン範囲を必ず指定します。</span><span class="sxs-lookup"><span data-stu-id="b3020-191">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="b3020-192">バージョンまたはバージョン範囲を指定しない場合、NuGet 2.8.x 以前では依存関係を解決するときに利用可能な最新のパッケージ バージョンが選択されますが、NuGet 3.x 以降ではパッケージの最小バージョンが選択されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-192">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="b3020-193">バージョンまたはバージョン範囲を指定すると、この不確実性が回避されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-193">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="b3020-194">プロジェクト ファイル内の参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="b3020-194">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version.
     Will resolve to the highest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. 
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. 
     Will resolve to the smallest acceptable stable version.
     -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher.
     Will resolve to the smallest acceptable stable version.-->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher.
     Will resolve to the smallest acceptable stable version. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

#### <a name="floating-version-resolutions"></a><span data-ttu-id="b3020-195">浮動バージョンの解決</span><span class="sxs-lookup"><span data-stu-id="b3020-195">Floating version resolutions</span></span> 

| <span data-ttu-id="b3020-196">Version</span><span class="sxs-lookup"><span data-stu-id="b3020-196">Version</span></span> | <span data-ttu-id="b3020-197">サーバーに存在するバージョン</span><span class="sxs-lookup"><span data-stu-id="b3020-197">Versions present on server</span></span> | <span data-ttu-id="b3020-198">解決方法</span><span class="sxs-lookup"><span data-stu-id="b3020-198">Resolution</span></span> | <span data-ttu-id="b3020-199">理由</span><span class="sxs-lookup"><span data-stu-id="b3020-199">Reason</span></span> | <span data-ttu-id="b3020-200">メモ</span><span class="sxs-lookup"><span data-stu-id="b3020-200">Notes</span></span> |
|----------|--------------|-------------|-------------|-------------|
| * | <span data-ttu-id="b3020-201">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-201">1.1.0</span></span> <br> <span data-ttu-id="b3020-202">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3020-202">1.1.1</span></span> <br> <span data-ttu-id="b3020-203">1.2.0</span><span class="sxs-lookup"><span data-stu-id="b3020-203">1.2.0</span></span> <br> <span data-ttu-id="b3020-204">1.3.0-alpha</span><span class="sxs-lookup"><span data-stu-id="b3020-204">1.3.0-alpha</span></span>  | <span data-ttu-id="b3020-205">1.2.0</span><span class="sxs-lookup"><span data-stu-id="b3020-205">1.2.0</span></span> | <span data-ttu-id="b3020-206">最も高い安定バージョン。</span><span class="sxs-lookup"><span data-stu-id="b3020-206">The highest stable version.</span></span> |
| <span data-ttu-id="b3020-207">1.1.\*</span><span class="sxs-lookup"><span data-stu-id="b3020-207">1.1.\*</span></span> | <span data-ttu-id="b3020-208">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-208">1.1.0</span></span> <br> <span data-ttu-id="b3020-209">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3020-209">1.1.1</span></span> <br> <span data-ttu-id="b3020-210">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="b3020-210">1.1.2-alpha</span></span> <br> <span data-ttu-id="b3020-211">1.2.0-alpha</span><span class="sxs-lookup"><span data-stu-id="b3020-211">1.2.0-alpha</span></span> | <span data-ttu-id="b3020-212">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3020-212">1.1.1</span></span> | <span data-ttu-id="b3020-213">指定したパターンに従う最も高い安定バージョン。</span><span class="sxs-lookup"><span data-stu-id="b3020-213">The highest stable version that respects the specified pattern.</span></span>|
| <span data-ttu-id="b3020-214">\* - \*</span><span class="sxs-lookup"><span data-stu-id="b3020-214">\* - \*</span></span> | <span data-ttu-id="b3020-215">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-215">1.1.0</span></span> <br> <span data-ttu-id="b3020-216">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3020-216">1.1.1</span></span> <br> <span data-ttu-id="b3020-217">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="b3020-217">1.1.2-alpha</span></span> <br> <span data-ttu-id="b3020-218">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="b3020-218">1.3.0-beta</span></span>  | <span data-ttu-id="b3020-219">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="b3020-219">1.3.0-beta</span></span> | <span data-ttu-id="b3020-220">安定していないバージョンも含めた、最も高いバージョン。</span><span class="sxs-lookup"><span data-stu-id="b3020-220">The highest version including the not stable versions.</span></span> | <span data-ttu-id="b3020-221">Visual Studio バージョン 16.6、NuGet バージョン 5.6、.NET Core SDK バージョン 3.1.300 で使用可能。</span><span class="sxs-lookup"><span data-stu-id="b3020-221">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |
| <span data-ttu-id="b3020-222">1.1.\* - \*</span><span class="sxs-lookup"><span data-stu-id="b3020-222">1.1.\* - \*</span></span> | <span data-ttu-id="b3020-223">1.1.0</span><span class="sxs-lookup"><span data-stu-id="b3020-223">1.1.0</span></span> <br> <span data-ttu-id="b3020-224">1.1.1</span><span class="sxs-lookup"><span data-stu-id="b3020-224">1.1.1</span></span> <br> <span data-ttu-id="b3020-225">1.1.2-alpha</span><span class="sxs-lookup"><span data-stu-id="b3020-225">1.1.2-alpha</span></span> <br> <span data-ttu-id="b3020-226">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="b3020-226">1.1.2-beta</span></span> <br> <span data-ttu-id="b3020-227">1.3.0-beta</span><span class="sxs-lookup"><span data-stu-id="b3020-227">1.3.0-beta</span></span>  | <span data-ttu-id="b3020-228">1.1.2-beta</span><span class="sxs-lookup"><span data-stu-id="b3020-228">1.1.2-beta</span></span> | <span data-ttu-id="b3020-229">安定していないバージョンも含めて、パターンに従う最も高いバージョン。</span><span class="sxs-lookup"><span data-stu-id="b3020-229">The highest version respecting the pattern and including the not stable versions.</span></span> | <span data-ttu-id="b3020-230">Visual Studio バージョン 16.6、NuGet バージョン 5.6、.NET Core SDK バージョン 3.1.300 で使用可能。</span><span class="sxs-lookup"><span data-stu-id="b3020-230">Available in Visual Studio version 16.6, NuGet version 5.6, .NET Core SDK version 3.1.300</span></span> |

<span data-ttu-id="b3020-231">**`packages.config` 内の参照**:</span><span class="sxs-lookup"><span data-stu-id="b3020-231">**References in `packages.config`:**</span></span>

<span data-ttu-id="b3020-232">`packages.config` では、すべての依存関係が、パッケージの復元時に使用される正確な `version` 属性と共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-232">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="b3020-233">`allowedVersions` 属性は、パッケージの更新先にできるバージョンを制限するために、更新操作中にのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-233">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

<span data-ttu-id="b3020-234">**`.nuspec` ファイル内の参照**</span><span class="sxs-lookup"><span data-stu-id="b3020-234">**References in `.nuspec` files**</span></span>

<span data-ttu-id="b3020-235">`<dependency>` 要素内の `version` 属性は、依存関係で許容される範囲のバージョンを示します。</span><span class="sxs-lookup"><span data-stu-id="b3020-235">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a><span data-ttu-id="b3020-236">正規化されたバージョン番号</span><span class="sxs-lookup"><span data-stu-id="b3020-236">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="b3020-237">これは、NuGet 3.4 以降での破壊的変更です。</span><span class="sxs-lookup"><span data-stu-id="b3020-237">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="b3020-238">インストール、再インストール、または復元操作中にリポジトリからパッケージを取得すると、NuGet 3.4 以降ではバージョン番号が次のように扱われます。</span><span class="sxs-lookup"><span data-stu-id="b3020-238">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="b3020-239">先頭のゼロはバージョン番号から削除されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-239">Leading zeroes are removed from version numbers:</span></span>

  <span data-ttu-id="b3020-240">1.00 は 1.0、1.01.1 は 1.1.1、1.00.0.1 は 1.0.0.1 として扱われます</span><span class="sxs-lookup"><span data-stu-id="b3020-240">1.00 is treated as 1.0 1.01.1 is treated as 1.1.1 1.00.0.1 is treated as 1.0.0.1</span></span>

- <span data-ttu-id="b3020-241">バージョン番号の 4 番目の部分のゼロは省略されます</span><span class="sxs-lookup"><span data-stu-id="b3020-241">A zero in the fourth part of the version number will be omitted</span></span>

  <span data-ttu-id="b3020-242">1.0.0.0 は 1.0.0、1.0.01.0 は 1.0.1 として扱われます</span><span class="sxs-lookup"><span data-stu-id="b3020-242">1.0.0.0 is treated as 1.0.0 1.0.01.0 is treated as 1.0.1</span></span>

- <span data-ttu-id="b3020-243">SemVer 2.0.0 ビルド メタデータは削除されます</span><span class="sxs-lookup"><span data-stu-id="b3020-243">SemVer 2.0.0 build metadata is removed</span></span>

  <span data-ttu-id="b3020-244">1.0.7+r3456 は 1.0.7 として扱われます</span><span class="sxs-lookup"><span data-stu-id="b3020-244">1.0.7+r3456 is treated as 1.0.7</span></span>

<span data-ttu-id="b3020-245">`pack` 操作と `restore` 操作では、可能な限りバージョンが正規化されます。</span><span class="sxs-lookup"><span data-stu-id="b3020-245">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="b3020-246">既にビルドされているパッケージの場合、この正規化はパッケージ自体のバージョン番号には影響しません。依存関係を解決するときに NuGet によってバージョンが照合される方法にのみ影響します。</span><span class="sxs-lookup"><span data-stu-id="b3020-246">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="b3020-247">ただし、NuGet パッケージ リポジトリでは、これらの値を NuGet と同じように処理して、パッケージのバージョンが重複しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b3020-247">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="b3020-248">したがって、パッケージのバージョン *1.0* を含むリポジトリでは、バージョン *1.0.0* を別の異なるパッケージとしてホストすることはできません。</span><span class="sxs-lookup"><span data-stu-id="b3020-248">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
