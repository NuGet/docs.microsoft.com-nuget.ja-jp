---
title: MSBuild を使用して NuGet パッケージを作成する
description: NuGet パッケージを設計し、作成する過程を詳しく説明します。ファイルやバージョン管理など、重要な決定ポイントが含まれます。
author: karann-msft
ms.author: karann
ms.date: 08/05/2019
ms.topic: conceptual
ms.openlocfilehash: a965a3049f46af59efcfad2ecf19e0923fda413b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488946"
---
# <a name="create-a-nuget-package-using-msbuild"></a><span data-ttu-id="4e841-103">MSBuild を使用して NuGet パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="4e841-103">Create a NuGet package using MSBuild</span></span>

<span data-ttu-id="4e841-104">自分のコードで NuGet パッケージを作成する場合、その機能をコンポーネントにパッケージ化し、数を問わず他の開発者と共有し、使用することができます。</span><span class="sxs-lookup"><span data-stu-id="4e841-104">When you create a NuGet package from your code, you package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="4e841-105">この記事では、MSBuild を使用してパッケージを作成する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="4e841-105">This article describes how to create a package using MSBuild.</span></span> <span data-ttu-id="4e841-106">MSBuild は、NuGet を含むすべての Visual Studio ワークロードにプレインストールされています。</span><span class="sxs-lookup"><span data-stu-id="4e841-106">MSBuild comes preinstalled with every Visual Studio workload that contains NuGet.</span></span> <span data-ttu-id="4e841-107">また、dotnet CLI と [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild) を使用して MSBuild を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="4e841-107">Additionally you can also use MSBuild through the dotnet CLI with [dotnet msbuild](https://docs.microsoft.com/en-us/dotnet/core/tools/dotnet-msbuild)</span></span>

<span data-ttu-id="4e841-108">[SDK スタイルの形式](../resources/check-project-format.md)を使用する .NET Core および .NET Standard プロジェクト、またその他の SDK スタイルのあらゆるプロジェクトに対して、NuGet ではプロジェクト ファイルにある情報を直接使ってパッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="4e841-108">For .NET Core and .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md), and any other SDK-style projects, NuGet uses information in the project file directly to create a package.</span></span>  <span data-ttu-id="4e841-109">`<PackageReference>` を使用する SDK スタイル以外のプロジェクトの場合、NuGet ではプロジェクト ファイルを使用してパッケージを作成することもできます。</span><span class="sxs-lookup"><span data-stu-id="4e841-109">For a non-SDK-style project that uses `<PackageReference>`, NuGet also uses the project file to create a package.</span></span>

<span data-ttu-id="4e841-110">SDK スタイルのプロジェクトには、既定でパック機能を利用できます。</span><span class="sxs-lookup"><span data-stu-id="4e841-110">SDK-style projects have the pack functionality available by default.</span></span> <span data-ttu-id="4e841-111">SDK スタイル以外の PackageReference プロジェクトでは、プロジェクトの依存関係に NuGet.Build.Tasks.Pack パッケージを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e841-111">For non SDK-style PackageReference projects, you need to add the NuGet.Build.Tasks.Pack package to the project dependencies.</span></span> <span data-ttu-id="4e841-112">MSBuild パック ターゲットの詳細については、「[MSBuild ターゲットとしての NuGet の pack と restore](../reference/msbuild-targets.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4e841-112">For detailed information about MSBuild pack targets, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

<span data-ttu-id="4e841-113">パッケージ (`msbuild -t:pack`) を作成するコマンドは、`dotnet pack` と同等の機能です。</span><span class="sxs-lookup"><span data-stu-id="4e841-113">The command that creates a package, `msbuild -t:pack`, is functionality equivalent to `dotnet pack`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e841-114">このトピックは、[SDK スタイル](../resources/check-project-format.md)のプロジェクト (通常は、.NET Core プロジェクトと .NET Standard プロジェクト)、および PackageReference を使った SDK スタイル以外のプロジェクトを対象としています。</span><span class="sxs-lookup"><span data-stu-id="4e841-114">This topic applies to [SDK-style](../resources/check-project-format.md) projects, typically .NET Core and .NET Standard projects, and to non-SDK-style projects that use PackageReference.</span></span>

