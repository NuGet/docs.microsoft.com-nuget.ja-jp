---
title: プロジェクトによって参照されるアセンブリを選択する
description: 実行時にすべてのアセンブリを利用できるとき、パッケージに含まれるアセンブリのサブセットをコンパイラで利用できるようにします。
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859032"
---
# <a name="select-assemblies-referenced-by-projects"></a><span data-ttu-id="a0cca-103">プロジェクトによって参照されるアセンブリを選択する</span><span class="sxs-lookup"><span data-stu-id="a0cca-103">Select Assemblies Referenced By Projects</span></span>

<span data-ttu-id="a0cca-104">実行時にすべてのアセンブリを利用できるとき、明示的なアセンブリ参照により、IntelliSense やコンパイルでアセンブリのサブセットを使用できます。</span><span class="sxs-lookup"><span data-stu-id="a0cca-104">Explicit assembly references allows a subset of assemblies to be used for IntelliSense and compiling, while all assemblies are available at run-time.</span></span> <span data-ttu-id="a0cca-105">`PackageReference` と `packages.config` では動作が異なるため、パッケージの作成者は両方のプロジェクト タイプと互換性があるパッケージを作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0cca-105">`PackageReference` and `packages.config` work differently, and as a result package authors need to take care to create the package to be compatible with both project types.</span></span>

> [!Note]
> <span data-ttu-id="a0cca-106">明示的なアセンブリ参照は .NET アセンブリに関連します。</span><span class="sxs-lookup"><span data-stu-id="a0cca-106">Explicit assembly references are related to .NET assemblies.</span></span> <span data-ttu-id="a0cca-107">マネージド アセンブリでプラットフォーム呼び出しされるネイティブ アセンブリを配布するメソッドではありません。</span><span class="sxs-lookup"><span data-stu-id="a0cca-107">It is not a method to distribute native assemblies that are P/Invoked by a managed assembly.</span></span>

## <a name="packagereference-support"></a><span data-ttu-id="a0cca-108">`PackageReference` サポート</span><span class="sxs-lookup"><span data-stu-id="a0cca-108">`PackageReference` support</span></span>

