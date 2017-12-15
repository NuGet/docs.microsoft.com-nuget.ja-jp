---
title: "NuGet パッケージのバージョンのリファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee3c826-dd3a-4fa9-863f-1fd80bc4230f
description: "バージョン番号と NuGet パッケージ、依存しているとの依存関係がどのようにインストールするのには、他のパッケージの範囲を指定する方法の詳細。"
keywords: "バージョン管理、NuGet パッケージの依存関係、NuGet の依存関係のバージョン、NuGet のバージョン番号、NuGet パッケージのバージョン、バージョン範囲、バージョン指定、正規化されたバージョン番号"
ms.reviewer:
- anandr
- karann-msft
- unniravindranathan
ms.openlocfilehash: 25b74ab629cab0fff7114bf1621606de5fc18dd2
ms.sourcegitcommit: 89bb9d429c19ff69084c35acad09daea3e16d56b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-versioning"></a>パッケージのバージョン管理

特定のパッケージは常に、そのパッケージの識別子と厳密なバージョン番号を使用する参照します。 たとえば、 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org がいくつか十特定使用可能なパッケージをバージョンからまで*4.1.10311*バージョン*6.1.3* (、最新の安定しました。リリース) などのさまざまなリリース前のバージョンおよび*6.2.0-beta1*です。

パッケージを作成するときに、省略可能なプレリリース テキスト サフィックスを持つ特定のバージョン番号を割り当てます。 その一方で、パッケージを使用する際に、厳密なバージョン番号または許容可能なバージョンの範囲のいずれかを指定できます。

このトピックの内容