## <a name="set-properties"></a><span data-ttu-id="4e841-115">プロパティの設定</span><span class="sxs-lookup"><span data-stu-id="4e841-115">Set properties</span></span>

<span data-ttu-id="4e841-116">次のプロパティは、パッケージを作成するために必要です。</span><span class="sxs-lookup"><span data-stu-id="4e841-116">The following properties are required to create a package.</span></span>

- <span data-ttu-id="4e841-117">`PackageId`、パッケージの識別子。パッケージをホストするギャラリー全体で一意にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4e841-117">`PackageId`, the package identifier, which must be unique across the gallery that hosts the package.</span></span> <span data-ttu-id="4e841-118">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="4e841-118">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="4e841-119">`Version`、*Major.Minor.Patch[-Suffix]* という形式の特別なバージョン番号。 *-Suffix* によって[プレリリース版](prerelease-packages.md)を識別します。</span><span class="sxs-lookup"><span data-stu-id="4e841-119">`Version`, a specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md).</span></span> <span data-ttu-id="4e841-120">指定しない場合は、既定値は 1.0.0 です。</span><span class="sxs-lookup"><span data-stu-id="4e841-120">If not specified, the default value is 1.0.0.</span></span>
- <span data-ttu-id="4e841-121">ホスト (nuget.org など) に表示されるパッケージ タイトル。</span><span class="sxs-lookup"><span data-stu-id="4e841-121">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="4e841-122">`Authors`、作成者と所有者の情報。</span><span class="sxs-lookup"><span data-stu-id="4e841-122">`Authors`, author and owner information.</span></span> <span data-ttu-id="4e841-123">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="4e841-123">If not specified, the default value is `AssemblyName`.</span></span>
- <span data-ttu-id="4e841-124">`Company`、会社名。</span><span class="sxs-lookup"><span data-stu-id="4e841-124">`Company`, your company name.</span></span> <span data-ttu-id="4e841-125">指定しない場合は、既定値の `AssemblyName` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="4e841-125">If not specified, the default value is `AssemblyName`.</span></span>

<span data-ttu-id="4e841-126">Visual Studio では、プロジェクトのプロパティにこれらの値を設定できます (ソリューション エクスプローラー内でプロジェクトを右クリックし、 **[プロパティ]** を選択して、 **[パッケージ]** タブを選択します)。</span><span class="sxs-lookup"><span data-stu-id="4e841-126">In Visual Studio, you can set these values in the project properties (right-click the project in Solution Explorer, choose **Properties**, and select the **Package** tab).</span></span> <span data-ttu-id="4e841-127">プロジェクト ファイル ( *.csproj*) 内でこれらのプロパティを直接設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="4e841-127">You can also set these properties directly in the project files (*.csproj*).</span></span>

```xml
<PropertyGroup>
  <PackageId>ClassLibDotNetStandard</PackageId>
  <Version>1.0.0</Version>
  <Authors>your_name</Authors>
  <Company>your_company</Company>
</PropertyGroup>
```

> [!Important]
> <span data-ttu-id="4e841-128">パッケージには、nuget.org または使用しているパッケージ ソース全体で一意になる識別子を付けてください。</span><span class="sxs-lookup"><span data-stu-id="4e841-128">Give the package an identifier that's unique across nuget.org or whatever package source you're using.</span></span>

<span data-ttu-id="4e841-129">次の例は、これらのプロパティを含む、シンプルかつ完全なプロジェクト ファイルを示しています。</span><span class="sxs-lookup"><span data-stu-id="4e841-129">The following example shows a simple, complete project file with these properties included.</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <PackageId>ClassLibDotNetStandard</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
  </PropertyGroup>
