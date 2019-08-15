---
title: NuGet パッケージバージョンリファレンス
description: NuGet パッケージが依存する他のパッケージのバージョン番号と範囲を指定する方法、および依存関係をインストールする方法について正確に説明します。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020000"
---
# <a name="package-versioning"></a><span data-ttu-id="b7a11-103">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="b7a11-103">Package versioning</span></span>

<span data-ttu-id="b7a11-104">特定のパッケージは、常にパッケージ識別子と正確なバージョン番号を使用して参照されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="b7a11-105">たとえば、nuget.org の[Entity Framework](https://www.nuget.org/packages/EntityFramework/)には、バージョン*4.1.10311*からバージョン*ef6.1.3* (最新の安定したリリース)、 *6.2.0-beta1 などのさまざまなプレリリースバージョンまで、いくつかの特定のパッケージが用意されています。* .</span><span class="sxs-lookup"><span data-stu-id="b7a11-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="b7a11-106">パッケージを作成するときに、オプションのプレリリーステキストサフィックスを使用して特定のバージョン番号を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="b7a11-107">一方、パッケージを使用する場合は、正確なバージョン番号または許容されるバージョンの範囲のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="b7a11-108">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="b7a11-108">In this topic:</span></span>

- <span data-ttu-id="b7a11-109">プレリリースのサフィックスを含む[バージョンの基本](#version-basics)。</span><span class="sxs-lookup"><span data-stu-id="b7a11-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="b7a11-110">バージョン範囲とワイルドカード</span><span class="sxs-lookup"><span data-stu-id="b7a11-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="b7a11-111">正規化されたバージョン番号</span><span class="sxs-lookup"><span data-stu-id="b7a11-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="b7a11-112">バージョンの基本</span><span class="sxs-lookup"><span data-stu-id="b7a11-112">Version basics</span></span>

<span data-ttu-id="b7a11-113">特定のバージョン番号は、Major. *Minor. Patch [-Suffix]* という形式になっています。ここで、コンポーネントには次の意味があります。</span><span class="sxs-lookup"><span data-stu-id="b7a11-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="b7a11-114">*メジャー*:互換性に影響する変更</span><span class="sxs-lookup"><span data-stu-id="b7a11-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="b7a11-115">*マイナー*: 新機能、ただし下位互換性あり</span><span class="sxs-lookup"><span data-stu-id="b7a11-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="b7a11-116">*修正プログラム*: 下位互換性のバグ修正のみ</span><span class="sxs-lookup"><span data-stu-id="b7a11-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="b7a11-117">*-サフィックス*(省略可能): プレリリースバージョンを示す文字列 ([セマンティックバージョン管理または SemVer 1.0 規則](http://semver.org/spec/v1.0.0.html)に従う)。</span><span class="sxs-lookup"><span data-stu-id="b7a11-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="b7a11-118">**使用例:**</span><span class="sxs-lookup"><span data-stu-id="b7a11-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="b7a11-119">nuget.org は、正確なバージョン番号を持たないパッケージのアップロードを拒否します。</span><span class="sxs-lookup"><span data-stu-id="b7a11-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="b7a11-120">バージョンは、パッケージの作成に`.nuspec`使用されるプロジェクトファイルまたはプロジェクトファイルで指定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7a11-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="b7a11-121">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="b7a11-121">Pre-release versions</span></span>

<span data-ttu-id="b7a11-122">技術的に言えば、パッケージ作成者は、任意の文字列をサフィックスとして使用してプレリリースバージョンを示すことができます。これは、NuGet がプレリリースとしてそのようなバージョンを扱い、他の解釈は行わないためです。</span><span class="sxs-lookup"><span data-stu-id="b7a11-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="b7a11-123">つまり、NuGet は、関連する任意の UI に完全なバージョン文字列を表示し、サフィックスの意味をコンシューマーに解釈したままにします。</span><span class="sxs-lookup"><span data-stu-id="b7a11-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="b7a11-124">ただし、通常、パッケージ開発者は、認識されている名前付け規則に従います。</span><span class="sxs-lookup"><span data-stu-id="b7a11-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="b7a11-125">`-alpha` :アルファリリース。通常は、進行中の作業と実験に使用されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="b7a11-126">`-beta` : ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="b7a11-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="b7a11-127">`-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。</span><span class="sxs-lookup"><span data-stu-id="b7a11-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="b7a11-128">NuGet 4.3.0 以降では、\* *1.0.1-build. 23*のように、ドット表記のプレリリース番号をサポートする[semver 2.0.0](http://semver.org/spec/v2.0.0.html)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b7a11-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="b7a11-129">ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b7a11-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="b7a11-130">*Build23*のような形式を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="b7a11-131">パッケージ参照を解決し、複数のパッケージバージョンがサフィックスによってのみ異なる場合は、NuGet によってサフィックスのないバージョンが最初に選択されます。その後、プレリリースバージョンの優先順位はアルファベットの逆順になります。</span><span class="sxs-lookup"><span data-stu-id="b7a11-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="b7a11-132">たとえば、次のバージョンは、正確な順序で選択されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="b7a11-133">セマンティックバージョン管理2.0.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="b7a11-134">NuGet では、nuget 4.3.0 以降と Visual Studio 2017 バージョン 15.3 + を使用して、[セマンティックバージョン管理 2.0.0](http://semver.org/spec/v2.0.0.html)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b7a11-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="b7a11-135">SemVer v 2.0.0 の特定のセマンティクスは、古いクライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b7a11-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="b7a11-136">NuGet では、次のいずれかのステートメントが true の場合、パッケージのバージョンが SemVer v 2.0.0 に限定されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="b7a11-137">プレリリースラベルはドットで区切られています (例: *1.0.0)。 1*</span><span class="sxs-lookup"><span data-stu-id="b7a11-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="b7a11-138">バージョンには、 *1.0.0 + githash*などのビルドメタデータが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7a11-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="b7a11-139">Nuget.org の場合、次のいずれかのステートメントが true の場合、パッケージは SemVer v 2.0.0 パッケージとして定義されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="b7a11-140">パッケージの独自のバージョンは SemVer v 2.0.0 に準拠していますが、前述のように SemVer v 1.0.0 に準拠していません。</span><span class="sxs-lookup"><span data-stu-id="b7a11-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="b7a11-141">パッケージの依存関係のバージョンの範囲には、最小または最大のバージョンがあります。これは、上記で定義されている semver v 2.0.0 に準拠していますが、SemVer v1.0 に準拠していません。たとえば、 *[1.0.0-alpha. 1,)* のようになります。</span><span class="sxs-lookup"><span data-stu-id="b7a11-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="b7a11-142">SemVer v 2.0.0 固有のパッケージを nuget.org にアップロードすると、パッケージは古いクライアントからは見えず、次の NuGet クライアントでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="b7a11-143">NuGet 4.3.0 +</span><span class="sxs-lookup"><span data-stu-id="b7a11-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="b7a11-144">Visual Studio 2017 バージョン 15.3 +</span><span class="sxs-lookup"><span data-stu-id="b7a11-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="b7a11-145">Visual Studio 2015 と[NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="b7a11-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="b7a11-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="b7a11-146">dotnet</span></span>
  - <span data-ttu-id="b7a11-147">dotnetcore .exe (.NET SDK 2.0.0 +)</span><span class="sxs-lookup"><span data-stu-id="b7a11-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="b7a11-148">サードパーティのクライアント:</span><span class="sxs-lookup"><span data-stu-id="b7a11-148">Third-party clients:</span></span>

- <span data-ttu-id="b7a11-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="b7a11-149">JetBrains Rider</span></span>
- <span data-ttu-id="b7a11-150">パケットバージョン5.0 以降</span><span class="sxs-lookup"><span data-stu-id="b7a11-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="b7a11-151">バージョン範囲とワイルドカード</span><span class="sxs-lookup"><span data-stu-id="b7a11-151">Version ranges and wildcards</span></span>

<span data-ttu-id="b7a11-152">パッケージの依存関係を参照する場合、NuGet はバージョン範囲を指定するための間隔表記の使用をサポートしています。次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="b7a11-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="b7a11-153">Notation</span><span class="sxs-lookup"><span data-stu-id="b7a11-153">Notation</span></span> | <span data-ttu-id="b7a11-154">適用されたルール</span><span class="sxs-lookup"><span data-stu-id="b7a11-154">Applied rule</span></span> | <span data-ttu-id="b7a11-155">説明</span><span class="sxs-lookup"><span data-stu-id="b7a11-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="b7a11-156">1</span><span class="sxs-lookup"><span data-stu-id="b7a11-156">1.0</span></span> | <span data-ttu-id="b7a11-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-157">x ≥ 1.0</span></span> | <span data-ttu-id="b7a11-158">最小バージョン (含む)</span><span class="sxs-lookup"><span data-stu-id="b7a11-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="b7a11-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="b7a11-159">(1.0,)</span></span> | <span data-ttu-id="b7a11-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-160">x > 1.0</span></span> | <span data-ttu-id="b7a11-161">最小バージョン、排他</span><span class="sxs-lookup"><span data-stu-id="b7a11-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="b7a11-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="b7a11-162">[1.0]</span></span> | <span data-ttu-id="b7a11-163">x = = 1.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-163">x == 1.0</span></span> | <span data-ttu-id="b7a11-164">正確なバージョンの一致</span><span class="sxs-lookup"><span data-stu-id="b7a11-164">Exact version match</span></span> |
| <span data-ttu-id="b7a11-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="b7a11-165">(,1.0]</span></span> | <span data-ttu-id="b7a11-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-166">x ≤ 1.0</span></span> | <span data-ttu-id="b7a11-167">最大バージョン (含む)</span><span class="sxs-lookup"><span data-stu-id="b7a11-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="b7a11-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="b7a11-168">(,1.0)</span></span> | <span data-ttu-id="b7a11-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-169">x < 1.0</span></span> | <span data-ttu-id="b7a11-170">最大バージョン、排他</span><span class="sxs-lookup"><span data-stu-id="b7a11-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="b7a11-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="b7a11-171">[1.0,2.0]</span></span> | <span data-ttu-id="b7a11-172">1.0 ≤ x ≤2.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="b7a11-173">完全な範囲 (含む)</span><span class="sxs-lookup"><span data-stu-id="b7a11-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="b7a11-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b7a11-174">(1.0,2.0)</span></span> | <span data-ttu-id="b7a11-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="b7a11-176">完全な範囲、排他</span><span class="sxs-lookup"><span data-stu-id="b7a11-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="b7a11-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="b7a11-177">[1.0,2.0)</span></span> | <span data-ttu-id="b7a11-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="b7a11-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="b7a11-179">包括的最小バージョンと排他最大バージョンの混合</span><span class="sxs-lookup"><span data-stu-id="b7a11-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="b7a11-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="b7a11-180">(1.0)</span></span>    | <span data-ttu-id="b7a11-181">無効な</span><span class="sxs-lookup"><span data-stu-id="b7a11-181">invalid</span></span> | <span data-ttu-id="b7a11-182">無効な</span><span class="sxs-lookup"><span data-stu-id="b7a11-182">invalid</span></span> |

<span data-ttu-id="b7a11-183">PackageReference 形式を使用する場合、NuGet では、数字のメジャー \*、マイナー、修正プログラム、およびプレリリースのサフィックス部分に対してワイルドカード表記 () を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="b7a11-184">ワイルドカードは、 `packages.config`形式ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="b7a11-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="b7a11-185">PackageReference のバージョン範囲には、プレリリースバージョンが含まれています。</span><span class="sxs-lookup"><span data-stu-id="b7a11-185">Version ranges in PackageReference include pre-release versions.</span></span> <span data-ttu-id="b7a11-186">仕様により、フローティングバージョンでは、をオプトインしない限り、プレリリースバージョンは解決されません。</span><span class="sxs-lookup"><span data-stu-id="b7a11-186">By design, floating versions do not resolve prerelease versions unless opted into.</span></span> <span data-ttu-id="b7a11-187">関連する機能の要求の状態については、「[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b7a11-187">For the status of the related feature request, see [issue 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297).</span></span>

### <a name="examples"></a><span data-ttu-id="b7a11-188">使用例</span><span class="sxs-lookup"><span data-stu-id="b7a11-188">Examples</span></span>

<span data-ttu-id="b7a11-189">プロジェクトファイル、 `packages.config`ファイル、および`.nuspec`ファイルで、パッケージの依存関係のバージョンまたはバージョンの範囲を常に指定します。</span><span class="sxs-lookup"><span data-stu-id="b7a11-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="b7a11-190">バージョンまたはバージョン範囲を指定しない場合、依存関係を解決するときに NuGet 2.8. x 以前のバージョンで利用可能な最新のパッケージバージョンが選択されます。一方、NuGet 3.x 以降では、パッケージの最小バージョンが選択されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="b7a11-191">バージョンまたはバージョンの範囲を指定すると、この不確実性が回避します。</span><span class="sxs-lookup"><span data-stu-id="b7a11-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="b7a11-192">プロジェクトファイル内の参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="b7a11-192">References in project files (PackageReference)</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="b7a11-193">**参照先`packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="b7a11-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="b7a11-194">で`packages.config`は、すべての依存関係が、 `version`パッケージの復元時に使用される正確な属性と共に一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="b7a11-195">`allowedVersions`属性は、更新操作中にのみ、パッケージが更新される可能性のあるバージョンを制限するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="b7a11-196">**ファイル内`.nuspec`の参照**</span><span class="sxs-lookup"><span data-stu-id="b7a11-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="b7a11-197">`<dependency>`要素`version`の属性は、依存関係で許容される範囲のバージョンを記述します。</span><span class="sxs-lookup"><span data-stu-id="b7a11-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="b7a11-198">正規化されたバージョン番号</span><span class="sxs-lookup"><span data-stu-id="b7a11-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="b7a11-199">これは、NuGet 3.4 以降の互換性に影響する変更点です。</span><span class="sxs-lookup"><span data-stu-id="b7a11-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="b7a11-200">インストール、再インストール、または復元操作中にリポジトリからパッケージを取得すると、NuGet 3.4 以降ではバージョン番号が次のように処理されるようになります。</span><span class="sxs-lookup"><span data-stu-id="b7a11-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="b7a11-201">先頭の0は、バージョン番号から削除されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-201">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="b7a11-202">バージョン番号の4番目の部分のゼロは省略されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-202">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="b7a11-203">`pack`および`restore`操作では、可能な限りバージョンが正規化されます。</span><span class="sxs-lookup"><span data-stu-id="b7a11-203">`pack` and `restore` operations normalize versions whenever possible.</span></span> <span data-ttu-id="b7a11-204">既にビルドされているパッケージの場合、この正規化はパッケージ自体のバージョン番号には影響しません。依存関係を解決するときに NuGet がバージョンと一致する方法にのみ影響します。</span><span class="sxs-lookup"><span data-stu-id="b7a11-204">For packages already built, this normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="b7a11-205">ただし、NuGet パッケージリポジトリでは、これらの値を NuGet と同じように処理して、パッケージのバージョンが重複しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="b7a11-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="b7a11-206">したがって、パッケージのバージョン*1.0*を含むリポジトリでは、バージョン*1.0.0*を別のパッケージとしてホストすることはできません。</span><span class="sxs-lookup"><span data-stu-id="b7a11-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
