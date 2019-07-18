---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 1e89aeb46f2538d46c013561a51a41702b2472d8
ms.sourcegitcommit: 6b71926f062ecddb8729ef8567baf67fd269642a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2019
ms.locfileid: "59932100"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>MSBuild ターゲットとしての NuGet の pack と restore

*NuGet 4.0 以降*

NuGet 4.0 以降では、PackageReference 形式を使用することにより、すべてのマニフェスト メタデータを、個別の `.nuspec` ファイルを使用せずにプロジェクト ファイルに直接保存できます。

MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。 これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます (NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../tools/cli-ref-pack.md) および [restore](../tools/cli-ref-restore.md) コマンドを使用します)。

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

PackageReference 形式を使用して、使用して .NET Standard プロジェクトの`msbuild -t:pack`NuGet パッケージの作成に使用するプロジェクト ファイルからの入力を描画します。

以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。 Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。 便宜上、この表は、[`.nuspec` ファイル](../reference/nuspec.md)の同等のプロパティごとに整理されています。

`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。

| 属性/NuSpec の値 | MSBuild のプロパティ | 既定値 | メモ |
|--------|--------|--------|--------|
| ID | PackageId | AssemblyName | MSBuild の $(AssemblyName) |
| Version | PackageVersion | Version | これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345") |
| VersionPrefix | PackageVersionPrefix | (なし) | PackageVersion を設定すると、PackageVersionPrefix は上書きされます |
| VersionSuffix | PackageVersionSuffix | (なし) | MSBuild の $(VersionSuffix) PackageVersion を設定すると、PackageVersionSuffix は上書きされます |
| Authors | Authors | 現在のユーザーのユーザー名 | |
| Owners | N/A | NuSpec にはありません | |
| Title | Title | PackageId| |
| Description | Description | "パッケージの説明" | |
| Copyright | Copyright | (なし) | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | False | |
| license | PackageLicenseExpression | (なし) | 対応しています `<license type="expression">` |
| license | PackageLicenseFile | (なし) | `<license type="file">` に相当します。 明示的に参照先のライセンス ファイルをパックする必要があります。 |
| LicenseUrl | PackageLicenseUrl | (なし) | `licenseUrl` PackageLicenseExpression または PackageLicenseFile プロパティを使用して、非推奨とされています。 |
| ProjectUrl | PackageProjectUrl | (なし) | |
| IconUrl | PackageIconUrl | (なし) | |
| Tags | PackageTags | (なし) | 複数のタグはセミコロン (;) で区切られます。 |
| ReleaseNotes | PackageReleaseNotes | (なし) | |
| Repository/Url | RepositoryUrl | (なし) | リポジトリの URL を複製するか、ソース コードを取得するために使用します。 例: *https://github.com/NuGet/NuGet.Client.git* |
| Repository/Type | RepositoryType | (なし) | リポジトリの種類。 例: *git*、 *tfs*します。 |
| Repository/Branch | RepositoryBranch | (なし) | 省略可能なリポジトリのブランチの情報。 *RepositoryUrl*にインクルードするには、このプロパティも指定する必要があります。 例:*マスター* (NuGet 4.7.0+) |
| Repository/Commit | RepositoryCommit | (なし) | 省略可能なリポジトリのコミットまたは変更セットをパッケージ ソースを示すためには、に対して構築されました。 *RepositoryUrl*にインクルードするには、このプロパティも指定する必要があります。 例:*0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0+) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Summary | サポートなし | | |

### <a name="pack-target-inputs"></a>pack ターゲットの入力

- IsPackable
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- Authors
- Description
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
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
- RepositoryBranch
- RepositoryCommit
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

### <a name="suppress-dependencies"></a>依存関係を抑制します。

パッケージの依存関係から NuGet パッケージの生成を抑制するのには、設定`SuppressDependenciesWhenPacking`に`true`これにより生成された nupkg ファイルからすべての依存関係をスキップしています。

### <a name="packageiconurl"></a>PackageIconUrl

変更の一環として[NuGet 問題 352](https://github.com/NuGet/Home/issues/352)、`PackageIconUrl`に最終的に変更されます`PackageIconUri`結果のパッケージのルートに含まれるアイコン ファイルへの相対パスを指定できます。

### <a name="output-assemblies"></a>出力アセンブリ

`nuget pack` は拡張子 `.exe`、`.dll`、`.xml`、`.winmd`、`.json`、および `.pri` の出力ファイルをコピーします。 コピーされる出力ファイルは、MSBuild が `BuiltOutputProjectGroup` ターゲットから提供するものによって変わります。

出力アセンブリの出力先を制御する MSBuild プロパティが 2 つあり、プロジェクト ファイルまたはコマンド ラインで使用できます。

- `IncludeBuildOutput`:ビルドの出力アセンブリをパッケージに含めるかどうかを決定するブール値。
- `BuildOutputTargetFolder`:出力アセンブリを配置するフォルダーを指定します。 出力アセンブリ (および他の出力ファイル) は、各フレームワーク フォルダーにコピーされます。

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

`MSBuild -t:pack -p:IncludeSymbols=true` を使用すると、対応する `.pdb` ファイルは他の出力ファイル (`.dll`、`.exe`、`.winmd`、`.xml`、`.json`、`.pri`) と共にコピーされます。 `IncludeSymbols=true` を設定すると、通常のパッケージ*と*シンボル パッケージが作成されます。

### <a name="includesource"></a>IncludeSource

これは、ソース ファイルと `.pdb` ファイルの両方がコピーされる点を除き、`IncludeSymbols` と同じです。 種類が `Compile` のすべてのファイルは `src\<ProjectName>\` にコピーされ、結果のパッケージには相対パス フォルダー構造が保持されます。 `TreatAsPackageReference` が `false` に設定された任意の `ProjectReference` のソース ファイルも同様の結果になります。

種類が Compile のファイルがプロジェクト フォルダー以外の場所にある場合は、単に `src\<ProjectName>\` に追加されます。

### <a name="packing-a-license-expression-or-a-license-file"></a>梱包ライセンス式またはライセンス ファイル

ライセンスの式を使用する場合は、PackageLicenseExpression プロパティを使用してください。 
[ライセンスの式のサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)します。

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[ライセンスの式と NuGet.org で受け入れられるライセンスについて](nuspec.md#license)します。

ライセンス ファイルをパックするときに、PackageLicenseFile プロパティを使用して、パッケージのルートを基準とした、パッケージのパスを指定する必要があります。 さらに、ファイルをパッケージに含まれるかどうかを確認する必要があります。 例えば:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```
[ライセンス ファイルのサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)します。

