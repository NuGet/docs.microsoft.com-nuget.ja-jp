---
title: dotnet CLI を使用して NuGet パッケージを作成する
description: NuGet パッケージを設計し、作成する過程を詳しく説明します。ファイルやバージョン管理など、重要な決定ポイントが含まれます。
author: karann-msft
ms.author: karann
ms.date: 02/20/2020
ms.topic: conceptual
ms.openlocfilehash: 712e4c7159aa9719052330d8e45f63e18e390325
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230585"
---
# <a name="create-a-nuget-package-using-the-dotnet-cli"></a><span data-ttu-id="891cf-103">dotnet CLI を使用して NuGet パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="891cf-103">Create a NuGet package using the dotnet CLI</span></span>

<span data-ttu-id="891cf-104">パッケージの動作やそれに含まれているコードに関係なく、CLI ツールのいずれか (`nuget.exe` または `dotnet.exe`) を使用して、他の開発者が何人でも共有して使用できるコンポーネントにその機能をパッケージ化できます。</span><span class="sxs-lookup"><span data-stu-id="891cf-104">No matter what your package does or what code it contains, you use one of the CLI tools, either `nuget.exe` or `dotnet.exe`, to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="891cf-105">この記事では、dotnet CLI を使用してパッケージを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="891cf-105">This article describes how to create a package using the dotnet CLI.</span></span> <span data-ttu-id="891cf-106">`dotnet` CLI をインストールするには、「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="891cf-106">To install the `dotnet` CLI, see [Install NuGet client tools](../install-nuget-client-tools.md).</span></span> <span data-ttu-id="891cf-107">Visual Studio 2017 以降では、dotnet CLI は .NET Core ワークロードに含まれています。</span><span class="sxs-lookup"><span data-stu-id="891cf-107">Starting in Visual Studio 2017, the dotnet CLI is included with .NET Core workloads.</span></span>

<span data-ttu-id="891cf-108">[SDK スタイルの形式](../resources/check-project-format.md)を使用する .NET Core および .NET Standard プロジェクト、またその他の SDK スタイルのあらゆるプロジェクトに対して、NuGet ではプロジェクト ファイルにある情報を直接使ってパッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="891cf-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span> <span data-ttu-id="891cf-109">ステップ バイ ステップのチュートリアルについては、「[.NET Standard パッケージの作成 (dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)」または「[.NET Standard パッケージの作成 (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="891cf-109">For step-by-step tutorials, see [Create .NET Standard Packages with dotnet CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) or [Create .NET Standard Packages with Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md).</span></span>

