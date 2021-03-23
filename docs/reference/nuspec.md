---
title: NuGet の nuspec ファイルリファレンス
description: .nuspec ファイルには、パッケージを作成するとき、およびパッケージのコンシューマーに情報を提供するために使われる、パッケージのメタデータが含まれています。
author: JonDouglas
ms.author: jodou
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 4028657862cfd56d0653b370e8344cab8392d69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859500"
---
# <a name="nuspec-reference"></a>.nuspec リファレンス

`.nuspec` ファイルは、パッケージのメタデータが含まれている XML マニフェストです。 このマニフェストは、パッケージを作成するためと、コンシューマーに情報を提供するための、両方に使われます。 パッケージにはマニフェストが常に含まれています。

このトピックの内容:

- [一般的な形式とスキーマ](#general-form-and-schema)
- [置換トークン](#replacement-tokens) (Visual Studio プロジェクトで使われるとき)
- [依存関係](#dependencies)
- [明示的なアセンブリ参照](#explicit-assembly-references)
- [フレームワーク アセンブリ参照](#framework-assembly-references)
- [アセンブリ ファイルを含める](#including-assembly-files)
- [コンテンツ ファイルを含める](#including-content-files)
- [Nuspec ファイルの例](#example-nuspec-files)

## <a name="project-type-compatibility"></a>プロジェクトの種類の互換性

- を `.nuspec` `nuget.exe pack` 使用する非 SDK 形式のプロジェクトには、を使用し `packages.config` ます。

- `.nuspec` [Sdk スタイルのプロジェクト](../resources/check-project-format.md)のパッケージを作成するためにファイルは必要ありません (通常、 [sdk 属性](/dotnet/core/tools/csproj#additions)を使用する .net Core および .NET Standard プロジェクト)。 ( `.nuspec` パッケージの作成時にが生成されることに注意してください)。

   またはを使用してパッケージを作成する場合は、 `dotnet.exe pack` `msbuild pack target` 通常、ファイル内の [すべてのプロパティ](../reference/msbuild-targets.md#pack-target) をプロジェクトファイルに含めることをお勧め `.nuspec` します。 ただし、代わりに[ `.nuspec` `dotnet.exe` また `msbuild pack target` はを使用して、パックするファイルを使用](../reference/msbuild-targets.md#packing-using-a-nuspec-file)することもできます。

- から PackageReference に移行されたプロジェクトでは、 `packages.config` パッケージを[](../consume-packages/package-references-in-project-files.md) `.nuspec` 作成するためにファイルは必要ありません。 代わりに、 [msbuild-{0}](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration)を使用します。

## <a name="general-form-and-schema"></a>一般的な形式とスキーマ

最新の `nuspec.xsd` スキーマ ファイルは、[NuGet GitHub リポジトリ](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd)にあります。

このスキーマでの `.nuspec` ファイルの一般的な形式は次のとおりです。

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

スキーマの視覚的な表現をはっきり表示したい場合は、Visual Studio のデザイン モードでスキーマ ファイルを開き、**[XML スキーマ エクスプローラー]** リンクをクリックします。 または、コードとしてファイルを開き、エディター内を右クリックして、**[XML スキーマ エクスプローラーで表示]** を選びます。 どちらの方法でも次のように表示されます (ほとんどを展開した場合)。

![Visual Studio のスキーマ エクスプローラーで開いた nuspec.xsd](media/SchemaExplorer.png)

一般的な XML の場合と同様に、nuspec ファイル内のすべての XML 要素名で大文字と小文字が区別されます。 たとえば、メタデータ要素の使用 `<description>` は正しいので、 `<Description>` 正しくありません。 各要素名の適切な大文字と小文字の指定については、以下で説明します。

### <a name="required-metadata-elements"></a>メタデータの必須要素

以下の要素はパッケージの最低要件であり、[メタデータの省略可能な要素](#optional-metadata-elements)を追加してパッケージに関する開発者の全体的なエクスペリエンスを向上させることを検討する必要があります。 

これらの要素は、`<metadata>` 要素内で指定する必要があります。

#### <a name="id"></a>id 
パッケージの識別子。大文字と小文字が区別されます。nuget.org 全体で、またはパッケージが存在するギャラリー全体で、一意である必要があります。 ID は、スペースまたは URL で無効な文字を含んでいてはならず、一般に .NET 名前空間の規則に従います。 ガイダンスについては、[一意のパッケージ識別子の選択](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number)に関するページをご覧ください。

パッケージを nuget.org にアップロードする場合、 `id` フィールドの文字数は128文字に制限されます。

#### <a name="version"></a>version
パッケージのバージョン。*major.minor.patch* のパターンに従います。 「[Package versioning](../concepts/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) で説明されているように、バージョン番号にはプレリリースのサフィックスを含めることができます。 

パッケージを nuget.org にアップロードする場合、 `version` フィールドの文字数は64文字に制限されます。

#### <a name="description"></a>description
UI 表示用のパッケージの説明。

パッケージを nuget.org にアップロードする場合、 `description` フィールドの文字数は4000文字に制限されます。

#### <a name="authors"></a>作成者
Nuget.org のプロファイル名と一致するパッケージ作成者のコンマ区切りのリスト。これらは nuget.org の NuGet ギャラリーに表示され、同じ作成者によってパッケージを相互参照するために使用されます。 

パッケージを nuget.org にアップロードする場合、 `authors` フィールドの文字数は4000文字に制限されます。

### <a name="optional-metadata-elements"></a>メタデータの省略可能な要素

#### <a name="owners"></a>owners
> [!Important]
> 所有者は非推奨とされます。 代わりに、作成者を使用してください。

Nuget.org のプロファイル名を使用して、パッケージ作成者のコンマ区切りのリスト。多くの場合、このリストはと同じです `authors` 。パッケージを nuget.org にアップロードするときには無視されます。「 [Nuget.org でのパッケージ所有者の管理」を](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)参照してください。 

#### <a name="projecturl"></a>projectUrl
パッケージのホーム ページの URL。多くの場合、UI 画面と nuget.org に表示されます。 

パッケージを nuget.org にアップロードする場合、 `projectUrl` フィールドの文字数は4000文字に制限されます。

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> licenseUrl は非推奨とされます。 代わりにライセンスを使用してください。

パッケージのライセンスの URL。多くの場合、nuget.org のような Ui に表示されます。

パッケージを nuget.org にアップロードする場合、 `licenseUrl` フィールドの文字数は4000文字に制限されます。

#### <a name="license"></a>license

***NuGet 4.9.0-** 以降でサポートされています*

SPDX ライセンス式またはパッケージ内のライセンスファイルへのパス。多くの場合、nuget.org のような Ui に表示されます。MIT や BSD-2 句などの一般的なライセンスでパッケージのライセンスを取得している場合は、関連付けられている [Spdx ライセンス識別子](https://spdx.org/licenses/)を使用します。 次に例を示します。

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org は、オープンソースイニシアチブまたは無償のソフトウェア基盤によって承認されたライセンス式のみを受け入れます。

パッケージが複数の一般的なライセンスでライセンスされている場合は、 [Spdx 式の構文バージョン 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)を使用して複合ライセンスを指定できます。 次に例を示します。

`<license type="expression">BSD-2-Clause OR MIT</license>`

ライセンス式でサポートされていないカスタムライセンスを使用する場合は、 `.txt` または `.md` ファイルをライセンスのテキストと共にパッケージ化することができます。 次に例を示します。

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

同等の MSBuild については、 [ライセンス式またはライセンスファイルのパッキング](msbuild-targets.md#packing-a-license-expression-or-a-license-file)に関する説明を参照してください。

NuGet のライセンス式の正確な構文については、 [Abnf](https://tools.ietf.org/html/rfc5234)で説明します。

```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl

> [!Important]
> iconUrl は非推奨とされます。 代わりにアイコンを使用してください。

UI 表示でパッケージのアイコンとして使用される透明な背景を持つ128x128 イメージの URL。 この要素の値は、"*画像を直接示す URL*" であり、画像を含む Web ページの URL ではないことに注意してください。 たとえば、GitHub のイメージを使用するには、" <em> https://github.com/ \<username\> / \<repository\> /raw/ \<branch\> / \<logo.png\> </em>" のような raw ファイル URL を使用します。 

パッケージを nuget.org にアップロードする場合、 `iconUrl` フィールドの文字数は4000文字に制限されます。

#### <a name="icon"></a>icon

***NuGet 5.3.0** 以降でサポートされています*

これはパッケージ内のイメージファイルへのパスであり、多くの場合、パッケージアイコンとして nuget.org のような Ui に表示されます。 イメージファイルのサイズは 1 MB に制限されています。 サポートされているファイル形式は、JPEG および PNG です。 128x128 のイメージの解像度をお勧めします。

たとえば、nuget.exe を使用してパッケージを作成するときに、次のコードを nuspec に追加します。

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[パッケージアイコン nuspec サンプル。](https://github.com/NuGet/Samples/tree/main/PackageIconNuspecExample)

同等の MSBuild については、「 [アイコンイメージファイルのパッキング」](msbuild-targets.md#packing-an-icon-image-file)を参照してください。

> [!Tip]
> を `icon` `iconUrl` サポートしていないソースとの下位互換性を維持するために、との両方を指定でき `icon` ます。 Visual Studio では `icon` 、将来のリリースでフォルダーベースのソースからのパッケージがサポートされるようになります。

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
パッケージをインストールする前にクライアントがユーザーに対してパッケージのライセンスへの同意を求めるプロンプトを表示する必要があるかどうかを示すブール値。

#### <a name="developmentdependency"></a>developmentDependency
*(2.8 以降)* 開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。 PackageReference (NuGet 4.8 以降) では、このフラグは、コンパイルからコンパイル時アセットを除外することも意味します。 「 [DevelopmentDependency support For PackageReference」を](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)参照してください。

#### <a name="summary"></a>まとめ
> [!Important]
> `summary` は非推奨とされます。 代わりに `description` を使用してください

UI 画面用のパッケージの短い説明。 省略すると、`description` を切り詰めたバージョンが使われます。

パッケージを nuget.org にアップロードする場合、 `summary` フィールドの文字数は4000文字に制限されます。

#### <a name="releasenotes"></a>releaseNotes
*(1.5 以降)* このリリースのパッケージで行われた変更の説明。Visual Studio パッケージ マネージャーの **[更新]** タブなどの UI で、パッケージの説明の代わりによく使われます。

パッケージを nuget.org にアップロードする場合、 `releaseNotes` フィールドの文字数は35000文字に制限されます。

#### <a name="copyright"></a>著作権
*(1.5 以降)* パッケージの著作権の詳細。

パッケージを nuget.org にアップロードする場合、 `copyright` フィールドの文字数は4000文字に制限されます。

#### <a name="language"></a>language
パッケージのロケール ID。 「[ローカライズされたパッケージの作成](../create-packages/creating-localized-packages.md)」をご覧ください。

#### <a name="tags"></a>tags
パッケージについて説明し、検索やフィルターでパッケージを見つけやすくするタグやキーワードを、スペースで区切って列記したリスト。 

パッケージを nuget.org にアップロードする場合、 `tags` フィールドの文字数は4000文字に制限されます。

#### <a name="serviceable"></a>serviceable 
*(3.3 以降)* NuGet 内部でのみ使われます。

#### <a name="repository"></a>repository
リポジトリメタデータ。4つの省略可能な属性で構成されています: `type` and `url` *(4.0 +)*、and `branch` `commit` *(4.6 +)*。 これらの属性を使用すると、を構築したリポジトリにをマップすることができ `.nupkg` ます。これにより、パッケージを構築した個々のブランチ名またはコミット sha-1 ハッシュが詳細に表示されます。 これは、バージョン管理ソフトウェアによって直接呼び出すことができる、一般公開されている url である必要があります。 これはコンピューター用の html ページである必要はありません。 [プロジェクトへのリンク] ページでは、代わりにフィールドを使用し `projectUrl` ます。

次に例を示します。
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

パッケージを nuget.org にアップロードする場合、 `type` 属性は100文字に制限され、 `url` 属性は4000文字に制限されます。

#### <a name="title"></a>title
UI 表示で使用できる、パッケージのわかりやすいタイトル。 (Visual Studio の nuget.org とパッケージマネージャーにはタイトルが表示されません)

パッケージを nuget.org にアップロードする場合、 `title` フィールドは256文字に制限されますが、表示目的では使用されません。

#### <a name="collection-elements"></a>コレクション要素

#### <a name="packagetypes"></a>packageTypes
*(3.5 以降)* 従来の依存関係パッケージ以外の場合に、パッケージの種類を指定する 0 個以上の `<packageType>` 要素のコレクション。 各 packageType は、*name* 属性と *version* 属性を持っています。 「[Setting a package type](../create-packages/set-package-type.md)」(パッケージの種類の設定) をご覧ください。

#### <a name="dependencies"></a>dependencies
パッケージの依存関係を指定する 0 個以上の `<dependency>` 要素のコレクション。 各 dependency は、*id*、*version*、*include* (3.x 以降)、*exclude* (3.x 以降) の各属性を持っています。 後の「[依存関係](#dependencies-element)」をご覧ください。

#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2 以降)* このパッケージで必要な .NET Framework アセンブリ参照を示す 0 個以上の `<frameworkAssembly>` 要素のコレクション。パッケージを使うプロジェクトに参照が確実に追加されるようにします。 各 frameworkAssembly は、*assemblyName* 属性と *targetFramework* 属性を持っています。 [フレームワーク アセンブリ参照 GAC の指定](#specifying-framework-assembly-references-gac)に関する後の説明をご覧ください。

#### <a name="references"></a>references
*(1.5 以降)* パッケージの `lib` フォルダー内のアセンブリのうちプロジェクト参照として追加するものを指定する、0 個以上の `<reference>` 要素のコレクション。 各参照は、*file* 属性を持っています。 `<references>` は `<group>` 要素を含むこともでき、その *targetFramework* 属性に `<reference>` 要素を含めることができます。 省略すると、`lib` のすべての参照が含まれます。 [明示的なアセンブリ参照の指定](#specifying-explicit-assembly-references)に関する後の説明をご覧ください。

#### <a name="contentfiles"></a>contentFiles
*(3.3 以降)* 使用する側のプロジェクトに含めるコンテンツ ファイルを示す `<files>` 要素のコレクション。 これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。 [パッケージに含めるファイルの指定](#specifying-files-to-include-in-the-package)に関する後の説明をご覧ください。

#### <a name="files"></a>files 
ノードには `<package>` `<files>` `<metadata>` 、 `<contentFiles>` パッケージに `<metadata>` 含めるアセンブリおよびコンテンツファイルを指定するためのノードが、の兄弟として、およびの子として含まれている場合があります。 詳しくは、このトピックで後述する「[アセンブリ ファイルを含める](#including-assembly-files)」と「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。

### <a name="metadata-attributes"></a>メタデータ属性

#### <a name="minclientversion"></a>minClientVersion
nuget.exe および Visual Studio パッケージ マネージャーで強制する、このパッケージをインストールできる NuGet クライアントの最小バージョンを指定します。 これは、NuGet クライアントの特定のバージョンで追加された `.nuspec` ファイルの特定の機能にパッケージが依存しているときに、常に使われます。 たとえば、`developmentDependency` 属性を使っているパッケージでは、`minClientVersion` に "2.8" を指定する必要があります。 同様に、`contentFiles` 要素 (次のセクションを参照) を使っているパッケージでは、`minClientVersion` を "3.3" に設定する必要があります。 また、バージョン 2.5 より前の NuGet クライアントはこのフラグを認識しないので、`minClientVersion` の値が何であっても、"*常に*" パッケージをインストールしないことにも注意してください。

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a>置換トークン

パッケージを作成する場合、 [ `nuget pack` コマンド](../reference/cli-reference/cli-ref-pack.md)は、ファイルのノード内の $ で区切られたトークンを、 `.nuspec` `<metadata>` プロジェクトファイルまたはコマンドのスイッチから取得した値に置き換え `pack` `-properties` ます。

コマンド ラインでは、`nuget pack -properties <name>=<value>;<name>=<value>` でトークンの値を指定します。 たとえば、`.nuspec` では `$owners$` や `$desc$` などのトークンを使っておき、パッキング時に次のようにして値を指定できます。

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

プロジェクトの値を使うには、次の表で説明するトークンを指定します (AssemblyInfo は、`Properties` 内の `AssemblyInfo.cs` や `AssemblyInfo.vb` などのファイルを参照します)。

これらのトークンを使うには、`nuget pack` を実行するときに、`.nuspec` だけでなくプロジェクト ファイルも指定します。 たとえば、次のコマンドを使うと、`.nuspec` ファイルの `$id$` および `$version$` トークンが、プロジェクトの `AssemblyName` および `AssemblyVersion` の値に置き換えられます。

```ps
nuget pack MyProject.csproj
```

通常、プロジェクトがある場合は、最初に `nuget spec MyProject.csproj` を使って `.nuspec` を作成すると、一部の標準的なトークンが自動的に追加されます。 ただし、`.nuspec` の必須要素に対する値がプロジェクトにないと、`nuget pack` は失敗します。 さらに、プロジェクトの値を変更する場合は、パッケージを作成する前に必ずビルドし直してください。これは、pack コマンドの `build` スイッチで簡単に行うことができます。

例外である `$configuration$` を除き、コマンド ラインの同じトークンに割り当てられている値より、プロジェクトの値の方が優先的に使われます。

| トークン | 値のソース | 値
| --- | --- | ---
| **$id $** | プロジェクト ファイル | プロジェクトファイルからの AssemblyName (title) |
| **$version $** | AssemblyInfo | ある場合は AssemblyInformationalVersion、ない場合は AssemblyVersion |
| **$author $** | AssemblyInfo | AssemblyCompany |
| **$title $** | AssemblyInfo | AssemblyTitle |
| **$description $** | AssemblyInfo | AssemblyDescription |
| **$copyright $** | AssemblyInfo | AssemblyCopyright |
| **$configuration $** | アセンブリ DLL | アセンブリのビルドに使われる構成。既定値は Debug。 Release 構成を使ってパッケージを作成するには、常にコマンド ラインで `-properties Configuration=Release` を使うことに注意してください。 |

[アセンブリ ファイル](#including-assembly-files)および[コンテンツ ファイル](#including-content-files)を含めるときは、トークンを使ってパスを解決することもできます。 トークンの名前は MSBuild のプロパティと同じであり、現在のビルド構成に基づいて含めるファイルを選ぶことができます。 たとえば、`.nuspec` ファイルで次のトークンを使うものとします。

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

そして、MSBuild で `AssemblyName` が `LoggingLibrary` であるアセンブリを `Release` 構成でビルドすると、パッケージ内の `.nuspec` ファイルの行は結果として次のようになります。

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Dependencies 要素

`<metadata>` 内の `<dependencies>` 要素は、最上位のパッケージが依存している他のパッケージを示す `<dependency>` 要素をいくつでも含むことができます。 各 `<dependency>` の属性は次にとおりです。

| 属性 | 説明 |
| --- | --- |
| `id` | (必須) "EntityFramework" や "NUnit" などの依存関係のパッケージ ID。これはパッケージ ページに表示されるパッケージ nuget.org の名前となります。 |
| `version` | (必須) 依存関係として許容されるバージョンの範囲。 厳密な構文については、「[Package versioning](../concepts/package-versioning.md#version-ranges)」(パッケージのバージョン管理) をご覧ください。 フローティングバージョンはサポートされていません。 |
| include | 最終的なパッケージに含める依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。 既定値は `all` です。 |
| 除外 | 最終的なパッケージから除外する依存関係を示す包含/除外タグ (下記参照) のコンマ区切りリスト。 既定値は、 `build,analyzers` 上書きすることができます。 `content/ ContentFiles`また、最終的なパッケージでは、上書きすることはできません。 `exclude` で指定されているタグの方が、`include` で指定されているタグより優先されます。 たとえば、`include="runtime, compile" exclude="compile"` は `include="runtime"` と同じです。 |

パッケージを nuget.org にアップロードする場合、各依存関係の `id` 属性は128文字に制限され、 `version` 属性は256文字に制限されます。

| 包含/除外タグ | ターゲットの影響を受けるフォルダー |
| --- | --- |
| contentFiles | コンテンツ |
| ランタイム | Runtime、Resources、FrameworkAssemblies |
| compile | lib |
| build | build (MSBuild のプロパティとターゲット) |
| native | native |
| なし | フォルダーなし |
| all | すべてのフォルダー |

たとえば、次の行は `PackageA` バージョン 1.1.0 以降および `PackageB` バージョン 1.x での依存関係を示します。

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

次の行も同じパッケージでの依存関係を示しますが、`PackageA` の `contentFiles` および `build` フォルダーを含めて、`PackageB` の `native` および `compile` フォルダーを除くすべてを含めることを指定します。

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> `.nuspec`を使用してプロジェクトからを作成する場合 `nuget spec` 、そのプロジェクトに存在する依存関係は、結果のファイルに自動的に含まれません `.nuspec` 。 代わりに `nuget pack myproject.csproj` 、を使用し、生成された *nupkg* ファイル内から *nuspec* ファイルを取得します。 この *nuspec* には、依存関係が含まれています。

### <a name="dependency-groups"></a>依存関係グループ

*バージョン2.0 以降*

1 つのフラット リストの代わりに、`<dependencies>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って依存関係を指定できます。

各グループには、`targetFramework` という名前の属性があり、0 個以上の `<dependency>` 要素が含まれます。 ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの依存関係が一緒にインストールされます。

依存関係の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。 正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。

> [!Important]
> グループの形式をフラット リストと併用することはできません。

> [!Note]
> フォルダーで使用される [ターゲットフレームワークモニカー (tfm)](../reference/target-frameworks.md) の形式 `lib/ref` は、で使用される tfm と比較して異なり `dependency groups` ます。 で宣言されたターゲットフレームワーク `dependencies group` とファイルのフォルダーが完全に一致しない場合、 `lib/ref` `.nuspec` `pack` コマンドによって [NuGet 警告 NU5128](../reference/errors-and-warnings/nu5128.md)が生成されます。

次の例では、`<group>` 要素のさまざまなバリエーションを示します。

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>明示的なアセンブリ参照

要素は、 `<references>` を使用してプロジェクトがパッケージを使用するときに、 `packages.config` ターゲットプロジェクトが参照するアセンブリを明示的に指定するために使用されます。 明示的な参照は、通常、設計時のみのアセンブリに使われます。 詳細については、「 [プロジェクトによって参照されるアセンブリの選択](../create-packages/select-assemblies-referenced-by-projects.md) 」のページを参照してください。

たとえば、次の `<references>` 要素は、パッケージに他のアセンブリがある場合でも、`xunit.dll` と `xunit.extensions.dll` に対する参照だけを追加するよう NuGet に指示します。

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a>[参照グループ]

1 つのフラット リストの代わりに、`<references>` の `<group>` 要素を使い、ターゲット プロジェクトのフレームワーク プロファイルに従って参照を指定できます。

各グループには、`targetFramework` という名前の属性があり、0 個以上の `<reference>` 要素が含まれます。 ターゲットのフレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの参照はプロジェクトに追加されます。

参照の既定のリストまたはフォールバック リストとしては、`targetFramework` 属性のない `<group>` 要素が使われます。 正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。

> [!Important]
> グループの形式をフラット リストと併用することはできません。

次の例では、`<group>` 要素のさまざまなバリエーションを示します。

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>フレームワーク アセンブリ参照

フレームワーク アセンブリは、.NET Framework の一部であり、指定されたコンピューターのグローバル アセンブリ キャッシュ (GAC) に既に存在している必要があります。 `<frameworkAssemblies>` 要素でこれらのアセンブリを指定することにより、プロジェクトに必要な参照がまだない場合であっても、そのような参照をプロジェクトに確実に追加できます。 もちろん、そのようなアセンブリがパッケージに直接含まれることはありません。

`<frameworkAssemblies>` 要素には 0 個以上の `<frameworkAssembly>` 要素を含めることができ、それぞれで次の属性を指定します。

| 属性 | 説明 |
| --- | --- |
| **assemblyName** | (必須) 完全修飾アセンブリ名。 |
| **targetFramework** | (省略可能) この参照を適用するターゲット フレームワークを指定します。 省略した場合は、参照がすべてのフレームワークに適用されることを示します。 正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。 |

次の例は、`System.Net` への参照はすべてのターゲット フレームワークに適用され、`System.ServiceModel` への参照は .NET Framework 4.0 のみに適用されることを示します。

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>アセンブリ ファイルを含める

「[パッケージを作成する](../create-packages/creating-a-package.md)」で説明されている規則に従う場合、`.nuspec` ファイルでファイルの一覧を明示的に指定する必要はありません。 `nuget pack` コマンドが必要なファイルを自動的に選びます。

> [!Important]
> プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、指定されている `.resources.dll` は、ローカライズされたサテライト アセンブリであると見なされるため "*除外*" されます。 そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。

この自動動作をバイパスして、パッケージに含めるファイルを明示的に制御するには、`<files>` 要素を `<package>` の子要素 (および `<metadata>` の兄弟要素) として配置し、各ファイルを個別の `<file>` 要素で示します。 次に例を示します。

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

NuGet 2.x 以前および `packages.config` を使っているプロジェクトでは、`<files>` 要素はパッケージのインストール時に変更できないコンテンツ ファイルを含めるためにも使われます。 NuGet 3.3 以降で、PackageReference を使用しているプロジェクトでは、代わりに `<contentFiles>` 要素が使用されます。 詳しくは、後の「[コンテンツ ファイルを含める](#including-content-files)」をご覧ください。

### <a name="file-element-attributes"></a>File 要素の属性

各 `<file>` 要素では、次の属性を指定します。

| 属性 | 説明 |
| --- | --- |
| **src** | 含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。 絶対パスを指定しない限り、パスは `.nuspec` ファイルが基準になります。 ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。 |
| **target** | ソース ファイルが格納されるパッケージ内のフォルダーへの相対パス。`lib`、`content`、`build`、または `tools` で始まっている必要があります。 [規則に基づく作業ディレクトリからの .nuspec の作成](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)に関するページをご覧ください。 |
| **もの** | `src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。 ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。 |

### <a name="examples"></a>例

**1 つのアセンブリ**

```
Source file:
    library.dll

.nuspec entry:
    <file src="library.dll" target="lib" />

Packaged result:
    lib\library.dll
```

**ターゲット フレームワークに固有の 1 つのアセンブリ**

```
Source file:
    library.dll

.nuspec entry:
    <file src="assemblies\net40\library.dll" target="lib\net40" />

Packaged result:
    lib\net40\library.dll
```

**ワイルドカードを使った DLL のセット**

```
Source files:
    bin\release\libraryA.dll
    bin\release\libraryB.dll

.nuspec entry:
    <file src="bin\release\*.dll" target="lib" />

Packaged result:
    lib\libraryA.dll
    lib\libraryB.dll
```

**異なるフレームワークの DLL**

```
Source files:
    lib\net40\library.dll
    lib\net20\library.dll

.nuspec entry (using ** recursive search):
    <file src="lib\**" target="lib" />

Packaged result:
    lib\net40\library.dll
    lib\net20\library.dll
```

**ファイルの除外**

```
Source files:
    \tools\fileA.bak
    \tools\fileB.bak
    \tools\fileA.log
    \tools\build\fileB.log

.nuspec entries:
    <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
    <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

Package result:
    (no files)
```

## <a name="including-content-files"></a>コンテンツ ファイルを含める

コンテンツ ファイルは、パッケージでプロジェクトに含める必要がある変更できないファイルです。 変更できないので、それを使うプロジェクトによる変更は意図されていません。 コンテンツ ファイルの例を次に示します。

- リソースとして埋め込まれる画像
- コンパイル済みのソース ファイル
- プロジェクトのビルド出力と共に含まれる必要があるスクリプト
- プロジェクトに含まれる必要はあるが、プロジェクト固有の変更は必要ない、パッケージの構成ファイル

コンテンツ ファイルをパッケージに含めるには、`<files>` 要素を使い、`target` 属性で `content` フォルダーを指定します。 ただし、PackageReference を使用しているプロジェクトにパッケージをインストールする場合、このようなファイルは無視され、代わりに `<contentFiles>` 要素が使用されます。

使用する側のプロジェクトとの最大限の互換性のため、パッケージでは両方の要素でコンテンツ ファイルを指定するのが理想的です。

### <a name="using-the-files-element-for-content-files"></a>コンテンツ ファイルに対する files 要素の使用

コンテンツ ファイルでは、アセンブリ ファイルの場合と同じ形式を使用しますが、次の例のように、`target` 属性で基本フォルダーとして `content` を指定します。

**基本的なコンテンツ ファイル**

```
Source files:
    css\mobile\style1.css
    css\mobile\style2.css

.nuspec entry:
    <file src="css\mobile\*.css" target="content\css\mobile" />

Packaged result:
    content\css\mobile\style1.css
    content\css\mobile\style2.css
```

**ディレクトリ構造を持つコンテンツ ファイル**

```
Source files:
    css\mobile\style.css
    css\mobile\wp7\style.css
    css\browser\style.css

.nuspec entry:
    <file src="css\**\*.css" target="content\css" />

Packaged result:
    content\css\mobile\style.css
    content\css\mobile\wp7\style.css
    content\css\browser\style.css
```

**ターゲット フレームワークに固有のコンテンツ ファイル**

```
Source file:
    css\cool\style.css

.nuspec entry
    <file src="css\cool\style.css" target="Content" />

Packaged result:
    content\style.css
```

**名前のドットでフォルダーにコピーされるコンテンツ ファイル**

この場合、NuGet は `target` の拡張子が `src` の拡張子と一致しないものと判断し、`target` での名前のその部分をフォルダーとして扱います。

```
Source file:
    images\picture.png

.nuspec entry:
    <file src="images\picture.png" target="Content\images\package.icons" />

Packaged result:
    content\images\package.icons\picture.png
```

**拡張子のないコンテンツ ファイル**

拡張子のないファイルを含めるには、ワイルドカード `*` または `**` を使います。

```
Source file:
    flags\installed

.nuspec entry:
    <file src="flags\**" target="flags" />

Packaged result:
    flags\installed
```

**深いパスと深いターゲットのコンテンツ ファイル**

この場合、ソースとターゲットのファイル拡張子が一致するので、NuGet はターゲットがフォルダーではなくファイル名であると想定します。

```
Source file:
    css\cool\style.css

.nuspec entry:
    <file src="css\cool\style.css" target="Content\css\cool" />
    or:
    <file src="css\cool\style.css" target="Content\css\cool\style.css" />

Packaged result:
    content\css\cool\style.css
```

**パッケージ内のコンテンツ ファイルの名前の変更**

```
Source file:
    ie\css\style.css

.nuspec entry:
    <file src="ie\css\style.css" target="Content\css\ie.css" />

Packaged result:
    content\css\ie.css
```

**ファイルの除外**

```
Source file:
    docs\*.txt (multiple files)

.nuspec entry:
    <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
    or
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

Packaged result:
    All .txt files from docs except admin.txt (first example)
    All .txt files from docs except admin.txt and log.txt (second example)
```

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>コンテンツ ファイルに対する contentFiles 要素の使用

*NuGet 4.0 以降で、PackageReference を使用している場合*

既定では、パッケージはコンテンツを `contentFiles` フォルダーに配置し (下記参照)、`nuget pack` は既定の属性を使ってそのフォルダーにすべてのファイルを格納します。 この場合は、`contentFiles` ノードを `.nuspec` に含める必要はまったくありません。

含まれるファイルを制御するには、含めるファイルを厳密に示す `<files>` 要素のコレクションである `<contentFiles>` 要素を指定します。

これらのファイルは、プロジェクト システム内でのファイルの使用方法が記述されている属性のセットで指定されます。

| 属性 | 説明 |
| --- | --- |
| **用意** | (必須) 含める 1 つまたは複数のファイルの場所。`exclude` 属性によって指定される除外の対象になります。 `contentFiles`絶対パスが指定されていない場合は、フォルダーに対する相対パスになります。 ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。 |
| **もの** | `src` の場所から除外するファイルまたはファイル パターンをセミコロンで区切ったリスト。 ワイルドカード文字 `*` を使うことができ、2 個のワイルドカード `**` は再帰的なフォルダー検索を意味します。 |
| **buildAction** | MSBuild のコンテンツ項目に割り当てるビルドアクション (、、、など) `Content` `None` `Embedded Resource` `Compile` 。既定値は `Compile` です。 |
| **copyToOutput** | コンテンツ項目をビルド (または発行) 出力フォルダーにコピーするかどうかを示すブール値。 既定値は false です。 |
| **flatten** | コンテンツ項目をビルド出力の単一フォルダーにコピーするか (true)、それともパッケージのフォルダー構造を保持するか (false) を示すブール値。 このフラグは、copyToOutput が true に設定されている場合のみ機能します。 既定値は false です。 |

パッケージをインストールするとき、NuGet は `<contentFiles>` の子要素を上から下に順番に適用します。 複数のエントリが同じファイルに一致する場合は、すべてのエントリが適用されます。 同じ属性に対して競合がある場合は、最上位のエントリが下位のエントリをオーバーライドします。

#### <a name="package-folder-structure"></a>パッケージ フォルダーの構造

パッケージ プロジェクトでは、次のパターンを使ってコンテンツを構成する必要があります。

```
/contentFiles/{codeLanguage}/{TxM}/{any?}
```

- `codeLanguages` には、`cs`、`vb`、`fs`、`any`、または指定された `$(ProjectLanguage)` に相当する小文字表現を指定できます。
- `TxM` は、NuGet がサポートする任意の有効なターゲット フレームワーク モニカーです (「[ターゲット フレームワーク](../reference/target-frameworks.md)」を参照)。
- この構文の末尾に、任意のフォルダー構造を追加できます。

次に例を示します。

```
Language- and framework-agnostic:
    /contentFiles/any/any/config.xml

net45 content for all languages
    /contentFiles/any/net45/config.xml

C#-specific content for net45 and up
    /contentFiles/cs/net45/sample.cs
```

空のフォルダーでは、`.` を使って、言語と TxM の特定の組み合わせにコンテンツを提供しないようにすることができます。次はその例です。

```
/contentFiles/vb/any/code.vb
/contentFiles/cs/any/.
```

#### <a name="example-contentfiles-section"></a>contentFiles セクションの例

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="framework-reference-groups"></a>フレームワーク参照グループ

*バージョン 5.1 + 追加 PackageReference のみ*

フレームワーク参照は、WPF や Windows フォームなどの共有フレームワークを表す .NET Core の概念です。
共有フレームワークを指定することで、パッケージによって、すべてのフレームワークの依存関係が参照元のプロジェクトに含まれるようになります。

各要素には、1つ `<group>` の `targetFramework` 属性と0個以上の要素が必要 `<frameworkReference>` です。

次の例は、.NET Core WPF プロジェクト用に生成された nuspec を示しています。
フレームワーク参照を含む手動作成 nuspecs は推奨されません。 代わりに、 [ターゲット](msbuild-targets.md) パックを使用することを検討してください。これにより、プロジェクトからそれらが自動的に推論されます。

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a>Nuspec ファイルの例

**依存関係またはファイルを指定しない単純な `.nuspec`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**依存関係を含む `.nuspec`**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**ファイルを含む `.nuspec`**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**フレームワーク アセンブリを含む `.nuspec`**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

この例では、指定したプロジェクト ターゲットに次のものがインストールされます。

- .NET4 -> `System.Web`、`System.Net`
- .NET4 Client Profile -> `System.Net`
- Silverlight 3 -> `System.Json`
- WindowsPhone -> `Microsoft.Devices.Sensors`
