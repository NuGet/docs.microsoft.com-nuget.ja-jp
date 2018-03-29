---
title: NuGet CLI パック コマンド |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe パック コマンドのリファレンス
keywords: nuget パックの参照、パック コマンド
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 14ecf724477f652275eb68a090bb57b8640d4a8a
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="pack-command-nuget-cli"></a>パック コマンド (NuGet CLI)

**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:** 2.7 +

に基づいて、指定された NuGet パッケージを作成`.nuspec`またはプロジェクト ファイルです。 `dotnet pack`コマンド (を参照してください[dotnet コマンド](dotnet-Commands.md)) および`msbuild /t:pack`(を参照してください[MSBuild ターゲット](../reference/msbuild-targets.md)) の代替として使用することがあります。

> [!Important]
> Mono で、プロジェクト ファイルからパッケージを作成することはサポートされていません。 内の非ローカル パスを調整する必要があります、 `.nuspec` nuget.exe しない Windows のパス名自体を変換するために、Unix 形式のパスにファイルします。

## <a name="usage"></a>使用法

```cli
nuget pack <nuspecPath | projectPath> [options]
```

ここで`<nuspecPath>`と`<projectPath>`指定、`.nuspec`またはプロジェクト ファイル、それぞれします。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| BasePath | 定義されているファイルのベース パスを設定、`.nuspec`ファイル。 |
| ビルド | パッケージを構築する前に、プロジェクトをビルドすることを指定します。 |
| 除外 | パッケージを作成するときに除外する 1 つまたは複数のワイルドカード パターンを指定します。 複数のパターンを指定するに繰り返します - 除外するフラグ。 次の例を参照してください。 |
| ExcludeEmptyDirectories | パッケージを作成するときに、空のディレクトリを含めることを防ぎます。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| IncludeReferencedProjects | 依存関係として、またはパッケージの一部として、ビルド、パッケージに参照先のプロジェクトを含める必要がありますを示します。 参照先プロジェクトに対応する`.nuspec`をその参照先プロジェクトが、依存関係として追加し、プロジェクトと同じ名前を持つファイルです。 それ以外の場合、参照先プロジェクトは、パッケージの一部として追加されます。 |
| MinClientVersion | 設定、 *minClientVersion*作成されたパッケージの属性です。 この値は、既存の値をオーバーライド*minClientVersion*で属性 (該当する場合)、`.nuspec`ファイル。 |
| MSBuildPath | *(4.0 以降)*よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。 |
| MSBuildVersion | *(3.2 +)*このコマンドで使用する MSBuild のバージョンを指定します。 サポートされている値は、4、12、14、15 です。 既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。 |
| NoDefaultExcludes | により、NuGet の既定の除外ファイルおよびファイルとフォルダーには、ピリオドなどの開始をパッケージ化`.svn`と`.gitignore`です。 |
| NoPackageAnalysis | パッケージのビルド後に、パックでパッケージの分析を実行しないことを指定します。 |
| OutputDirectory | 作成されたパッケージが格納されているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 |
| プロパティ | プロジェクト ファイル内の値をオーバーライドするプロパティの一覧を指定します参照してください[MSBuild プロジェクトの共通プロパティ](/visualstudio/msbuild/common-msbuild-project-properties)プロパティ名にします。 プロパティ引数をここでは、トークンのリスト = 値のペアをセミコロンで区切られた場所のたびに`$token$`で、`.nuspec`ファイルは指定した値に置き換えられます。 値は、引用符で囲まれた文字列にすることができます。 "Configuration"プロパティの既定値がある"Debug"に注意してください。 リリース構成を変更するには、使用`-Properties Configuration=Release`です。 |
| サフィックス | *(3.4.4+)*内部的に生成されたバージョン番号、ビルドまたはその他のプレリリース版の識別子を追加するために使用される通常にサフィックスを追加します。 たとえばを使用して`-suffix nightly`バージョン番号 like でパッケージを作成`1.2.3-nightly`です。 サフィックスは、警告、エラー、およびさまざまなバージョンの NuGet と NuGet パッケージ マネージャーの潜在的な非互換性を回避するのには文字で始める必要があります。 |
| シンボル | パッケージには、ソースとシンボルが含まれているを指定します。 使用すると、`.nuspec`ファイル、通常の NuGet パッケージ ファイルが作成され、対応するシンボル パッケージです。 |
| ツール | プロジェクトの出力ファイルを配置する必要がありますを指定します、`tool`フォルダーです。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |
| Version | バージョン番号よりも優先、`.nuspec`ファイル。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>開発の依存関係を除外

一部の NuGet パッケージは、独自のライブラリを作成できますが、必ずしも実際のパッケージの依存関係として必要のない開発依存関係として役立ちます。

`pack`コマンドは無視されます`package`エントリ`packages.config`がある、`developmentDependency`属性に設定`true`です。 これらのエントリは、作成されたパッケージ内の依存関係としては含まれません。

たとえば、次`packages.config`ソース プロジェクト ファイル。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

このプロジェクトのパッケージを作成して`nuget pack`依存関係を持つ`jQuery`と`microsoft-web-helpers`ではなく`netfx-Guard`です。

## <a name="examples"></a>使用例

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
