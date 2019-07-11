---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照)
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 16a14a72f8bb2e5d5a56f6c3c277f0988869273d
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426693"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="87d86-103">プロジェクト ファイルのパッケージ参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="87d86-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="87d86-104">`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。</span><span class="sxs-lookup"><span data-stu-id="87d86-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="87d86-105">PackageReference を使用する場合、呼び出されても、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.config` ファイルの設定が、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」で説明されているように引き続き適用されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="87d86-106">PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="87d86-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="87d86-107">依存関係とコンテンツ フローを細かく制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="87d86-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="87d86-108">(詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="87d86-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="87d86-109">プロジェクトの種類のサポート</span><span class="sxs-lookup"><span data-stu-id="87d86-109">Project type support</span></span>

<span data-ttu-id="87d86-110">既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。</span><span class="sxs-lookup"><span data-stu-id="87d86-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="87d86-111">.NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。</span><span class="sxs-lookup"><span data-stu-id="87d86-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="87d86-112">PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに "[移行](../reference/migrate-packages-config-to-package-reference.md)" してから、packages.config を削除します。</span><span class="sxs-lookup"><span data-stu-id="87d86-112">To use PackageReference, [migrate](../reference/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="87d86-113">完全な .NET Framework を対象とする ASP.NET アプリには、PackageReference の[制限されたサポート](https://github.com/NuGet/Home/issues/5877)しか追加されません。</span><span class="sxs-lookup"><span data-stu-id="87d86-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="87d86-114">C++ および JavaScript のプロジェクト タイプはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="87d86-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="87d86-115">PackageReference を追加する</span><span class="sxs-lookup"><span data-stu-id="87d86-115">Adding a PackageReference</span></span>

<span data-ttu-id="87d86-116">次の構文を使用し、プロジェクト ファイルに依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="87d86-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="87d86-117">依存関係のバージョンを制御する</span><span class="sxs-lookup"><span data-stu-id="87d86-117">Controlling dependency version</span></span>

<span data-ttu-id="87d86-118">パッケージのバージョンを指定するための規則は、`packages.config` を使用する場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="87d86-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="87d86-119">上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」 (パッケージ バージョン) にあります。</span><span class="sxs-lookup"><span data-stu-id="87d86-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="87d86-120">PackageReference のないプロジェクトに PackageReference を使用する</span><span class="sxs-lookup"><span data-stu-id="87d86-120">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="87d86-121">詳細:プロジェクトにパッケージをインストールしていない (プロジェクト ファイルに PackageReferences がなく、packages.config ファイルがない) が、プロジェクトを PackageReference スタイルで復元したい場合は、プロジェクト ファイルで Project プロパティ RestoreProjectStyle を PackageReference に設定できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="87d86-122">PackageReference スタイル (既存の csproj または SDK スタイルのプロジェクト) のプロジェクトを参照するとき、この設定が便利になることがあります。</span><span class="sxs-lookup"><span data-stu-id="87d86-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="87d86-123">そのようなプロジェクトが参照するパッケージを他のプロジェクトで "推移的に" 参照できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="87d86-124">最新バージョン</span><span class="sxs-lookup"><span data-stu-id="87d86-124">Floating Versions</span></span>

<span data-ttu-id="87d86-125">[最新バージョン](../consume-packages/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="87d86-125">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="87d86-126">依存関係アセットを制御する</span><span class="sxs-lookup"><span data-stu-id="87d86-126">Controlling dependency assets</span></span>

<span data-ttu-id="87d86-127">開発ハーネスとしてのみ依存関係を使用するとき、それはパッケージを使用するプロジェクトに公開しないほうが好ましい場合があります。</span><span class="sxs-lookup"><span data-stu-id="87d86-127">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="87d86-128">このシナリオでは、`PrivateAssets` メタデータを使用し、この動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-128">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="87d86-129">次のメタデータ タグは依存関係アセットを制御します。</span><span class="sxs-lookup"><span data-stu-id="87d86-129">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="87d86-130">タグ</span><span class="sxs-lookup"><span data-stu-id="87d86-130">Tag</span></span> | <span data-ttu-id="87d86-131">説明</span><span class="sxs-lookup"><span data-stu-id="87d86-131">Description</span></span> | <span data-ttu-id="87d86-132">既定値</span><span class="sxs-lookup"><span data-stu-id="87d86-132">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87d86-133">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="87d86-133">IncludeAssets</span></span> | <span data-ttu-id="87d86-134">これらのアセットは使用されます</span><span class="sxs-lookup"><span data-stu-id="87d86-134">These assets will be consumed</span></span> | <span data-ttu-id="87d86-135">all</span><span class="sxs-lookup"><span data-stu-id="87d86-135">all</span></span> |
| <span data-ttu-id="87d86-136">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="87d86-136">ExcludeAssets</span></span> | <span data-ttu-id="87d86-137">これらのアセットは使用されません</span><span class="sxs-lookup"><span data-stu-id="87d86-137">These assets will not be consumed</span></span> | <span data-ttu-id="87d86-138">none</span><span class="sxs-lookup"><span data-stu-id="87d86-138">none</span></span> |
| <span data-ttu-id="87d86-139">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="87d86-139">PrivateAssets</span></span> | <span data-ttu-id="87d86-140">これらのアセットは使用されますが、親プロジェクトに流れません</span><span class="sxs-lookup"><span data-stu-id="87d86-140">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="87d86-141">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="87d86-141">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="87d86-142">これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。</span><span class="sxs-lookup"><span data-stu-id="87d86-142">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="87d86-143">[値]</span><span class="sxs-lookup"><span data-stu-id="87d86-143">Value</span></span> | <span data-ttu-id="87d86-144">説明</span><span class="sxs-lookup"><span data-stu-id="87d86-144">Description</span></span> |
| --- | ---
| <span data-ttu-id="87d86-145">compile</span><span class="sxs-lookup"><span data-stu-id="87d86-145">compile</span></span> | <span data-ttu-id="87d86-146">`lib` フォルダーの内容と、プロジェクトをフォルダー内のアセンブリに対してコンパイルできるかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="87d86-146">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="87d86-147">runtime</span><span class="sxs-lookup"><span data-stu-id="87d86-147">runtime</span></span> | <span data-ttu-id="87d86-148">`lib` と `runtimes` フォルダーの内容と、これらのアセンブリがコピーされて出力ディレクトリをビルドするかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="87d86-148">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="87d86-149">contentFiles</span><span class="sxs-lookup"><span data-stu-id="87d86-149">contentFiles</span></span> | <span data-ttu-id="87d86-150">`contentfiles` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="87d86-150">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="87d86-151">build</span><span class="sxs-lookup"><span data-stu-id="87d86-151">build</span></span> | <span data-ttu-id="87d86-152">`build` フォルダーの props と targets</span><span class="sxs-lookup"><span data-stu-id="87d86-152">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="87d86-153">analyzers</span><span class="sxs-lookup"><span data-stu-id="87d86-153">analyzers</span></span> | <span data-ttu-id="87d86-154">.NET アナライザー</span><span class="sxs-lookup"><span data-stu-id="87d86-154">.NET analyzers</span></span> |
| <span data-ttu-id="87d86-155">native</span><span class="sxs-lookup"><span data-stu-id="87d86-155">native</span></span> | <span data-ttu-id="87d86-156">`native` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="87d86-156">Contents of the `native` folder</span></span> |
| <span data-ttu-id="87d86-157">none</span><span class="sxs-lookup"><span data-stu-id="87d86-157">none</span></span> | <span data-ttu-id="87d86-158">上記のいずれも該当しない。</span><span class="sxs-lookup"><span data-stu-id="87d86-158">None of the above are used.</span></span> |
| <span data-ttu-id="87d86-159">all</span><span class="sxs-lookup"><span data-stu-id="87d86-159">all</span></span> | <span data-ttu-id="87d86-160">上記のすべて (`none` を除く)</span><span class="sxs-lookup"><span data-stu-id="87d86-160">All of the above (except `none`)</span></span> |

<span data-ttu-id="87d86-161">次の例では、パッケージからのコンテンツ ファイルを除くすべてがプロジェクトによって使用され、コンテンツ ファイルとアナライザーを除くすべてが親プロジェクトに流れます。</span><span class="sxs-lookup"><span data-stu-id="87d86-161">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="87d86-162">`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに*流れる*ことに注目してください。</span><span class="sxs-lookup"><span data-stu-id="87d86-162">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="87d86-163">たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-163">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="87d86-164">AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-164">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="87d86-165">PackageReference 条件を追加する</span><span class="sxs-lookup"><span data-stu-id="87d86-165">Adding a PackageReference condition</span></span>

<span data-ttu-id="87d86-166">条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-166">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="87d86-167">ただし、現在のところ `TargetFramework` 変数のみに対応しています。</span><span class="sxs-lookup"><span data-stu-id="87d86-167">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="87d86-168">たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。</span><span class="sxs-lookup"><span data-stu-id="87d86-168">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="87d86-169">その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。</span><span class="sxs-lookup"><span data-stu-id="87d86-169">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="87d86-170">それを回避するために、次のように `PackageReference` で条件を指定します。</span><span class="sxs-lookup"><span data-stu-id="87d86-170">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="87d86-171">このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-171">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

<span data-ttu-id="87d86-173">条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-173">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="locking-dependencies"></a><span data-ttu-id="87d86-174">依存関係のロック</span><span class="sxs-lookup"><span data-stu-id="87d86-174">Locking dependencies</span></span>
<span data-ttu-id="87d86-175">"*この機能を使用できるのは、NuGet **4.9** 以降で、かつ Visual Studio 2017 **15.9** 以降を使用している場合です。* "</span><span class="sxs-lookup"><span data-stu-id="87d86-175">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="87d86-176">NuGet の復元への入力は、プロジェクト ファイルのパッケージ参照のセット (最上位レベルまたは直接の依存関係) であり、出力は推移的依存関係を含むパッケージのすべての依存関係の完全なクロージャーです。</span><span class="sxs-lookup"><span data-stu-id="87d86-176">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="87d86-177">入力の PackageReference リストが変更されていない場合、NuGet では常に同じパッケージの依存関係の完全なクロージャーを生成しようとします。</span><span class="sxs-lookup"><span data-stu-id="87d86-177">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="87d86-178">ただし、このようにすることができないシナリオがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="87d86-178">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="87d86-179">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="87d86-179">For example:</span></span>

* <span data-ttu-id="87d86-180">`<PackageReference Include="My.Sample.Lib" Version="4.*"/>` などの浮動バージョンを使用する場合。</span><span class="sxs-lookup"><span data-stu-id="87d86-180">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="87d86-181">ここでの意図はパッケージの復元ごとに最新バージョンに浮動することですが、グラフを特定の最新バージョンにロックして、利用可能な場合は明示的なジェスチャに基づいて後続のバージョンに浮動させることをユーザーが求めるシナリオがあります。</span><span class="sxs-lookup"><span data-stu-id="87d86-181">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="87d86-182">PackageReference のバージョン要件と一致する新しいパッケージのバージョンが公開されている場合。</span><span class="sxs-lookup"><span data-stu-id="87d86-182">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="87d86-183">たとえば、</span><span class="sxs-lookup"><span data-stu-id="87d86-183">E.g.</span></span> 

  * <span data-ttu-id="87d86-184">1 日目: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` を指定したが、NuGet リポジトリで利用可能なバージョンが 4.1.0、4.2.0 および 4.3.0 だった場合。</span><span class="sxs-lookup"><span data-stu-id="87d86-184">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="87d86-185">この場合、NuGet は 4.1.0 (最小に最も近いバージョン) に解決されています。</span><span class="sxs-lookup"><span data-stu-id="87d86-185">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="87d86-186">2 日目:バージョン 4.0.0 が公開されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-186">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="87d86-187">NuGet では完全一致が検索され、4.0.0 への解決が始められます。</span><span class="sxs-lookup"><span data-stu-id="87d86-187">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="87d86-188">指定したパッケージ バージョンがリポジトリから削除される場合。</span><span class="sxs-lookup"><span data-stu-id="87d86-188">A given package version is removed from the repository.</span></span> <span data-ttu-id="87d86-189">nuget.org ではパッケージの削除が許可されていませんが、すべてのパッケージ リポジトリがこの制約を持っているわけではありません。</span><span class="sxs-lookup"><span data-stu-id="87d86-189">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="87d86-190">これにより、削除されたバージョンに解決できない場合、NuGet では最適な一致が検索されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-190">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="87d86-191">ロック ファイルの有効化</span><span class="sxs-lookup"><span data-stu-id="87d86-191">Enabling lock file</span></span>
<span data-ttu-id="87d86-192">パッケージの依存関係の完全なクロージャーを保持するために、プロジェクトに対して MSBuild プロパティ `RestorePackagesWithLockFile` を設定して、ロック ファイル機能にオプトインすることができます。</span><span class="sxs-lookup"><span data-stu-id="87d86-192">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="87d86-193">このプロパティが設定されている場合、NuGet の復元でロック ファイル (すべてのパッケージの依存関係を一覧表示する `packages.lock.json` ファイル) が生成されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-193">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="87d86-194">プロジェクトのルート ディレクトリに `packages.lock.json` ファイルが含まれている場合、プロパティ `RestorePackagesWithLockFile` が設定されていない場合でも、常に復元でロック ファイルが使用されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-194">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="87d86-195">そのため、この機能にオプトインする別の方法は、プロジェクトのルート ディレクトリに空の `packages.lock.json` ファイルをダミーとして作成することです。</span><span class="sxs-lookup"><span data-stu-id="87d86-195">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="87d86-196">ロック ファイルでの `restore` の動作</span><span class="sxs-lookup"><span data-stu-id="87d86-196">`restore` behavior with lock file</span></span>
<span data-ttu-id="87d86-197">プロジェクトにロック ファイルが存在する場合、NuGet では `restore` を実行するためにこのロック ファイルが使用されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-197">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="87d86-198">プロジェクト ファイル (または依存プロジェクトのファイル) で言及されたパッケージの依存関係に変更があったかどうか確認するために、NuGet で簡単なチェックが行われます。変更がなかった場合は、ロック ファイルで言及されたパッケージを単純に復元します。</span><span class="sxs-lookup"><span data-stu-id="87d86-198">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="87d86-199">パッケージの依存関係を再評価することはありません。</span><span class="sxs-lookup"><span data-stu-id="87d86-199">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="87d86-200">NuGet によって、プロジェクト ファイルで言及したような定義された依存関係の変更が検出された場合、パッケージ グラフが再評価され、プロジェクトの新しいパッケージ クロージャを反映するためにロック ファイルが更新されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-200">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="87d86-201">実行中にパッケージの依存関係を変更したくない CI/CD やその他のシナリオでは、`lockedmode` を `true` に設定することでこれを実行できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-201">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="87d86-202">dotnet.exe の場合は、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="87d86-202">For dotnet.exe, run:</span></span>
```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="87d86-203">msbuild.exe の場合は、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="87d86-203">For msbuild.exe, run:</span></span>
```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="87d86-204">自分のプロジェクト ファイルにもこの条件付き MSBuild プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-204">You may also set this conditional MSBuild property in your project file:</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="87d86-205">ロック モードが `true` である場合、復元ではロック ファイルに記載されている正確なパッケージが復元されるか、または、ロック ファイルの作成後にプロジェクトの定義されたパッケージの依存関係を更新した場合は、失敗します。</span><span class="sxs-lookup"><span data-stu-id="87d86-205">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="87d86-206">ロック ファイルをソース リポジトリの一部にする</span><span class="sxs-lookup"><span data-stu-id="87d86-206">Make lock file part of your source repository</span></span>
<span data-ttu-id="87d86-207">アプリケーションを作成する場合、目的の実行可能ファイルとプロジェクトは依存関係チェーンの最初に位置します。NuGet が復元中にこれを使用できるように、ロック ファイルをソース コード リポジトリにチェックインします。</span><span class="sxs-lookup"><span data-stu-id="87d86-207">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="87d86-208">ただし、当該プロジェクトが出荷しないライブラリ プロジェクトである場合や、他のプロジェクトが依存する共通コード プロジェクトである場合は、ソース コードの一部としてロック ファイルをチェックイン**しないでください**。</span><span class="sxs-lookup"><span data-stu-id="87d86-208">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="87d86-209">ロック ファイルを保持しても問題はありませんが、共通コード プロジェクトのロックされているパッケージの依存関係は、ロック ファイル内で記載されているように、この共通コード プロジェクトに依存するプロジェクトの復元/ビルド中に使用されない場合があります。</span><span class="sxs-lookup"><span data-stu-id="87d86-209">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="87d86-210">例:</span><span class="sxs-lookup"><span data-stu-id="87d86-210">Eg.</span></span>
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
<span data-ttu-id="87d86-211">`ProjectA` が `PackageX` のバージョン `2.0.0` に依存し、`PackageX` のバージョン `1.0.0` に依存する `ProjectB` も参照している場合、`ProjectB` のロック ファイルでは `PackageX` のバージョン `1.0.0` に対する依存関係が記載されます。</span><span class="sxs-lookup"><span data-stu-id="87d86-211">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="87d86-212">ただし、`ProjectA` をビルドすると、そのロック ファイルには `PackageX` のバージョン **`2.0.0`** に対する依存関係が含まれます。`ProjectB` のロック ファイルに記載されている `1.0.0` では**ありません**。</span><span class="sxs-lookup"><span data-stu-id="87d86-212">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="87d86-213">したがって、共通コード プロジェクトのロックファイルは、それが依存するプロジェクトのために解決されるパッケージに対して強い力を持っていません。</span><span class="sxs-lookup"><span data-stu-id="87d86-213">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="87d86-214">ロック ファイルの拡張機能</span><span class="sxs-lookup"><span data-stu-id="87d86-214">Lock file extensibility</span></span>
<span data-ttu-id="87d86-215">以下で説明するように、ロック ファイルを使用して復元のさまざまな動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-215">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="87d86-216">オプション</span><span class="sxs-lookup"><span data-stu-id="87d86-216">Option</span></span> | <span data-ttu-id="87d86-217">対応する MSBuild オプション</span><span class="sxs-lookup"><span data-stu-id="87d86-217">MSBuild equivalent option</span></span> | 
|:---  |:--- |
| `--use-lock-file` | <span data-ttu-id="87d86-218">プロジェクトのロック ファイルでのブートス トラップの使用です。</span><span class="sxs-lookup"><span data-stu-id="87d86-218">Bootstraps use of lock file for a project.</span></span> <span data-ttu-id="87d86-219">代わりに、プロジェクト ファイル内で `RestorePackagesWithLockFile` プロパティを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="87d86-219">You can alternatively set `RestorePackagesWithLockFile` property in the project file</span></span> | 
| `--locked-mode` | <span data-ttu-id="87d86-220">復元のロック モードを有効にします。</span><span class="sxs-lookup"><span data-stu-id="87d86-220">Enables locked mode for restore.</span></span> <span data-ttu-id="87d86-221">これは、繰り返し可能なビルドを取得する必要がある CI/CD のシナリオで役立ちます。</span><span class="sxs-lookup"><span data-stu-id="87d86-221">This is useful in CI/CD scenarios where you would like to get the repeatable builds.</span></span> <span data-ttu-id="87d86-222">または、`RestoreLockedMode` MSBuild プロパティを `true` に設定する方法もあります。</span><span class="sxs-lookup"><span data-stu-id="87d86-222">This can be also by setting the `RestoreLockedMode` MSBuild property to `true`</span></span> |  
| `--force-evaluate` | <span data-ttu-id="87d86-223">このオプションは、プロジェクトで定義する浮動バージョンを使用するパッケージで役立ちます。</span><span class="sxs-lookup"><span data-stu-id="87d86-223">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="87d86-224">既定では、NuGet の復元では、`--force-evaluate` オプションを使用して復元を実行しない限り、各復元に基づくパッケージ バージョンの自動更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="87d86-224">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with `--force-evaluate` option.</span></span> |
| `--lock-file-path` | <span data-ttu-id="87d86-225">プロジェクトのカスタム ロック ファイルの場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="87d86-225">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="87d86-226">これは、MSBuild プロパティ `NuGetLockFilePath` を設定することでも実現できます。</span><span class="sxs-lookup"><span data-stu-id="87d86-226">This can be also achieved by setting the MSBuild property `NuGetLockFilePath`.</span></span> <span data-ttu-id="87d86-227">既定では、NuGet はルート ディレクトリでの `packages.lock.json` をサポートします。</span><span class="sxs-lookup"><span data-stu-id="87d86-227">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="87d86-228">同じディレクトリ内に複数のプロジェクトがある場合、NuGet はプロジェクト固有のロック ファイル `packages.<project_name>.lock.json` をサポートします。</span><span class="sxs-lookup"><span data-stu-id="87d86-228">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
