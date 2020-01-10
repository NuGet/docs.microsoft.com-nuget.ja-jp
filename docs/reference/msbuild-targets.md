---
title: MSBuild ターゲットとしての NuGet の pack と restore
description: NuGet の pack と restore は、NuGet 4.0 以降で MSBuild ターゲットとして直接使用できます。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 2c2b5b21569e2644154670d502146f1e0f9c4c81
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385015"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>MSBuild ターゲットとしての NuGet の pack と restore

*NuGet 4.0 以降*

[PackageReference](../consume-packages/package-references-in-project-files.md)形式では、NuGet 4.0 以降では、個別の `.nuspec` ファイルを使用するのではなく、すべてのマニフェストメタデータをプロジェクトファイル内に直接格納できます。

MSBuild 15.1 以降では、NuGet は以下のように `pack` および `restore` ターゲットを使用する MSBuild の最上級のメンバーです。 これらのターゲットを使用すると、他の MSBuild タスクやターゲットの場合と同様に NuGet を使用できます MSBuild を使用して NuGet パッケージを作成する手順については、「[msbuild を使用した nuget パッケージの作成](../create-packages/creating-a-package-msbuild.md)」を参照してください。 (NuGet 3.x 以前の場合は、代わりに NuGet CLI の [pack](../reference/cli-reference/cli-ref-pack.md) および [restore](../reference/cli-reference/cli-ref-restore.md) コマンドを使用します)。

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

> [!NOTE]
> `$(OutputPath)` は相対であり、プロジェクトのルートからコマンドを実行していることを前提としています。

## <a name="pack-target"></a>pack ターゲット

PackageReference 形式を使用する .NET Standard プロジェクトの場合、`msbuild -t:pack` を使用して、NuGet パッケージの作成に使用するプロジェクトファイルからの入力を描画します。

以下の表では、最初の `<PropertyGroup>` ノード内のプロジェクト ファイルに追加できる MSBuild のプロパティについて説明します。 Visual Studio 2017 以降では、プロジェクトを右クリックし、コンテキスト メニューで **[{project_name} の編集]** を選択して、この編集を簡単に行うことができます。 便宜上、この表は、[`.nuspec` ファイル](../reference/nuspec.md)の同等のプロパティごとに整理されています。

`.nuspec` の `Owners` および `Summary` プロパティは、MSBuild ではサポートされていない点に注意してください。

