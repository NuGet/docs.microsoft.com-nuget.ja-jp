---
title: Visual Studio 2015 での NET Standard および NET Framework NuGet パッケージの作成
description: NuGet 3.x と Visual Studio 2015 を使用して、.NET Standard および .NET Framework の NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 11dce27b93c3d09a2d27dc79f8d4fed86df879ba
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488974"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a><span data-ttu-id="e3eef-103">Visual Studio 2015 での NET Standard および NET Framework パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="e3eef-103">Create .NET Standard and .NET Framework packages with Visual Studio 2015</span></span>

<span data-ttu-id="e3eef-104">**注:**  .NET Standard ライブラリを開発するには、Visual Studio 2017 をお勧めします。</span><span class="sxs-lookup"><span data-stu-id="e3eef-104">**Note:** Visual Studio 2017 is recommended for developing .NET Standard libraries.</span></span> <span data-ttu-id="e3eef-105">Visual Studio 2015 でも動作できますが、.NET Core ツールはプレビュー状態にしかなりません。</span><span class="sxs-lookup"><span data-stu-id="e3eef-105">Visual Studio 2015 can work but the .NET Core tooling was brought only to Preview state.</span></span> <span data-ttu-id="e3eef-106">NuGet 4.x 以降および Visual Studio 2017 を使用している場合は、[Visual Studio 2017 でのパッケージの作成と公開](../quickstart/create-and-publish-a-package-using-visual-studio.md)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="e3eef-106">See [Create and publish a package with Visual Studio 2017](../quickstart/create-and-publish-a-package-using-visual-studio.md) for working with NuGet 4.x+ and Visual Studio 2017.</span></span>

<span data-ttu-id="e3eef-107">[.NET Standard ライブラリ](/dotnet/articles/standard/library)は、すべての .NET ランタイムで使用できるようにすることを目的とした .NET API の正式な仕様です。したがって、.NET エコシステムでより高い統一性が確立されます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-107">The [.NET Standard Library](/dotnet/articles/standard/library) is a formal specification of .NET APIs intended to be available on all .NET runtimes, thus establishing greater uniformity in the .NET ecosystem.</span></span> <span data-ttu-id="e3eef-108">.NET Standard Library は、ワークロードに関係なく、すべての .NET プラットフォーム用に統一された BCL (基本クラス ライブラリ) API のセットを定義して実装します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-108">The .NET Standard Library defines a uniform set of BCL (Base Class Library) APIs for all .NET platforms to implement, independent of workload.</span></span> <span data-ttu-id="e3eef-109">これにより、開発者はすべての .NET ランタイム間で使用可能なコードを生成できます。また、共有コードでプラットフォーム固有の条件付きコンパイル ディレクティブを除去するまでとはいかないまでも減らすことはできます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-109">It enables developers to produce code that is usable across all .NET runtimes, and reduces if not eliminates platform-specific conditional compilation directives in shared code.</span></span>

