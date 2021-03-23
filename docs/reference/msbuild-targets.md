---
title: NuGetターゲットとしてのパックと復元 MSBuild
description: NuGet パックと復元は、4.0 以降のターゲットとして直接使用でき MSBuild NuGet ます。
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 9d40d43d972537ee1cb11d54194ed6450ccd0b6e
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104858967"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGetターゲットとしてのパックと復元 MSBuild

*NuGet 4.0 +*

[PackageReference](../consume-packages/package-references-in-project-files.md)形式では、 NuGet 4.0 以降では、個別のファイルを使用するのではなく、プロジェクトファイル内に直接すべてのマニフェストメタデータを格納でき `.nuspec` ます。

MSBuild15.1 + で NuGet は、次に示すように、とのターゲットを持つファーストクラスの市民でもあり MSBuild `pack` `restore` ます。 これらのターゲットを使用すると、 NuGet 他のタスクやターゲットと同様にを操作でき MSBuild ます。 を使用したパッケージの作成手順については NuGet MSBuild 、「 [ NuGet を使用 MSBuild したパッケージの作成](../create-packages/creating-a-package-msbuild.md)」を参照してください。 (の場合 NuGet )3.x 以前のバージョンでは、CLI を使用して、 [パック](../reference/cli-reference/cli-ref-pack.md) と [復元](../reference/cli-reference/cli-ref-restore.md) コマンドを使用して NuGet います)。

## <a name="target-build-order"></a>ターゲットのビルド順序

`pack`と `restore` はターゲットであるため MSBuild 、それらにアクセスしてワークフローを拡張できます。 たとえば、パッキング後にパッケージをネットワーク共有にコピーするとします。 この場合、プロジェクト ファイルに以下を追加します。

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

同様に、タスクを作成 MSBuild し、独自のターゲットを作成して、タスクのプロパティを使用することもでき NuGet MSBuild ます。

> [!NOTE]
> `$(OutputPath)` は相対であり、プロジェクトのルートからコマンドを実行していることを想定しています。

## <a name="pack-target"></a>pack ターゲット

形式を使用する .NET プロジェクトでは `PackageReference` 、を使用して、 `msbuild -t:pack` パッケージの作成に使用するプロジェクトファイルからの入力を描画し NuGet ます。

次の表では、 MSBuild 最初のノード内のプロジェクトファイルに追加できるプロパティについて説明し `<PropertyGroup>` ます。 Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。 便宜上、テーブルは[ `.nuspec` ファイル](../reference/nuspec.md)内の同等のプロパティによって整理されています。

> [!NOTE]
> `Owners` およびの `Summary` プロパティ `.nuspec` は、ではサポートされていません MSBuild 。

