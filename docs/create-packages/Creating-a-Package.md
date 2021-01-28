---
title: nuget.exe CLI を使用して NuGet パッケージを作成する
description: ファイルやバージョン管理など、NuGet パッケージの設計と作成に関する詳細なガイド。
author: JonDouglas
ms.author: feaguila
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: ebaa14325e477c7d864f5c5e88d99f467194e62c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774713"
---
# <a name="create-a-package-using-the-nugetexe-cli"></a>nuget.exe CLI を使用してパッケージを作成する

パッケージの動作やそれに含まれているコードに関係なく、CLI ツールのいずれか (`nuget.exe` または `dotnet.exe`) を使用して、他の開発者が何人でも共有して使用できるコンポーネントにその機能をパッケージ化できます。 NuGet CLI ツールをインストールするには、「[NuGet クライアント ツールのインストール](../install-nuget-client-tools.md)」をご覧ください。 Visual Studio に CLI ツールが自動的に含まれることはないことにご注意ください。

- 非 SDK スタイルのプロジェクト (通常は .NET Framework プロジェクト) の場合は、この記事で説明されている手順に従ってパッケージを作成してください。 Visual Studio と `nuget.exe` CLI を使用した詳細な手順については、「[.NET Framework パッケージの作成と公開](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)」を参照してください。

- [SDK スタイルの形式](../resources/check-project-format.md)を使用する .NET Core および .NET Standard プロジェクト、またその他の SDK スタイルのあらゆるプロジェクトについては、「[Create a NuGet package using the dotnet CLI (dotnet CLI を使用して NuGet パッケージを作成する)](creating-a-package-dotnet-cli.md)」を参照してください。

- `packages.config` から [PackageReference](../consume-packages/package-references-in-project-files.md) に移行されたプロジェクトの場合は、[msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration) をご使用ください。

技術的には、NuGet パッケージは `.nupkg` 拡張子で名前が変更された ZIP ファイルに過ぎません。コンテンツは特定の規則に一致します。 このトピックでは、そのような規則に一致するパッケージの作成過程について説明します。

パッケージ化は、コンパイルされたコード (アセンブリ)、シンボル、パッケージとして届けるその他のファイルで始まります (「[Overview and workflow](overview-and-workflow.md)」 (概要とワークフロー) を参照してください)。 このプロセスは、パッケージに入るファイルのコンパイル (またはコンパイル以外の方法による生成) とは関係ありません。ただし、パッケージ ファイルの情報を引き出し、コンパイル済みアセンブリとパッケージの同期を維持することはできます。

> [!Important]
> このトピックは、非 SDK スタイルのプロジェクト、つまり通常は、Visual Studio 2017 以降のバージョンと NuGet 4.0 以降を使った .NET Core および .NET Standard プロジェクト以外のプロジェクトを対象としています。

## <a name="decide-which-assemblies-to-package"></a>パッケージ化するアセンブリを決定する

ほとんどの汎用パッケージには、他の開発者が自分のプロジェクトで使用できるアセンブリが 1 つまたは複数含まれています。

- 一般的に、各アセンブリが他に依存せずに有用であれば、NuGet パッケージあたりアセンブリを 1 つにすることが最善です。 たとえば、`Utilities.dll` が `Parser.dll` に依存し、`Parser.dll` がそれ自体で有用であれば、それぞれに 1 つパッケージを作成します。 それにより、開発者は `Utilities.dll` に依存せず `Parser.dll` を使用できます。

- 非依存では有用でない複数のアセンブリからライブラリが構成される場合、それらを組み合わせて 1 つのパッケージを作成できます。 前の例を使えば、`Utilities.dll` でのみ使用されるコードが `Parser.dll` に含まれる場合、同じパッケージで `Parser.dll` を維持できます。

- 同様に、`Utilities.dll` が `Utilities.resources.dll` に依存し、後者がそれ自体で有用ではない場合、両方を同じパッケージに入れます。

リソースは、実際には特殊なケースです。 プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、`.resources.dll` という名前のものは、ローカライズされたサテライト アセンブリであるため *除外* されます (「[ローカライズされたパッケージを作成する](creating-localized-packages.md)」を参照してください)。 そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。

