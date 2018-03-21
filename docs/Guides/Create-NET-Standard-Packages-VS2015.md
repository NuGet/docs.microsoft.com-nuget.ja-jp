---
title: "Visual Studio 2015 での .NET Standard NuGet パッケージの作成 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/02/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "NuGet 3.x と Visual Studio 2015 を使用して、.NET Standard NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。"
keywords: "パッケージを作成する, .NET Standard パッケージ, .NET Standard マッピング テーブル"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: abf6a56cbc84bdd066e31e77c7883825a8456144
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="create-net-standard-packages-with-visual-studio-2015"></a><span data-ttu-id="fa047-104">Visual Studio 2015 での .NET Standard NuGet パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="fa047-104">Create .NET Standard packages with Visual Studio 2015</span></span>

<span data-ttu-id="fa047-105">*NuGet 3.x に適用されます。NuGet 4.x 以降を使用している場合は、[Visual Studio 2017 でのパッケージの作成と公開](../quickstart/create-and-publish-a-package-using-visual-studio.md)に関するページを参照してください。*</span><span class="sxs-lookup"><span data-stu-id="fa047-105">*Applies to NuGet 3.x. See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+.*</span></span>

<span data-ttu-id="fa047-106">[.NET Standard ライブラリ](/dotnet/articles/standard/library)は、すべての .NET ランタイムで使用できるようにすることを目的とした .NET API の正式な仕様です。したがって、.NET エコシステムでより高い統一性が確立されます。</span><span class="sxs-lookup"><span data-stu-id="fa047-106">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="fa047-107">.NET Standard Library は、ワークロードに関係なく、すべての .NET プラットフォーム用に統一された BCL (基本クラス ライブラリ) API のセットを定義して実装します。</span><span class="sxs-lookup"><span data-stu-id="fa047-107">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="fa047-108">これにより、開発者はすべての .NET ランタイム間で使用可能なコードを生成できます。また、共有コードでプラットフォーム固有の条件付きコンパイル ディレクティブを除去するまでとはいかないまでも減らすことはできます。</span><span class="sxs-lookup"><span data-stu-id="fa047-108">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="fa047-109">このガイドでは、.NET Standard Library 1.4 をターゲットとする NuGet パッケージの作成方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="fa047-109">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4.</span></span> <span data-ttu-id="fa047-110">このようなライブラリは、.NET Framework 4.6.1、ユニバーサル Windows プラットフォーム 10、.NET Core、および Mono/Xamarin に適用できます。</span><span class="sxs-lookup"><span data-stu-id="fa047-110">Such a library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="fa047-111">詳細については、このトピックの後半の「[.NET Standard マッピング テーブル](#net-standard-mapping-table)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fa047-111">For details, see the [.NET Standard mapping table](#net-standard-mapping-table) later in this topic.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa047-112">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="fa047-112">Prerequisites</span></span>

1. <span data-ttu-id="fa047-113">Visual Studio 2015 更新プログラム 3</span><span class="sxs-lookup"><span data-stu-id="fa047-113">Visual Studio 2015 Update 3</span></span>
1. [<span data-ttu-id="fa047-114">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="fa047-114">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/)
1. <span data-ttu-id="fa047-115">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="fa047-115">NuGet CLI.</span></span> <span data-ttu-id="fa047-116">[nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの nuget.exe をダウンロードして、任意の場所に保存します。</span><span class="sxs-lookup"><span data-stu-id="fa047-116">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="fa047-117">次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。</span><span class="sxs-lookup"><span data-stu-id="fa047-117">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="fa047-118">nuget.exe はインストーラーではなく CLI ツール自体です。したがって、ブラウザーからダウンロードしたファイルは実行するのではなく、必ず保存してください。</span><span class="sxs-lookup"><span data-stu-id="fa047-118">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="fa047-119">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="fa047-119">Create the class library project</span></span>

1. <span data-ttu-id="fa047-120">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に移動し、**[Visual C#]、[Windows]** ノードの順に展開して **[クラス ライブラリ (ポータブル)]** を選択し、名前を AppLogger に変更してから [OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="fa047-120">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and click OK.</span></span>

    ![新しいクラス ライブラリ プロジェクトを作成する](media/NetStandard-NewProject.png)

1. <span data-ttu-id="fa047-122">表示された **[ポータブル クラス ライブラリの追加]** ダイアログ ボックスで、`.NET Framework 4.6` と `ASP.NET Core 1.0` オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="fa047-122">In the **Add Portable Class Library** dialog that appears, select the `.NET Framework 4.6` and `ASP.NET Core 1.0` options.</span></span>

1. <span data-ttu-id="fa047-123">ソリューション エクスプローラーで `AppLogger (Portable)` を右クリックして **[プロパティ]** を選択し、**[ライブラリ]** タブを選択してから **[ターゲット]** セクションの **[ターゲットの .NET Platform Standard]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="fa047-123">Right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then click **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="fa047-124">これで確認のプロンプトが表示されます。その後、ドロップダウンから `.NET Standard 1.4` を選択できます。</span><span class="sxs-lookup"><span data-stu-id="fa047-124">This will prompt for confirmation, after which you can select `.NET Standard 1.4` from the drop down:</span></span>

    ![.NET Standard 1.4 へのターゲットの設定](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="fa047-126">**[ビルド]** タブをクリックして **[構成]** を `Release` に変更し、**[XML ドキュメント ファイル]** のボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="fa047-126">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="fa047-127">たとえば、次のようにコンポーネントにコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="fa047-127">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="fa047-128">構成をリリースに設定し、プロジェクトをビルドし、DLL ファイルと XML ファイルが `bin\Release` フォルダー内に生成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="fa047-128">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="fa047-129">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="fa047-129">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="fa047-130">コマンド プロンプトを開き、(`.sln` ファイルの 1 レベル下の) `AppLogger.csproj` フォルダーを含むフォルダーに移動して NuGet `spec` コマンドを実行し、初期 `AppLogger.nuspec` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="fa047-130">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="fa047-131">`AppLogger.nuspec` をエディターで開き、以下の内容と一致するように更新して、YOUR_NAME を適切な値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="fa047-131">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="fa047-132">具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則を参照)。</span><span class="sxs-lookup"><span data-stu-id="fa047-132">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="fa047-133">また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="fa047-133">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="fa047-134">参照アセンブリを `.nuspec` ファイル、つまり、ライブラリの DLL および IntelliSense XML ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="fa047-134">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="fa047-135">ソリューションを右クリックし、**[ソリューションのビルド]** を選択してパッケージのすべてのファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="fa047-135">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="fa047-136">依存関係の宣言</span><span class="sxs-lookup"><span data-stu-id="fa047-136">Declaring dependencies</span></span>

<span data-ttu-id="fa047-137">他の NuGet パッケージに依存している場合は、マニフェストの `<dependencies>` 要素内で `<group>` 要素を使用して列挙します。</span><span class="sxs-lookup"><span data-stu-id="fa047-137">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="fa047-138">たとえば、NewtonSoft.Json 8.0.3 以降に対する依存関係を宣言するには、以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="fa047-138">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="fa047-139">*version* 属性の構文は、バージョン 8.0.3 以降が許容されることを示します。</span><span class="sxs-lookup"><span data-stu-id="fa047-139">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="fa047-140">別のバージョンの範囲を指定する場合は、「[パッケージのバージョン管理](../reference/package-versioning.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="fa047-140">To specify different version ranges, refer to [Package versioning](../reference/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="fa047-141">Readme の追加</span><span class="sxs-lookup"><span data-stu-id="fa047-141">Adding a readme</span></span>

<span data-ttu-id="fa047-142">`readme.txt` ファイルを作成し、プロジェクト ルート ディレクトリに配置して、`.nuspec` ファイルで参照します。</span><span class="sxs-lookup"><span data-stu-id="fa047-142">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="fa047-143">パッケージがプロジェクトにインストールされると、Visual Studio に `readme.txt` が表示されます。</span><span class="sxs-lookup"><span data-stu-id="fa047-143">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="fa047-144">.NET Core プロジェクトにインストールされている場合、または依存関係としてインストールされているパッケージの場合、このファイルは表示されません。</span><span class="sxs-lookup"><span data-stu-id="fa047-144">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="fa047-145">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="fa047-145">Package the component</span></span>

<span data-ttu-id="fa047-146">パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="fa047-146">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="fa047-147">これで `AppLogger.YOUR_NAME.1.0.0.nupkg` が生成されます。</span><span class="sxs-lookup"><span data-stu-id="fa047-147">This will generate `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="fa047-148">[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="fa047-148">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![AppLogger パッケージが表示された NuGet パッケージ エクスプローラー](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="fa047-150">`.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="fa047-150">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="fa047-151">したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。</span><span class="sxs-lookup"><span data-stu-id="fa047-151">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="fa047-152">パッケージを他の開発者が使用できるようにする場合は、「[パッケージを公開する](../create-packages/publish-a-package.md)」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="fa047-152">To make your package available to other developers, follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="fa047-153">`pack` には Mac OS X の場合は Mono 4.4.2 が必要であり、Linux 1 システムでは動作しないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="fa047-153">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="fa047-154">Mac の場合、`.nuspec` ファイルの Windows パス名を Unix 形式のパスに変換する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="fa047-154">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="net-standard-mapping-table"></a><span data-ttu-id="fa047-155">.NET Standard マッピング テーブル</span><span class="sxs-lookup"><span data-stu-id="fa047-155">.NET Standard mapping table</span></span>

| <span data-ttu-id="fa047-156">プラットフォーム名</span><span class="sxs-lookup"><span data-stu-id="fa047-156">Platform Name</span></span> | <span data-ttu-id="fa047-157">Alias</span><span class="sxs-lookup"><span data-stu-id="fa047-157">Alias</span></span> |
| --- | --- |
| <span data-ttu-id="fa047-158">.NET Standard</span><span class="sxs-lookup"><span data-stu-id="fa047-158">.NET Standard</span></span> | <span data-ttu-id="fa047-159">netstandard</span><span class="sxs-lookup"><span data-stu-id="fa047-159">netstandard</span></span> | <span data-ttu-id="fa047-160">1</span><span class="sxs-lookup"><span data-stu-id="fa047-160">1.0</span></span> | <span data-ttu-id="fa047-161">1.1</span><span class="sxs-lookup"><span data-stu-id="fa047-161">1.1</span></span> | <span data-ttu-id="fa047-162">1.2</span><span class="sxs-lookup"><span data-stu-id="fa047-162">1.2</span></span> | <span data-ttu-id="fa047-163">1.3</span><span class="sxs-lookup"><span data-stu-id="fa047-163">1.3</span></span> | <span data-ttu-id="fa047-164">1.4</span><span class="sxs-lookup"><span data-stu-id="fa047-164">1.4</span></span> | <span data-ttu-id="fa047-165">1.5</span><span class="sxs-lookup"><span data-stu-id="fa047-165">1.5</span></span> | <span data-ttu-id="fa047-166">1.6</span><span class="sxs-lookup"><span data-stu-id="fa047-166">1.6</span></span> |
| <span data-ttu-id="fa047-167">.NET Core</span><span class="sxs-lookup"><span data-stu-id="fa047-167">.NET Core</span></span> | <span data-ttu-id="fa047-168">netcoreapp</span><span class="sxs-lookup"><span data-stu-id="fa047-168">netcoreapp</span></span> | <span data-ttu-id="fa047-169">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-169">&#x2192;</span></span> | <span data-ttu-id="fa047-170">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-170">&#x2192;</span></span> | <span data-ttu-id="fa047-171">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-171">&#x2192;</span></span> | <span data-ttu-id="fa047-172">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-172">&#x2192;</span></span> | <span data-ttu-id="fa047-173">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-173">&#x2192;</span></span> | <span data-ttu-id="fa047-174">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-174">&#x2192;</span></span> | <span data-ttu-id="fa047-175">1</span><span class="sxs-lookup"><span data-stu-id="fa047-175">1.0</span></span> |
| <span data-ttu-id="fa047-176">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="fa047-176">.NET Framework</span></span> | <span data-ttu-id="fa047-177">net</span><span class="sxs-lookup"><span data-stu-id="fa047-177">net</span></span> | <span data-ttu-id="fa047-178">4.5</span><span class="sxs-lookup"><span data-stu-id="fa047-178">4.5</span></span> | <span data-ttu-id="fa047-179">4.5.1</span><span class="sxs-lookup"><span data-stu-id="fa047-179">4.5.1</span></span> | <span data-ttu-id="fa047-180">4.6</span><span class="sxs-lookup"><span data-stu-id="fa047-180">4.6</span></span> | <span data-ttu-id="fa047-181">4.6.1</span><span class="sxs-lookup"><span data-stu-id="fa047-181">4.6.1</span></span> | <span data-ttu-id="fa047-182">4.6.2</span><span class="sxs-lookup"><span data-stu-id="fa047-182">4.6.2</span></span> | <span data-ttu-id="fa047-183">4.6.3</span><span class="sxs-lookup"><span data-stu-id="fa047-183">4.6.3</span></span> |
| <span data-ttu-id="fa047-184">Mono/Xamarin プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="fa047-184">Mono/Xamarin Platforms</span></span> | <span data-ttu-id="fa047-185">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-185">&#x2192;</span></span> | <span data-ttu-id="fa047-186">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-186">&#x2192;</span></span> | <span data-ttu-id="fa047-187">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-187">&#x2192;</span></span> | <span data-ttu-id="fa047-188">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-188">&#x2192;</span></span> | <span data-ttu-id="fa047-189">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-189">&#x2192;</span></span> | <span data-ttu-id="fa047-190">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-190">&#x2192;</span></span> |
| <span data-ttu-id="fa047-191">ユニバーサル Windows プラットフォーム</span><span class="sxs-lookup"><span data-stu-id="fa047-191">Universal Windows Platform</span></span> | <span data-ttu-id="fa047-192">uap</span><span class="sxs-lookup"><span data-stu-id="fa047-192">uap</span></span> | <span data-ttu-id="fa047-193">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-193">&#x2192;</span></span> | <span data-ttu-id="fa047-194">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-194">&#x2192;</span></span> | <span data-ttu-id="fa047-195">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-195">&#x2192;</span></span> | <span data-ttu-id="fa047-196">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-196">&#x2192;</span></span> |<span data-ttu-id="fa047-197">10.0</span><span class="sxs-lookup"><span data-stu-id="fa047-197">10.0</span></span> |
| <span data-ttu-id="fa047-198">Windows</span><span class="sxs-lookup"><span data-stu-id="fa047-198">Windows</span></span> | <span data-ttu-id="fa047-199">win</span><span class="sxs-lookup"><span data-stu-id="fa047-199">win</span></span>| <span data-ttu-id="fa047-200">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-200">&#x2192;</span></span> | <span data-ttu-id="fa047-201">8.0</span><span class="sxs-lookup"><span data-stu-id="fa047-201">8.0</span></span> | <span data-ttu-id="fa047-202">8.1</span><span class="sxs-lookup"><span data-stu-id="fa047-202">8.1</span></span> |
| <span data-ttu-id="fa047-203">Windows Phone</span><span class="sxs-lookup"><span data-stu-id="fa047-203">Windows Phone</span></span> | <span data-ttu-id="fa047-204">wpa</span><span class="sxs-lookup"><span data-stu-id="fa047-204">wpa</span></span>| <span data-ttu-id="fa047-205">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-205">&#x2192;</span></span>| <span data-ttu-id="fa047-206">&#x2192;</span><span class="sxs-lookup"><span data-stu-id="fa047-206">&#x2192;</span></span> | <span data-ttu-id="fa047-207">8.1</span><span class="sxs-lookup"><span data-stu-id="fa047-207">8.1</span></span> |
| <span data-ttu-id="fa047-208">Windows Phone Silverlight</span><span class="sxs-lookup"><span data-stu-id="fa047-208">Windows Phone Silverlight</span></span> | <span data-ttu-id="fa047-209">wp</span><span class="sxs-lookup"><span data-stu-id="fa047-209">wp</span></span> | <span data-ttu-id="fa047-210">8.0</span><span class="sxs-lookup"><span data-stu-id="fa047-210">8.0</span></span> |

## <a name="related-topics"></a><span data-ttu-id="fa047-211">関連トピック</span><span class="sxs-lookup"><span data-stu-id="fa047-211">Related topics</span></span>

- [<span data-ttu-id="fa047-212">.nuspec リファレンス</span><span class="sxs-lookup"><span data-stu-id="fa047-212">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="fa047-213">複数の .NET Framework バージョンのサポート</span><span class="sxs-lookup"><span data-stu-id="fa047-213">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="fa047-214">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="fa047-214">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="fa047-215">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="fa047-215">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="fa047-216">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="fa047-216">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="fa047-217">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="fa047-217">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="fa047-218">.NET Standard ライブラリのドキュメント</span><span class="sxs-lookup"><span data-stu-id="fa047-218">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="fa047-219">.NET Framework から .NET Core への移植</span><span class="sxs-lookup"><span data-stu-id="fa047-219">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
