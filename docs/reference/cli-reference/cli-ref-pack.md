---
title: NuGet CLI パックコマンド
description: nuget.exe pack コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0483a75c7ee1fd851f935f44d96a417e2e86bf20
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622955"
---
# <a name="pack-command-nuget-cli"></a>pack コマンド (NuGet CLI)

**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** 2.7 以上

指定された [nuspec](../nuspec.md) またはプロジェクトファイルに基づいて NuGet パッケージを作成します。 `dotnet pack`コマンド (「 [dotnet コマンド](../dotnet-Commands.md)」を参照) と `msbuild -t:pack` (「 [MSBuild ターゲット](../msbuild-targets.md)」を参照) は、代替として使用できます。

> [!Important]
> [`dotnet pack`](../dotnet-Commands.md) [`msbuild -t:pack`](../msbuild-targets.md) [PackageReference](../../consume-packages/package-references-in-project-files.md)ベースのプロジェクトでは、またはを使用します。
> Mono では、プロジェクトファイルからパッケージを作成することはサポートされていません。 また、Windows のパス名は変換されないため、ファイル内のローカルではないパスを Unix 形式のパスに調整する必要があり `.nuspec` nuget.exe。

## <a name="usage"></a>使用法

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

`<nuspecPath>`と `<projectPath>` は、 `.nuspec` それぞれまたはプロジェクトファイルを指定します。

## <a name="options"></a>Options
- **`-BasePath`**

   [Nuspec](../nuspec.md)ファイルで定義されているファイルのベースパスを設定します。

- **`-Build`**

  パッケージをビルドする前にプロジェクトをビルドするように指定します。

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-Exclude`**

  パッケージの作成時に除外する1つ以上のワイルドカードパターンを指定します。 複数のパターンを指定するには、-Exclude フラグを繰り返します。 以下の例を参照してください。

- **`-ExcludeEmptyDirectories`**

  パッケージをビルドするときに空のディレクトリを含めないようにします。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-IncludeReferencedProjects`**

  ビルドされたパッケージに、依存関係として、またはパッケージの一部として参照プロジェクトを含める必要があることを示します。 参照先のプロジェクトに、 `.nuspec` プロジェクトと同じ名前の対応するファイルがある場合、その参照先プロジェクトは依存関係として追加されます。 それ以外の場合、参照されるプロジェクトはパッケージの一部として追加されます。

- **`-InstallPackageToOutputPath`**

  コマンドで、共有をフィードとしてサポートするようにパッケージ出力ディレクトリを準備する必要があるかどうかを指定します。

- **`-MinClientVersion`**

  作成したパッケージの *minClientVersion* 属性を設定します。 この値は、ファイル内の既存の *minClientVersion* 属性 (存在する場合) の値よりも優先され `.nuspec` ます。

- **`-MSBuildPath`**

  *(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これはよりも優先さ `-MSBuildVersion` れます。

- **`-MSBuildVersion`**

  *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。

- **`-NoDefaultExcludes`**

  やなど、ドットで始まる NuGet パッケージファイルとファイルおよびフォルダーの既定の除外を回避し `.svn` `.gitignore` ます。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-NoPackageAnalysis`**

  パッケージのビルド後に、パックでパッケージの分析を実行しないことを指定します。

- **`-OutputDirectory`**

  作成したパッケージが格納されているフォルダーを指定します。 フォルダーが指定されていない場合は、現在のフォルダーが使用されます。

- **`-OutputFileNamesWithoutVersion`**

  コマンドでバージョンを指定せずにパッケージの出力名を準備するかどうかを指定します。

- **`-PackagesDirectory`**

  Packages フォルダーを指定します。

- **`-p|-Properties`**

  他のオプションの後に、コマンドラインに最後に表示されます。 プロジェクトファイルの値をオーバーライドするプロパティの一覧を指定します。「プロパティ名の [一般的な MSBuild プロジェクトプロパティ](/visualstudio/msbuild/common-msbuild-project-properties) 」を参照してください。 ここでのプロパティ引数は、トークン = 値のペアの一覧です。セミコロンで区切られています。ファイル内での各出現箇所は、 `$token$` `.nuspec` 指定された値に置き換えられます。 値は、引用符で囲まれた文字列にすることができます。 "Configuration" プロパティの既定値は "Debug" であることに注意してください。 リリース構成に変更するには、を使用し `-Properties Configuration=Release` ます。 **一般に**、プロパティは、予期しない動作を避けるために、対応するプロジェクトのビルド中に使用されたものと同じである必要があります。

- **`-SolutionDirectory`**

  ソリューションディレクトリを指定します。

- **`-Suffix`**

  *(3.4.4 +)* 内部で生成されたバージョン番号にサフィックスを追加します。通常は、ビルドまたはその他のプレリリース識別子を追加するために使用されます。 たとえば、を使用すると、の `-suffix nightly` ようなバージョン番号のパッケージが作成され `1.2.3-nightly` ます。 サフィックスは、警告、エラー、およびさまざまなバージョンの NuGet と NuGet パッケージマネージャーとの互換性がない可能性を回避するために、英字で始める必要があります。

- **`-SymbolPackageFormat`**

  シンボルパッケージを作成するときに、で形式と形式のどちらかを選択でき `snupkg` `symbols.nupkg` ます。

- **`-Symbols`**

  パッケージにソースとシンボルが含まれていることを指定します。 ファイルと共に使用すると `.nuspec` 、通常の NuGet パッケージファイルと対応するシンボルパッケージが作成されます。 既定では、 [レガシシンボルパッケージ](../../create-packages/Symbol-Packages.md)が作成されます。 シンボル パッケージに推奨される新しい形式は .snupkg です。 「[シンボル パッケージ (.snupkg) の作成](../../create-packages/Symbol-Packages-snupkg.md)」を参照してください。

- **`-Tool`**

   プロジェクトの出力ファイルをフォルダーに配置するように指定し `tool` ます。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

- **`-Version`**

  ファイルのバージョン番号をオーバーライドし `.nuspec` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="excluding-development-dependencies"></a>開発の依存関係の除外

一部の NuGet パッケージは、独自のライブラリを作成するのに役立つ、開発の依存関係として役に立ちますが、実際のパッケージの依存関係としては必ずしも必要ではありません。

コマンドは、 `pack` 属性がに設定されて `package` いるのエントリを無視し `packages.config` `developmentDependency` `true` ます。 これらのエントリは、作成されたパッケージに依存関係として含まれません。

たとえば、ソースプロジェクトの次のファイルについて考えてみ `packages.config` ます。

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

このプロジェクトでは、によって作成されたパッケージは `nuget pack` とに依存しますが、には依存関係があり `jQuery` `microsoft-web-helpers` ません `netfx-Guard` 。

## <a name="suppressing-pack-warnings"></a>非表示 (パックの警告を)

パック操作中にすべての NuGet 警告を解決することをお勧めしますが、特定の状況では、それらを抑制することが保証されます。

これは、次の方法で実現できます。 

> nuget.exe pack nuspec NoWarn = NU5104

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