| 属性/NuSpec の値 | MSBuild のプロパティ | [既定値] | メモ |
|--------|--------|--------|--------|
| ID | PackageId | AssemblyName | MSBuild の $(AssemblyName) |
| Version | PackageVersion | Version | これは semver と互換性があります (たとえば、"1.0.0"、"1.0.0-beta"、または "1.0.0-beta-00345") |
| VersionPrefix | PackageVersionPrefix | 空 | PackageVersion を設定すると、PackageVersionPrefix は上書きされます |
| VersionSuffix | PackageVersionSuffix | 空 | MSBuild の $(VersionSuffix) PackageVersion を設定すると、PackageVersionSuffix は上書きされます |
| 執筆者 | 執筆者 | 現在のユーザーのユーザー名 | |
| 所有者 | N/A | NuSpec にはありません | |
| [タイトル] | [タイトル] | PackageId| |
| 説明 | 説明 | "パッケージの説明" | |
| Copyright | Copyright | 空 | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| ライセンス●らいせんす○ | PackageLicenseExpression | 空 | 対応しています `<license type="expression">` |
| ライセンス●らいせんす○ | PackageLicenseFile | 空 | `<license type="file">` に相当します。 参照されているライセンスファイルを明示的にパックする必要があります。 |
| LicenseUrl | PackageLicenseUrl | 空 | `PackageLicenseUrl` は推奨されていません。このプロパティを使用して、パッケージを使用してください。 |
| ProjectUrl | PackageProjectUrl | 空 | |
| アイコン | PackageIcon | 空 | 参照されているアイコンイメージファイルを明示的にパックする必要があります。|
| IconUrl | PackageIconUrl | 空 | ベストダウンレベルのエクスペリエンスを実現するには、`PackageIcon`に加えて `PackageIconUrl` を指定する必要があります。 長期的には、`PackageIconUrl` は非推奨とされます。 |
| Tags | PackageTags | 空 | 複数のタグはセミコロン (;) で区切られます。 |
| ReleaseNotes | PackageReleaseNotes | 空 | |
| Repository/Url | RepositoryUrl | 空 | ソースコードの複製または取得に使用されるリポジトリの URL。 例: *https://github.com/NuGet/NuGet.Client.git* |
| Repository/Type | RepositoryType | 空 | リポジトリの種類。 例: *git*、 *tfs*。 |
| Repository/Branch | RepositoryBranch | 空 | リポジトリのブランチ情報 (オプション)。 このプロパティを含めるには、 *RepositoryUrl*も指定する必要があります。 例: *master* (NuGet 4.7.0 +) |
| Repository/Commit | RepositoryCommit | 空 | 任意のリポジトリ コミットまたは変更セット。パッケージがどのソースに対してビルドされたかを示します。 このプロパティを含めるには、 *RepositoryUrl*も指定する必要があります。 例: *0e4d1b598f350b3dc675018d539114d1328189ef* (NuGet 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| 要約 | サポートなし | | |

### <a name="pack-target-inputs"></a>pack ターゲットの入力

- IsPackable
- SuppressDependenciesWhenPacking
- PackageVersion
- PackageId
- 執筆者
- 説明
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

### <a name="suppress-dependencies"></a>依存関係を表示しない

生成された NuGet パッケージからのパッケージの依存関係を抑制するには、`SuppressDependenciesWhenPacking` を `true` に設定します。これにより、生成された nupkg ファイルからのすべての依存関係がスキップされます。

### <a name="packageiconurl"></a>PackageIconUrl

新しい[`PackageIcon`](#packageicon)プロパティを優先するため、`PackageIconUrl` は非推奨とされます。

NuGet 5.3 & Visual Studio 2019 バージョン16.3 以降では、パッケージメタデータが `PackageIconUrl`を指定するだけの場合、`pack` は[NU5048](./errors-and-warnings/nu5048.md) warning を発生させます。

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> `PackageIcon`をまだサポートしていないクライアントとソースとの下位互換性を維持するには、`PackageIcon` と `PackageIconUrl` の両方を指定する必要があります。 Visual Studio は、今後のリリースでフォルダーベースのソースからのパッケージの `PackageIcon` をサポートします。

#### <a name="packing-an-icon-image-file"></a>アイコンイメージファイルのパッキング

アイコンイメージファイルをパッキングする場合は、パッケージのルートに対して相対的なパッケージパスを指定するために `PackageIcon` プロパティを使用する必要があります。 また、ファイルがパッケージに含まれていることを確認する必要があります。 イメージファイルのサイズは 1 MB に制限されています。 サポートされているファイル形式は、JPEG および PNG です。 64x64 のイメージ解像度をお勧めします。

例:

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

[パッケージアイコンのサンプル](https://github.com/NuGet/Samples/tree/master/PackageIconExample)です。

Nuspec に相当するものについては、「 [nuspec reference for icon」を参照](nuspec.md#icon)してください。

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

### <a name="packing-a-license-expression-or-a-license-file"></a>ライセンス式またはライセンスファイルのパッキング

ライセンス式を使用する場合は、"パッケージの表示" プロパティを使用する必要があります。 
[ライセンス式のサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample)。

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[NuGet.org によって受け付けられるライセンス式とライセンスの詳細については、こちらを参照](nuspec.md#license)してください。

ライセンスファイルをパッキングする場合は、パッケージのルートを基準としたパッケージパスを指定するために、"パッケージの作成" プロパティを使用する必要があります。 また、ファイルがパッケージに含まれていることを確認する必要があります。 例:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

[ライセンスファイルのサンプル](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample)。

### <a name="istool"></a>IsTool

`MSBuild -t:pack -p:IsTool=true` を使用すると、すべての出力ファイル ([Output Assemblies](#output-assemblies) シナリオに指定されているファイル) は、`lib` フォルダーではなく `tools` フォルダーにコピーされます。 これは、`.csproj` ファイルに `PackageType` を設定して指定する `DotNetCliTool` とは異なります。

### <a name="packing-using-a-nuspec"></a>.nuspec を使用したパック

通常は `.nuspec` ファイルに含まれる[すべてのプロパティ](../reference/msbuild-targets.md#pack-target)をプロジェクトファイルに含めることをお勧めしますが、`.nuspec` ファイルを使用してプロジェクトをパックすることもできます。 `PackageReference`を使用する SDK 形式以外のプロジェクトの場合は、`NuGet.Build.Tasks.Pack.targets` をインポートして、パックタスクを実行できるようにする必要があります。 Nuspec ファイルをパックする前に、プロジェクトを復元する必要があります。 (SDK スタイルのプロジェクトには、既定でパックターゲットが含まれています)。

Nuspec をパッキングする場合、プロジェクトファイルのターゲットフレームワークは無関係であり、使用されません。 次の 3 つの MSBuild プロパティが `.nuspec` を使用したパックと関係があります。

1. `NuspecFile`: パックに使用する `.nuspec` ファイルの相対パスまたは絶対パス。
1. `NuspecProperties`: キー=値ペアのセミコロン区切りの一覧。 MSBuild コマンドラインの解析方法に従い、複数のプロパティは `-p:NuspecProperties=\"key1=value1;key2=value2\"` のように指定する必要があります。  
1. `NuspecBasePath`: `.nuspec` ファイルのベース パス。

`dotnet.exe` を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

MSBuild を使用してプロジェクトをパックする場合は、次のようなコマンドを使用します。

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Dotnet または msbuild を使用して nuspec をパッキングすると、既定でプロジェクトのビルドも実行されることに注意してください。 これは、```--no-build``` プロパティを dotnet に渡すことによって回避できます。これは、プロジェクトファイル内の ```<NoBuild>true</NoBuild> ``` を設定するのと同じです。また、プロジェクトファイルに ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` を設定します。

Nuspec ファイルをパックする .csproj ファイルの例を次に示し*ます。*

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

### <a name="advanced-extension-points-to-create-customized-package"></a>カスタマイズしたパッケージを作成するための高度な拡張機能ポイント

`pack` ターゲットには、ターゲットフレームワーク固有の内部ビルドで実行される2つの拡張ポイントが用意されています。 拡張ポイントは、ターゲットフレームワーク固有のコンテンツとアセンブリをパッケージに含めることをサポートしています。

- `TargetsForTfmSpecificBuildOutput` ターゲット: `lib` フォルダー内のファイル、または `BuildOutputTargetFolder`を使用して指定されたフォルダー内のファイルに使用します。
- `TargetsForTfmSpecificContentInPackage` ターゲット: `BuildOutputTargetFolder`の外部のファイルに使用します。

#### <a name="targetsfortfmspecificbuildoutput"></a>TargetsForTfmSpecificBuildOutput

カスタムターゲットを作成し、`$(TargetsForTfmSpecificBuildOutput)` プロパティの値として指定します。 `BuildOutputTargetFolder` に入る必要があるファイル (既定では lib) では、ItemGroup `BuildOutputInPackage` にこれらのファイルを書き込み、次の2つのメタデータ値を設定する必要があります。

- `FinalOutputPath`: ファイルの絶対パス。指定されていない場合は、ソースパスの評価に Id が使用されます。
- `TargetPath`: (省略可能) ファイルが `lib\<TargetFramework>` 内のサブフォルダーに入る必要がある場合に設定されます。これは、それぞれのカルチャフォルダーの下にあるサテライトアセンブリのようになります。 既定値は、ファイルの名前です。

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

カスタムターゲットを作成し、`$(TargetsForTfmSpecificContentInPackage)` プロパティの値として指定します。 パッケージに含めるファイルについては、ターゲットはこれらのファイルを ItemGroup `TfmSpecificPackageFile` に書き込み、次のオプションのメタデータを設定する必要があります。

- `PackagePath`: パッケージ内でファイルが出力されるパス。 複数のファイルが同じパッケージパスに追加されると、NuGet は警告を発行します。
- `BuildAction`: パッケージパスが `contentFiles` フォルダー内にある場合にのみ必要な、ファイルに割り当てるビルドアクション。 既定値は "None" です。

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
1. MSBuild データを NuGet に渡します。
1. restore を実行します
1. パッケージをダウンロードします
1. アセット ファイル、ターゲット、およびプロパティを出力します

`restore` ターゲットは、PackageReference 形式を使用するプロジェクトに対して**のみ**機能します。 `packages.config` 形式を使用するプロジェクトでは機能し**ません**。代わりに[nuget restore](../reference/cli-reference/cli-ref-restore.md)を使用してください。

### <a name="restore-properties"></a>restore のプロパティ

追加の restore 設定を、プロジェクト ファイルの MSBuild プロパティで指定することができます。 また、`-p:` スイッチを使用して、コマンド ラインから値を設定することもできます (次の例を参照してください)。

| property | 説明 |
|--------|--------|
| RestoreSources | パッケージ ソースのセミコロン区切りの一覧。 |
| RestorePackagesPath | ユーザー パッケージ フォルダーのパス。 |
| RestoreDisableParallel | ダウンロード数を一度に 1 つまでに制限します。 |
| RestoreConfigFile | 適用する `Nuget.Config` ファイルのパス。 |
| RestoreNoCache | True の場合、キャッシュされたパッケージの使用を回避します。 「[グローバルパッケージとキャッシュフォルダーの管理」を](../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。 |
| RestoreIgnoreFailedSources | true の場合、失敗した、または不足しているパッケージ ソースを無視します。 |
| RestoreFallbackFolders | フォールバックフォルダー。ユーザーパッケージフォルダーを使用する場合と同じ方法で使用されます。 |
| RestoreAdditionalProjectSources | 復元中に使用する追加のソース。 |
| RestoreAdditionalProjectFallbackFolders | 復元中に使用する追加のフォールバックフォルダー。 |
| RestoreAdditionalProjectFallbackFoldersExcludes | `RestoreAdditionalProjectFallbackFolders` で指定されたフォールバックフォルダーを除外します |
| RestoreTaskAssemblyFile | `NuGet.Build.Tasks.dll` のパス。 |
| RestoreGraphProjectInput | 復元するプロジェクトのセミコロン区切りの一覧。絶対パスを指定する必要があります。 |
| RestoreUseSkipNonexistentTargets  | MSBuild を使用してプロジェクトが収集されると、`SkipNonexistentTargets` の最適化を使用してプロジェクトを収集するかどうかが決定されます。 設定しない場合、既定値は `true`になります。 その結果、プロジェクトのターゲットをインポートできない場合のフェールファースト動作になります。 |
| MSBuildProjectExtensionsPath | 出力フォルダー。 `BaseIntermediateOutputPath` と `obj` フォルダーを既定とします。 |
| RestoreForce | PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。 このフラグを指定することは、`project.assets.json` ファイルの削除に似ています。 これは、http キャッシュをバイパスしません。 |
| RestorePackagesWithLockFile | ロック ファイルの使用をオプトインします。 |
| RestoreLockedMode | ロックモードで復元を実行します。 これは、restore が依存関係を再評価しないことを意味します。 |
| NuGetLockFilePath | ロックファイルのカスタムの場所。 既定の場所はプロジェクトの横にあり、`packages.lock.json`という名前が付けられます。 |
| RestoreForceEvaluate | 復元によって依存関係が再計算され、警告なしでロックファイルが更新されます。 | 

#### <a name="examples"></a>使用例

[コマンド ライン]:

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

| File | 説明 |
|--------|--------|
| `project.assets.json` | すべてのパッケージ参照の依存関係グラフを含みます。 |
| `{projectName}.projectFileExtension.nuget.g.props` | パッケージに含まれる MSBuild プロパティへの参照 |
| `{projectName}.projectFileExtension.nuget.g.targets` | パッケージに含まれる MSBuild ターゲットへの参照 |

### <a name="restoring-and-building-with-one-msbuild-command"></a>1つの MSBuild コマンドを使用した復元とビルド

NuGet では、MSBuild のターゲットとプロパティを表示するパッケージを復元できるため、異なるグローバルプロパティを使用して復元とビルドの評価が実行されます。
これは、次のような場合に予期しない動作が発生する可能性があることを意味します。

```cli
msbuild -t:restore,build
```

 代わりに、推奨される方法は次のとおりです。

```cli
msbuild -t:build -restore
```

`build`に似た他のターゲットにも、同じロジックが適用されます。

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
