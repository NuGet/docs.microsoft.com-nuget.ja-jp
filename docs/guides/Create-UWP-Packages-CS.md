---
title: ユニバーサル Windows プラットフォーム用の NuGet パッケージの作成
description: C# でユニバーサル Windows プラットフォーム用の Windows ランタイム コンポーネントを使用して NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "78231753"
---
# <a name="create-uwp-packages-c"></a><span data-ttu-id="7bf13-103">UWP パッケージの作成 (C#)</span><span class="sxs-lookup"><span data-stu-id="7bf13-103">Create UWP packages (C#)</span></span>

<span data-ttu-id="7bf13-104">[ユニバーサル Windows プラットフォーム (UWP)](/windows/uwp) は、Windows 10 を実行するすべてのデバイスに共通のアプリ プラットフォームを提供します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-104">The [Universal Windows Platform (UWP)](/windows/uwp) provides a common app platform for every device that runs Windows 10.</span></span> <span data-ttu-id="7bf13-105">このモデル内では、UWP アプリはすべてのデバイスに共通の WinRT API と、アプリが実行されるデバイス ファミリに固有の API (Win32 と .NET を含む) の両方を呼び出すことができます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-105">Within this model, UWP apps can call both the WinRT APIs that are common to all devices, and also APIs (including Win32 and .NET) that are specific to the device family on which the app is running.</span></span>

<span data-ttu-id="7bf13-106">このチュートリアルでは、マネージド プロジェクトとネイティブ プロジェクトの両方で使用できる C# UWP コンポーネント (XAML コントロールを含む) で NuGet パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-106">In this walkthrough you create a NuGet package with a C# UWP component (including a XAML control) that can be used in both Managed and Native projects.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7bf13-107">前提条件</span><span class="sxs-lookup"><span data-stu-id="7bf13-107">Prerequisites</span></span>

