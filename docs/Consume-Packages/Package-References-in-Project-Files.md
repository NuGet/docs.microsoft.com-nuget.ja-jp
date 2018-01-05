---
title: "Visual Studio プロジェクト ファイルの NuGet PackageReference | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "NuGet 4.0+ と VS2017 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細"
keywords: "NuGet パッケージ依存性, パッケージ参照, プロジェクト ファイル, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="87cb2-104">プロジェクト ファイルのパッケージ参照 (PackageReference)</span><span class="sxs-lookup"><span data-stu-id="87cb2-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="87cb2-105">パッケージ参照では、`PackageReference` ノードを使用することで、プロジェクト ファイル内で直接、NuGet 依存関係を管理できます。個別の `packages.config` または `project.json` ファイルが不要になります。</span><span class="sxs-lookup"><span data-stu-id="87cb2-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="87cb2-106">この方法は NuGet の他の側面に影響を与えません。たとえば、`NuGet.Config` ファイルの設定は (パッケージ ソースを含む)、「[Configuring NuGet Behavior](Configuring-NuGet-Behavior.md)」 (NuGet 動作の構成) の説明にあるように、依然として適用されます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="87cb2-107">現在のところ、.NET Core プロジェクト、.NET Standard プロジェクト、Windows 10 Build 15063 (Creators Update) を対象とする UWP プロジェクトに関して、パッケージ参照は Visual Studio 2017 でのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="87cb2-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="87cb2-108">`PackageReference` 手法では、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択できます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="87cb2-109">依存関係とコンテンツ フローを細かく制御することもできます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="87cb2-110">動作と[依存関係の解決](Dependency-Resolution.md)の観点からは、`project.json` を使用する場合と同じになります。</span><span class="sxs-lookup"><span data-stu-id="87cb2-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it is the same as using `project.json`.</span></span>

<span data-ttu-id="87cb2-111">MSBuild とプロジェクト ファイルのパッケージ参照の統合については、「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md)」 (MSBuild ターゲットとしての NuGet pack および restore) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="87cb2-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="87cb2-112">PackageReference を追加する</span><span class="sxs-lookup"><span data-stu-id="87cb2-112">Adding a PackageReference</span></span>

<span data-ttu-id="87cb2-113">次の構文を使用し、プロジェクト ファイルに依存関係を追加します。</span><span class="sxs-lookup"><span data-stu-id="87cb2-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="87cb2-114">依存関係のバージョンを制御する</span><span class="sxs-lookup"><span data-stu-id="87cb2-114">Controlling dependency version</span></span>

<span data-ttu-id="87cb2-115">パッケージのバージョンを指定するための規則は、`packages.config` または `project.json` を使用する場合と同じです。</span><span class="sxs-lookup"><span data-stu-id="87cb2-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="87cb2-116">上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」 (パッケージ バージョン) にあります。</span><span class="sxs-lookup"><span data-stu-id="87cb2-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="87cb2-117">最新バージョン</span><span class="sxs-lookup"><span data-stu-id="87cb2-117">Floating Versions</span></span>

