---
title: レガシ シンボル パッケージ (.symbols.nupkg) の作成
description: シンボルのみを含む NuGet パッケージを作成し、Visual Studio でその他の NuGet パッケージをデバッグする方法。
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 374e9ccfc01cd06508e76529765db3f849342222
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "77476270"
---
# <a name="creating-legacy-symbol-packages-symbolsnupkg"></a><span data-ttu-id="8a9bb-103">レガシ シンボル パッケージ (.symbols.nupkg) の作成</span><span class="sxs-lookup"><span data-stu-id="8a9bb-103">Creating legacy symbol packages (.symbols.nupkg)</span></span>

> [!Important]
> <span data-ttu-id="8a9bb-104">シンボル パッケージに推奨される新しい形式は .snupkg です。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-104">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="8a9bb-105">「[シンボル パッケージ (.snupkg) の作成](Symbol-Packages-snupkg.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-105">See [Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md).</span></span> </br>
> <span data-ttu-id="8a9bb-106">.symbols.nupkg は、互換性のためにのみ、引き続きサポートされます。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-106">.symbols.nupkg is still supported but only for compatibility reasons.</span></span>

<span data-ttu-id="8a9bb-107">nuget.org やその他のソースに向けたパッケージの構築だけでなく、NuGet では、シンボル サーバーに公開可能な関連するシンボル パッケージの作成もサポートされています。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-107">In addition to building packages for nuget.org or other sources, NuGet also supports creating associated symbol packages that can be published to symbol servers.</span></span> <span data-ttu-id="8a9bb-108">レガシ シンボル パッケージの形式である .symbols.nupkg は、SymbolSource リポジトリにプッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-108">The legacy symbol package format, .symbols.nupkg, can be pushed to the SymbolSource repository.</span></span>

<span data-ttu-id="8a9bb-109">公開後、パッケージ コンシューマーは Visual Studio で自分のシンボル ソースに `https://nuget.smbsrc.net` を追加できます。それにより、Visual Studio デバッガーでパッケージ コードに入ることができます。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-109">Package consumers can then add `https://nuget.smbsrc.net` to their symbol sources in Visual Studio, which allows stepping into package code in the Visual Studio debugger.</span></span> <span data-ttu-id="8a9bb-110">このプロセスの詳細については、「[Visual Studio デバッガーでのシンボル (.pdb) ファイルとソース ファイルの指定](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-110">See [Specify symbol (.pdb) and source files in the Visual Studio debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger) for details on that process.</span></span>

## <a name="creating-a-legacy-symbol-package"></a><span data-ttu-id="8a9bb-111">レガシ シンボル パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="8a9bb-111">Creating a legacy symbol package</span></span>

<span data-ttu-id="8a9bb-112">レガシ シンボル パッケージを作成するには、次の規則に従います。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-112">To create a legacy symbol package, follow these conventions:</span></span>

- <span data-ttu-id="8a9bb-113">(コードを含む) プライマリ パッケージに `{identifier}.nupkg` という名前を付け、`.pdb` ファイルを除くすべてのファイルを含めます。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-113">Name the primary package (with your code) `{identifier}.nupkg` and include all your files except `.pdb` files.</span></span>
- <span data-ttu-id="8a9bb-114">レガシ シンボル パッケージに `{identifier}.symbols.nupkg` という名前を付け、アセンブリ DLL、`.pdb` ファイル、XMLDOC ファイル、ソース ファイルを含めます (後続のセクションを参照)。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-114">Name the legacy symbol package `{identifier}.symbols.nupkg` and include your assembly DLL, `.pdb` files, XMLDOC files, source files (see the sections that follow).</span></span>

<span data-ttu-id="8a9bb-115">いずれのパッケージも、`.nuspec` ファイルまたはプロジェクト ファイルから、`-Symbols` オプションで作成できます。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-115">You can create both packages with the `-Symbols` option, either from a `.nuspec` file or a project file:</span></span>

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

<span data-ttu-id="8a9bb-116">`pack` には Mac OS X の場合は Mono 4.4.2 が必要であり、Linux 1 システムでは動作しないことに注意してください。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-116">Note that `pack` requires Mono 4.4.2 on Mac OS X and does not work on Linux systems.</span></span> <span data-ttu-id="8a9bb-117">Mac の場合、`.nuspec` ファイルの Windows パス名を Unix 形式のパスに変換する必要もあります。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-117">On a Mac, you must also convert Windows pathnames in the `.nuspec` file to Unix-style paths.</span></span>

## <a name="legacy-symbol-package-structure"></a><span data-ttu-id="8a9bb-118">レガシ シンボル パッケージの構造</span><span class="sxs-lookup"><span data-stu-id="8a9bb-118">Legacy symbol package structure</span></span>

<span data-ttu-id="8a9bb-119">レガシ シンボル パッケージは、ライブラリ パッケージと同様の方法で複数のターゲット フレームワークを対象とすることができます。そのため、`lib` フォルダーの構造はプライマリ パッケージとまったく同じになります (`.pdb` ファイルは DLL と共に含まれます)。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-119">A legacy symbol package can target multiple target frameworks in the same way that a library package does, so the structure of the `lib` folder should be exactly the same as the primary package, only including `.pdb` files alongside the DLL.</span></span>

<span data-ttu-id="8a9bb-120">たとえば、NET 4.0 と Silverlight 4 をターゲットとするレガシ シンボル パッケージのレイアウトは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-120">For example, a legacy symbol package that targets .NET 4.0 and Silverlight 4 would have this layout:</span></span>

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

