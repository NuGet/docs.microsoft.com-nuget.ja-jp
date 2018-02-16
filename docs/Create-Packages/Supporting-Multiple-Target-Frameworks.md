---
title: "NuGet パッケージの複数バージョン対応 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 09/27/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "1 つの NuGet パッケージ内から複数の .NET Framework バージョンに対応するためのさまざま方法の説明。"
keywords: "NuGet パッケージ バージョン対応, .NET Framework バージョン, NuGet と .NET, 複数のフレームワークのバージョンに対応, NuGet パッケージ作成"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 723dbcc12ecc4e16d2ba4662559f107b9b22e2c2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="supporting-multiple-net-framework-versions"></a><span data-ttu-id="5818e-104">複数の .NET Framework バージョンのサポート</span><span class="sxs-lookup"><span data-stu-id="5818e-104">Supporting multiple .NET framework versions</span></span>

<span data-ttu-id="5818e-105">*NuGet 4.0+ を使用する .NET Core プロジェクトについては、「[NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md)」 (MSBuild ターゲットとしての NuGet pack および restore) をご覧ください。複数バージョン対応に関する詳細があります。*</span><span class="sxs-lookup"><span data-stu-id="5818e-105">*For .NET Core projects using NuGet 4.0+, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md) for details on cross-targeting.*</span></span>

<span data-ttu-id="5818e-106">多くのライブラリは、特定のバージョンの .NET Framework に対応しています。</span><span class="sxs-lookup"><span data-stu-id="5818e-106">Many libraries target a specific version of the .NET Framework.</span></span> <span data-ttu-id="5818e-107">たとえば、あるバージョンのライブラリは UWP に固有であり、別のバージョンは .NET Framework 4.6 の機能を活用します。</span><span class="sxs-lookup"><span data-stu-id="5818e-107">For example, you might have one version of your library that's specific to UWP, and another version that takes advantage of features in .NET Framework 4.6.</span></span>

