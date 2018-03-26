---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照) | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
keywords: NuGet パッケージの依存関係、パッケージ参照、プロジェクト ファイル、PackageReference、packages.config、VS2017、Visual Studio 2017、NuGet 4、.NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: e1880c9b294e19ef1b71c7b17b02df8ff1cf1b73
ms.sourcegitcommit: 718e6cb88e45fa07c85d653f216bf92eaaf81625
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/20/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="c2ee8-104">プロジェクト ファイルのパッケージ参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="c2ee8-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="c2ee8-105">`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="c2ee8-106">PackageReference の呼び出しは、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.Config` ファイルの設定が適用されます。詳細については、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="c2ee8-107">PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="c2ee8-108">依存関係とコンテンツ フローを細かく制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="c2ee8-109">(詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="c2ee8-110">既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="c2ee8-111">完全な .NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="c2ee8-112">PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに移行し、packages.config を削除します。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="c2ee8-113">PackageReference を追加する</span><span class="sxs-lookup"><span data-stu-id="c2ee8-113">Adding a PackageReference</span></span>

<span data-ttu-id="c2ee8-114">次の構文を使用し、プロジェクト ファイルに依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="c2ee8-115">依存関係のバージョンを制御する</span><span class="sxs-lookup"><span data-stu-id="c2ee8-115">Controlling dependency version</span></span>

<span data-ttu-id="c2ee8-116">パッケージのバージョンを指定するための規則は、`packages.config` を使用する場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c2ee8-117">上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」 (パッケージ バージョン) にあります。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="c2ee8-118">最新バージョン</span><span class="sxs-lookup"><span data-stu-id="c2ee8-118">Floating Versions</span></span>

<span data-ttu-id="c2ee8-119">[最新バージョン](../consume-packages/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="c2ee8-120">依存関係アセットを制御する</span><span class="sxs-lookup"><span data-stu-id="c2ee8-120">Controlling dependency assets</span></span>

<span data-ttu-id="c2ee8-121">開発ハーネスとしてのみ依存関係を使用するとき、それはパッケージを使用するプロジェクトに公開しないほうが好ましい場合があります。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="c2ee8-122">このシナリオでは、`PrivateAssets` メタデータを使用し、この動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c2ee8-123">次のメタデータ タグは依存関係アセットを制御します。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="c2ee8-124">タグ</span><span class="sxs-lookup"><span data-stu-id="c2ee8-124">Tag</span></span> | <span data-ttu-id="c2ee8-125">説明</span><span class="sxs-lookup"><span data-stu-id="c2ee8-125">Description</span></span> | <span data-ttu-id="c2ee8-126">既定値</span><span class="sxs-lookup"><span data-stu-id="c2ee8-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c2ee8-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="c2ee8-127">IncludeAssets</span></span> | <span data-ttu-id="c2ee8-128">これらのアセットは使用されます</span><span class="sxs-lookup"><span data-stu-id="c2ee8-128">These assets will be consumed</span></span> | <span data-ttu-id="c2ee8-129">すべて</span><span class="sxs-lookup"><span data-stu-id="c2ee8-129">all</span></span> |
| <span data-ttu-id="c2ee8-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="c2ee8-130">ExcludeAssets</span></span> | <span data-ttu-id="c2ee8-131">これらのアセットは使用されません</span><span class="sxs-lookup"><span data-stu-id="c2ee8-131">These assets will not be consumed</span></span> | <span data-ttu-id="c2ee8-132">none</span><span class="sxs-lookup"><span data-stu-id="c2ee8-132">none</span></span> |
| <span data-ttu-id="c2ee8-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="c2ee8-133">PrivateAssets</span></span> | <span data-ttu-id="c2ee8-134">これらのアセットは使用されますが、親プロジェクトに流れません</span><span class="sxs-lookup"><span data-stu-id="c2ee8-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="c2ee8-135">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="c2ee8-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="c2ee8-136">これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="c2ee8-137">[値]</span><span class="sxs-lookup"><span data-stu-id="c2ee8-137">Value</span></span> | <span data-ttu-id="c2ee8-138">説明</span><span class="sxs-lookup"><span data-stu-id="c2ee8-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="c2ee8-139">compile</span><span class="sxs-lookup"><span data-stu-id="c2ee8-139">compile</span></span> | <span data-ttu-id="c2ee8-140">`lib` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="c2ee8-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="c2ee8-141">ランタイム</span><span class="sxs-lookup"><span data-stu-id="c2ee8-141">runtime</span></span> | <span data-ttu-id="c2ee8-142">`runtimes` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="c2ee8-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="c2ee8-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="c2ee8-143">contentFiles</span></span> | <span data-ttu-id="c2ee8-144">`contentfiles` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="c2ee8-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="c2ee8-145">ビルド</span><span class="sxs-lookup"><span data-stu-id="c2ee8-145">build</span></span> | <span data-ttu-id="c2ee8-146">`build` フォルダーの props と targets</span><span class="sxs-lookup"><span data-stu-id="c2ee8-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="c2ee8-147">analyzers</span><span class="sxs-lookup"><span data-stu-id="c2ee8-147">analyzers</span></span> | <span data-ttu-id="c2ee8-148">.NET アナライザー</span><span class="sxs-lookup"><span data-stu-id="c2ee8-148">.NET analyzers</span></span> |
| <span data-ttu-id="c2ee8-149">native</span><span class="sxs-lookup"><span data-stu-id="c2ee8-149">native</span></span> | <span data-ttu-id="c2ee8-150">`native` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="c2ee8-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="c2ee8-151">none</span><span class="sxs-lookup"><span data-stu-id="c2ee8-151">none</span></span> | <span data-ttu-id="c2ee8-152">上記のいずれも該当しない。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-152">None of the above are used.</span></span> |
| <span data-ttu-id="c2ee8-153">すべて</span><span class="sxs-lookup"><span data-stu-id="c2ee8-153">all</span></span> | <span data-ttu-id="c2ee8-154">上記のすべて (`none` を除く)</span><span class="sxs-lookup"><span data-stu-id="c2ee8-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="c2ee8-155">次の例では、パッケージからのコンテンツ ファイルを除くすべてがプロジェクトによって使用され、コンテンツ ファイルとアナライザーを除くすべてが親プロジェクトに流れます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="c2ee8-156">`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに*流れる*ことに注目してください。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="c2ee8-157">たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="c2ee8-158">AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="c2ee8-159">PackageReference 条件を追加する</span><span class="sxs-lookup"><span data-stu-id="c2ee8-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="c2ee8-160">条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="c2ee8-161">ただし、現在のところ `TargetFramework` 変数のみに対応しています。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="c2ee8-162">たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="c2ee8-163">その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="c2ee8-164">それを回避するために、次のように `PackageReference` で条件を指定します。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="c2ee8-165">このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

<span data-ttu-id="c2ee8-167">条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。</span><span class="sxs-lookup"><span data-stu-id="c2ee8-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
