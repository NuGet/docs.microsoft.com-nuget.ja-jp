---
title: "Visual Studio 2015 での .NET Standard NuGet パッケージの作成 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 29b3bceb-0f35-4cdd-bbc3-a04eb823164c
description: "NuGet 3.x と Visual Studio 2015 を使用して、.NET Standard NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。"
keywords: "パッケージを作成する, .NET Standard パッケージ, .NET Standard マッピング テーブル"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: a912c27e1873d60426f2147995f69e2dcc433ca9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="de8e5-104">Visual Studio 2015 での .NET Standard NuGet パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="de8e5-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="de8e5-105">*NuGet 3.x に適用されます。NuGet 4.x+ を使用して作業を行う場合は、[Visual Studio 2017 での .NET Standard パッケージの作成](../guides/create-net-standard-packages-vs2017.md)に関するページを参照してください。*</span><span class="sxs-lookup"><span data-stu-id="de8e5-105">*Applies to NuGet 3.x. See [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="de8e5-106">[.NET Standard ライブラリ](https://docs.microsoft.com/dotnet/articles/standard/library)は、すべての .NET ランタイムで使用できるようにすることを目的とした .NET API の正式な仕様です。したがって、.NET エコシステムでより高い統一性が確立されます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-106">The [.NET Standard Library](https://docs.microsoft.com/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="de8e5-107">.NET Standard Library は、ワークロードに関係なく、すべての .NET プラットフォーム用に統一された BCL (基本クラス ライブラリ) API のセットを定義して実装します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="de8e5-108">これにより、開発者はすべての .NET ランタイム間で使用可能な PCL を生成でき、共有コードでプラットフォーム固有の条件付きコンパイル ディレクティブを除去するまでとはいかないまでも減らすことはできます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-108">It enables developers to produce PCLs that are usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="de8e5-109">このガイドでは、.NET Standard Library 1.4 をターゲットとする nuget パッケージの作成方法を示します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-109">This guide will walk you through creating a nuget package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="de8e5-110">これは、.NET Framework 4.6.1、ユニバーサル Windows プラットフォーム 10、.NET Core、および Mono/Xamarin に適用できます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-110">This will work across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="de8e5-111">詳細については、このトピックの後半の「[.NET Standard マッピング テーブル](#net-standard-mapping-table)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

1. [<span data-ttu-id="de8e5-112">前提条件</span><span class="sxs-lookup"><span data-stu-id="de8e5-112">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="de8e5-113">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="de8e5-113">Create the class library project</span></span>](#create-the-class-library-project)
1. [<span data-ttu-id="de8e5-114">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="de8e5-114">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="de8e5-115">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="de8e5-115">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="de8e5-116">追加オプション</span><span class="sxs-lookup"><span data-stu-id="de8e5-116">Additional options</span></span>](#additional-options)
1. [<span data-ttu-id="de8e5-117">.NET Standard マッピング テーブル</span><span class="sxs-lookup"><span data-stu-id="de8e5-117">.NET Standard mapping table</span></span>](#net-standard-mapping-table)
1. [<span data-ttu-id="de8e5-118">関連トピック</span><span class="sxs-lookup"><span data-stu-id="de8e5-118">Related topics</span></span>](#related-topics)


## <a name="pre-requisites"></a><span data-ttu-id="de8e5-119">前提条件</span><span class="sxs-lookup"><span data-stu-id="de8e5-119">Pre-requisites</span></span>

1. <span data-ttu-id="de8e5-120">Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="de8e5-120">Visual Studio 2015.</span></span> <span data-ttu-id="de8e5-121">[visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。もちろん、Professional Edition と Enterprise Edition も使用できます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-121">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span>
1. <span data-ttu-id="de8e5-122">.NET Core: [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849) から、Visual Studio 2015 用のテンプレートとその他のツールと共に .NET Core をインストールします。</span><span class="sxs-lookup"><span data-stu-id="de8e5-122">.NET Core: Install .NET Core along with templates and other tools for Visual Studio 2015 from [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849).</span></span>
1. <span data-ttu-id="de8e5-123">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="de8e5-123">NuGet CLI.</span></span> <span data-ttu-id="de8e5-124">[nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの nuget.exe をダウンロードして、任意の場所に保存します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-124">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="de8e5-125">次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。</span><span class="sxs-lookup"><span data-stu-id="de8e5-125">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="de8e5-126">nuget.exe はインストーラーではなく CLI ツール自体です。したがって、ブラウザーからダウンロードしたファイルは実行するのではなく、必ず保存してください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-126">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>



## <a name="create-the-class-library-project"></a><span data-ttu-id="de8e5-127">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="de8e5-127">Create the class library project</span></span>

1. <span data-ttu-id="de8e5-128">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に移動し、**[Visual C#]、[Windows]** ノードの順に展開して **[クラス ライブラリ (ポータブル)]** を選択し、名前を AppLogger に変更してから [OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="de8e5-128">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![新しいクラス ライブラリ プロジェクトを作成する](media/NetStandard-NewProject.png)

1. <span data-ttu-id="de8e5-130">表示された **[ポータブル クラス ライブラリの追加]** ダイアログ ボックスで、`.NET Framework 4.6` と `ASP.NET Core 1.0` オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-130">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>
1. <span data-ttu-id="de8e5-131">ソリューション エクスプローラーで `AppLogger (Portable)` を右クリックして **[プロパティ]** を選択し、**[ライブラリ]** タブを選択してから **[ターゲット]** セクションの **[ターゲットの .NET Platform Standard]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="de8e5-131">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="de8e5-132">これで確認のプロンプトが表示されます。その後、ドロップダウンから `.NET Standard 1.4` を選択できます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-132">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![.NET Standard 1.4 へのターゲットの設定](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="de8e5-134">**[ビルド]** タブをクリックして **[構成]** を `Release` に変更し、**[XML ドキュメント ファイル]** のボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="de8e5-134">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>
1. <span data-ttu-id="de8e5-135">たとえば、次のようにコンポーネントにコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-135">Add your code to the component, for example:</span></span>

    ```cs
    namespace AppLogger
    {
        public class Logger
        {
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log");
            }
        }
    }
    ```

1. <span data-ttu-id="de8e5-136">プロジェクト (Release 構成の) をビルドし、DLL および XML ファイルが bin\Release フォルダー内に生成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-136">Build the project (with the Release configuration) and check that DLL and XML files are produced within the bin\Release folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="de8e5-137">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="de8e5-137">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="de8e5-138">コマンド プロンプトを開き、(`.sln` ファイルの 1 レベル下の) `AppLogg.csproj` フォルダーを含むフォルダーに移動して NuGet `spec` コマンドを実行し、初期 `AppLogger.nuspec` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-138">Open a command prompt, navigate to the folder containing `AppLogg.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="de8e5-139">`AppLogger.nuspec` をエディターで開き、以下の内容と一致するように更新して、YOUR_NAME を適切な値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-139">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="de8e5-140">具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則を参照)。</span><span class="sxs-lookup"><span data-stu-id="de8e5-140">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="de8e5-141">また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-141">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>AppLogger.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>AppLogger</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016 (c) Contoso Corporation. All rights reserved.</copyright>
    <tags>logger logging logs</tags>
    </metadata>
</package>
```

1. <span data-ttu-id="de8e5-142">参照アセンブリを `.nuspec` ファイル、つまり、ライブラリの DLL および IntelliSense XML ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-142">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="de8e5-143">ソリューションを右クリックし、**[ソリューションのビルド]** を選択してパッケージのすべてのファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-143">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>


## <a name="package-the-component"></a><span data-ttu-id="de8e5-144">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="de8e5-144">Package the component</span></span>

<span data-ttu-id="de8e5-145">パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-145">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack AppLogger.nuspec
```

<span data-ttu-id="de8e5-146">これで `AppLogger.YOUR_NAME.1.0.0.nupkg` が生成されます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-146">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="de8e5-147">[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-147">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![AppLogger パッケージが表示された NuGet パッケージ エクスプローラー](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="de8e5-149">`.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="de8e5-149">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="de8e5-150">したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-150">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="de8e5-151">パッケージを他の開発者が使用できるようにする場合は、[パッケージの発行](../create-packages/publish-a-package.md)に関するページの手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-151">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="de8e5-152">`pack` には Mac OS X の場合は Mono 4.4.2 が必要であり、Linux 1 システムでは動作しないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-152">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="de8e5-153">Mac の場合、`.nuspec` ファイルの Windows パス名を Unix 形式のパスに変換する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="de8e5-153">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="additional-options"></a><span data-ttu-id="de8e5-154">[追加オプション]</span><span class="sxs-lookup"><span data-stu-id="de8e5-154">Additional options</span></span>

<span data-ttu-id="de8e5-155">次のセクションでは、NuGet パッケージを作成する場合の追加オプションについて説明します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-155">The following sections go into additional options for NuGet package creation:</span></span>

- [<span data-ttu-id="de8e5-156">依存関係の宣言</span><span class="sxs-lookup"><span data-stu-id="de8e5-156">Declaring dependencies</span></span>](#declaring-dependencies)
- [<span data-ttu-id="de8e5-157">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="de8e5-157">Supporting multiple target frameworks</span></span>](#supporting-multiple-target-frameworks)
- [<span data-ttu-id="de8e5-158">MSBuild のターゲットとプロパティの追加</span><span class="sxs-lookup"><span data-stu-id="de8e5-158">Adding targets and props for MSBuild</span></span>](#adding-targets-and-props-for-msbuild)
- [<span data-ttu-id="de8e5-159">ローカライズされたパッケージの作成</span><span class="sxs-lookup"><span data-stu-id="de8e5-159">Creating localized packages</span></span>](#creating-localized-packages)
- [<span data-ttu-id="de8e5-160">Readme の追加</span><span class="sxs-lookup"><span data-stu-id="de8e5-160">Adding a readme</span></span>](#adding-a-readme)

### <a name="declaring-dependencies"></a><span data-ttu-id="de8e5-161">依存関係の宣言</span><span class="sxs-lookup"><span data-stu-id="de8e5-161">Declaring dependencies</span></span>

<span data-ttu-id="de8e5-162">他の NuGet パッケージに対する依存関係がある場合、`<group>` 要素を使用して `<dependencies>` 要素で依存関係をリストします。</span><span class="sxs-lookup"><span data-stu-id="de8e5-162">If you have any dependencies on other NuGet packages, list those in the `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="de8e5-163">たとえば、NewtonSoft.Json 8.0.3 以降に対する依存関係を宣言するには、以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-163">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="de8e5-164">*version* 属性の構文は、バージョン 8.0.3 以降が許容されることを示します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-164">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="de8e5-165">別のバージョンの範囲を指定する場合は、「[パッケージのバージョン管理](../reference/package-versioning.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-165">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="supporting-multiple-target-frameworks"></a><span data-ttu-id="de8e5-166">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="de8e5-166">Supporting multiple target frameworks</span></span>

<span data-ttu-id="de8e5-167">たとえば、.NET Standard 1.4 で使用できない .NET Framework 4.6.2 の API を活用するとします。</span><span class="sxs-lookup"><span data-stu-id="de8e5-167">Suppose you'd like to take advantage of an API in .NET Framework 4.6.2 that is not available in .NET Standard 1.4.</span></span> <span data-ttu-id="de8e5-168">これを行うには、まず、条件付きコンパイルまたは共有プロジェクトを使用して、.NET 4.6.2 用にライブラリがコンパイルされていることを確認する必要があります </span><span class="sxs-lookup"><span data-stu-id="de8e5-168">To do this, you'll first need to make sure the library compiles for .NET 4.6.2 by using conditional compilation or shared projects.</span></span> <span data-ttu-id="de8e5-169">(Visual Studio では、NetCore プロジェクトを作成し、任意のフレームワークを複数のフレームワーク セクションに追加してからビルドできます)。次に、以下のように単純な規則に基づく作業ディレクトリを使用して、パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-169">(In Visual Studio, you can create a NetCore project, add the framework of choice to the multiple framework section, and then build.) Then you create the package using the simple convention-based working directory technique as follows:</span></span>

1. <span data-ttu-id="de8e5-170">`.nuspec` ファイルを含むプロジェクトのルート フォルダーで、`lib` という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-170">In the project's root folder containing your `.nuspec` file, create a folder named `lib`.</span></span>
1. <span data-ttu-id="de8e5-171">`lib` 内で、サポートするプラットフォームごとにフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-171">Inside `lib`, create folders for each platform you want to support:</span></span>

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. <span data-ttu-id="de8e5-172">`.nuspec` ファイルで、`package` ノードの下に `files` ノードを追加し、ワイルドカードを使用して `lib` のファイルを参照します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-172">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `lib` using wildcards.</span></span> <span data-ttu-id="de8e5-173">**注:** 規則に基づく作業ディレクトリの方法ではトークン置換はサポートされないため、リテラル値に置き換えてください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-173">**Note:** Token replacements are not supported with the convention-based working directory approach, so replace them with literal values:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>AppLogger.YOUR_NAME</id>
        <version>1.0.0.0</version>
        <title>AppLogger</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
        <files>
            <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="de8e5-174">`nuget pack AppLogger.spec` を使用して、もう一度パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-174">Create the package again using `nuget pack AppLogger.spec`.</span></span>

<span data-ttu-id="de8e5-175">この方法の使用の詳細については、「[Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)」 (複数の .NET Framework バージョンのサポート) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-175">For more details on using this technique, see [Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)</span></span>

### <a name="adding-targets-and-props-for-msbuild"></a><span data-ttu-id="de8e5-176">MSBuild のターゲットとプロパティの追加</span><span class="sxs-lookup"><span data-stu-id="de8e5-176">Adding targets and props for MSBuild</span></span>

<span data-ttu-id="de8e5-177">ビルド時のカスタム ツールまたはプロセスの実行など、場合によっては、パッケージを使用するプロジェクト内のカスタム ビルド ターゲットまたはプロパティを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="de8e5-177">In some cases you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="de8e5-178">これは、以下の手順で説明されているように `\build` フォルダーにファイルを追加することで行うことができます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-178">You do this by adding files in a `\build` folder as described in the steps below.</span></span> <span data-ttu-id="de8e5-179">NuGet は \build ファイルを使用してパッケージをインストールすると、.targets および .props ファイルを指すプロジェクト ファイルに MSBuild 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-179">When NuGet installs a package with \build files, it adds an MSBuild element in the project file pointing to the .targets and .props files.</span></span>

> [!Note]
> <span data-ttu-id="de8e5-180">`project.json` を使用する場合、ターゲットはプロジェクトに追加されませんが、`project.lock.json` を通じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-180">When using `project.json`, targets are not added to the project but are made available through the `project.lock.json`.</span></span>


1. <span data-ttu-id="de8e5-181">`.nuspec` ファイルを含むプロジェクト フォルダーで、`build` という名前のフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-181">In the project folder containing the your `.nuspec` file, create a folder named `build`.</span></span>
1. <span data-ttu-id="de8e5-182">`build` 内で、サポート対象ごとにフォルダーを作成し、その中に `.targets` と `.props` ファイルを配置します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-182">Inside `build`, create folders for each supported, and within those place your `.targets` and `.props` files:</span></span>

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. <span data-ttu-id="de8e5-183">`.nuspec` ファイルで、`package` ノードの下に `files` ノードを追加し、ワイルドカードを使用して `build` のファイルを参照します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-183">In the `.nuspec` file, add a `files` node under the `package` node and refer to the files in `build` using wildcards.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>...
        </metadata>
        <files>
            <file src="build\**" target="build" />
        </files>
    </package>
    ```

1. <span data-ttu-id="de8e5-184">`nuget pack AppLogger.nuspec` を使用して、もう一度パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-184">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>

<span data-ttu-id="de8e5-185">詳細については、「[パッケージに MSBuild プロパティとターゲットを含める](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="de8e5-185">For additional details, refer to [Include MSBuild props and targets in a package](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package).</span></span>


### <a name="creating-localized-packages"></a><span data-ttu-id="de8e5-186">ローカライズされたパッケージの作成</span><span class="sxs-lookup"><span data-stu-id="de8e5-186">Creating localized packages</span></span>

<span data-ttu-id="de8e5-187">ローカライズ版のライブラリを作成する場合は、ロケールごとに別のパッケージを作成するか、単一のパッケージ内にローカライズされたリソース アセンブリを含めることができます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-187">To create localized versions of your library, you can either create separate packages for different locales, or include localized resource assemblies within a single package.</span></span> <span data-ttu-id="de8e5-188">ここでは、ドイツ語とイタリア語の場合の後者の方法を実行する方法を説明します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-188">Here's how to do the latter approach for German and Italian:</span></span>

1. <span data-ttu-id="de8e5-189">`lib` の下の各ターゲット フレームワーク フォルダー内で、既定の英語以外のサポートされている言語ごとにフォルダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-189">Within each target framework folder under `lib`, create folders for each supported language other than the English default.</span></span> <span data-ttu-id="de8e5-190">これらのフォルダーには、リソース アセンブリおよびローカライズされた IntelliSense XML ファイルを配置できます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-190">In these folders you can place resource assemblies  and localized IntelliSense XML files.</span></span> <span data-ttu-id="de8e5-191">例:</span><span class="sxs-lookup"><span data-stu-id="de8e5-191">For example:</span></span>

        lib
        ├───netstandard1.4
        │   │   AppLogger.dll
        │   │   AppLogger.xml
        │   │
        │   ├───de
        │   │       AppLogger.resources.dll
        │   │       AppLogger.xml
        │   │
        │   └───it
        │           AppLogger.resources.dll
        │           AppLogger.xml
        └───net462
            │   AppLogger.dll
            │   AppLogger.xml
            │
            ├───de
            │       AppLogger.resources.dll
            │       AppLogger.xml
            │
            └───it
                    AppLogger.resources.dll
                    AppLogger.xml

1. <span data-ttu-id="de8e5-192">`.nuspec` ファイルで、`<files>` ノードのこれらのファイルを参照します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-192">In the `.nuspec` file, reference these files in the `<files>` node:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>...
        </metadata>
        <files>
        <file src="lib\**" target="lib" />
        </files>
    </package>
    ```

1. <span data-ttu-id="de8e5-193">`nuget pack AppLogger.nuspec` を使用して、もう一度パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-193">Create the package again using `nuget pack AppLogger.nuspec`.</span></span>


### <a name="adding-a-readme"></a><span data-ttu-id="de8e5-194">Readme の追加</span><span class="sxs-lookup"><span data-stu-id="de8e5-194">Adding a readme</span></span>

<span data-ttu-id="de8e5-195">パッケージのルートに `readme.txt` ファイルを含めた場合、パッケージが直接インストールされたときに Visual Studio に表示されます。</span><span class="sxs-lookup"><span data-stu-id="de8e5-195">When you include a `readme.txt` file in the root of the package, Visual Studio will display it when the package is installed directly.</span></span>

> [!Note]
> <span data-ttu-id="de8e5-196">Readme ファイルは、依存関係としてインストールされているパッケージや、.NET Core プロジェクトの場合は表示されません。</span><span class="sxs-lookup"><span data-stu-id="de8e5-196">Readme files are not shown for packages that are installed as a dependency, or for .NET Core projects.</span></span>


<span data-ttu-id="de8e5-197">これを行うには、`readme.txt` ファイルを作成し、プロジェクト ルート ディレクトリに配置して、`.nuspec` ファイルで参照します。</span><span class="sxs-lookup"><span data-stu-id="de8e5-197">To do this, create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>...
    </metadata>
    <files>
    <file src="readme.txt" target="" />
    </files>
</package>
```


## <a name="net-standard-mapping-table"></a><span data-ttu-id="de8e5-198">.NET Standard マッピング テーブル</span><span class="sxs-lookup"><span data-stu-id="de8e5-198">.NET Standard mapping table</span></span>

|<span data-ttu-id="de8e5-199">プラットフォーム名</span><span class="sxs-lookup"><span data-stu-id="de8e5-199">Platform Name</span></span> |<span data-ttu-id="de8e5-200">Alias</span><span class="sxs-lookup"><span data-stu-id="de8e5-200">Alias</span></span>|
|--------------|-----|
|<span data-ttu-id="de8e5-201">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="de8e5-201">.NET Standard</span></span> | <span data-ttu-id="de8e5-202">netstandard</span><span class="sxs-lookup"><span data-stu-id="de8e5-202">netstandard</span></span>| <span data-ttu-id="de8e5-203">1.0</span><span class="sxs-lookup"><span data-stu-id="de8e5-203">1.0</span></span>| <span data-ttu-id="de8e5-204">1.1</span><span class="sxs-lookup"><span data-stu-id="de8e5-204">1.1</span></span>| <span data-ttu-id="de8e5-205">1.2</span><span class="sxs-lookup"><span data-stu-id="de8e5-205">1.2</span></span>| <span data-ttu-id="de8e5-206">1.3</span><span class="sxs-lookup"><span data-stu-id="de8e5-206">1.3</span></span>| <span data-ttu-id="de8e5-207">1.4</span><span class="sxs-lookup"><span data-stu-id="de8e5-207">1.4</span></span>| <span data-ttu-id="de8e5-208">1.5</span><span class="sxs-lookup"><span data-stu-id="de8e5-208">1.5</span></span>| <span data-ttu-id="de8e5-209">1.6</span><span class="sxs-lookup"><span data-stu-id="de8e5-209">1.6</span></span>|
|<span data-ttu-id="de8e5-210">.NET Core</span><span class="sxs-lookup"><span data-stu-id="de8e5-210">.NET Core</span></span> | <span data-ttu-id="de8e5-211">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="de8e5-211">netcoreapp</span></span>| <span data-ttu-id="de8e5-212">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-212">&#x2192;</span></span>| <span data-ttu-id="de8e5-213">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-213">&#x2192;</span></span>| <span data-ttu-id="de8e5-214">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-214">&#x2192;</span></span>| <span data-ttu-id="de8e5-215">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-215">&#x2192;</span></span>| <span data-ttu-id="de8e5-216">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-216">&#x2192;</span></span>| <span data-ttu-id="de8e5-217">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-217">&#x2192;</span></span>| <span data-ttu-id="de8e5-218">1.0</span><span class="sxs-lookup"><span data-stu-id="de8e5-218">1.0</span></span>|
|<span data-ttu-id="de8e5-219">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="de8e5-219">.NET Framework</span></span>| <span data-ttu-id="de8e5-220">net</span><span class="sxs-lookup"><span data-stu-id="de8e5-220">net</span></span>| <span data-ttu-id="de8e5-221">4.5</span><span class="sxs-lookup"><span data-stu-id="de8e5-221">4.5</span></span>| <span data-ttu-id="de8e5-222">4.5.1</span><span class="sxs-lookup"><span data-stu-id="de8e5-222">4.5.1</span></span>| <span data-ttu-id="de8e5-223">4.6</span><span class="sxs-lookup"><span data-stu-id="de8e5-223">4.6</span></span>| <span data-ttu-id="de8e5-224">4.6.1</span><span class="sxs-lookup"><span data-stu-id="de8e5-224">4.6.1</span></span>| <span data-ttu-id="de8e5-225">4.6.2</span><span class="sxs-lookup"><span data-stu-id="de8e5-225">4.6.2</span></span>| <span data-ttu-id="de8e5-226">4.6.3</span><span class="sxs-lookup"><span data-stu-id="de8e5-226">4.6.3</span></span>|
|<span data-ttu-id="de8e5-227">Mono/Xamarin プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="de8e5-227">Mono/Xamarin Platforms</span></span>| <span data-ttu-id="de8e5-228">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-228">&#x2192;</span></span>| <span data-ttu-id="de8e5-229">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-229">&#x2192;</span></span>| <span data-ttu-id="de8e5-230">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-230">&#x2192;</span></span>| <span data-ttu-id="de8e5-231">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-231">&#x2192;</span></span>| <span data-ttu-id="de8e5-232">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-232">&#x2192;</span></span>| <span data-ttu-id="de8e5-233">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-233">&#x2192;</span></span>|
|<span data-ttu-id="de8e5-234">ユニバーサル Windows プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="de8e5-234">Universal Windows Platform</span></span>| <span data-ttu-id="de8e5-235">uap</span><span class="sxs-lookup"><span data-stu-id="de8e5-235">uap</span></span>| <span data-ttu-id="de8e5-236">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-236">&#x2192;</span></span>| <span data-ttu-id="de8e5-237">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-237">&#x2192;</span></span>| <span data-ttu-id="de8e5-238">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-238">&#x2192;</span></span>| <span data-ttu-id="de8e5-239">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-239">&#x2192;</span></span>|<span data-ttu-id="de8e5-240">10.0</span><span class="sxs-lookup"><span data-stu-id="de8e5-240">10.0</span></span>|
|<span data-ttu-id="de8e5-241">Windows</span><span class="sxs-lookup"><span data-stu-id="de8e5-241">Windows</span></span>| <span data-ttu-id="de8e5-242">win</span><span class="sxs-lookup"><span data-stu-id="de8e5-242">win</span></span>| <span data-ttu-id="de8e5-243">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-243">&#x2192;</span></span>| <span data-ttu-id="de8e5-244">8.0</span><span class="sxs-lookup"><span data-stu-id="de8e5-244">8.0</span></span>| <span data-ttu-id="de8e5-245">8.1</span><span class="sxs-lookup"><span data-stu-id="de8e5-245">8.1</span></span>|
|<span data-ttu-id="de8e5-246">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="de8e5-246">Windows Phone</span></span>| <span data-ttu-id="de8e5-247">wpa</span><span class="sxs-lookup"><span data-stu-id="de8e5-247">wpa</span></span>| <span data-ttu-id="de8e5-248">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-248">&#x2192;</span></span>| <span data-ttu-id="de8e5-249">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="de8e5-249">&#x2192;</span></span>|<span data-ttu-id="de8e5-250">8.1</span><span class="sxs-lookup"><span data-stu-id="de8e5-250">8.1</span></span>|
|<span data-ttu-id="de8e5-251">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="de8e5-251">Windows Phone Silverlight</span></span>| <span data-ttu-id="de8e5-252">wp</span><span class="sxs-lookup"><span data-stu-id="de8e5-252">wp</span></span>| <span data-ttu-id="de8e5-253">8.0</span><span class="sxs-lookup"><span data-stu-id="de8e5-253">8.0</span></span>|



## <a name="related-topics"></a><span data-ttu-id="de8e5-254">関連トピック</span><span class="sxs-lookup"><span data-stu-id="de8e5-254">Related topics</span></span>

- [<span data-ttu-id="de8e5-255">.nuspec 参照</span><span class="sxs-lookup"><span data-stu-id="de8e5-255">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="de8e5-256">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="de8e5-256">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="de8e5-257">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="de8e5-257">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="de8e5-258">複数の .NET Framework バージョンのサポート</span><span class="sxs-lookup"><span data-stu-id="de8e5-258">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="de8e5-259">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="de8e5-259">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="de8e5-260">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="de8e5-260">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="de8e5-261">.NET Standard ライブラリのドキュメント</span><span class="sxs-lookup"><span data-stu-id="de8e5-261">.NET Standard Library documentation</span></span>](https://docs.microsoft.com/dotnet/articles/standard/library)
- [<span data-ttu-id="de8e5-262">.NET Framework から .NET Core への移植</span><span class="sxs-lookup"><span data-stu-id="de8e5-262">Porting to .NET Core from .NET Framework</span></span>](https://docs.microsoft.com/dotnet/articles/core/porting/index)