| 属性/ nuspec 値 | MSBuild プロパティ | Default | Notes |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | MSBuild からの `$(AssemblyName)` |
| `Version` | `PackageVersion` | Version | これは semver と互換性があります `1.0.0` 。たとえば、、などです。 `1.0.0-beta``1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | 空 | 上書きの設定 `PackageVersion``PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | 空 | `$(VersionSuffix)` から MSBuild 。 上書きの設定 `PackageVersion``PackageVersionSuffix` |
| `Authors` | `Authors` | 現在のユーザーのユーザー名 | Nuget.org のプロファイル名と一致するパッケージ作成者のセミコロン区切りのリスト。これらは nuget.org のギャラリーに表示され、 NuGet 同じ作成者によってパッケージを相互参照するために使用されます。 |
| `Owners` | 該当なし | 存在しない nuspec | |
| `Title` | `Title` | `PackageId` | 人が読みやすいパッケージのタイトル。通常、nuget.org と、Visual Studio のパッケージ マネージャーの UI 画面で使用されます。 |
| `Description` | `Description` | "パッケージの説明" | アセンブリの長い説明。 `PackageDescription` が指定されていない場合、このプロパティはパッケージの説明としても使用されます。 |
| `Copyright` | `Copyright` | 空 | パッケージの著作権の詳細。 |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | クライアントがユーザーに対して、パッケージのインストール前にパッケージ ライセンスに同意することを必須にするかどうかを示すブール値。 |
| `license` | `PackageLicenseExpression` | 空 | `<license type="expression">` に相当します。 「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。 |
| `license` | `PackageLicenseFile` | 空 | カスタムライセンスまたは SPDX 識別子が割り当てられていないライセンスを使用している場合の、パッケージ内のライセンスファイルへのパス。 参照されているライセンスファイルを明示的にパックする必要があります。 `<license type="file">` に相当します。 「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。 |
| `LicenseUrl` | `PackageLicenseUrl` | 空 | `PackageLicenseUrl` は非推奨とされます。 代わりに、`PackageLicenseExpression` タグまたは `PackageLicenseFile` タグを使用してください。 |
| `ProjectUrl` | `PackageProjectUrl` | 空 | |
| `Icon` | `PackageIcon` | 空 | パッケージ アイコンとして使用するパッケージ内の画像へのパス。 参照されているアイコンイメージファイルを明示的にパックする必要があります。 詳細については、「[アイコンイメージファイル](#packing-an-icon-image-file)と[ `icon` メタデータ](/nuget/reference/nuspec#icon)のパッキング」を参照してください。 |
| `IconUrl` | `PackageIconUrl` | 空 | `PackageIconUrl` は、を優先するために非推奨とされ `PackageIcon` ます。 ただし、最も高いダウンレベルエクスペリエンスを実現するには、に加えてを指定する必要があり `PackageIconUrl` `PackageIcon` ます。 |
| `Tags` | `PackageTags` | 空 | パッケージを指定するタグのセミコロン区切りの一覧。 |
| `ReleaseNotes` | `PackageReleaseNotes` | 空 | パッケージのリリース ノート。 |
| `Repository/Url` | `RepositoryUrl` | 空 | ソースコードの複製または取得に使用されるリポジトリの URL。 例: *https://github.com/ NuGet / NuGet 。クライアント. git*。 |
| `Repository/Type` | `RepositoryType` | 空 | リポジトリの種類。 例: `git` (既定値)、 `tfs` 。 |
| `Repository/Branch` | `RepositoryBranch` | 空 | リポジトリのブランチ情報 (オプション)。 このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。 例: *master* ( NuGet 4.7.0 +)。 |
| `Repository/Commit` | `RepositoryCommit` | 空 | 任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。 このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。 例: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +)。 |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | サポートされていません | | |

### <a name="pack-target-inputs"></a>pack ターゲットの入力