<span data-ttu-id="e3eef-110">このガイドでは、 .NET Standard Library 1.4 をターゲットとするか、または .NET Framework 4.6 をターゲットとする NuGet パッケージの作成について説明します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-110">This guide walks you through creating a NuGet package targeting .NET Standard Library 1.4 or a package targeting .NET Framework 4.6.</span></span> <span data-ttu-id="e3eef-111">.NET Standard 1.4 ライブラリは、.NET Framework 4.6.1、ユニバーサル Windows プラットフォーム 10、.NET Core、および Mono/Xamarin に適用できます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-111">A .NET Standard 1.4 library works across .NET Framework 4.6.1, Universal Windows Platform 10, .NET Core, and Mono/Xamarin.</span></span> <span data-ttu-id="e3eef-112">詳細については、「[.NET Standard マッピング テーブル](/dotnet/standard/net-standard#net-implementation-support)」 (.NET ドキュメント) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e3eef-112">For details, see the [.NET Standard mapping table](/dotnet/standard/net-standard#net-implementation-support) (.NET documentation).</span></span> <span data-ttu-id="e3eef-113">必要な場合は、他のバージョンの .NET Standard ライブラリを選択できます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-113">You can choose other version of the .NET Standard Library if you want.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e3eef-114">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="e3eef-114">Prerequisites</span></span>

1. <span data-ttu-id="e3eef-115">Visual Studio 2015 更新プログラム 3</span><span class="sxs-lookup"><span data-stu-id="e3eef-115">Visual Studio 2015 Update 3</span></span>
1. <span data-ttu-id="e3eef-116">(.NET Standard のみ) [.NET Core SDK](https://www.microsoft.com/net/download/)</span><span class="sxs-lookup"><span data-stu-id="e3eef-116">(.NET Standard only) [.NET Core SDK](https://www.microsoft.com/net/download/)</span></span>
1. <span data-ttu-id="e3eef-117">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="e3eef-117">NuGet CLI.</span></span> <span data-ttu-id="e3eef-118">[nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの nuget.exe をダウンロードして、任意の場所に保存します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="e3eef-119">次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。</span><span class="sxs-lookup"><span data-stu-id="e3eef-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

    > [!Note]
    > <span data-ttu-id="e3eef-120">nuget.exe はインストーラーではなく CLI ツール自体です。したがって、ブラウザーからダウンロードしたファイルは実行するのではなく、必ず保存してください。</span><span class="sxs-lookup"><span data-stu-id="e3eef-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-class-library-project"></a><span data-ttu-id="e3eef-121">クラス ライブラリ プロジェクトを作成する</span><span class="sxs-lookup"><span data-stu-id="e3eef-121">Create the class library project</span></span>

1. <span data-ttu-id="e3eef-122">Visual Studio で、 **[ファイル] > [新規] > [プロジェクト]** の順に移動し、 **[Visual C#] > [Windows]** ノードの順に展開して **[クラス ライブラリ (ポータブル)]** を選択し、名前を AppLogger に変更してから **[OK]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-122">In Visual Studio, **File > New > Project**, expand the **Visual C# > Windows** node, select **Class Library (Portable)**, change the name to AppLogger, and select **OK**.</span></span>

    ![新しいクラス ライブラリ プロジェクトを作成する](media/NetStandard-NewProject.png)

1. <span data-ttu-id="e3eef-124">表示された **[ポータブル クラス ライブラリの追加]** ダイアログ ボックスで、`.NET Framework 4.6` と `ASP.NET Core 1.0` のオプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-124">In the **Add Portable Class Library** dialog that appears, select the options for `.NET Framework 4.6` and `ASP.NET Core 1.0`.</span></span> <span data-ttu-id="e3eef-125">(.NET Framework をターゲットにしている場合は、どちらか適切なオプションを選択できます。)</span><span class="sxs-lookup"><span data-stu-id="e3eef-125">(If targeting .NET Framework, you can select whichever options are appropriate.)</span></span>

1. <span data-ttu-id="e3eef-126">.NET Standard をターゲットにしている場合、ソリューション エクスプローラーで `AppLogger (Portable)` を右クリックして **[プロパティ]** を選択し、 **[ライブラリ]** タブを選択してから **[ターゲット]** セクションの **[ターゲットの .NET Platform Standard]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-126">If targeting .NET Standard, right-click the `AppLogger (Portable)` in Solution Explorer, select **Properties**, select the **Library** tab, then select  **Target .NET Platform Standard** in the **Targeting** section.</span></span> <span data-ttu-id="e3eef-127">この動作によって確認を促すメッセージが表示され、以降はドロップ ダウンから `.NET Standard 1.4` (または、使用可能な別のバージョン) を選択できるようになります。</span><span class="sxs-lookup"><span data-stu-id="e3eef-127">This action prompts for confirmation, after which you can select `.NET Standard 1.4` (or another available version) from the drop down:</span></span>

    ![.NET Standard 1.4 へのターゲットの設定](media/NetStandard-ChangeTarget.png)

1. <span data-ttu-id="e3eef-129">**[ビルド]** タブをクリックして **[構成]** を `Release` に変更し、 **[XML ドキュメント ファイル]** のボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="e3eef-129">Click on the **Build** tab, change the **Configuration** to `Release`, and check the box for **XML documentation file**.</span></span>

1. <span data-ttu-id="e3eef-130">たとえば、次のようにコンポーネントにコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-130">Add your code to the component, for example:</span></span>

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

1. <span data-ttu-id="e3eef-131">構成をリリースに設定し、プロジェクトをビルドし、DLL ファイルと XML ファイルが `bin\Release` フォルダー内に生成されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-131">Set the configuration to Release, build the project, and check that DLL and XML files are produced within the `bin\Release` folder.</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="e3eef-132">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="e3eef-132">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="e3eef-133">コマンド プロンプトを開き、(`.sln` ファイルの 1 レベル下の) `AppLogger.csproj` フォルダーを含むフォルダーに移動して NuGet `spec` コマンドを実行し、初期 `AppLogger.nuspec` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-133">Open a command prompt, navigate to the folder containing `AppLogger.csproj` folder (one level below where the `.sln` file is), and run the NuGet `spec` command to create the initial `AppLogger.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="e3eef-134">`AppLogger.nuspec` をエディターで開き、以下の内容と一致するように更新して、YOUR_NAME を適切な値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-134">Open `AppLogger.nuspec` in an editor and update it to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="e3eef-135">具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則を参照)。</span><span class="sxs-lookup"><span data-stu-id="e3eef-135">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="e3eef-136">また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-136">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

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

1. <span data-ttu-id="e3eef-137">参照アセンブリを `.nuspec` ファイル、つまり、ライブラリの DLL および IntelliSense XML ファイルに追加します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-137">Add reference assemblies to the `.nuspec` file, namely the library's DLL and the IntelliSense XML file:</span></span>

    <span data-ttu-id="e3eef-138">.NET Standard をターゲットにしている場合、エントリは以下のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-138">If targeting .NET Standard, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    <span data-ttu-id="e3eef-139">.NET Framework をターゲットにしている場合、エントリは以下のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-139">If targeting .NET Framework, the entries appear similar to the following:</span></span>

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. <span data-ttu-id="e3eef-140">ソリューションを右クリックし、 **[ソリューションのビルド]** を選択してパッケージのすべてのファイルを生成します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-140">Right-click the solution and select **Build Solution** to generate all the files for the package.</span></span>

### <a name="declaring-dependencies"></a><span data-ttu-id="e3eef-141">依存関係の宣言</span><span class="sxs-lookup"><span data-stu-id="e3eef-141">Declaring dependencies</span></span>

<span data-ttu-id="e3eef-142">他の NuGet パッケージに依存している場合は、マニフェストの `<dependencies>` 要素内で `<group>` 要素を使用して列挙します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-142">If you have any dependencies on other NuGet packages, list those in the manifest's `<dependencies>` element with `<group>` elements.</span></span> <span data-ttu-id="e3eef-143">たとえば、NewtonSoft.Json 8.0.3 以降に対する依存関係を宣言するには、以下を追加します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-143">For example, to declare a dependency on NewtonSoft.Json 8.0.3 or above, add the following:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

<span data-ttu-id="e3eef-144">*version* 属性の構文は、バージョン 8.0.3 以降が許容されることを示します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-144">The syntax of the *version* attribute here indicates that version 8.0.3 or above is acceptable.</span></span> <span data-ttu-id="e3eef-145">別のバージョンの範囲を指定する場合は、「[パッケージのバージョン管理](../concepts/package-versioning.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e3eef-145">To specify different version ranges, refer to [Package versioning](../concepts/package-versioning.md).</span></span>

### <a name="adding-a-readme"></a><span data-ttu-id="e3eef-146">Readme の追加</span><span class="sxs-lookup"><span data-stu-id="e3eef-146">Adding a readme</span></span>

<span data-ttu-id="e3eef-147">`readme.txt` ファイルを作成し、プロジェクト ルート ディレクトリに配置して、`.nuspec` ファイルで参照します。</span><span class="sxs-lookup"><span data-stu-id="e3eef-147">Create your `readme.txt` file, place it in the project root folder, and refer to it in the `.nuspec` file:</span></span>

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

<span data-ttu-id="e3eef-148">パッケージがプロジェクトにインストールされると、Visual Studio に `readme.txt` が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-148">Visual Studio display `readme.txt` when the package is installed into a project.</span></span> <span data-ttu-id="e3eef-149">.NET Core プロジェクトにインストールされている場合、または依存関係としてインストールされているパッケージの場合、このファイルは表示されません。</span><span class="sxs-lookup"><span data-stu-id="e3eef-149">The file is not shown when installed into .NET Core projects, or for packages that are installed as a dependency.</span></span>

## <a name="package-the-component"></a><span data-ttu-id="e3eef-150">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="e3eef-150">Package the component</span></span>

<span data-ttu-id="e3eef-151">パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-151">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack AppLogger.nuspec
```

<span data-ttu-id="e3eef-152">これにより、`AppLogger.YOUR_NAME.1.0.0.nupkg`が生成されます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-152">This generates `AppLogger.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="e3eef-153">[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツ (.NET Standard に対する表示) が表示されます。</span><span class="sxs-lookup"><span data-stu-id="e3eef-153">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents (shown for .NET Standard):</span></span>

![AppLogger パッケージが表示された NuGet パッケージ エクスプローラー](media/NetStandard-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="e3eef-155">`.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="e3eef-155">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="e3eef-156">したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。</span><span class="sxs-lookup"><span data-stu-id="e3eef-156">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="e3eef-157">パッケージを他の開発者が使用できるようにする場合は、「[パッケージを公開する](../nuget-org/publish-a-package.md)」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="e3eef-157">To make your package available to other developers, follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

<span data-ttu-id="e3eef-158">`pack` には Mac OS X の場合は Mono 4.4.2 が必要であり、Linux 1 システムでは動作しないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="e3eef-158">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="e3eef-159">Mac の場合、`.nuspec` ファイルの Windows パス名を Unix 形式のパスに変換する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="e3eef-159">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="related-topics"></a><span data-ttu-id="e3eef-160">関連トピック</span><span class="sxs-lookup"><span data-stu-id="e3eef-160">Related topics</span></span>

- [<span data-ttu-id="e3eef-161">.nuspec リファレンス</span><span class="sxs-lookup"><span data-stu-id="e3eef-161">.nuspec reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="e3eef-162">複数の .NET Framework バージョンのサポート</span><span class="sxs-lookup"><span data-stu-id="e3eef-162">Supporting multiple .NET framework versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="e3eef-163">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="e3eef-163">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="e3eef-164">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="e3eef-164">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="e3eef-165">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="e3eef-165">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="e3eef-166">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="e3eef-166">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="e3eef-167">.NET Standard ライブラリのドキュメント</span><span class="sxs-lookup"><span data-stu-id="e3eef-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="e3eef-168">.NET Framework から .NET Core への移植</span><span class="sxs-lookup"><span data-stu-id="e3eef-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
