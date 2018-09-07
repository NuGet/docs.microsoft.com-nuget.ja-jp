---
title: Visual Studio 2015 での NET Standard および NET Framework NuGet パッケージの作成
description: NuGet 3.x と Visual Studio 2015 を使用して、.NET Standard および .NET Framework の NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。
author: karann-msft
ms.author: karann
ms.date: 02/02/2018
ms.topic: tutorial
ms.openlocfilehash: 7b1ccfbede4cec53cee3ec7d1c023e4c5be60bf0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545914"
---
# <a name="create-net-standard-and-net-framework-packages-with-visual-studio-2015"></a>Visual Studio 2015 での NET Standard および NET Framework パッケージの作成

**注:** .NET Standard ライブラリを開発するには、Visual Studio 2017 をお勧めします。 Visual Studio 2015 でも動作できますが、.NET Core ツールはプレビュー状態にしかなりません。 NuGet 4.x 以降および Visual Studio 2017 を使用している場合は、[Visual Studio 2017 でのパッケージの作成と公開](../quickstart/create-and-publish-a-package-using-visual-studio.md)に関するページを参照してください。

[.NET Standard ライブラリ](/dotnet/articles/standard/library)は、すべての .NET ランタイムで使用できるようにすることを目的とした .NET API の正式な仕様です。したがって、.NET エコシステムでより高い統一性が確立されます。 .NET Standard Library は、ワークロードに関係なく、すべての .NET プラットフォーム用に統一された BCL (基本クラス ライブラリ) API のセットを定義して実装します。 これにより、開発者はすべての .NET ランタイム間で使用可能なコードを生成できます。また、共有コードでプラットフォーム固有の条件付きコンパイル ディレクティブを除去するまでとはいかないまでも減らすことはできます。