<span data-ttu-id="891cf-110">`msbuild -t:pack` は、`dotnet pack` と同等の機能です。</span><span class="sxs-lookup"><span data-stu-id="891cf-110">`msbuild -t:pack` is functionality equivalent to `dotnet pack`.</span></span> <span data-ttu-id="891cf-111">MSBuild を使用してビルドするには、「[NuGet パッケージの作成 (MSBuild)](creating-a-package-msbuild.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="891cf-111">To build with MSBuild, see [Create a NuGet package using MSBuild](creating-a-package-msbuild.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="891cf-112">このトピックは、[SDK スタイル](../resources/check-project-format.md)のプロジェクト (通常は .NET Core および .NET Standard プロジェクト) に適用されます。</span><span class="sxs-lookup"><span data-stu-id="891cf-112">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects.</span></span>

## <a name="set-properties"></a><span data-ttu-id="891cf-113">プロパティの設定</span><span class="sxs-lookup"><span data-stu-id="891cf-113">Set properties</span></span>

<span data-ttu-id="891cf-114">次のプロパティは、パッケージを作成するために必要です。</span><span class="sxs-lookup"><span data-stu-id="891cf-114">The following properties are required to create a package.</span></span>

- <span data-ttu-id="891cf-115">`PackageId`、パッケージの識別子。パッケージをホストするギャラリー全体で一意にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="891cf-115">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="891cf-116">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="891cf-116">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="891cf-117">`Version`、*Major.Minor.Patch[-Suffix]* という形式の特別なバージョン番号。 *-Suffix* によって[プレリリース版](prerelease-packages.md)を識別します。</span><span class="sxs-lookup"><span data-stu-id="891cf-117">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="891cf-118">指定しない場合は、既定値は 1.0.0 です。</span><span class="sxs-lookup"><span data-stu-id="891cf-118">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="891cf-119">ホスト (nuget.org など) に表示されるパッケージ タイトル。</span><span class="sxs-lookup"><span data-stu-id="891cf-119">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="891cf-120">`Authors`、作成者と所有者の情報。</span><span class="sxs-lookup"><span data-stu-id="891cf-120">`Authors`, author and owner information.</span></span> <span data-ttu-id="891cf-121">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="891cf-121">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="891cf-122">`Company`、会社名。</span><span class="sxs-lookup"><span data-stu-id="891cf-122">`Company`, your company name.</span></span> <span data-ttu-id="891cf-123">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="891cf-123">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="891cf-124">Visual Studio では、プロジェクトのプロパティにこれらの値を設定できます (ソリューション エクスプローラー内でプロジェクトを右クリックし、 **[プロパティ]** を選択して、 **[パッケージ]** タブを選択します)。</span><span class="sxs-lookup"><span data-stu-id="891cf-124">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="891cf-125">プロジェクト ファイル (`.csproj`) 内でこれらのプロパティを直接設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="891cf-125">You can also set these properties directly in the project files (`.csproj`).</span></span>

```xml
<PropertyGroup>
  <PackageId>AppLogger</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="891cf-126">パッケージには、nuget.org または使用しているパッケージ ソース全体で一意になる識別子を付けてください。</span><span class="sxs-lookup"><span data-stu-id="891cf-126">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="891cf-127">次の例は、これらのプロパティを含む、シンプルかつ完全なプロジェクト ファイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="891cf-127">The following example shows a simple, complete project file with these properties included.</span></span> <span data-ttu-id="891cf-128">(`dotnet new classlib` コマンドを使用して、新しい既定のプロジェクトを作成できます)。</span><span class="sxs-lookup"><span data-stu-id="891cf-128">(You can create a new default project using the `dotnet new classlib` command.)</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="891cf-129">また、[MSBuild pack ターゲット](../reference/msbuild-targets.md#pack-target)に関するセクション、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」、「[NuGet メタデータ プロパティ](/dotnet/core/tools/csproj#nuget-metadata-properties)」に説明されているように、`Title`、`PackageDescription`、`PackageTags` などのオプションのプロパティを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="891cf-129">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="891cf-130">公開用にビルドされたパッケージの場合は、**PackageTags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="891cf-130">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="891cf-131">依存関係の宣言とバージョン番号の指定の詳細については、「[プロジェクト ファイルのパッケージ参照 (PackageReference)](../consume-packages/package-references-in-project-files.md)」と「[パッケージのバージョン管理](../concepts/package-versioning.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="891cf-131">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="891cf-132">`<IncludeAssets>` および `<ExcludeAssets>` 属性を使用して、パッケージ内で直接、依存関係からアセットを表面化させることもできます。</span><span class="sxs-lookup"><span data-stu-id="891cf-132">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="891cf-133">詳しくは、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="891cf-133">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="add-an-optional-description-field"></a><span data-ttu-id="891cf-134">省略可能な説明フィールドを追加する</span><span class="sxs-lookup"><span data-stu-id="891cf-134">Add an optional description field</span></span>

[!INCLUDE [add description to package](includes/add-description.md)]

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="891cf-135">一意のパッケージ識別子を選択してバージョン番号を設定する</span><span class="sxs-lookup"><span data-stu-id="891cf-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="run-the-pack-command"></a><span data-ttu-id="891cf-136">pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="891cf-136">Run the pack command</span></span>

<span data-ttu-id="891cf-137">プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`dotnet pack` コマンドを実行します。このコマンドではプロジェクトのビルドも自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="891cf-137">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="891cf-138">出力に、`.nupkg` ファイルへのパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="891cf-138">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="891cf-139">ビルド時に自動的にパッケージを生成する</span><span class="sxs-lookup"><span data-stu-id="891cf-139">Automatically generate package on build</span></span>

<span data-ttu-id="891cf-140">`dotnet build` の実行時に自動的に `dotnet pack` を実行させるには、プロジェクト ファイルの `<PropertyGroup>` 内に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="891cf-140">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="891cf-141">ソリューション上で `dotnet pack` を実行した場合、これにより、パック化可能なソリューション内のすべてのプロジェクトがパックされます ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) プロパティは `true` に設定されます)。</span><span class="sxs-lookup"><span data-stu-id="891cf-141">When you run `dotnet pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="891cf-142">パッケージを自動的に生成する場合、パックする時間によってプロジェクトのビルド時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="891cf-142">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="891cf-143">パッケージ インストールのテスト</span><span class="sxs-lookup"><span data-stu-id="891cf-143">Test package installation</span></span>

<span data-ttu-id="891cf-144">パッケージを公開する前に、通常、パッケージをプロジェクトにインストールするプロセスをテストします。</span><span class="sxs-lookup"><span data-stu-id="891cf-144">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="891cf-145">このテストにより、必要なファイルがすべて、プロジェクト内の適切な場所に入ります。</span><span class="sxs-lookup"><span data-stu-id="891cf-145">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="891cf-146">インストールは Visual Studio またはコマンド ラインで手動テストできます。通常の[パッケージ インストール手順](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)を利用します。</span><span class="sxs-lookup"><span data-stu-id="891cf-146">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="891cf-147">パッケージは不変です。</span><span class="sxs-lookup"><span data-stu-id="891cf-147">Packages are immutable.</span></span> <span data-ttu-id="891cf-148">問題を修正する場合は、パッケージ内容を変更して、もう一度パックしてください。再テスト時に、[グローバル パッケージのフォルダーをクリアする](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)までは、古いバージョンのパッケージを引き続き使用することになります。</span><span class="sxs-lookup"><span data-stu-id="891cf-148">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="891cf-149">どのビルド時でも、一意のプレリリース ラベルを使用しないパッケージをテストする場合に、これは特に該当します。</span><span class="sxs-lookup"><span data-stu-id="891cf-149">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="891cf-150">次の手順</span><span class="sxs-lookup"><span data-stu-id="891cf-150">Next Steps</span></span>

<span data-ttu-id="891cf-151">`.nupkg` ファイルとなるパッケージを作成したら、「[パッケージの公開](../nuget-org/publish-a-package.md)」の説明にあるように、選択したギャラリーにパッケージを公開できます。</span><span class="sxs-lookup"><span data-stu-id="891cf-151">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="891cf-152">パッケージの機能を拡張したり、次のトピックで説明するように、その他の方法で他のシナリオをサポートしたりすると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="891cf-152">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="891cf-153">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="891cf-153">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="891cf-154">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="891cf-154">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="891cf-155">パッケージ アイコンの追加</span><span class="sxs-lookup"><span data-stu-id="891cf-155">Add a package icon</span></span>](../reference/nuspec.md#icon)
- [<span data-ttu-id="891cf-156">ソース ファイルと構成ファイルの変換</span><span class="sxs-lookup"><span data-stu-id="891cf-156">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="891cf-157">ローカリゼーション</span><span class="sxs-lookup"><span data-stu-id="891cf-157">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="891cf-158">プレリリース バージョン</span><span class="sxs-lookup"><span data-stu-id="891cf-158">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="891cf-159">パッケージの種類の設定</span><span class="sxs-lookup"><span data-stu-id="891cf-159">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="891cf-160">COM 相互運用アセンブリを含むパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="891cf-160">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="891cf-161">最後になりますが、次のような種類のパッケージもあります。</span><span class="sxs-lookup"><span data-stu-id="891cf-161">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="891cf-162">ネイティブ パッケージ</span><span class="sxs-lookup"><span data-stu-id="891cf-162">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="891cf-163">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="891cf-163">Symbol Packages</span></span>](../create-packages/symbol-packages-snupkg.md)
