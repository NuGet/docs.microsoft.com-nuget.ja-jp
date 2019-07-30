---
title: dotnet CLI を使用して NuGet パッケージを作成する
description: NuGet パッケージを設計し、作成する過程を詳しく説明します。ファイルやバージョン管理など、重要な決定ポイントが含まれます。
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: da5dbc8b1659cef66e8439b9a3c3bb2c9205cbe6
ms.sourcegitcommit: f291ff91561a6b58c2aec41c624d798e00ce41fa
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68462464"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="53fbb-103">dotnet CLI を使用して NuGet パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="53fbb-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="53fbb-104">パッケージの動作やそれに含まれているコードに関係なく、CLI ツールのいずれか (`nuget.exe` または `dotnet.exe`) を使用して、他の開発者が何人でも共有して使用できるコンポーネントにその機能をパッケージ化できます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="53fbb-105">この記事では、dotnet CLI を使用してパッケージを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="53fbb-106">`dotnet` CLI をインストールするには、「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="53fbb-107">Visual Studio 2017 以降では、dotnet CLI は .NET Core ワークロードに含まれています。</span><span class="sxs-lookup"><span data-stu-id="53fbb-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="53fbb-108">[SDK スタイルの形式](../resources/check-project-format.md)を使用する .NET Core および .NET Standard プロジェクト、またその他の SDK スタイルのあらゆるプロジェクトに対して、NuGet ではプロジェクト ファイルにある情報を直接使ってパッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="53fbb-109">ステップバイステップのチュートリアルについては、[dotnet CLI を使用した .NET Standard パッケージの作成](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)に関するページ、[Visual Studio を使用した .NET Standard パッケージの作成](../quickstart/create-and-publish-a-package-using-visual-studio.md)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md), [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="53fbb-110">`msbuild -t:pack` は、`dotnet pack` と同等の機能です。</span><span class="sxs-lookup"><span data-stu-id="53fbb-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="53fbb-111">MSBuild を使用してビルドする場合、その概念はこの記事の説明と同じですが、コマンド ラインのコマンドが少し異なります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-111">To build with MSBuild, the concepts are the same as described in this article, but the command line commands are slightly different.</span></span> <span data-ttu-id="53fbb-112">同様に、非 SDK スタイルのプロジェクトおよび `<PackageReference>` では、`msbuild /t:pack` を使用できます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-112">Similarly, with a non-SDK-style project and `<PackageReference>`, you can use `msbuild /t:pack`.</span></span> <span data-ttu-id="53fbb-113">これらのシナリオでは、依存関係に NuGet.Build.Tasks.Pack パッケージを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-113">In these scenarios, you need to add the NuGet.Build.Tasks.Pack package to their dependencies.</span></span> <span data-ttu-id="53fbb-114">「[MSBuild ターゲットとしての NuGet の pack と restore](../reference/msbuild-targets.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-114">See [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53fbb-115">このトピックは、[SDK スタイル](../resources/check-project-format.md)のプロジェクト (通常は .NET Core および .NET Standard プロジェクト) に適用されます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-115">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="53fbb-116">プロパティの設定</span><span class="sxs-lookup"><span data-stu-id="53fbb-116">Set properties</span></span>

<span data-ttu-id="53fbb-117">次のプロパティは、パッケージを作成するために必要です。</span><span class="sxs-lookup"><span data-stu-id="53fbb-117">The following properties are required to create a package.</span></span>

- <span data-ttu-id="53fbb-118">`PackageId`、パッケージの識別子。パッケージをホストするギャラリー全体で一意にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-118">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="53fbb-119">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-119">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="53fbb-120">`Version`、*Major.Minor.Patch[-Suffix]* という形式の特別なバージョン番号。 *-Suffix* によって[プレリリース版](prerelease-packages.md)を識別します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-120">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="53fbb-121">指定しない場合は、既定値は 1.0.0 です。</span><span class="sxs-lookup"><span data-stu-id="53fbb-121">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="53fbb-122">ホスト (nuget.org など) に表示されるパッケージ タイトル。</span><span class="sxs-lookup"><span data-stu-id="53fbb-122">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="53fbb-123">`Authors`、作成者と所有者の情報。</span><span class="sxs-lookup"><span data-stu-id="53fbb-123">`Authors`, author and owner information.</span></span> <span data-ttu-id="53fbb-124">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-124">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="53fbb-125">`Company`、会社名。</span><span class="sxs-lookup"><span data-stu-id="53fbb-125">`Company`, your company name.</span></span> <span data-ttu-id="53fbb-126">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-126">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="53fbb-127">Visual Studio では、プロジェクトのプロパティにこれらの値を設定できます (ソリューション エクスプローラー内でプロジェクトを右クリックし、 **[プロパティ]** を選択して、 **[パッケージ]** タブを選択します)。</span><span class="sxs-lookup"><span data-stu-id="53fbb-127">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="53fbb-128">プロジェクト ファイル (`.csproj`) 内でこれらのプロパティを直接設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-128">You can also set these properties directly in the project files (`.csproj`).</span></span>

    ```xml
    <PropertyGroup>
      ...
      <PackageId>AppLogger</PackageId>
      <Version>1.0.0</Version>
      <Authors>your_name</Authors>
      <Company>your_company</Company>
    </PropertyGroup>
    ```

> [!Important]
> <span data-ttu-id="53fbb-129">パッケージには、nuget.org または使用しているパッケージ ソース全体で一意になる識別子を付けてください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-129">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="53fbb-130">また、[MSBuild pack ターゲット](../reference/msbuild-targets.md#pack-target)に関するセクション、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」、「[NuGet メタデータ プロパティ](/dotnet/core/tools/csproj#nuget-metadata-properties)」に説明されているように、`Title`、`PackageDescription`、`PackageTags` などのオプションのプロパティを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="53fbb-131">公開用にビルドされたパッケージの場合は、**PackageTags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="53fbb-132">依存関係の宣言とバージョン番号の指定については、「[パッケージのバージョン管理](../reference/package-versioning.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-132">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="53fbb-133">`<IncludeAssets>` および `<ExcludeAssets>` 属性を使用して、パッケージ内で直接、依存関係からアセットを表面化させることもできます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="53fbb-134">詳しくは、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="53fbb-135">一意のパッケージ識別子を選択してバージョン番号を設定する</span><span class="sxs-lookup"><span data-stu-id="53fbb-135">Choose a unique package identifier and set the version number</span></span>

<span data-ttu-id="53fbb-136">パッケージ識別子とバージョン番号は、パッケージに含まれる正確なコードを一意に識別するため、プロジェクトの中で最も重要な 2 つの値です。</span><span class="sxs-lookup"><span data-stu-id="53fbb-136">The package identifier and the version number are the two most important values in the project because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="53fbb-137">**パッケージ識別子のベスト プラクティス:**</span><span class="sxs-lookup"><span data-stu-id="53fbb-137">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="53fbb-138">**一意性**:この識別子は、nuget.org 全体で、あるいはパッケージをホストするギャラリー全体で一意になる必要があります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-138">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="53fbb-139">識別子を決める前に、該当するギャラリーを検索し、その名前が既に使用されていないか確認してください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-139">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="53fbb-140">競合を避けるために、`Contoso.` のように、識別子の最初の部分に会社の名前を使用することが適しているパターンです。</span><span class="sxs-lookup"><span data-stu-id="53fbb-140">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="53fbb-141">**名前空間のような名前**:.NET の名前空間に似たパターンに従います。ハイフンの代わりにドット表記を使います。</span><span class="sxs-lookup"><span data-stu-id="53fbb-141">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="53fbb-142">たとえば、`Contoso-Utility-UsefulStuff` や `Contoso_Utility_UsefulStuff` ではなく `Contoso.Utility.UsefulStuff` を使用します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-142">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="53fbb-143">パッケージ識別子がコードで使用される名前空間と一致すれば、利用者にとっても便利です。</span><span class="sxs-lookup"><span data-stu-id="53fbb-143">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="53fbb-144">**サンプル パッケージ**:別のパッケージの使用方法を示すサンプル コードのパッケージを生成する場合、`Contoso.Utility.UsefulStuff.Sample` のように、識別子にサフィックスとして `.Sample` を付けます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-144">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="53fbb-145">(サンプル パッケージは、もちろん、他のパッケージに依存します。)サンプル パッケージを作成する場合は、`<IncludeAssets>` 内で `contentFiles` 値を使用します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-145">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the `contentFiles` value in `<IncludeAssets>`.</span></span> <span data-ttu-id="53fbb-146">`content` フォルダーで、`\Samples\Contoso.Utility.UsefulStuff.Sample` のように、`\Samples\<identifier>` という名前のフォルダーにサンプル コードを配置します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-146">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="53fbb-147">**パッケージ バージョンのベスト プラクティス:**</span><span class="sxs-lookup"><span data-stu-id="53fbb-147">**Best practices for the package version:**</span></span>

- <span data-ttu-id="53fbb-148">これは厳密には必須ではありませんが、一般的にはプロジェクト (またはアセンブリ) と一致するようにパッケージのバージョンを設定します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-148">In general, set the version of the package to match the project (or assembly), though this is not strictly required.</span></span> <span data-ttu-id="53fbb-149">パッケージを単一のアセンブリに限定する場合に、これはシンプルな方法です。</span><span class="sxs-lookup"><span data-stu-id="53fbb-149">This is a simple matter when you limit a package to a single assembly.</span></span> <span data-ttu-id="53fbb-150">概して、NuGet 自体は依存関係の解決時、パッケージ バージョンを使います。アセンブリ バージョンではありません。</span><span class="sxs-lookup"><span data-stu-id="53fbb-150">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="53fbb-151">非標準のバージョン スキーマを使用するとき、「[パッケージのバージョン管理](../reference/package-versioning.md)」で説明するように、NuGet バージョン管理ルールを検討してください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-151">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="53fbb-152">NuGet は、ほぼ [semver 2 に準拠](../reference/package-versioning.md#semantic-versioning-200)しています。</span><span class="sxs-lookup"><span data-stu-id="53fbb-152">NuGet is mostly [semver 2 compliant](../reference/package-versioning.md#semantic-versioning-200).</span></span>

> <span data-ttu-id="53fbb-153">依存関係の解決については、「[PackageReference による依存関係の解決](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-153">For information on dependency resolution, see [Dependency resolution with PackageReference](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference).</span></span> <span data-ttu-id="53fbb-154">バージョン管理の理解を深めるためにも役立つ可能性がある旧情報については、こちらの一連のブログ投稿を確認してください。</span><span class="sxs-lookup"><span data-stu-id="53fbb-154">For older information that may also be helpful to better understand versioning, see this series of blog posts.</span></span>
>
> - [<span data-ttu-id="53fbb-155">第 1 部: DLL 地獄</span><span class="sxs-lookup"><span data-stu-id="53fbb-155">Part 1: Taking on DLL Hell</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [<span data-ttu-id="53fbb-156">第 2 部: コア アルゴリズム</span><span class="sxs-lookup"><span data-stu-id="53fbb-156">Part 2: The core algorithm</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [<span data-ttu-id="53fbb-157">第 3 部:バインド リダイレクトによる統合</span><span class="sxs-lookup"><span data-stu-id="53fbb-157">Part 3: Unification via Binding Redirects</span></span>](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="run-the-pack-command"></a><span data-ttu-id="53fbb-158">pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="53fbb-158">Run the pack command</span></span>

<span data-ttu-id="53fbb-159">プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`dotnet pack` コマンドを実行します。このコマンドではプロジェクトのビルドも自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-159">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="53fbb-160">出力に、`.nupkg` ファイルへのパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-160">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="53fbb-161">ビルド時に自動的にパッケージを生成する</span><span class="sxs-lookup"><span data-stu-id="53fbb-161">Automatically generate package on build</span></span>

<span data-ttu-id="53fbb-162">`dotnet build` の実行時に自動的に `dotnet pack` を実行させるには、プロジェクト ファイルの `<PropertyGroup>` 内に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-162">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="53fbb-163">ソリューション上で `dotnet pack` を実行した場合、これにより、パック化可能なソリューション内のすべてのプロジェクトがパックされます ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) プロパティは `true` に設定されます)。</span><span class="sxs-lookup"><span data-stu-id="53fbb-163">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`.</span></span>

> [!NOTE]
> <span data-ttu-id="53fbb-164">パッケージを自動的に生成する場合、パックする時間によってプロジェクトのビルド時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-164">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="53fbb-165">パッケージ インストールのテスト</span><span class="sxs-lookup"><span data-stu-id="53fbb-165">Test package installation</span></span>

<span data-ttu-id="53fbb-166">パッケージを公開する前に、通常、パッケージをプロジェクトにインストールするプロセスをテストします。</span><span class="sxs-lookup"><span data-stu-id="53fbb-166">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="53fbb-167">このテストにより、必要なファイルがすべて、プロジェクト内の適切な場所に入ります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-167">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="53fbb-168">インストールは Visual Studio またはコマンド ラインで手動テストできます。通常の[パッケージ インストール手順](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)を利用します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-168">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="53fbb-169">パッケージは不変です。</span><span class="sxs-lookup"><span data-stu-id="53fbb-169">Packages are immutable.</span></span> <span data-ttu-id="53fbb-170">問題を修正する場合は、パッケージ内容を変更して、もう一度パックしてください。再テスト時に、[グローバル パッケージのフォルダーをクリアする](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)までは、古いバージョンのパッケージを引き続き使用することになります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-170">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="53fbb-171">どのビルド時でも、一意のプレリリース ラベルを使用しないパッケージをテストする場合に、これは特に該当します。</span><span class="sxs-lookup"><span data-stu-id="53fbb-171">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="53fbb-172">次の手順</span><span class="sxs-lookup"><span data-stu-id="53fbb-172">Next Steps</span></span>

<span data-ttu-id="53fbb-173">`.nupkg` ファイルとなるパッケージを作成したら、「[パッケージの公開](../nuget-org/publish-a-package.md)」の説明にあるように、選択したギャラリーにパッケージを公開できます。</span><span class="sxs-lookup"><span data-stu-id="53fbb-173">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="53fbb-174">パッケージの機能を拡張したり、次のトピックで説明するように、その他の方法で他のシナリオをサポートしたりすると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-174">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="53fbb-175">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="53fbb-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="53fbb-176">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="53fbb-176">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="53fbb-177">ソース ファイルと構成ファイルの変換</span><span class="sxs-lookup"><span data-stu-id="53fbb-177">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="53fbb-178">ローカリゼーション</span><span class="sxs-lookup"><span data-stu-id="53fbb-178">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="53fbb-179">プレリリース バージョン</span><span class="sxs-lookup"><span data-stu-id="53fbb-179">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="53fbb-180">パッケージの種類の設定</span><span class="sxs-lookup"><span data-stu-id="53fbb-180">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="53fbb-181">COM 相互運用アセンブリを含むパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="53fbb-181">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="53fbb-182">最後になりますが、次のような種類のパッケージもあります。</span><span class="sxs-lookup"><span data-stu-id="53fbb-182">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="53fbb-183">ネイティブ パッケージ</span><span class="sxs-lookup"><span data-stu-id="53fbb-183">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="53fbb-184">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="53fbb-184">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