<span data-ttu-id="5818e-108">それに対応するために、NuGet では、「[パッケージを作成する](../create-packages/creating-a-package.md#from-a-convention-based-working-directory)」に説明がある、規則ベースの作業ディレクトリ方法を利用するとき、1 つのパッケージに同じライブラリの複数のバージョンを置くことができます。</span><span class="sxs-lookup"><span data-stu-id="5818e-108">To accommodate this, NuGet supports putting multiple versions of the same library in a single package when using the convention-based working directory method described in [Creating a package](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span>

## <a name="framework-version-folder-structure"></a><span data-ttu-id="5818e-109">フレームワーク バージョンのフォルダー構造</span><span class="sxs-lookup"><span data-stu-id="5818e-109">Framework version folder structure</span></span>

<span data-ttu-id="5818e-110">1 つだけのバージョンのライブラリを含むパッケージまたは複数のフレームワークを対象とするパッケージをビルドするときは常に、小文字と大文字を区別するフレームワーク名を利用し、`lib` の下にサブフォルダーを作ります。次の規則を利用します。</span><span class="sxs-lookup"><span data-stu-id="5818e-110">When building a package that contains only one version of a library or target multiple frameworks, you always make subfolders under `lib` using different case-sensitive framework names with the following convention:</span></span>

    lib\{framework name}[{version}]

<span data-ttu-id="5818e-111">サポートされている名前の完全一覧については、[ターゲット フレームワーク参照](../reference/target-frameworks.md#supported-frameworks)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5818e-111">For a complete list of supported names, see the [Target Frameworks reference](../reference/target-frameworks.md#supported-frameworks).</span></span>

<span data-ttu-id="5818e-112">フレームワークに固有ではないライブラリ バージョンは、ルート `lib` フォルダーに直接置かないでください。</span><span class="sxs-lookup"><span data-stu-id="5818e-112">You should never have a version of the library that is not specific to a framework and placed directly in the root `lib` folder.</span></span> <span data-ttu-id="5818e-113">(この機能は `packages.config` でのみサポートされていました。)</span><span class="sxs-lookup"><span data-stu-id="5818e-113">(This capability was supported only with `packages.config`).</span></span> <span data-ttu-id="5818e-114">それを行うと、あらゆるターゲット フレームワークに対応するようになり、どこでもインストールできてしまいます。その結果、予想外のランタイム エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="5818e-114">Doing so would make the compatible with any target framework and allow it to be installed anywhere, likely resulting in unexpected runtime errors.</span></span> <span data-ttu-id="5818e-115">ルート フォルダー (`lib\abc.dll` など) またはサブフォルダー (`lib\abc\abc.dll` など) へのアセンブリ追加はなくなりました。PackagesReference 形式を使用するときは無視されます。</span><span class="sxs-lookup"><span data-stu-id="5818e-115">Adding assemblies in the root folder (such as `lib\abc.dll`) or subfolders (such as `lib\abc\abc.dll`) has been deprecated and is ignored when using the PackagesReference format.</span></span>

<span data-ttu-id="5818e-116">たとえば、次のフォルダー構造では、フレームワーク固有の 4 つのバージョンのアセンブリがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="5818e-116">For example, the following folder structure supports four versions of an assembly that are framework-specific:</span></span>

    \lib
        \net46
            \MyAssembly.dll
        \net461
            \MyAssembly.dll
        \uap
            \MyAssembly.dll
        \netcore
            \MyAssembly.dll

<span data-ttu-id="5818e-117">パッケージのビルド時、これらすべてのファイルを簡単に含めるには、`.nuspec` の `<files>` セクションに再帰的 `**` ワイルドカードを使用します。</span><span class="sxs-lookup"><span data-stu-id="5818e-117">To easily include all these files when building the package, use a recursive `**` wildcard in the `<files>` section of your `.nuspec`:</span></span>

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a><span data-ttu-id="5818e-118">アーキテクチャ固有フォルダー</span><span class="sxs-lookup"><span data-stu-id="5818e-118">Architecture-specific folders</span></span>

<span data-ttu-id="5818e-119">アーキテクチャ固有のアセンブリがあるとき、つまり、個々のアセンブリが ARM、x86、x64 を対象とするとき、`runtimes` という名前のフォルダーの `{platform}-{architecture}\lib\{framework}` または `{platform}-{architecture}\native` という名前のサブフォルダー内にそれを置く必要があります。</span><span class="sxs-lookup"><span data-stu-id="5818e-119">If you have architecture-specific assemblies, that is, separate assemblies that target ARM, x86, and x64, you must place them in a folder named `runtimes` within sub-folders named `{platform}-{architecture}\lib\{framework}` or `{platform}-{architecture}\native`.</span></span> <span data-ttu-id="5818e-120">たとえば、次のフォルダー構造は、Windows 10 と `uap10.0` フレームワークを対象とするネイティブ DLL とマネージ DLL の両方に対応します。</span><span class="sxs-lookup"><span data-stu-id="5818e-120">For example, the following folder structure would accommodate both native and managed DLLs targeting Windows 10 and the `uap10.0` framework:</span></span>

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

<span data-ttu-id="5818e-121">`.nuspec` マニフェストでこれらのファイルを参照する例については、「[Create UWP Packages](../guides/create-uwp-packages.md)」 (UWP パッケージの作成) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5818e-121">See [Create UWP Packages](../guides/create-uwp-packages.md) for an example of referencing these files in the `.nuspec` manifest.</span></span>

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a><span data-ttu-id="5818e-122">プロジェクトでアセンブリ バージョンとターゲット フレームワークを組み合わせる</span><span class="sxs-lookup"><span data-stu-id="5818e-122">Matching assembly versions and the target framework in a project</span></span>

<span data-ttu-id="5818e-123">複数のアセンブリ バージョンを含むパッケージを NuGet がインストールすると、アセンブリのフレームワーク名とプロジェクトのターゲット フレームワークの照合が試行されます。</span><span class="sxs-lookup"><span data-stu-id="5818e-123">When NuGet installs a package that has multiple assembly versions, it tries to match the framework name of the assembly with the target framework of the project.</span></span>

<span data-ttu-id="5818e-124">一致が見つからない場合、プロジェクトのターゲット フレームワークと同じかそれより下のバージョンの中で最も上のバージョンのアセンブリがコピーされます。</span><span class="sxs-lookup"><span data-stu-id="5818e-124">If a match is not found, NuGet copies the assembly for the highest version that is less than or equal to the project's target framework, if available.</span></span> <span data-ttu-id="5818e-125">互換性のあるアセンブリが見つからない場合、エラー メッセージが返されます。</span><span class="sxs-lookup"><span data-stu-id="5818e-125">If no compatible assembly is found, NuGet returns an appropriate error message.</span></span>

<span data-ttu-id="5818e-126">たとえば、パッケージに次のフォルダー構造があるとします。</span><span class="sxs-lookup"><span data-stu-id="5818e-126">For example, consider the following folder structure in a package:</span></span>

    \lib
        \net45
            \MyAssembly.dll
        \net461
            \MyAssembly.dll

<span data-ttu-id="5818e-127">.NET Framework 4.6 を対象とするプロジェクトにこのパッケージをインストールすると、NuGet は `net45` フォルダーにアセンブリをインストールします。4.6 以下で利用できる最も上のバージョンであるためです。</span><span class="sxs-lookup"><span data-stu-id="5818e-127">When installing this package in a project that targets .NET Framework 4.6, NuGet installs the assembly in the `net45` folder, because that's the highest available version that's less than or equal to 4.6.</span></span>

<span data-ttu-id="5818e-128">一方、プロジェクトが .NET Framework 4.6.1 を対象とする場合、NuGet は `net461` フォルダーにアセンブリをインストールします。</span><span class="sxs-lookup"><span data-stu-id="5818e-128">If the project targets .NET Framework 4.6.1, on the other hand, NuGet installs the assembly in the `net461` folder.</span></span>

<span data-ttu-id="5818e-129">プロジェクトが .NET Framework 4.0 以前を対象とする場合、NuGet はエラー メッセージを出し、互換性のあるアセンブリが見つからないことを伝えます。</span><span class="sxs-lookup"><span data-stu-id="5818e-129">If the project targets .NET framework 4.0 and earlier, NuGet throws an appropriate error message for not finding the compatible assembly.</span></span>

## <a name="grouping-assemblies-by-framework-version"></a><span data-ttu-id="5818e-130">フレームワーク バージョン別にアセンブリをグループ化する</span><span class="sxs-lookup"><span data-stu-id="5818e-130">Grouping assemblies by framework version</span></span>

<span data-ttu-id="5818e-131">NuGet は、パッケージ内の 1 つだけのライブラリ フォルダーからアセンブリをコピーします。</span><span class="sxs-lookup"><span data-stu-id="5818e-131">NuGet copies assemblies from only a single library folder in the package.</span></span> <span data-ttu-id="5818e-132">たとえば、パッケージに次のフォルダー構造があるとします。</span><span class="sxs-lookup"><span data-stu-id="5818e-132">For example, suppose a package has the following folder structure:</span></span>

    \lib
        \net40
            \MyAssembly.dll (v1.0)
            \MyAssembly.Core.dll (v1.0)
        \net45
            \MyAssembly.dll (v2.0)

<span data-ttu-id="5818e-133">.NET Framework 4.5 を対象とするプロジェクトにパッケージがインストールされるとき、インストールされる唯一のアセンブリは `MyAssembly.dll` (v2.0) です。</span><span class="sxs-lookup"><span data-stu-id="5818e-133">When the package is installed in a project that targets .NET Framework 4.5, `MyAssembly.dll` (v2.0) is the only assembly installed.</span></span> <span data-ttu-id="5818e-134">`MyAssembly.Core.dll` (v1.0) はインストールされません。`net45` フォルダーの一覧にないためです。</span><span class="sxs-lookup"><span data-stu-id="5818e-134">`MyAssembly.Core.dll` (v1.0) is not installed because it's not listed in the `net45` folder.</span></span> <span data-ttu-id="5818e-135">`MyAssembly.Core.dll` が `MyAssembly.dll` のバージョン 2.0 に結合されている可能性があるため、NuGet はこのように動作します。</span><span class="sxs-lookup"><span data-stu-id="5818e-135">NuGet behaves this way because `MyAssembly.Core.dll` might have merged into version 2.0 of `MyAssembly.dll`.</span></span>

<span data-ttu-id="5818e-136">.NET Framework 4.5 で `MyAssembly.Core.dll` をインストールする場合、`net45` フォルダーにコピーを置きます。</span><span class="sxs-lookup"><span data-stu-id="5818e-136">If you want `MyAssembly.Core.dll` to be installed for .NET Framework 4.5, place a copy in the `net45` folder.</span></span>

## <a name="grouping-assemblies-by-framework-profile"></a><span data-ttu-id="5818e-137">フレームワーク プロファイル別にアセンブリをグループ化する</span><span class="sxs-lookup"><span data-stu-id="5818e-137">Grouping assemblies by framework profile</span></span>

<span data-ttu-id="5818e-138">NuGet ではまた、ダッシュとプロファイル名をフォルダーの最後に付けることで特定のフレームワーク プロファイルを対象にすることができます。</span><span class="sxs-lookup"><span data-stu-id="5818e-138">NuGet also supports targeting a specific framework profile by appending a dash and the profile name to the end of the folder.</span></span>

    lib\{framework name}-{profile}

<span data-ttu-id="5818e-139">サポートされているプロファイルは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="5818e-139">The supported profiles are as follows:</span></span>

- <span data-ttu-id="5818e-140">`client`: Client Profile</span><span class="sxs-lookup"><span data-stu-id="5818e-140">`client`: Client Profile</span></span>
- <span data-ttu-id="5818e-141">`full`: Full Profile</span><span class="sxs-lookup"><span data-stu-id="5818e-141">`full`: Full Profile</span></span>
- <span data-ttu-id="5818e-142">`wp`: Windows Phone</span><span class="sxs-lookup"><span data-stu-id="5818e-142">`wp`: Windows Phone</span></span>
- <span data-ttu-id="5818e-143">`cf`: Compact Framework</span><span class="sxs-lookup"><span data-stu-id="5818e-143">`cf`: Compact Framework</span></span>

## <a name="determining-which-nuget-target-to-use"></a><span data-ttu-id="5818e-144">使用する NuGet ターゲットを決定する</span><span class="sxs-lookup"><span data-stu-id="5818e-144">Determining which NuGet target to use</span></span>

<span data-ttu-id="5818e-145">ポータブル クラス ライブラリを対象とするライブラリをパッケージ化するとき、フォルダー名と `.nuspec` ファイルで使用する NuGet ターゲットの決定にはこつが要ります。PCL のサブセットのみを対象とする場合は特にそうです。</span><span class="sxs-lookup"><span data-stu-id="5818e-145">When packaging libraries targeting the Portable Class Library it can be tricky to determine which NuGet target you should use in your folder names and `.nuspec` file, especially if targeting only a subset of the PCL.</span></span> <span data-ttu-id="5818e-146">次の外部リソースが役立ちます。</span><span class="sxs-lookup"><span data-stu-id="5818e-146">The following external resources will help you with this:</span></span>

- <span data-ttu-id="5818e-147">[.NET のフレームワーク プロファイル](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span><span class="sxs-lookup"><span data-stu-id="5818e-147">[Framework profiles in .NET](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)</span></span>
- <span data-ttu-id="5818e-148">[ポータブル クラス ライブラリ プロファイル](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): PCL プロファイルとそれと同等の NuGet ターゲットを列挙するテーブル</span><span class="sxs-lookup"><span data-stu-id="5818e-148">[Portable Class Library profiles](http://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Table enumerating PCL profiles and their equivalent NuGet targets</span></span>
- <span data-ttu-id="5818e-149">[ポータブル クラス ライブラリ プロファイル ツール](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): システムで利用できる PCL プロファイルを決定するためのコマンド ライン ツール</span><span class="sxs-lookup"><span data-stu-id="5818e-149">[Portable Class Library profiles tool](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): command line tool for determining PCL profiles available on your system</span></span>

## <a name="content-files-and-powershell-scripts"></a><span data-ttu-id="5818e-150">コンテンツ ファイルと PowerShell スクリプト</span><span class="sxs-lookup"><span data-stu-id="5818e-150">Content files and PowerShell scripts</span></span>

> [!Warning]
> <span data-ttu-id="5818e-151">変更可能なコンテンツ ファイルとスクリプト実行は `packages.config` 形式のみで利用できます。これらは、他のすべての形式を使用するときは使用されません。また、新しいパッケージにはこれらを使用しないでください。</span><span class="sxs-lookup"><span data-stu-id="5818e-151">Mutable content files and script execution are available with the `packages.config` format only; they are deprecated with all other formats and should not be used for any new packages.</span></span>

<span data-ttu-id="5818e-152">`packages.config` では、コンテンツ ファイルと PowerShell スクリプトを、`content` フォルダーと `tools` フォルダー内で同じフォルダー規則を使用し、ターゲット フレームワーク別にグループ化できます。</span><span class="sxs-lookup"><span data-stu-id="5818e-152">With `packages.config`, content files and PowerShell scripts can be grouped by target framework using the same folder convention inside the `content` and `tools` folders.</span></span> <span data-ttu-id="5818e-153">例:</span><span class="sxs-lookup"><span data-stu-id="5818e-153">For example:</span></span>

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

<span data-ttu-id="5818e-154">フレームワーク フォルダーを空のまま残す場合、NuGet はアセンブリ参照やコンテンツ ファイルを追加せず、そのフレームワークの PowerShell スクリプトを実行しません。</span><span class="sxs-lookup"><span data-stu-id="5818e-154">If a framework folder is left empty, NuGet doesn't add assembly references or content files or run the PowerShell scripts for that framework.</span></span>

> [!Note]
> <span data-ttu-id="5818e-155">`init.ps1` はソリューション レベルで実行され、プロジェクトに依存しないため、`tools` フォルダーの下に直接置く必要があります。</span><span class="sxs-lookup"><span data-stu-id="5818e-155">Because `init.ps1` is executed at the solution level and not dependent on project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="5818e-156">フレームワーク フォルダーの下に置いた場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="5818e-156">It's ignored if placed under a framework folder.</span></span>
