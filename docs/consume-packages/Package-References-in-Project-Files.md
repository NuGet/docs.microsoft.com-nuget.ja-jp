---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照)
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: e4df15be1f29e2c611876aaa49e16ac7d1823938
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248456"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="52ba9-103">プロジェクト ファイルのパッケージ参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="52ba9-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="52ba9-104">`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="52ba9-105">PackageReference の呼び出しは、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.config` ファイルの設定が適用されます。詳細については、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="52ba9-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="52ba9-106">PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="52ba9-107">依存関係とコンテンツ フローを細かく制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="52ba9-108">(詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="52ba9-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="52ba9-109">既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。</span><span class="sxs-lookup"><span data-stu-id="52ba9-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="52ba9-110">.NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。</span><span class="sxs-lookup"><span data-stu-id="52ba9-110">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="52ba9-111">PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに移行し、packages.config を削除します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="52ba9-112">PackageReference を追加する</span><span class="sxs-lookup"><span data-stu-id="52ba9-112">Adding a PackageReference</span></span>

<span data-ttu-id="52ba9-113">次の構文を使用し、プロジェクト ファイルに依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="52ba9-114">依存関係のバージョンを制御する</span><span class="sxs-lookup"><span data-stu-id="52ba9-114">Controlling dependency version</span></span>

<span data-ttu-id="52ba9-115">パッケージのバージョンを指定するための規則は、`packages.config` を使用する場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="52ba9-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="52ba9-116">上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」 (パッケージ バージョン) にあります。</span><span class="sxs-lookup"><span data-stu-id="52ba9-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="52ba9-117">PackageReference のないプロジェクトに PackageReference を使用する</span><span class="sxs-lookup"><span data-stu-id="52ba9-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="52ba9-118">詳細:プロジェクトにパッケージをインストールしていない (プロジェクト ファイルに PackageReferences がなく、packages.config ファイルがない) が、プロジェクトを PackageReference スタイルで復元したい場合は、プロジェクト ファイルで Project プロパティ RestoreProjectStyle を PackageReference に設定できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="52ba9-119">PackageReference スタイル (既存の csproj または SDK スタイルのプロジェクト) のプロジェクトを参照するとき、この設定が便利になることがあります。</span><span class="sxs-lookup"><span data-stu-id="52ba9-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="52ba9-120">そのようなプロジェクトが参照するパッケージを他のプロジェクトで "推移的に" 参照できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="52ba9-121">最新バージョン</span><span class="sxs-lookup"><span data-stu-id="52ba9-121">Floating Versions</span></span>

