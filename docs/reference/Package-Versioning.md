---
title: NuGet パッケージのバージョンの参照
description: バージョン番号、およびその他のパッケージ、依存する NuGet パッケージと依存関係をインストールする方法の範囲を指定する方法の詳細。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549774"
---
# <a name="package-versioning"></a><span data-ttu-id="0359e-103">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="0359e-103">Package versioning</span></span>

<span data-ttu-id="0359e-104">特定のパッケージは、パッケージの識別子と正確なバージョン番号を使用して常に参照されます。</span><span class="sxs-lookup"><span data-stu-id="0359e-104">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="0359e-105">たとえば、 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org ではいくつか数十特定使用可能なパッケージをバージョンからまで*4.1.10311*バージョン*6.1.3* (、最新の安定しました。リリース) などのさまざまなリリース前バージョンと*6.2.0-beta1*します。</span><span class="sxs-lookup"><span data-stu-id="0359e-105">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="0359e-106">パッケージを作成する場合は、省略可能なプレリリース テキスト サフィックスを含む特定のバージョン番号を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="0359e-106">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="0359e-107">その一方で、パッケージを利用する場合は、正確なバージョン番号または許容可能なバージョンの範囲のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="0359e-107">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="0359e-108">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="0359e-108">In this topic:</span></span>

