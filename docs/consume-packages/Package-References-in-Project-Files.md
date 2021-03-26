---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照)
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
author: nkolev92
ms.author: nikolev
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: df7c793d115622f04a148cbbc3ebf396a3e4ab69
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859188"
---
# <a name="package-references-packagereference-in-project-files"></a>プロジェクト ファイルのパッケージ参照 (`PackageReference`)

`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。 PackageReference を使用する場合、呼び出されても、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.config` ファイルの設定が、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」で説明されているように引き続き適用されます。

PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワークまたはその他のグループ化ごとにパッケージ参照を選択することもできます。 依存関係とコンテンツ フローを細かく制御することもできます。 (詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。

## <a name="project-type-support"></a>プロジェクトの種類のサポート

既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。 .NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。 PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに "[移行](../consume-packages/migrate-packages-config-to-package-reference.md)" してから、packages.config を削除します。

完全な .NET Framework を対象とする ASP.NET アプリには、PackageReference の[制限されたサポート](https://github.com/NuGet/Home/issues/5877)しか追加されません。 C++ および JavaScript のプロジェクト タイプはサポートされていません。

## <a name="adding-a-packagereference"></a>PackageReference を追加する

次の構文を使用し、プロジェクト ファイルに依存関係を追加します。

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a>依存関係のバージョンを制御する

パッケージのバージョンを指定するための規則は、`packages.config` を使用する場合と同じです。

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../concepts/package-versioning.md#version-ranges)」 (パッケージ バージョン) にあります。

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a>PackageReference のないプロジェクトに PackageReference を使用する

詳細: プロジェクトにパッケージをインストールしていないが (プロジェクト ファイルに PackageReferences がなく、packages.config ファイルがない)、プロジェクトを PackageReference スタイルで復元する場合、プロジェクト ファイルで Project プロパティ RestoreProjectStyle を PackageReference に設定できます。

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

PackageReference スタイル (既存の csproj または SDK スタイルのプロジェクト) のプロジェクトを参照するとき、この設定が便利になることがあります。 そのようなプロジェクトが参照するパッケージを他のプロジェクトで "推移的に" 参照できます。

## <a name="packagereference-and-sources"></a>PackageReference とソース

PackageReference プロジェクトでは、推移的な依存関係バージョンは復元時に解決されます。 そのため、PackageReference プロジェクトでは、すべてのソースがすべての復元に使用できる必要があります。 

## <a name="floating-versions"></a>最新バージョン

[最新バージョン](../concepts/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a>依存関係アセットを制御する

開発ハーネスとしてのみ依存関係を使用するとき、それはパッケージを使用するプロジェクトに公開しないほうが好ましい場合があります。 このシナリオでは、`PrivateAssets` メタデータを使用し、この動作を制御できます。

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

次のメタデータ タグは依存関係アセットを制御します。

| タグ | 説明 | Default value |
| --- | --- | --- |
| IncludeAssets | これらのアセットは使用されます | すべて |
| ExcludeAssets | これらのアセットは使用されません | なし |
| PrivateAssets | これらのアセットは使用されますが、親プロジェクトに流れません | contentfiles;analyzers;build |

これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。

| 値 | 説明 |
| --- | ---
| compile | `lib` フォルダーの内容と、プロジェクトをフォルダー内のアセンブリに対してコンパイルできるかどうかのコントロール |
| runtime | `lib` と `runtimes` フォルダーの内容と、これらのアセンブリがコピーされて出力ディレクトリをビルドするかどうかのコントロール |
| contentFiles | `contentfiles` フォルダーの内容 |
| build | `build` フォルダー内の `.props` と `.targets` |
| buildMultitargeting | *(4.0)* `.props` フォルダー内の `.targets` と `buildMultitargeting` (フレームワーク間でのターゲット設定用) |
| buildTransitive | *(5.0 以降)* `.props` フォルダー内の `.targets` と `buildTransitive` (使用するプロジェクトに推移的にフローするアセット用)。 [機能](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior)に関するページをご覧ください。 |
| analyzers | .NET アナライザー |
| native | `native` フォルダーの内容 |
| なし | 上記のいずれも該当しない。 |
| すべて | 上記のすべて (`none` を除く) |

次の例では、パッケージからのコンテンツ ファイルを除くすべてがプロジェクトによって使用され、コンテンツ ファイルとアナライザーを除くすべてが親プロジェクトに流れます。

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに *流れる* ことに注目してください。 たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。 AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。

> [!NOTE]
> `.nuspec` ファイル内で `developmentDependency` が `true` に設定されている場合、パッケージが開発専用の依存関係としてマークされます。これにより、そのパッケージは他のパッケージに依存関係として含まれなくなります。 PackageReference *(NuGet 4.8 以降)* では、このフラグは、コンパイルからコンパイル時アセットを除外することも意味します。 詳しくは、「[DevelopmentDependency support for PackageReference (PackageReference に対する DevelopmentDependency のサポート)](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)」をご覧ください。

## <a name="adding-a-packagereference-condition"></a>PackageReference 条件を追加する

条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。 ただし、現在のところ `TargetFramework` 変数のみに対応しています。

たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。 その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。 それを回避するために、次のように `PackageReference` で条件を指定します。

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a>GeneratePathProperty

この機能を使用できるのは、NuGet **5.0** 以降で、かつ Visual Studio 2019 **16.0** 以降を使用している場合です。

場合によっては、MSBuild ターゲットからパッケージ内のファイルを参照することが望ましい場合があります。
`packages.config` ベースのプロジェクトでは、パッケージは、プロジェク トファイルに対して相対的なフォルダーにインストールされます。 ただし、PackageReference では、パッケージは "*グローバルパッケージ*" フォルダーから [使用](../concepts/package-installation-process.md)されます。このフォルダーは、マシンごとに異なる場合があります。

このギャップを埋めるために、NuGet では、パッケージの使用元となる場所を指すプロパティが導入されました。

例:

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

また、NuGet では、ツール フォルダーを含むパッケージのプロパティが自動的に生成されます。

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
```

MSBuild のプロパティとパッケージ ID には同じ制限がないため、パッケージ ID を MSBuild の表示名 (`Pkg` という語が接頭辞として付けられます) に変更する必要があります。
生成されたプロパティの正確な名前を確認するには、生成された [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) ファイルを調べます。

## <a name="packagereference-aliases"></a>PackageReference の別名

まれに、異なるパッケージに同じ名前空間のクラスが含まれている場合があります。 NuGet 5.7 および Visual Studio 2019 Update 7 以降、ProjectReference と同等の PackageReference は [`Aliases`](/dotnet/api/microsoft.codeanalysis.projectreference.aliases) をサポートしています。
既定では、別名は用意されていません。 別名が指定されている場合、注釈付きパッケージに由来する "*すべての*" アセンブリは、別名で参照する必要があります。

サンプルの使用方法については、[NuGet\Samples](https://github.com/NuGet/Samples/tree/main/PackageReferenceAliasesExample) を参照してください。

プロジェクト ファイルで、次のように別名を指定します。

```xml
  <ItemGroup>
    <PackageReference Include="NuGet.Versioning" Version="5.8.0" Aliases="ExampleAlias" />
  </ItemGroup>
```

また、コードで次のように使用します。

```cs
extern alias ExampleAlias;

namespace PackageReferenceAliasesExample
{
...
        {
            var version = ExampleAlias.NuGet.Versioning.NuGetVersion.Parse("5.0.0");
            Console.WriteLine($"Version : {version}");
        }
...
}

```

## <a name="nuget-warnings-and-errors"></a>NuGet の警告とエラー

"*この機能を使用できるのは、NuGet **4.3** 以降で、かつ Visual Studio 2017 **15.3** 以降を使用している場合です。* "

多くのパックと復元シナリオでは、すべての NuGet の警告とエラーがコード化され、`NU****` から始まります。 すべての NuGet の警告とエラーは、[リファレンス](../reference/errors-and-warnings.md) ドキュメントに記載されています。

NuGet では、次の警告プロパティが監視されます。

- `TreatWarningsAsErrors`: すべての警告をエラーとして扱います。
- `WarningsAsErrors`: 指定した警告をエラーとして扱います。
- `NoWarn`: 特定の警告を非表示にします (プロジェクト全体またはパッケージ全体)。

例 :

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a>NuGet 警告の非表示

パックと復元操作中にすべての NuGet 警告を解決することをお勧めしますが、特定の状況では、それらを非表示にすることが認められています。
プロジェクト全体で警告を非表示にするには、次のことを検討してください。

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

警告は、グラフ内の特定のパッケージにのみ適用されることがあります。 PackageReference 項目に `NoWarn` を追加することで、その警告をより選択的に非表示にすることができます。 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a>Visual Studio での NuGet パッケージ警告の非表示

Visual Studio では、IDE から[警告を非表示にする](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
)こともできます。

## <a name="locking-dependencies"></a>依存関係のロック

"*この機能を使用できるのは、NuGet **4.9** 以降で、かつ Visual Studio 2017 **15.9** 以降を使用している場合です。* "

NuGet の復元への入力は、プロジェクト ファイルのパッケージ参照のセット (最上位レベルまたは直接の依存関係) であり、出力は推移的依存関係を含むパッケージのすべての依存関係の完全なクロージャーです。 入力の PackageReference リストが変更されていない場合、NuGet では常に同じパッケージの依存関係の完全なクロージャーを生成しようとします。 ただし、このようにすることができないシナリオがいくつかあります。 次に例を示します。

* `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` などの浮動バージョンを使用する場合。 ここでの意図はパッケージの復元ごとに最新バージョンに浮動することですが、グラフを特定の最新バージョンにロックして、利用可能な場合は明示的なジェスチャに基づいて後続のバージョンに浮動させることをユーザーが求めるシナリオがあります。
* PackageReference のバージョン要件と一致する新しいパッケージのバージョンが公開されている場合。 例: 

  * 1 日目: `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` を指定したが、NuGet リポジトリで利用可能なバージョンが 4.1.0、4.2.0 および 4.3.0 だった場合。 この場合、NuGet は 4.1.0 (最小に最も近いバージョン) に解決されています。

  * 2 日目: バージョン 4.0.0 が公開されます。 NuGet では完全一致が検索され、4.0.0 への解決が始められます。

* 指定したパッケージ バージョンがリポジトリから削除される場合。 nuget.org ではパッケージの削除が許可されていませんが、すべてのパッケージ リポジトリがこの制約を持っているわけではありません。 これにより、削除されたバージョンに解決できない場合、NuGet では最適な一致が検索されます。

### <a name="enabling-lock-file"></a>ロック ファイルの有効化

パッケージの依存関係の完全なクロージャーを保持するために、プロジェクトに対して MSBuild プロパティ `RestorePackagesWithLockFile` を設定して、ロック ファイル機能にオプトインすることができます。

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

このプロパティが設定されている場合、NuGet の復元でロック ファイル (すべてのパッケージの依存関係を一覧表示する `packages.lock.json` ファイル) が生成されます。 

> [!Note]
> プロジェクトのルート ディレクトリに `packages.lock.json` ファイルが含まれている場合、プロパティ `RestorePackagesWithLockFile` が設定されていない場合でも、常に復元でロック ファイルが使用されます。 そのため、この機能にオプトインする別の方法は、プロジェクトのルート ディレクトリに空の `packages.lock.json` ファイルをダミーとして作成することです。

### <a name="restore-behavior-with-lock-file"></a>ロック ファイルでの `restore` の動作
プロジェクトにロック ファイルが存在する場合、NuGet では `restore` を実行するためにこのロック ファイルが使用されます。 プロジェクト ファイル (または依存プロジェクトのファイル) で言及されたパッケージの依存関係に変更があったかどうか確認するために、NuGet で簡単なチェックが行われます。変更がなかった場合は、ロック ファイルで言及されたパッケージを単純に復元します。 パッケージの依存関係を再評価することはありません。

NuGet によって、プロジェクト ファイルで言及したような定義された依存関係の変更が検出された場合、パッケージ グラフが再評価され、プロジェクトの新しいパッケージ クロージャを反映するためにロック ファイルが更新されます。

実行中にパッケージの依存関係を変更したくない CI/CD やその他のシナリオでは、`lockedmode` を `true` に設定することでこれを実行できます。

dotnet.exe の場合は、次を実行します。

```
> dotnet.exe restore --locked-mode
```

msbuild.exe の場合は、次を実行します。

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

自分のプロジェクト ファイルにもこの条件付き MSBuild プロパティを設定できます。

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

ロック モードが `true` である場合、復元ではロック ファイルに記載されている正確なパッケージが復元されるか、または、ロック ファイルの作成後にプロジェクトの定義されたパッケージの依存関係を更新した場合は、失敗します。

### <a name="make-lock-file-part-of-your-source-repository"></a>ロック ファイルをソース リポジトリの一部にする
アプリケーションを作成する場合、目的の実行可能ファイルとプロジェクトは依存関係チェーンの最初に位置します。NuGet が復元中にこれを使用できるように、ロック ファイルをソース コード リポジトリにチェックインします。

ただし、当該プロジェクトが出荷しないライブラリ プロジェクトである場合や、他のプロジェクトが依存する共通コード プロジェクトである場合は、ソース コードの一部としてロック ファイルをチェックイン **しないでください**。 ロック ファイルを保持しても問題はありませんが、共通コード プロジェクトのロックされているパッケージの依存関係は、ロック ファイル内で記載されているように、この共通コード プロジェクトに依存するプロジェクトの復元/ビルド中に使用されない場合があります。

例:

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

`ProjectA` が `PackageX` のバージョン `2.0.0` に依存し、`PackageX` のバージョン `1.0.0` に依存する `ProjectB` も参照している場合、`ProjectB` のロック ファイルでは `PackageX` のバージョン `1.0.0` に対する依存関係が記載されます。 ただし、`ProjectA` をビルドすると、そのロック ファイルには `PackageX` のバージョン **`2.0.0`** に対する依存関係が含まれます。**のロック ファイルに記載されている** では`1.0.0`ありません`ProjectB`。 したがって、共通コード プロジェクトのロックファイルは、それが依存するプロジェクトのために解決されるパッケージに対して強い力を持っていません。

### <a name="lock-file-extensibility"></a>ロック ファイルの拡張機能

以下で説明するように、ロック ファイルを使用して復元のさまざまな動作を制御できます。

| NuGet.exe オプション | dotnet オプション | 対応する MSBuild オプション | 説明 |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | RestorePackagesWithLockFile | ロック ファイルの使用をオプトインします。 |
| `-LockedMode` | `--locked-mode` | RestoreLockedMode | 復元のロック モードを有効にします。 これは、繰り返し可能なビルドを必要とする CI/CD のシナリオで役立ちます。|   
| `-ForceEvaluate` | `--force-evaluate` | RestoreForceEvaluate | このオプションは、プロジェクトで定義する浮動バージョンを使用するパッケージで役立ちます。 既定では、NuGet の復元では、このオプションを指定して復元を実行しない限り、復元ごとのパッケージ バージョンの自動更新は行われません。 |
| `-LockFilePath` | `--lock-file-path` | NuGetLockFilePath | プロジェクトのカスタム ロック ファイルの場所を定義します。 既定では、NuGet はルート ディレクトリでの `packages.lock.json` をサポートします。 同じディレクトリ内に複数のプロジェクトがある場合、NuGet はプロジェクト固有のロック ファイル `packages.<project_name>.lock.json` をサポートします。 |

## <a name="assettargetfallback"></a>AssetTargetFallback

`AssetTargetFallback` プロパティを使用すると、プロジェクトから参照されるプロジェクトの互換性のある追加のフレームワーク バージョンと、プロジェクトに使用する NuGet パッケージを指定できます。

`PackageReference` を使用してパッケージの依存関係を指定し、そのパッケージにプロジェクトのターゲット フレームワークと互換性のある資産が含まれない場合は、`AssetTargetFallback` プロパティが機能します。 参照されたパッケージの互換性は、`AssetTargetFallback` で指定された各ターゲット フレームワークを使用して再確認されます。
`project` または `package` が `AssetTargetFallback` によって参照されている場合、[NU1701](../reference/errors-and-warnings/NU1701.md) 警告が表示されます。

`AssetTargetFallback` が互換性に与える影響の例については、次の表を参照してください。

| プロジェクト フレームワーク | AssetTargetFallback | パッケージ フレームワーク | 結果 |
|-------------------|---------------------|--------------------|--------|
| .NET Framework 4.7.2 | | .NET Standard 2.0 | .NET Standard 2.0 |
| .NET Core App 3.1 | | .NET Standard 2.0、.NET Framework 4.7.2 | .NET Standard 2.0 |
| .NET Core App 3.1 | | .NET Framework 4.7.2 | 互換性がありません。[`NU1202`](../reference/errors-and-warnings/NU1202.md) で失敗します |
| .NET Core App 3.1 | net472;net471 | .NET Framework 4.7.2 | .NET Framework 4.7.2。[`NU1701`](../reference/errors-and-warnings/NU1701.md) が表示されます |

`;` を区切り記号として使用して、複数のフレームワークを指定できます。 フォールバック フレームワークを追加するには、次の操作を行います。

```xml
<AssetTargetFallback Condition=" '$(TargetFramework)'=='netcoreapp3.1' ">
    $(AssetTargetFallback);net472;net471
</AssetTargetFallback>
```

既存の `AssetTargetFallback` 値に追加するのではなく、上書きする場合は、`$(AssetTargetFallback)` は省略できます。

> [!NOTE]
> [.NET SDK ベースのプロジェクト](/dotnet/core/sdk)を使用している場合は、適切な `$(AssetTargetFallback)` 値が構成されるため、手動で設定する必要はありません。
>
> `$(PackageTargetFallback)` は、この課題に対処しようとした初期の機能でしたが、根本的には破損しているため、使用 "*しないでください*"。 `$(PackageTargetFallback)` から `$(AssetTargetFallback)` に移行するには、プロパティ名を変更するだけです。
