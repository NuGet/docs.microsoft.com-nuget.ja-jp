---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照)
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237641"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="17419-103">プロジェクト ファイルのパッケージ参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="17419-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="17419-104">`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。</span><span class="sxs-lookup"><span data-stu-id="17419-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="17419-105">PackageReference を使用する場合、呼び出されても、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.config` ファイルの設定が、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」で説明されているように引き続き適用されます。</span><span class="sxs-lookup"><span data-stu-id="17419-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="17419-106">PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワークまたはその他のグループ化ごとにパッケージ参照を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="17419-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="17419-107">依存関係とコンテンツ フローを細かく制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="17419-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="17419-108">(詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="17419-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="17419-109">プロジェクトの種類のサポート</span><span class="sxs-lookup"><span data-stu-id="17419-109">Project type support</span></span>

<span data-ttu-id="17419-110">既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。</span><span class="sxs-lookup"><span data-stu-id="17419-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="17419-111">.NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。</span><span class="sxs-lookup"><span data-stu-id="17419-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="17419-112">PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに "[移行](../consume-packages/migrate-packages-config-to-package-reference.md)" してから、packages.config を削除します。</span><span class="sxs-lookup"><span data-stu-id="17419-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="17419-113">完全な .NET Framework を対象とする ASP.NET アプリには、PackageReference の[制限されたサポート](https://github.com/NuGet/Home/issues/5877)しか追加されません。</span><span class="sxs-lookup"><span data-stu-id="17419-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="17419-114">C++ および JavaScript のプロジェクト タイプはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="17419-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="17419-115">PackageReference を追加する</span><span class="sxs-lookup"><span data-stu-id="17419-115">Adding a PackageReference</span></span>

<span data-ttu-id="17419-116">次の構文を使用し、プロジェクト ファイルに依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="17419-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="17419-117">依存関係のバージョンを制御する</span><span class="sxs-lookup"><span data-stu-id="17419-117">Controlling dependency version</span></span>

<span data-ttu-id="17419-118">パッケージのバージョンを指定するための規則は、`packages.config` を使用する場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="17419-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="17419-119">上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../concepts/package-versioning.md#version-ranges)」 (パッケージ バージョン) にあります。</span><span class="sxs-lookup"><span data-stu-id="17419-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="17419-120">PackageReference のないプロジェクトに PackageReference を使用する</span><span class="sxs-lookup"><span data-stu-id="17419-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="17419-121">詳細: プロジェクトにパッケージをインストールしていないが (プロジェクト ファイルに PackageReferences がなく、packages.config ファイルがない)、プロジェクトを PackageReference スタイルで復元する場合、プロジェクト ファイルで Project プロパティ RestoreProjectStyle を PackageReference に設定できます。</span><span class="sxs-lookup"><span data-stu-id="17419-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="17419-122">PackageReference スタイル (既存の csproj または SDK スタイルのプロジェクト) のプロジェクトを参照するとき、この設定が便利になることがあります。</span><span class="sxs-lookup"><span data-stu-id="17419-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="17419-123">そのようなプロジェクトが参照するパッケージを他のプロジェクトで "推移的に" 参照できます。</span><span class="sxs-lookup"><span data-stu-id="17419-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="17419-124">PackageReference とソース</span><span class="sxs-lookup"><span data-stu-id="17419-124">PackageReference and sources</span></span>

<span data-ttu-id="17419-125">PackageReference プロジェクトでは、推移的な依存関係バージョンは復元時に解決されます。</span><span class="sxs-lookup"><span data-stu-id="17419-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="17419-126">そのため、PackageReference プロジェクトでは、すべてのソースがすべての復元に使用できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="17419-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="17419-127">最新バージョン</span><span class="sxs-lookup"><span data-stu-id="17419-127">Floating Versions</span></span>

