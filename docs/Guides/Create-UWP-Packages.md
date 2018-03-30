---
title: ユニバーサル Windows プラットフォーム用の NuGet パッケージの作成 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/21/2017
ms.topic: tutorial
ms.prod: nuget
ms.technology: ''
description: ユニバーサル Windows プラットフォーム用の Windows ランタイム コンポーネントを使用して NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。
keywords: パッケージを作成する, UWP のパッケージ, Windows ランタイム コンポーネント
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 6923cdc87b0a550abb51316e384c79137eeaf63a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="create-uwp-packages"></a><span data-ttu-id="ccf3d-104">UWP パッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="ccf3d-104">Create UWP packages</span></span>

<span data-ttu-id="ccf3d-105">[ユニバーサル Windows プラットフォーム (UWP)](https://developer.microsoft.com/windows) は、Windows 10 を実行するすべてのデバイスに共通のアプリ プラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-105">The [Universal Windows Platform (UWP)](https://developer.microsoft.com/windows) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="ccf3d-106">このモデル内では、UWP アプリはすべてのデバイスに共通の WinRT API と、アプリが実行されるデバイス ファミリに固有の API (Win32 と .NET を含む) の両方を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-106">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="ccf3d-107">このチュートリアルでは、マネージ プロジェクトとネイティブ プロジェクトの両方で使用できるネイティブ UWP コンポーネント (XAML コントロールを含む) で NuGet パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-107">In this walkthrough you create a NuGet package with a native UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccf3d-108">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="ccf3d-108">Prerequisites</span></span>

1. <span data-ttu-id="ccf3d-109">Visual Studio 2017 または Visual Studio 2015。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-109">Visual Studio 2017 or Visual Studio 2015.</span></span> <span data-ttu-id="ccf3d-110">[visualstudio.com](https://www.visualstudio.com/) から無料の 2017 Community Edition をインストールします。Professional Edition と Enterprise Edition を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-110">Install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="ccf3d-111">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-111">NuGet CLI.</span></span> <span data-ttu-id="ccf3d-112">[nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの `nuget.exe` をダウンロードして、任意の場所に保存します (`.exe`を直接ダウンロードします)。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-112">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="ccf3d-113">次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-113">Then add that location to your PATH environment variable if it isn't already.</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="ccf3d-114">UWP Windows ランタイム コンポーネントを作成する</span><span class="sxs-lookup"><span data-stu-id="ccf3d-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="ccf3d-115">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、**[Visual C++]、[Windows]、[ユニバーサル]** ノードの順に展開して **[Windows ランタイム コンポーネント (ユニバーサル Windows)]** テンプレートを選択し、名前を ImageEnhancer に変更して [OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C++ > Windows > Universal** node, select the **Windows Runtime Component (Universal Windows)** template, change the name to ImageEnhancer, and click OK.</span></span> <span data-ttu-id="ccf3d-116">プロンプトが表示されたら、ターゲット バージョンと最小バージョンの既定値を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![新しい UWP Windows ランタイム コンポーネント プロジェクトの作成](media/UWP-NewProject.png)

1. <span data-ttu-id="ccf3d-118">ソリューション エクスプローラーでプロジェクトを右クリックし、**[追加]、[新しい項目]** の順に選択して **[Visual C++]、[XAML]** ノードの順にクリックし、**[テンプレート コントロール]** を選択して名前を AwesomeImageControl.cpp に変更してから **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-118">Right click the project in Solution Explorer, select **Add > New Item**, click the **Visual C++ > XAML** node, select **Templated Control**, change the name to AwesomeImageControl.cpp, and click **Add**:</span></span>

    ![プロジェクトへの新しい XAML テンプレート コントロール項目の追加](media/UWP-NewXAMLControl.png)

1. <span data-ttu-id="ccf3d-120">ソリューション エクスプローラーでプロジェクトを右クリックして、**[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="ccf3d-121">[プロパティ] ページで、**[構成プロパティ]、[C/C++]** の順に展開して、**[出力ファイル]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-121">In the Properties page, expand **Configuration Properties > C/C++** and click **Output Files**.</span></span> <span data-ttu-id="ccf3d-122">次のように、右側のペインで、**[XML ドキュメント ファイルの生成]** の値を [はい] に変更します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-122">In the pane on the right, change the value for **Generate XML Documentation Files** to Yes:</span></span>

    ![[XML ドキュメント ファイルの生成] を [はい] に設定する](media/UWP-GenerateXMLDocFiles.png)

1. <span data-ttu-id="ccf3d-124">ここで*ソリューション*を右クリックし、**[バッチ ビルド]** を選択して、以下に示すようにダイアログの 3 つのデバッグ ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-124">Right click the *solution* now, select **Batch Build**, check the three Debug boxes in the dialog as shown below.</span></span> <span data-ttu-id="ccf3d-125">これで、ビルドの実行時に、Windows でサポートされるターゲット システムごとに完全な成果物セットが生成されるようになります。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-125">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![[バッチ ビルド]](media/UWP-BatchBuild.png)

1. <span data-ttu-id="ccf3d-127">[バッチ ビルド] ダイアログで、**[ビルド]** をクリックしてプロジェクトを検証し、NuGet パッケージで必要になる出力ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-127">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="ccf3d-128">このチュートリアルでは、パッケージのデバッグ成果物を使用します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-128">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="ccf3d-129">非デバッグ パッケージの場合は、代わりに [バッチ ビルド] ダイアログでリリース オプションをオンにして、以下の手順で結果として得られる Release フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-129">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="ccf3d-130">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="ccf3d-130">Create and update the .nuspec file</span></span>

<span data-ttu-id="ccf3d-131">初期 `.nuspec` ファイルを作成するには、次の 3 つの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-131">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="ccf3d-132">次のセクションでは、他の必要な更新について説明します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-132">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="ccf3d-133">コマンド プロンプトを開き、`ImageEnhancer.vcxproj` (これは、ソリューション ファイルの下のサブフォルダーになります) を含むフォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-133">Open a command prompt and navigate to the folder containing `ImageEnhancer.vcxproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="ccf3d-134">NuGet `spec` コマンドを実行して、`ImageEnhancer.nuspec` (ファイルの名前は `.vcxproj` ファイルの名前から取得されます) を生成します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-134">Run the NuGet `spec` command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.vcxproj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="ccf3d-135">`ImageEnhancer.nuspec` をエディターで開き、以下の内容と一致するように更新して、YOUR_NAME を適切な値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-135">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="ccf3d-136">具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則に関する記述を参照)。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="ccf3d-137">また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>ImageEnhancer.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>ImageEnhancer</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome Image Enhancer</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="ccf3d-138">公開用にビルドされたパッケージの場合は、`<tags>` 要素に特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="ccf3d-139">パッケージへの Windows メタデータの追加</span><span class="sxs-lookup"><span data-stu-id="ccf3d-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="ccf3d-140">Windows ランタイム コンポーネントには、一般公開されるすべての型を記述するメタデータが必要になります。このメタデータにより、他のアプリとライブラリでコンポーネントを使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="ccf3d-141">このメタデータは .winmd ファイルに含まれています。このファイルは、プロジェクトのコンパイル時に作成され、NuGet パッケージに含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="ccf3d-142">IntelliSense データを含む XML ファイルも同時にビルドされ、同様に含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="ccf3d-143">次の `<files>` コードを `.nuspec` ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="ccf3d-144">XAML コンテンツの追加</span><span class="sxs-lookup"><span data-stu-id="ccf3d-144">Adding XAML content</span></span>

<span data-ttu-id="ccf3d-145">コンポーネントに XAML コントロールを含めるには、コントロールの既定のテンプレートを持つ XAML ファイルを追加する必要があります (プロジェクト テンプレートによって生成される)。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="ccf3d-146">この場合、`<files>` セクションは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-146">This also goes in the `<files>` section:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- XAML controls -->
        <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    </files>
</package>
```

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="ccf3d-147">ネイティブ実装ライブラリの追加</span><span class="sxs-lookup"><span data-stu-id="ccf3d-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="ccf3d-148">コンポーネント内では、ImageEnhancer 型のコア ロジックがネイティブ コードに存在します。これは、ターゲット ランタイム (ARM、x86、および x64) ごとに生成されるさまざまな `ImageEnhancer.dll` アセンブリに含まれます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.dll` assemblies that are generated for each target runtime (ARM, x86, and x64).</span></span> <span data-ttu-id="ccf3d-149">これらをパッケージに含める場合は、次のように、関連付けられている .pri リソース ファイルと共に `<files>` セクションで参照します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- DLLs and resources -->
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
        <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>

        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
        <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>

        <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
        <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    </files>
</package>
```

### <a name="adding-targets"></a><span data-ttu-id="ccf3d-150">.targets の追加</span><span class="sxs-lookup"><span data-stu-id="ccf3d-150">Adding .targets</span></span>

<span data-ttu-id="ccf3d-151">次は、NuGet パッケージを使用する可能性のある C++ および JavaScript プロジェクトで、必要なアセンブリと winmd ファイルを識別するための .targets ファイルが必要になります </span><span class="sxs-lookup"><span data-stu-id="ccf3d-151">Next, C++ and JavaScript projects that might consume your NuGet package need a .targets file to identify the necessary assembly and winmd files.</span></span> <span data-ttu-id="ccf3d-152">(C# および Visual Basic プロジェクトでは、これは自動的に行われます)。下のテキストを `ImageEnhancer.targets` にコピーして、このファイルを作成し、`.nuspec` ファイルと同じフォルダーに保存します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-152">(C# and Visual Basic projects do this automatically.) Create this file by copying the text below into `ImageEnhancer.targets` and save it in the same folder as the `.nuspec` file.</span></span> <span data-ttu-id="ccf3d-153">_注_: この `.targets` ファイルはパッケージ ID (`.nupspec` ファイルの `<Id>` 要素など) と同じ名前にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-153">_Note_: This `.targets` file needs to be the same name as the package ID (e.g. the `<Id>` element in the `.nupspec` file):</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <PropertyGroup>
        <ImageEnhancer-Platform Condition="'$(Platform)' == 'Win32'">x86</ImageEnhancer-Platform>
        <ImageEnhancer-Platform Condition="'$(Platform)' != 'Win32'">$(Platform)</ImageEnhancer-Platform>
    </PropertyGroup>
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Reference Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\ImageEnhancer.winmd">
            <Implementation>ImageEnhancer.dll</Implementation>
        </Reference>
    <ReferenceCopyLocalPaths Include="$(MSBuildThisFileDirectory)..\..\runtimes\win10-$(ImageEnhancer-Platform)\native\ImageEnhancer.dll" />
    </ItemGroup>
</Project>
```

<span data-ttu-id="ccf3d-154">次に、`.nuspec` ファイル内の `ImageEnhancer.targets` を参照します。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-154">Then refer to `ImageEnhancer.targets` in your `.nuspec` file:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- .targets -->
        <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="ccf3d-155">最終的な .nuspec</span><span class="sxs-lookup"><span data-stu-id="ccf3d-155">Final .nuspec</span></span>

<span data-ttu-id="ccf3d-156">最終的な `.nuspec` ファイルは次のようになります。ここでも、YOUR_NAME は適切な値に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-156">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>ImageEnhancer.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>ImageEnhancer</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome Image Enhancer</description>
    <releaseNotes>First Release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.winmd" target="lib\uap10.0"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- DLLs and resources -->
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-arm\native"/>
    <file src="..\ARM\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-arm\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x64\native"/>
    <file src="..\x64\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x64\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.dll" target="runtimes\win10-x86\native"/>
    <file src="..\Debug\ImageEnhancer\ImageEnhancer.pri" target="runtimes\win10-x86\native"/>

    <!-- .targets -->
    <file src="ImageEnhancer.targets" target="build\native"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="ccf3d-157">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="ccf3d-157">Package the component</span></span>

<span data-ttu-id="ccf3d-158">パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-158">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="ccf3d-159">これにより、`ImageEnhancer.YOUR_NAME.1.0.0.nupkg`が生成されます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-159">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="ccf3d-160">[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-160">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![ImageEnhancer パッケージが表示された NuGet パッケージ エクスプローラー](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="ccf3d-162">`.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-162">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="ccf3d-163">したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-163">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="ccf3d-164">パッケージを他の開発者が使用できるようにする場合は、「[パッケージの公開](../create-packages/publish-a-package.md)」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="ccf3d-164">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="ccf3d-165">関連トピック</span><span class="sxs-lookup"><span data-stu-id="ccf3d-165">Related topics</span></span>

- [<span data-ttu-id="ccf3d-166">.nuspec 参照</span><span class="sxs-lookup"><span data-stu-id="ccf3d-166">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="ccf3d-167">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="ccf3d-167">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="ccf3d-168">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="ccf3d-168">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="ccf3d-169">複数の .NET Framework バージョンのサポート</span><span class="sxs-lookup"><span data-stu-id="ccf3d-169">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="ccf3d-170">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="ccf3d-170">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="ccf3d-171">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="ccf3d-171">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
