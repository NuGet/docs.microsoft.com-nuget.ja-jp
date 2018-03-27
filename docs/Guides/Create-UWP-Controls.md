---
title: "NuGet を使って UWP をパッケージ化する方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/14/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "必要なメタデータと、Visual Studio と Blend デザイナーのサポート ファイルが含まれている UWP コントロールが含まれている NuGet パッケージを作成する方法を説明します。"
keywords: "NuGet UWP コントロール、Visual Studio XAML デザイナー、Blend デザイナー、カスタム コントロール"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 1af5118eb71836d8b8bcfa8ff713d9fef3c86374
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="creating-uwp-controls-as-nuget-packages"></a>NuGet パッケージとして UWP コントロールを作成する

Visual Studio 2017 では、NuGet パッケージで配信する UWP コントロールの追加機能を活用することができます。 このガイドでは、[ExtensionSDKasNuGetPackage サンプル](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)を使用してこれらの機能を紹介します。 

## <a name="prerequisites"></a>必須コンポーネント

1. Visual Studio 2017
1. [UWP パッケージの作成](create-uwp-packages.md)方法

## <a name="add-toolboxassets-pane-support-for-xaml-controls"></a>XAML コントロールのツールボックス/資産ウィンドウのサポートを追加する

XAML コントロールが Visual Studio の XAML デザイナーのツールボックスと Blend の [資産] ウィンドウに表示されるようにするには、パッケージ プロジェクトの `tools` フォルダーのルートに `VisualStudioToolsManifest.xml` ファイルを作成します。 このファイルは、ツールボックスまたは [資産] ウィンドウにコントロールを表示する必要がない場合は必要ありません。

    \build
    \lib
    \tools
        VisualStudioToolsManifest.xml

ファイルの構造は、次のとおりです。

```xml
<FileList>
  <File Reference = "your_package_file">
    <ToolboxItems VSCategory="vs_category" BlendCategory="blend_category">
      <Item Type="type_full_name_1" />

      <!-- Any number of additional Items -->
      <Item Type="type_full_name_2" />
      <Item Type="type_full_name_3" />
    </ToolboxItems>
  </File>
</FileList>
```

それぞれの文字について以下に説明します。

- *your_package_file*: `ManagedPackage.winmd` などのコントロール ファイルの名前 ("ManagedPackage" はこの例で任意の名前を使用するだけで、それ以外の意味を持ちません)。
- *vs_category*: Visual Studio デザイナーのツールボックスにコントロールを表示するグループのラベル。 `VSCategory` は、コントロールをツールボックスに表示するために必要です。
- *blend_category*: Blend デザイナーの [資産] ウィンドウにコントロールを表示するグループのラベル。 `BlendCategory` は、コントロールを [資産] に表示するために必要です。
- *type_full_name_n*: `ManagedPackage.MyCustomControl` など、名前空間を含む、各コントロールの完全修飾名です。 マネージ コードとネイティブの両方の種類でドット形式が使用されることに注意してください。

より高度なシナリオでは、1 つのパッケージに複数のコントロール アセンブリが含まれているときに、複数の `<File>` 要素を `<FileList>` に含めることもできます。 コントロールをカテゴリ別に整理する場合は、複数 `<ToolboxItems>` ノードを 1 つの `<File>` 内に含めることもできます。

次の例では、`ManagedPackage.winmd` 内に実装されたコントロールが、Visual Studio と Blend で “Managed Package” という名前のグループに表示され、そのグループに “MyCustomControl” が表示されます。 これらのすべての名前は任意です。

```xml
<FileList>
  <File Reference = "ManagedPackage.winmd">
    <ToolboxItems VSCategory="Managed Package" BlendCategory="Managed Package">
      <Item Type="ManagedPackage.MyCustomControl" />
    </ToolboxItems>
  </File>
</FileList>
```

![Visual Studio で表示されるコントロールの例](media/UWP-control-vs-toolbox.png)

![Blend で表示されるコントロールの例](media/UWP-control-blend-assets.png)

> [!Note]
> ツールボックス/資産ウィンドウに表示するには、すべてのコントロールを明示的に指定する必要があります。 `Namespace.ControlName` 形式で指定したことを確認してください。

## <a name="add-custom-icons-to-your-controls"></a>コントロールにカスタム アイコンを追加する

ツールボックス/資産ウィンドウにカスタム アイコンを表示するには、プロジェクトに画像を追加するか、"Namespace.ControlName.extension" という名前の対応する `design.dll` プロジェクトに画像を追加し、ビルド アクションを "埋め込みリソース" に設定します。 利用できる形式は `.png`、`.jpg`、`.jpeg`、`.gif`、`.bmp` です。 推奨されるイメージ サイズは 64 × 64 ピクセルです。

次の例では、プロジェクトには、"ManagedPackage.MyCustomControl.png" という名前の画像ファイルが含まれています。

