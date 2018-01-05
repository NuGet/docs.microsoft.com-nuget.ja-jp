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
# <a name="create-net-standard-packages-with-visual-studio-2015"></a>Visual Studio 2015 での .NET Standard NuGet パッケージの作成

*NuGet 3.x に適用されます。NuGet 4.x+ を使用して作業を行う場合は、[Visual Studio 2017 での .NET Standard パッケージの作成](../guides/create-net-standard-packages-vs2017.md)に関するページを参照してください。*

[.NET Standard ライブラリ](https://docs.microsoft.com/dotnet/articles/standard/library)は、すべての .NET ランタイムで使用できるようにすることを目的とした .NET API の正式な仕様です。したがって、.NET エコシステムでより高い統一性が確立されます。 .NET Standard Library は、ワークロードに関係なく、すべての .NET プラットフォーム用に統一された BCL (基本クラス ライブラリ) API のセットを定義して実装します。 これにより、開発者はすべての .NET ランタイム間で使用可能な PCL を生成でき、共有コードでプラットフォーム固有の条件付きコンパイル ディレクティブを除去するまでとはいかないまでも減らすことはできます。

このガイドでは、.NET Standard Library 1.4 をターゲットとする nuget パッケージの作成方法を示します。 これは、.NET Framework 4.6.1、ユニバーサル Windows プラットフォーム 10、.NET Core、および Mono/Xamarin に適用できます。 詳細については、このトピックの後半の「[.NET Standard マッピング テーブル](#net-standard-mapping-table)」を参照してください。

1. [前提条件](#pre-requisites)
1. [クラス ライブラリ プロジェクトを作成する](#create-the-class-library-project)
1. [.nuspec ファイルを作成して更新する](#create-and-update-the-nuspec-file)
1. [コンポーネントをパッケージ化する](#package-the-component)
1. [追加オプション](#additional-options)
1. [.NET Standard マッピング テーブル](#net-standard-mapping-table)
1. [関連トピック](#related-topics)


## <a name="pre-requisites"></a>前提条件

1. Visual Studio 2015。 [visualstudio.com](https://www.visualstudio.com/) から無料の Community Edition をインストールします。もちろん、Professional Edition と Enterprise Edition も使用できます。
1. .NET Core: [https://go.microsoft.com/fwlink/?LinkId=824849](https://go.microsoft.com/fwlink/?LinkId=824849) から、Visual Studio 2015 用のテンプレートとその他のツールと共に .NET Core をインストールします。
1. NuGet CLI。 [nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの nuget.exe をダウンロードして、任意の場所に保存します。 次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。

> [!Note]
> nuget.exe はインストーラーではなく CLI ツール自体です。したがって、ブラウザーからダウンロードしたファイルは実行するのではなく、必ず保存してください。



## <a name="create-the-class-library-project"></a>クラス ライブラリ プロジェクトを作成する

1. Visual Studio で、**[ファイル]、[新規]、[プロジェクト]** の順に移動し、**[Visual C#]、[Windows]** ノードの順に展開して **[クラス ライブラリ (ポータブル)]** を選択し、名前を AppLogger に変更してから [OK] をクリックします。

    ![新しいクラス ライブラリ プロジェクトを作成する](media/NetStandard-NewProject.png)

1. 表示された **[ポータブル クラス ライブラリの追加]** ダイアログ ボックスで、`.NET Framework 4.6` と `ASP.NET Core 1.0` オプションを選択します。
1. ソリューション エクスプローラーで `AppLogger (Portable)` を右クリックして **[プロパティ]** を選択し、**[ライブラリ]** タブを選択してから **[ターゲット]** セクションの **[ターゲットの .NET Platform Standard]** をクリックします。 これで確認のプロンプトが表示されます。その後、ドロップダウンから `.NET Standard 1.4` を選択できます。

    ![.NET Standard 1.4 へのターゲットの設定](media/NetStandard-ChangeTarget.png)

1. **[ビルド]** タブをクリックして **[構成]** を `Release` に変更し、**[XML ドキュメント ファイル]** のボックスをオンにします。
1. たとえば、次のようにコンポーネントにコードを追加します。

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

1. プロジェクト (Release 構成の) をビルドし、DLL および XML ファイルが bin\Release フォルダー内に生成されていることを確認します。

## <a name="create-and-update-the-nuspec-file"></a>.nuspec ファイルを作成して更新する

1. コマンド プロンプトを開き、(`.sln` ファイルの 1 レベル下の) `AppLogg.csproj` フォルダーを含むフォルダーに移動して NuGet `spec` コマンドを実行し、初期 `AppLogger.nuspec` ファイルを作成します。

```
nuget spec
```

1. `AppLogger.nuspec` をエディターで開き、以下の内容と一致するように更新して、YOUR_NAME を適切な値に置き換えます。 具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則を参照)。 また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。

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

1. 参照アセンブリを `.nuspec` ファイル、つまり、ライブラリの DLL および IntelliSense XML ファイルに追加します。

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

1. ソリューションを右クリックし、**[ソリューションのビルド]** を選択してパッケージのすべてのファイルを生成します。


## <a name="package-the-component"></a>コンポーネントをパッケージ化する

パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。

```
nuget pack AppLogger.nuspec
```

これで `AppLogger.YOUR_NAME.1.0.0.nupkg` が生成されます。 [NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。

![AppLogger パッケージが表示された NuGet パッケージ エクスプローラー](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。 したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。

パッケージを他の開発者が使用できるようにする場合は、[パッケージの発行](../create-packages/publish-a-package.md)に関するページの手順に従ってください。

`pack` には Mac OS X の場合は Mono 4.4.2 が必要であり、Linux 1 システムでは動作しないことに注意してください。 Mac の場合、`.nuspec` ファイルの Windows パス名を Unix 形式のパスに変換する必要もあります。

## <a name="additional-options"></a>[追加オプション]

次のセクションでは、NuGet パッケージを作成する場合の追加オプションについて説明します。

- [依存関係の宣言](#declaring-dependencies)
- [複数のターゲット フレームワークのサポート](#supporting-multiple-target-frameworks)
- [MSBuild のターゲットとプロパティの追加](#adding-targets-and-props-for-msbuild)
- [ローカライズされたパッケージの作成](#creating-localized-packages)
- [Readme の追加](#adding-a-readme)

### <a name="declaring-dependencies"></a>依存関係の宣言

他の NuGet パッケージに対する依存関係がある場合、`<group>` 要素を使用して `<dependencies>` 要素で依存関係をリストします。 たとえば、NewtonSoft.Json 8.0.3 以降に対する依存関係を宣言するには、以下を追加します。

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

*version* 属性の構文は、バージョン 8.0.3 以降が許容されることを示します。 別のバージョンの範囲を指定する場合は、「[パッケージのバージョン管理](../reference/package-versioning.md)」を参照してください。

### <a name="supporting-multiple-target-frameworks"></a>複数のターゲット フレームワークのサポート

たとえば、.NET Standard 1.4 で使用できない .NET Framework 4.6.2 の API を活用するとします。 これを行うには、まず、条件付きコンパイルまたは共有プロジェクトを使用して、.NET 4.6.2 用にライブラリがコンパイルされていることを確認する必要があります  (Visual Studio では、NetCore プロジェクトを作成し、任意のフレームワークを複数のフレームワーク セクションに追加してからビルドできます)。次に、以下のように単純な規則に基づく作業ディレクトリを使用して、パッケージを作成します。

1. `.nuspec` ファイルを含むプロジェクトのルート フォルダーで、`lib` という名前のフォルダーを作成します。
1. `lib` 内で、サポートするプラットフォームごとにフォルダーを作成します。

        \lib
            \netstandard1.4
                \AppLogger.dll
            \net462
                \AppLogger.dll

1. `.nuspec` ファイルで、`package` ノードの下に `files` ノードを追加し、ワイルドカードを使用して `lib` のファイルを参照します。 **注:** 規則に基づく作業ディレクトリの方法ではトークン置換はサポートされないため、リテラル値に置き換えてください。

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

1. `nuget pack AppLogger.spec` を使用して、もう一度パッケージを作成します。

この方法の使用の詳細については、「[Supporting Multiple .NET Framework Versions](../create-packages/supporting-multiple-target-frameworks.md)」 (複数の .NET Framework バージョンのサポート) を参照してください。

### <a name="adding-targets-and-props-for-msbuild"></a>MSBuild のターゲットとプロパティの追加

ビルド時のカスタム ツールまたはプロセスの実行など、場合によっては、パッケージを使用するプロジェクト内のカスタム ビルド ターゲットまたはプロパティを追加する必要があります。 これは、以下の手順で説明されているように `\build` フォルダーにファイルを追加することで行うことができます。 NuGet は \build ファイルを使用してパッケージをインストールすると、.targets および .props ファイルを指すプロジェクト ファイルに MSBuild 要素を追加します。

> [!Note]
> `project.json` を使用する場合、ターゲットはプロジェクトに追加されませんが、`project.lock.json` を通じて使用できます。


1. `.nuspec` ファイルを含むプロジェクト フォルダーで、`build` という名前のフォルダーを作成します。
1. `build` 内で、サポート対象ごとにフォルダーを作成し、その中に `.targets` と `.props` ファイルを配置します。

        \build
            \netstandard1.4
                \AppLogger.props
                \AppLogger.targets
            \net462
                \AppLogger.props
                \AppLogger.targets

1. `.nuspec` ファイルで、`package` ノードの下に `files` ノードを追加し、ワイルドカードを使用して `build` のファイルを参照します。

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

1. `nuget pack AppLogger.nuspec` を使用して、もう一度パッケージを作成します。

詳細については、「[パッケージに MSBuild プロパティとターゲットを含める](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)」を参照してください。


### <a name="creating-localized-packages"></a>ローカライズされたパッケージの作成

ローカライズ版のライブラリを作成する場合は、ロケールごとに別のパッケージを作成するか、単一のパッケージ内にローカライズされたリソース アセンブリを含めることができます。 ここでは、ドイツ語とイタリア語の場合の後者の方法を実行する方法を説明します。

1. `lib` の下の各ターゲット フレームワーク フォルダー内で、既定の英語以外のサポートされている言語ごとにフォルダーを作成します。 これらのフォルダーには、リソース アセンブリおよびローカライズされた IntelliSense XML ファイルを配置できます。 例:

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

1. `.nuspec` ファイルで、`<files>` ノードのこれらのファイルを参照します。

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

1. `nuget pack AppLogger.nuspec` を使用して、もう一度パッケージを作成します。


### <a name="adding-a-readme"></a>Readme の追加

パッケージのルートに `readme.txt` ファイルを含めた場合、パッケージが直接インストールされたときに Visual Studio に表示されます。

> [!Note]
> Readme ファイルは、依存関係としてインストールされているパッケージや、.NET Core プロジェクトの場合は表示されません。


これを行うには、`readme.txt` ファイルを作成し、プロジェクト ルート ディレクトリに配置して、`.nuspec` ファイルで参照します。

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


## <a name="net-standard-mapping-table"></a>.NET Standard マッピング テーブル

|プラットフォーム名 |Alias|
|--------------|-----|
|.NET Standard | netstandard| 1.0| 1.1| 1.2| 1.3| 1.4| 1.5| 1.6|
|.NET Core | netcoreapp| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| 1.0|
|.NET Framework| net| 4.5| 4.5.1| 4.6| 4.6.1| 4.6.2| 4.6.3|
|Mono/Xamarin プラットフォーム| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;| &#x2192;|
|ユニバーサル Windows プラットフォーム| uap| &#x2192;| &#x2192;| &#x2192;| &#x2192;|10.0|
|Windows| win| &#x2192;| 8.0| 8.1|
|Windows Phone| wpa| &#x2192;| &#x2192;|8.1|
|Windows Phone Silverlight| wp| 8.0|



## <a name="related-topics"></a>関連トピック

- [.nuspec 参照](../schema/nuspec.md)
- [シンボル パッケージ](../create-packages/symbol-packages.md)
- [パッケージのバージョン管理](../reference/package-versioning.md)
- [複数の .NET Framework バージョンのサポート](../create-packages/supporting-multiple-target-frameworks.md)
- [パッケージに MSBuild プロパティとターゲットを含める](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [ローカライズされたパッケージを作成する](../create-packages/creating-localized-packages.md)
- [.NET Standard ライブラリのドキュメント](https://docs.microsoft.com/dotnet/articles/standard/library)
- [.NET Framework から .NET Core への移植](https://docs.microsoft.com/dotnet/articles/core/porting/index)