1. <span data-ttu-id="7bf13-108">Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="7bf13-108">Visual Studio 2019.</span></span> <span data-ttu-id="7bf13-109">[visualstudio.com](https://www.visualstudio.com/) から無料の 2019 Community Edition をインストールします。Professional Edition と Enterprise Edition を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-109">Install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well.</span></span>

1. <span data-ttu-id="7bf13-110">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="7bf13-110">NuGet CLI.</span></span> <span data-ttu-id="7bf13-111">`nuget.exe`nuget.org/downloads[ から最新バージョンの ](https://nuget.org/downloads) をダウンロードして、任意の場所に保存します (`.exe`を直接ダウンロードします)。</span><span class="sxs-lookup"><span data-stu-id="7bf13-111">Download the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice (the download is the `.exe` directly).</span></span> <span data-ttu-id="7bf13-112">次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。</span><span class="sxs-lookup"><span data-stu-id="7bf13-112">Then add that location to your PATH environment variable if it isn't already.</span></span> <span data-ttu-id="7bf13-113">[詳細についてはこちらをご覧ください](/nuget/reference/nuget-exe-cli-reference#windows)。</span><span class="sxs-lookup"><span data-stu-id="7bf13-113">[More details](/nuget/reference/nuget-exe-cli-reference#windows).</span></span>

## <a name="create-a-uwp-windows-runtime-component"></a><span data-ttu-id="7bf13-114">UWP Windows ランタイム コンポーネントを作成する</span><span class="sxs-lookup"><span data-stu-id="7bf13-114">Create a UWP Windows Runtime component</span></span>

1. <span data-ttu-id="7bf13-115">Visual Studio で、 **[ファイル]、[新規]、[プロジェクト]** の順に選択し、"uwp c#" を検索し、 **[Windows ランタイム コンポーネント (ユニバーサル Windows)]** テンプレートを選択し、[次へ] をクリックして、名前を ImageEnhancer に変更して [作成] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bf13-115">In Visual Studio, choose **File > New > Project**, search for "uwp c#", select the **Windows Runtime Component (Universal Windows)** template, click next, change the name to ImageEnhancer, and click Create.</span></span> <span data-ttu-id="7bf13-116">プロンプトが表示されたら、ターゲット バージョンと最小バージョンの既定値を受け入れます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-116">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

    ![新しい UWP Windows ランタイム コンポーネント プロジェクトの作成](media/UWP-NewProject-CS.png)

1. <span data-ttu-id="7bf13-118">ソリューション エクスプローラーでプロジェクトを右クリックし、 **[追加]、[新しい項目]** の順に選択し、 **[テンプレート コントロール]** を選択して、名前を AwesomeImageControl.cs に変更してから **[追加]** をクリックします。</span><span class="sxs-lookup"><span data-stu-id="7bf13-118">Right click the project in Solution Explorer, select **Add > New Item**, select **Templated Control**, change the name to AwesomeImageControl.cs, and click **Add**:</span></span>

    ![プロジェクトへの新しい XAML テンプレート コントロール項目の追加](media/UWP-NewXAMLControl-CS.png)

1. <span data-ttu-id="7bf13-120">ソリューション エクスプローラーでプロジェクトを右クリックして、 **[プロパティ]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-120">Right-click the project in Solution Explorer and select **Properties.**</span></span> <span data-ttu-id="7bf13-121">[プロパティ] ページで、 **[ビルド]** タブを選択し、 **[XML ドキュメント ファイル]** を有効にします。</span><span class="sxs-lookup"><span data-stu-id="7bf13-121">In the Properties page, choose **Build** tab and enable **XML Documentation File**:</span></span>

    ![[XML ドキュメント ファイルの生成] を [はい] に設定する](media/UWP-GenerateXMLDocFiles-CS.png)

1. <span data-ttu-id="7bf13-123">ここで*ソリューション*を右クリックし、 **[バッチ ビルド]** を選択して、以下に示すようにダイアログの 5 つのビルド ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="7bf13-123">Right click the *solution* now, select **Batch Build**, check the five build boxes in the dialog as shown below.</span></span> <span data-ttu-id="7bf13-124">これで、ビルドの実行時に、Windows でサポートされるターゲット システムごとに完全な成果物セットが生成されるようになります。</span><span class="sxs-lookup"><span data-stu-id="7bf13-124">This makes sure that when you do a build, you generate a full set of artifacts for each of the target systems that Windows supports.</span></span>

    ![[バッチ ビルド]](media/UWP-BatchBuild-CS.png)

1. <span data-ttu-id="7bf13-126">[バッチ ビルド] ダイアログで、 **[ビルド]** をクリックしてプロジェクトを検証し、NuGet パッケージで必要になる出力ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-126">In the Batch Build dialog, and click **Build** to verify the project and create the output files that you need for the NuGet package.</span></span>

> [!Note]
> <span data-ttu-id="7bf13-127">このチュートリアルでは、パッケージのデバッグ成果物を使用します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-127">In this walkthrough you use the Debug artifacts for the package.</span></span> <span data-ttu-id="7bf13-128">非デバッグ パッケージの場合は、代わりに [バッチ ビルド] ダイアログでリリース オプションをオンにして、以下の手順で結果として得られる Release フォルダーを参照します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-128">For non-debug package, check the Release options in the Batch Build dialog instead, and refer to the resulting Release folders in the steps that follow.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="7bf13-129">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="7bf13-129">Create and update the .nuspec file</span></span>

<span data-ttu-id="7bf13-130">初期 `.nuspec` ファイルを作成するには、次の 3 つの手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-130">To create the initial `.nuspec` file, do the three steps below.</span></span> <span data-ttu-id="7bf13-131">次のセクションでは、他の必要な更新について説明します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-131">The sections that follow then guide you through other necessary updates.</span></span>

1. <span data-ttu-id="7bf13-132">コマンド プロンプトを開き、`ImageEnhancer.csproj` (これは、ソリューション ファイルの下のサブフォルダーになります) を含むフォルダーに移動します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-132">Open a command prompt and navigate to the folder containing `ImageEnhancer.csproj` (this will be a subfolder below where the solution file is).</span></span>
1. <span data-ttu-id="7bf13-133">[`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) コマンドを実行して、`ImageEnhancer.nuspec` (ファイルの名前は `.csroj` ファイルの名前から取得されます) を生成します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-133">Run the [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) command to generate `ImageEnhancer.nuspec` (the name of the file is taken from the name of the `.csroj` file):</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="7bf13-134">`ImageEnhancer.nuspec` をエディターで開き、以下の内容と一致するように更新して、YOUR_NAME を適切な値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-134">Open `ImageEnhancer.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="7bf13-135">$propertyName$ 値が残らないようにします。</span><span class="sxs-lookup"><span data-stu-id="7bf13-135">Do not leave any of the $propertyName$ values.</span></span> <span data-ttu-id="7bf13-136">具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則に関する記述を参照)。</span><span class="sxs-lookup"><span data-stu-id="7bf13-136">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="7bf13-137">また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-137">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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
        <copyright>Copyright 2020</copyright>
        <tags>image enhancer imageenhancer</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="7bf13-138">公開用にビルドされたパッケージの場合は、`<tags>` 要素に特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-138">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

### <a name="adding-windows-metadata-to-the-package"></a><span data-ttu-id="7bf13-139">パッケージへの Windows メタデータの追加</span><span class="sxs-lookup"><span data-stu-id="7bf13-139">Adding Windows metadata to the package</span></span>

<span data-ttu-id="7bf13-140">Windows ランタイム コンポーネントには、一般公開されるすべての型を記述するメタデータが必要になります。このメタデータにより、他のアプリとライブラリでコンポーネントを使用できるようになります。</span><span class="sxs-lookup"><span data-stu-id="7bf13-140">A Windows Runtime Component requires metadata that describes all of its publicly available types, which makes it possible for other apps and libraries to consume the component.</span></span> <span data-ttu-id="7bf13-141">このメタデータは .winmd ファイルに含まれています。このファイルは、プロジェクトのコンパイル時に作成され、NuGet パッケージに含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7bf13-141">This metadata is contained in a .winmd file, which is created when you compile the project and must be included in your NuGet package.</span></span> <span data-ttu-id="7bf13-142">IntelliSense データを含む XML ファイルも同時にビルドされ、同様に含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="7bf13-142">An XML file with IntelliSense data is also built at the same time, and should be included as well.</span></span>

<span data-ttu-id="7bf13-143">次の `<files>` コードを `.nuspec` ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-143">Add the following `<files>` node to the `.nuspec` file:</span></span>

```xml
<package>
    <metadata>
        ...
    </metadata>

    <files>
        <!-- WinMd and IntelliSense files -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>
    </files>
</package>
```

### <a name="adding-xaml-content"></a><span data-ttu-id="7bf13-144">XAML コンテンツの追加</span><span class="sxs-lookup"><span data-stu-id="7bf13-144">Adding XAML content</span></span>

<span data-ttu-id="7bf13-145">コンポーネントに XAML コントロールを含めるには、コントロールの既定のテンプレートを持つ XAML ファイルを追加する必要があります (プロジェクト テンプレートによって生成される)。</span><span class="sxs-lookup"><span data-stu-id="7bf13-145">To include a XAML control with your component, you need to add the XAML file that has the default template for the control (as generated by the project template).</span></span> <span data-ttu-id="7bf13-146">この場合、`<files>` セクションは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7bf13-146">This also goes in the `<files>` section:</span></span>

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

### <a name="adding-the-native-implementation-libraries"></a><span data-ttu-id="7bf13-147">ネイティブ実装ライブラリの追加</span><span class="sxs-lookup"><span data-stu-id="7bf13-147">Adding the native implementation libraries</span></span>

<span data-ttu-id="7bf13-148">コンポーネント内では、ImageEnhancer 型のコア ロジックがネイティブ コードに存在します。これは、ターゲット ランタイム (ARM、ARM64、x86、および x64) ごとに生成されるさまざまな `ImageEnhancer.winmd` アセンブリに含まれます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-148">Within your component, the core logic of the ImageEnhancer type is in native code, which is contained in the various `ImageEnhancer.winmd` assemblies that are generated for each target runtime (ARM, ARM64, x86, and x64).</span></span> <span data-ttu-id="7bf13-149">これらをパッケージに含める場合は、次のように、関連付けられている .pri リソース ファイルと共に `<files>` セクションで参照します。</span><span class="sxs-lookup"><span data-stu-id="7bf13-149">To include these in the package, reference them in the `<files>` section along with their associated .pri resource files:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
        ...
    </metadata>
    <files>
        ...

        <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

### <a name="final-nuspec"></a><span data-ttu-id="7bf13-150">最終的な .nuspec</span><span class="sxs-lookup"><span data-stu-id="7bf13-150">Final .nuspec</span></span>

<span data-ttu-id="7bf13-151">最終的な `.nuspec` ファイルは次のようになります。ここでも、YOUR_NAME は適切な値に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="7bf13-151">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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
    <copyright>Copyright 2020</copyright>
    <tags>image enhancer imageenhancer</tags>
    </metadata>
    <files>
    <!-- WinMd and IntelliSense -->
      <file src="bin\Debug\ImageEnhancer.winmd" target="lib\uap10.0"/>
      <file src="bin\Debug\ImageEnhancer.xml" target="lib\uap10.0"/>

    <!-- XAML controls -->
    <file src="Themes\Generic.xaml" target="lib\uap10.0\Themes"/>

    <!-- WINMDs and resources -->
      <file src="bin\ARM\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm"/>
      <file src="bin\ARM\Debug\ImageEnhancer.pri" target="runtimes\win10-arm"/>

      <file src="bin\ARM64\Debug\ImageEnhancer.winmd" target="runtimes\win10-arm64"/>
      <file src="bin\ARM64\Debug\ImageEnhancer.pri" target="runtimes\win10-arm64"/>

      <file src="bin\x64\Debug\ImageEnhancer.winmd" target="runtimes\win10-x64"/>
      <file src="bin\x64\Debug\ImageEnhancer.pri" target="runtimes\win10-x64"/>

      <file src="bin\x86\Debug\ImageEnhancer.winmd" target="runtimes\win10-x86"/>
      <file src="bin\x86\Debug\ImageEnhancer.pri" target="runtimes\win10-x86"/>

    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="7bf13-152">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="7bf13-152">Package the component</span></span>

<span data-ttu-id="7bf13-153">パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) コマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-153">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) command:</span></span>

```cli
nuget pack ImageEnhancer.nuspec
```

<span data-ttu-id="7bf13-154">これにより、`ImageEnhancer.YOUR_NAME.1.0.0.nupkg`が生成されます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-154">This generates `ImageEnhancer.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="7bf13-155">[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7bf13-155">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![ImageEnhancer パッケージが表示された NuGet パッケージ エクスプローラー](media/UWP-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="7bf13-157">`.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="7bf13-157">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="7bf13-158">したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。</span><span class="sxs-lookup"><span data-stu-id="7bf13-158">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="7bf13-159">パッケージを他の開発者が使用できるようにする場合は、「[パッケージの公開](../nuget-org/publish-a-package.md)」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="7bf13-159">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="7bf13-160">関連トピック</span><span class="sxs-lookup"><span data-stu-id="7bf13-160">Related topics</span></span>

- [<span data-ttu-id="7bf13-161">.nuspec 参照</span><span class="sxs-lookup"><span data-stu-id="7bf13-161">.nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="7bf13-162">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="7bf13-162">Symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="7bf13-163">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="7bf13-163">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="7bf13-164">複数の .NET Framework バージョンのサポート</span><span class="sxs-lookup"><span data-stu-id="7bf13-164">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7bf13-165">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="7bf13-165">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="7bf13-166">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="7bf13-166">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)