![プロジェクトでカスタム アイコンを設定する](media/UWP-control-custom-icon.png)

> [!Note]
> ネイティブ コントロールの場合は、`design.dll` プロジェクトでリソースとしてアイコンを配置する必要があります。

## <a name="support-specific-windows-platform-versions"></a>特定の Windows プラットフォーム バージョンをサポートする

UWP パッケージに含まれる TargetPlatformVersion (TPV) と TargetPlatformMinVersion (TPMinV) は、アプリケーションをインストールできる OS バージョンの上限と下限の境界を定義します。 TPV ではさらに、アプリがビルドされる SDK のバージョンを指定します。 UWP パッケージを作成するときにこれらのプロパティを考慮してください。アプリで定義されているプラットフォームのバージョンの範囲外の API を使用すると、ビルドが失敗したり、実行時にアプリが失敗したりします。

たとえば、コントロール パッケージの TPMinV を Windows 10 Anniversary Edition (10.0、ビルド 14393) に設定し、その下限に一致する UWP プロジェクトによってのみパッケージが使用されるようにしたとします。 UWP プロジェクトでパッケージを使用できるようにするには、次のフォルダー名を使用してコントロールをパッケージ化する必要があります。

    \lib\uap10.0\*
    \ref\uap10.0\*

適切な TPMinV チェックを適用するには、[MSBuild ターゲット ファイル](/visualstudio/msbuild/msbuild-targets)を作成し、`build\uap10.0" folder as `<your_assembly_name>.targets 以下でパッケージ化します (<your_assembly_name>' は特定のアセンブリの名前に置き換えます)。

ターゲット ファイルがどのように表示されるかの例を次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">

  <Target Name="TPMinVCheck" BeforeTargets="ResolveAssemblyReferences" Condition="'$(TargetPlatformMinVersion)' != ''">
    <PropertyGroup>
      <RequiredTPMinV>10.0.14393</RequiredTPMinV>
      <ActualTPMinV>$(TargetPlatformMinVersion)</ActualTPMinV>
    </PropertyGroup>
    <Error Condition=" '$([System.Version]::Parse($(ActualTPMinV)).CompareTo($([System.Version]::Parse($(RequiredTPMinV)))))' == '-1' "        Text = "The INSERT_PACKAGE_ID_HERE nuget package cannot be used in the $(MSBuildProjectName) project since the project's TargetPlatformMinVersion - $(ActualTPMinV) does not match the Minimum Version - $(RequiredTPMinV) supported by the package" />
  </Target>
</Project>
```

## <a name="add-design-time-support"></a>デザイン時サポートの追加

プロパティ インスペクターのどこにコントロールのプロパティが表示されるかを構成するには、カスタム装飾などを追加し、ターゲット プラットフォームに合わせて `design.dll` ファイルを `lib\uap10.0\Design` フォルダー内に配置します。 また、**[[テンプレートの編集] > [コピーして編集]](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** 機能を確実に動作させるには、マージする `Generic.xaml` とリソース ディクショナリを `<your_assembly_name>\Themes` フォルダーに含める必要があります (ここでも実際のアセンブリ名を使用します)。 (このファイルはコントロールの実行時の動作には影響しません)。その結果、フォルダー構造は次のようになります。

    \lib
      \uap10.0
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml

> [!Note]
> 既定では、コントロールのプロパティは、プロパティ インスペクターの [その他] カテゴリの下に表示されます。

## <a name="use-strings-and-resources"></a>文字列とリソースの使用

文字列リソース (`.resw`) をパッケージに埋め込み、コントロールまたは使用中の UWP プロジェクトでそれを使用して、`.resw` ファイルの **[ビルド アクション]** プロパティを **PRIResource** に設定することができます。

たとえば、ExtensionSDKasNuGetPackage サンプルの [MyCustomControl.cs](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/ManagedPackage/MyCustomControl.cs) を参照してください。

## <a name="package-content-such-as-images"></a>画像などのパッケージの内容

コントロールまたは使用中の UWP プロジェクトで使用できる画像などのコンテンツをパッケージ化するには、対象のファイルを `lib\uap10.0` フォルダー内に配置します。

[MSBuild ターゲット ファイル](/visualstudio/msbuild/msbuild-targets)を作成して、資産が使用するプロジェクトの出力フォルダーにコピーされるようにすることもできます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<Project xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
    <ItemGroup Condition="'$(TargetPlatformIdentifier)' == 'UAP'">
        <Content Include="$(MSBuildThisFileDirectory)..\..\lib\uap10.0\contosoSampleImage.jpg">
            <CopyToOutputDirectory>Always</CopyToOutputDirectory>
        </Content>
    </ItemGroup>
</Project>
```

## <a name="see-also"></a>関連項目

- [UWP パッケージの作成](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage サンプル](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