- <span data-ttu-id="0359e-109">[バージョンの基本](#version-basics)プレリリースのサフィックスを含むです。</span><span class="sxs-lookup"><span data-stu-id="0359e-109">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="0359e-110">バージョン範囲およびワイルドカード</span><span class="sxs-lookup"><span data-stu-id="0359e-110">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="0359e-111">正規化されたバージョン番号</span><span class="sxs-lookup"><span data-stu-id="0359e-111">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="0359e-112">バージョンの基本</span><span class="sxs-lookup"><span data-stu-id="0359e-112">Version basics</span></span>

<span data-ttu-id="0359e-113">特定のバージョン番号が、 *Major.Minor.Patch [-サフィックス]* コンポーネントは次の意味。</span><span class="sxs-lookup"><span data-stu-id="0359e-113">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="0359e-114">*主要な*: 重大な変更</span><span class="sxs-lookup"><span data-stu-id="0359e-114">*Major*: Breaking changes</span></span>
- <span data-ttu-id="0359e-115">*マイナー*: 下位互換性がありますが、新機能</span><span class="sxs-lookup"><span data-stu-id="0359e-115">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="0359e-116">*パッチ*: 下位互換性のバグ修正のみ</span><span class="sxs-lookup"><span data-stu-id="0359e-116">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="0359e-117">*-サフィックス*(省略可能): ハイフンが続けてリリース前のバージョンを示す文字列 (以下、[セマンティック バージョン管理または SemVer 1.0 規則](http://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="0359e-117">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="0359e-118">**例:**</span><span class="sxs-lookup"><span data-stu-id="0359e-118">**Examples:**</span></span>

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> <span data-ttu-id="0359e-119">nuget.org では、正確なバージョン番号が不足しているパッケージのアップロードを拒否します。</span><span class="sxs-lookup"><span data-stu-id="0359e-119">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="0359e-120">バージョンを指定する必要があります、`.nuspec`またはプロジェクト ファイルのパッケージを作成するために使用します。</span><span class="sxs-lookup"><span data-stu-id="0359e-120">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="0359e-121">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="0359e-121">Pre-release versions</span></span>

<span data-ttu-id="0359e-122">厳密に言うと、パッケージ作成者は任意の文字列をサフィックスとして使用を NuGet がこのような任意のバージョンをプレリリースとして扱います、他の解釈も負わないものとは、リリース前のバージョンを示すためにします。</span><span class="sxs-lookup"><span data-stu-id="0359e-122">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="0359e-123">つまり、すべての UI で、完全なバージョンの文字列、NuGet が表示されますが関係しているコンシューマーにサフィックスの意味の解釈を離れること。</span><span class="sxs-lookup"><span data-stu-id="0359e-123">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="0359e-124">ただし、通常、パッケージの開発者に、認識されている名前付け規則。</span><span class="sxs-lookup"><span data-stu-id="0359e-124">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="0359e-125">`-alpha`: アルファ リリース、通常処理中や実験に使用します。</span><span class="sxs-lookup"><span data-stu-id="0359e-125">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="0359e-126">`-beta`: ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0359e-126">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="0359e-127">`-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。</span><span class="sxs-lookup"><span data-stu-id="0359e-127">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="0359e-128">NuGet 4.3.0 サポート[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)とプレリリース番号をドット表記をサポートする*1.0.1-build.23*します。</span><span class="sxs-lookup"><span data-stu-id="0359e-128">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="0359e-129">ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="0359e-129">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="0359e-130">ようなフォームを使用して*1.0.1-build23*します。</span><span class="sxs-lookup"><span data-stu-id="0359e-130">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="0359e-131">パッケージ参照と複数のパッケージ バージョンのみが異なるサフィックスを解決するには、NuGet は最初に、サフィックスが付いていないバージョンを選択し、アルファベットの逆順のプレリリース版に優先順位を適用します。</span><span class="sxs-lookup"><span data-stu-id="0359e-131">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="0359e-132">たとえば、次のバージョンが示されている正確な順序で選択されます。</span><span class="sxs-lookup"><span data-stu-id="0359e-132">For example, the following versions would be chosen in the exact order shown:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a><span data-ttu-id="0359e-133">セマンティック バージョニング 2.0.0</span><span class="sxs-lookup"><span data-stu-id="0359e-133">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="0359e-134">NuGet 4.3.0 と Visual Studio 2017 バージョン 15.3 以降、NuGet をサポート[セマンティック バージョニング 2.0.0](http://semver.org/spec/v2.0.0.html)します。</span><span class="sxs-lookup"><span data-stu-id="0359e-134">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="0359e-135">以前のクライアントでは、SemVer v2.0.0 の特定のセマンティクスはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="0359e-135">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="0359e-136">NuGet では、次のステートメントのいずれかが true の場合、SemVer v2.0.0 を特定するパッケージのバージョンと見なされます。</span><span class="sxs-lookup"><span data-stu-id="0359e-136">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="0359e-137">プレリリース版は、ラベルはドットで区切られた、たとえば、 *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="0359e-137">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="0359e-138">バージョンは、ビルド メタデータ、たとえば、 *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="0359e-138">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="0359e-139">Nuget.org の場合、次のステートメントのいずれかが true の場合、パッケージは SemVer v2.0.0 パッケージとして定義されます。</span><span class="sxs-lookup"><span data-stu-id="0359e-139">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="0359e-140">パッケージのバージョンでは、上記で定義された SemVer v2.0.0 の準拠が準拠していない SemVer v1.0.0 です。</span><span class="sxs-lookup"><span data-stu-id="0359e-140">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="0359e-141">パッケージの依存関係のバージョン範囲には SemVer v2.0.0 の準拠が準拠していない SemVer v1.0.0; 上で定義した、最小値または最大バージョンたとえば、 *[1.0.0-alpha.1,)* します。</span><span class="sxs-lookup"><span data-stu-id="0359e-141">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="0359e-142">SemVer v2.0.0 固有のパッケージを nuget.org にアップロードする場合、パッケージは、以前のクライアントを非表示と次の NuGet クライアントのみに使用可能なは。</span><span class="sxs-lookup"><span data-stu-id="0359e-142">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="0359e-143">NuGet 4.3.0</span><span class="sxs-lookup"><span data-stu-id="0359e-143">NuGet 4.3.0+</span></span>
- <span data-ttu-id="0359e-144">Visual Studio 2017 バージョン 15.3 以降</span><span class="sxs-lookup"><span data-stu-id="0359e-144">Visual Studio 2017 version 15.3+</span></span>
- <span data-ttu-id="0359e-145">Visual Studio 2015 と[NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span><span class="sxs-lookup"><span data-stu-id="0359e-145">Visual Studio 2015 with [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)</span></span>
- <span data-ttu-id="0359e-146">dotnet</span><span class="sxs-lookup"><span data-stu-id="0359e-146">dotnet</span></span>
  - <span data-ttu-id="0359e-147">dotnetcore.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="0359e-147">dotnetcore.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="0359e-148">サード パーティ製のクライアント:</span><span class="sxs-lookup"><span data-stu-id="0359e-148">Third-party clients:</span></span>

- <span data-ttu-id="0359e-149">JetBrains Rider</span><span class="sxs-lookup"><span data-stu-id="0359e-149">JetBrains Rider</span></span>
- <span data-ttu-id="0359e-150">バージョン 5.0 以降のパケットを作成します。</span><span class="sxs-lookup"><span data-stu-id="0359e-150">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="0359e-151">バージョン範囲およびワイルドカード</span><span class="sxs-lookup"><span data-stu-id="0359e-151">Version ranges and wildcards</span></span>

<span data-ttu-id="0359e-152">パッケージの依存関係を参照する、NuGet では、次のとおり、バージョン範囲を指定する間隔の表記を使用してサポートしています。</span><span class="sxs-lookup"><span data-stu-id="0359e-152">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="0359e-153">Notation</span><span class="sxs-lookup"><span data-stu-id="0359e-153">Notation</span></span> | <span data-ttu-id="0359e-154">適用されるルール</span><span class="sxs-lookup"><span data-stu-id="0359e-154">Applied rule</span></span> | <span data-ttu-id="0359e-155">説明</span><span class="sxs-lookup"><span data-stu-id="0359e-155">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="0359e-156">1</span><span class="sxs-lookup"><span data-stu-id="0359e-156">1.0</span></span> | <span data-ttu-id="0359e-157">x ≥ 1.0</span><span class="sxs-lookup"><span data-stu-id="0359e-157">x ≥ 1.0</span></span> | <span data-ttu-id="0359e-158">包括的な最小のバージョン</span><span class="sxs-lookup"><span data-stu-id="0359e-158">Minimum version, inclusive</span></span> |
| <span data-ttu-id="0359e-159">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="0359e-159">(1.0,)</span></span> | <span data-ttu-id="0359e-160">x > 1.0</span><span class="sxs-lookup"><span data-stu-id="0359e-160">x > 1.0</span></span> | <span data-ttu-id="0359e-161">排他の最小バージョン</span><span class="sxs-lookup"><span data-stu-id="0359e-161">Minimum version, exclusive</span></span> |
| <span data-ttu-id="0359e-162">[1.0]</span><span class="sxs-lookup"><span data-stu-id="0359e-162">[1.0]</span></span> | <span data-ttu-id="0359e-163">x = 1.0</span><span class="sxs-lookup"><span data-stu-id="0359e-163">x == 1.0</span></span> | <span data-ttu-id="0359e-164">バージョンに一致します。</span><span class="sxs-lookup"><span data-stu-id="0359e-164">Exact version match</span></span> |
| <span data-ttu-id="0359e-165">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="0359e-165">(,1.0]</span></span> | <span data-ttu-id="0359e-166">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="0359e-166">x ≤ 1.0</span></span> | <span data-ttu-id="0359e-167">包括の最大バージョン</span><span class="sxs-lookup"><span data-stu-id="0359e-167">Maximum version, inclusive</span></span> |
| <span data-ttu-id="0359e-168">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="0359e-168">(,1.0)</span></span> | <span data-ttu-id="0359e-169">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="0359e-169">x < 1.0</span></span> | <span data-ttu-id="0359e-170">排他の最大バージョン</span><span class="sxs-lookup"><span data-stu-id="0359e-170">Maximum version, exclusive</span></span> |
| <span data-ttu-id="0359e-171">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="0359e-171">[1.0,2.0]</span></span> | <span data-ttu-id="0359e-172">1.0 ≤ ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="0359e-172">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="0359e-173">正確な範囲は、包含</span><span class="sxs-lookup"><span data-stu-id="0359e-173">Exact range, inclusive</span></span> |
| <span data-ttu-id="0359e-174">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="0359e-174">(1.0,2.0)</span></span> | <span data-ttu-id="0359e-175">1.0 < x < 2.0</span><span class="sxs-lookup"><span data-stu-id="0359e-175">1.0 < x < 2.0</span></span> | <span data-ttu-id="0359e-176">正確な範囲は、排他的</span><span class="sxs-lookup"><span data-stu-id="0359e-176">Exact range, exclusive</span></span> |
| <span data-ttu-id="0359e-177">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="0359e-177">[1.0,2.0)</span></span> | <span data-ttu-id="0359e-178">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="0359e-178">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="0359e-179">包括的な最小値と排他最大バージョンが混在</span><span class="sxs-lookup"><span data-stu-id="0359e-179">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="0359e-180">(1.0)</span><span class="sxs-lookup"><span data-stu-id="0359e-180">(1.0)</span></span>    | <span data-ttu-id="0359e-181">無効な</span><span class="sxs-lookup"><span data-stu-id="0359e-181">invalid</span></span> | <span data-ttu-id="0359e-182">無効な</span><span class="sxs-lookup"><span data-stu-id="0359e-182">invalid</span></span> |

<span data-ttu-id="0359e-183">PackageReference 形式を使用して、NuGet もサポートしています、ワイルドカードの表記を使用して\*メジャー、マイナー、パッチ、および、番号のプレリリースのサフィックス部分。</span><span class="sxs-lookup"><span data-stu-id="0359e-183">When using the PackageReference format, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="0359e-184">ワイルドカードはサポートされていません、`packages.config`形式。</span><span class="sxs-lookup"><span data-stu-id="0359e-184">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="0359e-185">バージョン範囲を解決するときに、プレリリース版は含まれません。</span><span class="sxs-lookup"><span data-stu-id="0359e-185">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="0359e-186">プレリリース版*は*ワイルドカードを使用する場合に含まれる (\*)。</span><span class="sxs-lookup"><span data-stu-id="0359e-186">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="0359e-187">バージョン範囲 *[1.0,2.0]* などは含まれませんが、2.0 ベータ版、ワイルドカードの表記法_2.0-\*_ は。</span><span class="sxs-lookup"><span data-stu-id="0359e-187">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-\*_ does.</span></span> <span data-ttu-id="0359e-188">参照してください[発行 912](https://github.com/NuGet/Home/issues/912)プレリリース版のワイルドカードの詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="0359e-188">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="0359e-189">使用例</span><span class="sxs-lookup"><span data-stu-id="0359e-189">Examples</span></span>

<span data-ttu-id="0359e-190">常にプロジェクト ファイルで、バージョン、またはパッケージの依存関係のバージョンの範囲を指定`packages.config`ファイル、および`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="0359e-190">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="0359e-191">バージョンまたはバージョン範囲、NuGet を使用せず 2.8.x 以前選択最新バージョンの使用可能なパッケージを依存関係を解決するときに、NuGet 3.x を後で、最小のパッケージ バージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="0359e-191">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="0359e-192">バージョンまたはバージョン範囲がこの不確実性を回避を指定します。</span><span class="sxs-lookup"><span data-stu-id="0359e-192">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="0359e-193">プロジェクト ファイル (PackageReference) の参照</span><span class="sxs-lookup"><span data-stu-id="0359e-193">References in project files (PackageReference)</span></span>

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

<span data-ttu-id="0359e-194">**参照`packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="0359e-194">**References in `packages.config`:**</span></span>

<span data-ttu-id="0359e-195">`packages.config`、すべての依存関係がリストされ、正確な`version`パッケージを復元するときに使用される属性です。</span><span class="sxs-lookup"><span data-stu-id="0359e-195">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="0359e-196">`allowedVersions`属性は、パッケージを更新する可能性があるバージョンを制限する更新操作中にのみ使用します。</span><span class="sxs-lookup"><span data-stu-id="0359e-196">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="0359e-197">**参照`.nuspec`ファイル**</span><span class="sxs-lookup"><span data-stu-id="0359e-197">**References in `.nuspec` files**</span></span>

<span data-ttu-id="0359e-198">`version`属性、`<dependency>`要素には、依存関係として受け入れ可能な範囲のバージョンがについて説明します。</span><span class="sxs-lookup"><span data-stu-id="0359e-198">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="0359e-199">正規化されたバージョン番号</span><span class="sxs-lookup"><span data-stu-id="0359e-199">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="0359e-200">これは、NuGet 3.4 以降の互換性に影響する変更です。</span><span class="sxs-lookup"><span data-stu-id="0359e-200">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="0359e-201">を再インストールまたは復元操作、、のインストール中に、リポジトリからパッケージを取得するときに NuGet 3.4 以降はバージョン番号を、次のように扱われます。</span><span class="sxs-lookup"><span data-stu-id="0359e-201">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="0359e-202">バージョン番号から先頭のゼロは削除されます。</span><span class="sxs-lookup"><span data-stu-id="0359e-202">Leading zeroes are removed from version numbers:</span></span>

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- <span data-ttu-id="0359e-203">バージョン番号の 4 番目の部分のゼロは省略されます。</span><span class="sxs-lookup"><span data-stu-id="0359e-203">A zero in the fourth part of the version number will be omitted</span></span>

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

<span data-ttu-id="0359e-204">この正規化では、パッケージ自体; のバージョン番号には影響しませんこれは、のみ方法 NuGet と一致するバージョンの依存関係を解決するときに影響します。</span><span class="sxs-lookup"><span data-stu-id="0359e-204">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="0359e-205">ただし、NuGet パッケージのリポジトリでは、パッケージのバージョンの重複を防ぐためには、NuGet と同様にこれらの値を扱う必要があります。</span><span class="sxs-lookup"><span data-stu-id="0359e-205">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="0359e-206">バージョンを含むリポジトリしたがって*1.0*パッケージの必要がありますもホストしていないバージョン*1.0.0*独立した別のパッケージとして。</span><span class="sxs-lookup"><span data-stu-id="0359e-206">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