<span data-ttu-id="a0cca-109">あるプロジェクトで `PackageReference` を含むパッケージが使用されるとき、そのパッケージに `ref\<tfm>\` ディレクトリが含まれている場合、NuGet では、それらのアセンブリがコンパイル時アセットとして分類され、`lib\<tfm>\` アセンブリは実行時アセットとして分類されます。</span><span class="sxs-lookup"><span data-stu-id="a0cca-109">When a project uses a package with `PackageReference` and the package contains a `ref\<tfm>\` directory, NuGet will classify those assembles as compile-time assets, while the `lib\<tfm>\` assemblies are classified as runtime assets.</span></span> <span data-ttu-id="a0cca-110">`ref\<tfm>\` のアセンブリは実行時に使用されません。</span><span class="sxs-lookup"><span data-stu-id="a0cca-110">Assemblies in `ref\<tfm>\` are not used at runtime.</span></span> <span data-ttu-id="a0cca-111">つまり、`ref\<tfm>\` のあらゆるアセンブリには、`lib\<tfm>\` または関連する `runtime\` ディレクトリに一致するアセンブリがあることが求められます。ない場合、実行時エラーがおそらく発生します。</span><span class="sxs-lookup"><span data-stu-id="a0cca-111">This means it is necessary for any assembly in `ref\<tfm>\` to have a matching assembly in either `lib\<tfm>\` or a relevant `runtime\` directory, otherwise runtime errors will likely occur.</span></span> <span data-ttu-id="a0cca-112">`ref\<tfm>\` のアセンブリは実行時に使用されないため、パッケージ サイズを減らす[メタデータのみのアセンブリ](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md)になることがあります。</span><span class="sxs-lookup"><span data-stu-id="a0cca-112">Since assemblies in `ref\<tfm>\` are not used at runtime, they may be [metadata-only assemblies](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) to reduce package size.</span></span>

> [!Important]
> <span data-ttu-id="a0cca-113">あるパッケージに nuspec `<references>` 要素 (`packages.config` で使用、下記) が含まれるが、`ref\<tfm>\` のアセンブリが含まれない場合、NuGet では、コンパイル アセットとランタイム アセットの両方として、nuspec `<references>` 要素に一覧表示されるアセンブリがアドバタイズされます。</span><span class="sxs-lookup"><span data-stu-id="a0cca-113">If a package contains the nuspec `<references>` element (used by `packages.config`, see below) and does not contain assemblies in `ref\<tfm>\`, NuGet will advertise the assemblies listed in the nuspec `<references>` element as both the compile and runtime assets.</span></span> <span data-ttu-id="a0cca-114">つまり、参照されるアセンブリで `lib\<tfm>\` ディレクトリに他のアセンブリを読み込む必要があるとき、ランタイム例外が発生します。</span><span class="sxs-lookup"><span data-stu-id="a0cca-114">This means there will be runtime exceptions when the referenced assemblies need to load any other assembly in the `lib\<tfm>\` directory.</span></span>

> [!Note]
> <span data-ttu-id="a0cca-115">パッケージに `runtime\` ディレクトリが含まれる場合、NuGet では `lib\` ディレクトリのアセットが使用されないことがあります。</span><span class="sxs-lookup"><span data-stu-id="a0cca-115">If the package contains a `runtime\` directory, NuGet may not use the assets in the `lib\` directory.</span></span>

## <a name="packagesconfig-support"></a><span data-ttu-id="a0cca-116">`packages.config` サポート</span><span class="sxs-lookup"><span data-stu-id="a0cca-116">`packages.config` support</span></span>

<span data-ttu-id="a0cca-117">`packages.config` を使用して NuGet パッケージを管理するプロジェクトでは通常、`lib\<tfm>\` ディレクトリのすべてのアセンブリに参照が追加されます。</span><span class="sxs-lookup"><span data-stu-id="a0cca-117">Projects using `packages.config` to manage NuGet packages normally add references to all assemblies in the `lib\<tfm>\` directory.</span></span> <span data-ttu-id="a0cca-118">`ref\` ディレクトリは `PackageReference` をサポートする目的で追加されており、`packages.config` の使用時には考慮されません。</span><span class="sxs-lookup"><span data-stu-id="a0cca-118">The `ref\` directory was added to support `PackageReference` and therefore isn't considered when using `packages.config`.</span></span> <span data-ttu-id="a0cca-119">`packages.config` を使用するプロジェクトで参照されるアセンブリを明示的に設定するには、パッケージで [nuspec ファイルの `<references>` 要素](../reference/nuspec.md#explicit-assembly-references)を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0cca-119">To explicitly set which assemblies are referenced for projects using `packages.config`, the package must use the [`<references>` element in the nuspec file](../reference/nuspec.md#explicit-assembly-references).</span></span> <span data-ttu-id="a0cca-120">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="a0cca-120">For example:</span></span>

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> <span data-ttu-id="a0cca-121">`packages.config` プロジェクトでは、[ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) というプロセスを使用し、`bin\<configuration>\` 出力ディレクトリにアセンブリをコピーします。</span><span class="sxs-lookup"><span data-stu-id="a0cca-121">`packages.config` project use a process called [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md) to copy assemblies to the `bin\<configuration>\` output directory.</span></span> <span data-ttu-id="a0cca-122">プロジェクトのアセンブリがコピーされると、ビルド システムがアセンブリ マニフェストで参照アセンブリを探し、そのアセンブリをコピーし、すべてのアセンブリに再帰的に繰り返します。</span><span class="sxs-lookup"><span data-stu-id="a0cca-122">Your project's assembly is copied, then the build system looks at the assembly manifest for referenced assemblies, then copies those assemblies and recursively repeats for all assemblies.</span></span> <span data-ttu-id="a0cca-123">つまり、`lib\<tfm>\` ディレクトリのいずれかのアセンブリが他のアセンブリのマニフェストに依存関係として一覧表示されない場合 (`Assembly.Load`、MEF、またはその他の依存関係挿入フレームワークを利用し、実行時にアセンブリが読み込まれる場合)、`bin\<tfm>\` にあるとしても、プロジェクトの `bin\<configuration>\` 出力ディレクトリにコピーされないことがあります。</span><span class="sxs-lookup"><span data-stu-id="a0cca-123">This means that if any of the assemblies in your `lib\<tfm>\` directory are not listed in any other assembly's manifest as a dependency (if the assembly is loaded at runtime using `Assembly.Load`, MEF or another dependency injection framework), then it may not be copied to your project's `bin\<configuration>\` output directory despite being in `bin\<tfm>\`.</span></span>

## <a name="example"></a><span data-ttu-id="a0cca-124">例</span><span class="sxs-lookup"><span data-stu-id="a0cca-124">Example</span></span>

<span data-ttu-id="a0cca-125">パッケージには、.NET Framework 4.7.2 を対象とする 3 つのアセンブリ (`MyLib.dll`、`MyHelpers.dll`、`MyUtilities.dll`) が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a0cca-125">My package will contain three assemblies, `MyLib.dll`, `MyHelpers.dll` and `MyUtilities.dll`, which are targeting the .NET Framework 4.7.2.</span></span> <span data-ttu-id="a0cca-126">`MyUtilities.dll` には、他の 2 つのアセンブリでのみ使用されるクラスが含まれます。そのため、IntelliSense やコンパイルで、自分のパッケージを使用するプロジェクトでそれらのクラスを利用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="a0cca-126">`MyUtilities.dll` contains classes intended to be used only by the other two assemblies, so I don't want to make those classes available in IntelliSense or at compile time to projects using my package.</span></span> <span data-ttu-id="a0cca-127">`nuspec` ファイルには、次の XML 要素を含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0cca-127">My `nuspec` file needs to contain the following XML elements:</span></span>

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

<span data-ttu-id="a0cca-128">パッケージのファイルは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="a0cca-128">and the files in the package will be:</span></span>

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