<span data-ttu-id="87cb2-118">[最新バージョン](../consume-packages/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。</span><span class="sxs-lookup"><span data-stu-id="87cb2-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="87cb2-119">依存関係アセットを制御する</span><span class="sxs-lookup"><span data-stu-id="87cb2-119">Controlling dependency assets</span></span>

<span data-ttu-id="87cb2-120">開発ハーネスとしてのみ依存関係を使用するとき、それはパッケージを使用するプロジェクトに公開しないほうが好ましい場合があります。</span><span class="sxs-lookup"><span data-stu-id="87cb2-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="87cb2-121">このシナリオでは、`PrivateAssets` メタデータを使用し、この動作を制御できます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="87cb2-122">次のメタデータ タグは依存関係アセットを制御します。</span><span class="sxs-lookup"><span data-stu-id="87cb2-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="87cb2-123">タグ</span><span class="sxs-lookup"><span data-stu-id="87cb2-123">Tag</span></span> | <span data-ttu-id="87cb2-124">説明</span><span class="sxs-lookup"><span data-stu-id="87cb2-124">Description</span></span> | <span data-ttu-id="87cb2-125">既定値</span><span class="sxs-lookup"><span data-stu-id="87cb2-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="87cb2-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="87cb2-126">IncludeAssets</span></span> | <span data-ttu-id="87cb2-127">これらのアセットは使用されます</span><span class="sxs-lookup"><span data-stu-id="87cb2-127">These assets will be consumed</span></span> | <span data-ttu-id="87cb2-128">すべて</span><span class="sxs-lookup"><span data-stu-id="87cb2-128">all</span></span> |
| <span data-ttu-id="87cb2-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="87cb2-129">ExcludeAssets</span></span> | <span data-ttu-id="87cb2-130">これらのアセットは使用されません</span><span class="sxs-lookup"><span data-stu-id="87cb2-130">These assets will not be consumed</span></span> | <span data-ttu-id="87cb2-131">none</span><span class="sxs-lookup"><span data-stu-id="87cb2-131">none</span></span> | 
| <span data-ttu-id="87cb2-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="87cb2-132">PrivateAssets</span></span> | <span data-ttu-id="87cb2-133">これらのアセットは使用されますが、親プロジェクトに流れません</span><span class="sxs-lookup"><span data-stu-id="87cb2-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="87cb2-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="87cb2-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="87cb2-135">これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="87cb2-136">値</span><span class="sxs-lookup"><span data-stu-id="87cb2-136">Value</span></span> | <span data-ttu-id="87cb2-137">説明</span><span class="sxs-lookup"><span data-stu-id="87cb2-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="87cb2-138">compile</span><span class="sxs-lookup"><span data-stu-id="87cb2-138">compile</span></span> | <span data-ttu-id="87cb2-139">`lib` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="87cb2-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="87cb2-140">ランタイム</span><span class="sxs-lookup"><span data-stu-id="87cb2-140">runtime</span></span> | <span data-ttu-id="87cb2-141">`runtime` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="87cb2-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="87cb2-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="87cb2-142">contentFiles</span></span> | <span data-ttu-id="87cb2-143">`contentfiles` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="87cb2-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="87cb2-144">ビルド</span><span class="sxs-lookup"><span data-stu-id="87cb2-144">build</span></span> | <span data-ttu-id="87cb2-145">`build` フォルダーの props と targets</span><span class="sxs-lookup"><span data-stu-id="87cb2-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="87cb2-146">analyzers</span><span class="sxs-lookup"><span data-stu-id="87cb2-146">analyzers</span></span> | <span data-ttu-id="87cb2-147">.NET アナライザー</span><span class="sxs-lookup"><span data-stu-id="87cb2-147">.NET analyzers</span></span> |
| <span data-ttu-id="87cb2-148">native</span><span class="sxs-lookup"><span data-stu-id="87cb2-148">native</span></span> | <span data-ttu-id="87cb2-149">`native` フォルダーの内容</span><span class="sxs-lookup"><span data-stu-id="87cb2-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="87cb2-150">none</span><span class="sxs-lookup"><span data-stu-id="87cb2-150">none</span></span> | <span data-ttu-id="87cb2-151">上記のいずれも該当しない。</span><span class="sxs-lookup"><span data-stu-id="87cb2-151">None of the above are used.</span></span> |
| <span data-ttu-id="87cb2-152">すべて</span><span class="sxs-lookup"><span data-stu-id="87cb2-152">all</span></span> | <span data-ttu-id="87cb2-153">上記のすべて (`none` を除く)</span><span class="sxs-lookup"><span data-stu-id="87cb2-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="87cb2-154">次の例では、パッケージからのコンテンツ ファイルを除くすべてがプロジェクトによって使用され、コンテンツ ファイルとアナライザーを除くすべてが親プロジェクトに流れます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="87cb2-155">`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに*流れる*ことに注目してください。</span><span class="sxs-lookup"><span data-stu-id="87cb2-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="87cb2-156">たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="87cb2-157">AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="87cb2-158">PackageReference 条件を追加する</span><span class="sxs-lookup"><span data-stu-id="87cb2-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="87cb2-159">条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="87cb2-160">ただし、現在のところ `TargetFramework` 変数のみに対応しています。</span><span class="sxs-lookup"><span data-stu-id="87cb2-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="87cb2-161">たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。</span><span class="sxs-lookup"><span data-stu-id="87cb2-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="87cb2-162">その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。</span><span class="sxs-lookup"><span data-stu-id="87cb2-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="87cb2-163">それを回避するために、次のように `PackageReference` で条件を指定します。</span><span class="sxs-lookup"><span data-stu-id="87cb2-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="87cb2-164">このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

<span data-ttu-id="87cb2-166">条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。</span><span class="sxs-lookup"><span data-stu-id="87cb2-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
