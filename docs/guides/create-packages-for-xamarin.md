---
title: Visual Studio 2015 による Xamarin 用 NuGet パッケージの作成 (iOS、Android、および Windows 用)
description: iOS、Android、および Windows でネイティブ API を使用する、Xamarin の NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: tutorial
ms.openlocfilehash: 81f78de02d9b6510f195e04c78436e38f9b7353d
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842416"
---
# <a name="create-packages-for-xamarin-with-visual-studio-2015"></a><span data-ttu-id="f4871-103">Visual Studio 2015 での Xamarin 用パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="f4871-103">Create packages for Xamarin with Visual Studio 2015</span></span>

<span data-ttu-id="f4871-104">Xamarin 用 パッケージには、実行時のオペレーティング システムに応じて、iOS、Android、および Windows でネイティブ API を使用するコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f4871-104">A package for Xamarin contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="f4871-105">これを行うのは簡単ですが、開発者が共通の API のセキュリティ、外部からのアクセスを通じて PCL または .NET Standard ライブラリからパッケージを使用できるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="f4871-105">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="f4871-106">このチュートリアルでは、Visual Studio 2015 を使用して、iOS、Android、および Windows 上のモバイル プロジェクトで使用できるクロスプラットフォームの NuGet パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="f4871-106">In this walkthrough you use Visual Studio 2015 create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="f4871-107">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="f4871-107">Prerequisites</span></span>](#prerequisites)
1. [<span data-ttu-id="f4871-108">プロジェクトの構造体および抽象化コードを作成する</span><span class="sxs-lookup"><span data-stu-id="f4871-108">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="f4871-109">プラットフォーム固有のコードを記述する</span><span class="sxs-lookup"><span data-stu-id="f4871-109">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="f4871-110">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="f4871-110">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="f4871-111">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="f4871-111">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="f4871-112">関連トピック</span><span class="sxs-lookup"><span data-stu-id="f4871-112">Related topics</span></span>](#related-topics)

## <a name="prerequisites"></a><span data-ttu-id="f4871-113">必須コンポーネント</span><span class="sxs-lookup"><span data-stu-id="f4871-113">Prerequisites</span></span>

1. <span data-ttu-id="f4871-114">Visual Studio 2015、ユニバーサル Windows プラットフォーム (UWP) および Xamarin。</span><span class="sxs-lookup"><span data-stu-id="f4871-114">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="f4871-115">[visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。もちろん、Professional Edition と Enterprise Edition も使用できます。</span><span class="sxs-lookup"><span data-stu-id="f4871-115">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="f4871-116">UWP および Xamarin ツールを含めるには、カスタム インストールを選択して、適切なオプションを確認します。</span><span class="sxs-lookup"><span data-stu-id="f4871-116">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="f4871-117">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="f4871-117">NuGet CLI.</span></span> <span data-ttu-id="f4871-118">[nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの nuget.exe をダウンロードして、任意の場所に保存します。</span><span class="sxs-lookup"><span data-stu-id="f4871-118">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="f4871-119">次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。</span><span class="sxs-lookup"><span data-stu-id="f4871-119">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="f4871-120">nuget.exe はインストーラーではなく CLI ツール自体です。したがって、ブラウザーからダウンロードしたファイルは実行するのではなく、必ず保存してください。</span><span class="sxs-lookup"><span data-stu-id="f4871-120">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>

## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="f4871-121">プロジェクトの構造体および抽象化コードを作成する</span><span class="sxs-lookup"><span data-stu-id="f4871-121">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="f4871-122">Visual Studio 用の [Plugin For Xamarin テンプレート拡張機能](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)をダウンロードして実行します。</span><span class="sxs-lookup"><span data-stu-id="f4871-122">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="f4871-123">これらのテンプレートを使用することで、このチュートリアルで必要なプロジェクトの構造体を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="f4871-123">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="f4871-124">Visual Studio で、 **[ファイル]、[新規]、[プロジェクト]** の順に選択し、`Plugin` を検索して **[Plugin for Xamarin]** テンプレートを選択し、名前を LoggingLibrary に変更してから [OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="f4871-124">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Visual Studio の新しい空のアプリ (Xamarin.Forms ポータブル) プロジェクト](media/CrossPlatform-NewProject.png)

<span data-ttu-id="f4871-126">結果として得られるソリューションには、以下のようなさまざまなプラットフォーム固有のプロジェクトと共に 2 つの PCL プロジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f4871-126">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="f4871-127">`Plugin.LoggingLibrary.Abstractions (Portable)` という名前の PCL ではコンポーネントのパブリック インターフェイス (API のセキュリティ、外部からのアクセス) を定義します。この場合、ILoggingLibrary.cs ファイルに含まれている `ILoggingLibrary` インターフェイスとなります。</span><span class="sxs-lookup"><span data-stu-id="f4871-127">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="f4871-128">これは、ライブラリへのインターフェイスを定義する場所です。</span><span class="sxs-lookup"><span data-stu-id="f4871-128">This is where you define the interface to your library.</span></span>
- <span data-ttu-id="f4871-129">その他の PCL `Plugin.LoggingLibrary (Portable)` には、実行時に抽象インターフェイスのプラットフォーム固有の実装を検索する CrossLoggingLibrary.cs のコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="f4871-129">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="f4871-130">通常、このファイルを変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="f4871-130">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="f4871-131">`Plugin.LoggingLibrary.Android` などのプラットフォーム固有の各プロジェクトには、対応する LoggingLibraryImplementation.cs ファイルのインターフェイスのネイティブ実装が含まれます。</span><span class="sxs-lookup"><span data-stu-id="f4871-131">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="f4871-132">これは、ライブラリのコードをビルドする場所です。</span><span class="sxs-lookup"><span data-stu-id="f4871-132">This is where you build out your library's code.</span></span>

<span data-ttu-id="f4871-133">既定では、抽象化プロジェクトの ILoggingLibrary.cs ファイルにインターフェイス定義が含まれますが、メソッドは含まれません。</span><span class="sxs-lookup"><span data-stu-id="f4871-133">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="f4871-134">このチュートリアルでは、以下のように `Log` メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="f4871-134">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

```cs
using System;

namespace Plugin.LoggingLibrary.Abstractions
{
    /// <summary>
    /// Interface for LoggingLibrary
    /// </summary>
    public interface ILoggingLibrary
    {
        /// <summary>
        /// Log a message
        /// </summary>
        void Log(string text);
    }
}
```

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="f4871-135">プラットフォーム固有のコードを記述する</span><span class="sxs-lookup"><span data-stu-id="f4871-135">Write your platform-specific code</span></span>

<span data-ttu-id="f4871-136">`ILoggingLibrary` インターフェイスとそのメソッドのプラットフォーム固有の実装を行うには、次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="f4871-136">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="f4871-137">各プラットフォーム プロジェクトの `LoggingLibraryImplementation.cs` ファイルを開き、必要なコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="f4871-137">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="f4871-138">たとえば、`Plugin.LoggingLibrary.Android` プロジェクトを使用する場合は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="f4871-138">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

    ```cs
    using Plugin.LoggingLibrary.Abstractions;
    using System;

    namespace Plugin.LoggingLibrary
    {
        /// <summary>
        /// Implementation for Feature
        /// </summary>
        public class LoggingLibraryImplementation : ILoggingLibrary
        {
            /// <summary>
            /// Log a message
            /// </summary>
            public void Log(string text)
            {
                throw new NotImplementedException("Called Log on Android");
            }
        }
    }
    ```

1. <span data-ttu-id="f4871-139">サポートする各プラットフォームのプロジェクトでこの実装を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="f4871-139">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="f4871-140">iOS プロジェクトを右クリックし、 **[プロパティ]** を選択して **[ビルド]** タブをクリックし、 **[出力パス]** および **[XML ドキュメント ファイル]** の設定から "\iPhone" を削除します。</span><span class="sxs-lookup"><span data-stu-id="f4871-140">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="f4871-141">この操作は、このチュートリアルの後半での利便性のためだけに行います。</span><span class="sxs-lookup"><span data-stu-id="f4871-141">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="f4871-142">完了したら、ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="f4871-142">Save the file when done.</span></span>
1. <span data-ttu-id="f4871-143">ソリューションを右クリックし、 **[構成マネージャー]** を選択して、PCL とサポートする各プラットフォームの **[ビルド]** ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="f4871-143">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="f4871-144">ソリューションを右クリックし、 **[ソリューションのビルド]** を選択して作業内容を確認し、次にパッケージ化する成果物を生成します。</span><span class="sxs-lookup"><span data-stu-id="f4871-144">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you package next.</span></span> <span data-ttu-id="f4871-145">欠落している参照に関するエラーが発生した場合は、ソリューションを右クリックし、 **[NuGet パッケージの復元]** を選択して依存関係をインストールしてからリビルドします。</span><span class="sxs-lookup"><span data-stu-id="f4871-145">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="f4871-146">iOS 用にビルドするには、「[Xamarin.iOS for Visual Studio の概要](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)」の説明に従って、ネットワーク接続された Mac を Visual Studio に接続する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4871-146">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="f4871-147">使用可能な Mac がない場合は、構成マネージャーで iOS プロジェクトをクリアします (上記の手順 3)。</span><span class="sxs-lookup"><span data-stu-id="f4871-147">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>

## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="f4871-148">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="f4871-148">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="f4871-149">コマンド プロンプトを開き、`.sln` ファイルの 1 レベル下の `LoggingLibrary` フォルダーに移動して NuGet `spec` コマンドを実行し、初期 `Package.nuspec` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="f4871-149">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

    ```cli
    nuget spec
    ```

1. <span data-ttu-id="f4871-150">このファイルの名前を `LoggingLibrary.nuspec` に変更して、エディターで開きます。</span><span class="sxs-lookup"><span data-stu-id="f4871-150">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="f4871-151">以下の内容と一致するようにファイルを更新して、YOUR_NAME を適切な値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="f4871-151">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="f4871-152">具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則に関する記述を参照)。</span><span class="sxs-lookup"><span data-stu-id="f4871-152">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="f4871-153">また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="f4871-153">Also note that you must also update the author and description tags or you get an error during the packing step.</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
        <metadata>
        <id>LoggingLibrary.YOUR_NAME</id>
        <version>1.0.0</version>
        <title>LoggingLibrary</title>
        <authors>YOUR_NAME</authors>
        <owners>YOUR_NAME</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Tip]
> <span data-ttu-id="f4871-154">パッケージ バージョンの末尾を `-alpha`、`-beta` または `-rc` にしてパッケージをプレリリースとしてマークすることができます。プレリリース バージョンの詳細については、[プレリリース バージョン](../create-packages/prerelease-packages.md)に関するページを確認してください。</span><span class="sxs-lookup"><span data-stu-id="f4871-154">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="f4871-155">参照アセンブリを追加する</span><span class="sxs-lookup"><span data-stu-id="f4871-155">Add reference assemblies</span></span>

<span data-ttu-id="f4871-156">プラットフォーム固有の参照アセンブリを含めるには、サポート対象プラットフォームに応じて、以下の内容を `LoggingLibrary.nuspec` の `<files>` 要素に追加します。</span><span class="sxs-lookup"><span data-stu-id="f4871-156">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

```xml
<!-- Insert below <metadata> element -->
<files>
    <!-- Cross-platform reference assemblies -->
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
    <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

    <!-- iOS reference assemblies -->
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

    <!-- Android reference assemblies -->
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

    <!-- UWP reference assemblies -->
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
    <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
</files>
```

> [!Note]
> <span data-ttu-id="f4871-157">DLL および XML ファイルの名前を短くするには、指定されたプロジェクトを右クリックし、 **[ライブラリ]** タブを選択してアセンブリ名を変更します。</span><span class="sxs-lookup"><span data-stu-id="f4871-157">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>

### <a name="add-dependencies"></a><span data-ttu-id="f4871-158">依存関係を追加する</span><span class="sxs-lookup"><span data-stu-id="f4871-158">Add dependencies</span></span>

<span data-ttu-id="f4871-159">ネイティブ実装の特定の依存関係がある場合は、次の例のように `<dependencies>` 要素と `<group>` 要素を使用して指定します。</span><span class="sxs-lookup"><span data-stu-id="f4871-159">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="MonoAndroid">
        <!--MonoAndroid dependencies go here-->
    </group>
    <group targetFramework="Xamarin.iOS10">
        <!--Xamarin.iOS10 dependencies go here-->
    </group>
    <group targetFramework="uap">
        <!--uap dependencies go here-->
    </group>
</dependencies>
```

<span data-ttu-id="f4871-160">たとえば、以下の場合は、UAP ターゲットの依存関係として iTextSharp を設定します。</span><span class="sxs-lookup"><span data-stu-id="f4871-160">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="f4871-161">最終的な .nuspec</span><span class="sxs-lookup"><span data-stu-id="f4871-161">Final .nuspec</span></span>

<span data-ttu-id="f4871-162">最終的な `.nuspec` ファイルは次のようになります。ここでも、YOUR_NAME は適切な値に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="f4871-162">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
    <id>LoggingLibrary.YOUR_NAME</id>
    <version>1.0.0</version>
    <title>LoggingLibrary</title>
    <authors>YOUR_NAME</authors>
    <owners>YOUR_NAME</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <description>Awesome application logging utility</description>
    <releaseNotes>First release</releaseNotes>
    <copyright>Copyright 2016</copyright>
    <tags>logger logging logs</tags>
        <dependencies>
        <group targetFramework="MonoAndroid">
            <!--MonoAndroid dependencies go here-->
        </group>
        <group targetFramework="Xamarin.iOS10">
            <!--Xamarin.iOS10 dependencies go here-->
        </group>
        <group targetFramework="uap">
            <dependency id="iTextSharp" version="5.5.9" />
        </group>
    </dependencies>
    </metadata>
    <files>
        <!-- Cross-platform reference assemblies -->
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary\bin\Release\Plugin.LoggingLibrary.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.xml" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.dll" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.dll" />
        <file src="Plugin.LoggingLibrary.Abstractions\bin\Release\Plugin.LoggingLibrary.Abstractions.xml" target="lib\netstandard1.4\Plugin.LoggingLibrary.Abstractions.xml" />

        <!-- iOS reference assemblies -->
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.dll" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.iOS\bin\Release\Plugin.LoggingLibrary.xml" target="lib\Xamarin.iOS10\Plugin.LoggingLibrary.xml" />

        <!-- Android reference assemblies -->
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.dll" target="lib\MonoAndroid10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.Android\bin\Release\Plugin.LoggingLibrary.xml" target="lib\MonoAndroid10\Plugin.LoggingLibrary.xml" />

        <!-- UWP reference assemblies -->
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.dll" target="lib\UAP10\Plugin.LoggingLibrary.dll" />
        <file src="Plugin.LoggingLibrary.UWP\bin\Release\Plugin.LoggingLibrary.xml" target="lib\UAP10\Plugin.LoggingLibrary.xml" />
    </files>
</package>
```

## <a name="package-the-component"></a><span data-ttu-id="f4871-163">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="f4871-163">Package the component</span></span>

<span data-ttu-id="f4871-164">パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="f4871-164">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```cli
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="f4871-165">これで `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` が生成されます。</span><span class="sxs-lookup"><span data-stu-id="f4871-165">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="f4871-166">[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="f4871-166">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you see the following contents:</span></span>

![LoggingLibrary パッケージが表示された NuGet パッケージ エクスプローラー](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="f4871-168">`.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="f4871-168">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="f4871-169">したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。</span><span class="sxs-lookup"><span data-stu-id="f4871-169">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>

<span data-ttu-id="f4871-170">パッケージを他の開発者が使用できるようにする場合は、「[パッケージの公開](../nuget-org/publish-a-package.md)」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="f4871-170">To make your package available to other developers,  follow the instructions on [Publish a package](../nuget-org/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="f4871-171">関連トピック</span><span class="sxs-lookup"><span data-stu-id="f4871-171">Related topics</span></span>

- [<span data-ttu-id="f4871-172">.nuspec 参照</span><span class="sxs-lookup"><span data-stu-id="f4871-172">Nuspec Reference</span></span>](../reference/nuspec.md)
- [<span data-ttu-id="f4871-173">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="f4871-173">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="f4871-174">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="f4871-174">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="f4871-175">複数の .NET Framework バージョンのサポート</span><span class="sxs-lookup"><span data-stu-id="f4871-175">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="f4871-176">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="f4871-176">Include MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="f4871-177">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="f4871-177">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)