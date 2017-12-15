---
title: "NuGet パッケージのバージョンのリファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee3c826-dd3a-4fa9-863f-1fd80bc4230f
description: "バージョン番号と NuGet パッケージ、依存しているとの依存関係がどのようにインストールするのには、他のパッケージの範囲を指定する方法の詳細。"
keywords: "バージョン管理、NuGet パッケージの依存関係、NuGet の依存関係のバージョン、NuGet のバージョン番号、NuGet パッケージのバージョン、バージョン範囲、バージョン指定、正規化されたバージョン番号"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 25b74ab629cab0fff7114bf1621606de5fc18dd2
ms.sourcegitcommit: 89bb9d429c19ff69084c35acad09daea3e16d56b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-versioning"></a><span data-ttu-id="fa7c9-104">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="fa7c9-104">Package versioning</span></span>

<span data-ttu-id="fa7c9-105">特定のパッケージは常に、そのパッケージの識別子と厳密なバージョン番号を使用する参照します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-105">A specific package is always referred to using its package identifier and an exact version number.</span></span> <span data-ttu-id="fa7c9-106">たとえば、 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org がいくつか十特定使用可能なパッケージをバージョンからまで*4.1.10311*バージョン*6.1.3* (、最新の安定しました。リリース) などのさまざまなリリース前のバージョンおよび*6.2.0-beta1*です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-106">For example, [Entity Framework](https://www.nuget.org/packages/EntityFramework/) on nuget.org has several dozen specific packages available, ranging from version *4.1.10311* to version *6.1.3* (the latest stable release) and a variety of pre-release versions like *6.2.0-beta1*.</span></span>

<span data-ttu-id="fa7c9-107">パッケージを作成するときに、省略可能なプレリリース テキスト サフィックスを持つ特定のバージョン番号を割り当てます。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-107">When creating a package, you assign a specific version number with an optional pre-release text suffix.</span></span> <span data-ttu-id="fa7c9-108">その一方で、パッケージを使用する際に、厳密なバージョン番号または許容可能なバージョンの範囲のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-108">When consuming packages, on the other hand, you can specify either an exact version number or a range of acceptable versions.</span></span>

<span data-ttu-id="fa7c9-109">このトピックの内容</span><span class="sxs-lookup"><span data-stu-id="fa7c9-109">In this topic:</span></span>

- <span data-ttu-id="fa7c9-110">[バージョンの基礎](#version-basics)プレリリース サフィックスを含むです。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-110">[Version basics](#version-basics) including pre-release suffixes.</span></span>
- [<span data-ttu-id="fa7c9-111">バージョン範囲およびワイルドカード</span><span class="sxs-lookup"><span data-stu-id="fa7c9-111">Version ranges and wildcards</span></span>](#version-ranges-and-wildcards)
- [<span data-ttu-id="fa7c9-112">正規化されたバージョン番号</span><span class="sxs-lookup"><span data-stu-id="fa7c9-112">Normalized version numbers</span></span>](#normalized-version-numbers)

## <a name="version-basics"></a><span data-ttu-id="fa7c9-113">バージョンの基礎</span><span class="sxs-lookup"><span data-stu-id="fa7c9-113">Version basics</span></span>

<span data-ttu-id="fa7c9-114">特定のバージョン番号の形式は*Major.Minor.Patch [-サフィックス]*意味は次のコンポーネントのある、します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-114">A specific version number is in the form *Major.Minor.Patch[-Suffix]*, where the components have the following meanings:</span></span>

- <span data-ttu-id="fa7c9-115">*主要な*: 重大な変更</span><span class="sxs-lookup"><span data-stu-id="fa7c9-115">*Major*: Breaking changes</span></span>
- <span data-ttu-id="fa7c9-116">*マイナー*: 下位互換性のあるの新機能</span><span class="sxs-lookup"><span data-stu-id="fa7c9-116">*Minor*: New features, but backwards compatible</span></span>
- <span data-ttu-id="fa7c9-117">*修正プログラム*: 旧バージョンと互換性のあるバグの修正のみ</span><span class="sxs-lookup"><span data-stu-id="fa7c9-117">*Patch*: Backwards compatible bug fixes only</span></span>
- <span data-ttu-id="fa7c9-118">*-サフィックス*(省略可能): リリース前のバージョンを示す文字列でハイフンの後ろに (以下、[セマンティック バージョニングまたは SemVer 1.0 規約](http://semver.org/spec/v1.0.0.html))。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-118">*-Suffix* (optional): a hyphen followed by a string denoting a pre-release version (following the [Semantic Versioning or SemVer 1.0 convention](http://semver.org/spec/v1.0.0.html)).</span></span>

<span data-ttu-id="fa7c9-119">**例:**</span><span class="sxs-lookup"><span data-stu-id="fa7c9-119">**Examples:**</span></span>
```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> <span data-ttu-id="fa7c9-120">nuget.org は、厳密なバージョン番号が欠落しているパッケージのアップロードを拒否します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-120">nuget.org rejects any package upload that lacks an exact version number.</span></span> <span data-ttu-id="fa7c9-121">バージョンを指定する必要があります、`.nuspec`またはプロジェクト ファイルにパッケージを作成するために使用します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-121">The version must be specified in the `.nuspec` or project file used to create the package.</span></span>

### <a name="pre-release-versions"></a><span data-ttu-id="fa7c9-122">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="fa7c9-122">Pre-release versions</span></span>

<span data-ttu-id="fa7c9-123">技術的には、パッケージの作成者できる任意の文字列をサフィックスとして使用を NuGet がプレリリースとしてこのような任意のバージョンを処理し、他の解釈も負わないものとは、リリース前のバージョンを示すためにします。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-123">Technically speaking, package creators can use any string as a suffix to denote a pre-release version, as NuGet treats any such version as pre-release and makes no other interpretation.</span></span> <span data-ttu-id="fa7c9-124">NuGet 表示がどのような UI で、フル バージョンの文字列が含まれている、コンシューマーにサフィックスの意味の解釈を終了します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-124">That is, NuGet displays the full version string in whatever UI is involved, leaving any interpretation of the suffix's meaning to the consumer.</span></span>

<span data-ttu-id="fa7c9-125">ただし、パッケージの開発者は一般に認識されている名前付け規則に従います。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-125">That said, package developers generally follow recognized naming conventions:</span></span>

- <span data-ttu-id="fa7c9-126">`-alpha`: アルファ リリースでは、通常処理中と実験に使用します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-126">`-alpha`: Alpha release, typically used for work-in-progress and experimentation.</span></span>
- <span data-ttu-id="fa7c9-127">`-beta`: ベータ リリース、通常 1 つは、次の完全な機能のリリースでは、計画的なが既知のバグを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-127">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="fa7c9-128">`-rc`: リリース候補、最終的な可能性がありますが、リリース通常重大なバグが出現しない限り、(stable) です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-128">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="fa7c9-129">NuGet 4.3.0+ をサポートしている[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)、する番号をサポートするプレリリース ドット付き表記でとして*1.0.1-build.23*です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-129">NuGet 4.3.0+ supports [SemVer 2.0.0](http://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in *1.0.1-build.23*.</span></span> <span data-ttu-id="fa7c9-130">4.3.0 前に、のバージョンの NuGet では、ドット表記はサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-130">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="fa7c9-131">ようにフォームを使用して*1.0.1-build23*です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-131">You can use a form like *1.0.1-build23*.</span></span>

<span data-ttu-id="fa7c9-132">パッケージ参照および複数のパッケージ バージョンのみが異なるサフィックスを解決するには、NuGet は最初に、サフィックスが付いていないバージョンを選択し、プレリリース版では、アルファベットの逆順に優先順位を適用します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-132">When resolving package references and multiple package versions differ only by suffix, NuGet chooses a version without a suffix first, then applies precedence to pre-release versions in reverse alphabetical order.</span></span> <span data-ttu-id="fa7c9-133">たとえば、次のバージョンが示されている正確な順序で選択されます。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-133">For example, the following versions would be chosen in the exact order shown:</span></span>

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

## <a name="semantic-versioning-200"></a><span data-ttu-id="fa7c9-134">セマンティック バージョニング 2.0.0</span><span class="sxs-lookup"><span data-stu-id="fa7c9-134">Semantic Versioning 2.0.0</span></span>

<span data-ttu-id="fa7c9-135">NuGet をサポートしている NuGet 4.3.0+ と Visual Studio 2017 バージョン 15.3 +、[セマンティック バージョニング 2.0.0](http://semver.org/spec/v2.0.0.html)です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-135">With NuGet 4.3.0+ and Visual Studio 2017 version 15.3+, NuGet supports [Semantic Versioning 2.0.0](http://semver.org/spec/v2.0.0.html).</span></span>

<span data-ttu-id="fa7c9-136">SemVer v2.0.0 の特定のセマンティクスは、以前のクライアントではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-136">Certain semantics of SemVer v2.0.0 are not supported in older clients.</span></span> <span data-ttu-id="fa7c9-137">NuGet では、パッケージのバージョンが SemVer v2.0.0 固有である場合は true、次のステートメントのいずれかを検討します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-137">NuGet considers a package version to be SemVer v2.0.0 specific if either of the following statements is true:</span></span>

- <span data-ttu-id="fa7c9-138">プレリリース ラベルはドット区切り、たとえば、 *1.0.0-alpha.1*</span><span class="sxs-lookup"><span data-stu-id="fa7c9-138">The pre-release label is dot-separated, for example, *1.0.0-alpha.1*</span></span>
- <span data-ttu-id="fa7c9-139">バージョンには、ビルドのメタデータ、たとえば、 *1.0.0+githash*</span><span class="sxs-lookup"><span data-stu-id="fa7c9-139">The version has build-metadata, for example, *1.0.0+githash*</span></span>

<span data-ttu-id="fa7c9-140">Nuget.org をパッケージが定義されて SemVer v2.0.0 パッケージとして、次のステートメントのいずれかが true の場合。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-140">For nuget.org, a package is defined as a SemVer v2.0.0 package if either of the following statements is true:</span></span>

- <span data-ttu-id="fa7c9-141">パッケージのバージョンでは、上記で定義された SemVer v2.0.0 準拠していませんが、準拠していない SemVer v1.0.0 です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-141">The package's own version is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, as defined above.</span></span>
- <span data-ttu-id="fa7c9-142">最小値または最大なバージョンが SemVer v2.0.0 準拠していませんが、準拠していない SemVer v1.0.0; 上で定義したパッケージの依存関係のバージョンの範囲のいずれかがあります。たとえば、 *[1.0.0-alpha.1,)*です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-142">Any of the package's dependency version ranges has a minimum or maximum version that is SemVer v2.0.0 compliant but not SemVer v1.0.0 compliant, defined above; for example, *[1.0.0-alpha.1, )*.</span></span>

<span data-ttu-id="fa7c9-143">Nuget.org に SemVer v2.0.0 に固有のパッケージをアップロードする場合、パッケージを古いクライアントに非表示とは使用する次の NuGet クライアントのみ。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-143">If you upload a SemVer v2.0.0-specific package to nuget.org, the package is invisible to older clients and available to only the following NuGet clients:</span></span>

- <span data-ttu-id="fa7c9-144">NuGet 4.3.0+</span><span class="sxs-lookup"><span data-stu-id="fa7c9-144">NuGet 4.3.0+</span></span>
- <span data-ttu-id="fa7c9-145">Visual Studio 2017 バージョン 15.3 +</span><span class="sxs-lookup"><span data-stu-id="fa7c9-145">Visual Studio 2017 version 15.3+</span></span> 
- <span data-ttu-id="fa7c9-146">dotnet.exe (.NET SDK 2.0.0+)</span><span class="sxs-lookup"><span data-stu-id="fa7c9-146">dotnet.exe (.NET SDK 2.0.0+)</span></span>

<span data-ttu-id="fa7c9-147">サード パーティ製のクライアント:</span><span class="sxs-lookup"><span data-stu-id="fa7c9-147">Third-party clients:</span></span>

- <span data-ttu-id="fa7c9-148">JetBrains 名</span><span class="sxs-lookup"><span data-stu-id="fa7c9-148">JetBrains Rider</span></span>
- <span data-ttu-id="fa7c9-149">Version 5.0 以降のパケットを作成します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-149">Paket version 5.0+</span></span>

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a><span data-ttu-id="fa7c9-150">バージョン範囲およびワイルドカード</span><span class="sxs-lookup"><span data-stu-id="fa7c9-150">Version ranges and wildcards</span></span>

<span data-ttu-id="fa7c9-151">パッケージの依存関係の場合は、次のとおり、バージョン範囲を指定する間隔の表記を使用して NuGet をサポートします。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-151">When referring to package dependencies, NuGet supports using interval notation for specifying version ranges, summarized as follows:</span></span>

| <span data-ttu-id="fa7c9-152">Notation</span><span class="sxs-lookup"><span data-stu-id="fa7c9-152">Notation</span></span> | <span data-ttu-id="fa7c9-153">適用されるルール</span><span class="sxs-lookup"><span data-stu-id="fa7c9-153">Applied rule</span></span> | <span data-ttu-id="fa7c9-154">説明</span><span class="sxs-lookup"><span data-stu-id="fa7c9-154">Description</span></span> |
|----------|--------------|-------------|
| <span data-ttu-id="fa7c9-155">1.0</span><span class="sxs-lookup"><span data-stu-id="fa7c9-155">1.0</span></span> | <span data-ttu-id="fa7c9-156">1.0 ≤ x</span><span class="sxs-lookup"><span data-stu-id="fa7c9-156">1.0 ≤ x</span></span> | <span data-ttu-id="fa7c9-157">包括的な最小のバージョン</span><span class="sxs-lookup"><span data-stu-id="fa7c9-157">Minimum version, inclusive</span></span> |
| <span data-ttu-id="fa7c9-158">(1.0,)</span><span class="sxs-lookup"><span data-stu-id="fa7c9-158">(1.0,)</span></span> | <span data-ttu-id="fa7c9-159">1.0 < x</span><span class="sxs-lookup"><span data-stu-id="fa7c9-159">1.0 < x</span></span> | <span data-ttu-id="fa7c9-160">排他の最小バージョン</span><span class="sxs-lookup"><span data-stu-id="fa7c9-160">Minimum version, exclusive</span></span> |
| <span data-ttu-id="fa7c9-161">[1.0]</span><span class="sxs-lookup"><span data-stu-id="fa7c9-161">[1.0]</span></span> | <span data-ttu-id="fa7c9-162">x = = 1.0</span><span class="sxs-lookup"><span data-stu-id="fa7c9-162">x == 1.0</span></span> | <span data-ttu-id="fa7c9-163">バージョンに一致します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-163">Exact version match</span></span> |
| <span data-ttu-id="fa7c9-164">(,1.0]</span><span class="sxs-lookup"><span data-stu-id="fa7c9-164">(,1.0]</span></span> | <span data-ttu-id="fa7c9-165">x ≤ 1.0</span><span class="sxs-lookup"><span data-stu-id="fa7c9-165">x ≤ 1.0</span></span> | <span data-ttu-id="fa7c9-166">包括的に、最大のバージョン</span><span class="sxs-lookup"><span data-stu-id="fa7c9-166">Maximum version, inclusive</span></span> |
| <span data-ttu-id="fa7c9-167">(,1.0)</span><span class="sxs-lookup"><span data-stu-id="fa7c9-167">(,1.0)</span></span> | <span data-ttu-id="fa7c9-168">x < 1.0</span><span class="sxs-lookup"><span data-stu-id="fa7c9-168">x < 1.0</span></span> | <span data-ttu-id="fa7c9-169">排他の最大バージョン</span><span class="sxs-lookup"><span data-stu-id="fa7c9-169">Maximum version, exclusive</span></span> |
| <span data-ttu-id="fa7c9-170">[1.0,2.0]</span><span class="sxs-lookup"><span data-stu-id="fa7c9-170">[1.0,2.0]</span></span> | <span data-ttu-id="fa7c9-171">1.0 ≤ x ≤ 2.0</span><span class="sxs-lookup"><span data-stu-id="fa7c9-171">1.0 ≤ x ≤ 2.0</span></span> | <span data-ttu-id="fa7c9-172">正確な範囲を包括的</span><span class="sxs-lookup"><span data-stu-id="fa7c9-172">Exact range, inclusive</span></span> |
| <span data-ttu-id="fa7c9-173">(1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="fa7c9-173">(1.0,2.0)</span></span> | <span data-ttu-id="fa7c9-174">1.0 < < 2.0 x</span><span class="sxs-lookup"><span data-stu-id="fa7c9-174">1.0 < x < 2.0</span></span> | <span data-ttu-id="fa7c9-175">正確な範囲、排他</span><span class="sxs-lookup"><span data-stu-id="fa7c9-175">Exact range, exclusive</span></span> |
| <span data-ttu-id="fa7c9-176">[1.0,2.0)</span><span class="sxs-lookup"><span data-stu-id="fa7c9-176">[1.0,2.0)</span></span> | <span data-ttu-id="fa7c9-177">1.0 ≤ x < 2.0</span><span class="sxs-lookup"><span data-stu-id="fa7c9-177">1.0 ≤ x < 2.0</span></span> | <span data-ttu-id="fa7c9-178">包括的な最小値と排他最大バージョンが混在</span><span class="sxs-lookup"><span data-stu-id="fa7c9-178">Mixed inclusive minimum and exclusive maximum version</span></span> |
| <span data-ttu-id="fa7c9-179">(1.0)</span><span class="sxs-lookup"><span data-stu-id="fa7c9-179">(1.0)</span></span>    | <span data-ttu-id="fa7c9-180">無効な</span><span class="sxs-lookup"><span data-stu-id="fa7c9-180">invalid</span></span> | <span data-ttu-id="fa7c9-181">無効な</span><span class="sxs-lookup"><span data-stu-id="fa7c9-181">invalid</span></span> |

<span data-ttu-id="fa7c9-182">PackageReference を使用する場合または`project.json`参照形式、NuGet パッケージのワイルドカードの表記法を使用してサポートも\*メジャー、マイナー、Patch、および数のプレリリース版サフィックス部分。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-182">When using the PackageReference or `project.json` package reference formats, NuGet also supports using a wildcard notation, \*, for Major, Minor, Patch, and pre-release suffix parts of the number.</span></span> <span data-ttu-id="fa7c9-183">ワイルドカードはサポートされていません、`packages.config`形式です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-183">Wildcards are not supported with the `packages.config` format.</span></span>

> [!Note]
> <span data-ttu-id="fa7c9-184">バージョン範囲を解決するときに、プレリリース バージョンは含まれません。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-184">Pre-release versions are not included when resolving version ranges.</span></span> <span data-ttu-id="fa7c9-185">プレリリース版*は*、ワイルドカードを使用するときに含まれます (\*)。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-185">Pre-release versions *are* included when using a wildcard (\*).</span></span> <span data-ttu-id="fa7c9-186">バージョン範囲*[1.0,2.0]*、たとえば、含まない 2.0 のベータ版ではワイルドカードの表記法_2.0-*_はします。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-186">The version range *[1.0,2.0]*, for example, does not include 2.0-beta, but the wildcard notation _2.0-*_ does.</span></span> <span data-ttu-id="fa7c9-187">参照してください[発行 912](https://github.com/NuGet/Home/issues/912)プレリリース ワイルドカードの詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-187">See [issue 912](https://github.com/NuGet/Home/issues/912) for further discussion on pre-release wildcards.</span></span>

### <a name="examples"></a><span data-ttu-id="fa7c9-188">例</span><span class="sxs-lookup"><span data-stu-id="fa7c9-188">Examples</span></span>

<span data-ttu-id="fa7c9-189">常に、プロジェクト ファイル内のバージョンまたはパッケージの依存関係のバージョンの範囲を指定`packages.config`ファイル、および`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-189">Always specify a version or version range for package dependencies in project files, `packages.config` files, and `.nuspec` files.</span></span> <span data-ttu-id="fa7c9-190">バージョンまたはバージョン範囲、NuGet のない 2.8.x 以前選択して、最新の利用可能なパッケージ、依存関係を解決するときに対し NuGet 3.x し、後で、最小のパッケージ バージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-190">Without a version or version range, NuGet 2.8.x and earlier chooses the latest available package version when resolving a dependency, whereas NuGet 3.x and later chooses the lowest package version.</span></span> <span data-ttu-id="fa7c9-191">バージョンまたはバージョン範囲は、この不確実性を回避できます。 を指定します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-191">Specifying a version or version range avoids this uncertainty.</span></span>

#### <a name="references-in-project-files-packagereference"></a><span data-ttu-id="fa7c9-192">プロジェクト ファイル (PackageReference) 内の参照</span><span class="sxs-lookup"><span data-stu-id="fa7c9-192">References in project files (PackageReference)</span></span>

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

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

<span data-ttu-id="fa7c9-193">**参照`packages.config`:**</span><span class="sxs-lookup"><span data-stu-id="fa7c9-193">**References in `packages.config`:**</span></span>

<span data-ttu-id="fa7c9-194">`packages.config`、すべての依存関係が記載されている完全な`version`パッケージを復元するときに使用される属性です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-194">In `packages.config`, every dependency is listed with an exact `version` attribute that's used when restoring packages.</span></span> <span data-ttu-id="fa7c9-195">`allowedVersions`属性は、パッケージを更新する可能性があるバージョンを制限する更新操作中にのみ使用します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-195">The `allowedVersions` attribute is used only during update operations to constrain the versions to which the package might be updated.</span></span>

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

<span data-ttu-id="fa7c9-196">**参照`.nuspec`ファイル**</span><span class="sxs-lookup"><span data-stu-id="fa7c9-196">**References in `.nuspec` files**</span></span>

<span data-ttu-id="fa7c9-197">`version`属性、`<dependency>`要素に依存関係として受け入れ可能な範囲のバージョンを記述します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-197">The `version` attribute in a `<dependency>` element describes the range versions that are acceptable for a dependency.</span></span>

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

## <a name="normalized-version-numbers"></a><span data-ttu-id="fa7c9-198">正規化されたバージョン番号</span><span class="sxs-lookup"><span data-stu-id="fa7c9-198">Normalized version numbers</span></span>

> [!Note]
> <span data-ttu-id="fa7c9-199">これは、NuGet 3.4 以降では、互換性に影響する変更です。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-199">This is a breaking change for NuGet 3.4 and later.</span></span>

<span data-ttu-id="fa7c9-200">再インストール、または復元操作のインストール中に、リポジトリからパッケージを取得するときに NuGet 3.4 以降はバージョン番号を次のように処理します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-200">When obtaining packages from a repository during install, reinstall, or restore operations, NuGet 3.4+ treats version numbers as follows:</span></span>

- <span data-ttu-id="fa7c9-201">先頭の 0 は、バージョン番号から削除されます。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-201">Leading zeroes are removed from version numbers:</span></span>

    ```
    1.00 is treated as 1.0
    1.01.1 is treated as 1.1.1
    1.00.0.1 is treated as 1.0.0.1
    ```

- <span data-ttu-id="fa7c9-202">バージョン番号の 4 番目の部分のゼロは省略されます。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-202">A zero in the fourth part of the version number will be omitted</span></span>

    ```
    1.0.0.0 is treated as 1.0.0
    1.0.01.0 is treated as 1.0.1
    ```

<span data-ttu-id="fa7c9-203">この正規化には、パッケージ自体; のバージョン番号は変わりません。のみ方法 NuGet と一致するバージョンの依存関係を解決するときに影響します。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-203">This normalization does not affect the version numbers in the packages themselves; it affects only how NuGet matches versions when resolving dependencies.</span></span>

<span data-ttu-id="fa7c9-204">ただし、NuGet パッケージのリポジトリと同じ方法で NuGet パッケージのバージョンの重複を防ぐためにこれらの値を処理する必要があります。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-204">However, NuGet package repositories must treat these values in the same way as NuGet to prevent package version duplication.</span></span> <span data-ttu-id="fa7c9-205">バージョンを格納するリポジトリしたがって*1.0*パッケージの必要がありますもホストしていないバージョン*1.0.0*独立した異なるパッケージとして。</span><span class="sxs-lookup"><span data-stu-id="fa7c9-205">Thus a repository that contains version *1.0* of a package should not also host version *1.0.0* as a separate and different package.</span></span>