### <a name="istool"></a>IsTool

`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。 これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。

### <a name="packing-using-a-nuspec"></a>.nuspec を使用したパック

使用することができます、`.nuspec`ファイルをインポートする SDK のプロジェクト ファイルがある場合に、プロジェクトをパック`NuGet.Build.Tasks.Pack.targets`パック タスクを実行できるようにします。 Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。 プロジェクト ファイルのターゲット フレームワークは関係ありませんされ、nuspec をパックするときに使用されません。 次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。

1. `NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。
1. `NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。 MSBuild コマンドラインの解析方法に従い、複数のプロパティは `-p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。  
1. `NuspecBasePath`:ベース パス、`.nuspec`ファイル。

`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。

```cli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

既定では、プロジェクトを構築するために nuspec を梱包 dotnet.exe または msbuild を使用して潜在顧客もことに注意してください。 これを渡すことによって回避できます```--no-build```プロパティの設定に相当する、dotnet.exe を```<NoBuild>true</NoBuild> ```設定と共に、プロジェクト ファイルで```<IncludeBuildOutput>false</IncludeBuildOutput> ```プロジェクト ファイル

Nuspec ファイルをパックする csproj ファイルの例を示します。

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

### <a name="advanced-extension-points-to-create-customized-package"></a>カスタマイズされたパッケージを作成する拡張ポイントの詳細

`pack`ターゲットは、内部のターゲット フレームワーク固有のビルドで実行している 2 つの拡張機能ポイントを提供します。 拡張機能ポイントは、ターゲット フレームワークの特定のコンテンツなど、パッケージにアセンブリをサポートします。

- `TargetsForTfmSpecificBuildOutput` ターゲット:内のファイルの使用、`lib`フォルダー、またはフォルダーを使用して指定`BuildOutputTargetFolder`します。
- `TargetsForTfmSpecificContentInPackage` ターゲット:外部ファイルの使用、`BuildOutputTargetFolder`します。

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

カスタムのターゲットを作成しの値として指定する、`$(TargetsForTfmSpecificBuildOutput)`プロパティ。 移動する必要があるすべてのファイルに対して、 `BuildOutputTargetFolder` (既定では lib)、ターゲットは、ItemGroup にそれらのファイルを書き込む必要があります`BuildOutputInPackage`し、次の 2 つのメタデータ値の設定。

- `FinalOutputPath`:は、ファイルの絶対パス指定しない場合、ソース パスを評価する Id が使用します。
- `TargetPath`:(省略可能)ファイルがサブフォルダー内にする必要があるときに設定`lib\<TargetFramework>`サテライト アセンブリのそれぞれのカルチャ フォルダーの下には、その移動など、します。 既定値は、ファイルの名前です。

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