<span data-ttu-id="52ba9-122">[最新バージョン](../consume-packages/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="52ba9-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="52ba9-123">依存関係アセットを制御する</span><span class="sxs-lookup"><span data-stu-id="52ba9-123">Controlling dependency assets</span></span>

<span data-ttu-id="52ba9-124">開発ハーネスとしてのみ依存関係を使用するとき、それはパッケージを使用するプロジェクトに公開しないほうが好ましい場合があります。</span><span class="sxs-lookup"><span data-stu-id="52ba9-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="52ba9-125">このシナリオでは、`PrivateAssets` メタデータを使用し、この動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="52ba9-126">次のメタデータ タグは依存関係アセットを制御します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="52ba9-127">タグ</span><span class="sxs-lookup"><span data-stu-id="52ba9-127">Tag</span></span> | <span data-ttu-id="52ba9-128">説明</span><span class="sxs-lookup"><span data-stu-id="52ba9-128">Description</span></span> | <span data-ttu-id="52ba9-129">既定値</span><span class="sxs-lookup"><span data-stu-id="52ba9-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="52ba9-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="52ba9-130">IncludeAssets</span></span> | <span data-ttu-id="52ba9-131">これらのアセットは使用されます</span><span class="sxs-lookup"><span data-stu-id="52ba9-131">These assets will be consumed</span></span> | <span data-ttu-id="52ba9-132">all</span><span class="sxs-lookup"><span data-stu-id="52ba9-132">all</span></span> |
| <span data-ttu-id="52ba9-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="52ba9-133">ExcludeAssets</span></span> | <span data-ttu-id="52ba9-134">これらのアセットは使用されません</span><span class="sxs-lookup"><span data-stu-id="52ba9-134">These assets will not be consumed</span></span> | <span data-ttu-id="52ba9-135">none</span><span class="sxs-lookup"><span data-stu-id="52ba9-135">none</span></span> |
| <span data-ttu-id="52ba9-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="52ba9-136">PrivateAssets</span></span> | <span data-ttu-id="52ba9-137">これらのアセットは使用されますが、親プロジェクトに流れません</span><span class="sxs-lookup"><span data-stu-id="52ba9-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="52ba9-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="52ba9-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="52ba9-139">これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="52ba9-140">[値]</span><span class="sxs-lookup"><span data-stu-id="52ba9-140">Value</span></span> | <span data-ttu-id="52ba9-141">説明</span><span class="sxs-lookup"><span data-stu-id="52ba9-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="52ba9-142">compile</span><span class="sxs-lookup"><span data-stu-id="52ba9-142">compile</span></span> | <span data-ttu-id="52ba9-143">`lib` フォルダーの内容と、プロジェクトをフォルダー内のアセンブリに対してコンパイルできるかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="52ba9-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="52ba9-144">ランタイム</span><span class="sxs-lookup"><span data-stu-id="52ba9-144">runtime</span></span> | <span data-ttu-id="52ba9-145">`lib` と `runtimes` フォルダーの内容と、これらのアセンブリがコピーされて出力ディレクトリをビルドするかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="52ba9-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="52ba9-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="52ba9-146">contentFiles</span></span> | <span data-ttu-id="52ba9-147">`contentfiles` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="52ba9-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="52ba9-148">ビルド</span><span class="sxs-lookup"><span data-stu-id="52ba9-148">build</span></span> | <span data-ttu-id="52ba9-149">`build` フォルダーの props と targets</span><span class="sxs-lookup"><span data-stu-id="52ba9-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="52ba9-150">analyzers</span><span class="sxs-lookup"><span data-stu-id="52ba9-150">analyzers</span></span> | <span data-ttu-id="52ba9-151">.NET アナライザー</span><span class="sxs-lookup"><span data-stu-id="52ba9-151">.NET analyzers</span></span> |
| <span data-ttu-id="52ba9-152">native</span><span class="sxs-lookup"><span data-stu-id="52ba9-152">native</span></span> | <span data-ttu-id="52ba9-153">`native` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="52ba9-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="52ba9-154">none</span><span class="sxs-lookup"><span data-stu-id="52ba9-154">none</span></span> | <span data-ttu-id="52ba9-155">上記のいずれも該当しない。</span><span class="sxs-lookup"><span data-stu-id="52ba9-155">None of the above are used.</span></span> |
| <span data-ttu-id="52ba9-156">all</span><span class="sxs-lookup"><span data-stu-id="52ba9-156">all</span></span> | <span data-ttu-id="52ba9-157">上記のすべて (`none` を除く)</span><span class="sxs-lookup"><span data-stu-id="52ba9-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="52ba9-158">次の例では、パッケージからのコンテンツ ファイルを除くすべてがプロジェクトによって使用され、コンテンツ ファイルとアナライザーを除くすべてが親プロジェクトに流れます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="52ba9-159">`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに*流れる*ことに注目してください。</span><span class="sxs-lookup"><span data-stu-id="52ba9-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="52ba9-160">たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="52ba9-161">AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="52ba9-162">PackageReference 条件を追加する</span><span class="sxs-lookup"><span data-stu-id="52ba9-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="52ba9-163">条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="52ba9-164">ただし、現在のところ `TargetFramework` 変数のみに対応しています。</span><span class="sxs-lookup"><span data-stu-id="52ba9-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="52ba9-165">たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。</span><span class="sxs-lookup"><span data-stu-id="52ba9-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="52ba9-166">その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。</span><span class="sxs-lookup"><span data-stu-id="52ba9-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="52ba9-167">それを回避するために、次のように `PackageReference` で条件を指定します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="52ba9-168">このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

<span data-ttu-id="52ba9-170">条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="52ba9-171">依存関係のロック</span><span class="sxs-lookup"><span data-stu-id="52ba9-171">Locking dependencies</span></span>
<span data-ttu-id="52ba9-172">"*この機能を使用できるのは、NuGet **4.9** 以降で、かつ Visual Studio 2017 **15.9** 以降を使用している場合です。*"</span><span class="sxs-lookup"><span data-stu-id="52ba9-172">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="52ba9-173">NuGet の復元への入力は、プロジェクト ファイルのパッケージ参照のセット (最上位レベルまたは直接の依存関係) であり、出力は推移的依存関係を含むパッケージのすべての依存関係の完全なクロージャーです。</span><span class="sxs-lookup"><span data-stu-id="52ba9-173">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="52ba9-174">入力の PackageReference リストが変更されていない場合、NuGet では常に同じパッケージの依存関係の完全なクロージャーを生成しようとします。</span><span class="sxs-lookup"><span data-stu-id="52ba9-174">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="52ba9-175">ただし、このようにすることができないシナリオがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="52ba9-175">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="52ba9-176">例:</span><span class="sxs-lookup"><span data-stu-id="52ba9-176">For example:</span></span>

* <span data-ttu-id="52ba9-177">`<PackageReference Include="My.Sample.Lib" Version="4.*"/>` などの浮動バージョンを使用する場合。</span><span class="sxs-lookup"><span data-stu-id="52ba9-177">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="52ba9-178">ここでの意図はパッケージの復元ごとに最新バージョンに浮動することですが、グラフを特定の最新バージョンにロックして、利用可能な場合は明示的なジェスチャに基づいて後続のバージョンに浮動させることをユーザーが求めるシナリオがあります。</span><span class="sxs-lookup"><span data-stu-id="52ba9-178">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="52ba9-179">PackageReference のバージョン要件と一致する新しいパッケージのバージョンが公開されている場合。</span><span class="sxs-lookup"><span data-stu-id="52ba9-179">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="52ba9-180">たとえば、</span><span class="sxs-lookup"><span data-stu-id="52ba9-180">E.g.</span></span> 

  * <span data-ttu-id="52ba9-181">1 日目: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` を指定したが、NuGet リポジトリで利用可能なバージョンが 4.1.0、4.2.0 および 4.3.0 だった場合。</span><span class="sxs-lookup"><span data-stu-id="52ba9-181">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="52ba9-182">この場合、NuGet は 4.1.0 (最小に最も近いバージョン) に解決されています。</span><span class="sxs-lookup"><span data-stu-id="52ba9-182">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="52ba9-183">2 日目:バージョン 4.0.0 が公開されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-183">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="52ba9-184">NuGet では完全一致が検索され、4.0.0 への解決が始められます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-184">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="52ba9-185">指定したパッケージ バージョンがリポジトリから削除される場合。</span><span class="sxs-lookup"><span data-stu-id="52ba9-185">A given package version is removed from the repository.</span></span> <span data-ttu-id="52ba9-186">nuget.org ではパッケージの削除が許可されていませんが、すべてのパッケージ リポジトリがこの制約を持っているわけではありません。</span><span class="sxs-lookup"><span data-stu-id="52ba9-186">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="52ba9-187">これにより、削除されたバージョンに解決できない場合、NuGet では最適な一致が検索されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-187">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="52ba9-188">ロック ファイルの有効化</span><span class="sxs-lookup"><span data-stu-id="52ba9-188">Enabling lock file</span></span>
<span data-ttu-id="52ba9-189">パッケージの依存関係の完全なクロージャーを保持するために、プロジェクトに対して MSBuild プロパティ `RestorePackagesWithLockFile` を設定して、ロック ファイル機能にオプトインすることができます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-189">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="52ba9-190">このプロパティが設定されている場合、NuGet の復元でロック ファイル (すべてのパッケージの依存関係を一覧表示する `packages.lock.json` ファイル) が生成されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-190">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="52ba9-191">プロジェクトのルート ディレクトリに `packages.lock.json` ファイルが含まれている場合、プロパティ `RestorePackagesWithLockFile` が設定されていない場合でも、常に復元でロック ファイルが使用されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-191">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="52ba9-192">そのため、この機能にオプトインする別の方法は、プロジェクトのルート ディレクトリに空の `packages.lock.json` ファイルをダミーとして作成することです。</span><span class="sxs-lookup"><span data-stu-id="52ba9-192">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="52ba9-193">ロック ファイルでの `restore` の動作</span><span class="sxs-lookup"><span data-stu-id="52ba9-193">`restore` behavior with lock file</span></span>
<span data-ttu-id="52ba9-194">プロジェクトにロック ファイルが存在する場合、NuGet では `restore` を実行するためにこのロック ファイルが使用されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-194">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="52ba9-195">プロジェクト ファイル (または依存プロジェクトのファイル) で言及されたパッケージの依存関係に変更があったかどうか確認するために、NuGet で簡単なチェックが行われます。変更がなかった場合は、ロック ファイルで言及されたパッケージを単純に復元します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-195">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="52ba9-196">パッケージの依存関係を再評価することはありません。</span><span class="sxs-lookup"><span data-stu-id="52ba9-196">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="52ba9-197">NuGet によって、プロジェクト ファイルで言及したような定義された依存関係の変更が検出された場合、パッケージ グラフが再評価され、プロジェクトの新しいパッケージ クロージャを反映するためにロック ファイルが更新されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-197">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="52ba9-198">実行中にパッケージの依存関係を変更したくない CI/CD やその他のシナリオでは、`lockedmode` を `true` に設定することでこれを実行できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-198">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="52ba9-199">dotnet.exe の場合は、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-199">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="52ba9-200">msbuild.exe の場合は、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-200">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="52ba9-201">自分のプロジェクト ファイルにもこの条件付き MSBuild プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-201">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="52ba9-202">ロック モードが `true` である場合、復元ではロック ファイルに記載されている正確なパッケージが復元されるか、または、ロック ファイルの作成後にプロジェクトの定義されたパッケージの依存関係を更新した場合は、失敗します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-202">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="52ba9-203">ロック ファイルをソース リポジトリの一部にする</span><span class="sxs-lookup"><span data-stu-id="52ba9-203">Make lock file part of your source repository</span></span>
<span data-ttu-id="52ba9-204">アプリケーションを作成する場合、目的の実行可能ファイルとプロジェクトは依存関係チェーンの最初に位置します。NuGet が復元中にこれを使用できるように、ロック ファイルをソース コード リポジトリにチェックインします。</span><span class="sxs-lookup"><span data-stu-id="52ba9-204">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="52ba9-205">ただし、当該プロジェクトが出荷しないライブラリ プロジェクトである場合や、他のプロジェクトが依存する共通コード プロジェクトである場合は、ソース コードの一部としてロック ファイルをチェックイン**しないでください**。</span><span class="sxs-lookup"><span data-stu-id="52ba9-205">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="52ba9-206">ロック ファイルを保持しても問題はありませんが、共通コード プロジェクトのロックされているパッケージの依存関係は、ロック ファイル内で記載されているように、この共通コード プロジェクトに依存するプロジェクトの復元/ビルド中に使用されない場合があります。</span><span class="sxs-lookup"><span data-stu-id="52ba9-206">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="52ba9-207">例:</span><span class="sxs-lookup"><span data-stu-id="52ba9-207">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="52ba9-208">`ProjectA` が `PackageX` のバージョン `2.0.0` に依存し、`PackageX` のバージョン `1.0.0` に依存する `ProjectB` も参照している場合、`ProjectB` のロック ファイルでは `PackageX` のバージョン `1.0.0` に対する依存関係が記載されます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-208">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="52ba9-209">ただし、`ProjectA` をビルドすると、そのロック ファイルには `PackageX` のバージョン **`2.0.0`** に対する依存関係が含まれます。`ProjectB` のロック ファイルに記載されている `1.0.0` では**ありません**。</span><span class="sxs-lookup"><span data-stu-id="52ba9-209">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="52ba9-210">したがって、共通コード プロジェクトのロックファイルは、それが依存するプロジェクトのために解決されるパッケージに対して強い力を持っていません。</span><span class="sxs-lookup"><span data-stu-id="52ba9-210">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="52ba9-211">ロック ファイルの拡張機能</span><span class="sxs-lookup"><span data-stu-id="52ba9-211">Lock file extensibility</span></span>
<span data-ttu-id="52ba9-212">以下で説明するように、ロック ファイルを使用して復元のさまざまな動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-212">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="52ba9-213">オプション</span><span class="sxs-lookup"><span data-stu-id="52ba9-213">Option</span></span> | <span data-ttu-id="52ba9-214">対応する MSBuild オプション</span><span class="sxs-lookup"><span data-stu-id="52ba9-214">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="52ba9-215">プロジェクトのロック ファイルでのブートス トラップの使用です。</span><span class="sxs-lookup"><span data-stu-id="52ba9-215">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="52ba9-216">代わりに、プロジェクト ファイル内で `RestorePackagesWithLockFile` プロパティを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-216">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="52ba9-217">復元のロック モードを有効にします。</span><span class="sxs-lookup"><span data-stu-id="52ba9-217">Enables locked mode for restore.</span></span> <span data-ttu-id="52ba9-218">これは、繰り返し可能なビルドを取得する必要がある CI/CD のシナリオで役立ちます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-218">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="52ba9-219">または、`RestoreLockedMode` MSBuild プロパティを `true` に設定する方法もあります。</span><span class="sxs-lookup"><span data-stu-id="52ba9-219">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="52ba9-220">このオプションは、プロジェクトで定義する浮動バージョンを使用するパッケージで役立ちます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-220">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="52ba9-221">既定では、NuGet の復元では、`--force-evaluate` オプションを使用して復元を実行しない限り、各復元に基づくパッケージ バージョンの自動更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="52ba9-221">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="52ba9-222">プロジェクトのカスタム ロック ファイルの場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="52ba9-222">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="52ba9-223">これは、MSBuild プロパティ `NuGetLockFilePath` を設定することでも実現できます。</span><span class="sxs-lookup"><span data-stu-id="52ba9-223">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="52ba9-224">既定では、NuGet はルート ディレクトリでの `packages.lock.json` をサポートします。</span><span class="sxs-lookup"><span data-stu-id="52ba9-224">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="52ba9-225">同じディレクトリ内に複数のプロジェクトがある場合、NuGet はプロジェクト固有のロック ファイル `packages.<project_name>.lock.json` をサポートします。</span><span class="sxs-lookup"><span data-stu-id="52ba9-225">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
