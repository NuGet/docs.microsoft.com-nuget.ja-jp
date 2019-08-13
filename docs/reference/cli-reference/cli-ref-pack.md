---
title: NuGet CLI pack コマンド
description: Nuget.exe pack コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cab56cb87f46335f9fdebdbc1649fead16459877
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959730"
---
# <a name="pack-command-nuget-cli"></a>pack コマンド (NuGet CLI)

**適用対象:** パッケージ作成&bullet;で**サポートされているバージョン:** 2.7+

指定された[nuspec](../nuspec.md)またはプロジェクトファイルに基づいて NuGet パッケージを作成します。 コマンド`dotnet pack` (「 [dotnet コマンド](../dotnet-Commands.md)」を参照`msbuild -t:pack` ) と (「 [MSBuild ターゲット](../msbuild-targets.md)」を参照) は、代替として使用できます。

> [!Important]
> Mono では、プロジェクトファイルからパッケージを作成することはサポートされていません。 また、nuget.exe によって Windows のパス名自体`.nuspec`が変換されないため、ファイル内のローカルではないパスを Unix 形式のパスに調整する必要があります。

## <a name="usage"></a>使用法

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

`<nuspecPath>` `.nuspec`とは、それぞれまたはプロジェクトファイルを指定します。`<projectPath>`

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| BasePath | [Nuspec](../nuspec.md)ファイルで定義されているファイルのベースパスを設定します。 |
| Build | パッケージをビルドする前にプロジェクトをビルドするように指定します。 |
| Exclude | パッケージの作成時に除外する1つ以上のワイルドカードパターンを指定します。 複数のパターンを指定するには、-Exclude フラグを繰り返します。 次の例を参照してください。 |
| ExcludeEmptyDirectories | パッケージをビルドするときに空のディレクトリを含めないようにします。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| ConfigFile | パックコマンドの構成ファイルを指定します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| IncludeReferencedProjects | ビルドされたパッケージに、依存関係として、またはパッケージの一部として参照プロジェクトを含める必要があることを示します。 参照先のプロジェクトに、プロジェクト`.nuspec`と同じ名前の対応するファイルがある場合、その参照先プロジェクトは依存関係として追加されます。 それ以外の場合、参照されるプロジェクトはパッケージの一部として追加されます。 |
| MinClientVersion | 作成したパッケージの*minClientVersion*属性を設定します。 この値は、 `.nuspec`ファイル内の既存の*minClientVersion*属性 (存在する場合) の値よりも優先されます。 |
| MSBuildPath | *(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これは`-MSBuildVersion`よりも優先されます。 |
| MSBuildVersion | *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。 |
| NoDefaultExcludes | `.svn` や`.gitignore`など、ドットで始まる NuGet パッケージファイルとファイルおよびフォルダーの既定の除外を回避します。 |
| NoPackageAnalysis | パッケージのビルド後に、パックでパッケージの分析を実行しないことを指定します。 |
| OutputDirectory | 作成したパッケージが格納されているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。 |
| Properties | 他のオプションの後に、コマンドラインに最後に表示されます。 プロジェクトファイルの値をオーバーライドするプロパティの一覧を指定します。「プロパティ名の[一般的な MSBuild プロジェクトプロパティ](/visualstudio/msbuild/common-msbuild-project-properties)」を参照してください。 ここでのプロパティ引数は、トークン = 値のペアの一覧です。セミコロンで区切られて`$token$`います`.nuspec` 。ファイル内での各出現箇所は、指定された値に置き換えられます。 値は、引用符で囲まれた文字列にすることができます。 "Configuration" プロパティの既定値は "Debug" であることに注意してください。 リリース構成に変更するには、 `-Properties Configuration=Release`を使用します。 |
| Suffix | *(3.4.4 +)* 内部で生成されたバージョン番号にサフィックスを追加します。通常は、ビルドまたはその他のプレリリース識別子を追加するために使用されます。 たとえば、を使用`-suffix nightly`すると、のような`1.2.3-nightly`バージョン番号のパッケージが作成されます。 サフィックスは、警告、エラー、およびさまざまなバージョンの NuGet と NuGet パッケージマネージャーとの互換性がない可能性を回避するために、英字で始める必要があります。 |
| Symbols | パッケージにソースとシンボルが含まれていることを指定します。 `.nuspec`ファイルと共に使用すると、通常の NuGet パッケージファイルと対応するシンボルパッケージが作成されます。 既定では、[レガシシンボルパッケージ](../../create-packages/Symbol-Packages.md)が作成されます。 シンボル パッケージに推奨される新しい形式は .snupkg です。 「[シンボル パッケージ (.snupkg) の作成](../../create-packages/Symbol-Packages-snupkg.md)」を参照してください。 |
| Tool | プロジェクトの出力ファイルを`tool`フォルダーに配置するように指定します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |
| Version | `.nuspec`ファイルのバージョン番号をオーバーライドします。 |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="excluding-development-dependencies"></a>開発の依存関係の除外

一部の NuGet パッケージは、独自のライブラリを作成するのに役立つ、開発の依存関係として役に立ちますが、実際のパッケージの依存関係としては必ずしも必要ではありません。

`package` コマンドは`packages.config` 、 `developmentDependency`属性がに`true`設定されているのエントリを無視します。 `pack` これらのエントリは、作成されたパッケージに依存関係として含まれません。

たとえば、ソースプロジェクトの次`packages.config`のファイルについて考えてみます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

このプロジェクトでは、によって`nuget pack`作成されたパッケージ`jQuery`は`microsoft-web-helpers`とに`netfx-Guard`依存しますが、には依存関係がありません。

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
