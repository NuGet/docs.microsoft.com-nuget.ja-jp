---
title: "Visual Studio 2017 での .NET Standard 2.0 NuGet パッケージの作成 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 5/23/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 2c1de334-fdc9-4e1e-8ef6-a90b3e77ff0f
description: "NuGet 4.x と Visual Studio 2017 を使用して、.NET Standard 2.0 NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。"
keywords: "パッケージを作成する, .NET Standard パッケージ, .NET Core"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b48ad2f062fd3a9b99985dbda6f89e6039dac4d
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="create-net-standard-20-packages-with-visual-studio-2017"></a><span data-ttu-id="f4992-104">Visual Studio 2017 での .NET Standard 2.0 パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="f4992-104">Create .NET Standard 2.0 packages with Visual Studio 2017</span></span>

<span data-ttu-id="f4992-105">*Visual Studio 2017 Update 3 で提供される NuGet 4.x 以降および MSBuild 15.3 以降に適用されます。Visual Studio 2017 の以前のバージョンについては、これらの手順は \<TargetFramework\> プロパティを変更した .NET Standard 1.4 から 1.6 に当てはまります。NuGet 3.x 以降を使用して作業を行う場合は、「[Visual Studio 2015 での .NET Standard パッケージの作成](../guides/create-net-standard-packages-vs2015.md)」も参照してください。*</span><span class="sxs-lookup"><span data-stu-id="f4992-105">*Applies to NuGet 4.x+ and MSBuild 15.3+ as provided with Visual Studio 2017 Update 3. For earlier versions of Visual Studio 2017, these instructions apply to .NET Standard 1.4 to 1.6 by changing the \<TargetFramework\> property. Also see [Create .NET Standard Packages with Visual Studio 2015](../guides/create-net-standard-packages-vs2015.md) for working with NuGet 3.x+.*</span></span>

<span data-ttu-id="f4992-106">[.NET Standard ライブラリ](/dotnet/articles/standard/library)は、すべての .NET ランタイムで使用できるようにすることを目的とした .NET API の正式な仕様です。したがって、.NET エコシステムでより高い統一性が確立されます。</span><span class="sxs-lookup"><span data-stu-id="f4992-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="f4992-107">.NET Standard Library は、ワークロードに関係なく、すべての .NET プラットフォーム用に統一された BCL (基本クラス ライブラリ) API のセットを定義して実装します。</span><span class="sxs-lookup"><span data-stu-id="f4992-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="f4992-108">これにより、開発者はすべての .NET ランタイム間で使用可能な PCL を生成でき、共有コードでプラットフォーム固有の条件付きコンパイル ディレクティブを除去するまでとはいかないまでも減らすことはできます。</span><span class="sxs-lookup"><span data-stu-id="f4992-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="f4992-109">このガイドでは、Visual Studio 2017 Update 3 と NuGet 4.0 を使用した .NET Standard Library 2.0 をターゲットとする nuget パッケージの作成について説明します。</span><span class="sxs-lookup"><span data-stu-id="f4992-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 2.0 with Visual Studio 2017 Update 3 and NuGet 4.0.</span></span>

