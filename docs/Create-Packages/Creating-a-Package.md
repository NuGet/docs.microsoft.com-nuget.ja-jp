---
title: "NuGet パッケージの作成方法 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 456797cb-e3e4-4b88-9b01-8b5153cee802
description: "NuGet パッケージを設計し、作成する過程を詳しく説明します。ファイルやバージョン管理など、重要な決定ポイントが含まれます。"
keywords: "NuGet パッケージ作成, パッケージの作成, nuspec マニフェスト, NuGet パッケージ規則, NuGet パッケージ バージョン"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6675d21a2900a1b61e17c08518b328732f4472c5
ms.sourcegitcommit: 1cb047b24b3b69d80e808c23b2ace0d98d2dfdcc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/08/2018
---
# <a name="creating-nuget-packages"></a><span data-ttu-id="94d72-104">NuGet パッケージの作成</span><span class="sxs-lookup"><span data-stu-id="94d72-104">Creating NuGet packages</span></span>

<span data-ttu-id="94d72-105">パッケージやそれに含まれるコードに関係なく、`nuget.exe` を使用してその機能をコンポーネントにパッケージ化し、数を問わず他の開発者と共有できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-105">No matter what your package does or what code it contains, you use `nuget.exe` to package that functionality into a component that can be shared with and used by any number of other developers.</span></span> <span data-ttu-id="94d72-106">`nuget.exe` をインストールする方法については、「[Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli)」 (NuGet CLI のインストール) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-106">To install `nuget.exe`, see [Install NuGet CLI](../guides/Install-NuGet.md#nuget-cli).</span></span> <span data-ttu-id="94d72-107">Visual Studio では、`nuget.exe` が自動的に含まれることはありません。</span><span class="sxs-lookup"><span data-stu-id="94d72-107">Note that Visual Studio does not automatically include `nuget.exe`.</span></span>

<span data-ttu-id="94d72-108">技術的には、NuGet パッケージは `.nupkg` 拡張子で名前が変更された ZIP ファイルに過ぎません。コンテンツは特定の規則に一致します。</span><span class="sxs-lookup"><span data-stu-id="94d72-108">Technically speaking, a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension and whose contents match certain conventions.</span></span> <span data-ttu-id="94d72-109">このトピックでは、そのような規則に一致するパッケージの作成過程について説明します。</span><span class="sxs-lookup"><span data-stu-id="94d72-109">This topic describes the detailed process of creating a package that meets those conventions.</span></span> <span data-ttu-id="94d72-110">焦点を絞ったチュートリアルが必要であれば、「[Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md)」 (パッケージの作成と公開のクイックスタート) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-110">For a focused walkthrough, refer to [Create and Publish a Package Quickstart](../quickstart/create-and-publish-a-package.md).</span></span>

<span data-ttu-id="94d72-111">パッケージ化は、コンパイルされたコード (アセンブリ)、シンボル、パッケージとして届けるその他のファイルで始まります (「[Overview and workflow](Overview-and-Workflow.md)」 (概要とワークフロー) を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="94d72-111">Packaging begins with the compiled code (assemblies), symbols, and/or other files that you want to deliver as a package (see [Overview and workflow](Overview-and-Workflow.md)).</span></span> <span data-ttu-id="94d72-112">このプロセスは、パッケージに入るファイルのコンパイル (あるいはコンパイル以外の生成) とは関係ありません。パッケージ ファイルの情報を引き出し、コンパイルしたアセンブリとパッケージの同期を維持することはできます。</span><span class="sxs-lookup"><span data-stu-id="94d72-112">This process is independent from compiling or otherwise generating the files that go into the package, although you can use draw from information in a project file to keep the compiled assemblines and packages in sync.</span></span>

<span data-ttu-id="94d72-113">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="94d72-113">In this topic:</span></span>

- [<span data-ttu-id="94d72-114">パッケージ化するアセンブリを決定する</span><span class="sxs-lookup"><span data-stu-id="94d72-114">Deciding which assemblies to package</span></span>](#deciding-which-assemblies-to-package)
- [<span data-ttu-id="94d72-115">`.nuspec` ファイルのロールと構造</span><span class="sxs-lookup"><span data-stu-id="94d72-115">The role and structure of the `.nuspec` file</span></span>](#the-role-and-structure-of-the-nuspec-file)
- <span data-ttu-id="94d72-116">次から [`.nuspec` ファイルを作成する](#creating-the-nuspec-file):</span><span class="sxs-lookup"><span data-stu-id="94d72-116">[Creating the `.nuspec` file](#creating-the-nuspec-file) from:</span></span>
    - [<span data-ttu-id="94d72-117">規則ベースの作業ディレクトリ</span><span class="sxs-lookup"><span data-stu-id="94d72-117">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
    - [<span data-ttu-id="94d72-118">アセンブリ DLL</span><span class="sxs-lookup"><span data-stu-id="94d72-118">An assembly DLL</span></span>](#from-an-assembly-dll)
    - [<span data-ttu-id="94d72-119">Visual Studio プロジェクト</span><span class="sxs-lookup"><span data-stu-id="94d72-119">A Visual Studio project</span></span>](#from-a-visual-studio-project)
    - [<span data-ttu-id="94d72-120">新しいファイルと既定値</span><span class="sxs-lookup"><span data-stu-id="94d72-120">New file with default values</span></span>](#new-file-with-default-values)    
- [<span data-ttu-id="94d72-121">一意のパッケージ識別子を選択し、バージョン番号を設定する</span><span class="sxs-lookup"><span data-stu-id="94d72-121">Choosing a unique package identifier and setting the version number</span></span>](#choosing-a-unique-package-identifier-and-setting-the-version-number)
- <span data-ttu-id="94d72-122">[パッケージの種類を設定する](#setting-a-package-type) (NuGet 3.5 以降)</span><span class="sxs-lookup"><span data-stu-id="94d72-122">[Setting a package type](#setting-a-package-type) (NuGet 3.5 and later)</span></span>
- [<span data-ttu-id="94d72-123">ReadMe とその他のファイルの追加</span><span class="sxs-lookup"><span data-stu-id="94d72-123">Adding a readme and other files</span></span>](#adding-a-readme-and-other-files)
- [<span data-ttu-id="94d72-124">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="94d72-124">Including MSBuild props and targets in a package</span></span>](#including-msbuild-props-and-targets-in-a-package)
- [<span data-ttu-id="94d72-125">COM 相互運用アセンブリを含むパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="94d72-125">Authoring packages that contain COM interop assemblies</span></span>](#authoring-packages-with-com-interop-assemblies)
- [<span data-ttu-id="94d72-126">nuget パックを実行し、.nupkg ファイルを生成する</span><span class="sxs-lookup"><span data-stu-id="94d72-126">Running nuget pack to generate the .nupkg file</span></span>](#running-nuget-pack-to-generate-the-nupkg-file)

<span data-ttu-id="94d72-127">以上の中心的手順を終えたら、本書で説明するように、他のさまざまな機能を組み込むことができます。</span><span class="sxs-lookup"><span data-stu-id="94d72-127">After these core steps, you can incorporate a variety of other features as described elsewhere in this documentation.</span></span> <span data-ttu-id="94d72-128">下の「[次の手順](#next-steps)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="94d72-128">See [Next steps](#next-steps) below.</span></span>

> [!Note]
> <span data-ttu-id="94d72-129">このトピックは、Visual Studio 2017 と NuGet 4.0+ を使用する .NET Core プロジェクト以外のプロジェクト タイプに適用されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-129">This topic applies to project types other than .NET Core projects using Visual Studio 2017 and NuGet 4.0+.</span></span> <span data-ttu-id="94d72-130">NuGet 4.0+ を使用する .NET Core プロジェクトの場合、NuGet は `.csproj` ファイルの情報を直接使用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-130">In those .NET Core projects, NuGet uses information in the `.csproj` file directly.</span></span> <span data-ttu-id="94d72-131">詳細については、「[Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md)」 (Visual Studio 2017 で .NET Standard パッケージを作成する) と「[NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md)」 (MSBuild ターゲットとしての NuGet pack および restore) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-131">For details, see [Create .NET Standard Packages with Visual Studio 2017](../guides/create-net-standard-packages-vs2017.md) and [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="deciding-which-assemblies-to-package"></a><span data-ttu-id="94d72-132">パッケージ化するアセンブリを決定する</span><span class="sxs-lookup"><span data-stu-id="94d72-132">Deciding which assemblies to package</span></span>

<span data-ttu-id="94d72-133">ほとんどの汎用パッケージには、他の開発者が自分のプロジェクトで使用できるアセンブリが 1 つまたは複数含まれています。</span><span class="sxs-lookup"><span data-stu-id="94d72-133">Most general-purpose packages contain one or more assemblies that other developers can use in their own projects.</span></span>

- <span data-ttu-id="94d72-134">一般的に、各アセンブリが他に依存せずに有用であれば、NuGet パッケージあたりアセンブリを 1 つにすることが最善です。</span><span class="sxs-lookup"><span data-stu-id="94d72-134">In general, it's best to have one assembly per NuGet package, provided that each assembly is independently useful.</span></span> <span data-ttu-id="94d72-135">たとえば、`Utilities.dll` が `Parser.dll` に依存し、`Parser.dll` がそれ自体で有用であれば、それぞれに 1 つパッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="94d72-135">For example, if you have a `Utilities.dll` that depends on `Parser.dll`, and `Parser.dll` is useful on its own, then create one package for each.</span></span> <span data-ttu-id="94d72-136">それにより、開発者は `Utilities.dll` に依存せず `Parser.dll` を使用できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-136">Doing so allows developers to use `Parser.dll` independently of `Utilities.dll`.</span></span>

- <span data-ttu-id="94d72-137">非依存では有用でない複数のアセンブリからライブラリが構成される場合、それらを組み合わせて 1 つのパッケージを作成できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-137">If your library is composed of multiple assemblies that aren't independently useful, then it's fine to combine them into one package.</span></span> <span data-ttu-id="94d72-138">前の例を使えば、`Utilities.dll` でのみ使用されるコードが `Parser.dll` に含まれる場合、同じパッケージで `Parser.dll` を維持できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-138">Using the previous example, if `Parser.dll` contains code that's used only by `Utilities.dll`, then it's fine to keep `Parser.dll` in the same package.</span></span>
    - <span data-ttu-id="94d72-139">同様に、`Utilities.dll` が `Utilities.resources.dll` に依存し、後者がそれ自体で有用ではない場合、両方を同じパッケージに入れます。</span><span class="sxs-lookup"><span data-stu-id="94d72-139">Similarly, if `Utilities.dll` depends on `Utilities.resources.dll`, where again the latter is not useful on its own, then put both in the same package.</span></span>

<span data-ttu-id="94d72-140">リソースは、実際には特殊なケースです。</span><span class="sxs-lookup"><span data-stu-id="94d72-140">Resources are, in fact, a special case.</span></span> <span data-ttu-id="94d72-141">プロジェクトにパッケージをインストールするとき、NuGet はパッケージの DLL にアセンブリ参照を自動的に追加します。ただし、`.resources.dll` という名前のものは、ローカライズされたサテライト アセンブリであるため*除外*されます (「[ローカライズされたパッケージを作成する](creating-localized-packages.md)」を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="94d72-141">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies (see [Creating localized packages](creating-localized-packages.md)).</span></span> <span data-ttu-id="94d72-142">そのため、避けなければ不可欠なパッケージ コードが含まれてしまうファイルには `.resources.dll` を使わないようにします。</span><span class="sxs-lookup"><span data-stu-id="94d72-142">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="94d72-143">ライブラリに COM 相互運用アセンブリが含まれる場合、「[COM 相互運用アセンブリでパッケージを作成する](#authoring-packages-with-com-interop-assemblies)」の追加ガイドラインに従ってください。</span><span class="sxs-lookup"><span data-stu-id="94d72-143">If your library contains COM interop assemblies, follow additional the guidelines in [Authoring packages with COM interop assemblies](#authoring-packages-with-com-interop-assemblies).</span></span>

## <a name="the-role-and-structure-of-the-nuspec-file"></a><span data-ttu-id="94d72-144">.nuspec ファイルのロールと構造</span><span class="sxs-lookup"><span data-stu-id="94d72-144">The role and structure of the .nuspec file</span></span>

<span data-ttu-id="94d72-145">パッケージ化するファイルがわかったら、次の手順は、`.nuspec` XML ファイルでパッケージ マニフェストを作成することです。</span><span class="sxs-lookup"><span data-stu-id="94d72-145">Once you know what files you want to package, the next step is creating a package manifest in a `.nuspec` XML file.</span></span>

<span data-ttu-id="94d72-146">マニフェスト:</span><span class="sxs-lookup"><span data-stu-id="94d72-146">The manifest:</span></span>

1. <span data-ttu-id="94d72-147">パッケージの内容を説明し、それ自体、パッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="94d72-147">Describes the package's contents and is itself included in the package.</span></span>
1. <span data-ttu-id="94d72-148">パッケージの作成を推進し、パッケージをプロジェクトにインストールする方法を NuGet に指示します。</span><span class="sxs-lookup"><span data-stu-id="94d72-148">Drives both the creation of the package and instructs NuGet on how to install the package into a project.</span></span> <span data-ttu-id="94d72-149">たとえば、マニフェストは他の依存関係を特定します。それにより、NuGet はメイン パッケージのインストール時にそのような依存関係もインストールできます。</span><span class="sxs-lookup"><span data-stu-id="94d72-149">For example, the manifest identifies other package dependencies such that NuGet can also install those dependencies when the main package is installed.</span></span>
1. <span data-ttu-id="94d72-150">下の説明のように、必須プロパティと任意プロパティの両方が含まれます。</span><span class="sxs-lookup"><span data-stu-id="94d72-150">Contains both required and optional properties as described below.</span></span> <span data-ttu-id="94d72-151">ここにはない他のプロパティなど、詳しくは、[.nuspec リファレンス](../schema/nuspec.md)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="94d72-151">For exact details, including other properties not mentioned here, see  the [.nuspec reference](../schema/nuspec.md).</span></span>

<span data-ttu-id="94d72-152">必須プロパティ:</span><span class="sxs-lookup"><span data-stu-id="94d72-152">Required properties:</span></span>

- <span data-ttu-id="94d72-153">パッケージの識別子。パッケージをホストするギャラリー全体で一意にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="94d72-153">The package identifier, which must be unique across the gallery that hosts the package.</span></span>
- <span data-ttu-id="94d72-154">*Major.Minor.Patch[-Suffix]* という形式の特別なバージョン番号。*-Suffix* で[プレリリース版](Prerelease-Packages.md)を識別します。</span><span class="sxs-lookup"><span data-stu-id="94d72-154">A specific version number in the form *Major.Minor.Patch[-Suffix]* where *-Suffix* identifies [pre-release versions](Prerelease-Packages.md)</span></span>
- <span data-ttu-id="94d72-155">ホスト (nuget.org など) に表示されるパッケージ タイトル。</span><span class="sxs-lookup"><span data-stu-id="94d72-155">The package title as it should appears on the host (like nuget.org)</span></span>
- <span data-ttu-id="94d72-156">作成者と所有者の情報。</span><span class="sxs-lookup"><span data-stu-id="94d72-156">Author and owner information.</span></span>
- <span data-ttu-id="94d72-157">パッケージの詳しい説明。</span><span class="sxs-lookup"><span data-stu-id="94d72-157">A long description of the package.</span></span>

<span data-ttu-id="94d72-158">共通の任意プロパティ:</span><span class="sxs-lookup"><span data-stu-id="94d72-158">Common optional properties:</span></span>

- <span data-ttu-id="94d72-159">リリース ノート</span><span class="sxs-lookup"><span data-stu-id="94d72-159">Release notes</span></span>
- <span data-ttu-id="94d72-160">著作権情報</span><span class="sxs-lookup"><span data-stu-id="94d72-160">Copyright information</span></span>
- <span data-ttu-id="94d72-161">[Visual Studio のパッケージ マネージャー UI](../Tools/Package-Manager-UI.md) の簡単な説明。</span><span class="sxs-lookup"><span data-stu-id="94d72-161">A short description for the [Package Manager UI in Visual Studio](../Tools/Package-Manager-UI.md)</span></span>
- <span data-ttu-id="94d72-162">ロケール ID</span><span class="sxs-lookup"><span data-stu-id="94d72-162">A locale ID</span></span>
- <span data-ttu-id="94d72-163">ホーム ページとライセンス URL</span><span class="sxs-lookup"><span data-stu-id="94d72-163">Home page and license URLs</span></span>
- <span data-ttu-id="94d72-164">アイコン URL</span><span class="sxs-lookup"><span data-stu-id="94d72-164">An icon URL</span></span>
- <span data-ttu-id="94d72-165">依存関係と参照の一覧</span><span class="sxs-lookup"><span data-stu-id="94d72-165">Lists of dependencies and references</span></span>
- <span data-ttu-id="94d72-166">ギャラリー検索で役立つタグ</span><span class="sxs-lookup"><span data-stu-id="94d72-166">Tags that assist in gallery searches</span></span>

<span data-ttu-id="94d72-167">次は典型的な `.nuspec` ファイルです (ただし、架空のものです)。プロパティを説明するコメントが付いています。</span><span class="sxs-lookup"><span data-stu-id="94d72-167">The following is a typical (but fictitious) `.nuspec` file, with comments describing the properties:</span></span>

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

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
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

<span data-ttu-id="94d72-168">依存関係の宣言とバージョン番号の指定については、「[パッケージのバージョン管理](../reference/package-versioning.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-168">For details on declaring dependencies and specifying version numbers, see [Package versioning](../reference/package-versioning.md).</span></span> <span data-ttu-id="94d72-169">パッケージで直接、依存関係からアセットを表面化させることもできます。`dependency` 要素で `include` 属性と `exclude` 属性を使用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-169">It is also possible to surface assets from dependencies directly in the package by using the `include` and `exclude` attributes on the `dependency` element.</span></span> <span data-ttu-id="94d72-170">[.nuspec リファレンスの依存関係](../Schema/nuspec.md#dependencies)をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="94d72-170">See [.nuspec Reference - Dependencies](../Schema/nuspec.md#dependencies).</span></span>

<span data-ttu-id="94d72-171">マニフェストはそれから作成されたパッケージに含まれるため、既存のパッケージを調べることで追加の例をいくつも見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="94d72-171">Because the manifest is included in the package created from it, you can find any number of additional examples by examining existing packages.</span></span> <span data-ttu-id="94d72-172">探す場所としては、コンピューターのグローバル パッケージ キャッシュが適しています。この場所は次のコマンドで返されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-172">A good source is the global package cache on your machine, the location of which is returned by the following command:</span></span>

```
nuget locals -list global-packages
```

<span data-ttu-id="94d72-173">*package\version* フォルダーに進み、`.nupkg` ファイルを `.zip` ファイルにコピーし、その `.zip` ファイルを開き、その中の `.nuspec` を調べます。</span><span class="sxs-lookup"><span data-stu-id="94d72-173">Go into any *package\version* folder, copy the `.nupkg` file to a `.zip` file, then open that `.zip` file and examine the `.nuspec` within it.</span></span>

> [!Note]
> <span data-ttu-id="94d72-174">Visual Studio プロジェクトから `.nuspec` を作成すると、マニフェストに含まれるトークンは、パッケージのビルド時、プロジェクトからの情報で置換されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-174">When creating a `.nuspec` from a Visual Studio project, the manifest contains tokens that are replaced with information from the project when the package is built.</span></span> <span data-ttu-id="94d72-175">「[Visual Studio プロジェクトから .nuspec を作成する](#from-a-visual-studio-project)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-175">See [Creating the .nuspec from a Visual Studio project](#from-a-visual-studio-project).</span></span>

## <a name="creating-the-nuspec-file"></a><span data-ttu-id="94d72-176">.nuspec ファイルを作成する</span><span class="sxs-lookup"><span data-stu-id="94d72-176">Creating the .nuspec file</span></span>

<span data-ttu-id="94d72-177">完全なマニフェストの作成は、一般的に、次のいずれかの方法で生成された基本 `.nuspec` ファイルで始まります。</span><span class="sxs-lookup"><span data-stu-id="94d72-177">Creating a complete manifest typically begins with a basic `.nuspec` file generated through one of the following methods:</span></span>

- [<span data-ttu-id="94d72-178">規則ベースの作業ディレクトリ</span><span class="sxs-lookup"><span data-stu-id="94d72-178">A convention-based working directory</span></span>](#from-a-convention-based-working-directory)
- [<span data-ttu-id="94d72-179">アセンブリ DLL</span><span class="sxs-lookup"><span data-stu-id="94d72-179">An assembly DLL</span></span>](#from-an-assembly-dll)
- [<span data-ttu-id="94d72-180">Visual Studio プロジェクト</span><span class="sxs-lookup"><span data-stu-id="94d72-180">A Visual Studio project</span></span>](#from-a-visual-studio-project)    
- [<span data-ttu-id="94d72-181">新しいファイルと既定値</span><span class="sxs-lookup"><span data-stu-id="94d72-181">New file with default values</span></span>](#new-file-with-default-values)

<span data-ttu-id="94d72-182">最終パッケージの厳密な内容が説明されるように、ファイルを手作業で編集します。</span><span class="sxs-lookup"><span data-stu-id="94d72-182">You then edit the file by hand so that it describes the exact content you want in the final package.</span></span>

> [!Important]
> <span data-ttu-id="94d72-183">生成された `.nuspec` ファイルに含まれるプレースホルダーは、`nuget pack` コマンドでパッケージを作成する前に変更する必要があります。</span><span class="sxs-lookup"><span data-stu-id="94d72-183">Generated `.nuspec` files contain placeholders that must be modified before creating the package with the `nuget pack` command.</span></span> <span data-ttu-id="94d72-184">`.nuspec` にプレースホルダーが含まれる場合、このコマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="94d72-184">That command fails if the `.nuspec` contains any placeholders.</span></span>

### <a name="from-a-convention-based-working-directory"></a><span data-ttu-id="94d72-185">規則ベースの作業ディレクトリから</span><span class="sxs-lookup"><span data-stu-id="94d72-185">From a convention-based working directory</span></span>

<span data-ttu-id="94d72-186">NuGet パッケージは `.nupkg` 拡張子で名前が変更されている ZIP ファイルに過ぎないため、多くの場合、ファイル システムで必要なフォルダー構造を作り、その構造から `.nuspec` ファイルを直接作成するのが最も簡単です。</span><span class="sxs-lookup"><span data-stu-id="94d72-186">Because a NuGet package is just a ZIP file that's been renamed with the `.nupkg` extension, its often easiest to create the folder structure you want on the file system, then create the `.nuspec` file directly from that structure.</span></span> <span data-ttu-id="94d72-187">`nuget pack` コマンドはその後、そのフォルダー構造にすべてのファイルを自動的に追加します。ただし、`.` で始まるフォルダーを除きます。同じ構造にプライベート ファイルを維持できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-187">The `nuget pack` command then automatically adds all files in that folder structure (excluding any folders that begin with `.`, allowing you keep private files in the same structure).</span></span>

<span data-ttu-id="94d72-188">この手法の長所は、パッケージに含めるファイルをマニフェストに指定する必要がないことです (このトピックの後半で説明します)。</span><span class="sxs-lookup"><span data-stu-id="94d72-188">The advantage to this approach is that you don't need to specify in the manifest which files you want to include in the package (as explained later in this topic).</span></span> <span data-ttu-id="94d72-189">パッケージに入るまさにそのフォルダー構造をビルド プロセスで生成させることができます。また、その他の方法ではプロジェクトに含まれないことがある他のファイルを簡単に含めることができます。</span><span class="sxs-lookup"><span data-stu-id="94d72-189">You can simply have your build process produce the exact folder structure that goes into the package, and you can easily include other files that might not be part of a project otherwise:</span></span>

- <span data-ttu-id="94d72-190">ターゲット プロジェクトに挿入する必要があるコンテンツとソース コード。</span><span class="sxs-lookup"><span data-stu-id="94d72-190">Content and source code that should be injected into the target project.</span></span>
- <span data-ttu-id="94d72-191">PowerShell スクリプト (NuGet 2.x で使用されるパッケージには、NuGet 3.x 以降ではサポートされていないインストール スクリプトも含めることができます)。</span><span class="sxs-lookup"><span data-stu-id="94d72-191">PowerShell scripts (packages used in NuGet 2.x can include installation scripts as well, which is not supported in NuGet 3.x and later).</span></span>
- <span data-ttu-id="94d72-192">プロジェクトの既存の構成とソース コード ファイルへの変換。</span><span class="sxs-lookup"><span data-stu-id="94d72-192">Transformations to existing configuration and source code files in a project.</span></span>

<span data-ttu-id="94d72-193">フォルダー規則は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="94d72-193">The folder conventions are as follows:</span></span>

| <span data-ttu-id="94d72-194">フォルダー</span><span class="sxs-lookup"><span data-stu-id="94d72-194">Folder</span></span> | <span data-ttu-id="94d72-195">説明</span><span class="sxs-lookup"><span data-stu-id="94d72-195">Description</span></span> | <span data-ttu-id="94d72-196">パッケージ インストール時のアクション</span><span class="sxs-lookup"><span data-stu-id="94d72-196">Action upon package install</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94d72-197">(ルート)</span><span class="sxs-lookup"><span data-stu-id="94d72-197">(root)</span></span> | <span data-ttu-id="94d72-198">ReadMe.txt の場所</span><span class="sxs-lookup"><span data-stu-id="94d72-198">Location for readme.txt</span></span> | <span data-ttu-id="94d72-199">Visual Studio では、パッケージのインストール時に ReadMe.txt ファイルが表示されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-199">Visual Studio displays a readme.txt file in the package root when the package is installed.</span></span> |
| <span data-ttu-id="94d72-200">lib/{tfm}</span><span class="sxs-lookup"><span data-stu-id="94d72-200">lib/{tfm}</span></span> | <span data-ttu-id="94d72-201">指定されたターゲット フレームワーク モニカー (TFM) のアセンブリ (`.dll`)、ドキュメント (`.xml`)、シンボル (`.pdb`)</span><span class="sxs-lookup"><span data-stu-id="94d72-201">Assembly (`.dll`), documentation (`.xml`), and symbol (`.pdb`) files for the given Target Framework Moniker (TFM)</span></span> | <span data-ttu-id="94d72-202">アセンブリは参照として追加されます。`.xml` と `.pdb` はプロジェクト フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="94d72-202">Assemblies are added as references; `.xml` and `.pdb` copied into project folders.</span></span> <span data-ttu-id="94d72-203">フレームワーク ターゲット固有のサブフォルダーを作成するには、「[複数のターゲット フレームワークのサポート](Supporting-Multiple-Target-Frameworks.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-203">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md) for creating framework target-specific sub-folders.</span></span> |
| <span data-ttu-id="94d72-204">runtimes</span><span class="sxs-lookup"><span data-stu-id="94d72-204">runtimes</span></span> | <span data-ttu-id="94d72-205">アーキテクチャ固有のアセンブリ (`.dll`)、シンボル (`.pdb`)、ネイティブ リソース (`.pri`) ファイル</span><span class="sxs-lookup"><span data-stu-id="94d72-205">Architecture-specific assembly (`.dll`), symbol (`.pdb`), and native resource (`.pri`) files</span></span> | <span data-ttu-id="94d72-206">アセンブリは参照として追加されます。その他のファイルはプロジェクト フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="94d72-206">Assemblies are added as references; other files are copied into project folders.</span></span> <span data-ttu-id="94d72-207">「[複数のターゲット フレームワークのサポート](Supporting-Multiple-Target-Frameworks.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-207">See [Supporting multiple target frameworks](Supporting-Multiple-Target-Frameworks.md).</span></span> |
| <span data-ttu-id="94d72-208">コンテンツ</span><span class="sxs-lookup"><span data-stu-id="94d72-208">content</span></span> | <span data-ttu-id="94d72-209">任意のファイル</span><span class="sxs-lookup"><span data-stu-id="94d72-209">Arbitrary files</span></span> | <span data-ttu-id="94d72-210">コンテンツはプロジェクト ルートにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="94d72-210">Contents are copied to the project root.</span></span> <span data-ttu-id="94d72-211">**コンテンツ** フォルダーは最終的にパッケージを使用するターゲット アプリケーションのルートであると考えてください。</span><span class="sxs-lookup"><span data-stu-id="94d72-211">Think of the **content** folder as the root of the target application that ultimately consumes the package.</span></span> <span data-ttu-id="94d72-212">パッケージでアプリケーションの */images* フォルダーに画像が追加されるようにするには、パッケージの *content/images* フォルダーにそれを置きます。</span><span class="sxs-lookup"><span data-stu-id="94d72-212">To have the package add an image in the application's */images* folder, place it in the package's *content/images* folder.</span></span> |
| <span data-ttu-id="94d72-213">ビルド</span><span class="sxs-lookup"><span data-stu-id="94d72-213">build</span></span> | <span data-ttu-id="94d72-214">MSBuild の `.targets` ファイルと `.props` ファイル</span><span class="sxs-lookup"><span data-stu-id="94d72-214">MSBuild `.targets` and `.props` files</span></span> | <span data-ttu-id="94d72-215">プロジェクト ファイルの (NuGet 2.x) または `project.lock.json` (NuGet 3.x+) に自動的に挿入されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-215">Automatically inserted into the project file (NuGet 2.x) or `project.lock.json` (NuGet 3.x+).</span></span> |
| <span data-ttu-id="94d72-216">ツール</span><span class="sxs-lookup"><span data-stu-id="94d72-216">tools</span></span> | <span data-ttu-id="94d72-217">Powershell のスクリプトとプログラムにはパッケージ マネージャー コンソールからアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="94d72-217">Powershell scripts and programs accessible from the Package Manager Console</span></span> | <span data-ttu-id="94d72-218">`tools` フォルダーはパッケージ マネージャー コンソールだけの `PATH` 環境変数に追加されます (厳密に言うと、プロジェクトのビルド時に MSBuild に設定される `PATH` にでは*ありません*)。</span><span class="sxs-lookup"><span data-stu-id="94d72-218">The `tools` folder is added to the `PATH` environment variable for the Package Manager Console only (Specifically, *not* to the `PATH` as set for MSBuild when building the project).</span></span> |

<span data-ttu-id="94d72-219">フォルダー構造には、任意の数のターゲット フレームワークに対して任意の数のアセンブリを含めることができるため、複数のフレームワークをサポートするパッケージの作成時、この方法は必須となります。</span><span class="sxs-lookup"><span data-stu-id="94d72-219">Because your folder structure can contain any number of assemblies for any number of target frameworks, this method is necessary when creating packages that support multiple frameworks</span></span> 

<span data-ttu-id="94d72-220">いずれの場合でも、必要なフォルダー構造を配置したら、そのフォルダーで次のコマンドを実行し、`.nuspec` ファイルを作成します。</span><span class="sxs-lookup"><span data-stu-id="94d72-220">In any case, once you have the desired folder structure in place, run the following command in that folder to create the `.nuspec` file:</span></span>

```
nuget spec
```

<span data-ttu-id="94d72-221">繰り返しになりますが、生成された `.nuspec` には、フォルダー構造のファイルに対する明示的な参照が含まれません。</span><span class="sxs-lookup"><span data-stu-id="94d72-221">Again, the generated `.nuspec` contains no explicit references to files in the folder structure.</span></span> <span data-ttu-id="94d72-222">NuGet は、パッケージが作成されるとき、すべてのファイルを自動的に含めます。</span><span class="sxs-lookup"><span data-stu-id="94d72-222">NuGet automatically includes all files when the package is created.</span></span> <span data-ttu-id="94d72-223">ただし、マニフェストのその他の部分でプレースホルダー値を編集する必要があります。</span><span class="sxs-lookup"><span data-stu-id="94d72-223">You still need to edit placeholder values in other parts of the manifest, however.</span></span>

### <a name="from-an-assembly-dll"></a><span data-ttu-id="94d72-224">アセンブリ DLL から</span><span class="sxs-lookup"><span data-stu-id="94d72-224">From an assembly DLL</span></span>

<span data-ttu-id="94d72-225">単純にアセンブリからパッケージを作成する場合、次のコマンドを使用し、アセンブリでメタデータから `.nuspec` ファイルを生成できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-225">In the simple case of creating a package from an assembly, you can generate a `.nuspec` file from the metadata in the assembly using the following command:</span></span>

```
nuget spec <assembly-name>.dll
```

<span data-ttu-id="94d72-226">このフォームを使用すると、マニフェストのいくつかのプレースホルダーがアセンブリからの具体的な値で置換されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-226">Using this form replaces a few placeholders in the manifest with specific values from the assembly.</span></span> <span data-ttu-id="94d72-227">たとえば、`<id>` プロパティはアセンブリ名に設定され、`<version>` はアセンブリ バージョンに設定されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-227">For example, the `<id>` property is set to the assembly name, and `<version>` is set to the assembly version.</span></span> <span data-ttu-id="94d72-228">しかしながら、マニフェストの他のプロパティには、アセンブリのそれに該当する値が与えられず、引き続きプレースホルダーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="94d72-228">Other properties in the manifest, however, don't have matching values in the assembly and thus still contain placeholders.</span></span>

### <a name="from-a-visual-studio-project"></a><span data-ttu-id="94d72-229">Visual Studio プロジェクトから</span><span class="sxs-lookup"><span data-stu-id="94d72-229">From a Visual Studio project</span></span>

<span data-ttu-id="94d72-230">`.csproj` または `.vbproj` ファイルから `.nuspec` を作成する方法が便利です。これらのプロジェクトにインストールされているその他のパッケージが依存関係として自動的に参照されるためです。</span><span class="sxs-lookup"><span data-stu-id="94d72-230">Creating a `.nuspec` from a `.csproj` or `.vbproj` file is convenient because other packages that have been installed into those project are automatically referenced as dependencies.</span></span> <span data-ttu-id="94d72-231">プロジェクト ファイルと同じフォルダーで次のコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-231">Simply use the following command in the same folder as the project file:</span></span>

```
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

<span data-ttu-id="94d72-232">結果的に生成される `<project-name>.nuspec` ファイルには、パッケージ化のときにプロジェクトからの値で置換される*トークン*が含まれます。他のパッケージが既にインストールされている場合、その参照が含まれます。</span><span class="sxs-lookup"><span data-stu-id="94d72-232">The resulting `<project-name>.nuspec` file contains *tokens* that are replaced at packaging time with values from the project, including references to any other packages that have already been installed.</span></span>

<span data-ttu-id="94d72-233">トークンは、プロジェクト プロパティの両側で `$` 記号によって区切られます。</span><span class="sxs-lookup"><span data-stu-id="94d72-233">A token is delimited by `$` symbols on both sides of the project property.</span></span> <span data-ttu-id="94d72-234">たとえば、この方法で生成されるマニフェストの `<id>` 値は通常、次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-234">For example, the `<id>` value in a manifest generated in this way typically appears as follows:</span></span>

```xml
<id>$id$</id>
```

<span data-ttu-id="94d72-235">このトークンは、パッケージ化のとき、プロジェクト ファイルからの `AssemblyName` 値で置換されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-235">This token is replaced with the `AssemblyName` value from the project file at packing time.</span></span> <span data-ttu-id="94d72-236">プロジェクト値と `.nuspec` トークンのマッピングについては、[置換トークンの参照に関するトピック](../schema/nuspec.md#replacement-tokens)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-236">For the exact mapping of project values to `.nuspec` tokens, see the [Replacement Tokens reference](../schema/nuspec.md#replacement-tokens).</span></span>

<span data-ttu-id="94d72-237">トークンを利用することで、プロジェクトを更新するとき、`.nuspec` のバージョン番号などの重要な値を自分で更新する必要がなくなります。</span><span class="sxs-lookup"><span data-stu-id="94d72-237">Tokens relieve you from needing to update crucial values like the version number in the `.nuspec` as you update the project.</span></span> <span data-ttu-id="94d72-238">(必要であれば、トークンはいつでもリテラル値に変更できます。)</span><span class="sxs-lookup"><span data-stu-id="94d72-238">(You can always replace the tokens with literal values, if desired).</span></span> 

<span data-ttu-id="94d72-239">この後の「[nuget パックを実行し、.nupkg ファイルを生成する](#running-nuget-pack-to-generate-the-nupkg-file)」で説明するように、Visual Studio プロジェクトから作業するとき、いくつかの追加パッケージ化オプションを利用できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-239">Note that there are several additional packaging options available when working from a Visual Studio project, as described in [Running nuget pack to generate the .nupkg file](#running-nuget-pack-to-generate-the-nupkg-file) later on.</span></span>

#### <a name="solution-level-packages"></a><span data-ttu-id="94d72-240">ソリューションレベル パッケージ</span><span class="sxs-lookup"><span data-stu-id="94d72-240">Solution-level packages</span></span>

<span data-ttu-id="94d72-241">*NuGet 2.x のみ。NuGet 3.0+ では利用できません。*</span><span class="sxs-lookup"><span data-stu-id="94d72-241">*NuGet 2.x only. Not available in NuGet 3.0+.*</span></span>

<span data-ttu-id="94d72-242">NuGet 2.x では、パッケージ マネージャー コンソールのツールまたは追加コマンドをインストールするソリューションレベル パッケージの概念がサポートされました (`tools` フォルダーのコンテンツ)。しかしながら、参照、コンテンツ、またはソリューションのプロジェクトに対するビルド カスタマイズは追加されません。</span><span class="sxs-lookup"><span data-stu-id="94d72-242">NuGet 2.x supported the notion of a solution-level package that installs tools or additional commands for the Package Manager Console (the contents of the `tools` folder), but does not add references, content, or build customizations to any projects in the solution.</span></span> <span data-ttu-id="94d72-243">このようなパッケージのその直接の `lib`、`content`、`build` フォルダーにはファイルは含まれておらず、その依存関係の `lib`、`content`、`build` フォルダーにもファイルは含まれていません。</span><span class="sxs-lookup"><span data-stu-id="94d72-243">Such packages contain no files in its direct `lib`, `content`, or `build` folders, and none of its dependencies have files in their respective `lib`, `content`, or `build` folders.</span></span> 

<span data-ttu-id="94d72-244">NuGet は、プロジェクトの `packages.config` ファイルではなく、`.nuget` フォルダーの `packages.config` ファイルで、インストールされたソリューションレベル パッケージを追跡記録します。</span><span class="sxs-lookup"><span data-stu-id="94d72-244">NuGet tracks installed solution-level packages in a `packages.config` file in the `.nuget` folder, rather than the project's `packages.config` file.</span></span>

### <a name="new-file-with-default-values"></a><span data-ttu-id="94d72-245">新しいファイルと既定値</span><span class="sxs-lookup"><span data-stu-id="94d72-245">New file with default values</span></span>

<span data-ttu-id="94d72-246">次のコマンドでは、プレースホルダーを含む既定のマニフェストが作成されます。それにより、適切なファイル構造で始められます。</span><span class="sxs-lookup"><span data-stu-id="94d72-246">The following command creates a default manifest with placeholders, which ensures you start with the proper file structure:</span></span>

```
nuget spec [<package-name>]
```

<span data-ttu-id="94d72-247">\<package-name\> を省略した場合、結果的に生成されるファイルは `Package.nuspec` になります。</span><span class="sxs-lookup"><span data-stu-id="94d72-247">If you omit \<package-name\>, the resulting file is `Package.nuspec`.</span></span> <span data-ttu-id="94d72-248">`Contoso.Utility.UsefulStuff` のような名前を指定すると、ファイルは `Contoso.Utility.UsefulStuff.nuspec` になります。</span><span class="sxs-lookup"><span data-stu-id="94d72-248">If you provide a name such as `Contoso.Utility.UsefulStuff`, the file is `Contoso.Utility.UsefulStuff.nuspec`.</span></span>

<span data-ttu-id="94d72-249">結果的に生成される `.nuspec` には、`projectUrl` のような値のプレースホルダーが含まれます。</span><span class="sxs-lookup"><span data-stu-id="94d72-249">The resulting `.nuspec` contains placeholders for values like the `projectUrl`.</span></span> <span data-ttu-id="94d72-250">必ずファイルを編集してからそれを利用し、最終的な `.nupkg` ファイルを作成してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-250">Be sure to edit the file before using it to create the final `.nupkg` file.</span></span>

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a><span data-ttu-id="94d72-251">一意のパッケージ識別子を選択し、バージョン番号を設定する</span><span class="sxs-lookup"><span data-stu-id="94d72-251">Choosing a unique package identifier and setting the version number</span></span>

<span data-ttu-id="94d72-252">パッケージ識別子 (`<id>` 要素) とバージョン番号 (`<version>` 要素) は、パッケージに含まれるコードを一意に識別するため、マニフェストの中で最も重要な値です。</span><span class="sxs-lookup"><span data-stu-id="94d72-252">The package identifier (`<id>` element) and the version number (`<version>` element) are the two most important values in the manifest because they uniquely identify the exact code that's contained in the package.</span></span>

<span data-ttu-id="94d72-253">**パッケージ識別子のベスト プラクティス:**</span><span class="sxs-lookup"><span data-stu-id="94d72-253">**Best practices for the package identifier:**</span></span>

- <span data-ttu-id="94d72-254">**一意性**: この識別子は、nuget.org 全体で、あるいはパッケージをホストするギャラリー全体で一意になる必要があります。</span><span class="sxs-lookup"><span data-stu-id="94d72-254">**Uniqueness**: The identifier must be unique across nuget.org or whatever gallery hosts the package.</span></span> <span data-ttu-id="94d72-255">識別子を決める前に、該当するギャラリーを検索し、その名前が既に使用されていないか確認してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-255">Before deciding on an identifier, search the applicable gallery to check if the name is already in use.</span></span> <span data-ttu-id="94d72-256">競合を避けるために、`Contoso.` のように、識別子の最初の部分に会社の名前を使用することが適しているパターンです。</span><span class="sxs-lookup"><span data-stu-id="94d72-256">To avoid conflicts, a good pattern is to use your company name as the first part of the identifier, such as `Contoso.`.</span></span>
- <span data-ttu-id="94d72-257">**名前空間のような名前**: .NET の名前空間に似たパターンに従います。ハイフンの代わりにドット表記を使います。</span><span class="sxs-lookup"><span data-stu-id="94d72-257">**Namespace-like names**: Follow a pattern similar to namespaces in .NET, using dot notation instead of hyphens.</span></span> <span data-ttu-id="94d72-258">たとえば、`Contoso-Utility-UsefulStuff` や `Contoso_Utility_UsefulStuff` ではなく `Contoso.Utility.UsefulStuff` を使用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-258">For example, use `Contoso.Utility.UsefulStuff` rather than `Contoso-Utility-UsefulStuff` or `Contoso_Utility_UsefulStuff`.</span></span> <span data-ttu-id="94d72-259">パッケージ識別子がコードで使用される名前空間と一致すれば、利用者にとっても便利です。</span><span class="sxs-lookup"><span data-stu-id="94d72-259">Consumers also find it helpful when the package identifier matches the namespaces used in the code.</span></span>
- <span data-ttu-id="94d72-260">**サンプル パッケージ**: 別のパッケージの使用方法を示すサンプル コードのパッケージを生成する場合、`Contoso.Utility.UsefulStuff.Sample` のように、識別子のサフィックスとして `.Sample` を付けます。</span><span class="sxs-lookup"><span data-stu-id="94d72-260">**Sample Packages**: If you produce a package of sample code that demonstrates how to use another package, attach `.Sample` as a suffix to the identifier, as in `Contoso.Utility.UsefulStuff.Sample`.</span></span> <span data-ttu-id="94d72-261">(サンプル パッケージは、もちろん、他のパッケージに依存します。)サンプル パッケージを作成するとき、前述のように、規則ベースの作業ディレクトリを使用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-261">(The sample package would of course have a dependency on the other package.) When creating a sample package, use the convention-based working directory method described earlier.</span></span> <span data-ttu-id="94d72-262">`content` フォルダーで、`\Samples\Contoso.Utility.UsefulStuff.Sample` のように、`\Samples\<identifier>` という名前のフォルダーにサンプル コードを配置します。</span><span class="sxs-lookup"><span data-stu-id="94d72-262">In the `content` folder, arrange the sample code in a folder called `\Samples\<identifier>` as in `\Samples\Contoso.Utility.UsefulStuff.Sample`.</span></span>

<span data-ttu-id="94d72-263">**パッケージ バージョンのベスト プラクティス:**</span><span class="sxs-lookup"><span data-stu-id="94d72-263">**Best practices for the package version:**</span></span>

- <span data-ttu-id="94d72-264">必須ではありませんが、一般的に、ライブラリに合わせてパッケージの番号を設定します。</span><span class="sxs-lookup"><span data-stu-id="94d72-264">In general, set the version of the package to match the library, though this is not strictly required.</span></span> <span data-ttu-id="94d72-265">これはパッケージを 1 つのアセンブリに限定すれば簡単なことです。「[パッケージ化するアセンブリを決定する](#deciding-which-assemblies-to-package)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-265">This is a simple matter when you limit a package to a single assembly, as described earlier in [Deciding which assemblies to package](#deciding-which-assemblies-to-package).</span></span> <span data-ttu-id="94d72-266">概して、NuGet 自体は依存関係の解決時、パッケージ バージョンを使います。アセンブリ バージョンではありません。</span><span class="sxs-lookup"><span data-stu-id="94d72-266">Overall, remember that NuGet itself deals with package versions when resolving dependencies, not assembly versions.</span></span>
- <span data-ttu-id="94d72-267">非標準のバージョン スキーマを使用するとき、「[パッケージのバージョン管理](../reference/package-versioning.md)」で説明するように、NuGet バージョン管理ルールを検討してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-267">When using a non-standard version scheme, be sure to consider the NuGet versioning rules as explained in [Package versioning](../reference/package-versioning.md).</span></span>

> <span data-ttu-id="94d72-268">バージョン管理の理解には、次の一連のブログ投稿が役立ちます。</span><span class="sxs-lookup"><span data-stu-id="94d72-268">The following series of brief blog posts are also helpful to understand versioning:</span></span>
>
> - <span data-ttu-id="94d72-269">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html) (パート 1: DLL 地獄)</span><span class="sxs-lookup"><span data-stu-id="94d72-269">[Part 1: Taking on DLL Hell](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)</span></span>
> - <span data-ttu-id="94d72-270">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html) (パート 2: コア アルゴリズム)</span><span class="sxs-lookup"><span data-stu-id="94d72-270">[Part 2: The core algorithm](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)</span></span>
> - <span data-ttu-id="94d72-271">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html) (パート 3: バインド リダイレクトによる統合)</span><span class="sxs-lookup"><span data-stu-id="94d72-271">[Part 3: Unification via Binding Redirects](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)</span></span>

## <a name="setting-a-package-type"></a><span data-ttu-id="94d72-272">パッケージの種類の設定</span><span class="sxs-lookup"><span data-stu-id="94d72-272">Setting a package type</span></span>

<span data-ttu-id="94d72-273">NuGet 3.5+ では、パッケージに特定の*パッケージの種類*の印を付け、その用途を示すことができます。</span><span class="sxs-lookup"><span data-stu-id="94d72-273">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="94d72-274">種類の印が付いていないパッケージ (初期のバージョンの NuGet で作成されたすべてのパッケージが相当) は種類が `Dependency` に初期設定されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-274">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="94d72-275">種類が `Dependency` のパッケージでは、ビルド時または実行時アセットがライブラリとアプリケーションに追加されます。(互換性があれば) あらゆる種類のプロジェクトにインストールできます。</span><span class="sxs-lookup"><span data-stu-id="94d72-275">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="94d72-276">種類が `DotnetCliTool` のパッケージは [.NET CLI](/dotnet/articles/core/tools/index) の拡張であり、コマンド ラインから呼び出されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-276">`DotnetCliTool` type packages are extensions to the [.NET CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="94d72-277">このようなパッケージは .NET Core プロジェクトにのみインストールできます。復元操作には影響を与えません。</span><span class="sxs-lookup"><span data-stu-id="94d72-277">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="94d72-278">このようなプロジェクト別の拡張機能に関する詳細は、[.NET Core 拡張性](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility)ドキュメントにあります。</span><span class="sxs-lookup"><span data-stu-id="94d72-278">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

    <span data-ttu-id="94d72-279">DotnetCliTool パッケージがインストールされると、Visual Studio では、`dependencies` ノードではなく、`project.json` `tools` ノードにパッケージが置かれます。</span><span class="sxs-lookup"><span data-stu-id="94d72-279">When a DotnetCliTool package is installed, Visual Studio places the package in the `project.json` `tools` node instead of the `dependencies` node.</span></span>

- <span data-ttu-id="94d72-280">カスタム タイプのパッケージでは、パッケージ ID と同じ形式ルールに準拠する任意の種類識別子が使用されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-280">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="94d72-281">ただし、`Dependency` と `DotnetCliTool` 以外の種類は、Visual Studio の NuGet パッケージ マネージャーには認識されません。</span><span class="sxs-lookup"><span data-stu-id="94d72-281">Any type other than `Dependency` and `DotnetCliTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="94d72-282">パッケージの種類は `.nuspec` ファイルか `project.json` で設定されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-282">Package types are set either in the `.nuspec` file or in `project.json`.</span></span> <span data-ttu-id="94d72-283">いずれの場合でも、種類 `Dependency` を明示的に*設定せず*、種類が指定されているときにこの種類を採用する NuGet に依存する方法が下位互換性のために最適です。</span><span class="sxs-lookup"><span data-stu-id="94d72-283">In both cases, it's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="94d72-284">`.nuspec`: `<metadata>` 要素の下の `packageTypes\packageType` ノード内のパッケージの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="94d72-284">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

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

- <span data-ttu-id="94d72-285">`project.json`: `packOptions.packageType` プロパティ json 内のパッケージの種類を示します。</span><span class="sxs-lookup"><span data-stu-id="94d72-285">`project.json`: Indicate the package type within a `packOptions.packageType` property json:</span></span>

    ```json
    {
        // ...
        "packOptions": {
        "packageType": "DotnetCliTool"
        }
    }
    ```

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="94d72-286">ReadMe とその他のファイルの追加</span><span class="sxs-lookup"><span data-stu-id="94d72-286">Adding a readme and other files</span></span>

<span data-ttu-id="94d72-287">パッケージに含めるファイルを直接指定するには、`.nuspec` ファイルの `<files>` ノードを使用します。このノードは `<metadata>` タグの*後に入ります*。</span><span class="sxs-lookup"><span data-stu-id="94d72-287">To directly specify files to include in the package, use the `<files>` node in the `.nuspec` file, which *follows* the `<metadata>` tag:</span></span>

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
> <span data-ttu-id="94d72-288">規則ベースの作業ディレクトリ手法を利用するとき、ReadMe.txt をパッケージ ルートに、`content` フォルダーにその他のコンテンツを配置できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-288">When using the convention-based working directory approach, you can place the readme.txt in the package root and other content in the `content` folder.</span></span> <span data-ttu-id="94d72-289">マニフェストで必須の `<file>` 要素はありません。</span><span class="sxs-lookup"><span data-stu-id="94d72-289">No `<file>` elements are necessary in the manifest.</span></span>

<span data-ttu-id="94d72-290">パッケージ ルートに `readme.txt` という名前のファイルを含めると、Visual Studio では、パッケージを直接インストールした直後、そのファイルの内容がプレーンテキストとして表示されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-290">When you include a file named `readme.txt` in the package root, Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="94d72-291">(パッケージが依存関係としてインストールされた場合、ReadMe ファイルは表示されません。)</span><span class="sxs-lookup"><span data-stu-id="94d72-291">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="94d72-292">たとえば、HtmlAgilityPack パッケージの ReadMe は次のように表示されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-292">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![インストール時の NuGet パッケージの ReadMe ファイルの表示](media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="94d72-294">`.nuspec` ファイルに空の `<files>` ノードを含める場合、NuGet では、`lib` フォルダーの内容以外の内容はパッケージに入りません。</span><span class="sxs-lookup"><span data-stu-id="94d72-294">If you include an empty `<files>` node in the `.nuspec` file, NuGet doesn't include any other content in the package other than what's in the `lib` folder.</span></span>

## <a name="including-msbuild-props-and-targets-in-a-package"></a><span data-ttu-id="94d72-295">パッケージに MSBuild プロパティとターゲットを含める</span><span class="sxs-lookup"><span data-stu-id="94d72-295">Including MSBuild props and targets in a package</span></span>

<span data-ttu-id="94d72-296">ビルド時のカスタム ツールまたはプロセスの実行など、場合によっては、パッケージを使用するプロジェクト内のカスタム ビルド ターゲットまたはプロパティを追加する必要があります。</span><span class="sxs-lookup"><span data-stu-id="94d72-296">In some cases, you might want to add custom build targets or properties in projects that consume your package, such as running a custom tool or process during build.</span></span> <span data-ttu-id="94d72-297">これは、プロジェクトの `\build` フォルダー内に形式 `<package_id>.targets` または `<package_id>.props` で (`Contoso.Utility.UsefulStuff.targets` のように) ファイルを配置することで行います。</span><span class="sxs-lookup"><span data-stu-id="94d72-297">You do this by placing files in the form `<package_id>.targets` or `<package_id>.props` (such as `Contoso.Utility.UsefulStuff.targets`) within the `\build` folder of the project.</span></span>

<span data-ttu-id="94d72-298">ルート `\build` フォルダーのファイルは、すべてのターゲット フレームワークで適切であると見なされます。</span><span class="sxs-lookup"><span data-stu-id="94d72-298">Files in the root `\build` folder are considered suitable for all target frameworks.</span></span> <span data-ttu-id="94d72-299">ファイルをフレームワーク固有にするには、次のように、まず、適切なサブフォルダーにそのファイルを配置します。</span><span class="sxs-lookup"><span data-stu-id="94d72-299">To provide framework-specific files, first place those within appropriate subfolders, such as the following:</span></span>

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

<span data-ttu-id="94d72-300">次に `.nuspec` ファイルで、`<files>` ノードのそれらのファイルを参照するようにします。</span><span class="sxs-lookup"><span data-stu-id="94d72-300">Then in the `.nuspec` file, be sure to refer to these files in the `<files>` node:</span></span>

```xml
<?xml version="1.0"?>
<package >
    <metadata>
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

<span data-ttu-id="94d72-301">NuGet 2.x は `\build` ファイルを使用してパッケージをインストールすると、`.targets` ファイルと `.props` ファイルを指すプロジェクト ファイルに MSBuild `<Import>` 要素を追加します。</span><span class="sxs-lookup"><span data-stu-id="94d72-301">When NuGet 2.x installs a package with `\build` files, it adds an MSBuild `<Import>` elements in the project file pointing to the `.targets` and `.props` files.</span></span> <span data-ttu-id="94d72-302">(`.props` はプロジェクト ファイルの一番上に、`.targets` は一番下に追加されます。)</span><span class="sxs-lookup"><span data-stu-id="94d72-302">(`.props` is added at the top of the project file; `.targets` is added at the bottom.)</span></span>

<span data-ttu-id="94d72-303">NuGet 3.x を使用する場合、ターゲットはプロジェクトに追加されませんが、`project.lock.json` を通じて使用できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-303">With NuGet 3.x, targets are not added to the project but are instead made available through the `project.lock.json`.</span></span>

## <a name="authoring-packages-with-com-interop-assemblies"></a><span data-ttu-id="94d72-304">COM 相互運用アセンブリを含むパッケージを作成する</span><span class="sxs-lookup"><span data-stu-id="94d72-304">Authoring packages with COM interop assemblies</span></span>

<span data-ttu-id="94d72-305">COM 相互運用アセンブリを含むパッケージには、PackageReference 形式を利用して正しい `EmbedInteropTypes` メタデータがプロジェクトに追加されるように、適切な [targets ファイル](#including-msbuild-props-and-targets-in-a-package)が含まれる必要があります。</span><span class="sxs-lookup"><span data-stu-id="94d72-305">Packages that contain COM interop assemblies must include an appropriate [targets file](#including-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="94d72-306">既定では、PackageReference が使用されるとき、`EmbedInteropTypes` メタデータは常にすべてのアセンブリに対して false になります。それにより、targets ファイルでこのメタデータが明示的に追加されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-306">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="94d72-307">競合を回避するために、ターゲット名を一意にする必要があります。理想的には、パッケージ名と組み込むアセンブリの組み合わせを使用します。下の例の `{InteropAssemblyName}` をその値で置換します。</span><span class="sxs-lookup"><span data-stu-id="94d72-307">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="94d72-308">(例については、[NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) もご覧ください。)</span><span class="sxs-lookup"><span data-stu-id="94d72-308">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml      
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="94d72-309">`packages.config` 参照形式を利用するとき、パッケージからアセンブリの参照を追加すると、NuGet と Visual Studio は COM 相互運用アセンブリがないか調べ、プロジェクト ファイルで `EmbedInteropTypes` を true に設定します。</span><span class="sxs-lookup"><span data-stu-id="94d72-309">Note that when using the `packages.config` reference format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="94d72-310">この場合、ターゲットが上書きされます。</span><span class="sxs-lookup"><span data-stu-id="94d72-310">In this case the targets are overriden.</span></span>

<span data-ttu-id="94d72-311">また、既定では、[ビルド アセットの推移的なフローはありません](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets)。</span><span class="sxs-lookup"><span data-stu-id="94d72-311">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="94d72-312">ここで説明したように作成したパッケージの動作は、プロジェクトからプロジェクト参照に推移的依存関係として引き出されたときとは異なります。</span><span class="sxs-lookup"><span data-stu-id="94d72-312">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="94d72-313">パッケージの利用者は、ビルドを含めないように PrivateAssets の既定値を変更することでそれをフローさせることができます。</span><span class="sxs-lookup"><span data-stu-id="94d72-313">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>  

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a><span data-ttu-id="94d72-314">nuget パックを実行し、.nupkg ファイルを生成する</span><span class="sxs-lookup"><span data-stu-id="94d72-314">Running nuget pack to generate the .nupkg file</span></span>

<span data-ttu-id="94d72-315">アセンブリまたは規則ベースの作業ディレクトリを使用するとき、自分の `.nuspec` ファイルで `nuget pack` を実行してパッケージを作成します。`<manifest-name>` を特定のファイル名で置換します。</span><span class="sxs-lookup"><span data-stu-id="94d72-315">When using an assembly or the convention-based working directory, create a package by running `nuget pack` with your `.nuspec` file, replacing `<manifest-name>` with your specific filename:</span></span>

```
nuget pack <project-name>.nuspec
```

<span data-ttu-id="94d72-316">Visual Studio プロジェクトを使用するとき、自分のプロジェクト ファイルで `nuget pack` を実行します。それにより、プロジェクトの `.nuspec` ファイルが自動的に読み込まれ、その中にトークンがあれば、プロジェクト ファイルの値を利用して置換されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-316">When using a Visual Studio project, run `nuget pack` with your project file, which automatically loads the project's `.nuspec` file and replaces any tokens within it using values in the project file:</span></span>

```
nuget pack <project-name>.csproj
```

> [!Note]
> <span data-ttu-id="94d72-317">トークンを置換するには、プロジェクト ファイルを直接使用する必要があります。プロジェクトがトークン値のソースであるからです。</span><span class="sxs-lookup"><span data-stu-id="94d72-317">Using the project file directly is necessary for token replacement because the project is the source of the token values.</span></span> <span data-ttu-id="94d72-318">`.nuspec` ファイルで `nuget pack` を使用する場合、トークンは置換されません。</span><span class="sxs-lookup"><span data-stu-id="94d72-318">Token replacement does not happen if you use `nuget pack` with a `.nuspec` file.</span></span>

<span data-ttu-id="94d72-319">いずれの場合も、`nuget pack` では、`.git` や `.hg` のようなピリオドで始まるフォルダーは除外されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-319">In all cases, `nuget pack` excludes folders that start with a period, such as `.git` or `.hg`.</span></span>

<span data-ttu-id="94d72-320">NuGet では、修正が必要なエラーが `.nuspec` ファイルで見つかった場合、それが示されます。マニフェストのプレースホルダー値を変更し忘れたなどです。</span><span class="sxs-lookup"><span data-stu-id="94d72-320">NuGet indicates if there are any errors in the `.nuspec` file that need correcting, such as forgetting to change placeholder values in the manifest.</span></span>

<span data-ttu-id="94d72-321">`nuget pack` が成功すると、`.nupkg` ファイルが生成されます。「[パッケージの公開](../create-packages/publish-a-package.md)」に説明があるように、このファイルを適切なギャラリーに公開できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-321">Once `nuget pack` succeeds, you have a `.nupkg` file that you can publish to a suitable gallery as described in [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

> [!Tip]
> <span data-ttu-id="94d72-322">作成後のパッケージを調べる便利な方法は、[パッケージ エクスプローラー](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) ツールでそれを開くことです。</span><span class="sxs-lookup"><span data-stu-id="94d72-322">A helpful way to examine a package after creating it is to open it in the [Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer) tool.</span></span> <span data-ttu-id="94d72-323">パッケージの内容とそのマニフェストがグラフィック表示されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-323">This gives you a graphical view of the package contents and its manifest.</span></span> <span data-ttu-id="94d72-324">生成された `.nupkg` ファイルの名前を `.zip` ファイルに変更し、その内容を直接調べることもできます。</span><span class="sxs-lookup"><span data-stu-id="94d72-324">You can also rename the resulting `.nupkg` file to a `.zip` file and explore its contents directly.</span></span>

### <a name="additional-options"></a><span data-ttu-id="94d72-325">追加オプション</span><span class="sxs-lookup"><span data-stu-id="94d72-325">Additional options</span></span>

<span data-ttu-id="94d72-326">`nuget pack` ではさまざまなコマンドライン スイッチを使用できます。ファイルを除外したり、マニフェストのバージョン番号を上書きしたり、出力フォルダーを変更したりできます。</span><span class="sxs-lookup"><span data-stu-id="94d72-326">You can use various command-line switches with `nuget pack` to exclude files, override the version number in the manifest, and change the output folder, among other features.</span></span> <span data-ttu-id="94d72-327">完全な一覧は、[pack コマンドに関するページ](../tools/cli-ref-pack.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="94d72-327">For a complete list, refer to the [pack command reference](../tools/cli-ref-pack.md).</span></span>

<span data-ttu-id="94d72-328">Visual Studio プロジェクトの共通オプションには以下のようなものがあります。</span><span class="sxs-lookup"><span data-stu-id="94d72-328">The following options are a few that are common with Visual Studio projects:</span></span>

- <span data-ttu-id="94d72-329">**参照されるプロジェクト**: プロジェクトが他のプロジェクトを参照する場合、参照されるプロジェクトをパッケージの一部あるいは依存関係として追加できます。`-IncludeReferencedProjects` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-329">**Referenced projects**: If the project references other projects, you can add the referenced projects as part of the package, or as dependencies, by using the `-IncludeReferencedProjects` option:</span></span>

    ```
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    <span data-ttu-id="94d72-330">この包含プロセスは再帰的です。`MyProject.csproj` が B と C を参照し、それらのプロジェクトが D、E、F を参照する場合、B、C、D、E、F からのファイルがパッケージに含まれます。</span><span class="sxs-lookup"><span data-stu-id="94d72-330">This inclusion process is recursive, so if `MyProject.csproj` references projects B and C, and those projects reference D, E, and F, then files from B, C, D, E, and F are included in the package.</span></span>

    <span data-ttu-id="94d72-331">参照されるプロジェクトにそれ自体の `.nuspec` ファイルが含まれる場合、NuGet では、その参照されるプロジェクトが依存関係として追加されます。</span><span class="sxs-lookup"><span data-stu-id="94d72-331">If a referenced project includes a `.nuspec` file of its own, then NuGet adds that referenced project as a dependency instead.</span></span>  <span data-ttu-id="94d72-332">そのプロジェクトを個別にパッケージ化し、公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="94d72-332">You need to package and publish that project separately.</span></span>

- <span data-ttu-id="94d72-333">**ビルド構成**: 既定では、NuGet では、プロジェクト ファイルに設定されている既定のビルド構成が使用されます。一般的には、*デバッグ*です。</span><span class="sxs-lookup"><span data-stu-id="94d72-333">**Build configuration**: By default, NuGet uses the default build configuration set in the project file, typically *Debug*.</span></span> <span data-ttu-id="94d72-334">*リリース*など、別のビルド構成からファイルをパッケージ化するには、構成と共に `-properties` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-334">To pack files from a different build configuration, such as *Release*, use the `-properties` option with the configuration:</span></span>

    ```
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- <span data-ttu-id="94d72-335">**シンボル**: 利用者がデバッガーでパッケージ コードをステップ実行することを可能にするシンボルを含めるには、`-Symbols` オプションを使用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-335">**Symbols**: to include symbols that allow consumers to step through your package code in the debugger, use the `-Symbols` option:</span></span>

    ```
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a><span data-ttu-id="94d72-336">パッケージ インストールのテスト</span><span class="sxs-lookup"><span data-stu-id="94d72-336">Testing package installation</span></span>

<span data-ttu-id="94d72-337">パッケージを公開する前に、通常、パッケージをプロジェクトにインストールするプロセスをテストします。</span><span class="sxs-lookup"><span data-stu-id="94d72-337">Before publishing a package, you typically want to test the process of installing a package into a project.</span></span> <span data-ttu-id="94d72-338">このテストにより、必要なファイルがすべて、プロジェクト内の適切な場所に入ります。</span><span class="sxs-lookup"><span data-stu-id="94d72-338">The tests make sure that the necessarily files all end up in their correct places in the project.</span></span>

<span data-ttu-id="94d72-339">インストールは Visual Studio またはコマンド ラインで手動テストできます。通常の[パッケージ インストール手順](../Quickstart/Use-a-Package.md)を利用します。</span><span class="sxs-lookup"><span data-stu-id="94d72-339">You can test installations manually in Visual Studio or on the command line using the normal [package installation steps](../Quickstart/Use-a-Package.md).</span></span>

<span data-ttu-id="94d72-340">自動テストの基本プロセスは次のようになります。</span><span class="sxs-lookup"><span data-stu-id="94d72-340">For automated testing, the basic process is as follows:</span></span>

1. <span data-ttu-id="94d72-341">`.nupkg` ファイルをローカル フォルダーにコピーします。</span><span class="sxs-lookup"><span data-stu-id="94d72-341">Copy the `.nupkg` file to a local folder.</span></span>
1. <span data-ttu-id="94d72-342">`nuget sources -name <name> -source <path>` コマンドを利用し、パッケージ ソースにフォルダーを追加します ([nuget ソース](../tools/cli-ref-sources.md)を参照してください)。</span><span class="sxs-lookup"><span data-stu-id="94d72-342">Add the folder to your package sources using the `nuget sources -name <name> -source <path>` command (see [nuget sources](../tools/cli-ref-sources.md)).</span></span> <span data-ttu-id="94d72-343">指定されたコンピューターのいずれかで、このローカル ソースを 1 回設定します。</span><span class="sxs-lookup"><span data-stu-id="94d72-343">Note that you need only set this local source once on any given computer.</span></span>
1. <span data-ttu-id="94d72-344">`nuget install <packageID> -source <name>` を利用し、そのソースからパッケージをインストールします。`<name>` は、`nuget sources` に指定されたソースの名前に一致します。</span><span class="sxs-lookup"><span data-stu-id="94d72-344">Install the package from that source using `nuget install <packageID> -source <name>` where `<name>` matches the name of your source as given to `nuget sources`.</span></span> <span data-ttu-id="94d72-345">ソースを指定することで、そのソースだけからパッケージがインストールされます。</span><span class="sxs-lookup"><span data-stu-id="94d72-345">Specifying the source ensures that the package is installed from that source alone.</span></span>
1. <span data-ttu-id="94d72-346">ファイルが正しくインストールされていることをファイル システムで調べます。</span><span class="sxs-lookup"><span data-stu-id="94d72-346">Examine the file system to check that files are installed correctly.</span></span>

## <a name="next-steps"></a><span data-ttu-id="94d72-347">次の手順</span><span class="sxs-lookup"><span data-stu-id="94d72-347">Next Steps</span></span>

<span data-ttu-id="94d72-348">`.nupkg` ファイルとなるパッケージを作成したら、「[パッケージの公開](../create-packages/publish-a-package.md)」の説明にあるように、選択したギャラリーにパッケージを公開できます。</span><span class="sxs-lookup"><span data-stu-id="94d72-348">Once you've created a package, which is a `.nupkg` file, you can publish it to the gallery of your choice as described on [Publishing a Package](../create-packages/publish-a-package.md).</span></span>

<span data-ttu-id="94d72-349">パッケージの機能を拡張したり、次のトピックで説明するように、その他の方法で他のシナリオをサポートしたりすると便利な場合があります。</span><span class="sxs-lookup"><span data-stu-id="94d72-349">You might also want to extend the capabilities of your package or otherwise support other scenarios as described in the following topics:</span></span>

- [<span data-ttu-id="94d72-350">パッケージのバージョン管理</span><span class="sxs-lookup"><span data-stu-id="94d72-350">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="94d72-351">複数のターゲット フレームワークのサポート</span><span class="sxs-lookup"><span data-stu-id="94d72-351">Supporting multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="94d72-352">ソース ファイルと構成ファイルの変換</span><span class="sxs-lookup"><span data-stu-id="94d72-352">Transformations of source and configuration files</span></span>](../create-packages/source-and-config-file-transformations.md)
- [<span data-ttu-id="94d72-353">ローカリゼーション</span><span class="sxs-lookup"><span data-stu-id="94d72-353">Localization</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="94d72-354">プレリリース バージョン</span><span class="sxs-lookup"><span data-stu-id="94d72-354">Pre-release versions</span></span>](../create-packages/prerelease-packages.md)

<span data-ttu-id="94d72-355">最後になりますが、次のような種類のパッケージもあります。</span><span class="sxs-lookup"><span data-stu-id="94d72-355">Finally, there are additional package types to be aware of:</span></span>

- [<span data-ttu-id="94d72-356">ネイティブ パッケージ</span><span class="sxs-lookup"><span data-stu-id="94d72-356">Native Packages</span></span>](../create-packages/native-packages.md)
- [<span data-ttu-id="94d72-357">シンボル パッケージ</span><span class="sxs-lookup"><span data-stu-id="94d72-357">Symbol Packages</span></span>](../create-packages/symbol-packages.md)