このガイドでは、 .NET Standard Library 1.4 をターゲットとするか、または .NET Framework 4.6 をターゲットとする NuGet パッケージの作成について説明します。 .NET Standard 1.4 ライブラリは、.NET Framework 4.6.1、ユニバーサル Windows プラットフォーム 10、.NET Core、および Mono/Xamarin に適用できます。 詳細については、「[.NET Standard マッピング テーブル](/dotnet/standard/net-standard#net-implementation-support)」 (.NET ドキュメント) を参照してください。 必要な場合は、他のバージョンの .NET Standard ライブラリを選択できます。

## <a name="prerequisites"></a>必須コンポーネント

1. Visual Studio 2015 更新プログラム 3
1. (.NET Standard のみ) [.NET Core SDK](https://www.microsoft.com/net/download/)
1. NuGet CLI。 [nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの nuget.exe をダウンロードして、任意の場所に保存します。 次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。

    > [!Note]
    > nuget.exe はインストーラーではなく CLI ツール自体です。したがって、ブラウザーからダウンロードしたファイルは実行するのではなく、必ず保存してください。

## <a name="create-the-class-library-project"></a>クラス ライブラリ プロジェクトを作成する

1. Visual Studio で、**[ファイル] > [新規] > [プロジェクト]** の順に移動し、**[Visual C#] > [Windows]** ノードの順に展開して **[クラス ライブラリ (ポータブル)]** を選択し、名前を AppLogger に変更してから **[OK]** を選択します。

    ![新しいクラス ライブラリ プロジェクトを作成する](media/NetStandard-NewProject.png)

1. 表示された **[ポータブル クラス ライブラリの追加]** ダイアログ ボックスで、`.NET Framework 4.6` と `ASP.NET Core 1.0` のオプションを選択します。 (.NET Framework をターゲットにしている場合は、どちらか適切なオプションを選択できます。)

1. .NET Standard をターゲットにしている場合、ソリューション エクスプローラーで `AppLogger (Portable)` を右クリックして **[プロパティ]** を選択し、**[ライブラリ]** タブを選択してから **[ターゲット]** セクションの **[ターゲットの .NET Platform Standard]** を選択します。 この動作によって確認を促すメッセージが表示され、以降はドロップ ダウンから `.NET Standard 1.4` (または、使用可能な別のバージョン) を選択できるようになります。

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
                Console.WriteLine(text);
            }
        }
    }
    ```

1. 構成をリリースに設定し、プロジェクトをビルドし、DLL ファイルと XML ファイルが `bin\Release` フォルダー内に生成されていることを確認します。

## <a name="create-and-update-the-nuspec-file"></a>.nuspec ファイルを作成して更新する

1. コマンド プロンプトを開き、(`.sln` ファイルの 1 レベル下の) `AppLogger.csproj` フォルダーを含むフォルダーに移動して NuGet `spec` コマンドを実行し、初期 `AppLogger.nuspec` ファイルを作成します。

    ```cli
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
        <copyright>Copyright 2018 (c) Contoso Corporation. All rights reserved.</copyright>
        <tags>logger logging logs</tags>
        </metadata>
    </package>
    ```

1. 参照アセンブリを `.nuspec` ファイル、つまり、ライブラリの DLL および IntelliSense XML ファイルに追加します。

    .NET Standard をターゲットにしている場合、エントリは以下のように表示されます。

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\netstandard1.4\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\netstandard1.4\AppLogger.xml" />
    </files>
    ```

    .NET Framework をターゲットにしている場合、エントリは以下のように表示されます。

    ```xml
    <!-- Insert below <metadata> element -->
    <files>
        <file src="bin\Release\AppLogger.dll" target="lib\net46\AppLogger.dll" />
        <file src="bin\Release\AppLogger.xml" target="lib\net46\AppLogger.xml" />
    </files>
    ```

1. ソリューションを右クリックし、**[ソリューションのビルド]** を選択してパッケージのすべてのファイルを生成します。

### <a name="declaring-dependencies"></a>依存関係の宣言

他の NuGet パッケージに依存している場合は、マニフェストの `<dependencies>` 要素内で `<group>` 要素を使用して列挙します。 たとえば、NewtonSoft.Json 8.0.3 以降に対する依存関係を宣言するには、以下を追加します。

```xml
<!-- Insert within the <metadata> element -->
<dependencies>
    <group targetFramework="uap">
        <dependency id="Newtonsoft.Json" version="8.0.3" />
    </group>
</dependencies>
```

*version* 属性の構文は、バージョン 8.0.3 以降が許容されることを示します。 別のバージョンの範囲を指定する場合は、「[パッケージのバージョン管理](../reference/package-versioning.md)」を参照してください。

### <a name="adding-a-readme"></a>Readme の追加

`readme.txt` ファイルを作成し、プロジェクト ルート ディレクトリに配置して、`.nuspec` ファイルで参照します。

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

パッケージがプロジェクトにインストールされると、Visual Studio に `readme.txt` が表示されます。 .NET Core プロジェクトにインストールされている場合、または依存関係としてインストールされているパッケージの場合、このファイルは表示されません。

## <a name="package-the-component"></a>コンポーネントをパッケージ化する

パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の `pack` コマンドを実行できます。

```cli
nuget pack AppLogger.nuspec
```

これにより、`AppLogger.YOUR_NAME.1.0.0.nupkg`が生成されます。 [NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツ (.NET Standard に対する表示) が表示されます。

![AppLogger パッケージが表示された NuGet パッケージ エクスプローラー](media/NetStandard-PackageExplorer.png)

> [!Tip]
> `.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。 したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。

パッケージを他の開発者が使用できるようにする場合は、「[パッケージを公開する](../create-packages/publish-a-package.md)」の手順に従ってください。

`pack` には Mac OS X の場合は Mono 4.4.2 が必要であり、Linux 1 システムでは動作しないことに注意してください。 Mac の場合、`.nuspec` ファイルの Windows パス名を Unix 形式のパスに変換する必要もあります。

## <a name="related-topics"></a>関連トピック

- [.nuspec リファレンス](../reference/nuspec.md)
- [複数の .NET Framework バージョンのサポート](../create-packages/supporting-multiple-target-frameworks.md)
- [パッケージに MSBuild プロパティとターゲットを含める](../create-packages/creating-a-package.md#including-msbuild-props-and-targets-in-a-package)
- [ローカライズされたパッケージを作成する](../create-packages/creating-localized-packages.md)
- [シンボル パッケージ](../create-packages/symbol-packages.md)
- [パッケージのバージョン管理](../reference/package-versioning.md)
- [.NET Standard ライブラリのドキュメント](/dotnet/articles/standard/library)
- [.NET Framework から .NET Core への移植](/dotnet/articles/core/porting/index)
