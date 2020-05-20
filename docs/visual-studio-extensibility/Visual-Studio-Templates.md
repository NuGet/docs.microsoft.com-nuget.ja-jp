---
title: Visual Studio テンプレートの NuGet パッケージ
description: NuGet パッケージを Visual Studio プロジェクトと項目テンプレートの一部として含める方法について説明します。
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498248"
---
# <a name="packages-in-visual-studio-templates"></a>Visual Studio テンプレートのパッケージ

Visual Studio プロジェクト テンプレートと項目テンプレートは多くの場合、プロジェクトまたは項目が作成されるときに特定のパッケージがインストールされていることを確認する必要があります。 たとえば、ASP.NET MVC 3 テンプレートは、jQuery、Modernizr、およびその他のパッケージをインストールします。

これをサポートするため、テンプレートの作成者は、NuGet に個々のライブラリではなく、必要なパッケージをインストールするように指示できます。 こうすることで、開発者が後から好きなときにこれらのパッケージを簡単に更新できます。

テンプレートそのものを作成する詳細については、「[方法 : プロジェクト テンプレートを作成する](/visualstudio/ide/how-to-create-project-templates)」または「[Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates)」(カスタムのプロジェクトおよび項目テンプレートを作成する) を参照してください。

このセクションの残りの部分では、NuGet パッケージを正しく含めるテンプレートを作成するときに実行する具体的な手順について説明します。

