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
# <a name="create-cross-platform-packages"></a>クロスプラットフォーム パッケージの作成

クロスプラットフォーム パッケージには、実行時のオペレーティング システムに応じて、iOS、Android、および Windows でネイティブ API を使用するコードが含まれます。 これを行うのは簡単ですが、開発者が共通の API のセキュリティ、外部からのアクセスを通じて PCL または .NET Standard ライブラリからパッケージを使用できるようにすることをお勧めします。

このチュートリアルでは、iOS、Android、および Windows 上のモバイル プロジェクトで使用できるクロスプラットフォームの NuGet パッケージを作成します。

1. [前提条件](#pre-requisites)
1. [プロジェクトの構造体および抽象化コードを作成する](#create-the-project-structure-and-abstraction-code)
1. [プラットフォーム固有のコードを記述する](#write-your-platform-specific-code)
1. [.nuspec ファイルを作成して更新する](#create-and-update-the-nuspec-file)
1. [コンポーネントをパッケージ化する](#package-the-component)
1. [関連トピック](#related-topics)

## <a name="pre-requisites"></a>前提条件

1. Visual Studio 2015、ユニバーサル Windows プラットフォーム (UWP) および Xamarin。 [visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。もちろん、Professional Edition と Enterprise Edition も使用できます。 UWP および Xamarin ツールを含めるには、カスタム インストールを選択して、適切なオプションを確認します。
1. NuGet CLI。 [nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの nuget.exe をダウンロードして、任意の場所に保存します。 次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。

> [!Note]
> nuget.exe はインストーラーではなく CLI ツール自体です。したがって、ブラウザーからダウンロードしたファイルは実行するのではなく、必ず保存してください。


## <a name="create-the-project-structure-and-abstraction-code"></a>プロジェクトの構造体および抽象化コードを作成する

1. Visual Studio 用の [Plugin For Xamarin テンプレート拡張機能](https://marketplace.visualstudio.com/items?itemName=vs-publisher-473885.PluginForXamarinTemplates)をダウンロードして実行します。 これらのテンプレートを使用することで、このチュートリアルで必要なプロジェクトの構造体を簡単に作成できます。
1. Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に選択し、`Plugin` を検索して **[Plugin for Xamarin]** テンプレートを選択し、名前を LoggingLibrary に変更してから [OK] をクリックします。

    ![Visual Studio の新しい空のアプリ (Xamarin.Forms ポータブル) プロジェクト](media/CrossPlatform-NewProject.png)

結果として得られるソリューションには、以下のようなさまざまなプラットフォーム固有のプロジェクトと共に 2 つの PCL プロジェクトが含まれます。

- `Plugin.LoggingLibrary.Abstractions (Portable)` という名前の PCL ではコンポーネントのパブリック インターフェイス (API のセキュリティ、外部からのアクセス) を定義します。この場合、ILoggingLibrary.cs ファイルに含まれている `ILoggingLibrary` インターフェイスとなります。 これは、ライブラリへのインターフェイスを定義する場所です。
- その他の PCL `Plugin.LoggingLibrary (Portable)` には、実行時に抽象インターフェイスのプラットフォーム固有の実装を検索する CrossLoggingLibrary.cs のコードが含まれます。 通常、このファイルを変更する必要はありません。
- `Plugin.LoggingLibrary.Android` などのプラットフォーム固有の各プロジェクトには、対応する LoggingLibraryImplementation.cs ファイルのインターフェイスのネイティブ実装が含まれます。 これは、ライブラリのコードをビルドする場所です。

既定では、抽象化プロジェクトの ILoggingLibrary.cs ファイルにインターフェイス定義が含まれますが、メソッドは含まれません。 このチュートリアルでは、以下のように `Log` メソッドを追加します。

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

## <a name="write-your-platform-specific-code"></a>プラットフォーム固有のコードを記述する

`ILoggingLibrary` インターフェイスとそのメソッドのプラットフォーム固有の実装を行うには、次の操作を実行します。

1. 各プラットフォーム プロジェクトの `LoggingLibraryImplementation.cs` ファイルを開き、必要なコードを追加します。 たとえば、`Plugin.LoggingLibrary.Android` プロジェクトを使用する場合は次のようになります。

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

1. サポートする各プラットフォームのプロジェクトでこの実装を繰り返します。
1. iOS プロジェクトを右クリックし、**[プロパティ]** を選択して **[ビルド]** タブをクリックし、**[出力パス]** および **[XML ドキュメント ファイル]** の設定から "\iPhone" を削除します。 この操作は、このチュートリアルの後半での利便性のためだけに行います。 完了したら、ファイルを保存します。
1. ソリューションを右クリックし、**[構成マネージャー]** を選択して、PCL とサポートする各プラットフォームの **[ビルド]** ボックスをオンにします。
1. ソリューションを右クリックし、**[ソリューションのビルド]** を選択して作業内容を確認し、次にパッケージ化する成果物を生成します。 欠落している参照に関するエラーが発生した場合は、ソリューションを右クリックし、**[NuGet パッケージの復元]** を選択して依存関係をインストールしてからリビルドします。

> [!Note]
> iOS 用にビルドするには、「[Xamarin.iOS for Visual Studio の概要](https://developer.xamarin.com/guides/ios/getting_started/installation/windows/introduction_to_xamarin_ios_for_visual_studio/)」の説明に従って、ネットワーク接続された Mac を Visual Studio に接続する必要があります。 使用可能な Mac がない場合は、構成マネージャーで iOS プロジェクトをクリアします (上記の手順 3)。


## <a name="create-and-update-the-nuspec-file"></a>.nuspec ファイルを作成して更新する

1. コマンド プロンプトを開き、`.sln` ファイルの 1 レベル下の `LoggingLibrary` フォルダーに移動して NuGet `spec` コマンドを実行し、初期 `Package.nuspec` ファイルを作成します。

```
nuget spec
```

1. このファイルの名前を `LoggingLibrary.nuspec` に変更して、エディターで開きます。
1. 以下の内容と一致するようにファイルを更新して、YOUR_NAME を適切な値に置き換えます。 具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則に関する記述を参照)。 また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。

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
> パッケージ バージョンの末尾を `-alpha`、`-beta` または `-rc` にしてパッケージをプレリリースとしてマークすることができます。プレリリース バージョンの詳細については、[プレリリース バージョン](../create-packages/prerelease-packages.md)に関するページを確認してください。

### <a name="add-reference-assemblies"></a>参照アセンブリを追加する

プラットフォーム固有の参照アセンブリを含めるには、サポート対象プラットフォームに応じて、以下の内容を `LoggingLibrary.nuspec` の `<files>` 要素に追加します。

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
> DLL および XML ファイルの名前を短くするには、指定されたプロジェクトを右クリックし、**[ライブラリ]** タブを選択してアセンブリ名を変更します。


### <a name="add-dependencies"></a>依存関係を追加する

ネイティブ実装の特定の依存関係がある場合は、次の例のように `<dependencies>` 要素と `<group>` 要素を使用して指定します。

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

たとえば、以下の場合は、UAP ターゲットの依存関係として iTextSharp を設定します。

```xml
<dependencies>
    <group targetFramework="uap">
        <dependency id="iTextSharp" version="5.5.9" />
    </group>
</dependencies>
```

### <a name="final-nuspec"></a>最終的な .nuspec

最終的な `.nuspec` ファイルは次のようになります。ここでも、YOUR_NAME は適切な値に置き換える必要があります。

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

## <a name="package-the-component"></a>コンポーネントをパッケージ化する

パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。

```
nuget pack LoggingLibrary.nuspec
```

これで `LoggingLibrary.YOUR_NAME.1.0.0.nupkg` が生成されます。 [NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。

![LoggingLibrary パッケージが表示された NuGet パッケージ エクスプローラー](media/Cross-Platform-PackageExplorer.png)

> [!Tip]
> `.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。 したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。


パッケージを他の開発者が使用できるようにする場合は、「[パッケージの公開](../create-packages/publish-a-package.md)」の手順に従ってください。

## <a name="related-topics"></a>関連トピック

- [.nuspec 参照](../schema/nuspec.md)
- [シンボル パッケージ](../create-packages/symbol-packages.md)
- [パッケージのバージョン管理](../reference/package-versioning.md)
- [複数の .NET Framework バージョンのサポート](../create-packages/supporting-multiple-target-frameworks.md)
- [パッケージに MSBuild プロパティとターゲットを含める](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [ローカライズされたパッケージを作成する](../create-packages/creating-localized-packages.md)