1. [<span data-ttu-id="f4992-110">前提条件</span><span class="sxs-lookup"><span data-stu-id="f4992-110">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="f4992-111">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="f4992-111">Create the class library project</span></span>](#create-the-netstandard-class-library-project)
1. [<span data-ttu-id="f4992-112">.csproj ファイル内のメタデータを編集する</span><span class="sxs-lookup"><span data-stu-id="f4992-112">Edit metadata in the .csproj file</span></span>](#edit-metadata-in-the-csproj-file)
1. [<span data-ttu-id="f4992-113">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="f4992-113">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="f4992-114">関連トピック</span><span class="sxs-lookup"><span data-stu-id="f4992-114">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="f4992-115">前提条件</span><span class="sxs-lookup"><span data-stu-id="f4992-115">Pre-requisites</span></span>

<span data-ttu-id="f4992-116">このチュートリアルでは、Visual Studio 2017 Update 3 と **.NET Core クロスプラットフォーム開発**ワークロードが必要です。</span><span class="sxs-lookup"><span data-stu-id="f4992-116">This walkthrough requires Visual Studio 2017 Update 3 with the **.NET Core cross-platform development** workload.</span></span> <span data-ttu-id="f4992-117">[visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。Professional Edition と Enterprise Edition も使用できます。</span><span class="sxs-lookup"><span data-stu-id="f4992-117">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/), or use the Professional and Enterprise editions.</span></span>

<span data-ttu-id="f4992-118">Visual Studio のインストーラーで、必要なワークロードは次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4992-118">The require workload appears as follows in the Visual Studio installer:</span></span>

![Visual Studio インストーラーの [.NET Core クロスプラット フォーム開発] ワークロード](media/NuGet4-01-Workload.png)

## <a name="create-the-net-standard-class-library-project"></a><span data-ttu-id="f4992-120">.NET Standard クラス ライブラリ プロジェクトの作成</span><span class="sxs-lookup"><span data-stu-id="f4992-120">Create the .NET Standard class library project</span></span>

1. <span data-ttu-id="f4992-121">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に移動し、**[Visual C#]、[.NET Standard]** ノードの順に展開して、**[Class Library (Net Standard)]\(クラス ライブラリ (.Net Standard)\)** を選択し、名前を AppLogger に変更してから [OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f4992-121">In Visual Studio, **File > New > Project**, expand the **Visual C# > .NET Standard** node, select **Class Library (Net Standard)**, change the name to AppLogger, and click OK.</span></span>

    ![新しいクラス ライブラリ プロジェクトを作成する](media/NuGet4-02-NewProject.png)

1. <span data-ttu-id="f4992-123">ビルド構成を **[リリース]** に変更します。</span><span class="sxs-lookup"><span data-stu-id="f4992-123">Change the build configuration to **Release**.</span></span>
1. <span data-ttu-id="f4992-124">ソリューション エクスプローラーで `AppLogger` プロジェクトを右クリックし、**[プロパティ]** を選択し、**[ビルド]** タブを選択し、**[XML ドキュメント ファイル]** のチェック ボックスをオンにし、ファイル名を単に `AppLogger.xml` に設定します。</span><span class="sxs-lookup"><span data-stu-id="f4992-124">Right-click the `AppLogger` project in Solution Explorer, select **Properties**, select the **Build** tab, check the box for **XML documentation file**, and set the filename to just `AppLogger.xml`.</span></span> <span data-ttu-id="f4992-125">次いでプロジェクトを保存します。</span><span class="sxs-lookup"><span data-stu-id="f4992-125">Then save the project.</span></span>

1. <span data-ttu-id="f4992-126">次のように、コンポーネントにコードを追加します (ここではコンソールにメッセージが明確に出力されるのみです)。</span><span class="sxs-lookup"><span data-stu-id="f4992-126">Add your code to the component, such as the following (which clearly just outputs messages to the console):</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                Console.WriteLine(text);
            }
        }
    }
    ```

1. <span data-ttu-id="f4992-127">プロジェクト (Release 構成の) をビルドし、DLL および XML ファイルが `bin\Release\netstandard2.0` フォルダー内に生成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f4992-127">Build the project (with the Release configuration) and check that DLL and XML files are produced within the `bin\Release\netstandard2.0` folder.</span></span>

## <a name="edit-metadata-in-the-csproj-file"></a><span data-ttu-id="f4992-128">.csproj ファイルでメタデータを編集する</span><span class="sxs-lookup"><span data-stu-id="f4992-128">Edit metadata in the .csproj file</span></span>

<span data-ttu-id="f4992-129">NuGet 4.0 と .NET Core のプロジェクトでは、パッケージのメタデータは、`.nuspec` などの外部ファイルではなく `.csproj` ファイルに直接含まれます。</span><span class="sxs-lookup"><span data-stu-id="f4992-129">With NuGet 4.0 and .NET Core projects, package metadata is contained directly in the `.csproj` file instead of external files such as a `.nuspec`.</span></span> <span data-ttu-id="f4992-130">そのメタデータの完全な説明については、「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target)」 (NuGet パックと MSBuild のターゲットとしての復元) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f4992-130">A full description of that metadata is found in [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

1. <span data-ttu-id="f4992-131">ソリューション エクスプローラーでプロジェクトを右クリックし、**[Edit AppLogger.csproj]\(AppLogger.csproj の編集\)** を選択し、最初のプロパティ グループを編集して次のようにパッケージ情報が含まれるようにします。</span><span class="sxs-lookup"><span data-stu-id="f4992-131">Right-click the project in Solution Explorer, select **Edit AppLogger.csproj**, and then edit the first property group to include package information such as the following:</span></span>

    ```xml
    <PropertyGroup>
        <TargetFramework>netstandard2.0</TargetFramework>
        <PackageId>AppLogger.YOUR_NAME</PackageId>
        <PackageVersion>1.0.0</PackageVersion>
        <Authors>YOUR_NAME</Authors>
        <Description>Awesome application logging utility</Description>
        <PackageRequireLicenseAcceptance>false</PackageRequireLicenseAcceptance>
        <PackageReleaseNotes>First release</PackageReleaseNotes>
        <Copyright>Copyright 2017 (c) Contoso Corporation. All rights reserved.</Copyright>
        <PackageTags>logger logging logs</PackageTags>
    </PropertyGroup>
    ```

1. <span data-ttu-id="f4992-132">プロジェクトを保存し、ソリューションを右クリックし、**[ソリューションのビルド]** を選択し、パッケージのすべてのファイルをここでは正しいメタデータで生成します。</span><span class="sxs-lookup"><span data-stu-id="f4992-132">Save the project, then right-click the solution and select **Build Solution** to again generate all the files for the package, this time with the correct metadata.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="f4992-133">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="f4992-133">Package the component</span></span>

<span data-ttu-id="f4992-134">NuGet 4.0 は、前のセクションで追加したように、プロジェクトに必要なパッケージ メタデータが含まれる場合、MSBuild バージョン 15.1 以降を使用したパック ターゲット (Visual Studio 2017 Update 3 の一部として MSBuild 15.3 を含む) をサポートします。</span><span class="sxs-lookup"><span data-stu-id="f4992-134">NuGet 4.0 supports a pack target using MSBuild version 15.1+ (including MSBuild 15.3 as part of Visual Studio 2017 Update 3) when the project contains the necessary package metadata, as was added in the previous section.</span></span> <span data-ttu-id="f4992-135">この方法で MSBuild を呼び出すには、`.csproj` ファイルと同じフォルダーに、コマンド ラインで単純にパック ターゲットを指定します。</span><span class="sxs-lookup"><span data-stu-id="f4992-135">To invoke MSBuild in this way, simply specify the pack target on the command line in the same folder as the `.csproj` file:</span></span>

    msbuild /t:pack /p:Configuration=Release

<span data-ttu-id="f4992-136">コンテンツ ファイル、シンボル、ソース コードなどを含める `msbuild /t:pack` のその他のオプションについては、「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target)」 (NuGet パックと MSBuild のターゲットとしての復元) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f4992-136">For additional options with `msbuild /t:pack`, such as including content files, symbols, and source code, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md#pack-target).</span></span>

<span data-ttu-id="f4992-137">いずれの場合も、上記のコマンドは、その構成をビルドする際に、既定で `bin\Release` フォルダーに `AppLogger.YOUR_NAME.1.0.0.nupkg` が生成されます。</span><span class="sxs-lookup"><span data-stu-id="f4992-137">In any case, the command above generates `AppLogger.YOUR_NAME.1.0.0.nupkg` in the `bin\Release` folder by default, as it builds that configuration.</span></span> <span data-ttu-id="f4992-138">`/p` スイッチを省略した場合、既定の構成は `Debug` になります。</span><span class="sxs-lookup"><span data-stu-id="f4992-138">If you omit the `/p` switch, the default configuration will be `Debug`.</span></span> 

<span data-ttu-id="f4992-139">[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4992-139">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![AppLogger パッケージが表示された NuGet パッケージ エクスプローラー](media/NuGet4-03-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="f4992-141">`.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="f4992-141">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="f4992-142">したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。</span><span class="sxs-lookup"><span data-stu-id="f4992-142">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="f4992-143">パッケージを他の開発者が使用できるようにする場合は、「[パッケージの公開](../create-packages/publish-a-package.md)」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="f4992-143">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="f4992-144">関連トピック</span><span class="sxs-lookup"><span data-stu-id="f4992-144">Related topics</span></span>

- <span data-ttu-id="f4992-145">「[Package References in Project Files](../consume-packages/package-references-in-project-files.md)」 (プロジェクト ファイル内のパッケージ参照) では、プロジェクト ファイルに直接パッケージを記述する場合の詳細がすべて説明されています。</span><span class="sxs-lookup"><span data-stu-id="f4992-145">[Package References in Project Files](../consume-packages/package-references-in-project-files.md) describes all the details of describing your package directly in the project file.</span></span>
- <span data-ttu-id="f4992-146">「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md)」 (NuGet パックと MSBuild のターゲットとしての復元) では、パッケージを作成するために `msbuild /t:pack` を使用するすべてのオプションが説明されています。</span><span class="sxs-lookup"><span data-stu-id="f4992-146">[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md) describes all the options for using `msbuild /t:pack` to create the package.</span></span>
- [<span data-ttu-id="f4992-147">.NET Standard ライブラリのドキュメント</span><span class="sxs-lookup"><span data-stu-id="f4992-147">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="f4992-148">.NET Framework から .NET Core への移植</span><span class="sxs-lookup"><span data-stu-id="f4992-148">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