<span data-ttu-id="17419-128">[最新バージョン](../concepts/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="17419-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="17419-129">依存関係アセットを制御する</span><span class="sxs-lookup"><span data-stu-id="17419-129">Controlling dependency assets</span></span>

<span data-ttu-id="17419-130">開発ハーネスとしてのみ依存関係を使用するとき、それはパッケージを使用するプロジェクトに公開しないほうが好ましい場合があります。</span><span class="sxs-lookup"><span data-stu-id="17419-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="17419-131">このシナリオでは、`PrivateAssets` メタデータを使用し、この動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="17419-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="17419-132">次のメタデータ タグは依存関係アセットを制御します。</span><span class="sxs-lookup"><span data-stu-id="17419-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="17419-133">タグ</span><span class="sxs-lookup"><span data-stu-id="17419-133">Tag</span></span> | <span data-ttu-id="17419-134">説明</span><span class="sxs-lookup"><span data-stu-id="17419-134">Description</span></span> | <span data-ttu-id="17419-135">Default value</span><span class="sxs-lookup"><span data-stu-id="17419-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="17419-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="17419-136">IncludeAssets</span></span> | <span data-ttu-id="17419-137">これらのアセットは使用されます</span><span class="sxs-lookup"><span data-stu-id="17419-137">These assets will be consumed</span></span> | <span data-ttu-id="17419-138">すべて</span><span class="sxs-lookup"><span data-stu-id="17419-138">all</span></span> |
| <span data-ttu-id="17419-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="17419-139">ExcludeAssets</span></span> | <span data-ttu-id="17419-140">これらのアセットは使用されません</span><span class="sxs-lookup"><span data-stu-id="17419-140">These assets will not be consumed</span></span> | <span data-ttu-id="17419-141">なし</span><span class="sxs-lookup"><span data-stu-id="17419-141">none</span></span> |
| <span data-ttu-id="17419-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="17419-142">PrivateAssets</span></span> | <span data-ttu-id="17419-143">これらのアセットは使用されますが、親プロジェクトに流れません</span><span class="sxs-lookup"><span data-stu-id="17419-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="17419-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="17419-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="17419-145">これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。</span><span class="sxs-lookup"><span data-stu-id="17419-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="17419-146">値</span><span class="sxs-lookup"><span data-stu-id="17419-146">Value</span></span> | <span data-ttu-id="17419-147">説明</span><span class="sxs-lookup"><span data-stu-id="17419-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="17419-148">compile</span><span class="sxs-lookup"><span data-stu-id="17419-148">compile</span></span> | <span data-ttu-id="17419-149">`lib` フォルダーの内容と、プロジェクトをフォルダー内のアセンブリに対してコンパイルできるかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="17419-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="17419-150">runtime</span><span class="sxs-lookup"><span data-stu-id="17419-150">runtime</span></span> | <span data-ttu-id="17419-151">`lib` と `runtimes` フォルダーの内容と、これらのアセンブリがコピーされて出力ディレクトリをビルドするかどうかのコントロール</span><span class="sxs-lookup"><span data-stu-id="17419-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="17419-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="17419-152">contentFiles</span></span> | <span data-ttu-id="17419-153">`contentfiles` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="17419-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="17419-154">build</span><span class="sxs-lookup"><span data-stu-id="17419-154">build</span></span> | <span data-ttu-id="17419-155">`build` フォルダー内の `.props` と `.targets`</span><span class="sxs-lookup"><span data-stu-id="17419-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="17419-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="17419-156">buildMultitargeting</span></span> | <span data-ttu-id="17419-157">*(4.0)* `.props` フォルダー内の `.targets` と `buildMultitargeting` (フレームワーク間でのターゲット設定用)</span><span class="sxs-lookup"><span data-stu-id="17419-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="17419-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="17419-158">buildTransitive</span></span> | <span data-ttu-id="17419-159">*(5.0 以降)* `.props` フォルダー内の `.targets` と `buildTransitive` (使用するプロジェクトに推移的にフローするアセット用)。</span><span class="sxs-lookup"><span data-stu-id="17419-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="17419-160">[機能](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="17419-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="17419-161">analyzers</span><span class="sxs-lookup"><span data-stu-id="17419-161">analyzers</span></span> | <span data-ttu-id="17419-162">.NET アナライザー</span><span class="sxs-lookup"><span data-stu-id="17419-162">.NET analyzers</span></span> |
| <span data-ttu-id="17419-163">native</span><span class="sxs-lookup"><span data-stu-id="17419-163">native</span></span> | <span data-ttu-id="17419-164">`native` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="17419-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="17419-165">なし</span><span class="sxs-lookup"><span data-stu-id="17419-165">none</span></span> | <span data-ttu-id="17419-166">上記のいずれも該当しない。</span><span class="sxs-lookup"><span data-stu-id="17419-166">None of the above are used.</span></span> |
| <span data-ttu-id="17419-167">すべて</span><span class="sxs-lookup"><span data-stu-id="17419-167">all</span></span> | <span data-ttu-id="17419-168">上記のすべて (`none` を除く)</span><span class="sxs-lookup"><span data-stu-id="17419-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="17419-169">次の例では、パッケージからのコンテンツ ファイルを除くすべてがプロジェクトによって使用され、コンテンツ ファイルとアナライザーを除くすべてが親プロジェクトに流れます。</span><span class="sxs-lookup"><span data-stu-id="17419-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="17419-170">`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに *流れる* ことに注目してください。</span><span class="sxs-lookup"><span data-stu-id="17419-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="17419-171">たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="17419-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="17419-172">AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。</span><span class="sxs-lookup"><span data-stu-id="17419-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="17419-173">`.nuspec` ファイル内で `developmentDependency` が `true` に設定されている場合、パッケージが開発専用の依存関係としてマークされます。これにより、そのパッケージは他のパッケージに依存関係として含まれなくなります。</span><span class="sxs-lookup"><span data-stu-id="17419-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="17419-174">PackageReference *(NuGet 4.8 以降)* では、このフラグは、コンパイルからコンパイル時アセットを除外することも意味します。</span><span class="sxs-lookup"><span data-stu-id="17419-174">With PackageReference *(NuGet 4.8+)* , this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="17419-175">詳しくは、「[DevelopmentDependency support for PackageReference (PackageReference に対する DevelopmentDependency のサポート)](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="17419-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="17419-176">PackageReference 条件を追加する</span><span class="sxs-lookup"><span data-stu-id="17419-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="17419-177">条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。</span><span class="sxs-lookup"><span data-stu-id="17419-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="17419-178">ただし、現在のところ `TargetFramework` 変数のみに対応しています。</span><span class="sxs-lookup"><span data-stu-id="17419-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="17419-179">たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。</span><span class="sxs-lookup"><span data-stu-id="17419-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="17419-180">その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。</span><span class="sxs-lookup"><span data-stu-id="17419-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="17419-181">それを回避するために、次のように `PackageReference` で条件を指定します。</span><span class="sxs-lookup"><span data-stu-id="17419-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="17419-182">このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。</span><span class="sxs-lookup"><span data-stu-id="17419-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

<span data-ttu-id="17419-184">条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。</span><span class="sxs-lookup"><span data-stu-id="17419-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="17419-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="17419-185">GeneratePathProperty</span></span>

<span data-ttu-id="17419-186">この機能を使用できるのは、NuGet **5.0** 以降で、かつ Visual Studio 2019 **16.0** 以降を使用している場合です。</span><span class="sxs-lookup"><span data-stu-id="17419-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="17419-187">場合によっては、MSBuild ターゲットからパッケージ内のファイルを参照することが望ましい場合があります。</span><span class="sxs-lookup"><span data-stu-id="17419-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="17419-188">`packages.config` ベースのプロジェクトでは、パッケージは、プロジェク トファイルに対して相対的なフォルダーにインストールされます。</span><span class="sxs-lookup"><span data-stu-id="17419-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="17419-189">ただし、PackageReference では、パッケージは " *グローバルパッケージ* " フォルダーから [使用](../concepts/package-installation-process.md)されます。このフォルダーは、マシンごとに異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="17419-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="17419-190">このギャップを埋めるために、NuGet では、パッケージの使用元となる場所を指すプロパティが導入されました。</span><span class="sxs-lookup"><span data-stu-id="17419-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="17419-191">例:</span><span class="sxs-lookup"><span data-stu-id="17419-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="17419-192">また、NuGet では、ツール フォルダーを含むパッケージのプロパティが自動的に生成されます。</span><span class="sxs-lookup"><span data-stu-id="17419-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="17419-193">MSBuild のプロパティとパッケージ ID には同じ制限がないため、パッケージ ID を MSBuild の表示名 (`Pkg` という語が接頭辞として付けられます) に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="17419-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="17419-194">生成されたプロパティの正確な名前を確認するには、生成された [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) ファイルを調べます。</span><span class="sxs-lookup"><span data-stu-id="17419-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="17419-195">NuGet の警告とエラー</span><span class="sxs-lookup"><span data-stu-id="17419-195">NuGet warnings and errors</span></span>

<span data-ttu-id="17419-196">" *この機能を使用できるのは、NuGet **4.3** 以降で、かつ Visual Studio 2017 **15.3** 以降を使用している場合です。* "</span><span class="sxs-lookup"><span data-stu-id="17419-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="17419-197">多くのパックと復元シナリオでは、すべての NuGet の警告とエラーがコード化され、`NU****` から始まります。</span><span class="sxs-lookup"><span data-stu-id="17419-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="17419-198">すべての NuGet の警告とエラーは、[リファレンス](../reference/errors-and-warnings.md) ドキュメントに記載されています。</span><span class="sxs-lookup"><span data-stu-id="17419-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="17419-199">NuGet では、次の警告プロパティが監視されます。</span><span class="sxs-lookup"><span data-stu-id="17419-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="17419-200">`TreatWarningsAsErrors`: すべての警告をエラーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="17419-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="17419-201">`WarningsAsErrors`: 指定した警告をエラーとして扱います。</span><span class="sxs-lookup"><span data-stu-id="17419-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="17419-202">`NoWarn`: 特定の警告を非表示にします (プロジェクト全体またはパッケージ全体)。</span><span class="sxs-lookup"><span data-stu-id="17419-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="17419-203">例 :</span><span class="sxs-lookup"><span data-stu-id="17419-203">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="17419-204">NuGet 警告の非表示</span><span class="sxs-lookup"><span data-stu-id="17419-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="17419-205">パックと復元操作中にすべての NuGet 警告を解決することをお勧めしますが、特定の状況では、それらを非表示にすることが認められています。</span><span class="sxs-lookup"><span data-stu-id="17419-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="17419-206">プロジェクト全体で警告を非表示にするには、次のことを検討してください。</span><span class="sxs-lookup"><span data-stu-id="17419-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="17419-207">警告は、グラフ内の特定のパッケージにのみ適用されることがあります。</span><span class="sxs-lookup"><span data-stu-id="17419-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="17419-208">PackageReference 項目に `NoWarn` を追加することで、その警告をより選択的に非表示にすることができます。</span><span class="sxs-lookup"><span data-stu-id="17419-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="17419-209">Visual Studio での NuGet パッケージ警告の非表示</span><span class="sxs-lookup"><span data-stu-id="17419-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="17419-210">Visual Studio では、IDE から[警告を非表示にする](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
)こともできます。</span><span class="sxs-lookup"><span data-stu-id="17419-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="17419-211">依存関係のロック</span><span class="sxs-lookup"><span data-stu-id="17419-211">Locking dependencies</span></span>

<span data-ttu-id="17419-212">" *この機能を使用できるのは、NuGet **4.9** 以降で、かつ Visual Studio 2017 **15.9** 以降を使用している場合です。* "</span><span class="sxs-lookup"><span data-stu-id="17419-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="17419-213">NuGet の復元への入力は、プロジェクト ファイルのパッケージ参照のセット (最上位レベルまたは直接の依存関係) であり、出力は推移的依存関係を含むパッケージのすべての依存関係の完全なクロージャーです。</span><span class="sxs-lookup"><span data-stu-id="17419-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="17419-214">入力の PackageReference リストが変更されていない場合、NuGet では常に同じパッケージの依存関係の完全なクロージャーを生成しようとします。</span><span class="sxs-lookup"><span data-stu-id="17419-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="17419-215">ただし、このようにすることができないシナリオがいくつかあります。</span><span class="sxs-lookup"><span data-stu-id="17419-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="17419-216">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="17419-216">For example:</span></span>

* <span data-ttu-id="17419-217">`<PackageReference Include="My.Sample.Lib" Version="4.*"/>` などの浮動バージョンを使用する場合。</span><span class="sxs-lookup"><span data-stu-id="17419-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="17419-218">ここでの意図はパッケージの復元ごとに最新バージョンに浮動することですが、グラフを特定の最新バージョンにロックして、利用可能な場合は明示的なジェスチャに基づいて後続のバージョンに浮動させることをユーザーが求めるシナリオがあります。</span><span class="sxs-lookup"><span data-stu-id="17419-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="17419-219">PackageReference のバージョン要件と一致する新しいパッケージのバージョンが公開されている場合。</span><span class="sxs-lookup"><span data-stu-id="17419-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="17419-220">例:</span><span class="sxs-lookup"><span data-stu-id="17419-220">E.g.</span></span> 

  * <span data-ttu-id="17419-221">1 日目: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` を指定したが、NuGet リポジトリで利用可能なバージョンが 4.1.0、4.2.0 および 4.3.0 だった場合。</span><span class="sxs-lookup"><span data-stu-id="17419-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="17419-222">この場合、NuGet は 4.1.0 (最小に最も近いバージョン) に解決されています。</span><span class="sxs-lookup"><span data-stu-id="17419-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="17419-223">2 日目: バージョン 4.0.0 が公開されます。</span><span class="sxs-lookup"><span data-stu-id="17419-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="17419-224">NuGet では完全一致が検索され、4.0.0 への解決が始められます。</span><span class="sxs-lookup"><span data-stu-id="17419-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="17419-225">指定したパッケージ バージョンがリポジトリから削除される場合。</span><span class="sxs-lookup"><span data-stu-id="17419-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="17419-226">nuget.org ではパッケージの削除が許可されていませんが、すべてのパッケージ リポジトリがこの制約を持っているわけではありません。</span><span class="sxs-lookup"><span data-stu-id="17419-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="17419-227">これにより、削除されたバージョンに解決できない場合、NuGet では最適な一致が検索されます。</span><span class="sxs-lookup"><span data-stu-id="17419-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="17419-228">ロック ファイルの有効化</span><span class="sxs-lookup"><span data-stu-id="17419-228">Enabling lock file</span></span>

<span data-ttu-id="17419-229">パッケージの依存関係の完全なクロージャーを保持するために、プロジェクトに対して MSBuild プロパティ `RestorePackagesWithLockFile` を設定して、ロック ファイル機能にオプトインすることができます。</span><span class="sxs-lookup"><span data-stu-id="17419-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="17419-230">このプロパティが設定されている場合、NuGet の復元でロック ファイル (すべてのパッケージの依存関係を一覧表示する `packages.lock.json` ファイル) が生成されます。</span><span class="sxs-lookup"><span data-stu-id="17419-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="17419-231">プロジェクトのルート ディレクトリに `packages.lock.json` ファイルが含まれている場合、プロパティ `RestorePackagesWithLockFile` が設定されていない場合でも、常に復元でロック ファイルが使用されます。</span><span class="sxs-lookup"><span data-stu-id="17419-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="17419-232">そのため、この機能にオプトインする別の方法は、プロジェクトのルート ディレクトリに空の `packages.lock.json` ファイルをダミーとして作成することです。</span><span class="sxs-lookup"><span data-stu-id="17419-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="17419-233">ロック ファイルでの `restore` の動作</span><span class="sxs-lookup"><span data-stu-id="17419-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="17419-234">プロジェクトにロック ファイルが存在する場合、NuGet では `restore` を実行するためにこのロック ファイルが使用されます。</span><span class="sxs-lookup"><span data-stu-id="17419-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="17419-235">プロジェクト ファイル (または依存プロジェクトのファイル) で言及されたパッケージの依存関係に変更があったかどうか確認するために、NuGet で簡単なチェックが行われます。変更がなかった場合は、ロック ファイルで言及されたパッケージを単純に復元します。</span><span class="sxs-lookup"><span data-stu-id="17419-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="17419-236">パッケージの依存関係を再評価することはありません。</span><span class="sxs-lookup"><span data-stu-id="17419-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="17419-237">NuGet によって、プロジェクト ファイルで言及したような定義された依存関係の変更が検出された場合、パッケージ グラフが再評価され、プロジェクトの新しいパッケージ クロージャを反映するためにロック ファイルが更新されます。</span><span class="sxs-lookup"><span data-stu-id="17419-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="17419-238">実行中にパッケージの依存関係を変更したくない CI/CD やその他のシナリオでは、`lockedmode` を `true` に設定することでこれを実行できます。</span><span class="sxs-lookup"><span data-stu-id="17419-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="17419-239">dotnet.exe の場合は、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="17419-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="17419-240">msbuild.exe の場合は、次を実行します。</span><span class="sxs-lookup"><span data-stu-id="17419-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="17419-241">自分のプロジェクト ファイルにもこの条件付き MSBuild プロパティを設定できます。</span><span class="sxs-lookup"><span data-stu-id="17419-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="17419-242">ロック モードが `true` である場合、復元ではロック ファイルに記載されている正確なパッケージが復元されるか、または、ロック ファイルの作成後にプロジェクトの定義されたパッケージの依存関係を更新した場合は、失敗します。</span><span class="sxs-lookup"><span data-stu-id="17419-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="17419-243">ロック ファイルをソース リポジトリの一部にする</span><span class="sxs-lookup"><span data-stu-id="17419-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="17419-244">アプリケーションを作成する場合、目的の実行可能ファイルとプロジェクトは依存関係チェーンの最初に位置します。NuGet が復元中にこれを使用できるように、ロック ファイルをソース コード リポジトリにチェックインします。</span><span class="sxs-lookup"><span data-stu-id="17419-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="17419-245">ただし、当該プロジェクトが出荷しないライブラリ プロジェクトである場合や、他のプロジェクトが依存する共通コード プロジェクトである場合は、ソース コードの一部としてロック ファイルをチェックイン **しないでください** 。</span><span class="sxs-lookup"><span data-stu-id="17419-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="17419-246">ロック ファイルを保持しても問題はありませんが、共通コード プロジェクトのロックされているパッケージの依存関係は、ロック ファイル内で記載されているように、この共通コード プロジェクトに依存するプロジェクトの復元/ビルド中に使用されない場合があります。</span><span class="sxs-lookup"><span data-stu-id="17419-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="17419-247">例:</span><span class="sxs-lookup"><span data-stu-id="17419-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="17419-248">`ProjectA` が `PackageX` のバージョン `2.0.0` に依存し、`PackageX` のバージョン `1.0.0` に依存する `ProjectB` も参照している場合、`ProjectB` のロック ファイルでは `PackageX` のバージョン `1.0.0` に対する依存関係が記載されます。</span><span class="sxs-lookup"><span data-stu-id="17419-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="17419-249">ただし、`ProjectA` をビルドすると、そのロック ファイルには `PackageX` のバージョン **`2.0.0`** に対する依存関係が含まれます。 **のロック ファイルに記載されている** では`1.0.0`ありません`ProjectB`。</span><span class="sxs-lookup"><span data-stu-id="17419-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="17419-250">したがって、共通コード プロジェクトのロックファイルは、それが依存するプロジェクトのために解決されるパッケージに対して強い力を持っていません。</span><span class="sxs-lookup"><span data-stu-id="17419-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="17419-251">ロック ファイルの拡張機能</span><span class="sxs-lookup"><span data-stu-id="17419-251">Lock file extensibility</span></span>

<span data-ttu-id="17419-252">以下で説明するように、ロック ファイルを使用して復元のさまざまな動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="17419-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="17419-253">NuGet.exe オプション</span><span class="sxs-lookup"><span data-stu-id="17419-253">NuGet.exe option</span></span> | <span data-ttu-id="17419-254">dotnet オプション</span><span class="sxs-lookup"><span data-stu-id="17419-254">dotnet option</span></span> | <span data-ttu-id="17419-255">対応する MSBuild オプション</span><span class="sxs-lookup"><span data-stu-id="17419-255">MSBuild equivalent option</span></span> | <span data-ttu-id="17419-256">説明</span><span class="sxs-lookup"><span data-stu-id="17419-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="17419-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="17419-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="17419-258">ロック ファイルの使用をオプトインします。</span><span class="sxs-lookup"><span data-stu-id="17419-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="17419-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="17419-259">RestoreLockedMode</span></span> | <span data-ttu-id="17419-260">復元のロック モードを有効にします。</span><span class="sxs-lookup"><span data-stu-id="17419-260">Enables locked mode for restore.</span></span> <span data-ttu-id="17419-261">これは、繰り返し可能なビルドを必要とする CI/CD のシナリオで役立ちます。</span><span class="sxs-lookup"><span data-stu-id="17419-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="17419-262">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="17419-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="17419-263">このオプションは、プロジェクトで定義する浮動バージョンを使用するパッケージで役立ちます。</span><span class="sxs-lookup"><span data-stu-id="17419-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="17419-264">既定では、NuGet の復元では、このオプションを指定して復元を実行しない限り、復元ごとのパッケージ バージョンの自動更新は行われません。</span><span class="sxs-lookup"><span data-stu-id="17419-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="17419-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="17419-265">NuGetLockFilePath</span></span> | <span data-ttu-id="17419-266">プロジェクトのカスタム ロック ファイルの場所を定義します。</span><span class="sxs-lookup"><span data-stu-id="17419-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="17419-267">既定では、NuGet はルート ディレクトリでの `packages.lock.json` をサポートします。</span><span class="sxs-lookup"><span data-stu-id="17419-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="17419-268">同じディレクトリ内に複数のプロジェクトがある場合、NuGet はプロジェクト固有のロック ファイル `packages.<project_name>.lock.json` をサポートします。</span><span class="sxs-lookup"><span data-stu-id="17419-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