#### <a name="targetsfortfmspecificcontentinpackage"></a>TargetsForTfmSpecificContentInPackage

カスタムのターゲットを作成しの値として指定する、`$(TargetsForTfmSpecificContentInPackage)`プロパティ。 パッケージに含める任意のファイルのターゲットは、ItemGroup にそれらのファイルを書き込む必要があります`TfmSpecificPackageFile`し、次の省略可能なメタデータを設定します。

- `PackagePath`:パスは、ファイルがパッケージの出力をする必要があります。 NuGet は、1 つ以上のファイルが同じパッケージのパスに追加された場合に警告を発行します。
- `BuildAction`:かどうかは、パッケージ パスでは、ファイルに割り当てるビルド アクションにのみ必要な`contentFiles`フォルダー。 "None"に既定値です。

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
1. MSBuild データを nuget.build.tasks.dll に渡します
1. restore を実行します
1. パッケージをダウンロードします
1. アセット ファイル、ターゲット、およびプロパティを出力します

`restore`対象 works**のみ**PackageReference 形式を使用してプロジェクトの。 **いない**を使用するプロジェクトの作業、`packages.config`は書式指定を使用して、 [nuget 復元](../tools/cli-ref-restore.md)代わりにします。

### <a name="restore-properties"></a>restore のプロパティ

追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。 また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。

| プロパティ | Description |
|--------|--------|
| RestoreSources | パッケージ ソースのセミコロン区切りの一覧。 |
| RestorePackagesPath | ユーザー パッケージ フォルダーのパス。 |
| RestoreDisableParallel | ダウンロード数を一度に 1 つまでに制限します。 |
| RestoreConfigFile | 適用する `Nuget.Config` ファイルのパス。 |
| RestoreNoCache | True の場合は、キャッシュされたパッケージを使用して回避できます。 参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。 |
| RestoreIgnoreFailedSources | true の場合、失敗した、または不足しているパッケージ ソースを無視します。 |
| RestoreFallbackFolders | フォールバックのフォルダーは、フォルダーが使用されるユーザー パッケージと同じ方法で使用されます。 |
| RestoreAdditionalProjectSources | 復元中に使用するソースを追加します。 |
| RestoreAdditionalProjectFallbackFolders | 復元中に使用するフォールバック フォルダーを追加します。 |
| RestoreAdditionalProjectFallbackFoldersExcludes | 指定されたフォールバック フォルダーは除外されます。 `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll` のパス。 |
| RestoreGraphProjectInput | 復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。 |
| RestoreUseSkipNonexistentTargets  | プロジェクトが MSBuild を使用して収集されるかどうかを判断します経由で収集されるタイミング、`SkipNonexistentTargets`最適化します。 設定しない場合、既定値は`true`します。 結果は、プロジェクトのターゲットをインポートできない場合の高速動作です。 |
| MSBuildProjectExtensionsPath | 既定では、出力フォルダー`BaseIntermediateOutputPath`と`obj`フォルダー。 |

#### <a name="examples"></a>使用例

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

| ファイル | Description |
|--------|--------|
| `project.assets.json` | すべてのパッケージ参照の依存関係グラフが含まれています。 |
| `{projectName}.projectFileExtension.nuget.g.props` | パッケージに含まれる MSBuild プロパティへの参照 |
| `{projectName}.projectFileExtension.nuget.g.targets` | パッケージに含まれる MSBuild ターゲットへの参照 |

### <a name="restoring-and-building-with-one-msbuild-command"></a>復元して、1 つの MSBuild コマンドを使用してビルド

NuGet では、MSBuild ターゲットおよびプロパティがダウンするパッケージを復元できます、という事実が原因は、復元とビルドの評価が異なるグローバル プロパティで実行されます。
これは、次の必要がある、多くの場合、不適切な予測できない動作を意味します。

```cli
msbuild -t:restore,build
```

 代わりに推奨される方法は次のとおりです。

```cli
msbuild -t:build -restore
```

ような他のターゲットに同じロジックが適用されます`build`します。

### <a name="packagetargetfallback"></a>PackageTargetFallback

`PackageTargetFallback` 要素では、パッケージの復元時に使用する、互換性のある一連のターゲットを指定できます。 dotnet [TxM](../reference/target-frameworks.md) を使用するパッケージが、dotnet TxM を宣言していない互換性のあるパッケージと連携できるように設計されています。 つまり、プロジェクトで dotnet TxM を使用せず、依存するすべてのパッケージに dotnet TxM を与える必要がある場合、非 dotnet プラットフォームを dotnet 対応にするためにプロジェクトに `<PackageTargetFallback>` を追加します。

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
