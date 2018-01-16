---
title: "クロスプラットフォーム NuGet パッケージの作成 (iOS、Android、および Windows 用) | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: ae24824b-a138-4d12-a810-1f653ddffd32
description: "iOS、Android、および Windows でネイティブ API を使用する、Xamarin の NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。"
keywords: "パッケージを作成する, Xamarin のパッケージ, クロスプラットフォーム パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f372856232f151efcf972881cffbe7d4bb7ed6ee
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="create-cross-platform-packages"></a><span data-ttu-id="232b5-104">クロスプラットフォーム パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="232b5-104">Create cross-platform packages</span></span>

<span data-ttu-id="232b5-105">クロスプラットフォーム パッケージには、実行時のオペレーティング システムに応じて、iOS、Android、および Windows でネイティブ API を使用するコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="232b5-105">A cross-platform package contains code that uses native APIs on iOS, Android, and Windows, depending on the run-time operating system.</span></span> <span data-ttu-id="232b5-106">これを行うのは簡単ですが、開発者が共通の API のセキュリティ、外部からのアクセスを通じて PCL または .NET Standard ライブラリからパッケージを使用できるようにすることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="232b5-106">Although this is straightforward to do, it's preferable to let developers consume the package from a PCL or .NET Standard libraries through a common API surface area.</span></span>

<span data-ttu-id="232b5-107">このチュートリアルでは、iOS、Android、および Windows 上のモバイル プロジェクトで使用できるクロスプラットフォームの NuGet パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="232b5-107">In this walkthrough you'll create a cross-platform NuGet package that can be used in mobile projects on iOS, Android, and Windows.</span></span>

