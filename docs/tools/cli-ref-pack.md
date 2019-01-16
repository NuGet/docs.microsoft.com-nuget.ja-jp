---
title: NuGet CLI pack コマンド
description: Nuget.exe パック コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d39ec8caf94caa767b6c502cc475e278aa718b95
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324787"
---
# <a name="pack-command-nuget-cli"></a>pack コマンド (NuGet CLI)

**適用対象:** パッケージの作成&bullet;**サポートされているバージョン。** 2.7+

に基づいて、指定された NuGet パッケージを作成します。`.nuspec`またはプロジェクト ファイル。 `dotnet pack`コマンド (を参照してください[dotnet コマンド](dotnet-Commands.md)) と`msbuild -t:pack`(を参照してください[MSBuild ターゲット](../reference/msbuild-targets.md)) の代替として使用することがあります。

> [!Important]
> Mono で、プロジェクト ファイルからパッケージを作成することはサポートされていません。 非ローカル パスを調整する必要があります、 `.nuspec` Unix 形式のパスにファイルの nuget.exe が Windows パス名自体を変換しません。

## <a name="usage"></a>使用法

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

場所`<nuspecPath>`と`<projectPath>`指定、`.nuspec`またはプロジェクト ファイルをそれぞれします。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| BasePath | 定義されているファイルの基本パスを設定、`.nuspec`ファイル。 |
| ビルド | パッケージを構築する前に、プロジェクトをビルドすることを指定します。 |
| 除外 | パッケージを作成するときに除外する 1 つまたは複数のワイルドカード パターンを指定します。 1 つ以上のパターンを指定するには、繰り返し除外するフラグ。 次の例を参照してください。 |
| ExcludeEmptyDirectories | パッケージを作成するときに、空のディレクトリを含めることをできないようにします。 |
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ConfigFile | Pack コマンドの構成ファイルを指定します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| IncludeReferencedProjects | 依存関係として、または、パッケージの一部として、ビルドされたパッケージに参照されるプロジェクトを含める必要がありますを示します。 参照先プロジェクトが、対応する`.nuspec`をその参照先プロジェクトが依存関係として追加し、プロジェクトと同じ名前を持つファイル。 それ以外の場合、参照先のプロジェクトは、パッケージの一部として追加されます。 |
| MinClientVersion | 設定、 *minClientVersion*作成したパッケージの属性。 この値は、既存の値をオーバーライド*minClientVersion* (あれば) 属性、`.nuspec`ファイル。 |
| MSBuildPath | *(4.0 以降)* よりも優先、コマンドで使用する MSBuild のパスを示す`-MSBuildVersion`します。 |
| MSBuildVersion | *(3.2 以降)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされている値は、4、12、14、15 です。 パスに MSBuild が取得される、既定でそれ以外の場合、既定値 MSBuild の最上位のインストールされているバージョンです。 |
| NoDefaultExcludes | NuGet の既定の除外をできないようにファイルとフォルダーなど、ドットで始まるファイルをパッケージ化`.svn`と`.gitignore`します。 |
| NoPackageAnalysis | パッケージのビルド後に、パックでパッケージの分析を実行しないことを指定します。 |
| OutputDirectory | 作成したパッケージが格納されているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 |
| プロパティ | その他のオプションの後に、コマンドラインの最後は表示されます。 は、プロジェクト ファイル内の値をオーバーライドするプロパティの一覧を指定します参照してください[MSBuild プロジェクトの共通プロパティ](/visualstudio/msbuild/common-msbuild-project-properties)プロパティ名。 プロパティの引数をここでは、トークンのリスト = 値のペアをセミコロンで区切った、出現するたび`$token$`で、`.nuspec`ファイルが指定した値と置き換えられます。 値は引用符で囲まれた文字列を指定できます。 「構成」プロパティの既定値は"Debug"に注意してください。 リリース構成を変更するには、使用`-Properties Configuration=Release`します。 |
| サフィックス | *(3.4.4+)* 内部的に生成されたバージョン番号、ビルドまたはその他のプレリリース版の識別子を追加するために通常使用するサフィックスを追加します。 たとえばを使用して`-suffix nightly`などの数字のバージョンでパッケージを作成`1.2.3-nightly`です。 サフィックスは、警告、エラー、およびさまざまなバージョンの NuGet、NuGet パッケージ マネージャーの潜在的な非互換性を回避するために文字で始まる必要があります。 |
| シンボル | ソースとシンボル パッケージに含まれることを指定します。 使用すると、`.nuspec`正規の NuGet パッケージ ファイルが作成されますファイル、および対応するシンボル パッケージ。 既定で作成、[レガシ シンボル パッケージ](../create-packages/Symbol-Packages.md)します。 シンボル パッケージに推奨される新しい形式は .snupkg です。 「[シンボル パッケージ (.snupkg) の作成](../create-packages/Symbol-Packages-snupkg.md)」を参照してください。 |
| ツール | プロジェクトの出力ファイルが配置されることを指定します、`tool`フォルダー。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |
| Version | バージョン番号をオーバーライド、`.nuspec`ファイル。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="excluding-development-dependencies"></a>開発の依存関係を除外

NuGet パッケージの一部は、独自のライブラリを作成できますが、実際のパッケージの依存関係としては必ずしも必要ありません開発依存関係として役立ちます。

`pack`コマンドは無視されます`package`エントリ`packages.config`がある、`developmentDependency`属性に設定`true`します。 これらのエントリは、作成したパッケージの依存関係として含まれません。

たとえば、次`packages.config`ソース プロジェクト ファイル。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

このプロジェクトでパッケージを作成して`nuget pack`依存関係になります`jQuery`と`microsoft-web-helpers`なく`netfx-Guard`します。

## <a name="examples"></a>使用例

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
