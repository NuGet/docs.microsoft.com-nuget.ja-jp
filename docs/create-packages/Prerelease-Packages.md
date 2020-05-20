---
title: NuGet パッケージのプレリリース版
description: プレリリース パッケージのビルド ガイド
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610711"
---
# <a name="building-pre-release-packages"></a><span data-ttu-id="40867-103">プレリリース パッケージのビルド</span><span class="sxs-lookup"><span data-stu-id="40867-103">Building pre-release packages</span></span>

<span data-ttu-id="40867-104">更新したパッケージを新しいバージョン番号でリリースすると、NuGet はそれを "最新の安定版リリース" として見なし、たとえば、Visual Studio 内のパッケージ マネージャー UI で下記のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="40867-104">Whenever you release an updated package with a new version number, NuGet considers that one as the "latest stable release" as shown, for example in the Package Manager UI within Visual Studio:</span></span>

![最新の安定版リリースを示すパッケージ マネージャー UI](media/Prerelease_01-LatestStable.png)

<span data-ttu-id="40867-106">安定版リリースとは、実稼働環境で使用するだけの信頼性があると見なされるリリースです。</span><span class="sxs-lookup"><span data-stu-id="40867-106">A stable release is one that's considered reliable enough to be used in production.</span></span> <span data-ttu-id="40867-107">最新の安定版リリースは、パッケージ更新またはパッケージ復元でインストールされるリリースでもあります (「[Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) の説明にある制約に左右されます)。</span><span class="sxs-lookup"><span data-stu-id="40867-107">The latest stable release is also the one that will be installed as a package update or during package restore (subject to constraints as described in [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)).</span></span>

<span data-ttu-id="40867-108">ソフトウェア リリース ライフサイクルをサポートするために、NuGet 1.6 以降では、プレリリース パッケージを配信できます。バージョン番号には、`-alpha`、`-beta`、`-rc` のようなセマンティック バージョン管理サフィックスが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40867-108">To support the software release lifecycle, NuGet 1.6 and later allows for the distribution of pre-release packages, where the version number includes a semantic versioning suffix such as `-alpha`, `-beta`, or `-rc`.</span></span> <span data-ttu-id="40867-109">詳細については、「[Package versioning](../concepts/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="40867-109">For more information, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

<span data-ttu-id="40867-110">次の方法のいずれかを使って、このようなバージョンを指定できます。</span><span class="sxs-lookup"><span data-stu-id="40867-110">You can specify such versions using one of the following ways:</span></span>