- [バージョンの基礎](#version-basics)プレリリース サフィックスを含むです。
- [バージョン範囲およびワイルドカード](#version-ranges-and-wildcards)
- [正規化されたバージョン番号](#normalized-version-numbers)

## <a name="version-basics"></a>バージョンの基礎

特定のバージョン番号の形式は*Major.Minor.Patch [-サフィックス]*意味は次のコンポーネントのある、します。

- *主要な*: 重大な変更
- *マイナー*: 下位互換性のあるの新機能
- *修正プログラム*: 旧バージョンと互換性のあるバグの修正のみ
- *-サフィックス*(省略可能): リリース前のバージョンを示す文字列でハイフンの後ろに (以下、[セマンティック バージョニングまたは SemVer 1.0 規約](http://semver.org/spec/v1.0.0.html))。

**例:**
```
1.0.1
6.11.1231
4.3.1-rc
2.2.44-beta1
```

> [!Important]
> nuget.org は、厳密なバージョン番号が欠落しているパッケージのアップロードを拒否します。 バージョンを指定する必要があります、`.nuspec`またはプロジェクト ファイルにパッケージを作成するために使用します。

### <a name="pre-release-versions"></a>プレリリース版

技術的には、パッケージの作成者できる任意の文字列をサフィックスとして使用を NuGet がプレリリースとしてこのような任意のバージョンを処理し、他の解釈も負わないものとは、リリース前のバージョンを示すためにします。 NuGet 表示がどのような UI で、フル バージョンの文字列が含まれている、コンシューマーにサフィックスの意味の解釈を終了します。

ただし、パッケージの開発者は一般に認識されている名前付け規則に従います。

- `-alpha`: アルファ リリースでは、通常処理中と実験に使用します。
- `-beta`: ベータ リリース、通常 1 つは、次の完全な機能のリリースでは、計画的なが既知のバグを含めることができます。
- `-rc`: リリース候補、最終的な可能性がありますが、リリース通常重大なバグが出現しない限り、(stable) です。

> [!Note]
> NuGet 4.3.0+ をサポートしている[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)、する番号をサポートするプレリリース ドット付き表記でとして*1.0.1-build.23*です。 4.3.0 前に、のバージョンの NuGet では、ドット表記はサポートされていません。 ようにフォームを使用して*1.0.1-build23*です。

パッケージ参照および複数のパッケージ バージョンのみが異なるサフィックスを解決するには、NuGet は最初に、サフィックスが付いていないバージョンを選択し、プレリリース版では、アルファベットの逆順に優先順位を適用します。 たとえば、次のバージョンが示されている正確な順序で選択されます。

```
1.0.1
1.0.1-zzz
1.0.1-rc
1.0.1-open
1.0.1-beta
1.0.1-alpha2
1.0.1-alpha
1.0.1-aaa
```

## <a name="semantic-versioning-200"></a>セマンティック バージョニング 2.0.0

NuGet をサポートしている NuGet 4.3.0+ と Visual Studio 2017 バージョン 15.3 +、[セマンティック バージョニング 2.0.0](http://semver.org/spec/v2.0.0.html)です。

SemVer v2.0.0 の特定のセマンティクスは、以前のクライアントではサポートされていません。 NuGet では、パッケージのバージョンが SemVer v2.0.0 固有である場合は true、次のステートメントのいずれかを検討します。

- プレリリース ラベルはドット区切り、たとえば、 *1.0.0-alpha.1*
- バージョンには、ビルドのメタデータ、たとえば、 *1.0.0+githash*

Nuget.org をパッケージが定義されて SemVer v2.0.0 パッケージとして、次のステートメントのいずれかが true の場合。

- パッケージのバージョンでは、上記で定義された SemVer v2.0.0 準拠していませんが、準拠していない SemVer v1.0.0 です。
- 最小値または最大なバージョンが SemVer v2.0.0 準拠していませんが、準拠していない SemVer v1.0.0; 上で定義したパッケージの依存関係のバージョンの範囲のいずれかがあります。たとえば、 *[1.0.0-alpha.1,)*です。

Nuget.org に SemVer v2.0.0 に固有のパッケージをアップロードする場合、パッケージを古いクライアントに非表示とは使用する次の NuGet クライアントのみ。

- NuGet 4.3.0+
- Visual Studio 2017 バージョン 15.3 + 
- dotnet.exe (.NET SDK 2.0.0+)

サード パーティ製のクライアント:

- JetBrains 名
- Version 5.0 以降のパケットを作成します。

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>バージョン範囲およびワイルドカード

パッケージの依存関係の場合は、次のとおり、バージョン範囲を指定する間隔の表記を使用して NuGet をサポートします。

| Notation | 適用されるルール | 説明 |
|----------|--------------|-------------|
| 1.0 | 1.0 ≤ x | 包括的な最小のバージョン |
| (1.0,) | 1.0 < x | 排他の最小バージョン |
| [1.0] | x = = 1.0 | バージョンに一致します。 |
| (,1.0] | x ≤ 1.0 | 包括的に、最大のバージョン |
| (,1.0) | x < 1.0 | 排他の最大バージョン |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 正確な範囲を包括的 |
| (1.0,2.0) | 1.0 < < 2.0 x | 正確な範囲、排他 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 包括的な最小値と排他最大バージョンが混在 |
| (1.0)    | 無効な | 無効な |

PackageReference を使用する場合または`project.json`参照形式、NuGet パッケージのワイルドカードの表記法を使用してサポートも\*メジャー、マイナー、Patch、および数のプレリリース版サフィックス部分。 ワイルドカードはサポートされていません、`packages.config`形式です。

> [!Note]
> バージョン範囲を解決するときに、プレリリース バージョンは含まれません。 プレリリース版*は*、ワイルドカードを使用するときに含まれます (\*)。 バージョン範囲*[1.0,2.0]*、たとえば、含まない 2.0 のベータ版ではワイルドカードの表記法_2.0-*_はします。 参照してください[発行 912](https://github.com/NuGet/Home/issues/912)プレリリース ワイルドカードの詳細についてはします。

### <a name="examples"></a>例

常に、プロジェクト ファイル内のバージョンまたはパッケージの依存関係のバージョンの範囲を指定`packages.config`ファイル、および`.nuspec`ファイル。 バージョンまたはバージョン範囲、NuGet のない 2.8.x 以前選択して、最新の利用可能なパッケージ、依存関係を解決するときに対し NuGet 3.x し、後で、最小のパッケージ バージョンを選択します。 バージョンまたはバージョン範囲は、この不確実性を回避できます。 を指定します。

#### <a name="references-in-project-files-packagereference"></a>プロジェクト ファイル (PackageReference) 内の参照

```xml
<!-- Accepts any version 6.1 and above. -->
<PackageReference Include="ExamplePackage" Version="6.1" />

<!-- Accepts any 6.x.y version. -->
<PackageReference Include="ExamplePackage" Version="6.*" />
<PackageReference Include="ExamplePackage" Version="[6,7)" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<PackageReference Include="ExamplePackage" Version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<PackageReference Include="ExamplePackage" Version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<PackageReference Include="ExamplePackage" Version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<PackageReference Include="ExamplePackage" Version="[1.3.2,1.5)" />
```

**参照`packages.config`:**

`packages.config`、すべての依存関係が記載されている完全な`version`パッケージを復元するときに使用される属性です。 `allowedVersions`属性は、パッケージを更新する可能性があるバージョンを制限する更新操作中にのみ使用します。

```xml
<!-- Install/restore version 6.1.0, accept any version 6.1.0 and above on update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="6.1.0" />

<!-- Install/restore version 6.1.0, and do not change during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6.1.0]" />

<!-- Install/restore version 6.1.0, accept any 6.x version during update. -->
<package id="ExamplePackage" version="6.1.0" allowedVersions="[6,7)" />

<!-- Install/restore version 4.1.4, accept any version above, but not including, 4.1.3.
     Could be used to guarantee a dependency with a specific bug fix. -->
<package id="ExamplePackage" version="4.1.4" allowedVersions="(4.1.3,)" />

<!-- Install/restore version 3.1.2, accept any version up below 5.x on update, which might be
     used to prevent pulling in a later version of a dependency that changed its interface.
     However, this form is not recommended because it can be difficult to determine the lowest version. -->
<package id="ExamplePackage" version="3.1.2" allowedVersions="(,5.0)" />

<!-- Install/restore version 1.1.4, accept any 1.x or 2.x version on update, but not
     0.x or 3.x and higher. -->
<package id="ExamplePackage" version="1.1.4" allowedVersions="[1,3)" />

<!-- Install/restore version 1.3.5, accepts 1.3.2 up to 1.4.x on update, but not 1.5 and higher. -->
<package id="ExamplePackage" version="1.3.5" allowedVersions="[1.3.2,1.5)" />
```

**参照`.nuspec`ファイル**

`version`属性、`<dependency>`要素に依存関係として受け入れ可能な範囲のバージョンを記述します。

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

<!-- Accepts any 6.x.y version. -->
<dependency id="ExamplePackage" version="6.*" />

<!-- Accepts any version above, but not including 4.1.3. Could be
     used to guarantee a dependency with a specific bug fix. -->
<dependency id="ExamplePackage" version="(4.1.3,)" />

<!-- Accepts any version up below 5.x, which might be used to prevent pulling in a later
     version of a dependency that changed its interface. However, this form is not
     recommended because it can be difficult to determine the lowest version. -->
<dependency id="ExamplePackage" version="(,5.0)" />

<!-- Accepts any 1.x or 2.x version, but not 0.x or 3.x and higher. -->
<dependency id="ExamplePackage" version="[1,3)" />

<!-- Accepts 1.3.2 up to 1.4.x, but not 1.5 and higher. -->
<dependency id="ExamplePackage" version="[1.3.2,1.5)" />
```

## <a name="normalized-version-numbers"></a>正規化されたバージョン番号

> [!Note]
> これは、NuGet 3.4 以降では、互換性に影響する変更です。

再インストール、または復元操作のインストール中に、リポジトリからパッケージを取得するときに NuGet 3.4 以降はバージョン番号を次のように処理します。

- 先頭の 0 は、バージョン番号から削除されます。

    ```
    1.00 is treated as 1.0
    1.01.1 is treated as 1.1.1
    1.00.0.1 is treated as 1.0.0.1
    ```

- バージョン番号の 4 番目の部分のゼロは省略されます。

    ```
    1.0.0.0 is treated as 1.0.0
    1.0.01.0 is treated as 1.0.1
    ```

この正規化には、パッケージ自体; のバージョン番号は変わりません。のみ方法 NuGet と一致するバージョンの依存関係を解決するときに影響します。

ただし、NuGet パッケージのリポジトリと同じ方法で NuGet パッケージのバージョンの重複を防ぐためにこれらの値を処理する必要があります。 バージョンを格納するリポジトリしたがって*1.0*パッケージの必要がありますもホストしていないバージョン*1.0.0*独立した異なるパッケージとして。
