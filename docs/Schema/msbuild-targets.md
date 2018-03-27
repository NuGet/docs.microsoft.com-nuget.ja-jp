---
title: "MSBuild ターゲットとしての NuGet の pack と restore | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 04/03/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。"
keywords: "NuGet と MSBuild, NuGet の pack ターゲット, NuGet の restore ターゲット"
ms.reviewer:
- karann-msft
ms.openlocfilehash: 169d73709eeb17aade7d99da66bbb4f346f8093f
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/31/2018
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>MSBuild ターゲットとしての NuGet の pack と restore

*NuGet 4.0 以降*

NuGet 4.0 以降では、PackageReference 形式を使用することにより、すべてのマニフェスト メタデータを、個別の `.nuspec` ファイルを使用せずにプロジェクト ファイルに直接保存できます。

MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。 これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます  (NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../tools/cli-ref-pack.md) および [restore](../tools/cli-ref-restore.md) コマンドを使用します)。

## <a name="target-build-order"></a>ターゲットのビルド順序

`pack` と `restore` は MSBuild のターゲットなので、アクセスするとワークフローを強化できます。 たとえば、パック後にパッケージをネットワーク共有にコピーするとします。 この場合、プロジェクト ファイルに以下を追加します。

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
    <Copy
        SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
        DestinationFolder="\\myshare\packageshare\"
        />
</Target>
```

同様に、MSBuild タスクを記述し、独自のターゲットを記述して、MSBuild タスクで NuGet プロパティを使用することができます。

## <a name="pack-target"></a>pack ターゲット

pack ターゲット (つまり `msbuild /t:pack`) を使用すると、MSBuild はプロジェクト ファイルからの入力を描画します。 以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。 Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。 便宜上、この表は、[`.nuspec` ファイル](../schema/nuspec.md)の同等のプロパティごとに整理されています。

`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。

| 属性/NuSpec の値 | MSBuild のプロパティ | 既定値 | メモ |
|--------|--------|--------|--------|
| ID | PackageId | AssemblyName | MSBuild の $(AssemblyName) |
| Version | PackageVersion | Version | これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345") |
| VersionPrefix | PackageVersionPrefix | (なし) | PackageVersion を設定すると、PackageVersionPrefix は上書きされます |
| VersionSuffix | PackageVersionSuffix | (なし) | MSBuild の $(VersionSuffix) PackageVersion を設定すると、PackageVersionSuffix は上書きされます |
| Authors | Authors | 現在のユーザーのユーザー名 | |
| 所有者 | N/A | NuSpec にはありません | |
| Title | Title | PackageId| |
| 説明 | 説明 | "パッケージの説明" | |
| Copyright | Copyright | (なし) | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| LicenseUrl | PackageLicenseUrl | (なし) | |
| ProjectUrl | PackageProjectUrl | (なし) | |
| IconUrl | PackageIconUrl | (なし) | |
| Tags | PackageTags | (なし) | 複数のタグはセミコロン (;) で区切られます。 |
| ReleaseNotes | PackageReleaseNotes | (なし) | |
| RepositoryUrl | RepositoryUrl | (なし) | |
| RepositoryType | RepositoryType | (なし) | |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| まとめ | サポートなし | | |

### <a name="pack-target-inputs"></a>pack ターゲットの入力

- IsPackable
- PackageVersion
- PackageId
- Authors
- 説明
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>pack のシナリオ

### <a name="packageiconurl"></a>PackageIconUrl