- <span data-ttu-id="40867-111">**プロジェクトで [`PackageReference`](../consume-packages/package-references-in-project-files.md) を使う場合**: `.csproj` ファイルの [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) 要素にセマンティック バージョン サフィックスを含めます。</span><span class="sxs-lookup"><span data-stu-id="40867-111">**If your project uses [`PackageReference`](../consume-packages/package-references-in-project-files.md)**: include the semantic version suffix in the `.csproj` file's [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) element:</span></span>

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- <span data-ttu-id="40867-112">**プロジェクトに [`packages.config`](../reference/packages-config.md) ファイルがある場合**: [`.nuspec`](../reference/nuspec.md) ファイルの [`version`](../reference/nuspec.md#version) 要素にセマンティック バージョン サフィックスを含めます。</span><span class="sxs-lookup"><span data-stu-id="40867-112">**If your project has a [`packages.config`](../reference/packages-config.md) file**: include the semantic version suffix in the [`.nuspec`](../reference/nuspec.md) file's [`version`](../reference/nuspec.md#version) element:</span></span>

    ```xml
    <version>1.0.1-alpha</version>
    ```

<span data-ttu-id="40867-113">安定版バージョンをリリースする用意ができたら、サフィックスを削除します。このパッケージはあらゆるプレリリース版に優先します。</span><span class="sxs-lookup"><span data-stu-id="40867-113">When you're ready to release a stable version, just remove the suffix and the package takes precedence over any pre-release versions.</span></span> <span data-ttu-id="40867-114">繰り返しになりますが、「[Package versioning](../concepts/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="40867-114">Again, see [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span>

## <a name="installing-and-updating-pre-release-packages"></a><span data-ttu-id="40867-115">プレリリース パッケージのインストールと更新</span><span class="sxs-lookup"><span data-stu-id="40867-115">Installing and updating pre-release packages</span></span>

<span data-ttu-id="40867-116">既定で、NuGet ではパッケージの使用時にプレリリース版を含めませんが、この動作は次のように変更できます。</span><span class="sxs-lookup"><span data-stu-id="40867-116">By default, NuGet does not include pre-release versions when working with packages, but you can change this behavior as follows:</span></span>

- <span data-ttu-id="40867-117">**Visual Studio のパッケージ マネージャー UI**: **[NuGet パッケージの管理]** UI で、 **[プレリリースを含める]** ボックスを選択します。</span><span class="sxs-lookup"><span data-stu-id="40867-117">**Package Manager UI in Visual Studio**: In the **Manage NuGet Packages** UI, check the **Include prerelease** box:</span></span>

    ![Visual Studio の [プレリリースを含める] チェックボックス](media/Prerelease_02-CheckPrerelease.png)

    <span data-ttu-id="40867-119">このボックスをオンまたはオフにするとパッケージ マネージャー UI とインストールできるバージョンの一覧が更新されます。</span><span class="sxs-lookup"><span data-stu-id="40867-119">Setting or clearing this box will refresh the Package Manager UI and the list of available versions you can install.</span></span>

- <span data-ttu-id="40867-120">**パッケージ マネージャー コンソール**: `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package`、`Update-Package` コマンドで `-IncludePrerelease` スイッチを使用します。</span><span class="sxs-lookup"><span data-stu-id="40867-120">**Package Manager Console**: Use the `-IncludePrerelease` switch with the `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package`, and `Update-Package` commands.</span></span> <span data-ttu-id="40867-121">「[PowerShell Reference](../reference/powershell-reference.md)」 (PowerShell リファレンス) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="40867-121">Refer to the [PowerShell Reference](../reference/powershell-reference.md).</span></span>

- <span data-ttu-id="40867-122">**NuGet CLI**: `install`、`update`、`delete`、`mirror` コマンドで `-prerelease` スイッチを使用します。</span><span class="sxs-lookup"><span data-stu-id="40867-122">**NuGet CLI**: Use the `-prerelease` switch with the `install`, `update`, `delete`, and `mirror` commands.</span></span> <span data-ttu-id="40867-123">「[NuGet CLI reference](../reference/nuget-exe-cli-reference.md)」 (NuGet CLI リファレンス) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="40867-123">Refer to the [NuGet CLI reference](../reference/nuget-exe-cli-reference.md)</span></span>

## <a name="semantic-versioning"></a><span data-ttu-id="40867-124">セマンティック バージョニング</span><span class="sxs-lookup"><span data-stu-id="40867-124">Semantic versioning</span></span>

<span data-ttu-id="40867-125">「[Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html)」 (セマンティック バージョニングまたは SemVer 規則) では、バージョン番号の文字列を活用し、基礎となっているコードの意味を伝える方法が説明されています。</span><span class="sxs-lookup"><span data-stu-id="40867-125">The [Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html) describes how to utilize strings in version numbers to convey the meaning of the underlying code.</span></span>

<span data-ttu-id="40867-126">この規則では、各バージョンが 3 つの部分、`Major.Minor.Patch` から構成されています。それぞれ次のような意味があります。</span><span class="sxs-lookup"><span data-stu-id="40867-126">In this convention, each version has three parts, `Major.Minor.Patch`, with the following meaning:</span></span>

- <span data-ttu-id="40867-127">`Major`: 互換性に影響する変更点</span><span class="sxs-lookup"><span data-stu-id="40867-127">`Major`: Breaking changes</span></span>
- <span data-ttu-id="40867-128">`Minor`: 新機能、ただし下位互換性あり</span><span class="sxs-lookup"><span data-stu-id="40867-128">`Minor`: New features, but backwards compatible</span></span>
- <span data-ttu-id="40867-129">`Patch`: 下位互換性のバグ修正のみ</span><span class="sxs-lookup"><span data-stu-id="40867-129">`Patch`: Backwards compatible bug fixes only</span></span>

<span data-ttu-id="40867-130">プレリリース版には、パッチ番号の後にハイフンと文字列が付きます。</span><span class="sxs-lookup"><span data-stu-id="40867-130">Pre-release versions are then denoted by appending a hyphen and a string after the patch number.</span></span> <span data-ttu-id="40867-131">技術的に言えば、ハイフンの後には*あらゆる*文字列を使用できます。それで NuGet はパッケージをプレリリースとして扱います。</span><span class="sxs-lookup"><span data-stu-id="40867-131">Technically speaking, you can use *any* string after the hyphen and NuGet will treat the package as pre-release.</span></span> <span data-ttu-id="40867-132">NuGet は該当 UI に完全なバージョン番号を表示します。利用者はその意味を自分で解釈します。</span><span class="sxs-lookup"><span data-stu-id="40867-132">NuGet then displays the full version number in the applicable UI, leaving consumers to interpret the meaning for themselves.</span></span>

<span data-ttu-id="40867-133">それを踏まえた上で、次のような認められている命名規則に従うことが一般的に推奨されます。</span><span class="sxs-lookup"><span data-stu-id="40867-133">With this in mind, it's generally good to follow recognized naming conventions such as the following:</span></span>

- <span data-ttu-id="40867-134">`-alpha`: アルファ リリース。一般的に、進行中の製品または実験に使用されます。</span><span class="sxs-lookup"><span data-stu-id="40867-134">`-alpha`: Alpha release, typically used for work-in-progress and experimentation</span></span>
- <span data-ttu-id="40867-135">`-beta`: ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。</span><span class="sxs-lookup"><span data-stu-id="40867-135">`-beta`: Beta release, typically one that is feature complete for the next planned release, but may contain known bugs.</span></span>
- <span data-ttu-id="40867-136">`-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。</span><span class="sxs-lookup"><span data-stu-id="40867-136">`-rc`: Release candidate, typically a release that's potentially final (stable) unless significant bugs emerge.</span></span>

> [!Note]
> <span data-ttu-id="40867-137">NuGet 4.3.0 以降は、`1.0.1-build.23` のように、ドット表記のプレリリース番号をサポートする[セマンティック バージョニング v2.0.0](https://semver.org/spec/v2.0.0.html) をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="40867-137">NuGet 4.3.0+ supports [Semantic Versioning v2.0.0](https://semver.org/spec/v2.0.0.html), which supports pre-release numbers with dot notation, as in `1.0.1-build.23`.</span></span> <span data-ttu-id="40867-138">ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="40867-138">Dot notation is not supported with NuGet versions before 4.3.0.</span></span> <span data-ttu-id="40867-139">以前のバージョンの NuGet では、`1.0.1-build23` のような形式を使用できましたが、これは常にプレリリース版と見なされていました。</span><span class="sxs-lookup"><span data-stu-id="40867-139">In earlier versions of NuGet, you could use a form like `1.0.1-build23` but this was always considered a pre-release version.</span></span>

<span data-ttu-id="40867-140">ただし、どのようなサフィックスを使用する場合でも、NuGet はアルファベットの逆順で優先順序を与えます。</span><span class="sxs-lookup"><span data-stu-id="40867-140">Whatever suffixes you use, however, NuGet will give them precedence in reverse alphabetical order:</span></span>

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

<span data-ttu-id="40867-141">このように、サフィックスのないバージョンは常にプレリリース版に優先します。</span><span class="sxs-lookup"><span data-stu-id="40867-141">As shown, the version without any suffix will always take precedence over pre-release versions.</span></span>

<span data-ttu-id="40867-142">semver2 では、0 を前に付ける必要はありませんが、古いバージョンのスキーマでは付与されています。</span><span class="sxs-lookup"><span data-stu-id="40867-142">Leading 0s are not needed with semver2, but they are with the old version schema.</span></span> <span data-ttu-id="40867-143">プレリリース タグと共に数値のサフィックスを使用し、その数字が 2 桁 (以上) になる可能性がある場合、beta.01 や beta.05 のように、数字が大きくなっても確実に正しく並べ替えられるように、前に付けるゼロを使用してください。</span><span class="sxs-lookup"><span data-stu-id="40867-143">If you use numerical suffixes with pre-release tags that might use double-digit numbers (or more), use leading zeroes as in beta.01 and beta.05 to ensure that they sort correctly when the numbers get larger.</span></span> <span data-ttu-id="40867-144">この推奨事項は、古いバージョンのスキーマのみに適用されます。</span><span class="sxs-lookup"><span data-stu-id="40867-144">This recommendation only applies to the old version schema.</span></span>
