---
title: "NuGet シンボル パッケージの作成方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "シンボルのみを含む NuGet パッケージを作成し、Visual Studio でその他の NuGet パッケージをデバッグする方法。"
keywords: "NuGet シンボル パッケージ, NuGet パッケージ デバッグ, NuGet デバッグ対応, パッケージ シンボル, シンボル パッケージ規則"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: e1d90009c739a7f358e9581c7032523b8b284936
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="creating-symbol-packages"></a>シンボル パッケージを作成する

nuget.org やその他のソースのためにパッケージをビルドするだけでなく、NuGet では、関連するシンボル パッケージを作成し、それを SymbolSource リポジトリに公開することもできます。

公開後、パッケージ コンシューマーは Visual Studio で自分のシンボル ソースに `https://nuget.smbsrc.net` を追加できます。それにより、Visual Studio デバッガーでパッケージ コードに入ることができます。 このプロセスの詳細については、「[Visual Studio デバッガーでのシンボル (.pdb) ファイルとソース ファイルの指定](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)」を参照してください。

## <a name="creating-a-symbol-package"></a>シンボル パッケージを作成する

シンボル パッケージを作成するには、次の規則に従います。

- (コードを含む) プライマリ パッケージに `{identifier}.nupkg` という名前を付け、`.pdb` ファイルを除くすべてのファイルを含めます。
- シンボル パッケージに `{identifier}.symbols.nupkg` という名前を付け、アセンブリ DLL、`.pdb` ファイル、XMLDOC ファイル、ソース ファイルを含めます (後続のセクションを参照してください)。

いずれのパッケージも、`.nuspec` ファイルまたはプロジェクト ファイルから、`-Symbols` オプションで作成できます。

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

`pack` には Mac OS X の場合は Mono 4.4.2 が必要であり、Linux 1 システムでは動作しないことに注意してください。 Mac の場合、`.nuspec` ファイルの Windows パス名を Unix 形式のパスに変換する必要もあります。

## <a name="symbol-package-structure"></a>シンボル パッケージ構造

シンボル パッケージは、ライブラリ パッケージの場合と同じように、複数のターゲット フレームワークを対象とすることができます。そのため、`lib` フォルダーの構造はプライマリ パッケージとまったく同じになります (`.pdb` ファイルは DLL と共に含まれます)。

たとえば、NET 4.0 と Silverlight 4 を対象とするシンボル パッケージのレイアウトは次のようになります。

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

ソース ファイルは、`src` という名前の別個の特別なフォルダーに置かれます。このフォルダーはソース リポジトリの相対的構造に従う必要があります。 これは PDB に、一致する DLL のコンパイルに使用されるソース ファイルの絶対パスが含まれるためです。このパスは公開プロセス中に検出される必要があります。 基本パス (共通パス プレフィックス) は取り除くことができます。たとえば、これらのファイルからライブラリが構築されるとします。

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

`lib` フォルダーを除き、シンボル パッケージにはこのレイアウトが含まれている必要があります。

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>nuspec でファイルを参照する

シンボル パッケージは規則によって、前のセクションで説明したフォルダー構造から構築できます。あるいは、マニフェストの `files` セクションでその内容を指定することで構築できます。 たとえば、前のセクションのようなパッケージを構築するには、`.nuspec` ファイルで次を使用します。

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>シンボル パッケージを公開する

> [!Important]
> nuget.org にパッケージをプッシュするには、[nuget.exe v4.1.0 以降](https://www.nuget.org/downloads)を使用する必要があります。これは必須の [NuGet プロトコル](../api/nuget-protocols.md)を実装します。

1. 便宜上、最初に NuGet で API キーを保存します ([パッケージの公開](../create-packages/publish-a-package.md)ページを参照してください)。この保存は nuget.org と symbolsource.org の両方に適用されます。symbolsource.org はあなたがパッケージ所有者であることを nuget.org に確認するためです。

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. プライマリ パッケージを nuget.org に公開したら、シンボル パッケージを次のようにプッシュします。ファイル名の `.symbols` に起因し、symbolsource.org がターゲットとして自動的に使用されます。

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> nuget.exe 4.5.0 以上の場合、シンボル パッケージが symbolsource.org に自動的にプッシュされることはありません。次の手順で説明するように、シンボル パッケージを個別にプッシュする必要はありません。

1. 別のシンボル リポジトリに公開するには、あるいは命名規則に従わないシンボル パッケージをプッシュするには、`-Source` オプションを使用します。

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. 次を利用し、プライマリ パッケージとシンボル パッケージの両方を両方のリポジトリに同時にプッシュすることもできます。

    ```cli
    nuget push MyPackage.nupkg
    ```

その場合、NuGet はプライマリ パッケージを nuget.org に公開した後、`MyPackage.symbols.nupkg` があればそれを https://nuget.smbsrc.net/ (symbolsource.org のプッシュ URL) に公開します。

## <a name="see-also"></a>参照

[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (新しい SymbolSource エンジンへの移行) (symbolsource.org)
