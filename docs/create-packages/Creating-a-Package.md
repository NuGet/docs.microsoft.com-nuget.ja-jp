---
title: NuGet パッケージの作成方法
description: NuGet パッケージを設計し、作成する過程を詳しく説明します。ファイルやバージョン管理など、重要な決定ポイントが含まれます。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 1221631b22eed7d2d8e58bd08ff120d91231d49b
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580398"
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="2e8d8-103">NuGet パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="2e8d8-103">Creating NuGet packages</span></span>

<span data-ttu-id="2e8d8-104">パッケージやそれに含まれるコードに関係なく、`nuget.exe` を使用してその機能をコンポーネントにパッケージ化し、数を問わず他の開発者と共有できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-104">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="2e8d8-105">`nuget.exe` をインストールする方法については、「[Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli)」 (NuGet CLI のインストール) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-105">To install `nuget.exe`, see [Install NuGet CLI](../install-nuget-client-tools.md#nugetexe-cli).</span></span> <span data-ttu-id="2e8d8-106">Visual Studio では、`nuget.exe` が自動的に含まれることはありません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-106">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="2e8d8-107">技術的には、NuGet パッケージは `.nupkg` 拡張子で名前が変更された ZIP ファイルに過ぎません。コンテンツは特定の規則に一致します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-107">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="2e8d8-108">このトピックでは、そのような規則に一致するパッケージの作成過程について説明します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-108">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="2e8d8-109">焦点を絞ったチュートリアルが必要であれば、「[Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md)」 (クイックスタート: パッケージの作成と公開) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-109">For a focused walkthrough, refer to [Quickstart: create and publish a package](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="2e8d8-110">パッケージ化は、コンパイルされたコード (アセンブリ)、シンボル、パッケージとして届けるその他のファイルで始まります (「[Overview and workflow](overview-and-workflow.md)」 (概要とワークフロー) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-110">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](overview-and-workflow.md)).</span></span> <span data-ttu-id="2e8d8-111">このプロセスは、パッケージに入るファイルのコンパイル (またはコンパイル以外の方法による生成) とは関係ありません。ただし、パッケージ ファイルの情報を引き出し、コンパイル済みアセンブリとパッケージの同期を維持することはできます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-111">This process is independent from compiling or otherwise generating the files that go into the package, although you can draw from information in a project file to keep the compiled assemblies and packages in sync.</span></span>

> [!Note]
> <span data-ttu-id="2e8d8-112">このトピックは、Visual Studio 2017 と NuGet 4.0+ を使用する .NET Core プロジェクト以外のプロジェクト タイプに適用されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-112">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="2e8d8-113">.NET Core プロジェクトの場合、NuGet は、プロジェクト ファイルの情報を直接使用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-113">In those .NET Core projects, NuGet uses information in the project file directly.</span></span> <span data-ttu-id="2e8d8-114">詳細については、「[Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md)」 (Visual Studio 2017 で .NET Standard パッケージを作成する) と「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」 (MSBuild ターゲットとしての NuGet pack および restore) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-114">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="2e8d8-115">パッケージ化するアセンブリを決定する</span><span class="sxs-lookup"><span data-stu-id="2e8d8-115">Deciding which assemblies to package</span></span>

<span data-ttu-id="2e8d8-116">ほとんどの汎用パッケージには、他の開発者が自分のプロジェクトで使用できるアセンブリが 1 つまたは複数含まれています。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-116">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="2e8d8-117">一般的に、各アセンブリが他に依存せずに有用であれば、NuGet パッケージあたりアセンブリを 1 つにすることが最善です。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-117">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="2e8d8-118">たとえば、`Utilities.dll` が `Parser.dll` に依存し、`Parser.dll` がそれ自体で有用であれば、それぞれに 1 つパッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-118">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="2e8d8-119">それにより、開発者は `Utilities.dll` に依存せず `Parser.dll` を使用できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-119">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="2e8d8-120">非依存では有用でない複数のアセンブリからライブラリが構成される場合、それらを組み合わせて 1 つのパッケージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-120">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="2e8d8-121">前の例を使えば、`Utilities.dll` でのみ使用されるコードが `Parser.dll` に含まれる場合、同じパッケージで `Parser.dll` を維持できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-121">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>

- <span data-ttu-id="2e8d8-122">同様に、`Utilities.dll` が `Utilities.resources.dll` に依存し、後者がそれ自体で有用ではない場合、両方を同じパッケージに入れます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-122">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="2e8d8-123">リソースは、実際には特殊なケースです。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-123">Resources are, in fact, a special case.</span></span> <span data-ttu-id="2e8d8-124">プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、`.resources.dll` という名前のものは、ローカライズされたサテライト アセンブリであるため*除外*されます (「[ローカライズされたパッケージを作成する](creating-localized-packages.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-124">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="2e8d8-125">そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-125">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="2e8d8-126">ライブラリに COM 相互運用アセンブリが含まれる場合、「[COM 相互運用アセンブリでパッケージを作成する](#authoring-packages-with-com-interop-assemblies)」の追加ガイドラインに従ってください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-126">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="2e8d8-127">.nuspec ファイルのロールと構造</span><span class="sxs-lookup"><span data-stu-id="2e8d8-127">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="2e8d8-128">パッケージ化するファイルがわかったら、次の手順は、`.nuspec` XML ファイルでパッケージ マニフェストを作成することです。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-128">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="2e8d8-129">マニフェスト:</span><span class="sxs-lookup"><span data-stu-id="2e8d8-129">The manifest:</span></span>

1. <span data-ttu-id="2e8d8-130">パッケージの内容を説明し、それ自体、パッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-130">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="2e8d8-131">パッケージの作成を推進し、パッケージをプロジェクトにインストールする方法を NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-131">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="2e8d8-132">たとえば、マニフェストは他の依存関係を特定します。それにより、NuGet はメイン パッケージのインストール時にそのような依存関係もインストールできます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-132">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="2e8d8-133">下の説明のように、必須プロパティと任意プロパティの両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-133">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="2e8d8-134">ここにはない他のプロパティなど、詳しくは、[.nuspec リファレンス](../reference/nuspec.md)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-134">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../reference/nuspec.md).</span></span>

<span data-ttu-id="2e8d8-135">必須プロパティ:</span><span class="sxs-lookup"><span data-stu-id="2e8d8-135">Required properties:</span></span>

- <span data-ttu-id="2e8d8-136">パッケージの識別子。パッケージをホストするギャラリー全体で一意にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-136">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="2e8d8-137">*Major.Minor.Patch[-Suffix]* という形式の特別なバージョン番号。*-Suffix* で[プレリリース版](prerelease-packages.md)を識別します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-137">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](prerelease-packages.md)</span></span>
- <span data-ttu-id="2e8d8-138">ホスト (nuget.org など) に表示されるパッケージ タイトル。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-138">The package title as it should appear on the host (like nuget.org)</span></span>
- <span data-ttu-id="2e8d8-139">作成者と所有者の情報。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-139">Author and owner information.</span></span>
- <span data-ttu-id="2e8d8-140">パッケージの詳しい説明。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-140">A long description of the package.</span></span>

<span data-ttu-id="2e8d8-141">共通の任意プロパティ:</span><span class="sxs-lookup"><span data-stu-id="2e8d8-141">Common optional properties:</span></span>

- <span data-ttu-id="2e8d8-142">リリース ノート</span><span class="sxs-lookup"><span data-stu-id="2e8d8-142">Release notes</span></span>
- <span data-ttu-id="2e8d8-143">著作権情報</span><span class="sxs-lookup"><span data-stu-id="2e8d8-143">Copyright information</span></span>
- <span data-ttu-id="2e8d8-144">[Visual Studio のパッケージ マネージャー UI](../tools/package-manager-ui.md) の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-144">A short description for the [Package Manager UI in Visual Studio](../tools/package-manager-ui.md)</span></span>
- <span data-ttu-id="2e8d8-145">ロケール ID</span><span class="sxs-lookup"><span data-stu-id="2e8d8-145">A locale ID</span></span>
- <span data-ttu-id="2e8d8-146">ホーム ページとライセンス URL</span><span class="sxs-lookup"><span data-stu-id="2e8d8-146">Home page and license URLs</span></span>
- <span data-ttu-id="2e8d8-147">アイコン URL</span><span class="sxs-lookup"><span data-stu-id="2e8d8-147">An icon URL</span></span>
- <span data-ttu-id="2e8d8-148">依存関係と参照の一覧</span><span class="sxs-lookup"><span data-stu-id="2e8d8-148">Lists of dependencies and references</span></span>
- <span data-ttu-id="2e8d8-149">ギャラリー検索で役立つタグ</span><span class="sxs-lookup"><span data-stu-id="2e8d8-149">Tags that assist in gallery searches</span></span>

<span data-ttu-id="2e8d8-150">次は典型的な `.nuspec` ファイルです (ただし、架空のものです)。プロパティを説明するコメントが付いています。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-150">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
        <!-- The identifier that must be unique within the hosting gallery -->
        <id>Contoso.Utility.UsefulStuff</id>

        <!-- The package version number that is used when resolving dependencies -->
        <version>1.8.3-beta</version>

        <!-- Authors contain text that appears directly on the gallery -->
        <authors>Dejana Tesic, Rajeev Dey</authors>

        <!-- 
            Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  
        -->
        <owners>dejanatc, rjdey</owners>

         <!-- License and project URLs provide links for the gallery -->
        <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
        <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

        <!-- The icon is used in Visual Studio's package manager UI -->
        <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

        <!-- 
            If true, this value prompts the user to accept the license when
            installing the package. 
        -->
        <requireLicenseAcceptance>false</requireLicenseAcceptance>

        <!-- Any details about this particular release -->
        <releaseNotes>Bug fixes and performance improvements</releaseNotes>

        <!-- 
            The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. 
        -->
        <description>Core utility functions for web applications</description>

        <!-- Copyright information -->
        <copyright>Copyright ©2016 Contoso Corporation</copyright>

        <!-- Tags appear in the gallery and can be used for tag searches -->
        <tags>web utility http json url parsing</tags>

        <!-- Dependencies are automatically installed when the package is installed -->
        <dependencies>
            <dependency id="Newtonsoft.Json" version="9.0" />
        </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

<span data-ttu-id="2e8d8-151">依存関係の宣言とバージョン番号の指定については、「[パッケージのバージョン管理](../reference/package-versioning.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-151">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="2e8d8-152">パッケージで直接、依存関係からアセットを表面化させることもできます。`dependency` 要素で `include` 属性と `exclude` 属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-152">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="2e8d8-153">[.nuspec リファレンスの依存関係](../reference/nuspec.md#dependencies)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-153">See [.nuspec Reference - Dependencies](../reference/nuspec.md#dependencies).</span></span>

<span data-ttu-id="2e8d8-154">マニフェストはそれから作成されたパッケージに含まれるため、既存のパッケージを調べることで追加の例をいくつも見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-154">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="2e8d8-155">探す場所としては、コンピューターの "*グローバル パッケージ*" フォルダーが適しています。この場所は次のコマンドで返されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-155">A good source is the *global-packages* folder on your computer, the location of which is returned by the following command:</span></span>

```cli
nuget locals -list global-packages
```

<span data-ttu-id="2e8d8-156">*package\version* フォルダーに進み、`.nupkg` ファイルを `.zip` ファイルにコピーし、その `.zip` ファイルを開き、その中の `.nuspec` を調べます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-156">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="2e8d8-157">Visual Studio プロジェクトから `.nuspec` を作成すると、マニフェストに含まれるトークンは、パッケージのビルド時、プロジェクトからの情報で置換されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-157">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="2e8d8-158">「[Visual Studio プロジェクトから .nuspec を作成する](#from-a-visual-studio-project)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-158">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="2e8d8-159">.nuspec ファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="2e8d8-159">Creating the .nuspec file</span></span>

<span data-ttu-id="2e8d8-160">完全なマニフェストの作成は、一般的に、次のいずれかの方法で生成された基本 `.nuspec` ファイルで始まります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-160">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="2e8d8-161">規則ベースの作業ディレクトリ</span><span class="sxs-lookup"><span data-stu-id="2e8d8-161">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="2e8d8-162">アセンブリ DLL</span><span class="sxs-lookup"><span data-stu-id="2e8d8-162">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="2e8d8-163">Visual Studio プロジェクト</span><span class="sxs-lookup"><span data-stu-id="2e8d8-163">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="2e8d8-164">新しいファイルと既定値</span><span class="sxs-lookup"><span data-stu-id="2e8d8-164">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="2e8d8-165">最終パッケージの厳密な内容が説明されるように、ファイルを手作業で編集します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-165">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="2e8d8-166">生成された `.nuspec` ファイルに含まれるプレースホルダーは、`nuget pack` コマンドでパッケージを作成する前に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-166">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="2e8d8-167">`.nuspec` にプレースホルダーが含まれる場合、このコマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-167">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="2e8d8-168">規則ベースの作業ディレクトリから</span><span class="sxs-lookup"><span data-stu-id="2e8d8-168">From a convention-based working directory</span></span>

<span data-ttu-id="2e8d8-169">NuGet パッケージは `.nupkg` 拡張子で名前が変更されている ZIP ファイルに過ぎないため、多くの場合、ローカルのファイル システムに必要なフォルダー構造を作り、その構造から `.nuspec` ファイルを直接作成するのが最も簡単です。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-169">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, it's often easiest to create the folder structure you want on your local file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="2e8d8-170">`nuget pack` コマンドはその後、そのフォルダー構造にすべてのファイルを自動的に追加します。ただし、`.` で始まるフォルダーを除きます。同じ構造にプライベート ファイルを維持できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-170">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you to keep private files in the same structure).</span></span>

<span data-ttu-id="2e8d8-171">この手法の長所は、パッケージに含めるファイルをマニフェストに指定する必要がないことです (このトピックの後半で説明します)。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-171">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="2e8d8-172">パッケージに入るまさにそのフォルダー構造をビルド プロセスで生成させることができます。また、その他の方法ではプロジェクトに含まれないことがある他のファイルを簡単に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-172">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="2e8d8-173">ターゲット プロジェクトに挿入する必要があるコンテンツとソース コード。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-173">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="2e8d8-174">PowerShell スクリプト (NuGet 2.x で使用されるパッケージには、NuGet 3.x 以降ではサポートされていないインストール スクリプトも含めることができます)。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-174">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="2e8d8-175">プロジェクトの既存の構成とソース コード ファイルへの変換。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-175">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="2e8d8-176">フォルダー規則は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-176">The folder conventions are as follows:</span></span>

| <span data-ttu-id="2e8d8-177">フォルダー</span><span class="sxs-lookup"><span data-stu-id="2e8d8-177">Folder</span></span> | <span data-ttu-id="2e8d8-178">説明</span><span class="sxs-lookup"><span data-stu-id="2e8d8-178">Description</span></span> | <span data-ttu-id="2e8d8-179">パッケージ インストール時のアクション</span><span class="sxs-lookup"><span data-stu-id="2e8d8-179">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2e8d8-180">(ルート)</span><span class="sxs-lookup"><span data-stu-id="2e8d8-180">(root)</span></span> | <span data-ttu-id="2e8d8-181">ReadMe.txt の場所</span><span class="sxs-lookup"><span data-stu-id="2e8d8-181">Location for readme.txt</span></span> | <span data-ttu-id="2e8d8-182">Visual Studio では、パッケージのインストール時に ReadMe.txt ファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-182">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="2e8d8-183">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="2e8d8-183">lib/{tfm}</span></span> | <span data-ttu-id="2e8d8-184">指定されたターゲット フレームワーク モニカー (TFM) のアセンブリ (`.dll`)、ドキュメント (`.xml`)、シンボル (`.pdb`)</span><span class="sxs-lookup"><span data-stu-id="2e8d8-184">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="2e8d8-185">アセンブリはランタイムに加えてコンパイル時にも参照として追加されます。`.xml` と `.pdb` はプロジェクト フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-185">Assemblies are added as references for compile as well as runtime; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="2e8d8-186">フレームワーク ターゲット固有のサブフォルダーを作成するには、「[複数のターゲット フレームワークのサポート](supporting-multiple-target-frameworks.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-186">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="2e8d8-187">ref/{tfm}</span><span class="sxs-lookup"><span data-stu-id="2e8d8-187">ref/{tfm}</span></span> | <span data-ttu-id="2e8d8-188">指定したターゲット フレームワーク モニカー (TFM) のアセンブリ (`.dll`) およびシンボル (`.pdb`) ファイル</span><span class="sxs-lookup"><span data-stu-id="2e8d8-188">Assembly (`.dll`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="2e8d8-189">アセンブリはコンパイル時にのみ参照として追加されます。したがって、プロジェクトの bin フォルダーには何もコピーされません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-189">Assemblies are added as references only for compile time; So nothing will be copied into project bin folder.</span></span> |
| <span data-ttu-id="2e8d8-190">runtimes</span><span class="sxs-lookup"><span data-stu-id="2e8d8-190">runtimes</span></span> | <span data-ttu-id="2e8d8-191">アーキテクチャ固有のアセンブリ (`.dll`)、シンボル (`.pdb`)、ネイティブ リソース (`.pri`) ファイル</span><span class="sxs-lookup"><span data-stu-id="2e8d8-191">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="2e8d8-192">アセンブリはランタイムでのみ参照として追加されます。その他のファイルはプロジェクト フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-192">Assemblies are added as references only for runtime; other files are copied into project folders.</span></span> <span data-ttu-id="2e8d8-193">対応するコンパイル時のアセンブリを指定するために、対応する (TFM) `AnyCPU` 固有のアセンブリが常に `/ref/{tfm}` フォルダーの下にあります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-193">There should always be a corresponding (TFM) `AnyCPU` specific assembly under `/ref/{tfm}` folder to provide corresponding compile time assembly.</span></span> <span data-ttu-id="2e8d8-194">「[複数のターゲット フレームワークのサポート](supporting-multiple-target-frameworks.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-194">See [Supporting multiple target frameworks](supporting-multiple-target-frameworks.md).</span></span> |
| <span data-ttu-id="2e8d8-195">コンテンツ</span><span class="sxs-lookup"><span data-stu-id="2e8d8-195">content</span></span> | <span data-ttu-id="2e8d8-196">任意のファイル</span><span class="sxs-lookup"><span data-stu-id="2e8d8-196">Arbitrary files</span></span> | <span data-ttu-id="2e8d8-197">コンテンツはプロジェクト ルートにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-197">Contents are copied to the project root.</span></span> <span data-ttu-id="2e8d8-198">**コンテンツ** フォルダーは最終的にパッケージを使用するターゲット アプリケーションのルートであると考えてください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-198">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="2e8d8-199">パッケージでアプリケーションの */images* フォルダーに画像が追加されるようにするには、パッケージの *content/images* フォルダーにそれを置きます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-199">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="2e8d8-200">ビルド</span><span class="sxs-lookup"><span data-stu-id="2e8d8-200">build</span></span> | <span data-ttu-id="2e8d8-201">MSBuild の `.targets` ファイルと `.props` ファイル</span><span class="sxs-lookup"><span data-stu-id="2e8d8-201">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="2e8d8-202">プロジェクト ファイルまたは `project.lock.json` (NuGet 3.x 以降) に自動的に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-202">Automatically inserted into the project file or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="2e8d8-203">ツール</span><span class="sxs-lookup"><span data-stu-id="2e8d8-203">tools</span></span> | <span data-ttu-id="2e8d8-204">Powershell のスクリプトとプログラムにはパッケージ マネージャー コンソールからアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-204">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="2e8d8-205">`tools` フォルダーはパッケージ マネージャー コンソールだけの `PATH` 環境変数に追加されます (厳密に言うと、プロジェクトのビルド時に MSBuild に設定される `PATH` にでは*ありません*)。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-205">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="2e8d8-206">フォルダー構造には、任意の数のターゲット フレームワークに対して任意の数のアセンブリを含めることができるため、複数のフレームワークをサポートするパッケージの作成時、この方法は必須となります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-206">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks.</span></span>

<span data-ttu-id="2e8d8-207">いずれの場合でも、必要なフォルダー構造を配置したら、そのフォルダーで次のコマンドを実行し、`.nuspec` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-207">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```cli
nuget spec
```

<span data-ttu-id="2e8d8-208">繰り返しになりますが、生成された `.nuspec` には、フォルダー構造のファイルに対する明示的な参照が含まれません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-208">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="2e8d8-209">NuGet は、パッケージが作成されるとき、すべてのファイルを自動的に含めます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-209">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="2e8d8-210">ただし、マニフェストのその他の部分でプレースホルダー値を編集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-210">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="2e8d8-211">アセンブリ DLL から</span><span class="sxs-lookup"><span data-stu-id="2e8d8-211">From an assembly DLL</span></span>

<span data-ttu-id="2e8d8-212">単純にアセンブリからパッケージを作成する場合、次のコマンドを使用し、アセンブリでメタデータから `.nuspec` ファイルを生成できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-212">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```cli
nuget spec <assembly-name>.dll
```

<span data-ttu-id="2e8d8-213">このフォームを使用すると、マニフェストのいくつかのプレースホルダーがアセンブリからの具体的な値で置換されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-213">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="2e8d8-214">たとえば、`<id>` プロパティはアセンブリ名に設定され、`<version>` はアセンブリ バージョンに設定されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-214">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="2e8d8-215">しかしながら、マニフェストの他のプロパティには、アセンブリのそれに該当する値が与えられず、引き続きプレースホルダーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-215">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="2e8d8-216">Visual Studio プロジェクトから</span><span class="sxs-lookup"><span data-stu-id="2e8d8-216">From a Visual Studio project</span></span>

<span data-ttu-id="2e8d8-217">`.csproj` または `.vbproj` ファイルから `.nuspec` を作成する方法が便利です。これらのプロジェクトにインストールされているその他のパッケージが依存関係として自動的に参照されるためです。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-217">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="2e8d8-218">プロジェクト ファイルと同じフォルダーで次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-218">Simply use the following command in the same folder as the project file:</span></span>

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="2e8d8-219">結果的に生成される `<project-name>.nuspec` ファイルには、パッケージ化のときにプロジェクトからの値で置換される*トークン*が含まれます。他のパッケージが既にインストールされている場合、その参照が含まれます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-219">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="2e8d8-220">トークンは、プロジェクト プロパティの両側で `$` 記号によって区切られます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-220">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="2e8d8-221">たとえば、この方法で生成されるマニフェストの `<id>` 値は通常、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-221">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="2e8d8-222">このトークンは、パッケージ化のとき、プロジェクト ファイルからの `AssemblyName` 値で置換されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-222">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="2e8d8-223">プロジェクト値と `.nuspec` トークンのマッピングについては、[置換トークンの参照に関するトピック](../reference/nuspec.md#replacement-tokens)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-223">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../reference/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="2e8d8-224">トークンを利用することで、プロジェクトを更新するとき、`.nuspec` のバージョン番号などの重要な値を自分で更新する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-224">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="2e8d8-225">(必要であれば、トークンはいつでもリテラル値に変更できます。)</span><span class="sxs-lookup"><span data-stu-id="2e8d8-225">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="2e8d8-226">この後の「[nuget パックを実行し、.nupkg ファイルを生成する](#running-nuget-pack-to-generate-the-nupkg-file)」で説明するように、Visual Studio プロジェクトから作業するとき、いくつかの追加パッケージ化オプションを利用できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-226">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="2e8d8-227">ソリューションレベル パッケージ</span><span class="sxs-lookup"><span data-stu-id="2e8d8-227">Solution-level packages</span></span>

<span data-ttu-id="2e8d8-228">*NuGet 2.x のみ。NuGet 3.0+ では利用できません。*</span><span class="sxs-lookup"><span data-stu-id="2e8d8-228">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="2e8d8-229">NuGet 2.x では、パッケージ マネージャー コンソールのツールまたは追加コマンドをインストールするソリューションレベル パッケージの概念がサポートされました (`tools` フォルダーのコンテンツ)。しかしながら、参照、コンテンツ、またはソリューションのプロジェクトに対するビルド カスタマイズは追加されません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-229">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="2e8d8-230">このようなパッケージのその直接の `lib`、`content`、`build` フォルダーにはファイルは含まれておらず、その依存関係の `lib`、`content`、`build` フォルダーにもファイルは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-230">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span>

<span data-ttu-id="2e8d8-231">NuGet は、プロジェクトの `packages.config` ファイルではなく、`.nuget` フォルダーの `packages.config` ファイルで、インストールされたソリューションレベル パッケージを追跡記録します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-231">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="2e8d8-232">新しいファイルと既定値</span><span class="sxs-lookup"><span data-stu-id="2e8d8-232">New file with default values</span></span>

<span data-ttu-id="2e8d8-233">次のコマンドでは、プレースホルダーを含む既定のマニフェストが作成されます。それにより、適切なファイル構造で始められます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-233">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```cli
nuget spec [<package-name>]
```

<span data-ttu-id="2e8d8-234">\<package-name\> を省略した場合、結果的に生成されるファイルは `Package.nuspec` になります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-234">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="2e8d8-235">`Contoso.Utility.UsefulStuff` のような名前を指定すると、ファイルは `Contoso.Utility.UsefulStuff.nuspec` になります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-235">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="2e8d8-236">結果的に生成される `.nuspec` には、`projectUrl` のような値のプレースホルダーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-236">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="2e8d8-237">必ずファイルを編集してからそれを利用し、最終的な `.nupkg` ファイルを作成してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-237">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="2e8d8-238">一意のパッケージ識別子を選択し、バージョン番号を設定する</span><span class="sxs-lookup"><span data-stu-id="2e8d8-238">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="2e8d8-239">パッケージ識別子 (`<id>` 要素) とバージョン番号 (`<version>` 要素) は、パッケージに含まれるコードを一意に識別するため、マニフェストの中で最も重要な値です。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-239">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="2e8d8-240">**パッケージ識別子のベスト プラクティス:**</span><span class="sxs-lookup"><span data-stu-id="2e8d8-240">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="2e8d8-241">**一意性**: この識別子は、nuget.org 全体で、あるいはパッケージをホストするギャラリー全体で一意になる必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-241">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="2e8d8-242">識別子を決める前に、該当するギャラリーを検索し、その名前が既に使用されていないか確認してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-242">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="2e8d8-243">競合を避けるために、`Contoso.` のように、識別子の最初の部分に会社の名前を使用することが適しているパターンです。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-243">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="2e8d8-244">**名前空間のような名前**: .NET の名前空間に似たパターンに従います。ハイフンの代わりにドット表記を使います。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-244">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="2e8d8-245">たとえば、`Contoso-Utility-UsefulStuff` や `Contoso_Utility_UsefulStuff` ではなく `Contoso.Utility.UsefulStuff` を使用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-245">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="2e8d8-246">パッケージ識別子がコードで使用される名前空間と一致すれば、利用者にとっても便利です。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-246">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="2e8d8-247">**サンプル パッケージ**: 別のパッケージの使用方法を示すサンプル コードのパッケージを生成する場合、`Contoso.Utility.UsefulStuff.Sample` のように、識別子のサフィックスとして `.Sample` を付けます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-247">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="2e8d8-248">(サンプル パッケージは、もちろん、他のパッケージに依存します。)サンプル パッケージを作成するとき、前述のように、規則ベースの作業ディレクトリを使用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-248">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="2e8d8-249">`content` フォルダーで、`\Samples\Contoso.Utility.UsefulStuff.Sample` のように、`\Samples\<identifier>` という名前のフォルダーにサンプル コードを配置します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-249">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="2e8d8-250">**パッケージ バージョンのベスト プラクティス:**</span><span class="sxs-lookup"><span data-stu-id="2e8d8-250">**Best practices for the package version:**</span></span>

- <span data-ttu-id="2e8d8-251">必須ではありませんが、一般的に、ライブラリに合わせてパッケージの番号を設定します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-251">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="2e8d8-252">これはパッケージを 1 つのアセンブリに限定すれば簡単なことです。「[パッケージ化するアセンブリを決定する](#deciding-which-assemblies-to-package)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-252">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="2e8d8-253">概して、NuGet 自体は依存関係の解決時、パッケージ バージョンを使います。アセンブリ バージョンではありません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-253">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="2e8d8-254">非標準のバージョン スキーマを使用するとき、「[パッケージのバージョン管理](../reference/package-versioning.md)」で説明するように、NuGet バージョン管理ルールを検討してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-254">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="2e8d8-255">バージョン管理の理解には、次の一連のブログ投稿が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-255">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - <span data-ttu-id="2e8d8-256">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (パート 1: DLL 地獄)</span><span class="sxs-lookup"><span data-stu-id="2e8d8-256">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="2e8d8-257">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (パート 2: コア アルゴリズム)</span><span class="sxs-lookup"><span data-stu-id="2e8d8-257">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="2e8d8-258">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (パート 3: バインド リダイレクトによる統合)</span><span class="sxs-lookup"><span data-stu-id="2e8d8-258">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="setting-a-package-type"></a><span data-ttu-id="2e8d8-259">パッケージの種類の設定</span><span class="sxs-lookup"><span data-stu-id="2e8d8-259">Setting a package type</span></span>

<span data-ttu-id="2e8d8-260">NuGet 3.5+ では、パッケージに特定の*パッケージの種類*の印を付け、その用途を示すことができます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-260">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="2e8d8-261">種類の印が付いていないパッケージ (初期のバージョンの NuGet で作成されたすべてのパッケージが相当) は種類が `Dependency` に初期設定されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-261">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="2e8d8-262">種類が `Dependency` のパッケージでは、ビルド時または実行時アセットがライブラリとアプリケーションに追加されます。(互換性があれば) あらゆる種類のプロジェクトにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-262">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="2e8d8-263">種類が `DotnetCliTool` のパッケージは [.NET CLI](/dotnet/articles/core/tools/index) の拡張であり、コマンド ラインから呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-263">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="2e8d8-264">このようなパッケージは .NET Core プロジェクトにのみインストールできます。復元操作には影響を与えません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-264">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="2e8d8-265">このようなプロジェクト別の拡張機能に関する詳細は、[.NET Core 拡張性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)ドキュメントにあります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-265">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="2e8d8-266">カスタム タイプのパッケージでは、パッケージ ID と同じ形式ルールに準拠する任意の種類識別子が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-266">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="2e8d8-267">ただし、`Dependency` と `DotnetCliTool` 以外の種類は、Visual Studio の NuGet パッケージ マネージャーには認識されません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-267">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="2e8d8-268">パッケージの種類は `.nuspec` ファイルで設定されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-268">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="2e8d8-269">下位互換性を維持するには、種類 `Dependency` を明示的に設定*しない*で、NuGet に依存するのが最適な方法です。NuGet は、種類が指定されない場合、この種類を想定します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-269">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="2e8d8-270">`.nuspec`: `<metadata>` 要素の下の `packageTypes\packageType` ノード内のパッケージの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-270">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="2e8d8-271">ReadMe とその他のファイルの追加</span><span class="sxs-lookup"><span data-stu-id="2e8d8-271">Adding a readme and other files</span></span>

<span data-ttu-id="2e8d8-272">パッケージに含めるファイルを直接指定するには、`.nuspec` ファイルの `<files>` ノードを使用します。このノードは `<metadata>` タグの*後に入ります*。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-272">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
        <!-- Add a readme -->
        <file src="readme.txt" target="" />

        <!-- Add files from an arbitrary folder that's not necessarily in the project -->
        <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> <span data-ttu-id="2e8d8-273">規則ベースの作業ディレクトリ手法を利用するとき、ReadMe.txt をパッケージ ルートに、`content` フォルダーにその他のコンテンツを配置できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-273">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="2e8d8-274">マニフェストで必須の `<file>` 要素はありません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-274">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="2e8d8-275">パッケージ ルートに `readme.txt` という名前のファイルを含めると、Visual Studio では、パッケージを直接インストールした直後、そのファイルの内容がプレーンテキストとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-275">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="2e8d8-276">(パッケージが依存関係としてインストールされた場合、ReadMe ファイルは表示されません。)</span><span class="sxs-lookup"><span data-stu-id="2e8d8-276">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="2e8d8-277">たとえば、HtmlAgilityPack パッケージの ReadMe は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-277">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![インストール時の NuGet パッケージの ReadMe ファイルの表示](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="2e8d8-279">`.nuspec` ファイルに空の `<files>` ノードを含める場合、NuGet では、`lib` フォルダーの内容以外の内容はパッケージに入りません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-279">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="2e8d8-280">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="2e8d8-280">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="2e8d8-281">ビルド時のカスタム ツールまたはプロセスの実行など、場合によっては、パッケージを使用するプロジェクト内のカスタム ビルド ターゲットまたはプロパティを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-281">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="2e8d8-282">これは、プロジェクトの `\build` フォルダー内に形式 `<package_id>.targets` または `<package_id>.props` で (`Contoso.Utility.UsefulStuff.targets` のように) ファイルを配置することで行います。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-282">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="2e8d8-283">ルート `\build` フォルダーのファイルは、すべてのターゲット フレームワークで適切であると見なされます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-283">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="2e8d8-284">ファイルをフレームワーク固有にするには、次のように、まず、適切なサブフォルダーにそのファイルを配置します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-284">To provide framework-specific files, first place them within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="2e8d8-285">次に `.nuspec` ファイルで、`<files>` ノードのそれらのファイルを参照するようにします。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-285">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
        <!-- Include everything in \build -->
        <file src="build\**" target="build" />

        <!-- Other files -->
        <!-- ... -->
    </files>
</package>
```

<span data-ttu-id="2e8d8-286">[NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files) で、パッケージに MSBuild のプロパティとターゲットを含めることができるようになりました。そのため、`metadata` 要素に `minClientVersion="2.5"` 属性を追加して、パッケージを使用するために必要な最小限の NuGet クライアント バージョンを示すことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-286">Including MSBuild props and targets in a package was [introduced with NuGet 2.5](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files), therefore it is recommended to add the `minClientVersion="2.5"` attribute to the `metadata` element, to indicate the minimum NuGet client version required to consume the package.</span></span>

<span data-ttu-id="2e8d8-287">NuGet で `\build` ファイルを使用してパッケージをインストールすると、`.targets` ファイルと `.props` ファイルを指す MSBuild `<Import>` 要素がプロジェクト ファイルに追加されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-287">When NuGet installs a package with `\build` files, it adds MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="2e8d8-288">(`.props` はプロジェクト ファイルの一番上に、`.targets` は一番下に追加されます。)別個の条件付き MSBuild `<Import>` 要素が、各ターゲット フレームワークに追加されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-288">(`.props` is added at the top of the project file; `.targets` is added at the bottom.) A separate conditional MSBuild `<Import>` element is added for each target framework.</span></span>

<span data-ttu-id="2e8d8-289">相互フレームワーク ターゲットの MSBuild `.props` および `.targets` ファイルは、`\buildCrossTargeting` フォルダーに配置できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-289">MSBuild `.props` and `.targets` files for cross-framework targeting can be placed in the `\buildCrossTargeting` folder.</span></span> <span data-ttu-id="2e8d8-290">パッケージ インストール時に、NuGet は対応する `<Import>` 要素を条件付きのプロジェクト ファイルに追加します。その際、ターゲット フレームワークは設定されません (MSBuild プロパティ `$(TargetFramework)` は必ず空になっています)。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-290">During package installation, NuGet adds the corresponding `<Import>` elements to the project file with the condition, that the target framework is not set (the MSBuild property `$(TargetFramework)` must be empty).</span></span>

<span data-ttu-id="2e8d8-291">NuGet 3.x を使用する場合、ターゲットはプロジェクトに追加されませんが、`project.lock.json` を通じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-291">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="2e8d8-292">COM 相互運用アセンブリを含むパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="2e8d8-292">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="2e8d8-293">COM 相互運用アセンブリを含むパッケージには、PackageReference 形式を利用して正しい `EmbedInteropTypes` メタデータがプロジェクトに追加されるように、適切な [targets ファイル](#including-msbuild-props-and-targets-in-a-package)が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-293">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="2e8d8-294">既定では、PackageReference が使用されるとき、`EmbedInteropTypes` メタデータは常にすべてのアセンブリに対して false になります。それにより、targets ファイルでこのメタデータが明示的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-294">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="2e8d8-295">競合を回避するために、ターゲット名を一意にする必要があります。理想的には、パッケージ名と組み込むアセンブリの組み合わせを使用します。下の例の `{InteropAssemblyName}` をその値で置換します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-295">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="2e8d8-296">(例については、[NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) もご覧ください。)</span><span class="sxs-lookup"><span data-stu-id="2e8d8-296">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="2e8d8-297">`packages.config` 管理形式を利用するとき、パッケージからアセンブリの参照を追加すると、NuGet と Visual Studio は COM 相互運用アセンブリがないか調べ、プロジェクト ファイルで `EmbedInteropTypes` を true に設定します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-297">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="2e8d8-298">この場合、ターゲットがオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-298">In this case the targets are overriden.</span></span>

<span data-ttu-id="2e8d8-299">また、既定では、[ビルド アセットの推移的なフローはありません](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-299">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="2e8d8-300">ここで説明したように作成したパッケージの動作は、プロジェクトからプロジェクト参照に推移的依存関係として引き出されたときとは異なります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-300">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="2e8d8-301">パッケージの利用者は、ビルドを含めないように PrivateAssets の既定値を変更することでそれをフローさせることができます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-301">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="2e8d8-302">nuget パックを実行し、.nupkg ファイルを生成する</span><span class="sxs-lookup"><span data-stu-id="2e8d8-302">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="2e8d8-303">アセンブリまたは規則ベースの作業ディレクトリを使用するとき、自分の `.nuspec` ファイルで `nuget pack` を実行してパッケージを作成します。`<project-name>` を特定のファイル名で置換します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-303">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<project-name>` with your specific filename:</span></span>

```cli
nuget pack <project-name>.nuspec
```

<span data-ttu-id="2e8d8-304">Visual Studio プロジェクトを使用するとき、自分のプロジェクト ファイルで `nuget pack` を実行します。それにより、プロジェクトの `.nuspec` ファイルが自動的に読み込まれ、その中にトークンがあれば、プロジェクト ファイルの値を利用して置換されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-304">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="2e8d8-305">トークンを置換するには、プロジェクト ファイルを直接使用する必要があります。プロジェクトがトークン値のソースであるからです。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-305">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="2e8d8-306">`.nuspec` ファイルで `nuget pack` を使用する場合、トークンは置換されません。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-306">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="2e8d8-307">いずれの場合も、`nuget pack` では、`.git` や `.hg` のようなピリオドで始まるフォルダーは除外されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-307">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="2e8d8-308">NuGet では、修正が必要なエラーが `.nuspec` ファイルで見つかった場合、それが示されます。マニフェストのプレースホルダー値を変更し忘れたなどです。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-308">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="2e8d8-309">`nuget pack` が成功すると、`.nupkg` ファイルが生成されます。「[パッケージの公開](../create-packages/publish-a-package.md)」に説明があるように、このファイルを適切なギャラリーに公開できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-309">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="2e8d8-310">作成後のパッケージを調べる便利な方法は、[パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ツールでそれを開くことです。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-310">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="2e8d8-311">パッケージの内容とそのマニフェストがグラフィック表示されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-311">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="2e8d8-312">生成された `.nupkg` ファイルの名前を `.zip` ファイルに変更し、その内容を直接調べることもできます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-312">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="2e8d8-313">追加オプション</span><span class="sxs-lookup"><span data-stu-id="2e8d8-313">Additional options</span></span>

<span data-ttu-id="2e8d8-314">`nuget pack` ではさまざまなコマンドライン スイッチを使用できます。ファイルを除外したり、マニフェストのバージョン番号をオーバーライドしたり、出力フォルダーを変更したりできます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-314">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="2e8d8-315">完全な一覧は、[pack コマンドに関するページ](../tools/cli-ref-pack.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-315">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="2e8d8-316">Visual Studio プロジェクトの共通オプションには以下のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-316">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="2e8d8-317">**参照されるプロジェクト**: プロジェクトが他のプロジェクトを参照する場合、参照されるプロジェクトをパッケージの一部あるいは依存関係として追加できます。`-IncludeReferencedProjects` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-317">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="2e8d8-318">この包含プロセスは再帰的です。`MyProject.csproj` が B と C を参照し、それらのプロジェクトが D、E、F を参照する場合、B、C、D、E、F からのファイルがパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-318">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="2e8d8-319">参照されるプロジェクトにそれ自体の `.nuspec` ファイルが含まれる場合、NuGet では、その参照されるプロジェクトが依存関係として追加されます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-319">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="2e8d8-320">そのプロジェクトを個別にパッケージ化し、公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-320">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="2e8d8-321">**ビルド構成**: 既定では、NuGet では、プロジェクト ファイルに設定されている既定のビルド構成が使用されます。一般的には、*デバッグ*です。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-321">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="2e8d8-322">*リリース*など、別のビルド構成からファイルをパッケージ化するには、構成と共に `-properties` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-322">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="2e8d8-323">**シンボル**: 利用者がデバッガーでパッケージ コードをステップ実行することを可能にするシンボルを含めるには、`-Symbols` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-323">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="2e8d8-324">パッケージ インストールのテスト</span><span class="sxs-lookup"><span data-stu-id="2e8d8-324">Testing package installation</span></span>

<span data-ttu-id="2e8d8-325">パッケージを公開する前に、通常、パッケージをプロジェクトにインストールするプロセスをテストします。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-325">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="2e8d8-326">このテストにより、必要なファイルがすべて、プロジェクト内の適切な場所に入ります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-326">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="2e8d8-327">インストールは Visual Studio またはコマンド ラインで手動テストできます。通常の[パッケージ インストール手順](../consume-packages/ways-to-install-a-package.md)を利用します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-327">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../consume-packages/ways-to-install-a-package.md).</span></span>

<span data-ttu-id="2e8d8-328">自動テストの基本プロセスは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-328">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="2e8d8-329">`.nupkg` ファイルをローカル フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-329">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="2e8d8-330">`nuget sources add -name <name> -source <path>` コマンドを利用し、パッケージ ソースにフォルダーを追加します ([nuget ソース](../tools/cli-ref-sources.md)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-330">Add the folder to your package sources using the `nuget sources add -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="2e8d8-331">指定されたコンピューターのいずれかで、このローカル ソースを 1 回設定します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-331">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="2e8d8-332">`nuget install <packageID> -source <name>` を利用し、そのソースからパッケージをインストールします。`<name>` は、`nuget sources` に指定されたソースの名前に一致します。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-332">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="2e8d8-333">ソースを指定することで、そのソースだけからパッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-333">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="2e8d8-334">ファイル システムで、ファイルが正しくインストールされていることを調べます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-334">Examine your file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2e8d8-335">次の手順</span><span class="sxs-lookup"><span data-stu-id="2e8d8-335">Next Steps</span></span>

<span data-ttu-id="2e8d8-336">`.nupkg` ファイルとなるパッケージを作成したら、「[パッケージの公開](../create-packages/publish-a-package.md)」の説明にあるように、選択したギャラリーにパッケージを公開できます。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-336">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="2e8d8-337">パッケージの機能を拡張したり、次のトピックで説明するように、その他の方法で他のシナリオをサポートしたりすると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-337">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="2e8d8-338">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="2e8d8-338">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="2e8d8-339">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="2e8d8-339">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2e8d8-340">ソース ファイルと構成ファイルの変換</span><span class="sxs-lookup"><span data-stu-id="2e8d8-340">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="2e8d8-341">ローカリゼーション</span><span class="sxs-lookup"><span data-stu-id="2e8d8-341">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="2e8d8-342">プレリリース バージョン</span><span class="sxs-lookup"><span data-stu-id="2e8d8-342">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="2e8d8-343">最後になりますが、次のような種類のパッケージもあります。</span><span class="sxs-lookup"><span data-stu-id="2e8d8-343">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="2e8d8-344">ネイティブ パッケージ</span><span class="sxs-lookup"><span data-stu-id="2e8d8-344">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="2e8d8-345">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="2e8d8-345">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
