---
title: "Visual Studio プロジェクト ファイルの NuGet PackageReference | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "NuGet 4.0+ と VS2017 でサポートされているプロジェクト ファイルの NuGet PackageReference に関する詳細"
keywords: "NuGet パッケージ依存性, パッケージ参照, プロジェクト ファイル, PackageReference, packages.config, project.json, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c8fc9e558557af444d9a35ace36d043a5f6382a7
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-references-packagereference-in-project-files"></a>プロジェクト ファイルのパッケージ参照 (PackageReference)

パッケージ参照では、`PackageReference` ノードを使用することで、プロジェクト ファイル内で直接、NuGet 依存関係を管理できます。個別の `packages.config` または `project.json` ファイルが不要になります。 この方法は NuGet の他の側面に影響を与えません。たとえば、`NuGet.Config` ファイルの設定は (パッケージ ソースを含む)、「[Configuring NuGet Behavior](Configuring-NuGet-Behavior.md)」 (NuGet 動作の構成) の説明にあるように、依然として適用されます。

> [!Important]
> 現在のところ、.NET Core プロジェクト、.NET Standard プロジェクト、Windows 10 Build 15063 (Creators Update) を対象とする UWP プロジェクトに関して、パッケージ参照は Visual Studio 2017 でのみサポートされています。

`PackageReference` 手法では、MSBuild 条件を使用し、ターゲット フレームワーク、構成、プラットフォーム、その他のグループ化ごとにパッケージ参照を選択できます。 依存関係とコンテンツ フローを細かく制御することもできます。 動作と[依存関係の解決](Dependency-Resolution.md)の観点からは、`project.json` を使用する場合と同じになります。

MSBuild とプロジェクト ファイルのパッケージ参照の統合については、「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md)」 (MSBuild ターゲットとしての NuGet pack および restore) を参照してください。

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

パッケージのバージョンを指定するための規則は、`packages.config` または `project.json` を使用する場合と同じです。

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

上記の例では、3.6.0 は 3.6.0 以上のあらゆるバージョンを意味し、最も下のバージョンが優先されます。詳細は、「[Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards)」 (パッケージ バージョン) にあります。

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

| 値 | 説明 |
| --- | ---
| compile | `lib` フォルダーの内容 |
| ランタイム | `runtime` フォルダーの内容 |
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
