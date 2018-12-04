---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照)
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: d4f0177183ee3edf595c4ce10d1f26cbaca5755d
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453573"
---
# <a name="package-references-packagereference-in-project-files"></a>プロジェクト ファイルのパッケージ参照 (PackageReference)

`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。 PackageReference の呼び出しは、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.config` ファイルの設定が適用されます。詳細については、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」を参照してください。

PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択することもできます。 依存関係とコンテンツ フローを細かく制御することもできます。 (詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。

既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。 .NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。 PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに移行し、packages.config を削除します。

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

上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」 (パッケージ バージョン) にあります。

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

## <a name="floating-versions"></a>最新バージョン

[最新バージョン](../consume-packages/dependency-resolution.md#floating-versions)が `PackageReference` でサポートされています。

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

| タグ | 説明 | 既定値 |
| --- | --- | --- |
| IncludeAssets | これらのアセットは使用されます | all |
| ExcludeAssets | これらのアセットは使用されません | none |
| PrivateAssets | これらのアセットは使用されますが、親プロジェクトに流れません | contentfiles;analyzers;build |

これらのタグに使用できる値は次のようになります。単独で表示する `all` と `none` を除き、複数の値はセミコロンで区切られます。

| [値] | 説明 |
| --- | ---
| compile | `lib` フォルダーの内容と、プロジェクトをフォルダー内のアセンブリに対してコンパイルできるかどうかのコントロール |
| ランタイム | `lib` と `runtimes` フォルダーの内容と、これらのアセンブリがコピーされて出力ディレクトリをビルドするかどうかのコントロール |
| contentFiles | `contentfiles` フォルダーの内容 |
| ビルド | `build` フォルダーの props と targets |
| analyzers | .NET アナライザー |
| native | `native` フォルダーの内容 |
| none | 上記のいずれも該当しない。 |
| all | 上記のすべて (`none` を除く) |

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

`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに*流れる*ことに注目してください。 たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。 AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。

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

## <a name="locking-dependencies"></a>依存関係のロック
"*この機能を使用できるのは、NuGet **4.9** 以降で、かつ Visual Studio 2017 **15.9 Preview 5** 以降を使用している場合です。*"

NuGet の復元への入力は、プロジェクト ファイルのパッケージ参照のセット (最上位レベルまたは直接の依存関係) であり、出力は推移的依存関係を含むパッケージのすべての依存関係の完全なクロージャーです。 入力の PackageReference リストが変更されていない場合、NuGet では常に同じパッケージの依存関係の完全なクロージャーを生成しようとします。 ただし、このようにすることができないシナリオがいくつかあります。 例:

* `<PackageReference Include="My.Sample.Lib" Version="4.*"/>` などの浮動バージョンを使用する場合。 ここでの意図はパッケージの復元ごとに最新バージョンに浮動することですが、グラフを特定の最新バージョンにロックして、利用可能な場合は明示的なジェスチャに基づいて後続のバージョンに浮動させることをユーザーが求めるシナリオがあります。
* PackageReference のバージョン要件と一致する新しいパッケージのバージョンが公開されている場合。 たとえば、 

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
アプリケーションを作成する場合、目的の実行可能ファイルとプロジェクトは依存関係チェーンの最後に位置します。NuGet が復元中にこれを使用できるように、ロック ファイルをソース コード リポジトリにチェックインします。

ただし、当該プロジェクトが出荷しないライブラリ プロジェクトである場合や、他のプロジェクトが依存する共通コード プロジェクトである場合は、ソース コードの一部としてロック ファイルをチェックイン**しないでください**。 ロック ファイルを保持しても問題はありませんが、共通コード プロジェクトのロックされているパッケージの依存関係は、ロック ファイル内で記載されているように、この共通コード プロジェクトに依存するプロジェクトの復元/ビルド中に使用されない場合があります。

例:
```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```
`ProjectA` が `PackageX` のバージョン `2.0.0` に依存し、`PackageX` のバージョン `1.0.0` に依存する `ProjectB` も参照している場合、`ProjectB` のロック ファイルでは `PackageX` のバージョン `1.0.0` に対する依存関係が記載されます。 ただし、`ProjectA` をビルドすると、そのロック ファイルには `PackageX` のバージョン **`2.0.0`** に対する依存関係が含まれます。`ProjectB` のロック ファイルに記載されている `1.0.0` では**ありません**。 したがって、共通コード プロジェクトのロックファイルは、それが依存するプロジェクトのために解決されるパッケージに対して強い力を持っていません。

### <a name="lock-file-extensibility"></a>ロック ファイルの拡張機能
以下で説明するように、ロック ファイルを使用して復元のさまざまな動作を制御できます。

| オプション | 対応する MSBuild オプション | 
|:---  |:--- |
| `--use-lock-file` | プロジェクトのロック ファイルでのブートス トラップの使用です。 代わりに、プロジェクト ファイル内で `RestorePackagesWithLockFile` プロパティを設定することもできます。 | 
| `--locked-mode` | 復元のロック モードを有効にします。 これは、繰り返し可能なビルドを取得する必要がある CI/CD のシナリオで役立ちます。 または、`RestoreLockedMode` MSBuild プロパティを `true` に設定する方法もあります。 |  
| `--force-evaluate` | このオプションは、プロジェクトで定義する浮動バージョンを使用するパッケージで役立ちます。 既定では、NuGet の復元では、`--force-evaluate` オプションを使用して復元を実行しない限り、各復元に基づくパッケージ バージョンの自動更新は行われません。 |
| `--lock-file-path` | プロジェクトのカスタム ロック ファイルの場所を定義します。 これは、MSBuild プロパティ `NuGetLockFilePath` を設定することでも実現できます。 既定では、NuGet はルート ディレクトリでの `packages.lock.json` をサポートします。 同じディレクトリ内に複数のプロジェクトがある場合、NuGet はプロジェクト固有のロック ファイル `packages.<project_name>.lock.json` をサポートします。 |
