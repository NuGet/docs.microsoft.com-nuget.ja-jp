---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照)
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 9ae8e8dc4e7e901acacffed8b7dfb4162c5ad2b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551391"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="2abe6-103">プロジェクト ファイルのパッケージ参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="2abe6-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="2abe6-104">`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。</span><span class="sxs-lookup"><span data-stu-id="2abe6-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="2abe6-105">PackageReference の呼び出しは、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.Config` ファイルの設定が適用されます。詳細については、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2abe6-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="2abe6-106">PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="2abe6-107">依存関係とコンテンツ フローを細かく制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="2abe6-108">(詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="2abe6-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="2abe6-109">既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。</span><span class="sxs-lookup"><span data-stu-id="2abe6-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="2abe6-110">完全な .NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。</span><span class="sxs-lookup"><span data-stu-id="2abe6-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="2abe6-111">PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに移行し、packages.config を削除します。</span><span class="sxs-lookup"><span data-stu-id="2abe6-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="2abe6-112">PackageReference を追加する</span><span class="sxs-lookup"><span data-stu-id="2abe6-112">Adding a PackageReference</span></span>

<span data-ttu-id="2abe6-113">次の構文を使用し、プロジェクト ファイルに依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="2abe6-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="2abe6-114">依存関係のバージョンを制御する</span><span class="sxs-lookup"><span data-stu-id="2abe6-114">Controlling dependency version</span></span>

<span data-ttu-id="2abe6-115">パッケージのバージョンを指定するための規則は、`packages.config` を使用する場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="2abe6-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2abe6-116">上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」 (パッケージ バージョン) にあります。</span><span class="sxs-lookup"><span data-stu-id="2abe6-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="2abe6-117">PackageReference のないプロジェクトに PackageReference を使用する</span><span class="sxs-lookup"><span data-stu-id="2abe6-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="2abe6-118">詳細: プロジェクトにパッケージをインストールしていないが (プロジェクト ファイルに PackageReferences がなく、packages.config ファイルがない)、プロジェクトを PackageReference スタイルで復元する場合、プロジェクト ファイルで Project プロパティ RestoreProjectStyle を PackageReference に設定できます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="2abe6-119">PackageReference スタイル (既存の csproj または SDK スタイルのプロジェクト) のプロジェクトを参照するとき、この設定が便利になることがあります。</span><span class="sxs-lookup"><span data-stu-id="2abe6-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="2abe6-120">そのようなプロジェクトが参照するパッケージを他のプロジェクトで "推移的に" 参照できます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="2abe6-121">最新バージョン</span><span class="sxs-lookup"><span data-stu-id="2abe6-121">Floating Versions</span></span>

<span data-ttu-id="2abe6-122">[最新バージョン](../consume-packages/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2abe6-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="2abe6-123">依存関係アセットを制御する</span><span class="sxs-lookup"><span data-stu-id="2abe6-123">Controlling dependency assets</span></span>

<span data-ttu-id="2abe6-124">開発ハーネスとしてのみ依存関係を使用するとき、それはパッケージを使用するプロジェクトに公開しないほうが好ましい場合があります。</span><span class="sxs-lookup"><span data-stu-id="2abe6-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="2abe6-125">このシナリオでは、`PrivateAssets` メタデータを使用し、この動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2abe6-126">次のメタデータ タグは依存関係アセットを制御します。</span><span class="sxs-lookup"><span data-stu-id="2abe6-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="2abe6-127">タグ</span><span class="sxs-lookup"><span data-stu-id="2abe6-127">Tag</span></span> | <span data-ttu-id="2abe6-128">説明</span><span class="sxs-lookup"><span data-stu-id="2abe6-128">Description</span></span> | <span data-ttu-id="2abe6-129">既定値</span><span class="sxs-lookup"><span data-stu-id="2abe6-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2abe6-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="2abe6-130">IncludeAssets</span></span> | <span data-ttu-id="2abe6-131">これらのアセットは使用されます</span><span class="sxs-lookup"><span data-stu-id="2abe6-131">These assets will be consumed</span></span> | <span data-ttu-id="2abe6-132">すべて</span><span class="sxs-lookup"><span data-stu-id="2abe6-132">all</span></span> |
| <span data-ttu-id="2abe6-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="2abe6-133">ExcludeAssets</span></span> | <span data-ttu-id="2abe6-134">これらのアセットは使用されません</span><span class="sxs-lookup"><span data-stu-id="2abe6-134">These assets will not be consumed</span></span> | <span data-ttu-id="2abe6-135">none</span><span class="sxs-lookup"><span data-stu-id="2abe6-135">none</span></span> |
| <span data-ttu-id="2abe6-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="2abe6-136">PrivateAssets</span></span> | <span data-ttu-id="2abe6-137">これらのアセットは使用されますが、親プロジェクトに流れません</span><span class="sxs-lookup"><span data-stu-id="2abe6-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="2abe6-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="2abe6-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="2abe6-139">これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="2abe6-140">[値]</span><span class="sxs-lookup"><span data-stu-id="2abe6-140">Value</span></span> | <span data-ttu-id="2abe6-141">説明</span><span class="sxs-lookup"><span data-stu-id="2abe6-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="2abe6-142">compile</span><span class="sxs-lookup"><span data-stu-id="2abe6-142">compile</span></span> | <span data-ttu-id="2abe6-143">`lib` フォルダーの内容と、プロジェクトをフォルダー内のアセンブリに対してコンパイルできるかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="2abe6-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="2abe6-144">ランタイム</span><span class="sxs-lookup"><span data-stu-id="2abe6-144">runtime</span></span> | <span data-ttu-id="2abe6-145">`lib` と `runtimes` フォルダーの内容と、これらのアセンブリがコピーされて出力ディレクトリをビルドするかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="2abe6-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="2abe6-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="2abe6-146">contentFiles</span></span> | <span data-ttu-id="2abe6-147">`contentfiles` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="2abe6-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="2abe6-148">ビルド</span><span class="sxs-lookup"><span data-stu-id="2abe6-148">build</span></span> | <span data-ttu-id="2abe6-149">`build` フォルダーの props と targets</span><span class="sxs-lookup"><span data-stu-id="2abe6-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="2abe6-150">analyzers</span><span class="sxs-lookup"><span data-stu-id="2abe6-150">analyzers</span></span> | <span data-ttu-id="2abe6-151">.NET アナライザー</span><span class="sxs-lookup"><span data-stu-id="2abe6-151">.NET analyzers</span></span> |
| <span data-ttu-id="2abe6-152">native</span><span class="sxs-lookup"><span data-stu-id="2abe6-152">native</span></span> | <span data-ttu-id="2abe6-153">`native` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="2abe6-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="2abe6-154">none</span><span class="sxs-lookup"><span data-stu-id="2abe6-154">none</span></span> | <span data-ttu-id="2abe6-155">上記のいずれも該当しない。</span><span class="sxs-lookup"><span data-stu-id="2abe6-155">None of the above are used.</span></span> |
| <span data-ttu-id="2abe6-156">すべて</span><span class="sxs-lookup"><span data-stu-id="2abe6-156">all</span></span> | <span data-ttu-id="2abe6-157">上記のすべて (`none` を除く)</span><span class="sxs-lookup"><span data-stu-id="2abe6-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="2abe6-158">次の例では、パッケージからのコンテンツ ファイルを除くすべてがプロジェクトによって使用され、コンテンツ ファイルとアナライザーを除くすべてが親プロジェクトに流れます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="2abe6-159">`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに*流れる*ことに注目してください。</span><span class="sxs-lookup"><span data-stu-id="2abe6-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="2abe6-160">たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="2abe6-161">AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="2abe6-162">PackageReference 条件を追加する</span><span class="sxs-lookup"><span data-stu-id="2abe6-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="2abe6-163">条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="2abe6-164">ただし、現在のところ `TargetFramework` 変数のみに対応しています。</span><span class="sxs-lookup"><span data-stu-id="2abe6-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="2abe6-165">たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。</span><span class="sxs-lookup"><span data-stu-id="2abe6-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="2abe6-166">その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。</span><span class="sxs-lookup"><span data-stu-id="2abe6-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="2abe6-167">それを回避するために、次のように `PackageReference` で条件を指定します。</span><span class="sxs-lookup"><span data-stu-id="2abe6-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="2abe6-168">このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

<span data-ttu-id="2abe6-170">条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。</span><span class="sxs-lookup"><span data-stu-id="2abe6-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