</Project>
```

<span data-ttu-id="4e841-130">また、[MSBuild pack ターゲット](../reference/msbuild-targets.md#pack-target)に関するセクション、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」、「[NuGet メタデータ プロパティ](/dotnet/core/tools/csproj#nuget-metadata-properties)」に説明されているように、`Title`、`PackageDescription`、`PackageTags` などのオプションのプロパティを設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="4e841-130">You can also set the optional properties, such as `Title`, `PackageDescription`, and `PackageTags`, as described in [MSBuild pack targets](../reference/msbuild-targets.md#pack-target), [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets), and [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

> [!NOTE]
> <span data-ttu-id="4e841-131">公開用にビルドされたパッケージの場合は、**PackageTags**プロパティに特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="4e841-131">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

<span data-ttu-id="4e841-132">依存関係の宣言とバージョン番号の指定の詳細については、「[プロジェクト ファイルのパッケージ参照 (PackageReference)](../consume-packages/package-references-in-project-files.md)」と「[パッケージのバージョン管理](../concepts/package-versioning.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4e841-132">For details on declaring dependencies and specifying version numbers, see [Package references in project files](../consume-packages/package-references-in-project-files.md) and [Package versioning](../concepts/package-versioning.md).</span></span> <span data-ttu-id="4e841-133">`<IncludeAssets>` および `<ExcludeAssets>` 属性を使用して、パッケージ内で直接、依存関係からアセットを表面化させることもできます。</span><span class="sxs-lookup"><span data-stu-id="4e841-133">It is also possible to surface assets from dependencies directly in the package by using the `<IncludeAssets>` and `<ExcludeAssets>` attributes.</span></span> <span data-ttu-id="4e841-134">詳しくは、「[依存関係アセットを制御する](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="4e841-134">For more information, seee [Controlling dependency assets](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span>

## <a name="choose-a-unique-package-identifier-and-set-the-version-number"></a><span data-ttu-id="4e841-135">一意のパッケージ識別子を選択してバージョン番号を設定する</span><span class="sxs-lookup"><span data-stu-id="4e841-135">Choose a unique package identifier and set the version number</span></span>

[!INCLUDE [choose-package-id](includes/choose-package-id.md)]

## <a name="add-the-nugetbuildtaskspack-package"></a><span data-ttu-id="4e841-136">NuGet.Build.Tasks.Pack パッケージを追加する</span><span class="sxs-lookup"><span data-stu-id="4e841-136">Add the NuGet.Build.Tasks.Pack package</span></span>

<span data-ttu-id="4e841-137">SDK スタイル以外のプロジェクトと PackageReference で MSBuild を使用している場合は、プロジェクトに NuGet.Build.Tasks.Pack パッケージを追加します。</span><span class="sxs-lookup"><span data-stu-id="4e841-137">If you are using MSBuild with a non-SDK-style project and PackageReference, add the NuGet.Build.Tasks.Pack package to your project.</span></span>

1. <span data-ttu-id="4e841-138">プロジェクト ファイルを開き、以下を `<PropertyGroup>` 要素の後に追加します。</span><span class="sxs-lookup"><span data-stu-id="4e841-138">Open the project file and add the following after the `<PropertyGroup>` element:</span></span>

   ```xml
   <ItemGroup>
     <!-- ... -->
     <PackageReference Include="NuGet.Build.Tasks.Pack" Version="5.2.0"/>
     <!-- ... -->
   </ItemGroup>
   ```

2. <span data-ttu-id="4e841-139">開発者コマンド プロンプトを開きます (**検索**ボックスに「**開発者コマンド プロンプト**」と入力します)。</span><span class="sxs-lookup"><span data-stu-id="4e841-139">Open a Developer command prompt (In the **Search** box, type **Developer command prompt**).</span></span>

   <span data-ttu-id="4e841-140">MSBuild に必要なすべてのパスが構成されるため、通常は **[スタート]** メニューから Visual Studio 用開発者コマンド プロンプトを使用します。</span><span class="sxs-lookup"><span data-stu-id="4e841-140">You typically want to start the Developer Command Prompt for Visual Studio from the **Start** menu, as it will be configured with all the necessary paths for MSBuild.</span></span>

3. <span data-ttu-id="4e841-141">プロジェクト ファイルが含まれているフォルダーに切り替え、次のコマンドを入力して、NuGet.Build.Tasks.Pack パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="4e841-141">Switch to the folder containing the project file and type the following command to install the NuGet.Build.Tasks.Pack package.</span></span>

   ```cmd
   # Uses the project file in the current folder by default
   msbuild -t:restore
   ```

   <span data-ttu-id="4e841-142">MSBuild の出力にビルドが正常に完了したことが示されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="4e841-142">Make sure that the MSBuild output indicates that the build completed successfully.</span></span>

## <a name="run-the-msbuild--tpack-command"></a><span data-ttu-id="4e841-143">msbuild -t:pack コマンドを実行する</span><span class="sxs-lookup"><span data-stu-id="4e841-143">Run the msbuild -t:pack command</span></span>

<span data-ttu-id="4e841-144">プロジェクトから NuGet パッケージ (`.nupkg` ファイル) を作成するには、`msbuild -t:pack` コマンドを実行します。このコマンドではプロジェクトのビルドも自動的に行われます。</span><span class="sxs-lookup"><span data-stu-id="4e841-144">To build a NuGet package (a `.nupkg` file) from the project, run the `msbuild -t:pack` command, which also builds the project automatically:</span></span>

<span data-ttu-id="4e841-145">Visual Studio 用開発者コマンド プロンプトで次のコマンドを入力します。</span><span class="sxs-lookup"><span data-stu-id="4e841-145">In the Developer command prompt for Visual Studio, type the following command:</span></span>

```cmd
# Uses the project file in the current folder by default
msbuild -t:pack
```

<span data-ttu-id="4e841-146">出力に、`.nupkg` ファイルへのパスが表示されます。</span><span class="sxs-lookup"><span data-stu-id="4e841-146">The output shows the path to the `.nupkg` file.</span></span>

```output
Microsoft (R) Build Engine version 16.1.76+g14b0a930a7 for .NET Framework
Copyright (C) Microsoft Corporation. All rights reserved.