ライブラリに COM 相互運用アセンブリが含まれる場合は、[COM 相互運用アセンブリを含むパッケージの作成](author-packages-with-com-interop-assemblies.md)に関するページに記載されている追加ガイドラインに従ってください。

## <a name="the-role-and-structure-of-the-nuspec-file"></a>.nuspec ファイルのロールと構造

パッケージ化するファイルがわかったら、次の手順は、`.nuspec` XML ファイルでパッケージ マニフェストを作成することです。

マニフェスト:

1. パッケージの内容を説明し、それ自体、パッケージに含まれます。
1. パッケージの作成を推進し、パッケージをプロジェクトにインストールする方法を NuGet に指示します。 たとえば、マニフェストは他の依存関係を特定します。それにより、NuGet はメイン パッケージのインストール時にそのような依存関係もインストールできます。
1. 下の説明のように、必須プロパティと任意プロパティの両方が含まれます。 ここにはない他のプロパティなど、詳しくは、[.nuspec リファレンス](../reference/nuspec.md)をご覧ください。

必須プロパティ:

- パッケージの識別子。パッケージをホストするギャラリー全体で一意にする必要があります。
- *Major.Minor.Patch[-Suffix]* という形式の特別なバージョン番号。 *-Suffix* で [プレリリース版](prerelease-packages.md)を識別します。
- ホスト (nuget.org など) に表示されるパッケージ タイトル。
- 作成者と所有者の情報。
- パッケージの詳しい説明。

共通の任意プロパティ:

