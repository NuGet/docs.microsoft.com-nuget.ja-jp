---
title: レガシ シンボル パッケージ (.symbols.nupkg) の作成
description: シンボルのみを含む NuGet パッケージを作成し、Visual Studio でその他の NuGet パッケージをデバッグする方法。
author: JonDouglas
ms.author: jodou
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: d9a96986bf80aa15423d7dcee6ea3fe59255252b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774542"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a>レガシ シンボル パッケージ (.symbols.nupkg) の作成

> [!Important]
> シンボル パッケージに推奨される新しい形式は .snupkg です。 「[シンボル パッケージ (.snupkg) の作成](Symbol-Packages-snupkg.md)」を参照してください。 </br>
> .symbols.nupkg は、互換性のためにのみ、引き続きサポートされます。

nuget.org やその他のソースに向けたパッケージの構築だけでなく、NuGet では、シンボル サーバーに公開可能な関連するシンボル パッケージの作成もサポートされています。 レガシ シンボル パッケージの形式である .symbols.nupkg は、SymbolSource リポジトリにプッシュすることができます。

公開後、パッケージ コンシューマーは Visual Studio で自分のシンボル ソースに `https://nuget.smbsrc.net` を追加できます。それにより、Visual Studio デバッガーでパッケージ コードに入ることができます。 このプロセスの詳細については、「[Visual Studio デバッガーでのシンボル (.pdb) ファイルとソース ファイルの指定](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)」を参照してください。

## <a name="creating-a-legacy-symbol-package"></a>レガシ シンボル パッケージの作成

レガシ シンボル パッケージを作成するには、次の規則に従います。

- (コードを含む) プライマリ パッケージに `{identifier}.nupkg` という名前を付け、`.pdb` ファイルを除くすべてのファイルを含めます。
- レガシ シンボル パッケージに `{identifier}.symbols.nupkg` という名前を付け、アセンブリ DLL、`.pdb` ファイル、XMLDOC ファイル、ソース ファイルを含めます (後続のセクションを参照)。

いずれのパッケージも、`.nuspec` ファイルまたはプロジェクト ファイルから、`-Symbols` オプションで作成できます。

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

`pack` には Mac OS X の場合は Mono 4.4.2 が必要であり、Linux 1 システムでは動作しないことに注意してください。 Mac の場合、`.nuspec` ファイルの Windows パス名を Unix 形式のパスに変換する必要もあります。

## <a name="legacy-symbol-package-structure"></a>レガシ シンボル パッケージの構造

レガシ シンボル パッケージは、ライブラリ パッケージと同様の方法で複数のターゲット フレームワークを対象とすることができます。そのため、`lib` フォルダーの構造はプライマリ パッケージとまったく同じになります (`.pdb` ファイルは DLL と共に含まれます)。

たとえば、NET 4.0 と Silverlight 4 をターゲットとするレガシ シンボル パッケージのレイアウトは次のようになります。

```
\lib
    \net40
        \MyAssembly.dll
        \MyAssembly.pdb
    \sl40
        \MyAssembly.dll
        \MyAssembly.pdb
```

ソース ファイルは、`src` という名前の別個の特別なフォルダーに置かれます。このフォルダーはソース リポジトリの相対的構造に従う必要があります。 これは PDB に、一致する DLL のコンパイルに使用されるソース ファイルの絶対パスが含まれるためです。このパスは公開プロセス中に検出される必要があります。 基本パス (共通パス プレフィックス) は取り除くことができます。たとえば、これらのファイルからライブラリが構築されるとします。

```
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
```

`lib` フォルダーを除き、レガシ シンボル パッケージには次のレイアウトが含まれている必要があります。

```
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
```

## <a name="referring-to-files-in-the-nuspec"></a>nuspec でファイルを参照する

レガシ シンボル パッケージは、前のセクションで説明したフォルダー構造から、規則によって構築できます。あるいは、マニフェストの `files` セクションにその内容を指定することで構築できます。 たとえば、前のセクションのようなパッケージを構築するには、`.nuspec` ファイルで次を使用します。

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a>レガシ シンボル パッケージの公開

> [!Important]
> nuget.org にパッケージをプッシュするには、[nuget.exe v4.9.1 以降](https://www.nuget.org/downloads)を使用する必要があります。これは必須の [NuGet プロトコル](../api/nuget-protocols.md)を実装します。

1. 便宜上、最初に NuGet で API キーを保存します ([パッケージの公開](../nuget-org/publish-a-package.md)ページを参照してください)。この保存は nuget.org と symbolsource.org の両方に適用されます。symbolsource.org はあなたがパッケージ所有者であることを nuget.org に確認するためです。

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. プライマリ パッケージを nuget.org に公開したら、レガシ シンボル パッケージを次のようにプッシュします。ファイル名の `.symbols` によって、symbolsource.org が自動的にターゲットとして使用されます。

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. 別のシンボル リポジトリに公開するか、命名規則に従わないレガシ シンボル パッケージをプッシュするには、`-Source` オプションを使用します。

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. 次を利用し、プライマリ パッケージとシンボル パッケージの両方を両方のリポジトリに同時にプッシュすることもできます。

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > nuget.exe 4.5.0 以上の場合、シンボル パッケージが symbolsource.org に自動的にプッシュされることはありません。前の手順で説明したように、シンボル パッケージを個別にプッシュする必要があります。
   
その場合、NuGet は、nuget.org にプライマリ パッケージを公開した後、`MyPackage.symbols.nupkg` があればそれを https://nuget.smbsrc.net/ (symbolsource.org のプッシュ URL) に公開します。

## <a name="see-also"></a>関連項目

* [シンボル パッケージ (.snupkg) の作成](Symbol-Packages-snupkg.md) - シンボル パッケージに推奨される新しい形式です
* [Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (新しい SymbolSource エンジンへの移行) (symbolsource.org)