1. [<span data-ttu-id="232b5-108">前提条件</span><span class="sxs-lookup"><span data-stu-id="232b5-108">Pre-requisites</span></span>](#pre-requisites)
1. [<span data-ttu-id="232b5-109">プロジェクトの構造体および抽象化コードを作成する</span><span class="sxs-lookup"><span data-stu-id="232b5-109">Create the project structure and abstraction code</span></span>](#create-the-project-structure-and-abstraction-code)
1. [<span data-ttu-id="232b5-110">プラットフォーム固有のコードを記述する</span><span class="sxs-lookup"><span data-stu-id="232b5-110">Write your platform-specific code</span></span>](#write-your-platform-specific-code)
1. [<span data-ttu-id="232b5-111">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="232b5-111">Create and update the .nuspec file</span></span>](#create-and-update-the-nuspec-file)
1. [<span data-ttu-id="232b5-112">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="232b5-112">Package the component</span></span>](#package-the-component)
1. [<span data-ttu-id="232b5-113">関連トピック</span><span class="sxs-lookup"><span data-stu-id="232b5-113">Related topics</span></span>](#related-topics)

## <a name="pre-requisites"></a><span data-ttu-id="232b5-114">前提条件</span><span class="sxs-lookup"><span data-stu-id="232b5-114">Pre-requisites</span></span>

1. <span data-ttu-id="232b5-115">Visual Studio 2015、ユニバーサル Windows プラットフォーム (UWP) および Xamarin。</span><span class="sxs-lookup"><span data-stu-id="232b5-115">Visual Studio 2015 with Universal Windows Platform (UWP) and Xamarin.</span></span> <span data-ttu-id="232b5-116">[visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。もちろん、Professional Edition と Enterprise Edition も使用できます。</span><span class="sxs-lookup"><span data-stu-id="232b5-116">Install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/); you can use the Professional and Enterprise editions as well, of course.</span></span> <span data-ttu-id="232b5-117">UWP および Xamarin ツールを含めるには、カスタム インストールを選択して、適切なオプションを確認します。</span><span class="sxs-lookup"><span data-stu-id="232b5-117">To include UWP and Xamarin tools, select a Custom install and check the appropriate options.</span></span>
1. <span data-ttu-id="232b5-118">NuGet CLI。</span><span class="sxs-lookup"><span data-stu-id="232b5-118">NuGet CLI.</span></span> <span data-ttu-id="232b5-119">[nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの nuget.exe をダウンロードして、任意の場所に保存します。</span><span class="sxs-lookup"><span data-stu-id="232b5-119">Download the latest version of nuget.exe from [nuget.org/downloads](https://nuget.org/downloads), saving it to a location of your choice.</span></span> <span data-ttu-id="232b5-120">次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。</span><span class="sxs-lookup"><span data-stu-id="232b5-120">Then add that location to your PATH environment variable if it isn't already.</span></span>

> [!Note]
> <span data-ttu-id="232b5-121">nuget.exe はインストーラーではなく CLI ツール自体です。したがって、ブラウザーからダウンロードしたファイルは実行するのではなく、必ず保存してください。</span><span class="sxs-lookup"><span data-stu-id="232b5-121">nuget.exe is the CLI tool itself, not an installer, so be sure to save the downloaded file from your browser instead of running it.</span></span>


## <a name="create-the-project-structure-and-abstraction-code"></a><span data-ttu-id="232b5-122">プロジェクトの構造体および抽象化コードを作成する</span><span class="sxs-lookup"><span data-stu-id="232b5-122">Create the project structure and abstraction code</span></span>

1. <span data-ttu-id="232b5-123">Visual Studio 用の [Plugin For Xamarin テンプレート拡張機能](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)をダウンロードして実行します。</span><span class="sxs-lookup"><span data-stu-id="232b5-123">Download and run the [Plugin for Xamarin Templates extension](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates) for Visual Studio.</span></span> <span data-ttu-id="232b5-124">これらのテンプレートを使用することで、このチュートリアルで必要なプロジェクトの構造体を簡単に作成できます。</span><span class="sxs-lookup"><span data-stu-id="232b5-124">These templates will make it easy to create the necessary project structure for this walkthrough.</span></span>
1. <span data-ttu-id="232b5-125">Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、`Plugin` を検索して **[Plugin for Xamarin]** テンプレートを選択し、名前を LoggingLibrary に変更してから [OK] をクリックします。</span><span class="sxs-lookup"><span data-stu-id="232b5-125">In Visual Studio, **File > New > Project**, search for `Plugin`, select the **Plugin for Xamarin** template, change the name to LoggingLibrary, and click OK.</span></span>

    ![Visual Studio の新しい空のアプリ (Xamarin.Forms ポータブル) プロジェクト](media/CrossPlatform-NewProject.png)

<span data-ttu-id="232b5-127">結果として得られるソリューションには、以下のようなさまざまなプラットフォーム固有のプロジェクトと共に 2 つの PCL プロジェクトが含まれます。</span><span class="sxs-lookup"><span data-stu-id="232b5-127">The resulting solution contains two PCL projects, along with a variety of platform-specific projects:</span></span>

- <span data-ttu-id="232b5-128">`Plugin.LoggingLibrary.Abstractions (Portable)` という名前の PCL ではコンポーネントのパブリック インターフェイス (API のセキュリティ、外部からのアクセス) を定義します。この場合、ILoggingLibrary.cs ファイルに含まれている `ILoggingLibrary` インターフェイスとなります。</span><span class="sxs-lookup"><span data-stu-id="232b5-128">The PCL named `Plugin.LoggingLibrary.Abstractions (Portable)`, defines the public interface (the API surface area) of the component, in this case the `ILoggingLibrary` interface contained in the ILoggingLibrary.cs file.</span></span> <span data-ttu-id="232b5-129">これは、ライブラリへのインターフェイスを定義する場所です。</span><span class="sxs-lookup"><span data-stu-id="232b5-129">This is where you'll define the interface to your library.</span></span>
- <span data-ttu-id="232b5-130">その他の PCL `Plugin.LoggingLibrary (Portable)` には、実行時に抽象インターフェイスのプラットフォーム固有の実装を検索する CrossLoggingLibrary.cs のコードが含まれます。</span><span class="sxs-lookup"><span data-stu-id="232b5-130">The other PCL, `Plugin.LoggingLibrary (Portable)`, contains code in CrossLoggingLibrary.cs that will locate a platform-specific implementation of the abstract interface at run time.</span></span> <span data-ttu-id="232b5-131">通常、このファイルを変更する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="232b5-131">You typically don't need to modify this file.</span></span>
- <span data-ttu-id="232b5-132">`Plugin.LoggingLibrary.Android` などのプラットフォーム固有の各プロジェクトには、対応する LoggingLibraryImplementation.cs ファイルのインターフェイスのネイティブ実装が含まれます。</span><span class="sxs-lookup"><span data-stu-id="232b5-132">The platform-specific projects, such as `Plugin.LoggingLibrary.Android`, each contain contain a native implementation of the interface in their respective LoggingLibraryImplementation.cs files.</span></span> <span data-ttu-id="232b5-133">これは、ライブラリのコードをビルドする場所です。</span><span class="sxs-lookup"><span data-stu-id="232b5-133">This is where you'll build out your library's code.</span></span>

<span data-ttu-id="232b5-134">既定では、抽象化プロジェクトの ILoggingLibrary.cs ファイルにインターフェイス定義が含まれますが、メソッドは含まれません。</span><span class="sxs-lookup"><span data-stu-id="232b5-134">By default, the ILoggingLibrary.cs file of the Abstractions project contains an interface definition, but no methods.</span></span> <span data-ttu-id="232b5-135">このチュートリアルでは、以下のように `Log` メソッドを追加します。</span><span class="sxs-lookup"><span data-stu-id="232b5-135">For the purposes of this walkthrough, add a `Log` method as follows:</span></span>

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

## <a name="write-your-platform-specific-code"></a><span data-ttu-id="232b5-136">プラットフォーム固有のコードを記述する</span><span class="sxs-lookup"><span data-stu-id="232b5-136">Write your platform-specific code</span></span>

<span data-ttu-id="232b5-137">`ILoggingLibrary` インターフェイスとそのメソッドのプラットフォーム固有の実装を行うには、次の操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="232b5-137">To implement a platform-specific implementation of the `ILoggingLibrary` interface and its methods, do the following:</span></span>

1. <span data-ttu-id="232b5-138">各プラットフォーム プロジェクトの `LoggingLibraryImplementation.cs` ファイルを開き、必要なコードを追加します。</span><span class="sxs-lookup"><span data-stu-id="232b5-138">Open the `LoggingLibraryImplementation.cs` file of each platform project and add the necessary code.</span></span> <span data-ttu-id="232b5-139">たとえば、`Plugin.LoggingLibrary.Android` プロジェクトを使用する場合は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="232b5-139">For example (using the `Plugin.LoggingLibrary.Android` project):</span></span>

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

1. <span data-ttu-id="232b5-140">サポートする各プラットフォームのプロジェクトでこの実装を繰り返します。</span><span class="sxs-lookup"><span data-stu-id="232b5-140">Repeat this implementation in the projects for each platform you want to support.</span></span>
1. <span data-ttu-id="232b5-141">iOS プロジェクトを右クリックし、**[プロパティ]** を選択して **[ビルド]** タブをクリックし、**[出力パス]** および **[XML ドキュメント ファイル]** の設定から "\iPhone" を削除します。</span><span class="sxs-lookup"><span data-stu-id="232b5-141">Right-click the iOS project, select **Properties**, click the **Build** tab, and remove "\iPhone" from the **Output path** and **XML documentation file** settings.</span></span> <span data-ttu-id="232b5-142">この操作は、このチュートリアルの後半での利便性のためだけに行います。</span><span class="sxs-lookup"><span data-stu-id="232b5-142">This is just for later convenience in this walkthrough.</span></span> <span data-ttu-id="232b5-143">完了したら、ファイルを保存します。</span><span class="sxs-lookup"><span data-stu-id="232b5-143">Save the file when done.</span></span>
1. <span data-ttu-id="232b5-144">ソリューションを右クリックし、**[構成マネージャー]** を選択して、PCL とサポートする各プラットフォームの **[ビルド]** ボックスをオンにします。</span><span class="sxs-lookup"><span data-stu-id="232b5-144">Right-click the solution, select **Configuration Manager...**, and check the **Build** boxes for the PCLs and each platform you're supporting.</span></span>
1. <span data-ttu-id="232b5-145">ソリューションを右クリックし、**[ソリューションのビルド]** を選択して作業内容を確認し、次にパッケージ化する成果物を生成します。</span><span class="sxs-lookup"><span data-stu-id="232b5-145">Right-click the solution and select **Build Solution** to check your work and produce the artifacts that you'll package next.</span></span> <span data-ttu-id="232b5-146">欠落している参照に関するエラーが発生した場合は、ソリューションを右クリックし、**[NuGet パッケージの復元]** を選択して依存関係をインストールしてからリビルドします。</span><span class="sxs-lookup"><span data-stu-id="232b5-146">If you get errors about missing references, right-click the solution, select **Restore NuGet Packages** to install dependencies, and rebuild.</span></span>

> [!Note]
> <span data-ttu-id="232b5-147">iOS 用にビルドするには、「[Xamarin.iOS for Visual Studio の概要](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)」の説明に従って、ネットワーク接続された Mac を Visual Studio に接続する必要があります。</span><span class="sxs-lookup"><span data-stu-id="232b5-147">To build for iOS you need a networked Mac connected to Visual Studio as described on [Introduction to Xamarin.iOS for Visual Studio](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/).</span></span> <span data-ttu-id="232b5-148">使用可能な Mac がない場合は、構成マネージャーで iOS プロジェクトをクリアします (上記の手順 3)。</span><span class="sxs-lookup"><span data-stu-id="232b5-148">If you don't have a Mac available, clear the iOS project in the configuration manager (step 3 above).</span></span>


## <a name="create-and-update-the-nuspec-file"></a><span data-ttu-id="232b5-149">.nuspec ファイルを作成して更新する</span><span class="sxs-lookup"><span data-stu-id="232b5-149">Create and update the .nuspec file</span></span>

1. <span data-ttu-id="232b5-150">コマンド プロンプトを開き、`.sln` ファイルの 1 レベル下の `LoggingLibrary` フォルダーに移動して NuGet `spec` コマンドを実行し、初期 `Package.nuspec` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="232b5-150">Open a command prompt, navigate to the `LoggingLibrary` folder that's one level below where the `.sln` file is, and run the NuGet `spec` command to create the initial `Package.nuspec` file:</span></span>

```
nuget spec
```

1. <span data-ttu-id="232b5-151">このファイルの名前を `LoggingLibrary.nuspec` に変更して、エディターで開きます。</span><span class="sxs-lookup"><span data-stu-id="232b5-151">Rename this file to `LoggingLibrary.nuspec` and open it in an editor.</span></span>
1. <span data-ttu-id="232b5-152">以下の内容と一致するようにファイルを更新して、YOUR_NAME を適切な値に置き換えます。</span><span class="sxs-lookup"><span data-stu-id="232b5-152">Update the file to match the following, replacing YOUR_NAME with an appropriate value.</span></span> <span data-ttu-id="232b5-153">具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則に関する記述を参照)。</span><span class="sxs-lookup"><span data-stu-id="232b5-153">The `<id>` value, specifically, must be unique across nuget.org (see the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)).</span></span> <span data-ttu-id="232b5-154">また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="232b5-154">Also note that you must also update the author and description tags or you'll get an error during the packing step.</span></span>

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
> <span data-ttu-id="232b5-155">パッケージ バージョンの末尾を `-alpha`、`-beta` または `-rc` にしてパッケージをプレリリースとしてマークすることができます。プレリリース バージョンの詳細については、[プレリリース バージョン](../create-packages/prerelease-packages.md)に関するページを確認してください。</span><span class="sxs-lookup"><span data-stu-id="232b5-155">You can suffix your package version with `-alpha`, `-beta` or `-rc` to mark your package as pre-release, check [Pre-release versions](../create-packages/prerelease-packages.md) for more information about pre-release versions.</span></span>

### <a name="add-reference-assemblies"></a><span data-ttu-id="232b5-156">参照アセンブリを追加する</span><span class="sxs-lookup"><span data-stu-id="232b5-156">Add reference assemblies</span></span>

<span data-ttu-id="232b5-157">プラットフォーム固有の参照アセンブリを含めるには、サポート対象プラットフォームに応じて、以下の内容を `LoggingLibrary.nuspec` の `<files>` 要素に追加します。</span><span class="sxs-lookup"><span data-stu-id="232b5-157">To include platform-specific reference assemblies, add the following to the `<files>` element of `LoggingLibrary.nuspec` as appropriate for your supported platforms:</span></span>

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
> <span data-ttu-id="232b5-158">DLL および XML ファイルの名前を短くするには、指定されたプロジェクトを右クリックし、**[ライブラリ]** タブを選択してアセンブリ名を変更します。</span><span class="sxs-lookup"><span data-stu-id="232b5-158">To shorten the names of the DLL and XML files, right-click on any given project, select the **Library** tab, and change the assembly names.</span></span>


### <a name="add-dependencies"></a><span data-ttu-id="232b5-159">依存関係を追加する</span><span class="sxs-lookup"><span data-stu-id="232b5-159">Add dependencies</span></span>

<span data-ttu-id="232b5-160">ネイティブ実装の特定の依存関係がある場合は、次の例のように `<dependencies>` 要素と `<group>` 要素を使用して指定します。</span><span class="sxs-lookup"><span data-stu-id="232b5-160">If you have specific dependencies for native implementations, use the `<dependencies>` element with `<group>` elements to specify them, for example:</span></span>

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

<span data-ttu-id="232b5-161">たとえば、以下の場合は、UAP ターゲットの依存関係として iTextSharp を設定します。</span><span class="sxs-lookup"><span data-stu-id="232b5-161">For example, the following would set iTextSharp as a dependency for the UAP target:</span></span>

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a><span data-ttu-id="232b5-162">最終的な .nuspec</span><span class="sxs-lookup"><span data-stu-id="232b5-162">Final .nuspec</span></span>

<span data-ttu-id="232b5-163">最終的な `.nuspec` ファイルは次のようになります。ここでも、YOUR_NAME は適切な値に置き換える必要があります。</span><span class="sxs-lookup"><span data-stu-id="232b5-163">Your final `.nuspec` file should now look like the following, where again YOUR_NAME should be replaced with an appropriate value:</span></span>

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

## <a name="package-the-component"></a><span data-ttu-id="232b5-164">コンポーネントをパッケージ化する</span><span class="sxs-lookup"><span data-stu-id="232b5-164">Package the component</span></span>

<span data-ttu-id="232b5-165">パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。</span><span class="sxs-lookup"><span data-stu-id="232b5-165">With the completed `.nuspec` referencing all the files you need to include in the package, you're ready to run the `pack` command:</span></span>

```
nuget pack LoggingLibrary.nuspec
```

<span data-ttu-id="232b5-166">これで `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` が生成されます。</span><span class="sxs-lookup"><span data-stu-id="232b5-166">This will generate `LoggingLibrary.YOUR_NAME.1.0.0.nupkg`.</span></span> <span data-ttu-id="232b5-167">[NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。</span><span class="sxs-lookup"><span data-stu-id="232b5-167">Opening this file in a tool like the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) and expanding all the nodes, you'll see the following contents:</span></span>

![LoggingLibrary パッケージが表示された NuGet パッケージ エクスプローラー](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> <span data-ttu-id="232b5-169">`.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。</span><span class="sxs-lookup"><span data-stu-id="232b5-169">A `.nupkg` file is just a ZIP file with a different extension.</span></span> <span data-ttu-id="232b5-170">したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。</span><span class="sxs-lookup"><span data-stu-id="232b5-170">You can also examine package contents, then, by changing `.nupkg` to `.zip`, but remember to restore the extension before uploading a package to nuget.org.</span></span>


<span data-ttu-id="232b5-171">パッケージを他の開発者が使用できるようにする場合は、「[パッケージの公開](../create-packages/publish-a-package.md)」の手順に従ってください。</span><span class="sxs-lookup"><span data-stu-id="232b5-171">To make your package available to other developers,  follow the instructions on [Publish a package](../create-packages/publish-a-package.md).</span></span>

## <a name="related-topics"></a><span data-ttu-id="232b5-172">関連トピック</span><span class="sxs-lookup"><span data-stu-id="232b5-172">Related topics</span></span>

- [<span data-ttu-id="232b5-173">.nuspec 参照</span><span class="sxs-lookup"><span data-stu-id="232b5-173">Nuspec Reference</span></span>](../schema/nuspec.md)
- [<span data-ttu-id="232b5-174">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="232b5-174">Symbol packages</span></span>](../create-packages/symbol-packages.md)
- [<span data-ttu-id="232b5-175">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="232b5-175">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="232b5-176">複数の .NET Framework バージョンのサポート</span><span class="sxs-lookup"><span data-stu-id="232b5-176">Supporting Multiple .NET Framework Versions</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="232b5-177">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="232b5-177">Including MSBuild props and targets in a package</span></span>](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="232b5-178">ローカライズされたパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="232b5-178">Creating Localized Packages</span></span>](../create-packages/creating-localized-packages.md)