- リリース ノート
- 著作権情報
- [Visual Studio のパッケージ マネージャー UI](../consume-packages/install-use-packages-visual-studio.md) の簡単な説明。
- ロケール ID
- [プロジェクトの URL]
- 式またはファイルとしてライセンス (`licenseUrl` は非推奨なので、[`license` nuspec メタデータ要素](../reference/nuspec.md#license)を代わりに使用してください)
- アイコン ファイル (`iconUrl` は非推奨なので、[`icon` nuspec メタデータ要素](../reference/nuspec.md#icon)を代わりに使用してください)
- 依存関係と参照の一覧
- ギャラリー検索で役立つタグ

次は典型的な `.nuspec` ファイルです (ただし、架空のものです)。プロパティを説明するコメントが付いています。

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- Package version number that is used when resolving dependencies -->
        <version>1.8.3</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>
        
         <!-- Project URL provides a link for the gallery -->
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

         <!-- License information is displayed on the gallery -->
        <license type="expression">Apache-2.0</license>
        

        <!-- Icon is used in Visual Studio's package manager UI -->
        <icon>icon.png</icon>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
        <file src="icon.png" target="" />
    </files>
</package>
```

依存関係の宣言とバージョン番号の指定の詳細については、「[packages.config 参照](../reference/packages-config.md)」と「[パッケージのバージョン管理](../concepts/package-versioning.md)」を参照してください。 パッケージで直接、依存関係からアセットを表面化させることもできます。`dependency` 要素で `include` 属性と `exclude` 属性を使用します。 [.nuspec リファレンスの依存関係](../reference/nuspec.md#dependencies)をご覧ください。

マニフェストはそれから作成されたパッケージに含まれるため、既存のパッケージを調べることで追加の例をいくつも見つけることができます。 探す場所としては、コンピューターの "*グローバル パッケージ*" フォルダーが適しています。この場所は次のコマンドで返されます。

```cli
nuget locals -list global-packages
```

*package\version* フォルダーに進み、`.nupkg` ファイルを `.zip` ファイルにコピーし、その `.zip` ファイルを開き、その中の `.nuspec` を調べます。

> [!Note]
> Visual Studio プロジェクトから `.nuspec` を作成すると、マニフェストに含まれるトークンは、パッケージのビルド時、プロジェクトからの情報で置換されます。 「[Visual Studio プロジェクトから .nuspec を作成する](#from-a-visual-studio-project)」を参照してください。

## <a name="create-the-nuspec-file"></a>.nuspec ファイルの作成

完全なマニフェストの作成は、一般的に、次のいずれかの方法で生成された基本 `.nuspec` ファイルで始まります。

- [規則ベースの作業ディレクトリ](#from-a-convention-based-working-directory)
- [アセンブリ DLL](#from-an-assembly-dll)
- [Visual Studio プロジェクト](#from-a-visual-studio-project)    
- [新しいファイルと既定値](#new-file-with-default-values)

最終パッケージの厳密な内容が説明されるように、ファイルを手作業で編集します。

> [!Important]
> 生成された `.nuspec` ファイルに含まれるプレースホルダーは、`nuget pack` コマンドでパッケージを作成する前に変更する必要があります。 `.nuspec` にプレースホルダーが含まれる場合、このコマンドは失敗します。

### <a name="from-a-convention-based-working-directory"></a>規則ベースの作業ディレクトリから

NuGet パッケージは `.nupkg` 拡張子で名前が変更されている ZIP ファイルに過ぎないため、多くの場合、ローカルのファイル システムに必要なフォルダー構造を作り、その構造から `.nuspec` ファイルを直接作成するのが最も簡単です。 `nuget pack` コマンドはその後、そのフォルダー構造にすべてのファイルを自動的に追加します。ただし、`.` で始まるフォルダーを除きます。同じ構造にプライベート ファイルを維持できます。

この手法の長所は、パッケージに含めるファイルをマニフェストに指定する必要がないことです (このトピックの後半で説明します)。 パッケージに入るまさにそのフォルダー構造をビルド プロセスで生成させることができます。また、その他の方法ではプロジェクトに含まれないことがある他のファイルを簡単に含めることができます。

- ターゲット プロジェクトに挿入する必要があるコンテンツとソース コード。
- Powershell スクリプト
- プロジェクトの既存の構成とソース コード ファイルへの変換。

フォルダー規則は次のとおりです。

| フォルダー | 説明 | パッケージ インストール時のアクション |
| --- | --- | --- |
| (ルート) | ReadMe.txt の場所 | Visual Studio では、パッケージのインストール時に ReadMe.txt ファイルが表示されます。 |
| lib/{tfm} | 指定されたターゲット フレームワーク モニカー (TFM) のアセンブリ (`.dll`)、ドキュメント (`.xml`)、シンボル (`.pdb`) | アセンブリはランタイムに加えてコンパイル時にも参照として追加されます。`.xml` と `.pdb` はプロジェクト フォルダーにコピーされます。 フレームワーク ターゲット固有のサブフォルダーを作成するには、「[複数のターゲット フレームワークのサポート](supporting-multiple-target-frameworks.md)」を参照してください。 |
| ref/{tfm} | 指定したターゲット フレームワーク モニカー (TFM) のアセンブリ (`.dll`) およびシンボル (`.pdb`) ファイル | アセンブリはコンパイル時にのみ参照として追加されます。したがって、プロジェクトの bin フォルダーには何もコピーされません。 |
| runtimes | アーキテクチャ固有のアセンブリ (`.dll`)、シンボル (`.pdb`)、ネイティブ リソース (`.pri`) ファイル | アセンブリはランタイムでのみ参照として追加されます。その他のファイルはプロジェクト フォルダーにコピーされます。 対応するコンパイル時のアセンブリを指定するために、対応する (TFM) `AnyCPU` 固有のアセンブリが常に `/ref/{tfm}` フォルダーの下にあります。 「[複数のターゲット フレームワークのサポート](supporting-multiple-target-frameworks.md)」を参照してください。 |
| content | 任意のファイル | コンテンツはプロジェクト ルートにコピーされます。 **コンテンツ** フォルダーは最終的にパッケージを使用するターゲット アプリケーションのルートであると考えてください。 パッケージでアプリケーションの */images* フォルダーに画像が追加されるようにするには、パッケージの *content/images* フォルダーにそれを置きます。 |
| build | *(3.x+)* MSBuild の `.targets` ファイルと `.props` ファイル | プロジェクトに自動的に挿入されます。 |
| buildMultiTargeting | *(4.0+)* MSBuild の `.targets` ファイルと `.props` ファイル (フレームワーク間でのターゲット設定用) | プロジェクトに自動的に挿入されます。 |
| buildTransitive | *(5.0 以降)* 任意の使用するフォルダーに推移的にフローする MSBuild の `.targets` および `.props` ファイル。 [機能](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)に関するページをご覧ください。 | プロジェクトに自動的に挿入されます。 |
| tools | Powershell のスクリプトとプログラムにはパッケージ マネージャー コンソールからアクセスできます。 | `tools` フォルダーはパッケージ マネージャー コンソールだけの `PATH` 環境変数に追加されます (厳密に言うと、プロジェクトのビルド時に MSBuild に設定される `PATH` にでは *ありません*)。 |

フォルダー構造には、任意の数のターゲット フレームワークに対して任意の数のアセンブリを含めることができるため、複数のフレームワークをサポートするパッケージの作成時、この方法は必須となります。

いずれの場合でも、必要なフォルダー構造を配置したら、そのフォルダーで次のコマンドを実行し、`.nuspec` ファイルを作成します。

```cli
nuget spec
```

繰り返しになりますが、生成された `.nuspec` には、フォルダー構造のファイルに対する明示的な参照が含まれません。 NuGet は、パッケージが作成されるとき、すべてのファイルを自動的に含めます。 ただし、マニフェストのその他の部分でプレースホルダー値を編集する必要があります。

### <a name="from-an-assembly-dll"></a>アセンブリ DLL から

単純にアセンブリからパッケージを作成する場合、次のコマンドを使用し、アセンブリでメタデータから `.nuspec` ファイルを生成できます。

```cli
nuget spec <assembly-name>.dll
```

このフォームを使用すると、マニフェストのいくつかのプレースホルダーがアセンブリからの具体的な値で置換されます。 たとえば、`<id>` プロパティはアセンブリ名に設定され、`<version>` はアセンブリ バージョンに設定されます。 しかしながら、マニフェストの他のプロパティには、アセンブリのそれに該当する値が与えられず、引き続きプレースホルダーが含まれます。

### <a name="from-a-visual-studio-project"></a>Visual Studio プロジェクトから

`.csproj` または `.vbproj` ファイルから `.nuspec` を作成する方法が便利です。これらのプロジェクトにインストールされているその他のパッケージが依存関係として自動的に参照されるためです。 プロジェクト ファイルと同じフォルダーで次のコマンドを使用します。

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

結果的に生成される `<project-name>.nuspec` ファイルには、パッケージ化のときにプロジェクトからの値で置換される *トークン* が含まれます。他のパッケージが既にインストールされている場合、その参照が含まれます。

*.nuspec* にパッケージの依存関係を含める場合は、代わりに `nuget pack` を使い、生成された *.nupkg* ファイル内から *.nuspec* ファイルを取得します。 たとえば、次のコマンドを使用します。

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget pack myproject.csproj
```

トークンは、プロジェクト プロパティの両側で `$` 記号によって区切られます。 たとえば、この方法で生成されるマニフェストの `<id>` 値は通常、次のように表示されます。

```xml
<id>$id$</id>
```

このトークンは、パッケージ化のとき、プロジェクト ファイルからの `AssemblyName` 値で置換されます。 プロジェクト値と `.nuspec` トークンのマッピングについては、[置換トークンの参照に関するトピック](../reference/nuspec.md#replacement-tokens)を参照してください。

トークンを利用することで、プロジェクトを更新するとき、`.nuspec` のバージョン番号などの重要な値を自分で更新する必要がなくなります。 (必要であれば、トークンはいつでもリテラル値に変更できます。) 

この後の「[nuget パックを実行し、.nupkg ファイルを生成する](#run-nuget-pack-to-generate-the-nupkg-file)」で説明するように、Visual Studio プロジェクトから作業するとき、いくつかの追加パッケージ化オプションを利用できます。

#### <a name="solution-level-packages"></a>ソリューションレベル パッケージ

*NuGet 2.x のみ。NuGet 3.0+ では利用できません。*

NuGet 2.x では、パッケージ マネージャー コンソールのツールまたは追加コマンドをインストールするソリューションレベル パッケージの概念がサポートされました (`tools` フォルダーのコンテンツ)。しかしながら、参照、コンテンツ、またはソリューションのプロジェクトに対するビルド カスタマイズは追加されません。 このようなパッケージのその直接の `lib`、`content`、`build` フォルダーにはファイルは含まれておらず、その依存関係の `lib`、`content`、`build` フォルダーにもファイルは含まれていません。

NuGet は、プロジェクトの `packages.config` ファイルではなく、`.nuget` フォルダーの `packages.config` ファイルで、インストールされたソリューションレベル パッケージを追跡記録します。

### <a name="new-file-with-default-values"></a>新しいファイルと既定値

次のコマンドでは、プレースホルダーを含む既定のマニフェストが作成されます。それにより、適切なファイル構造で始められます。

```cli
nuget spec [<package-name>]
```

\<package-name\> を省略すると、結果として得られるファイルは `Package.nuspec` になります。 `Contoso.Utility.UsefulStuff` のような名前を指定すると、ファイルは `Contoso.Utility.UsefulStuff.nuspec` になります。

結果的に生成される `.nuspec` には、`projectUrl` のような値のプレースホルダーが含まれます。 必ずファイルを編集してからそれを利用し、最終的な `.nupkg` ファイルを作成してください。

## <a name="choose-a-unique-package-identifier-and-setting-the-version-number"></a>一意のパッケージ識別子を選択し、バージョン番号を設定する

パッケージ識別子 (`<id>` 要素) とバージョン番号 (`<version>` 要素) は、パッケージに含まれるコードを一意に識別するため、マニフェストの中で最も重要な値です。

**パッケージ識別子のベスト プラクティス:**

- **一意性**:この識別子は、nuget.org 全体で、あるいはパッケージをホストするギャラリー全体で一意になる必要があります。 識別子を決める前に、該当するギャラリーを検索し、その名前が既に使用されていないか確認してください。 競合を避けるために、`Contoso.` のように、識別子の最初の部分に会社の名前を使用することが適しているパターンです。
- **名前空間のような名前**:.NET の名前空間に似たパターンに従います。ハイフンの代わりにドット表記を使います。 たとえば、`Contoso-Utility-UsefulStuff` や `Contoso_Utility_UsefulStuff` ではなく `Contoso.Utility.UsefulStuff` を使用します。 パッケージ識別子がコードで使用される名前空間と一致すれば、利用者にとっても便利です。
- **サンプル パッケージ**:別のパッケージの使用方法を示すサンプル コードのパッケージを生成する場合、`Contoso.Utility.UsefulStuff.Sample` のように、識別子にサフィックスとして `.Sample` を付けます。 (サンプル パッケージは、もちろん、他のパッケージに依存します。)サンプル パッケージを作成するとき、前述のように、規則ベースの作業ディレクトリを使用します。 `content` フォルダーで、`\Samples\Contoso.Utility.UsefulStuff.Sample` のように、`\Samples\<identifier>` という名前のフォルダーにサンプル コードを配置します。

**パッケージ バージョンのベスト プラクティス:**

- 必須ではありませんが、一般的に、ライブラリに合わせてパッケージの番号を設定します。 これはパッケージを 1 つのアセンブリに限定すれば簡単なことです。「[パッケージ化するアセンブリを決定する](#decide-which-assemblies-to-package)」を参照してください。 概して、NuGet 自体は依存関係の解決時、パッケージ バージョンを使います。アセンブリ バージョンではありません。
- 非標準のバージョン スキーマを使用するとき、「[パッケージのバージョン管理](../concepts/package-versioning.md)」で説明するように、NuGet バージョン管理ルールを検討してください。

> バージョン管理の理解には、次の一連のブログ投稿が役立ちます。
>
> - [第 1 部: DLL 地獄](https://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [第 2 部: コア アルゴリズム](https://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [第 3 部:バインド リダイレクトによる統合](https://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="add-a-readme-and-other-files"></a>ReadMe とその他のファイルの追加

パッケージに含めるファイルを直接指定するには、`.nuspec` ファイルの `<files>` ノードを使用します。このノードは `<metadata>` タグの *後に入ります*。

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> 規則ベースの作業ディレクトリ手法を利用するとき、ReadMe.txt をパッケージ ルートに、`content` フォルダーにその他のコンテンツを配置できます。 マニフェストで必須の `<file>` 要素はありません。

パッケージ ルートに `readme.txt` という名前のファイルを含めると、Visual Studio では、パッケージを直接インストールした直後、そのファイルの内容がプレーンテキストとして表示されます。 (パッケージが依存関係としてインストールされた場合、ReadMe ファイルは表示されません。) たとえば、HtmlAgilityPack パッケージの ReadMe は次のように表示されます。

![インストール時の NuGet パッケージの ReadMe ファイルの表示](media/Create_01-ShowReadme.png)

> [!Note]
> `.nuspec` ファイルに空の `<files>` ノードを含める場合、NuGet では、`lib` フォルダーの内容以外の内容はパッケージに入りません。

## <a name="include-msbuild-props-and-targets-in-a-package"></a>パッケージに MSBuild プロパティとターゲットを含める

ビルド時のカスタム ツールまたはプロセスの実行など、場合によっては、パッケージを使用するプロジェクト内のカスタム ビルド ターゲットまたはプロパティを追加する必要があります。 これは、プロジェクトの `\build` フォルダー内に形式 `<package_id>.targets` または `<package_id>.props` で (`Contoso.Utility.UsefulStuff.targets` のように) ファイルを配置することで行います。

ルート `\build` フォルダーのファイルは、すべてのターゲット フレームワークで適切であると見なされます。 ファイルをフレームワーク固有にするには、次のように、まず、適切なサブフォルダーにそのファイルを配置します。

```
    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
```

次に `.nuspec` ファイルで、`<files>` ノードのそれらのファイルを参照するようにします。

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

[NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files) で、パッケージに MSBuild のプロパティとターゲットを含めることができるようになりました。そのため、`metadata` 要素に `minClientVersion="2.5"` 属性を追加して、パッケージを使用するために必要な最小限の NuGet クライアント バージョンを示すことをお勧めします。

NuGet で `\build` ファイルを使用してパッケージをインストールすると、`.targets` ファイルと `.props` ファイルを指す MSBuild `<Import>` 要素がプロジェクト ファイルに追加されます。 (`.props` はプロジェクト ファイルの一番上に、`.targets` は一番下に追加されます。)別個の条件付き MSBuild `<Import>` 要素が、各ターゲット フレームワークに追加されます。

相互フレームワーク ターゲットの MSBuild `.props` および `.targets` ファイルは、`\buildMultiTargeting` フォルダーに配置できます。 パッケージ インストール時に、NuGet は対応する `<Import>` 要素を条件付きのプロジェクト ファイルに追加します。その際、ターゲット フレームワークは設定されません (MSBuild プロパティ `$(TargetFramework)` は必ず空になっています)。

NuGet 3.x を使用する場合、ターゲットはプロジェクトに追加されず、代わりに `{projectName}.nuget.g.targets` と `{projectName}.nuget.g.props` を通じて使用できます。

## <a name="run-nuget-pack-to-generate-the-nupkg-file"></a>nuget パックを実行し、.nupkg ファイルを生成する

アセンブリまたは規則ベースの作業ディレクトリを使用するとき、自分の `.nuspec` ファイルで `nuget pack` を実行してパッケージを作成します。`<project-name>` を特定のファイル名で置換します。

```cli
nuget pack <project-name>.nuspec
```

Visual Studio プロジェクトを使用するとき、自分のプロジェクト ファイルで `nuget pack` を実行します。それにより、プロジェクトの `.nuspec` ファイルが自動的に読み込まれ、その中にトークンがあれば、プロジェクト ファイルの値を利用して置換されます。

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> トークンを置換するには、プロジェクト ファイルを直接使用する必要があります。プロジェクトがトークン値のソースであるからです。 `.nuspec` ファイルで `nuget pack` を使用する場合、トークンは置換されません。

いずれの場合も、`nuget pack` では、`.git` や `.hg` のようなピリオドで始まるフォルダーは除外されます。

NuGet では、修正が必要なエラーが `.nuspec` ファイルで見つかった場合、それが示されます。マニフェストのプレースホルダー値を変更し忘れたなどです。

`nuget pack` が成功すると、`.nupkg` ファイルが生成されます。「[パッケージの公開](../nuget-org/publish-a-package.md)」に説明があるように、このファイルを適切なギャラリーに公開できます。

> [!Tip]
> 作成後のパッケージを調べる便利な方法は、[パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ツールでそれを開くことです。 パッケージの内容とそのマニフェストがグラフィック表示されます。 生成された `.nupkg` ファイルの名前を `.zip` ファイルに変更し、その内容を直接調べることもできます。

### <a name="additional-options"></a>追加オプション

`nuget pack` ではさまざまなコマンドライン スイッチを使用できます。ファイルを除外したり、マニフェストのバージョン番号をオーバーライドしたり、出力フォルダーを変更したりできます。 完全な一覧は、[pack コマンドに関するページ](../reference/cli-reference/cli-ref-pack.md)を参照してください。

Visual Studio プロジェクトの共通オプションには以下のようなものがあります。

- **参照されるプロジェクト**:プロジェクトが他のプロジェクトを参照する場合、参照されるプロジェクトをパッケージの一部あるいは依存関係として追加できます。`-IncludeReferencedProjects` オプションを使用します。

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    この包含プロセスは再帰的です。`MyProject.csproj` が B と C を参照し、それらのプロジェクトが D、E、F を参照する場合、B、C、D、E、F からのファイルがパッケージに含まれます。

    参照されるプロジェクトにそれ自体の `.nuspec` ファイルが含まれる場合、NuGet では、その参照されるプロジェクトが依存関係として追加されます。  そのプロジェクトを個別にパッケージ化し、公開する必要があります。

- **ビルド構成**:既定では、NuGet では、プロジェクト ファイルに設定されている既定のビルド構成が使用されます。一般的には、"*デバッグ*" です。 *リリース* など、別のビルド構成からファイルをパッケージ化するには、構成と共に `-properties` オプションを使用します。

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **シンボル**: 利用者がデバッガーでパッケージ コードをステップ実行することを可能にするシンボルを含めるには、`-Symbols` オプションを使用します。

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="test-package-installation"></a>パッケージ インストールのテスト

パッケージを公開する前に、通常、パッケージをプロジェクトにインストールするプロセスをテストします。 このテストにより、必要なファイルがすべて、プロジェクト内の適切な場所に入ります。

インストールは Visual Studio またはコマンド ラインで手動テストできます。通常の[パッケージ インストール手順](../consume-packages/overview-and-workflow.md#ways-to-install-a-nuget-package)を利用します。

自動テストの基本プロセスは次のようになります。

1. `.nupkg` ファイルをローカル フォルダーにコピーします。
1. `nuget sources add -name <name> -source <path>` コマンドを利用し、パッケージ ソースにフォルダーを追加します ([nuget ソース](../reference/cli-reference/cli-ref-sources.md)を参照してください)。 指定されたコンピューターのいずれかで、このローカル ソースを 1 回設定します。
1. `nuget install <packageID> -source <name>` を利用し、そのソースからパッケージをインストールします。`<name>` は、`nuget sources` に指定されたソースの名前に一致します。 ソースを指定することで、そのソースだけからパッケージがインストールされます。
1. ファイル システムで、ファイルが正しくインストールされていることを調べます。

## <a name="next-steps"></a>次の手順

`.nupkg` ファイルとなるパッケージを作成したら、「[パッケージの公開](../nuget-org/publish-a-package.md)」の説明にあるように、選択したギャラリーにパッケージを公開できます。

パッケージの機能を拡張したり、次のトピックで説明するように、その他の方法で他のシナリオをサポートしたりすると便利な場合があります。

- [パッケージのバージョン管理](../concepts/package-versioning.md)
- [複数のターゲット フレームワークのサポート](../create-packages/supporting-multiple-target-frameworks.md)
- [ソース ファイルと構成ファイルの変換](../create-packages/source-and-config-file-transformations.md)
- [ローカリゼーション](../create-packages/creating-localized-packages.md)
- [プレリリース バージョン](../create-packages/prerelease-packages.md)
- [パッケージの種類の設定](../create-packages/set-package-type.md)
- [COM 相互運用アセンブリを含むパッケージを作成する](../create-packages/author-packages-with-COM-interop-assemblies.md)

最後になりますが、次のような種類のパッケージもあります。

- [ネイティブ パッケージ](../guides/native-packages.md)
- [シンボル パッケージ](../create-packages/symbol-packages-snupkg.md)
