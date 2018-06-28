---
title: NuGet PackageReference 形式 (プロジェクト ファイルのパッケージ参照)
description: NuGet 4.0 以降と VS2017 および .NET Core 2.0 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 61f447877459764906cf9a2b88b32a8bc0553689
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817672"
---
# <a name="package-references-packagereference-in-project-files"></a>プロジェクト ファイルのパッケージ参照 (PackageReference)

`PackageReference` ノードを使用するパッケージ参照では、(個別の `packages.config` ファイルとは異なり) NuGet の依存関係をプロジェクト ファイル内で直接管理します。 PackageReference の呼び出しは、NuGet の他の側面には影響を与えません。たとえば、(パッケージ ソースを含む) `NuGet.Config` ファイルの設定が適用されます。詳細については、「[NuGet の動作を構成する](configuring-nuget-behavior.md)」を参照してください。

PackageReference の場合、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択することもできます。 依存関係とコンテンツ フローを細かく制御することもできます。 (詳細については、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」(MSBuild ターゲットとしての NuGet のパックと復元) を参照してください)。

既定では、PackageReference は、Windows 10 Build 15063 (Creators Update) 以降を対象とする .NET Core プロジェクト、.NET Standard プロジェクト、および UWP プロジェクトに使用されます。ただし、C++ UWP プロジェクトは例外です。 完全な .NET Framework プロジェクトは PackageReference をサポートしていますが、現在の既定は `packages.config` です。 PackageReference を使用するには、依存関係を `packages.config` からプロジェクト ファイルに移行し、packages.config を削除します。

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
| IncludeAssets | これらのアセットは使用されます | すべて |
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

`build` は `PrivateAssets` で含まれないため、targets と props は親プロジェクトに*流れる*ことに注目してください。 たとえば、上記の参照は、AppLogger という名前の NuGet パッケージをビルドするプロジェクトで使用されます。 AppLogger は、AppLogger を使用するプロジェクトと同様に、`Contoso.Utility.UsefulStuff` から targets と props を使用できます。

## <a name="adding-a-packagereference-condition"></a>PackageReference 条件を追加する

条件を使用し、パッケージを含めるかどうかを制御できます。条件では、あらゆる MSBuild 変数や、targets または props ファイルに定義されている変数を使用できます。 ただし、現在のところ `TargetFramework` 変数のみに対応しています。

たとえば、`net452` と共に `netstandard1.4` を対象とするが、`net452` にのみ該当する依存関係があるとします。 その場合、パッケージを使用する `netstandard1.4` プロジェクトでは、その不要な依存関係を追加することが望まれません。 それを回避するために、次のように `PackageReference` で条件を指定します。

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

このプロジェクトでビルドされたパッケージには、`net452` ターゲットのみの依存関係として Newtonsoft.json が追加されることが示されます。

![VS2017 で PackageReference に条件を適用した結果](media/PackageReference-Condition.png)

条件は `ItemGroup` レベルでも適用できます。また、条件はすべての子 `PackageReference` 要素に適用されます。

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