Build started 8/5/2019 3:09:15 PM.
Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" on node 1 (pack target(s)).
GenerateTargetFrameworkMonikerAttribute:
Skipping target "GenerateTargetFrameworkMonikerAttribute" because all output files are up-to-date with respect to the input files.
CoreCompile:
  ...
CopyFilesToOutputDirectory:
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.dll" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll".
  ClassLib_DotNetStandard -> C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.dll
  Copying file from "C:\Users\username\source\repos\ClassLib_DotNetStandard\obj\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb" to "C:\Use
  rs\username\source\repos\ClassLib_DotNetStandard\bin\Debug\netstandard2.0\ClassLib_DotNetStandard.pdb".
GenerateNuspec:
  Successfully created package 'C:\Users\username\source\repos\ClassLib_DotNetStandard\bin\Debug\AppLogger.1.0.0.nupkg'.
Done Building Project "C:\Users\username\source\repos\ClassLib_DotNetStandard\ClassLib_DotNetStandard.csproj" (pack target(s)).

Build succeeded.
    0 Warning(s)
    0 Error(s)

Time Elapsed 00:00:01.21
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="4e841-147">ビルド時に自動的にパッケージを生成する</span><span class="sxs-lookup"><span data-stu-id="4e841-147">Automatically generate package on build</span></span>

<span data-ttu-id="4e841-148">プロジェクトのビルドまたは復元時に自動的に `msbuild -t:pack` を実行させるには、プロジェクト ファイルの `<PropertyGroup>` 内に次の行を追加します。</span><span class="sxs-lookup"><span data-stu-id="4e841-148">To automatically run `msbuild -t:pack` when you build or restore the project, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