| プロパティ | Description |
| - | - |
| `IsPackable` | プロジェクトをパックできるかどうかを示すブール値。 既定値は `true` です。 |
| `SuppressDependenciesWhenPacking` | `true`生成されたパッケージからのパッケージの依存関係を抑制するには、に設定し NuGet ます。 |
| `PackageVersion` | 結果のパッケージのバージョンを指定します。 すべての形式の NuGet バージョン文字列を受け入れます。 既定値は `$(Version)` です。つまり、プロジェクトのプロパティ `Version` の値です。 |
| `PackageId` | 結果のパッケージの名前を指定します。 指定しない場合、`pack` 操作の既定では、`AssemblyName` またはディレクトリ名をパッケージ名として使用します。 |
| `PackageDescription` | UI 画面用のパッケージの長い説明。 |
| `Authors` | Nuget.org のプロファイル名と一致するパッケージ作成者のセミコロン区切りのリスト。これらは nuget.org のギャラリーに表示され、 NuGet 同じ作成者によってパッケージを相互参照するために使用されます。 |
| `Description` | アセンブリの長い説明。 `PackageDescription` が指定されていない場合、このプロパティはパッケージの説明としても使用されます。 |
| `Copyright` | パッケージの著作権の詳細。 |
| `PackageRequireLicenseAcceptance` | クライアントがユーザーに対して、パッケージのインストール前にパッケージ ライセンスに同意することを必須にするかどうかを示すブール値。 既定値は、`false` です。 |
| `DevelopmentDependency` | 開発専用の依存関係としてパッケージをマークするかどうかを指定するブール値。指定すると、そのパッケージは他のパッケージに依存関係として含まれなくなります。 `PackageReference`( NuGet 4.8 以降) では、このフラグはコンパイル時のアセットがコンパイルから除外されることも意味します。 詳しくは、「[DevelopmentDependency support for PackageReference (PackageReference に対する DevelopmentDependency のサポート)](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)」をご覧ください。 |
| `PackageLicenseExpression` | [Spdx ライセンス識別子](https://spdx.org/licenses/)または式 (など) `Apache-2.0` 。 詳細については、「 [ライセンス式またはライセンスファイルのパッキング](#packing-a-license-expression-or-a-license-file)」を参照してください。 |
| `PackageLicenseFile` | カスタムライセンスまたは SPDX 識別子が割り当てられていないライセンスを使用している場合の、パッケージ内のライセンスファイルへのパス。 |
| `PackageLicenseUrl` | `PackageLicenseUrl` は非推奨とされます。 代わりに、`PackageLicenseExpression` タグまたは `PackageLicenseFile` タグを使用してください。 |
| `PackageProjectUrl` | |
| `PackageIcon` | パッケージのルートに対して相対的なパッケージアイコンパスを指定します。 詳細については、「 [アイコンイメージファイルのパッキング](#packing-an-icon-image-file)」を参照してください。 |
| `PackageReleaseNotes` | パッケージのリリース ノート。 |
| `PackageTags` | パッケージを指定するタグのセミコロン区切りの一覧。 |
| `PackageOutputPath` | パックされたパッケージをドロップする出力パスを指定します。 既定値は `$(OutputPath)` です。 |
| `IncludeSymbols` | このブール値は、プロジェクトをパックするときに、パッケージが追加のシンボル パッケージを作成するかどうかを指定します。 シンボル パッケージの形式は、`SymbolPackageFormat` プロパティで制御します。 詳細については、「 [IncludeSymbols](#includesymbols)」を参照してください。 |
| `IncludeSource` | このブール値は、パック プロセスでソース パッケージを作成するかどうかを示します。 ソース パッケージには、ライブラリのソース コードと PDB ファイルが含まれます。 ソース ファイルは、結果のパッケージ ファイルの `src/ProjectName` ディレクトリに置かれます。 詳細については、「データの追加」を[参照してください。](#includesource) |
| `PackageType` | |
| `IsTool` | すべての出力ファイルを *lib* フォルダーではなく *tools* フォルダーにコピーするかどうかを指定します。 詳細については、「 [IsTool](#istool)」を参照してください。 |
| `RepositoryUrl` | ソースコードの複製または取得に使用されるリポジトリの URL。 例: *https://github.com/ NuGet / NuGet 。クライアント. git*。 |
| `RepositoryType` | リポジトリの種類。 例: `git` (既定値)、 `tfs` 。 |
| `RepositoryBranch` | リポジトリのブランチ情報 (オプション)。 このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。 例: *master* ( NuGet 4.7.0 +)。 |
| `RepositoryCommit` | 任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。 このプロパティを含めるには、`RepositoryUrl` も指定する必要があります。 例: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0 +)。 |
| `SymbolPackageFormat` | シンボル パッケージの形式を指定します。 "Symbols. nupkg" の場合、従来のシンボルパッケージは、Pdb、Dll、およびその他の出力ファイルを含む、 *シンボル* が含まれた拡張子が付いて作成されます。 "Snupkg" の場合、ポータブル Pdb を含む snupkg シンボルパッケージが作成されます。 既定値は "symbols. nupkg" です。 |
| `NoPackageAnalysis` | `pack`パッケージのビルド後にパッケージ分析を実行しないことを指定します。 |
| `MinClientVersion` | NuGetnuget.exe と Visual Studio パッケージマネージャーによって適用される、このパッケージをインストールできるクライアントの最小バージョンを指定します。 |
| `IncludeBuildOutput` | このブール値は、ビルド出力アセンブリを *.nupkg* ファイルにパッケージ化するかどうかを指定します。 |
| `IncludeContentInPack` | このブール値は、の型を持つ項目 `Content` が、結果のパッケージに自動的に含まれるかどうかを指定します。 既定では、 `true`です。 |
| `BuildOutputTargetFolder` | 出力アセンブリを配置するフォルダーを指定します。 出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。 詳細については、「 [出力アセンブリ](#output-assemblies)」を参照してください。 |
| `ContentTargetFolders` | が指定されていない場合に、すべてのコンテンツファイルの移動先となる既定の場所を指定し `PackagePath` ます。 既定値は "content;contentFiles" です。 詳細については、「[Including content in a package](#including-content-in-a-package)」 (パッケージにコンテンツを追加する) を参照してください。 |
| `NuspecFile` | *.nuspec* パッキングに使用されるファイルへの相対パスまたは絶対パス。 指定した場合、パッケージ化情報 **専用** に使用され、プロジェクト内の情報は使用されません。 詳細については、「を[使用した .nuspec パッキング](#packing-using-a-nuspec-file)」を参照してください。 |
| `NuspecBasePath` | ファイルのベースパス *.nuspec* 。 詳細については、「を[使用した .nuspec パッキング](#packing-using-a-nuspec-file)」を参照してください。 |
| `NuspecProperties` | キー=値ペアのセミコロン区切りの一覧。 詳細については、「を[使用した .nuspec パッキング](#packing-using-a-nuspec-file)」を参照してください。 |

## <a name="pack-scenarios"></a>pack のシナリオ

### <a name="suppressing-dependencies"></a>依存関係の抑制

生成されたパッケージからパッケージの依存関係を抑制するに NuGet `SuppressDependenciesWhenPacking` は、をに設定し `true` ます。これにより、生成された nupkg ファイルからのすべての依存関係をスキップできます。

### `PackageIconUrl`

`PackageIconUrl` は、プロパティを優先するために非推奨とされ [`PackageIcon`](#packageicon) ます。 NuGet5.3 および Visual Studio 2019 バージョン16.3 以降では、 `pack` パッケージメタデータでのみが指定されている場合、は[NU5048](./errors-and-warnings/nu5048.md) warning を発生させ `PackageIconUrl` ます。

### `PackageIcon`

> [!Tip]
> まだサポートされていないクライアントおよびソースとの下位互換性を維持するに `PackageIcon` は、との両方を指定し `PackageIcon` `PackageIconUrl` ます。 Visual Studio で `PackageIcon` は、フォルダーベースのソースからのパッケージがサポートされています。

#### <a name="packing-an-icon-image-file"></a>アイコンイメージファイルのパッキング

アイコンイメージファイルをパッキングする場合は、プロパティを使用して、 `PackageIcon` パッケージのルートを基準としたアイコンファイルのパスを指定します。 また、ファイルがパッケージに含まれていることを確認します。 イメージファイルのサイズは 1 MB に制限されています。 サポートされているファイル形式は、JPEG および PNG です。 128x128 のイメージの解像度をお勧めします。

次に例を示します。

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[パッケージアイコンのサンプル](https://github.com/NuGet/Samples/tree/main/PackageIconExample)です。

同等のものについては、 nuspec [ nuspec アイコンの参照](nuspec.md#icon)を確認してください。

### <a name="output-assemblies"></a>出力アセンブリ

`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。 コピーされる出力ファイルは、ターゲットのによって提供される内容によって異なり MSBuild `BuiltOutputProjectGroup` ます。

MSBuildプロジェクトファイルまたはコマンドラインでは、出力アセンブリの移動先を制御するために使用できるプロパティが2つあります。

- `IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。
- `BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。 出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。

### <a name="package-references"></a>パッケージ参照

「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。

### <a name="project-to-project-references"></a>プロジェクト間参照

プロジェクト間参照は、既定ではパッケージ参照と見なされ NuGet ます。 次に例を示します。

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

また、次のメタデータをプロジェクト参照に追加することもできます。

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>パッケージにコンテンツを含める

コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。 次のようなエントリでオーバーライドしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

次のようにパッケージ パスを指定しない場合、既定では、すべてがパッケージ内の `content` および `contentFiles\any\<target_framework>` フォルダーのルートに追加され、相対フォルダー構造が保持されます。

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

すべてのコンテンツを (およびの代わりに) 特定のルートフォルダーにのみコピーする場合は `content` 、 `contentFiles` プロパティを使用できます MSBuild `ContentTargetFolders` 。既定値は "content; contentfiles" ですが、他のフォルダー名に設定することもできます。 `ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。

`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。 空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。 たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

プロパティもあり MSBuild `$(IncludeContentInPack)` ます。既定値は `true` です。 これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。

上記のいずれかの項目に設定できるその他のパック固有のメタデータには、 ```<PackageCopyToOutput>``` ```<PackageFlatten>``` 出力のエントリのセットと値が含まれ ```CopyToOutput``` ```Flatten``` ```contentFiles``` nuspec ます。

> [!Note]
> コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。
>
> glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。

### <a name="includesymbols"></a>IncludeSymbols

`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。 `IncludeSymbols=true` を設定すると、通常のパッケージ *と* シンボル パッケージが作成されます。

### <a name="includesource"></a>IncludeSource

これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。 種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。 `TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。

種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。

### <a name="packing-a-license-expression-or-a-license-file"></a>ライセンス式またはライセンスファイルのパッキング

ライセンス式を使用する場合は、プロパティを使用し `PackageLicenseExpression` ます。 サンプルについては、「 [ライセンス式のサンプル](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)」を参照してください。

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

組織で受け入れられるライセンス式とライセンスの詳細については NuGet 、「 [ライセンスメタデータ](nuspec.md#license)」を参照してください。

ライセンスファイルをパッキングする場合は、パッケージ `PackageLicenseFile` のルートに対して相対的なパッケージパスをプロパティを使用して指定します。 また、ファイルがパッケージに含まれていることを確認します。 次に例を示します。

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

サンプルについては、「 [ライセンスファイルのサンプル](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)」を参照してください。

> [!NOTE]
> 、、およびのいずれか1つだけを `PackageLicenseExpression` `PackageLicenseFile` `PackageLicenseUrl` 同時に指定できます。

### <a name="packing-a-file-without-an-extension"></a>拡張子のないファイルのパッキング

ライセンスファイルをパッキングする場合など、一部のシナリオでは、拡張子のないファイルを含めることができます。
履歴上の理由により、 NuGet  &  MSBuild パスをディレクトリとして拡張せずに扱います。

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[拡張機能サンプルのないファイル](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/)。

### <a name="istool"></a>IsTool

`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。 これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。

### <a name="packing-using-a-nuspec-file"></a>ファイルを使用したパッキング `.nuspec`

通常はファイル内の [すべてのプロパティ](../reference/msbuild-targets.md#pack-target) をプロジェクトファイルに含めることをお勧めし `.nuspec` ますが、プロジェクトを `.nuspec` パックするためにファイルを使用することもできます。 を使用する SDK スタイル以外のプロジェクトでは `PackageReference` 、をインポートして、 `NuGet.Build.Tasks.Pack.targets` パックタスクを実行できるようにする必要があります。 ただし、ファイルをパックする前に、プロジェクトを復元する必要があり nuspec ます。 (SDK スタイルのプロジェクトには、既定でパックターゲットが含まれています)。

プロジェクトファイルのターゲットフレームワークは無関係であり、をパッキングするときには使用されません nuspec 。 次の3つの MSBuild プロパティは、を使用したパッキングに関連してい `.nuspec` ます。

1. `NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。
1. `NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。 コマンドラインの解析方法によっては、次のように MSBuild 複数のプロパティを指定する必要があり `-p:NuspecProperties="key1=value1;key2=value2"` ます。  
1. `NuspecBasePath`: `.nuspec` ファイルのベース パス。

`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

nuspecdotnet.exe または msbuild を使用してをパッキングすると、既定でプロジェクトがビルドされることにも注意してください。 これは、プロパティを dotnet.exe に渡すことによって回避できます。これは、プロジェクトファイルの ```--no-build``` 設定 ```<NoBuild>true</NoBuild> ``` と共に、プロジェクトファイル内の設定に相当し ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` ます。

ファイルをパックする .csproj ファイルの例を次に示し *ます。* nuspec

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>カスタマイズされたパッケージを作成するための高度な拡張ポイント

ターゲットには、 `pack` ターゲットフレームワーク固有の内部ビルドで実行される2つの拡張ポイントが用意されています。 拡張ポイントは、ターゲットフレームワーク固有のコンテンツとアセンブリをパッケージに含めることをサポートしています。

- `TargetsForTfmSpecificBuildOutput` ターゲット: フォルダー内のファイル、 `lib` またはを使用して指定されたフォルダー内のファイルに使用し `BuildOutputTargetFolder` ます。
- `TargetsForTfmSpecificContentInPackage` ターゲット: の外部のファイルに対して使用し `BuildOutputTargetFolder` ます。

#### `TargetsForTfmSpecificBuildOutput`

カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificBuildOutput)` ます。 (既定では lib) に移動する必要があるファイルの場合、 `BuildOutputTargetFolder` ターゲットはこれらのファイルを ItemGroup に書き込み、 `BuildOutputInPackage` 次の2つのメタデータ値を設定する必要があります。

- `FinalOutputPath`: ファイルの絶対パス。指定されていない場合は、ソースパスの評価に Id が使用されます。
- `TargetPath`: (省略可能) ファイルが内のサブフォルダーに入る必要があるときに設定し `lib\<TargetFramework>` ます。これは、それぞれのカルチャフォルダーの下にあるサテライトアセンブリのようになります。 既定値は、ファイルの名前です。

例:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### `TargetsForTfmSpecificContentInPackage`

カスタムターゲットを作成し、プロパティの値として指定し `$(TargetsForTfmSpecificContentInPackage)` ます。 パッケージに含めるファイルについては、ターゲットはこれらのファイルを ItemGroup に書き込み、 `TfmSpecificPackageFile` 次のオプションのメタデータを設定する必要があります。

- `PackagePath`: パッケージでファイルを出力するパス。 NuGet 複数のファイルが同じパッケージパスに追加された場合に、警告を発行します。
- `BuildAction`: ファイルに割り当てるビルドアクション。パッケージパスがフォルダー内にある場合にのみ必要です `contentFiles` 。 既定値は "None" です。

例:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>restore ターゲット

`MSBuild -t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。

1. すべてのプロジェクト間参照を読み取ります
1. プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します
1. MSBuild.Build.Tasks.dll にデータを渡す NuGet
1. restore を実行します
1. パッケージのダウンロード
1. アセット ファイル、ターゲット、およびプロパティを出力します

ターゲットは、 `restore` PackageReference 形式を使用するプロジェクトに対して機能します。
`MSBuild 16.5+` では、形式の [オプトインもサポート](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) されてい `packages.config` ます。

> [!NOTE]
> ターゲットを `restore` ターゲットと組み合わせて [実行することはできません](#restoring-and-building-with-one-msbuild-command) `build` 。

### <a name="restore-properties"></a>restore のプロパティ

その他の復元設定は MSBuild 、プロジェクトファイルのプロパティから取得できます。 また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。

| プロパティ | Description |
|--------|--------|
| `RestoreSources` | パッケージ ソースのセミコロン区切りの一覧。 |
| `RestorePackagesPath` | ユーザー パッケージ フォルダーのパス。 |
| `RestoreDisableParallel` | ダウンロード数を一度に 1 つまでに制限します。 |
| `RestoreConfigFile` | 適用する `Nuget.Config` ファイルのパス。 |
| `RestoreNoCache` | True の場合、キャッシュされたパッケージの使用を回避します。 「 [グローバルパッケージとキャッシュフォルダーの管理」を](../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。 |
| `RestoreIgnoreFailedSources` | true の場合、失敗した、または不足しているパッケージ ソースを無視します。 |
| `RestoreFallbackFolders` | フォールバックフォルダー。ユーザーパッケージフォルダーを使用する場合と同じ方法で使用されます。 |
| `RestoreAdditionalProjectSources` | 復元中に使用する追加のソース。 |
| `RestoreAdditionalProjectFallbackFolders` | 復元中に使用する追加のフォールバックフォルダー。 |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | で指定されたフォールバックフォルダーを除外します。 `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | `NuGet.Build.Tasks.dll` のパス。 |
| `RestoreGraphProjectInput` | 復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。 |
| `RestoreUseSkipNonexistentTargets`  | プロジェクトをで収集すると、そのプロジェクトが MSBuild 最適化を使用して収集されるかどうかが決まり `SkipNonexistentTargets` ます。 設定しない場合、の既定値はに `true` なります。 その結果、プロジェクトのターゲットをインポートできない場合のフェールファースト動作になります。 |
| `MSBuildProjectExtensionsPath` | 出力フォルダー。を既定 `BaseIntermediateOutputPath` として、フォルダーをにし `obj` ます。 |
| `RestoreForce` | PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、ファイルの削除に似てい `project.assets.json` ます。 これは、http キャッシュをバイパスしません。 |
| `RestorePackagesWithLockFile` | ロック ファイルの使用をオプトインします。 |
| `RestoreLockedMode` | ロックモードで復元を実行します。 これは、restore が依存関係を再評価しないことを意味します。 |
| `NuGetLockFilePath` | ロックファイルのカスタムの場所。 既定の場所はプロジェクトの横にあり、という名前が付けられ `packages.lock.json` ます。 |
| `RestoreForceEvaluate` | 復元によって依存関係が再計算され、警告なしでロックファイルが更新されます。 |
| `RestorePackagesConfig` | packages.config のプロジェクトを復元するオプトインスイッチ。でのみサポートさ `MSBuild -t:restore` れます。 |
| `RestoreUseStaticGraphEvaluation` | 標準評価ではなく、静的なグラフの評価を使用するオプトインスイッチ MSBuild 。 静的グラフの評価は、大規模なリポジトリとソリューションで非常に高速な試験的な機能です。 |

#### <a name="examples"></a>例

コマンド ライン:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

プロジェクト ファイル:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>restore の出力

restore で、次のファイルがビルドの `obj` フォルダーに作成されます。

| ファイル | 説明 |
|--------|--------|
| `project.assets.json` | すべてのパッケージ参照の依存関係グラフを含みます。 |
| `{projectName}.projectFileExtension.nuget.g.props` | MSBuildパッケージに含まれる props への参照 |
| `{projectName}.projectFileExtension.nuget.g.targets` | MSBuildパッケージに含まれているターゲットへの参照 |

### <a name="restoring-and-building-with-one-msbuild-command"></a>1つのコマンドを使用した復元とビルド MSBuild

NuGetターゲットと props をダウンするパッケージを復元できるという事実により MSBuild 、復元とビルドの評価は異なるグローバルプロパティを使用して実行されます。
これは、次のような場合に予期しない動作が発生する可能性があることを意味します。

```cli
msbuild -t:restore,build
```

 代わりに、推奨される方法は次のとおりです。

```cli
msbuild -t:build -restore
```

と同様に、同じロジックが他のターゲットにも適用され `build` ます。

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>を使用した PackageReference および packages.config プロジェクトの復元 MSBuild

MSBuild16.5 + では、の packages.config もサポートされてい `msbuild -t:restore` ます。

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` restore は、ではなく、でのみ使用でき `MSBuild 16.5+` ます。 `dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>静的グラフの評価を使用した復元 MSBuild

> [!NOTE]
> MSBuild16.6 + で NuGet は、コマンドラインからの静的なグラフ評価を使用する実験的な機能が追加されました。これにより、大規模なリポジトリの復元時間が大幅に短縮されます。

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

または、ディレクトリのプロパティを設定して有効にすることもできます。

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Visual Studio 2019. x と5.x の NuGet 場合、この機能は試験的でオプトインと見なされます。 この機能が既定で有効になるタイミングの詳細については、「 [ NuGet /home # 9803](https://github.com/NuGet/Home/issues/9803) 」を参照してください。

静的なグラフの復元では、復元の msbuild 部分が変更されますが、プロジェクトの読み取りと評価は復元アルゴリズムではありません。 復元アルゴリズムは、すべての NuGet ツール ( NuGet .exe、 MSBuild .exe、dotnet.exe、および Visual Studio) で同じです。

ほとんどのシナリオでは、静的なグラフ復元は、現在の復元とは動作が異なる場合があります。また、宣言された特定の PackageReferences または ProjectReferences が見つからない可能性があります。

静的なグラフの復元に移行するときは、次の実行を検討してください。

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet 変更を報告 *しない* でください。 不一致が発生した場合は、 [ NuGet /home](https://github.com/nuget/home/issues/new)で問題を報告してください。

### <a name="replacing-one-library-from-a-restore-graph"></a>復元グラフの 1 つのライブラリを置き換える

復元結果のアセンブリが間違っている場合は、パッケージの既定の選択を除外し、独自の選択で置き換えることができます。 まず、最上位の `PackageReference` ですべてのアセットを除外します。

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

次に、DLL の適切なローカル コピーに独自の参照を追加します。

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
