---
title: NuGet パッケージの複数バージョン対応
description: 1 つの NuGet パッケージ内から複数の .NET Framework バージョンに対応するためのさまざま方法の説明。
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 34f7c6132ba6050e20114642932ccf29a5ec088d
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428625"
---
# <a name="support-multiple-net-versions"></a><span data-ttu-id="7dd8a-103">複数の .NET バージョンをサポートする</span><span class="sxs-lookup"><span data-stu-id="7dd8a-103">Support multiple .NET versions</span></span>

<span data-ttu-id="7dd8a-104">多くのライブラリは、特定のバージョンの .NET Framework に対応しています。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-104">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="7dd8a-105">たとえば、あるバージョンのライブラリは UWP に固有であり、別のバージョンは .NET Framework 4.6 の機能を活用します。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-105">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span> <span data-ttu-id="7dd8a-106">これに対応するために、NuGet では 1 つのパッケージに同じライブラリの複数のバージョンを配置することがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-106">To accommodate this, NuGet supports putting multiple versions of the same library in a single package.</span></span>

<span data-ttu-id="7dd8a-107">この記事では、パッケージやアセンブリのビルド方法に関係なく、NuGet パッケージのレイアウトについて説明します (つまり、SDK スタイルではない複数の *.csproj* ファイルとカスタムの *.nuspec* ファイルを使う場合でも、複数をターゲットにした SDK スタイルの *.csproj* を単一ファイルで使う場合でも、レイアウトは同じです)。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-107">This article describes the layout of a NuGet package, regardless of how the package or assemblies are built (that is, the layout is the same whether using multiple non-SDK-style *.csproj* files and a custom *.nuspec* file, or a single multi-targeted SDK-style *.csproj*).</span></span> <span data-ttu-id="7dd8a-108">SDK スタイルのプロジェクトの場合、NuGet の [pack ターゲット](../reference/msbuild-targets.md)では、パッケージの整理方法が認識され、適切な lib フォルダーにアセンブリを配置したり、ターゲット フレームワーク (TFM) ごとに依存関係グループを作成する操作が自動化されます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-108">For an SDK-style project, NuGet [pack targets](../reference/msbuild-targets.md) knows how the package must be layed out and automates putting the assemblies in the correct lib folders and creating dependency groups for each target framework (TFM).</span></span> <span data-ttu-id="7dd8a-109">詳細な手順については、「[プロジェクト ファイル内で複数の .NET Framework バージョンをサポートする](multiple-target-frameworks-project-file.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-109">For detailed instructions, see [Support multiple .NET Framework versions in your project file](multiple-target-frameworks-project-file.md).</span></span>

<span data-ttu-id="7dd8a-110">「[パッケージの作成](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)」で説明されている規則ベースの作業ディレクトリを使用する場合は、この記事の説明に従って手動でパッケージをレイアウトする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-110">You must manually lay out the package as described in this article when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> <span data-ttu-id="7dd8a-111">SDK スタイルのプロジェクトでは自動の方法を使用することをお勧めしますが、この記事で説明されているように、パッケージを手動で配置することもできます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-111">For an SDK-style project, the automated method is recommended, but you may also choose to manually lay out the package as described in this article.</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="7dd8a-112">フレームワーク バージョンのフォルダー構造</span><span class="sxs-lookup"><span data-stu-id="7dd8a-112">Framework version folder structure</span></span>

<span data-ttu-id="7dd8a-113">1 つだけのバージョンのライブラリを含むパッケージまたは複数のフレームワークを対象とするパッケージをビルドするときは常に、小文字と大文字を区別するフレームワーク名を利用し、`lib` の下にサブフォルダーを作ります。次の規則を利用します。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-113">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="7dd8a-114">サポートされている名前の完全一覧については、[ターゲット フレームワーク参照](../reference/target-frameworks.md#supported-frameworks)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-114">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="7dd8a-115">フレームワークに固有ではないライブラリ バージョンは、ルート `lib` フォルダーに直接置かないでください。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-115">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="7dd8a-116">(この機能は `packages.config` でのみサポートされていました。)</span><span class="sxs-lookup"><span data-stu-id="7dd8a-116">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="7dd8a-117">これにより、ライブラリがあらゆるターゲット フレームワークに対応するようになり、どこでもインストールできてしまいます。その結果、予想外のランタイム エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-117">Doing so would make the library compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="7dd8a-118">ルート フォルダー (`lib\abc.dll` など) またはサブフォルダー (`lib\abc\abc.dll` など) へのアセンブリ追加は非推奨となりました。PackagesReference 形式を使用するときは無視されます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-118">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="7dd8a-119">たとえば、次のフォルダー構造では、フレームワーク固有の 4 つのバージョンのアセンブリがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-119">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="7dd8a-120">パッケージのビルド時、これらすべてのファイルを簡単に含めるには、`**` の `<files>` セクションに再帰的 `.nuspec` ワイルドカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-120">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="7dd8a-121">アーキテクチャ固有フォルダー</span><span class="sxs-lookup"><span data-stu-id="7dd8a-121">Architecture-specific folders</span></span>

<span data-ttu-id="7dd8a-122">アーキテクチャ固有のアセンブリがあるとき、つまり、個々のアセンブリが ARM、x86、x64 を対象とするとき、`runtimes` という名前のフォルダーの `{platform}-{architecture}\lib\{framework}` または `{platform}-{architecture}\native` という名前のサブフォルダー内にそれを置く必要があります。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-122">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="7dd8a-123">たとえば、次のフォルダー構造は、Windows 10 と `uap10.0` フレームワークを対象とするネイティブ DLL とマネージド DLL の両方に対応します。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-123">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

    \runtimes
        \win10-arm
            \native
            \lib\uap10.0
        \win10-x86
            \native
            \lib\uap10.0
        \win10-x64
            \native
            \lib\uap10.0

<span data-ttu-id="7dd8a-124">これらのアセンブリはランタイムでのみ使用できます。そのため、対応するコンパイル時のアセンブリも指定する必要がある場合は、`AnyCPU` アセンブリを `/ref/{tfm}` フォルダー内に置きます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-124">These assemblies will only be available at runtime, so if you want to provide the corresponding compile time assembly as well then have `AnyCPU` assembly in `/ref/{tfm}` folder.</span></span> 

<span data-ttu-id="7dd8a-125">NuGet では、コンパイル時またはランタイムのアセットを常に 1 つのフォルダーから選択するため、`/ref` からの互換性のあるアセットが存在する場合は、コンパイル時のアセンブリを追加するために `/lib` が無視されます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-125">Please note, NuGet always picks these compile or runtime assets from one folder so if there are some compatible assets from `/ref` then `/lib` will be ignored to add compile-time assemblies.</span></span> <span data-ttu-id="7dd8a-126">同様に、`/runtimes` からの互換性のあるアセットが存在する場合も、ランタイムのために `/lib` が無視されます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-126">Similarly, if there are some compatible assets from `/runtimes` then also `/lib` will be ignored for runtime.</span></span>

<span data-ttu-id="7dd8a-127">[ マニフェストでこれらのファイルを参照する例については、「](../guides/create-uwp-packages.md)Create UWP Packages`.nuspec`」 (UWP パッケージの作成) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-127">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

<span data-ttu-id="7dd8a-128">また、[NuGet を使用した Windows ストア アプリのコンポーネントのパッケージ化](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)に関するページもご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-128">Also, see [Packing a Windows store app component with NuGet](https://blogs.msdn.microsoft.com/mim/2013/09/02/packaging-a-windows-store-apps-component-with-nuget-part-2)</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="7dd8a-129">プロジェクトでアセンブリ バージョンとターゲット フレームワークを組み合わせる</span><span class="sxs-lookup"><span data-stu-id="7dd8a-129">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="7dd8a-130">複数のアセンブリ バージョンを含むパッケージを NuGet がインストールすると、アセンブリのフレームワーク名とプロジェクトのターゲット フレームワークの照合が試行されます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-130">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="7dd8a-131">一致が見つからない場合、プロジェクトのターゲット フレームワークと同じかそれより下のバージョンの中で最も上のバージョンのアセンブリがコピーされます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-131">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="7dd8a-132">互換性のあるアセンブリが見つからない場合、エラー メッセージが返されます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-132">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="7dd8a-133">たとえば、パッケージに次のフォルダー構造があるとします。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-133">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="7dd8a-134">.NET Framework 4.6 を対象とするプロジェクトにこのパッケージをインストールすると、NuGet は `net45` フォルダーにアセンブリをインストールします。4.6 以下で利用できる最も上のバージョンであるためです。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-134">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="7dd8a-135">一方、プロジェクトが .NET Framework 4.6.1 を対象とする場合、NuGet は `net461` フォルダーにアセンブリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-135">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="7dd8a-136">プロジェクトが .NET Framework 4.0 以前を対象とする場合、NuGet はエラー メッセージを出し、互換性のあるアセンブリが見つからないことを伝えます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-136">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="7dd8a-137">フレームワーク バージョン別にアセンブリをグループ化する</span><span class="sxs-lookup"><span data-stu-id="7dd8a-137">Grouping assemblies by framework version</span></span>

<span data-ttu-id="7dd8a-138">NuGet は、パッケージ内の 1 つだけのライブラリ フォルダーからアセンブリをコピーします。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-138">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="7dd8a-139">たとえば、パッケージに次のフォルダー構造があるとします。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-139">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="7dd8a-140">.NET Framework 4.5 を対象とするプロジェクトにパッケージがインストールされるとき、インストールされる唯一のアセンブリは `MyAssembly.dll` (v2.0) です。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-140">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="7dd8a-141">`MyAssembly.Core.dll` (v1.0) はインストールされません。`net45` フォルダーの一覧にないためです。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-141">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="7dd8a-142">`MyAssembly.Core.dll` が `MyAssembly.dll` のバージョン 2.0 に結合されている可能性があるため、NuGet はこのように動作します。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-142">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="7dd8a-143">.NET Framework 4.5 で `MyAssembly.Core.dll` をインストールする場合、`net45` フォルダーにコピーを置きます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-143">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="7dd8a-144">フレームワーク プロファイル別にアセンブリをグループ化する</span><span class="sxs-lookup"><span data-stu-id="7dd8a-144">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="7dd8a-145">NuGet ではまた、ダッシュとプロファイル名をフォルダーの最後に付けることで特定のフレームワーク プロファイルを対象にすることができます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-145">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="7dd8a-146">サポートされているプロファイルは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-146">The supported profiles are as follows:</span></span>

- <span data-ttu-id="7dd8a-147">`client`: Client Profile</span><span class="sxs-lookup"><span data-stu-id="7dd8a-147">`client`: Client Profile</span></span>
- <span data-ttu-id="7dd8a-148">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="7dd8a-148">`full`: Full Profile</span></span>
- <span data-ttu-id="7dd8a-149">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="7dd8a-149">`wp`: Windows Phone</span></span>
- <span data-ttu-id="7dd8a-150">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="7dd8a-150">`cf`: Compact Framework</span></span>

## <a name="declaring-dependencies-advanced"></a><span data-ttu-id="7dd8a-151">依存関係の宣言 (高度)</span><span class="sxs-lookup"><span data-stu-id="7dd8a-151">Declaring dependencies (Advanced)</span></span>

<span data-ttu-id="7dd8a-152">プロジェクト ファイルをパックするとき、NuGet はそのプロジェクトから依存関係を自動的に生成しようとします。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-152">When packing a project file, NuGet tries to automatically generate the dependencies from the project.</span></span> <span data-ttu-id="7dd8a-153">このセクションに記載されている、 *.nuspec* ファイルを使用した依存関係の宣言に関する情報が必要になるのは、通常は、高度なシナリオだけです。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-153">The information in this section about using a *.nuspec* file to declare dependencies is typically necessary for advanced scenarios only.</span></span>

<span data-ttu-id="7dd8a-154">" *(バージョン 2.0 以降)* " *要素内の* 要素を使って、ターゲット プロジェクトのターゲット フレームワークに対応する `<group>`.nuspec`<dependencies>` でパッケージの依存関係を宣言できます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-154">*(Version 2.0+)* You can declare package dependencies in the *.nuspec* corresponding to the target framework of the target project using `<group>` elements within the `<dependencies>` element.</span></span> <span data-ttu-id="7dd8a-155">詳しくは、[dependencies 要素](../reference/nuspec.md#dependencies-element)に関する記事をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-155">For more information, see [dependencies element](../reference/nuspec.md#dependencies-element).</span></span>

<span data-ttu-id="7dd8a-156">各グループには、`targetFramework` という名前の属性があり、0 個以上の `<dependency>` 要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-156">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="7dd8a-157">ターゲット フレームワークにプロジェクトのフレームワーク プロファイルとの互換性がある場合、これらの依存関係が一緒にインストールされます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-157">Those dependencies are installed together when the target framework is compatible with the project's framework profile.</span></span> <span data-ttu-id="7dd8a-158">正確なフレームワーク識別子については、「[ターゲット フレームワーク](../reference/target-frameworks.md)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-158">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

<span data-ttu-id="7dd8a-159">*lib/* および *ref/* フォルダー内のファイルに対しては、ターゲット フレームワーク モニカー (TFM) ごとに 1 つのグループを使用することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-159">We recommend using one group per Target Framework Moniker (TFM) for files in the *lib/* and *ref/* folders.</span></span>

<span data-ttu-id="7dd8a-160">次の例では、`<group>` 要素のさまざまなバリエーションを示します。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-160">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="7dd8a-161">使用する NuGet ターゲットを決定する</span><span class="sxs-lookup"><span data-stu-id="7dd8a-161">Determining which NuGet target to use</span></span>

<span data-ttu-id="7dd8a-162">ポータブル クラス ライブラリを対象とするライブラリをパッケージ化するとき、フォルダー名と `.nuspec` ファイルで使用する NuGet ターゲットの決定にはこつが要ります。PCL のサブセットのみを対象とする場合は特にそうです。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-162">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="7dd8a-163">次の外部リソースが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-163">The following external resources will help you with this:</span></span>

- <span data-ttu-id="7dd8a-164">[.NET のフレームワーク プロファイル](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span><span class="sxs-lookup"><span data-stu-id="7dd8a-164">[Framework profiles in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephencleary.com)</span></span>
- <span data-ttu-id="7dd8a-165">[ポータブル クラス ライブラリ プロファイル](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL プロファイルとそれと同等の NuGet ターゲットを列挙するテーブル</span><span class="sxs-lookup"><span data-stu-id="7dd8a-165">[Portable Class Library profiles](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="7dd8a-166">[ポータブル クラス ライブラリ プロファイル ツール](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): システムで利用できる PCL プロファイルを決定するためのコマンド ライン ツール</span><span class="sxs-lookup"><span data-stu-id="7dd8a-166">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="7dd8a-167">コンテンツ ファイルと PowerShell スクリプト</span><span class="sxs-lookup"><span data-stu-id="7dd8a-167">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="7dd8a-168">変更可能なコンテンツ ファイルとスクリプト実行は `packages.config` 形式のみで利用できます。これらは、他のすべての形式を使用するときは非推奨とされます。また、新しいパッケージにはこれらを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-168">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="7dd8a-169">`packages.config` では、コンテンツ ファイルと PowerShell スクリプトを、`content` フォルダーと `tools` フォルダー内で同じフォルダー規則を使用し、ターゲット フレームワーク別にグループ化できます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-169">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="7dd8a-170">次に例を示します。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-170">For example:</span></span>

    \content
        \net46
            \MyContent.txt
        \net461
            \MyContent461.txt
        \uap
            \MyUWPContent.html
        \netcore
    \tools
        init.ps1
        \net46
            install.ps1
            uninstall.ps1
        \uap
            install.ps1
            uninstall.ps1

<span data-ttu-id="7dd8a-171">フレームワーク フォルダーを空のまま残す場合、NuGet はアセンブリ参照やコンテンツ ファイルを追加せず、そのフレームワークの PowerShell スクリプトを実行しません。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-171">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="7dd8a-172">`init.ps1` はソリューション レベルで実行され、プロジェクトに依存しないため、`tools` フォルダーの下に直接置く必要があります。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-172">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="7dd8a-173">フレームワーク フォルダーの下に置いた場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="7dd8a-173">It's ignored if placed under a framework folder.</span></span>
