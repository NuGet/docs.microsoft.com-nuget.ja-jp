---
title: NuGet を使用して UI コントロールをパッケージ化する方法
description: UWP コントロールまたは WPF コントロールを含む NuGet パッケージを作成する方法について説明します。これには、必要なメタデータと、Visual Studio と Blend デザイナー用のサポート ファイルが含まれます。
author: karann-msft
ms.author: karann
ms.date: 05/23/2018
ms.topic: tutorial
ms.openlocfilehash: dd36987e020c2daa02bb875aa9dbd69c85bba4d3
ms.sourcegitcommit: 1bd72dca2f85b4267b9924236f1d23dd7b0ed733
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/23/2018
ms.locfileid: "49951747"
---
# <a name="creating-ui-controls-as-nuget-packages"></a>NuGet パッケージとして UI コントロールを作成する

Visual Studio 2017 では、NuGet パッケージで配信する UWP コントロールと WPF コントロール用の追加機能を活用できます。 このガイドでは、UWP コントロールのコンテキストから、[ExtensionSDKasNuGetPackage サンプル](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)を使用してこれらの機能を紹介します。 特に言及がない限り、WPF コントロールに対しても同じことが該当します。

## <a name="prerequisites"></a>必須コンポーネント

1. Visual Studio 2017
1. [UWP パッケージの作成](create-uwp-packages.md)方法

## <a name="generate-library-layout"></a>ライブラリ レイアウトの生成

> [!Note]
> これは、UWP コントロールにのみ該当します。

`GenerateLibraryLayout` プロパティを設定すると、nuspec に個別のファイル エントリがなくても、パッケージ化の準備ができているレイアウトでプロジェクト ビルドの出力が生成されます。

プロジェクト プロパティから [ビルド] タブに移動し、[ライブラリ レイアウトの生成] チェック ボックスをオンにします。 これにより、プロジェクト ファイルが変更され、現在選択しているビルド構成とプラットフォームに対して `GenerateLibraryLayout` フラグが true に設定されます。

または、プロジェクト ファイルを編集して、最初の無条件プロパティ グループに `<GenerateLibraryLayout>true</GenerateLibraryLayout>` を追加します。 これにより、ビルド構成とプラットフォームに関係なく、プロパティが適用されます。

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
- *type_full_name_n*: `ManagedPackage.MyCustomControl` など、名前空間を含む、各コントロールの完全修飾名です。 マネージド コードとネイティブの両方の種類でドット形式が使用されることに注意してください。

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

ツールボックス/資産ウィンドウにカスタム アイコンを表示するには、プロジェクトに画像を追加するか、"Namespace.ControlName.extension" という名前の対応する `design.dll` プロジェクトに画像を追加し、ビルド アクションを "埋め込みリソース" に設定します。 また、関連付けられている `AssemblyInfo.cs` によって ProvideMetadata 属性 (`[assembly: ProvideMetadata(typeof(RegisterMetadata))]`) が指定されていることを確認する必要があります。 この[サンプル](https://github.com/NuGet/Samples/blob/master/ExtensionSDKasNuGetPackage/NativePackage.Design/Properties/AssemblyInfo.cs#L20)をご覧ください。

利用できる形式は `.png`、`.jpg`、`.jpeg`、`.gif`、`.bmp` です。 推奨されるイメージ サイズは 64 × 64 ピクセルです。

次の例では、プロジェクトには、"ManagedPackage.MyCustomControl.png" という名前の画像ファイルが含まれています。

![プロジェクトでカスタム アイコンを設定する](media/UWP-control-custom-icon.png)

> [!Note]
> ネイティブ コントロールの場合は、`design.dll` プロジェクトでリソースとしてアイコンを配置する必要があります。

## <a name="support-specific-windows-platform-versions"></a>特定の Windows プラットフォーム バージョンをサポートする

UWP パッケージに含まれる TargetPlatformVersion (TPV) と TargetPlatformMinVersion (TPMinV) は、アプリケーションをインストールできる OS バージョンの上限と下限の境界を定義します。 TPV ではさらに、アプリがビルドされる SDK のバージョンを指定します。 UWP パッケージを作成するときにこれらのプロパティを考慮してください。アプリで定義されているプラットフォームのバージョンの範囲外の API を使用すると、ビルドが失敗したり、実行時にアプリが失敗したりします。

たとえば、コントロール パッケージの TPMinV を Windows 10 Anniversary Edition (10.0、ビルド 14393) に設定し、その下限に一致する UWP プロジェクトによってのみパッケージが使用されるようにしたとします。 UWP プロジェクトでパッケージを使用できるようにするには、次のフォルダー名を使用してコントロールをパッケージ化する必要があります。

    \lib\uap10.0.14393\*
    \ref\uap10.0.14393\*

NuGet では、使用するプロジェクトの TPMinV が自動的にチェックされ、Windows 10 Anniversary Edition (10.0、ビルド 14393) よりも低かった場合はインストールが失敗します。

WPF の場合、たとえば、.NET Framework v4.6.1 以上をターゲットとするプロジェクトにのみ WPF コントロールのパッケージが使用されるようにするとします。 これを強制するには、次のフォルダー名を使用してコントロールをパッケージ化する必要があります。

    \lib\net461\*
    \ref\net461\*

## <a name="add-design-time-support"></a>デザイン時サポートの追加

プロパティ インスペクターのどこにコントロールのプロパティが表示されるかを構成するには、カスタム装飾などを追加し、ターゲット プラットフォームに合わせて `design.dll` ファイルを `lib\uap10.0.14393\Design` フォルダー内に配置します。 また、**[[テンプレートの編集] > [コピーして編集]](/windows/uwp/controls-and-patterns/xaml-styles#modify-the-default-system-styles)** 機能を確実に動作させるには、マージする `Generic.xaml` とリソース ディクショナリを `<your_assembly_name>\Themes` フォルダーに含める必要があります (ここでも実際のアセンブリ名を使用します)。 (このファイルはコントロールの実行時の動作には影響しません)。その結果、フォルダー構造は次のようになります。

    \lib
      \uap10.0.14393
        \Design
          \MyControl.design.dll
        \your_assembly_name
          \Themes
            Generic.xaml


WPF の場合は、WPF コントロールのパッケージが .NET Framework v4.6.1 以上をターゲットとするプロジェクトによって使用される例で続行します。

    \lib
      \net461
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

> [!Note]
> これは、UWP コントロールにのみ該当します。

## <a name="see-also"></a>関連項目

- [UWP パッケージの作成](create-uwp-packages.md)
- [ExtensionSDKasNuGetPackage サンプル](https://github.com/NuGet/Samples/tree/master/ExtensionSDKasNuGetPackage)