<span data-ttu-id="8a9bb-121">ソース ファイルは、`src` という名前の別個の特別なフォルダーに置かれます。このフォルダーはソース リポジトリの相対的構造に従う必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-121">Source files are then placed in a separate special folder named `src`, which must follow the relative structure of your source repository.</span></span> <span data-ttu-id="8a9bb-122">これは PDB に、一致する DLL のコンパイルに使用されるソース ファイルの絶対パスが含まれるためです。このパスは公開プロセス中に検出される必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-122">This is because PDBs contain absolute paths to source files used to compile the matching DLL, and they need to be found during the publishing process.</span></span> <span data-ttu-id="8a9bb-123">基本パス (共通パス プレフィックス) は取り除くことができます。たとえば、これらのファイルからライブラリが構築されるとします。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-123">A base path (common path prefix) can be stripped out. For example, consider a library built from these files:</span></span>

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

<span data-ttu-id="8a9bb-124">`lib` フォルダーを除き、レガシ シンボル パッケージには次のレイアウトが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-124">Apart from the `lib` folder, a legacy symbol package would need to contain this layout:</span></span>

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

## <a name="referring-to-files-in-the-nuspec"></a><span data-ttu-id="8a9bb-125">nuspec でファイルを参照する</span><span class="sxs-lookup"><span data-stu-id="8a9bb-125">Referring to files in the nuspec</span></span>

<span data-ttu-id="8a9bb-126">レガシ シンボル パッケージは、前のセクションで説明したフォルダー構造から、規則によって構築できます。あるいは、マニフェストの `files` セクションにその内容を指定することで構築できます。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-126">A legacy symbol package can be built by conventions, from a folder structure as described in the previous section, or by specifying its contents in the `files` section of the manifest.</span></span> <span data-ttu-id="8a9bb-127">たとえば、前のセクションのようなパッケージを構築するには、`.nuspec` ファイルで次を使用します。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-127">For example, to build the package shown in the previous section, use the following in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-legacy-symbol-package"></a><span data-ttu-id="8a9bb-128">レガシ シンボル パッケージの公開</span><span class="sxs-lookup"><span data-stu-id="8a9bb-128">Publishing a legacy symbol package</span></span>

> [!Important]
> <span data-ttu-id="8a9bb-129">nuget.org にパッケージをプッシュするには、[nuget.exe v4.9.1 以降](https://www.nuget.org/downloads)を使用する必要があります。これは必須の [NuGet プロトコル](../api/nuget-protocols.md)を実装します。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-129">To push packages to nuget.org you must use [nuget.exe v4.9.1 or above](https://www.nuget.org/downloads), which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

1. <span data-ttu-id="8a9bb-130">便宜上、最初に NuGet で API キーを保存します ([パッケージの公開](../nuget-org/publish-a-package.md)ページを参照してください)。この保存は nuget.org と symbolsource.org の両方に適用されます。symbolsource.org はあなたがパッケージ所有者であることを nuget.org に確認するためです。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-130">For convenience, first save your API key with NuGet (see [publish a package](../nuget-org/publish-a-package.md), which will apply to both nuget.org and symbolsource.org, because symbolsource.org will check with nuget.org to verify that you are the package owner.</span></span>

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. <span data-ttu-id="8a9bb-131">プライマリ パッケージを nuget.org に公開したら、レガシ シンボル パッケージを次のようにプッシュします。ファイル名の `.symbols` によって、symbolsource.org が自動的にターゲットとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-131">After publishing your primary package to nuget.org, push the legacy symbol package as follows, which will automatically use symbolsource.org as the target because of the `.symbols` in the filename:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. <span data-ttu-id="8a9bb-132">別のシンボル リポジトリに公開するか、命名規則に従わないレガシ シンボル パッケージをプッシュするには、`-Source` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-132">To publish to a different symbol repository, or to push a legacy symbol package that doesn't follow the naming convention, use the `-Source` option:</span></span>

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. <span data-ttu-id="8a9bb-133">次を利用し、プライマリ パッケージとシンボル パッケージの両方を両方のリポジトリに同時にプッシュすることもできます。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-133">You can also push both primary and symbol packages to both repositories at the same time using the following:</span></span>

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > <span data-ttu-id="8a9bb-134">nuget.exe 4.5.0 以上の場合、シンボル パッケージが symbolsource.org に自動的にプッシュされることはありません。前の手順で説明したように、シンボル パッケージを個別にプッシュする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-134">With nuget.exe 4.5.0 or above, the symbols packages are not automatically pushed to symbolsource.org. You would need to push the symbols packages separately as explained in the earlier steps.</span></span>
   
<span data-ttu-id="8a9bb-135">その場合、NuGet は、nuget.org にプライマリ パッケージを公開した後、`MyPackage.symbols.nupkg` があればそれを https://nuget.smbsrc.net/ (symbolsource.org のプッシュ URL) に公開します。</span><span class="sxs-lookup"><span data-stu-id="8a9bb-135">In this case, NuGet will publish `MyPackage.symbols.nupkg`, if present, to https://nuget.smbsrc.net/ (the push URL for symbolsource.org), after it publishes the primary package to nuget.org.</span></span>

## <a name="see-also"></a><span data-ttu-id="8a9bb-136">関連項目</span><span class="sxs-lookup"><span data-stu-id="8a9bb-136">See also</span></span>

* <span data-ttu-id="8a9bb-137">[シンボル パッケージ (.snupkg) の作成](Symbol-Packages-snupkg.md) - シンボル パッケージに推奨される新しい形式です</span><span class="sxs-lookup"><span data-stu-id="8a9bb-137">[Creating symbol packages (.snupkg)](Symbol-Packages-snupkg.md) - The new recommended format for symbol packages</span></span>
* <span data-ttu-id="8a9bb-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (新しい SymbolSource エンジンへの移行) (symbolsource.org)</span><span class="sxs-lookup"><span data-stu-id="8a9bb-138">[Moving to the new SymbolSource engine](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)</span></span>
