---
title: ユニバーサル Windows プラットフォーム用の NuGet パッケージの作成
description: C# でユニバーサル Windows プラットフォーム用の Windows ランタイム コンポーネントを使用して NuGet パッケージを作成するためのエンド ツー エンド チュートリアル。
author: rrelyea
ms.author: rrelyea
ms.date: 02/28/2020
ms.topic: tutorial
ms.openlocfilehash: 61f46f2623769927f881877cfe3f96132211b442
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231753"
---
# <a name="create-uwp-packages-c"></a>UWP パッケージの作成 (C#)

[ユニバーサル Windows プラットフォーム (UWP)](/windows/uwp) は、Windows 10 を実行するすべてのデバイスに共通のアプリ プラットフォームを提供します。 このモデル内では、UWP アプリはすべてのデバイスに共通の WinRT API と、アプリが実行されるデバイス ファミリに固有の API (Win32 と .NET を含む) の両方を呼び出すことができます。

このチュートリアルでは、マネージド プロジェクトとネイティブ プロジェクトの両方で使用できる C# UWP コンポーネント (XAML コントロールを含む) で NuGet パッケージを作成します。

## <a name="prerequisites"></a>必須コンポーネント

1. Visual Studio 2019。 [visualstudio.com](https://www.visualstudio.com/) から無料の 2019 Community Edition をインストールします。Professional Edition と Enterprise Edition を使用することもできます。

1. NuGet CLI。 [nuget.org/downloads](https://nuget.org/downloads) から最新バージョンの `nuget.exe` をダウンロードして、任意の場所に保存します (`.exe`を直接ダウンロードします)。 次に、その場所を PATH 環境変数に追加します (まだ存在していない場合)。 詳細については、[こちら](/nuget/reference/nuget-exe-cli-reference#windows)を参照してください。

## <a name="create-a-uwp-windows-runtime-component"></a>UWP Windows ランタイム コンポーネントを作成する

1. Visual Studio で、 **[ファイル]、[新規]、[プロジェクト]** の順に選択し、"uwp c#" を検索し、 **[Windows ランタイム コンポーネント (ユニバーサル Windows)]** テンプレートを選択し、[次へ] をクリックして、名前を ImageEnhancer に変更して [作成] をクリックします。 プロンプトが表示されたら、ターゲット バージョンと最小バージョンの既定値を受け入れます。

    ![新しい UWP Windows ランタイム コンポーネント プロジェクトの作成](media/UWP-NewProject-CS.png)

1. ソリューション エクスプローラーでプロジェクトを右クリックし、 **[追加]、[新しい項目]** の順に選択し、 **[テンプレート コントロール]** を選択して、名前を AwesomeImageControl.cs に変更してから **[追加]** をクリックします。

    ![プロジェクトへの新しい XAML テンプレート コントロール項目の追加](media/UWP-NewXAMLControl-CS.png)

1. ソリューション エクスプローラーでプロジェクトを右クリックして、 **[プロパティ]** を選択します。 [プロパティ] ページで、 **[ビルド]** タブを選択し、 **[XML ドキュメント ファイル]** を有効にします。

    ![[XML ドキュメント ファイルの生成] を [はい] に設定する](media/UWP-GenerateXMLDocFiles-CS.png)

1. ここで*ソリューション*を右クリックし、 **[バッチ ビルド]** を選択して、以下に示すようにダイアログの 5 つのビルド ボックスをオンにします。 これで、ビルドの実行時に、Windows でサポートされるターゲット システムごとに完全な成果物セットが生成されるようになります。

    ![[バッチ ビルド]](media/UWP-BatchBuild-CS.png)

1. [バッチ ビルド] ダイアログで、 **[ビルド]** をクリックしてプロジェクトを検証し、NuGet パッケージで必要になる出力ファイルを作成します。

> [!Note]
> このチュートリアルでは、パッケージのデバッグ成果物を使用します。 非デバッグ パッケージの場合は、代わりに [バッチ ビルド] ダイアログでリリース オプションをオンにして、以下の手順で結果として得られる Release フォルダーを参照します。

## <a name="create-and-update-the-nuspec-file"></a>.nuspec ファイルを作成して更新する

初期 `.nuspec` ファイルを作成するには、次の 3 つの手順を実行します。 次のセクションでは、他の必要な更新について説明します。

1. コマンド プロンプトを開き、`ImageEnhancer.csproj` (これは、ソリューション ファイルの下のサブフォルダーになります) を含むフォルダーに移動します。
1. [`NuGet spec`](/nuget/reference/cli-reference/cli-ref-spec) コマンドを実行して、`ImageEnhancer.nuspec` (ファイルの名前は `.csroj` ファイルの名前から取得されます) を生成します。

    ```cli
    nuget spec
    ```

1. `ImageEnhancer.nuspec` をエディターで開き、以下の内容と一致するように更新して、YOUR_NAME を適切な値に置き換えます。 $propertyName$ 値が残らないようにします。 具体的には、`<id>` 値を nuget.org で固有のものにする必要があります (「[パッケージの作成](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)」で説明されている名前付け規則に関する記述を参照)。 また、作成者と説明のタグを更新する必要があることに注意してください。そうしないと、パッキングの手順でエラーが発生します。

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
> 公開用にビルドされたパッケージの場合は、`<tags>` 要素に特に注意してください。これらのタグは他のユーザーがパッケージを検索して、パッケージの動作を理解するのに役立ちます。

### <a name="adding-windows-metadata-to-the-package"></a>パッケージへの Windows メタデータの追加

Windows ランタイム コンポーネントには、一般公開されるすべての型を記述するメタデータが必要になります。このメタデータにより、他のアプリとライブラリでコンポーネントを使用できるようになります。 このメタデータは .winmd ファイルに含まれています。このファイルは、プロジェクトのコンパイル時に作成され、NuGet パッケージに含める必要があります。 IntelliSense データを含む XML ファイルも同時にビルドされ、同様に含める必要があります。

次の `<files>` コードを `.nuspec` ファイルに追加します。

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

### <a name="adding-xaml-content"></a>XAML コンテンツの追加

コンポーネントに XAML コントロールを含めるには、コントロールの既定のテンプレートを持つ XAML ファイルを追加する必要があります (プロジェクト テンプレートによって生成される)。 この場合、`<files>` セクションは次のようになります。

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

### <a name="adding-the-native-implementation-libraries"></a>ネイティブ実装ライブラリの追加

コンポーネント内では、ImageEnhancer 型のコア ロジックがネイティブ コードに存在します。これは、ターゲット ランタイム (ARM、ARM64、x86、および x64) ごとに生成されるさまざまな `ImageEnhancer.winmd` アセンブリに含まれます。 これらをパッケージに含める場合は、次のように、関連付けられている .pri リソース ファイルと共に `<files>` セクションで参照します。

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

### <a name="final-nuspec"></a>最終的な .nuspec

最終的な `.nuspec` ファイルは次のようになります。ここでも、YOUR_NAME は適切な値に置き換える必要があります。

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

## <a name="package-the-component"></a>コンポーネントをパッケージ化する

パッケージに含める必要があるすべてのファイルを参照する `.nuspec` が完成したら、以下の [`nuget pack`](/nuget/reference/cli-reference/cli-ref-pack) コマンドを実行できます。

```cli
nuget pack ImageEnhancer.nuspec
```

これにより、`ImageEnhancer.YOUR_NAME.1.0.0.nupkg`が生成されます。 [NuGet パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)などのツールでこのファイルを開き、すべてのノードを展開すると、以下のコンテンツが表示されます。

![ImageEnhancer パッケージが表示された NuGet パッケージ エクスプローラー](media/UWP-PackageExplorer.png)

> [!Tip]
> `.nupkg` ファイルは、異なる拡張子が付いた単なる .zip ファイルです。 したがって、`.nupkg` を `.zip` に変えてパッケージの内容を調べることもできますが、パッケージを nuget.org にアップロードする前に必ず、拡張子を復元してください。

パッケージを他の開発者が使用できるようにする場合は、「[パッケージの公開](../nuget-org/publish-a-package.md)」の手順に従ってください。

## <a name="related-topics"></a>関連トピック

- [.nuspec 参照](../reference/nuspec.md)
- [シンボル パッケージ](../create-packages/symbol-packages-snupkg.md)
- [パッケージのバージョン管理](../concepts/package-versioning.md)
- [複数の .NET Framework バージョンのサポート](../create-packages/supporting-multiple-target-frameworks.md)
- [パッケージに MSBuild プロパティとターゲットを含める](../create-packages/creating-a-package.md#include-msbuild-props-and-targets-in-a-package)
- [ローカライズされたパッケージを作成する](../create-packages/creating-localized-packages.md)
