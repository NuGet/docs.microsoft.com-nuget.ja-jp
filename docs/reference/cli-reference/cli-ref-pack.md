---
title: NuGet CLI パックコマンド
description: nuget.exe pack コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 649c440d868c89068a069a396919b58b999369e5
ms.sourcegitcommit: f29fa9b93fd59e679fab50d7413bbf67da3ea5b3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/17/2020
ms.locfileid: "86451139"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="6909f-103">pack コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="6909f-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="6909f-104">**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** 2.7 以上</span><span class="sxs-lookup"><span data-stu-id="6909f-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="6909f-105">指定された[nuspec](../nuspec.md)またはプロジェクトファイルに基づいて NuGet パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="6909f-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="6909f-106">`dotnet pack`コマンド (「 [dotnet コマンド](../dotnet-Commands.md)」を参照) と `msbuild -t:pack` (「 [MSBuild ターゲット](../msbuild-targets.md)」を参照) は、代替として使用できます。</span><span class="sxs-lookup"><span data-stu-id="6909f-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="6909f-107">[`dotnet pack`](../dotnet-Commands.md) [`msbuild -t:pack`](../msbuild-targets.md) [PackageReference](../../consume-packages/package-references-in-project-files.md)ベースのプロジェクトでは、またはを使用します。</span><span class="sxs-lookup"><span data-stu-id="6909f-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="6909f-108">Mono では、プロジェクトファイルからパッケージを作成することはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="6909f-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="6909f-109">また、Windows のパス名は変換されないため、ファイル内のローカルではないパスを Unix 形式のパスに調整する必要があり `.nuspec` nuget.exe。</span><span class="sxs-lookup"><span data-stu-id="6909f-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="6909f-110">使用</span><span class="sxs-lookup"><span data-stu-id="6909f-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="6909f-111">`<nuspecPath>`と `<projectPath>` は、 `.nuspec` それぞれまたはプロジェクトファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="6909f-112">Options</span><span class="sxs-lookup"><span data-stu-id="6909f-112">Options</span></span>

