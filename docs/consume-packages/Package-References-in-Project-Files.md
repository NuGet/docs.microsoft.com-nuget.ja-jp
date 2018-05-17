---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照)
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="dd70a-103">プロジェクト ファイルのパッケージ参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="dd70a-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="dd70a-104">`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。</span><span class="sxs-lookup"><span data-stu-id="dd70a-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="dd70a-105">PackageReference の呼び出しは、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.Config` ファイルの設定が適用されます。詳細については、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="dd70a-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="dd70a-106">PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="dd70a-107">依存関係とコンテンツ フローを細かく制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="dd70a-108">(詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="dd70a-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="dd70a-109">既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。</span><span class="sxs-lookup"><span data-stu-id="dd70a-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="dd70a-110">完全な .NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。</span><span class="sxs-lookup"><span data-stu-id="dd70a-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="dd70a-111">PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに移行し、packages.config を削除します。</span><span class="sxs-lookup"><span data-stu-id="dd70a-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="dd70a-112">PackageReference を追加する</span><span class="sxs-lookup"><span data-stu-id="dd70a-112">Adding a PackageReference</span></span>

<span data-ttu-id="dd70a-113">次の構文を使用し、プロジェクト ファイルに依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="dd70a-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="dd70a-114">依存関係のバージョンを制御する</span><span class="sxs-lookup"><span data-stu-id="dd70a-114">Controlling dependency version</span></span>

<span data-ttu-id="dd70a-115">パッケージのバージョンを指定するための規則は、`packages.config` を使用する場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="dd70a-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="dd70a-116">上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」 (パッケージ バージョン) にあります。</span><span class="sxs-lookup"><span data-stu-id="dd70a-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="dd70a-117">最新バージョン</span><span class="sxs-lookup"><span data-stu-id="dd70a-117">Floating Versions</span></span>

<span data-ttu-id="dd70a-118">[最新バージョン](../consume-packages/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="dd70a-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="dd70a-119">依存関係アセットを制御する</span><span class="sxs-lookup"><span data-stu-id="dd70a-119">Controlling dependency assets</span></span>

<span data-ttu-id="dd70a-120">開発ハーネスとしてのみ依存関係を使用するとき、それはパッケージを使用するプロジェクトに公開しないほうが好ましい場合があります。</span><span class="sxs-lookup"><span data-stu-id="dd70a-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="dd70a-121">このシナリオでは、`PrivateAssets` メタデータを使用し、この動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="dd70a-122">次のメタデータ タグは依存関係アセットを制御します。</span><span class="sxs-lookup"><span data-stu-id="dd70a-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="dd70a-123">タグ</span><span class="sxs-lookup"><span data-stu-id="dd70a-123">Tag</span></span> | <span data-ttu-id="dd70a-124">説明</span><span class="sxs-lookup"><span data-stu-id="dd70a-124">Description</span></span> | <span data-ttu-id="dd70a-125">既定値</span><span class="sxs-lookup"><span data-stu-id="dd70a-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd70a-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="dd70a-126">IncludeAssets</span></span> | <span data-ttu-id="dd70a-127">これらのアセットは使用されます</span><span class="sxs-lookup"><span data-stu-id="dd70a-127">These assets will be consumed</span></span> | <span data-ttu-id="dd70a-128">すべて</span><span class="sxs-lookup"><span data-stu-id="dd70a-128">all</span></span> |
| <span data-ttu-id="dd70a-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="dd70a-129">ExcludeAssets</span></span> | <span data-ttu-id="dd70a-130">これらのアセットは使用されません</span><span class="sxs-lookup"><span data-stu-id="dd70a-130">These assets will not be consumed</span></span> | <span data-ttu-id="dd70a-131">none</span><span class="sxs-lookup"><span data-stu-id="dd70a-131">none</span></span> |
| <span data-ttu-id="dd70a-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="dd70a-132">PrivateAssets</span></span> | <span data-ttu-id="dd70a-133">これらのアセットは使用されますが、親プロジェクトに流れません</span><span class="sxs-lookup"><span data-stu-id="dd70a-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="dd70a-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="dd70a-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="dd70a-135">これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="dd70a-136">[値]</span><span class="sxs-lookup"><span data-stu-id="dd70a-136">Value</span></span> | <span data-ttu-id="dd70a-137">説明</span><span class="sxs-lookup"><span data-stu-id="dd70a-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="dd70a-138">compile</span><span class="sxs-lookup"><span data-stu-id="dd70a-138">compile</span></span> | <span data-ttu-id="dd70a-139">`lib` フォルダーの内容と、プロジェクトをフォルダー内のアセンブリに対してコンパイルできるかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="dd70a-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="dd70a-140">ランタイム</span><span class="sxs-lookup"><span data-stu-id="dd70a-140">runtime</span></span> | <span data-ttu-id="dd70a-141">`lib` と `runtimes` フォルダーの内容と、これらのアセンブリがコピーされて出力ディレクトリをビルドするかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="dd70a-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="dd70a-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="dd70a-142">contentFiles</span></span> | <span data-ttu-id="dd70a-143">`contentfiles` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="dd70a-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="dd70a-144">ビルド</span><span class="sxs-lookup"><span data-stu-id="dd70a-144">build</span></span> | <span data-ttu-id="dd70a-145">`build` フォルダーの props と targets</span><span class="sxs-lookup"><span data-stu-id="dd70a-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="dd70a-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="dd70a-146">analyzers</span></span> | <span data-ttu-id="dd70a-147">.NET アナライザー</span><span class="sxs-lookup"><span data-stu-id="dd70a-147">.NET analyzers</span></span> |
| <span data-ttu-id="dd70a-148">native</span><span class="sxs-lookup"><span data-stu-id="dd70a-148">native</span></span> | <span data-ttu-id="dd70a-149">`native` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="dd70a-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="dd70a-150">none</span><span class="sxs-lookup"><span data-stu-id="dd70a-150">none</span></span> | <span data-ttu-id="dd70a-151">上記のいずれも該当しない。</span><span class="sxs-lookup"><span data-stu-id="dd70a-151">None of the above are used.</span></span> |
| <span data-ttu-id="dd70a-152">すべて</span><span class="sxs-lookup"><span data-stu-id="dd70a-152">all</span></span> | <span data-ttu-id="dd70a-153">上記のすべて (`none` を除く)</span><span class="sxs-lookup"><span data-stu-id="dd70a-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="dd70a-154">次の例では、パッケージからのコンテンツ ファイルを除くすべてがプロジェクトによって使用され、コンテンツ ファイルとアナライザーを除くすべてが親プロジェクトに流れます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="dd70a-155">`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに*流れる*ことに注目してください。</span><span class="sxs-lookup"><span data-stu-id="dd70a-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="dd70a-156">たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="dd70a-157">AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="dd70a-158">PackageReference 条件を追加する</span><span class="sxs-lookup"><span data-stu-id="dd70a-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="dd70a-159">条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="dd70a-160">ただし、現在のところ `TargetFramework` 変数のみに対応しています。</span><span class="sxs-lookup"><span data-stu-id="dd70a-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="dd70a-161">たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。</span><span class="sxs-lookup"><span data-stu-id="dd70a-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="dd70a-162">その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。</span><span class="sxs-lookup"><span data-stu-id="dd70a-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="dd70a-163">それを回避するために、次のように `PackageReference` で条件を指定します。</span><span class="sxs-lookup"><span data-stu-id="dd70a-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="dd70a-164">このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

<span data-ttu-id="dd70a-166">条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。</span><span class="sxs-lookup"><span data-stu-id="dd70a-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