- [パッケージをテンプレートに追加する](#adding-packages-to-a-template)
- [ベスト プラクティス](#best-practices)

例については、[NuGetInVsTemplates のサンプル](https://bitbucket.org/marcind/nugetinvstemplates)を参照してください。

## <a name="adding-packages-to-a-template"></a>パッケージをテンプレートに追加する

テンプレートがインスタンス化されるときに、インストールするパッケージのリストとともにこれらのパッケージがある場所に関する情報を読み込むため、[テンプレート ウィザード](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)が呼び出されます。 パッケージは、VSIX に埋め込んだり、テンプレートに埋め込むことができます。または、レジストリ キーを使用してファイル パスを参照する場合は、ローカル ハード ドライブ上に配置することもできます。 これらの場所の詳細については、このセクションで後述します。

[テンプレート ウィザード](/visualstudio/extensibility/how-to-use-wizards-with-project-templates)を使用して、プレインストールされたパッケージが機能します。 テンプレートがインスタンス化されるときに、特殊なウィザードが呼び出されます。 このウィザードはインストールする必要があるパッケージのリストを読み込み、その情報を適切な NuGet API に渡します。

テンプレートにパッケージを含める手順:

1. `vstemplate` ファイルに、[`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) 要素を追加して、NuGet テンプレート ウィザードへの参照を追加します。

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` は、`TemplateWizard` クラスのみを含むアセンブリで、`NuGet.VisualStudio.dll` で実際の実装を呼び出す単純なラッパーです。 プロジェクト/項目テンプレートが新しいバージョンの NuGet で引き続き機能するように、アセンブリのバージョンは変わりません。

1. プロジェクトにインストールするパッケージのリストを追加します。

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    複数のパッケージ ソースをサポートするため、ウィザードでは複数の `<package>` 要素がサポートされます。 `id` と `version` の両方の属性が必要です。つまり、新しいバージョンが利用可能な場合でも、パッケージの特定のバージョンがインストールされます。 これによりパッケージの更新によりテンプレートが破損されるのを防ぎ、テンプレートを使用する開発者にパッケージの更新の選択を任せます。

1. 次のセクションで説明するように、NuGet がパッケージを検索するリポジトリを指定します。

### <a name="vsix-package-repository"></a>VSIX パッケージ リポジトリ

Visual Studio プロジェクト/項目テンプレートの推奨される配置方法は、[VSIX 拡張機能](/visualstudio/extensibility/shipping-visual-studio-extensions)です。これを使用すると、複数のプロジェクト/項目テンプレートをまとめてパッケージ化し、開発者が VS 拡張機能マネージャーまたは Visual Studio ギャラリーを使用して、テンプレートを簡単に検出することができるからです。 拡張機能への更新プログラムも、[Visual Studio 拡張機能マネージャーの自動更新メカニズム](/visualstudio/extensibility/how-to-update-a-visual-studio-extension)を使用して簡単に展開できます。

VSIX 自体は、テンプレートで必要となるパッケージのソースとして使用できます。

1. `.vstemplate` ファイルで次のように `<packages>` 要素を変更します。

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    `repository` 属性がリポジトリの種類を `extension` として指定するのに対し、`repositoryId` は VSIX 自体の一意の識別子です (これが、拡張機能の `vsixmanifest` ファイル内の `ID` 属性の値です。「[VSIX 拡張機能スキーマ 2.0 リファレンス](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)」を参照してください)。

1. `nupkg` ファイルを VSIX 内の `Packages` というフォルダー内に配置します。

1. 必要なパッケージ ファイルを `<Asset>` として `vsixmanifest` ファイルに追加します (「[VSIX 拡張機能スキーマ 2.0 リファレンス](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)」を参照してください)。

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. パッケージは、プロジェクト テンプレートと同じ VSIX に配布することも、別の VSIX に配置する (自分のシナリオにとってその方が合理的な場合) こともできます。 ただし、制御できない VSIX を参照しないでください。その拡張機能への変更によりテンプレートが破損する可能性があります。

### <a name="template-package-repository"></a>テンプレート パッケージ リポジトリ

1 つのプロジェクト/項目テンプレートのみを配布して、複数のテンプレートをまとめてパッケージ化する必要がない場合は、プロジェクト/項目テンプレートの ZIP ファイルにパッケージを直接含める、よりシンプルですがより制限された方法を使用できます。

1. `.vstemplate` ファイルで次のように `<packages>` 要素を変更します。

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    `repository` 属性には値 `template` があり、`repositoryId` 属性は必要ありません。

1. プロジェクト/項目テンプレートの ZIP ファイルのルート フォルダーにパッケージを配置します。

複数のテンプレートを含む VSIX でこの方法を使用すると、テンプレートで 1 つ以上のパッケージが共通するときに、不要な肥大化につながることに注意してください。 このような場合、前のセクションで説明したように、[VSIX をリポジトリとして](#vsix-package-repository)使用します。

### <a name="registry-specified-folder-path"></a>レジストリで指定されたフォルダーのパス

MSI を使用してインストールされる SDK は、開発者のマシンに直接 NuGet パッケージをインストールできます。 これにより、プロジェクト テンプレートまたは項目テンプレートを使用するときに、パッケージを抽出することなく、すぐに利用できるようになります。 ASP.NET テンプレートは、この方法を使用します。

1. MSI にパッケージをマシンにインストールさせます。 `.nupkg` ファイルだけをインストールすることも、ファイルと共に展開されたコンテンツをインストールして、テンプレートを使用するときに追加の手順を省略することもできます。 この場合、`.nupkg` ファイルがルート フォルダーにあり、各パッケージが ID/バージョンのペアが名前になったサブフォルダーを持つ、NuGet の標準のフォルダー構造に従います。

1. パッケージの場所を識別するレジストリ キーを記述します。

    - キーの場所: マシン全体の `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository`、またはユーザーごとにインストールされるテンプレートとパッケージの場合は、代わりに `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository` を使用します。
    - キー名: 自分にとって一意の名前を使用します。 たとえば、VS 2012 の ASP.NET MVC 4 テンプレートでは、`AspNetMvc4VS11` を使用します。
    - 値: パッケージ フォルダーへの完全パス。

1. `.vstemplate` ファイル内の `<packages>` 要素に、属性 `repository="registry"` を追加し、`keyName` 属性でレジストリ キーの名前を指定します。

    - 解凍前のパッケージがある場合は、`isPreunzipped="true"` 属性を使用します。
    - *(NuGet 3.2 以降)* パッケージのインストール終了時にデザイン時ビルドを強制する場合は、`forceDesignTimeBuild="true"` 属性を追加します。
    - テンプレート自体には既に必要な参照が含まれているため、最適化として `skipAssemblyReferences="true"` を追加します。

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>ベスト プラクティス

1. NuGet VSIX で依存関係を宣言するため、VSIX マニフェストに依存関係への参照を追加します。

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. `.vstemplate` ファイルに [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) を含めることにより、作成時にプロジェクト/項目テンプレートが保存されるようにする必要があります。

1. テンプレートに、`packages.config` ファイルは含まれません。また、NuGet パッケージがインストールされるときに追加される参照やコンテンツも含まれません。
