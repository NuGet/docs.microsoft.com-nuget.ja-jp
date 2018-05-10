---
title: NuGet パッケージのプレリリース版
description: プレリリース パッケージのビルド ガイド
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: a4540d29d9ca01f98ee5d1786e8a175ee0ea79f4
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="building-pre-release-packages"></a>プレリリース パッケージのビルド

更新したパッケージを新しいバージョン番号でリリースすると、NuGet はそれを "最新の安定版リリース" として見なし、たとえば、Visual Studio 内のパッケージ マネージャー UI で下記のように表示されます。

![最新の安定版リリースを示すパッケージ マネージャー UI](media/Prerelease_01-LatestStable.png)

安定版リリースとは、実稼働環境で使用するだけの信頼性があると見なされるリリースです。 最新の安定版リリースは、パッケージ更新またはパッケージ復元でインストールされるリリースでもあります (「[Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) の説明にある制約に左右されます)。

ソフトウェア リリース ライフサイクルをサポートするために、NuGet 1.6 以降では、プレリリース パッケージを配信できます。バージョン番号には、`-alpha`、`-beta`、`-rc` のようなセマンティック バージョン管理サフィックスが含まれます。 詳細については、「[Package versioning](../reference/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) を参照してください。

このようなバージョンは 2 つの方法で指定できます。

- `.nuspec` ファイル: `version` 要素にセマンティック バージョン サフィックスを含めます:

    ```xml
    <version>1.0.1-alpha</version>
    ```

- アセンブリ属性: Visual Studio プロジェクト (`.csproj` または `.vbproj`) からパッケージをビルドするとき、`AssemblyInformationalVersionAttribute` を使用してバージョンを指定します:

    ```cs
    [assembly: AssemblyInformationalVersion("1.0.1-beta")]
    ```

    NuGet は、セマンティック バージョン管理に対応していない `AssemblyVersion` 属性に指定されている値ではなく、この値を選択します。

安定版バージョンをリリースする用意ができたら、サフィックスを削除します。このパッケージはあらゆるプレリリース版に優先します。 繰り返しになりますが、「[Package versioning](../reference/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) を参照してください。

## <a name="installing-and-updating-pre-release-packages"></a>プレリリース パッケージのインストールと更新

既定で、NuGet ではパッケージの使用時にプレリリース版を含めませんが、この動作は次のように変更できます。

- **Visual Studio のパッケージ マネージャー UI**: **[NuGet パッケージの管理]** UI で、**[プレリリースを含める]** ボックスを選択します。

    ![Visual Studio の [プレリリースを含める] チェックボックス](media/Prerelease_02-CheckPrerelease.png)

    このボックスをオンまたはオフにするとパッケージ マネージャー UI とインストールできるバージョンの一覧が更新されます。

- **パッケージ マネージャー コンソール**: `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package`、`Update-Package` コマンドで `-IncludePrerelease` スイッチを使用します。 「[PowerShell Reference](../tools/powershell-reference.md)」 (PowerShell リファレンス) を参照してください。

- **NuGet CLI**: `install`、`update`、`delete`、`mirror` コマンドで `-prerelease` スイッチを使用します。 「[NuGet CLI reference](../tools/nuget-exe-cli-reference.md)」(NuGet CLI リファレンス) を参照してください。

## <a name="semantic-versioning"></a>セマンティック バージョン管理

「[Semantic Versioning or SemVer convention](http://semver.org/spec/v1.0.0.html)」 (セマンティック バージョン管理または SemVer 規則) では、バージョン番号の文字列を活用し、基礎となっているコードの意味を伝える方法が説明されています。

この規則では、各バージョンが 3 つの部分、`Major.Minor.Patch` から構成されています。それぞれ次のような意味があります。

- `Major`: 互換性に影響する変更点
- `Minor`: 新機能、ただし下位互換性あり
- `Patch`: 下位互換性のバグ修正のみ

プレリリース版には、パッチ番号の後にハイフンと文字列が付きます。 技術的に言えば、ハイフンの後には*あらゆる*文字列を使用できます。それで NuGet はパッケージをプレリリースとして扱います。 NuGet は該当 UI に完全なバージョン番号を表示します。利用者はその意味を自分で解釈します。

それを踏まえた上で、次のような認められている命名規則に従うことが一般的に推奨されます。

- `-alpha`: アルファ リリース。一般的に、進行中の製品または実験に使用されます。
- `-beta`: ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。
- `-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。

> [!Note]
> NuGet 4.3.0 以降は、`1.0.1-build.23` のように、ドット表記のプレリリース番号をサポートする[セマンティック バージョニング v2.0.0](http://semver.org/spec/v2.0.0.html) をサポートしています。 ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。 以前のバージョンの NuGet では、`1.0.1-build23` のような形式を使用できましたが、これは常にプレリリース版と見なされていました。

ただし、どのようなサフィックスを使用する場合でも、NuGet はアルファベットの逆順で優先順序を与えます。

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta12
    1.0.1-beta05
    1.0.1-beta
    1.0.1-alpha2
    1.0.1-alpha

このように、サフィックスのないバージョンは常にプレリリース版に優先します。 数値のサフィックスとプレリリース タグを使用するとき、番号が 2 桁 (以上) になる場合、beta01 や beta05 のように、先行ゼロを使用してください。それにより、番号が大きくなっても正しく並べ替えられます。
