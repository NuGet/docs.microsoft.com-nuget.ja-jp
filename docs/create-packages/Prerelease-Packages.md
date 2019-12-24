---
title: NuGet パッケージのプレリリース版
description: プレリリース パッケージのビルド ガイド
author: karann-msft
ms.author: karann
ms.date: 08/14/2017
ms.topic: conceptual
ms.openlocfilehash: 1c19f962dc9e42154c0f4374432548e867e9538a
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610711"
---
# <a name="building-pre-release-packages"></a>プレリリース パッケージのビルド

更新したパッケージを新しいバージョン番号でリリースすると、NuGet はそれを "最新の安定版リリース" として見なし、たとえば、Visual Studio 内のパッケージ マネージャー UI で下記のように表示されます。

![最新の安定版リリースを示すパッケージ マネージャー UI](media/Prerelease_01-LatestStable.png)

安定版リリースとは、実稼働環境で使用するだけの信頼性があると見なされるリリースです。 最新の安定版リリースは、パッケージ更新またはパッケージ復元でインストールされるリリースでもあります (「[Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md)」 (パッケージの再インストールと更新) の説明にある制約に左右されます)。

ソフトウェア リリース ライフサイクルをサポートするために、NuGet 1.6 以降では、プレリリース パッケージを配信できます。バージョン番号には、`-alpha`、`-beta`、`-rc` のようなセマンティック バージョン管理サフィックスが含まれます。 詳細については、「[Package versioning](../concepts/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) を参照してください。

次の方法のいずれかを使って、このようなバージョンを指定できます。

- **プロジェクトで [`PackageReference`](../consume-packages/package-references-in-project-files.md) を使う場合**: `.csproj` ファイルの [`PackageVersion`](/dotnet/core/tools/csproj.md#packageversion) 要素にセマンティック バージョン サフィックスを含めます。

    ```xml
    <PropertyGroup>
        <PackageVersion>1.0.1-alpha</PackageVersion>
    </PropertyGroup>
    ```

- **プロジェクトに [`packages.config`](../reference/packages-config.md) ファイルがある場合**: [`.nuspec`](../reference/nuspec.md) ファイルの [`version`](../reference/nuspec.md#version) 要素にセマンティック バージョン サフィックスを含めます。

    ```xml
    <version>1.0.1-alpha</version>
    ```

安定版バージョンをリリースする用意ができたら、サフィックスを削除します。このパッケージはあらゆるプレリリース版に優先します。 繰り返しになりますが、「[Package versioning](../concepts/package-versioning.md#pre-release-versions)」(パッケージのバージョン管理) を参照してください。

## <a name="installing-and-updating-pre-release-packages"></a>プレリリース パッケージのインストールと更新

既定で、NuGet ではパッケージの使用時にプレリリース版を含めませんが、この動作は次のように変更できます。

- **Visual Studio のパッケージ マネージャー UI**: **[NuGet パッケージの管理]** UI で、 **[プレリリースを含める]** ボックスを選択します。

    ![Visual Studio の [プレリリースを含める] チェックボックス](media/Prerelease_02-CheckPrerelease.png)

    このボックスをオンまたはオフにするとパッケージ マネージャー UI とインストールできるバージョンの一覧が更新されます。

- **パッケージ マネージャー コンソール**: `Find-Package`、`Get-Package`、`Install-Package`、`Sync-Package`、`Update-Package` コマンドで `-IncludePrerelease` スイッチを使用します。 「[PowerShell Reference](../reference/powershell-reference.md)」 (PowerShell リファレンス) を参照してください。

- **NuGet CLI**: `install`、`update`、`delete`、`mirror` コマンドで `-prerelease` スイッチを使用します。 「[NuGet CLI reference](../reference/nuget-exe-cli-reference.md)」(NuGet CLI リファレンス) を参照してください。

## <a name="semantic-versioning"></a>セマンティック バージョン管理

「[Semantic Versioning or SemVer convention](https://semver.org/spec/v1.0.0.html)」 (セマンティック バージョニングまたは SemVer 規則) では、バージョン番号の文字列を活用し、基礎となっているコードの意味を伝える方法が説明されています。

この規則では、各バージョンが 3 つの部分、`Major.Minor.Patch` から構成されています。それぞれ次のような意味があります。

- `Major`:互換性に影響する変更
- `Minor`: 新機能、ただし下位互換性あり
- `Patch`: 下位互換性のバグ修正のみ

プレリリース版には、パッチ番号の後にハイフンと文字列が付きます。 技術的に言えば、ハイフンの後には*あらゆる*文字列を使用できます。それで NuGet はパッケージをプレリリースとして扱います。 NuGet は該当 UI に完全なバージョン番号を表示します。利用者はその意味を自分で解釈します。

それを踏まえた上で、次のような認められている命名規則に従うことが一般的に推奨されます。

- `-alpha`: アルファ リリース。一般的に、進行中の製品または実験に使用されます。
- `-beta`: ベータ リリース。一般的に、次に計画されているリリースの機能をすべて利用できますが、既知のバグが含まれている可能性があります。
- `-rc`: リリース候補。一般的に、重大なバグが現れない限り、最終版 (安定版) となる可能性があるリリース。

> [!Note]
> NuGet 4.3.0 以降は、`1.0.1-build.23` のように、ドット表記のプレリリース番号をサポートする[セマンティック バージョニング v2.0.0](https://semver.org/spec/v2.0.0.html) をサポートしています。 ドット表記は、バージョン 4.3.0 より前の NuGet ではサポートされていません。 以前のバージョンの NuGet では、`1.0.1-build23` のような形式を使用できましたが、これは常にプレリリース版と見なされていました。

ただし、どのようなサフィックスを使用する場合でも、NuGet はアルファベットの逆順で優先順序を与えます。

    1.0.1
    1.0.1-zzz
    1.0.1-rc
    1.0.1-open
    1.0.1-beta.12
    1.0.1-beta.5
    1.0.1-beta
    1.0.1-alpha.2
    1.0.1-alpha

このように、サフィックスのないバージョンは常にプレリリース版に優先します。

semver2 では、0 を前に付ける必要はありませんが、古いバージョンのスキーマでは付与されています。 プレリリース タグと共に数値のサフィックスを使用し、その数字が 2 桁 (以上) になる可能性がある場合、beta.01 や beta.05 のように、数字が大きくなっても確実に正しく並べ替えられるように、前に付けるゼロを使用してください。 この推奨事項は、古いバージョンのスキーマのみに適用されます。
