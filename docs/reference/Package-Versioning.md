---
title: NuGet パッケージのバージョンの参照
description: バージョン番号、およびその他のパッケージ、依存する NuGet パッケージと依存関係をインストールする方法の範囲を指定する方法の詳細。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: b980c1084fe8e31573053a4dcf38bbfa6146e6de
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549774"
---
# <a name="package-versioning"></a>パッケージのバージョン管理

特定のパッケージは、パッケージの識別子と正確なバージョン番号を使用して常に参照されます。 たとえば、 [Entity Framework](https://www.nuget.org/packages/EntityFramework/) nuget.org ではいくつか数十特定使用可能なパッケージをバージョンからまで*4.1.10311*バージョン*6.1.3* (、最新の安定しました。リリース) などのさまざまなリリース前バージョンと*6.2.0-beta1*します。

パッケージを作成する場合は、省略可能なプレリリース テキスト サフィックスを含む特定のバージョン番号を割り当てます。 その一方で、パッケージを利用する場合は、正確なバージョン番号または許容可能なバージョンの範囲のいずれかを指定できます。

このトピックの内容:

- [バージョンの基本](#version-basics)プレリリースのサフィックスを含むです。
- [バージョン範囲およびワイルドカード](#version-ranges-and-wildcards)
- [正規化されたバージョン番号](#normalized-version-numbers)

## <a name="version-basics"></a>バージョンの基本

特定のバージョン番号が、 *Major.Minor.Patch [-サフィックス]* コンポーネントは次の意味。

- *主要な*: 重大な変更
- *マイナー*: 下位互換性がありますが、新機能
- *パッチ*: 下位互換性のバグ修正のみ
- *-サフィックス*(省略可能): ハイフンが続けてリリース前のバージョンを示す文字列 (以下、[セマンティック バージョン管理または SemVer 1.0 規則](http://semver.org/spec/v1.0.0.html))。

**例:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org では、正確なバージョン番号が不足しているパッケージのアップロードを拒否します。 バージョンを指定する必要があります、`.nuspec`またはプロジェクト ファイルのパッケージを作成するために使用します。

### <a name="pre-release-versions"></a>プレリリース版

厳密に言うと、パッケージ作成者は任意の文字列をサフィックスとして使用を NuGet がこのような任意のバージョンをプレリリースとして扱います、他の解釈も負わないものとは、リリース前のバージョンを示すためにします。 つまり、すべての UI で、完全なバージョンの文字列、NuGet が表示されますが関係しているコンシューマーにサフィックスの意味の解釈を離れること。

ただし、通常、パッケージの開発者に、認識されている名前付け規則。

- `-alpha`: アルファ リリース、通常処理中や実験に使用します。
- `-beta`: ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。
- `-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。

> [!Note]
> NuGet 4.3.0 サポート[SemVer 2.0.0](http://semver.org/spec/v2.0.0.html)とプレリリース番号をドット表記をサポートする*1.0.1-build.23*します。 ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。 ようなフォームを使用して*1.0.1-build23*します。

パッケージ参照と複数のパッケージ バージョンのみが異なるサフィックスを解決するには、NuGet は最初に、サフィックスが付いていないバージョンを選択し、アルファベットの逆順のプレリリース版に優先順位を適用します。 たとえば、次のバージョンが示されている正確な順序で選択されます。

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>セマンティック バージョニング 2.0.0

NuGet 4.3.0 と Visual Studio 2017 バージョン 15.3 以降、NuGet をサポート[セマンティック バージョニング 2.0.0](http://semver.org/spec/v2.0.0.html)します。

以前のクライアントでは、SemVer v2.0.0 の特定のセマンティクスはサポートされていません。 NuGet では、次のステートメントのいずれかが true の場合、SemVer v2.0.0 を特定するパッケージのバージョンと見なされます。

- プレリリース版は、ラベルはドットで区切られた、たとえば、 *1.0.0-alpha.1*
- バージョンは、ビルド メタデータ、たとえば、 *1.0.0+githash*

Nuget.org の場合、次のステートメントのいずれかが true の場合、パッケージは SemVer v2.0.0 パッケージとして定義されます。

- パッケージのバージョンでは、上記で定義された SemVer v2.0.0 の準拠が準拠していない SemVer v1.0.0 です。
- パッケージの依存関係のバージョン範囲には SemVer v2.0.0 の準拠が準拠していない SemVer v1.0.0; 上で定義した、最小値または最大バージョンたとえば、 *[1.0.0-alpha.1,)* します。

SemVer v2.0.0 固有のパッケージを nuget.org にアップロードする場合、パッケージは、以前のクライアントを非表示と次の NuGet クライアントのみに使用可能なは。

- NuGet 4.3.0
- Visual Studio 2017 バージョン 15.3 以降
- Visual Studio 2015 と[NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

サード パーティ製のクライアント:

- JetBrains Rider
- バージョン 5.0 以降のパケットを作成します。

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>バージョン範囲およびワイルドカード

パッケージの依存関係を参照する、NuGet では、次のとおり、バージョン範囲を指定する間隔の表記を使用してサポートしています。

| Notation | 適用されるルール | 説明 |
|----------|--------------|-------------|
| 1 | x ≥ 1.0 | 包括的な最小のバージョン |
| (1.0,) | x > 1.0 | 排他の最小バージョン |
| [1.0] | x = 1.0 | バージョンに一致します。 |
| (,1.0] | x ≤ 1.0 | 包括の最大バージョン |
| (,1.0) | x < 1.0 | 排他の最大バージョン |
| [1.0,2.0] | 1.0 ≤ ≤ 2.0 | 正確な範囲は、包含 |
| (1.0,2.0) | 1.0 < x < 2.0 | 正確な範囲は、排他的 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 包括的な最小値と排他最大バージョンが混在 |
| (1.0)    | 無効な | 無効な |

PackageReference 形式を使用して、NuGet もサポートしています、ワイルドカードの表記を使用して\*メジャー、マイナー、パッチ、および、番号のプレリリースのサフィックス部分。 ワイルドカードはサポートされていません、`packages.config`形式。

> [!Note]
> バージョン範囲を解決するときに、プレリリース版は含まれません。 プレリリース版*は*ワイルドカードを使用する場合に含まれる (\*)。 バージョン範囲 *[1.0,2.0]* などは含まれませんが、2.0 ベータ版、ワイルドカードの表記法_2.0-*_ は。 参照してください[発行 912](https://github.com/NuGet/Home/issues/912)プレリリース版のワイルドカードの詳細についてはします。

### <a name="examples"></a>使用例

常にプロジェクト ファイルで、バージョン、またはパッケージの依存関係のバージョンの範囲を指定`packages.config`ファイル、および`.nuspec`ファイル。 バージョンまたはバージョン範囲、NuGet を使用せず 2.8.x 以前選択最新バージョンの使用可能なパッケージを依存関係を解決するときに、NuGet 3.x を後で、最小のパッケージ バージョンを選択します。 バージョンまたはバージョン範囲がこの不確実性を回避を指定します。

#### <a name="references-in-project-files-packagereference"></a>プロジェクト ファイル (PackageReference) の参照

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
```

**参照`packages.config`:**

`packages.config`、すべての依存関係がリストされ、正確な`version`パッケージを復元するときに使用される属性です。 `allowedVersions`属性は、パッケージを更新する可能性があるバージョンを制限する更新操作中にのみ使用します。

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

`version`属性、`<dependency>`要素には、依存関係として受け入れ可能な範囲のバージョンがについて説明します。

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
> これは、NuGet 3.4 以降の互換性に影響する変更です。

を再インストールまたは復元操作、、のインストール中に、リポジトリからパッケージを取得するときに NuGet 3.4 以降はバージョン番号を、次のように扱われます。

- バージョン番号から先頭のゼロは削除されます。

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- バージョン番号の 4 番目の部分のゼロは省略されます。

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

この正規化では、パッケージ自体; のバージョン番号には影響しませんこれは、のみ方法 NuGet と一致するバージョンの依存関係を解決するときに影響します。

ただし、NuGet パッケージのリポジトリでは、パッケージのバージョンの重複を防ぐためには、NuGet と同様にこれらの値を扱う必要があります。 バージョンを含むリポジトリしたがって*1.0*パッケージの必要がありますもホストしていないバージョン*1.0.0*独立した別のパッケージとして。
