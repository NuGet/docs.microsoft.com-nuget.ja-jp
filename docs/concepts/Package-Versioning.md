---
title: NuGet パッケージ バージョンのリファレンス
description: NuGet パッケージが依存する他のパッケージのバージョン番号と範囲を指定する方法と、依存関係をインストールする方法について詳しく説明します。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 912c0d015e2f499bc7386483bc6c35ecd765d3d4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428475"
---
# <a name="package-versioning"></a>パッケージのバージョン管理

特定のパッケージは、常にパッケージ識別子と正確なバージョン番号を使用して参照されます。 たとえば、nuget.org の [Entity Framework](https://www.nuget.org/packages/EntityFramework/) には、バージョン *4.1.10311* からバージョン *6.1.3* (最新の安定したリリース) までの数十の特定のパッケージと、*6.2.0-beta1* のようなさまざまなプレリリース バージョンがあります。

パッケージの作成時に、オプションのプレリリース テキスト サフィックスを使用して特定のバージョン番号を割り当てます。 一方、パッケージを使用するときには、正確なバージョン番号または許容されるバージョンの範囲のいずれかを指定できます。

このトピックの内容:

- プレリリース サフィックスを含む[バージョンの基本](#version-basics)。
- [バージョン範囲](#version-ranges)
- [正規化されたバージョン番号](#normalized-version-numbers)

## <a name="version-basics"></a>バージョンの基本

特定のバージョン番号は、*Major.Minor.Patch[-Suffix]* という形式になっています。ここで、各構成要素には次の意味があります。

- *Major*:互換性に影響する変更
- *Minor*: 新機能、ただし下位互換性あり
- *Patch*: 下位互換性のバグ修正のみ
- *-Suffix* (省略可能): ハイフンに続けて、プレリリース バージョンを示す文字列 ([セマンティック バージョニングまたは SemVer 1.0 規約](https://semver.org/spec/v1.0.0.html)に従う)。

**例:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org では、正確なバージョン番号がないパッケージのアップロードがすべて拒否されます。 バージョンは、`.nuspec` 内またはパッケージの作成に使用されるプロジェクト ファイル内で指定する必要があります。

### <a name="pre-release-versions"></a>プレリリース バージョン

技術的に言えば、パッケージの作成者は、任意の文字列をサフィックスとして使用してプレリリース バージョンを示すことができます。これは、NuGet ではそのようなバージョンがプレリリースとして扱われ、他の解釈は行われないためです。 つまり、NuGet では、関係する UI に完全なバージョン文字列が表示され、サフィックスの意味の解釈はコンシューマーに委ねられます。

つまり、パッケージ開発者は一般に、認識されている名前付け規則に従います。

- `-alpha`:アルファ リリース。一般的に、進行中の製品または実験に使用されます。
- `-beta`: ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。
- `-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。

> [!Note]
> NuGet 4.3.0 以降では、*1.0.1-build.23* のように、ドット表記のプレリリース番号をサポートする [SemVer 2.0.0](https://semver.org/spec/v2.0.0.html) がサポートされます。 ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。 *1.0.1-build23* のような形式を使用できます。

パッケージ参照を解決するときに、複数のパッケージ バージョンのサフィックスだけが異なる場合、NuGet ではサフィックスのないバージョンが最初に選択され、プレリリース バージョンにアルファベットの逆順の優先順位が適用されます。 たとえば、以下のバージョンは、示されているとおりの順序で選択されます。

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>セマンティック バージョニング 2.0.0

NuGet 4.3.0 以降と Visual Studio 2017 バージョン 15.3 以降では、NuGet によって[セマンティック バージョニング 2.0.0](https://semver.org/spec/v2.0.0.html) がサポートされます。

SemVer v2.0.0 の特定のセマンティクスは、以前のクライアントではサポートされません。 NuGet では、次のいずれかの文が真の場合に、パッケージ バージョンが SemVer v2.0.0 に固有であると見なされます。

- プレリリース ラベルがドットで区切られている (例: *1.0.0-alpha.1*)
- バージョンにビルド メタデータが含まれている (例: *1.0.0+githash*)

nuget.org では、次のいずれかの文が真の場合に、パッケージが SemVer v2.0.0 パッケージとして定義されます。

- パッケージの独自のバージョンが上で定義されている SemVer v2.0.0 に準拠しているが、SemVer v1.0.0 には準拠していない。
- パッケージの依存関係のバージョン範囲のいずれかの最小または最大バージョンが上で定義されている SemVer v2.0.0 に準拠しているが、SemVer v1.0.0 には準拠していない (例: *[1.0.0-alpha.1, )* )。

SemVer v2.0.0 固有のパッケージを nuget.org にアップロードした場合、パッケージは以前のクライアントでは非表示になり、以下の NuGet クライアントでのみ使用できます。

- NuGet 4.3.0 以降
- Visual Studio 2017 バージョン 15.3 以降
- Visual Studio 2015 と [NuGet VSIX v3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore.exe (.NET SDK 2.0.0+)

サード パーティ製クライアント:

- JetBrains Rider
- Paket バージョン 5.0 以降

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges"></a>バージョン範囲

パッケージの依存関係を参照する場合、以下にまとめるように、NuGet ではバージョン範囲を指定するために間隔表記の使用がサポートされます。

| Notation | 適用されるルール | 説明 |
|----------|--------------|-------------|
| 1 | x ≥ 1.0 | 最小バージョン (示されている値を含む) |
| (1.0,) | x > 1.0 | 最小バージョン (示されている値を含まない) |
| [1.0] | x == 1.0 | 正確なバージョンの一致 |
| (,1.0] | x ≤ 1.0 | 最大バージョン (示されている値を含む) |
| (,1.0) | x < 1.0 | 最大バージョン (示されている値を含まない) |
| [1.0,2.0] | 1.0 ≤ x ≤ 2.0 | 正確な範囲 (示されている値を含む) |
| (1.0,2.0) | 1.0 < x < 2.0 | 正確な範囲 (示されている値を含まない) |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 示されている値を含む最小バージョンと示されている値を含まない最大バージョンの組み合わせ |
| (1.0)    | 無効な | 無効な |

PackageReference 形式を使用する場合、NuGet では、番号の Major、Minor、Patch、およびプレリリース サフィックス部分に浮動小数点表記 \* を使用できます。 `packages.config` 形式では、浮動小数点バージョンはサポートされていません。

> [!Note]
> PackageReference のバージョン範囲には、プレリリース バージョンが含まれます。 仕様により、浮動バージョンでは、オプトインしない限りプレリリース バージョンは解決されません。 関連する機能要求の状態については、[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297) に関するページをご覧ください。

### <a name="examples"></a>使用例

プロジェクト ファイル、`packages.config` ファイル、`.nuspec` ファイル内では、パッケージの依存関係のバージョンまたはバージョン範囲を必ず指定します。 バージョンまたはバージョン範囲を指定しない場合、NuGet 2.8.x 以前では依存関係を解決するときに利用可能な最新のパッケージ バージョンが選択されますが、NuGet 3.x 以降ではパッケージの最小バージョンが選択されます。 バージョンまたはバージョン範囲を指定すると、この不確実性が回避されます。

#### <a name="references-in-project-files-packagereference"></a>プロジェクト ファイル内の参照 (PackageReference)

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

**`packages.config` 内の参照**:

`packages.config` では、すべての依存関係が、パッケージの復元時に使用される正確な `version` 属性と共に一覧表示されます。 `allowedVersions` 属性は、パッケージの更新先にできるバージョンを制限するために、更新操作中にのみ使用されます。

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

**`.nuspec` ファイル内の参照**

`<dependency>` 要素内の `version` 属性は、依存関係で許容される範囲のバージョンを示します。

```xml
<!-- Accepts any version 6.1 and above. -->
<dependency id="ExamplePackage" version="6.1" />

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
> これは、NuGet 3.4 以降での破壊的変更です。

インストール、再インストール、または復元操作中にリポジトリからパッケージを取得すると、NuGet 3.4 以降ではバージョン番号が次のように扱われます。

- 先頭のゼロはバージョン番号から削除されます。

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- バージョン番号の 4 番目の部分のゼロは省略されます

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack` 操作と `restore` 操作では、可能な限りバージョンが正規化されます。 既にビルドされているパッケージの場合、この正規化はパッケージ自体のバージョン番号には影響しません。依存関係を解決するときに NuGet によってバージョンが照合される方法にのみ影響します。

ただし、NuGet パッケージ リポジトリでは、これらの値を NuGet と同じように処理して、パッケージのバージョンが重複しないようにする必要があります。 したがって、パッケージのバージョン *1.0* を含むリポジトリでは、バージョン *1.0.0* を別の異なるパッケージとしてホストすることはできません。