[NuGet の問題 2582](https://github.com/NuGet/Home/issues/2582) への変更の一部として、最終的に `PackageIconUrl` は `PackageIconUri` に変更され、結果のパッケージのルートに含まれるアイコン ファイルへの相対パスを使用できるようになる予定です。

### <a name="output-assemblies"></a>出力アセンブリ

`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。 コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。

出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。

- `IncludeBuildOutput`: ビルドの出力アセンブリをパッケージに含めるかどうかを決めるブール値。
- `BuildOutputTargetFolder`: 出力アセンブリを配置するフォルダーを指定します。 出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。

### <a name="package-references"></a>パッケージ参照

「[Package References (PackageReference) in Project Files](../consume-packages/package-references-in-project-files.md)」(プロジェクト ファイルのパッケージ参照 (PackageReference)) を参照してください。

### <a name="project-to-project-references"></a>プロジェクト間参照

プロジェクト間参照は、既定で NuGet パッケージ参照として見なされています。次に例を示します。

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

コンテンツを含めるには、既存の `<Content>` 項目にメタデータを追加します。 次のようなエントリで上書きしない場合、既定で "Content" という種類のすべての要素はパッケージに含まれます。

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

(`content` および `contentFiles` フォルダーの両方ではなく) すべてのコンテンツを特定のルート フォルダーにのみコピーする場合、MSBuild プロパティの `ContentTargetFolders` を使用できます。このプロパティの既定値は "content;contentFiles" ですが、他の任意のフォルダー名に設定できます。 `ContentTargetFolders` に "contentFiles" と指定するだけで、`buildAction` に基づいて `contentFiles\any\<target_framework>` または `contentFiles\<language>\<target_framework>` 以下にファイルが配置されます。

`PackagePath` には、セミコロンで区切った一連のターゲット パスを指定できます。 空のパッケージ パスを指定すると、ファイルはパッケージのルートに追加されます。 たとえば、次のように指定すると、`libuv.txt` は `content\myfiles`、`content\samples`、およびパッケージ ルートに追加されます。

```xml
<Content Include="..\win7-x64\libuv.txt">
    <Pack>true</Pack>
    <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

また、MSBuild プロパティの `$(IncludeContentInPack)` もあります。既定値は `true` です。 これを任意のプロジェクトで `false` に設定すると、プロジェクトのコンテンツは NuGet パッケージに含まれません。

上記の任意の項目に設定できる他の pack 固有のメタデータとして、NuSpec の ```contentFiles``` エントリに ```CopyToOutput``` 値と ```Flatten``` 値を設定する ```<PackageCopyToOutput>``` と ```<PackageFlatten>``` があります。

> [!Note]
> コンテンツ項目とは別に、`<Pack>` と `<PackagePath>` のメタデータは、ビルド アクション (Compile、EmbeddedResource、ApplicationDefinition、Page、Resource、SplashScreen、DesignData、DesignDataWithDesignTimeCreatableTypes、CodeAnalysisDictionary、AndroidAsset、AndroidResource、BundleResource、または None) でファイルに設定することもできます。
>
> glob パターンの使用時にファイル名をパッケージ パスに付加する pack の場合、パッケージ パスの末尾にフォルダー セパレーター文字を付ける必要があります。そうしないと、パッケージ パスはファイル名を含む完全パスとして扱われます。

### <a name="includesymbols"></a>IncludeSymbols

`MSBuild /t:pack /p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。 `IncludeSymbols=true` を設定すると、通常のパッケージ*と*シンボル パッケージが作成されます。

### <a name="includesource"></a>IncludeSource

これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。 種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。 `TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。

種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。

### <a name="istool"></a>IsTool

`MSBuild /t:pack /p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。 これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。

### <a name="packing-using-a-nuspec"></a>.nuspec を使用したパック

パック タスクを実行するために `NuGet.Build.Tasks.Pack.targets` をインポートするプロジェクト ファイルがある場合、`.nuspec` ファイルを使用してプロジェクトをパックできます。 次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。

1. `NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。
1. `NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。 MSBuild コマンドラインの解析方法に従い、複数のプロパティは `/p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。  
1. `NuspecBasePath`: `.nuspec` ファイルのベース パス。

`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。

```cli
dotnet pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。

```cli
msbuild /t:pack <path to .csproj file> /p:NuspecFile=<path to nuspec file> /p:NuspecProperties=<> /p:NuspecBasePath=<Base path> 
```

## <a name="restore-target"></a>restore ターゲット

`MSBuild /t:restore` (`nuget restore` と `dotnet restore` が .NET Core プロジェクトで使用) は、次のようにプロジェクト ファイルで参照されるパッケージを復元します。

1. すべてのプロジェクト間参照を読み取ります
1. プロジェクトのプロパティを読み取って、中間フォルダーとターゲット フレームワークを検出します
1. MSBuild データを NuGet.Build.Tasks.dll に渡します
1. restore を実行します
1. パッケージをダウンロードします
1. アセット ファイル、ターゲット、およびプロパティを出力します

### <a name="restore-properties"></a>restore のプロパティ

追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。 また、`/p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。

| プロパティ | 説明 |
|--------|--------|
| RestoreSources | パッケージ ソースのセミコロン区切りの一覧。 |
| RestorePackagesPath | ユーザー パッケージ フォルダーのパス。 |
| RestoreDisableParallel | ダウンロード数を一度に 1 つまでに制限します。 |
| RestoreConfigFile | 適用する `Nuget.Config` ファイルのパス。 |
| RestoreNoCache | true の場合、Web キャッシュを使用しません。 |
| RestoreIgnoreFailedSources | true の場合、失敗した、または不足しているパッケージ ソースを無視します。 |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll` のパス。 |
| RestoreGraphProjectInput | 復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。 |
| RestoreOutputPath | 出力フォルダー。既定値は `obj` フォルダーです。 |

#### <a name="examples"></a>使用例

コマンド ライン:

```cli
msbuild /t:restore /p:RestoreConfigFile=<path>
```

プロジェクト ファイル:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
<PropertyGroup>
```

### <a name="restore-outputs"></a>restore の出力

restore で、次のファイルがビルドの `obj` フォルダーに作成されます。

| ファイル | 説明 |
|--------|--------|
| `project.assets.json` | 以前の `project.lock.json` |
| `{projectName}.projectFileExtension.nuget.g.props` | パッケージに含まれる MSBuild プロパティへの参照 |
| `{projectName}.projectFileExtension.nuget.g.targets` | パッケージに含まれる MSBuild ターゲットへの参照 |

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます。 dotnet [TxM](../schema/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。 つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。

たとえば、プロジェクトが `netstandard1.6` TxM を使用し、依存しているパッケージに `lib/net45/a.dll` と `lib/portable-net45+win81/a.dll` のみが含まれている場合、そのプロジェクトはビルドできません。 後者の DLL を構築する予定の場合は、`portable-net45+win81` DLL に互換性を持たせるために、次のように `PackageTargetFallback` を追加します。

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

プロジェクト内のすべてのターゲットについてフォールバックを宣言するには、`Condition` 属性を省略します。 また、次のように `$(PackageTargetFallback)` を含めて、既存の `PackageTargetFallback` を拡張することもできます。

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

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