| <span data-ttu-id="6909f-113">オプション</span><span class="sxs-lookup"><span data-stu-id="6909f-113">Option</span></span> | <span data-ttu-id="6909f-114">説明</span><span class="sxs-lookup"><span data-stu-id="6909f-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6909f-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="6909f-115">BasePath</span></span> | <span data-ttu-id="6909f-116">[Nuspec](../nuspec.md)ファイルで定義されているファイルのベースパスを設定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-116">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span> |
| <span data-ttu-id="6909f-117">Build</span><span class="sxs-lookup"><span data-stu-id="6909f-117">Build</span></span> | <span data-ttu-id="6909f-118">パッケージをビルドする前にプロジェクトをビルドするように指定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="6909f-119">Exclude (除外)</span><span class="sxs-lookup"><span data-stu-id="6909f-119">Exclude</span></span> | <span data-ttu-id="6909f-120">パッケージの作成時に除外する1つ以上のワイルドカードパターンを指定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="6909f-121">複数のパターンを指定するには、-Exclude フラグを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="6909f-121">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="6909f-122">以下の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6909f-122">See example below.</span></span> |
| <span data-ttu-id="6909f-123">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="6909f-123">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="6909f-124">パッケージをビルドするときに空のディレクトリを含めないようにします。</span><span class="sxs-lookup"><span data-stu-id="6909f-124">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="6909f-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6909f-125">ForceEnglishOutput</span></span> | <span data-ttu-id="6909f-126">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="6909f-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6909f-127">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6909f-127">ConfigFile</span></span> | <span data-ttu-id="6909f-128">パックコマンドの構成ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-128">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="6909f-129">Help</span><span class="sxs-lookup"><span data-stu-id="6909f-129">Help</span></span> | <span data-ttu-id="6909f-130">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="6909f-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="6909f-131">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="6909f-131">IncludeReferencedProjects</span></span> | <span data-ttu-id="6909f-132">ビルドされたパッケージに、依存関係として、またはパッケージの一部として参照プロジェクトを含める必要があることを示します。</span><span class="sxs-lookup"><span data-stu-id="6909f-132">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="6909f-133">参照先のプロジェクトに、 `.nuspec` プロジェクトと同じ名前の対応するファイルがある場合、その参照先プロジェクトは依存関係として追加されます。</span><span class="sxs-lookup"><span data-stu-id="6909f-133">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="6909f-134">それ以外の場合、参照されるプロジェクトはパッケージの一部として追加されます。</span><span class="sxs-lookup"><span data-stu-id="6909f-134">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="6909f-135">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="6909f-135">MinClientVersion</span></span> | <span data-ttu-id="6909f-136">作成したパッケージの*minClientVersion*属性を設定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-136">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="6909f-137">この値は、ファイル内の既存の*minClientVersion*属性 (存在する場合) の値よりも優先され `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="6909f-137">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="6909f-138">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="6909f-138">MSBuildPath</span></span> | <span data-ttu-id="6909f-139">*(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これはよりも優先さ `-MSBuildVersion` れます。</span><span class="sxs-lookup"><span data-stu-id="6909f-139">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="6909f-140">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="6909f-140">MSBuildVersion</span></span> | <span data-ttu-id="6909f-141">*(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-141">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="6909f-142">サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。</span><span class="sxs-lookup"><span data-stu-id="6909f-142">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="6909f-143">既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。</span><span class="sxs-lookup"><span data-stu-id="6909f-143">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="6909f-144">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="6909f-144">NoDefaultExcludes</span></span> | <span data-ttu-id="6909f-145">やなど、ドットで始まる NuGet パッケージファイルとファイルおよびフォルダーの既定の除外を回避し `.svn` `.gitignore` ます。</span><span class="sxs-lookup"><span data-stu-id="6909f-145">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="6909f-146">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="6909f-146">NoPackageAnalysis</span></span> | <span data-ttu-id="6909f-147">パッケージのビルド後に、パックでパッケージの分析を実行しないことを指定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-147">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="6909f-148">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="6909f-148">OutputDirectory</span></span> | <span data-ttu-id="6909f-149">作成したパッケージが格納されているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-149">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="6909f-150">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="6909f-150">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="6909f-151">プロパティ</span><span class="sxs-lookup"><span data-stu-id="6909f-151">Properties</span></span> | <span data-ttu-id="6909f-152">他のオプションの後に、コマンドラインに最後に表示されます。</span><span class="sxs-lookup"><span data-stu-id="6909f-152">Should appear last on the command line after other options.</span></span> <span data-ttu-id="6909f-153">プロジェクトファイルの値をオーバーライドするプロパティの一覧を指定します。「プロパティ名の[一般的な MSBuild プロジェクトプロパティ](/visualstudio/msbuild/common-msbuild-project-properties)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6909f-153">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="6909f-154">ここでのプロパティ引数は、トークン = 値のペアの一覧です。セミコロンで区切られています。ファイル内での各出現箇所は、 `$token$` `.nuspec` 指定された値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="6909f-154">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="6909f-155">値は、引用符で囲まれた文字列にすることができます。</span><span class="sxs-lookup"><span data-stu-id="6909f-155">Values can be strings in quotation marks.</span></span> <span data-ttu-id="6909f-156">"Configuration" プロパティの既定値は "Debug" であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="6909f-156">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="6909f-157">リリース構成に変更するには、を使用し `-Properties Configuration=Release` ます。</span><span class="sxs-lookup"><span data-stu-id="6909f-157">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="6909f-158">**一般に**、プロパティは、予期しない動作を避けるために、対応するプロジェクトのビルド中に使用されたものと同じである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6909f-158">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span> |
| <span data-ttu-id="6909f-159">サフィックス</span><span class="sxs-lookup"><span data-stu-id="6909f-159">Suffix</span></span> | <span data-ttu-id="6909f-160">*(3.4.4 +)* 内部で生成されたバージョン番号にサフィックスを追加します。通常は、ビルドまたはその他のプレリリース識別子を追加するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="6909f-160">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="6909f-161">たとえば、を使用すると、の `-suffix nightly` ようなバージョン番号のパッケージが作成され `1.2.3-nightly` ます。</span><span class="sxs-lookup"><span data-stu-id="6909f-161">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="6909f-162">サフィックスは、警告、エラー、およびさまざまなバージョンの NuGet と NuGet パッケージマネージャーとの互換性がない可能性を回避するために、英字で始める必要があります。</span><span class="sxs-lookup"><span data-stu-id="6909f-162">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="6909f-163">記号</span><span class="sxs-lookup"><span data-stu-id="6909f-163">Symbols</span></span> | <span data-ttu-id="6909f-164">パッケージにソースとシンボルが含まれていることを指定します。</span><span class="sxs-lookup"><span data-stu-id="6909f-164">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="6909f-165">ファイルと共に使用すると `.nuspec` 、通常の NuGet パッケージファイルと対応するシンボルパッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="6909f-165">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="6909f-166">既定では、[レガシシンボルパッケージ](../../create-packages/Symbol-Packages.md)が作成されます。</span><span class="sxs-lookup"><span data-stu-id="6909f-166">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="6909f-167">シンボル パッケージに推奨される新しい形式は .snupkg です。</span><span class="sxs-lookup"><span data-stu-id="6909f-167">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="6909f-168">「[シンボル パッケージ (.snupkg) の作成](../../create-packages/Symbol-Packages-snupkg.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6909f-168">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="6909f-169">ツール</span><span class="sxs-lookup"><span data-stu-id="6909f-169">Tool</span></span> | <span data-ttu-id="6909f-170">プロジェクトの出力ファイルをフォルダーに配置するように指定し `tool` ます。</span><span class="sxs-lookup"><span data-stu-id="6909f-170">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="6909f-171">詳細度</span><span class="sxs-lookup"><span data-stu-id="6909f-171">Verbosity</span></span> | <span data-ttu-id="6909f-172">出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。</span><span class="sxs-lookup"><span data-stu-id="6909f-172">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="6909f-173">バージョン</span><span class="sxs-lookup"><span data-stu-id="6909f-173">Version</span></span> | <span data-ttu-id="6909f-174">ファイルのバージョン番号をオーバーライドし `.nuspec` ます。</span><span class="sxs-lookup"><span data-stu-id="6909f-174">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="6909f-175">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="6909f-175">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="6909f-176">開発の依存関係の除外</span><span class="sxs-lookup"><span data-stu-id="6909f-176">Excluding development dependencies</span></span>

<span data-ttu-id="6909f-177">一部の NuGet パッケージは、独自のライブラリを作成するのに役立つ、開発の依存関係として役に立ちますが、実際のパッケージの依存関係としては必ずしも必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="6909f-177">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="6909f-178">コマンドは、 `pack` 属性がに設定されて `package` いるのエントリを無視し `packages.config` `developmentDependency` `true` ます。</span><span class="sxs-lookup"><span data-stu-id="6909f-178">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="6909f-179">これらのエントリは、作成されたパッケージに依存関係として含まれません。</span><span class="sxs-lookup"><span data-stu-id="6909f-179">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="6909f-180">たとえば、ソースプロジェクトの次のファイルについて考えてみ `packages.config` ます。</span><span class="sxs-lookup"><span data-stu-id="6909f-180">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="6909f-181">このプロジェクトでは、によって作成されたパッケージは `nuget pack` とに依存しますが、には依存関係があり `jQuery` `microsoft-web-helpers` ません `netfx-Guard` 。</span><span class="sxs-lookup"><span data-stu-id="6909f-181">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="6909f-182">非表示 (パックの警告を)</span><span class="sxs-lookup"><span data-stu-id="6909f-182">Suppressing pack warnings</span></span>

<span data-ttu-id="6909f-183">パック操作中にすべての NuGet 警告を解決することをお勧めしますが、特定の状況では、それらを抑制することが保証されます。</span><span class="sxs-lookup"><span data-stu-id="6909f-183">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="6909f-184">これは、次の方法で実現できます。</span><span class="sxs-lookup"><span data-stu-id="6909f-184">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="6909f-185">nuget.exe pack nuspec NoWarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="6909f-185">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="6909f-186">使用例</span><span class="sxs-lookup"><span data-stu-id="6909f-186">Examples</span></span>

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