<span data-ttu-id="4e841-149">ソリューション上で `msbuild -t:pack` を実行した場合、これにより、パック化可能なソリューション内のすべてのプロジェクトがパックされます ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) プロパティは `true` に設定されます)。</span><span class="sxs-lookup"><span data-stu-id="4e841-149">When you run `msbuild -t:pack` on a solution, this packs all the projects in the solution that are packable ([<IsPackable>](/dotnet/core/tools/csproj#nuget-metadata-properties) property is set to `true`).</span></span>

> [!NOTE]
> <span data-ttu-id="4e841-150">パッケージを自動的に生成する場合、パックする時間によってプロジェクトのビルド時間が長くなります。</span><span class="sxs-lookup"><span data-stu-id="4e841-150">When you automatically generate the package, the time to pack increases the build time for your project.</span></span>

### <a name="test-package-installation"></a><span data-ttu-id="4e841-151">パッケージ インストールのテスト</span><span class="sxs-lookup"><span data-stu-id="4e841-151">Test package installation</span></span>

<span data-ttu-id="4e841-152">パッケージを公開する前に、通常、パッケージをプロジェクトにインストールするプロセスをテストします。</span><span class="sxs-lookup"><span data-stu-id="4e841-152">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="4e841-153">このテストにより、必要なファイルがすべて、プロジェクト内の適切な場所に入ります。</span><span class="sxs-lookup"><span data-stu-id="4e841-153">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="4e841-154">インストールは Visual Studio またはコマンド ラインで手動テストできます。通常の[パッケージ インストール手順](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)を利用します。</span><span class="sxs-lookup"><span data-stu-id="4e841-154">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4e841-155">パッケージは不変です。</span><span class="sxs-lookup"><span data-stu-id="4e841-155">Packages are immutable.</span></span> <span data-ttu-id="4e841-156">問題を修正する場合は、パッケージ内容を変更して、もう一度パックしてください。再テスト時に、[グローバル パッケージのフォルダーをクリアする](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders)までは、古いバージョンのパッケージを引き続き使用することになります。</span><span class="sxs-lookup"><span data-stu-id="4e841-156">If you correct a problem, change the contents of the package and pack again, when you retest you will still be using the old version of the package until you [clear your global packages](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders) folder.</span></span> <span data-ttu-id="4e841-157">どのビルド時でも、一意のプレリリース ラベルを使用しないパッケージをテストする場合に、これは特に該当します。</span><span class="sxs-lookup"><span data-stu-id="4e841-157">This is especially relevant when testing packages that don't use a unique prerelease label on every build.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e841-158">次の手順</span><span class="sxs-lookup"><span data-stu-id="4e841-158">Next Steps</span></span>

<span data-ttu-id="4e841-159">`.nupkg` ファイルとなるパッケージを作成したら、「[パッケージの公開](../nuget-org/publish-a-package.md)」の説明にあるように、選択したギャラリーにパッケージを公開できます。</span><span class="sxs-lookup"><span data-stu-id="4e841-159">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="4e841-160">パッケージの機能を拡張したり、次のトピックで説明するように、その他の方法で他のシナリオをサポートしたりすると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="4e841-160">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="4e841-161">MSBuild ターゲットとしての NuGet の pack と restore</span><span class="sxs-lookup"><span data-stu-id="4e841-161">NuGet pack and restore as MSBuild targets</span></span>](../reference/msbuild-targets.md)
- [<span data-ttu-id="4e841-162">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="4e841-162">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="4e841-163">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="4e841-163">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="4e841-164">ソース ファイルと構成ファイルの変換</span><span class="sxs-lookup"><span data-stu-id="4e841-164">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="4e841-165">ローカリゼーション</span><span class="sxs-lookup"><span data-stu-id="4e841-165">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="4e841-166">プレリリース バージョン</span><span class="sxs-lookup"><span data-stu-id="4e841-166">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)
- [<span data-ttu-id="4e841-167">パッケージの種類の設定</span><span class="sxs-lookup"><span data-stu-id="4e841-167">Set package type</span></span>](../create-packages/set-package-type.md)
- [<span data-ttu-id="4e841-168">COM 相互運用アセンブリを含むパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="4e841-168">Create packages with COM interop assemblies</span></span>](../create-packages/author-packages-with-COM-interop-assemblies.md)

<span data-ttu-id="4e841-169">最後になりますが、次のような種類のパッケージもあります。</span><span class="sxs-lookup"><span data-stu-id="4e841-169">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="4e841-170">ネイティブ パッケージ</span><span class="sxs-lookup"><span data-stu-id="4e841-170">Native Packages</span></span>](../guides/native-packages.md)
- [<span data-ttu-id="4e841-171">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="4e841-171">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
