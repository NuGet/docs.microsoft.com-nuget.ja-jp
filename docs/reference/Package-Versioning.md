---
title: NuGet パッケージバージョンリファレンス
description: NuGet パッケージが依存する他のパッケージのバージョン番号と範囲を指定する方法、および依存関係をインストールする方法について正確に説明します。
author: karann-msft
ms.author: karann
ms.date: 03/23/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 7c6992d6bf3142eb6aca70f1fa3c46f72efd25a0
ms.sourcegitcommit: fc1b716afda999148eb06d62beedb350643eb346
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/14/2019
ms.locfileid: "69020000"
---
# <a name="package-versioning"></a>パッケージのバージョン管理

特定のパッケージは、常にパッケージ識別子と正確なバージョン番号を使用して参照されます。 たとえば、nuget.org の[Entity Framework](https://www.nuget.org/packages/EntityFramework/)には、バージョン*4.1.10311*からバージョン*ef6.1.3* (最新の安定したリリース)、 *6.2.0-beta1 などのさまざまなプレリリースバージョンまで、いくつかの特定のパッケージが用意されています。* .

パッケージを作成するときに、オプションのプレリリーステキストサフィックスを使用して特定のバージョン番号を割り当てます。 一方、パッケージを使用する場合は、正確なバージョン番号または許容されるバージョンの範囲のいずれかを指定できます。

このトピックの内容:

- プレリリースのサフィックスを含む[バージョンの基本](#version-basics)。
- [バージョン範囲とワイルドカード](#version-ranges-and-wildcards)
- [正規化されたバージョン番号](#normalized-version-numbers)

## <a name="version-basics"></a>バージョンの基本

特定のバージョン番号は、Major. *Minor. Patch [-Suffix]* という形式になっています。ここで、コンポーネントには次の意味があります。

- *メジャー*:互換性に影響する変更
- *マイナー*: 新機能、ただし下位互換性あり
- *修正プログラム*: 下位互換性のバグ修正のみ
- *-サフィックス*(省略可能): プレリリースバージョンを示す文字列 ([セマンティックバージョン管理または SemVer 1.0 規則](http://semver.org/spec/v1.0.0.html)に従う)。

**使用例:**

    1.0.1
    6.11.1231
    4.3.1-rc
    2.2.44-beta1

> [!Important]
> nuget.org は、正確なバージョン番号を持たないパッケージのアップロードを拒否します。 バージョンは、パッケージの作成に`.nuspec`使用されるプロジェクトファイルまたはプロジェクトファイルで指定する必要があります。

### <a name="pre-release-versions"></a>プレリリース版

技術的に言えば、パッケージ作成者は、任意の文字列をサフィックスとして使用してプレリリースバージョンを示すことができます。これは、NuGet がプレリリースとしてそのようなバージョンを扱い、他の解釈は行わないためです。 つまり、NuGet は、関連する任意の UI に完全なバージョン文字列を表示し、サフィックスの意味をコンシューマーに解釈したままにします。

ただし、通常、パッケージ開発者は、認識されている名前付け規則に従います。

- `-alpha` :アルファリリース。通常は、進行中の作業と実験に使用されます。
- `-beta` : ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。
- `-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。

> [!Note]
> NuGet 4.3.0 以降では、* *1.0.1-build. 23*のように、ドット表記のプレリリース番号をサポートする[semver 2.0.0](http://semver.org/spec/v2.0.0.html)をサポートしています。 ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。 *Build23*のような形式を使用できます。

パッケージ参照を解決し、複数のパッケージバージョンがサフィックスによってのみ異なる場合は、NuGet によってサフィックスのないバージョンが最初に選択されます。その後、プレリリースバージョンの優先順位はアルファベットの逆順になります。 たとえば、次のバージョンは、正確な順序で選択されます。

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha
    1.0.1-aaa

## <a name="semantic-versioning-200"></a>セマンティックバージョン管理2.0.0

NuGet では、nuget 4.3.0 以降と Visual Studio 2017 バージョン 15.3 + を使用して、[セマンティックバージョン管理 2.0.0](http://semver.org/spec/v2.0.0.html)をサポートしています。

SemVer v 2.0.0 の特定のセマンティクスは、古いクライアントではサポートされていません。 NuGet では、次のいずれかのステートメントが true の場合、パッケージのバージョンが SemVer v 2.0.0 に限定されます。

- プレリリースラベルはドットで区切られています (例: *1.0.0)。 1*
- バージョンには、 *1.0.0 + githash*などのビルドメタデータが含まれています。

Nuget.org の場合、次のいずれかのステートメントが true の場合、パッケージは SemVer v 2.0.0 パッケージとして定義されます。

- パッケージの独自のバージョンは SemVer v 2.0.0 に準拠していますが、前述のように SemVer v 1.0.0 に準拠していません。
- パッケージの依存関係のバージョンの範囲には、最小または最大のバージョンがあります。これは、上記で定義されている semver v 2.0.0 に準拠していますが、SemVer v1.0 に準拠していません。たとえば、 *[1.0.0-alpha. 1,)* のようになります。

SemVer v 2.0.0 固有のパッケージを nuget.org にアップロードすると、パッケージは古いクライアントからは見えず、次の NuGet クライアントでのみ使用できます。

- NuGet 4.3.0 +
- Visual Studio 2017 バージョン 15.3 +
- Visual Studio 2015 と[NUGET VSIX v 3.6.0](https://dist.nuget.org/visualstudio-2015-vsix/latest/NuGet.Tools.vsix)
- dotnet
  - dotnetcore .exe (.NET SDK 2.0.0 +)

サードパーティのクライアント:

- JetBrains Rider
- パケットバージョン5.0 以降

<!-- For compatibility with previous dependency-versions page -->
<a name="version-ranges"></a>

## <a name="version-ranges-and-wildcards"></a>バージョン範囲とワイルドカード

パッケージの依存関係を参照する場合、NuGet はバージョン範囲を指定するための間隔表記の使用をサポートしています。次に例を示します。

| Notation | 適用されたルール | 説明 |
|----------|--------------|-------------|
| 1 | x ≥ 1.0 | 最小バージョン (含む) |
| (1.0,) | x > 1.0 | 最小バージョン、排他 |
| [1.0] | x = = 1.0 | 正確なバージョンの一致 |
| (,1.0] | x ≤ 1.0 | 最大バージョン (含む) |
| (,1.0) | x < 1.0 | 最大バージョン、排他 |
| [1.0,2.0] | 1.0 ≤ x ≤2.0 | 完全な範囲 (含む) |
| (1.0,2.0) | 1.0 < x < 2.0 | 完全な範囲、排他 |
| [1.0,2.0) | 1.0 ≤ x < 2.0 | 包括的最小バージョンと排他最大バージョンの混合 |
| (1.0)    | 無効な | 無効な |

PackageReference 形式を使用する場合、NuGet では、数字のメジャー \*、マイナー、修正プログラム、およびプレリリースのサフィックス部分に対してワイルドカード表記 () を使用することもできます。 ワイルドカードは、 `packages.config`形式ではサポートされていません。

> [!Note]
> PackageReference のバージョン範囲には、プレリリースバージョンが含まれています。 仕様により、フローティングバージョンでは、をオプトインしない限り、プレリリースバージョンは解決されません。 関連する機能の要求の状態については、「[問題 6434](https://github.com/NuGet/Home/issues/6434#issuecomment-358782297)」を参照してください。

### <a name="examples"></a>使用例

プロジェクトファイル、 `packages.config`ファイル、および`.nuspec`ファイルで、パッケージの依存関係のバージョンまたはバージョンの範囲を常に指定します。 バージョンまたはバージョン範囲を指定しない場合、依存関係を解決するときに NuGet 2.8. x 以前のバージョンで利用可能な最新のパッケージバージョンが選択されます。一方、NuGet 3.x 以降では、パッケージの最小バージョンが選択されます。 バージョンまたはバージョンの範囲を指定すると、この不確実性が回避します。

#### <a name="references-in-project-files-packagereference"></a>プロジェクトファイル内の参照 (PackageReference)

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

**参照先`packages.config`:**

で`packages.config`は、すべての依存関係が、 `version`パッケージの復元時に使用される正確な属性と共に一覧表示されます。 `allowedVersions`属性は、更新操作中にのみ、パッケージが更新される可能性のあるバージョンを制限するために使用されます。

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

**ファイル内`.nuspec`の参照**

`<dependency>`要素`version`の属性は、依存関係で許容される範囲のバージョンを記述します。

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
> これは、NuGet 3.4 以降の互換性に影響する変更点です。

インストール、再インストール、または復元操作中にリポジトリからパッケージを取得すると、NuGet 3.4 以降ではバージョン番号が次のように処理されるようになります。

- 先頭の0は、バージョン番号から削除されます。

        1.00 is treated as 1.0
        1.01.1 is treated as 1.1.1
        1.00.0.1 is treated as 1.0.0.1

- バージョン番号の4番目の部分のゼロは省略されます。

        1.0.0.0 is treated as 1.0.0
        1.0.01.0 is treated as 1.0.1

`pack`および`restore`操作では、可能な限りバージョンが正規化されます。 既にビルドされているパッケージの場合、この正規化はパッケージ自体のバージョン番号には影響しません。依存関係を解決するときに NuGet がバージョンと一致する方法にのみ影響します。

ただし、NuGet パッケージリポジトリでは、これらの値を NuGet と同じように処理して、パッケージのバージョンが重複しないようにする必要があります。 したがって、パッケージのバージョン*1.0*を含むリポジトリでは、バージョン*1.0.0*を別のパッケージとしてホストすることはできません。
