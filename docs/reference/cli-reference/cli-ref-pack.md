---
title: NuGet CLI パックコマンド
description: Nuget.exe pack コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e12944bdd5d43b8b9e84908be480a5249dd924f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327659"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="a9316-103">pack コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a9316-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="a9316-104">**適用対象:** パッケージ作成&bullet;で**サポートされているバージョン:** 2.7+</span><span class="sxs-lookup"><span data-stu-id="a9316-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="a9316-105">指定された`.nuspec`またはプロジェクトファイルに基づいて NuGet パッケージを作成します。</span><span class="sxs-lookup"><span data-stu-id="a9316-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="a9316-106">コマンド`dotnet pack` (「 [dotnet コマンド](../dotnet-Commands.md)」を参照`msbuild -t:pack` ) と (「 [MSBuild ターゲット](../msbuild-targets.md)」を参照) は、代替として使用できます。</span><span class="sxs-lookup"><span data-stu-id="a9316-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="a9316-107">Mono では、プロジェクトファイルからパッケージを作成することはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="a9316-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="a9316-108">また、nuget.exe によって Windows のパス名自体`.nuspec`が変換されないため、ファイル内のローカルではないパスを Unix 形式のパスに調整する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a9316-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="a9316-109">使用法</span><span class="sxs-lookup"><span data-stu-id="a9316-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="a9316-110">`<nuspecPath>` `.nuspec`とは、それぞれまたはプロジェクトファイルを指定します。`<projectPath>`</span><span class="sxs-lookup"><span data-stu-id="a9316-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="a9316-111">オプション</span><span class="sxs-lookup"><span data-stu-id="a9316-111">Options</span></span>

| <span data-ttu-id="a9316-112">オプション</span><span class="sxs-lookup"><span data-stu-id="a9316-112">Option</span></span> | <span data-ttu-id="a9316-113">説明</span><span class="sxs-lookup"><span data-stu-id="a9316-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a9316-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="a9316-114">BasePath</span></span> | <span data-ttu-id="a9316-115">`.nuspec`ファイルで定義されているファイルのベースパスを設定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="a9316-116">Build</span><span class="sxs-lookup"><span data-stu-id="a9316-116">Build</span></span> | <span data-ttu-id="a9316-117">パッケージをビルドする前にプロジェクトをビルドするように指定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="a9316-118">Exclude</span><span class="sxs-lookup"><span data-stu-id="a9316-118">Exclude</span></span> | <span data-ttu-id="a9316-119">パッケージの作成時に除外する1つ以上のワイルドカードパターンを指定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="a9316-120">複数のパターンを指定するには、-Exclude フラグを繰り返します。</span><span class="sxs-lookup"><span data-stu-id="a9316-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="a9316-121">次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a9316-121">See example below.</span></span> |
| <span data-ttu-id="a9316-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="a9316-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="a9316-123">パッケージをビルドするときに空のディレクトリを含めないようにします。</span><span class="sxs-lookup"><span data-stu-id="a9316-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="a9316-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a9316-124">ForceEnglishOutput</span></span> | <span data-ttu-id="a9316-125">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="a9316-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a9316-126">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a9316-126">ConfigFile</span></span> | <span data-ttu-id="a9316-127">パックコマンドの構成ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-127">Specify the configuration file for the pack command.</span></span> |
| <span data-ttu-id="a9316-128">Help</span><span class="sxs-lookup"><span data-stu-id="a9316-128">Help</span></span> | <span data-ttu-id="a9316-129">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="a9316-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="a9316-130">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="a9316-130">IncludeReferencedProjects</span></span> | <span data-ttu-id="a9316-131">ビルドされたパッケージに、依存関係として、またはパッケージの一部として参照プロジェクトを含める必要があることを示します。</span><span class="sxs-lookup"><span data-stu-id="a9316-131">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="a9316-132">参照先のプロジェクトに、プロジェクト`.nuspec`と同じ名前の対応するファイルがある場合、その参照先プロジェクトは依存関係として追加されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-132">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="a9316-133">それ以外の場合、参照されるプロジェクトはパッケージの一部として追加されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-133">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="a9316-134">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="a9316-134">MinClientVersion</span></span> | <span data-ttu-id="a9316-135">作成したパッケージの*minClientVersion*属性を設定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-135">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="a9316-136">この値は、 `.nuspec`ファイル内の既存の*minClientVersion*属性 (存在する場合) の値よりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-136">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="a9316-137">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="a9316-137">MSBuildPath</span></span> | <span data-ttu-id="a9316-138">*(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これは`-MSBuildVersion`よりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-138">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="a9316-139">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="a9316-139">MSBuildVersion</span></span> | <span data-ttu-id="a9316-140">*(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-140">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="a9316-141">サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。</span><span class="sxs-lookup"><span data-stu-id="a9316-141">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="a9316-142">既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。</span><span class="sxs-lookup"><span data-stu-id="a9316-142">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="a9316-143">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="a9316-143">NoDefaultExcludes</span></span> | <span data-ttu-id="a9316-144">`.svn` や`.gitignore`など、ドットで始まる NuGet パッケージファイルとファイルおよびフォルダーの既定の除外を回避します。</span><span class="sxs-lookup"><span data-stu-id="a9316-144">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="a9316-145">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="a9316-145">NoPackageAnalysis</span></span> | <span data-ttu-id="a9316-146">パッケージのビルド後に、パックでパッケージの分析を実行しないことを指定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-146">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="a9316-147">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="a9316-147">OutputDirectory</span></span> | <span data-ttu-id="a9316-148">作成したパッケージが格納されているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-148">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="a9316-149">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-149">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="a9316-150">Properties</span><span class="sxs-lookup"><span data-stu-id="a9316-150">Properties</span></span> | <span data-ttu-id="a9316-151">他のオプションの後に、コマンドラインに最後に表示されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-151">Should appear last on the command line after other options.</span></span> <span data-ttu-id="a9316-152">プロジェクトファイルの値をオーバーライドするプロパティの一覧を指定します。「プロパティ名の[一般的な MSBuild プロジェクトプロパティ](/visualstudio/msbuild/common-msbuild-project-properties)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a9316-152">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="a9316-153">ここでのプロパティ引数は、トークン = 値のペアの一覧です。セミコロンで区切られて`$token$`います`.nuspec` 。ファイル内での各出現箇所は、指定された値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="a9316-153">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="a9316-154">値は、引用符で囲まれた文字列にすることができます。</span><span class="sxs-lookup"><span data-stu-id="a9316-154">Values can be strings in quotation marks.</span></span> <span data-ttu-id="a9316-155">"Configuration" プロパティの既定値は "Debug" であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a9316-155">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="a9316-156">リリース構成に変更するには、 `-Properties Configuration=Release`を使用します。</span><span class="sxs-lookup"><span data-stu-id="a9316-156">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="a9316-157">Suffix</span><span class="sxs-lookup"><span data-stu-id="a9316-157">Suffix</span></span> | <span data-ttu-id="a9316-158">*(3.4.4 +)* 内部で生成されたバージョン番号にサフィックスを追加します。通常は、ビルドまたはその他のプレリリース識別子を追加するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-158">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="a9316-159">たとえば、を使用`-suffix nightly`すると、のような`1.2.3-nightly`バージョン番号のパッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-159">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="a9316-160">サフィックスは、警告、エラー、およびさまざまなバージョンの NuGet と NuGet パッケージマネージャーとの互換性がない可能性を回避するために、英字で始める必要があります。</span><span class="sxs-lookup"><span data-stu-id="a9316-160">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="a9316-161">Symbols</span><span class="sxs-lookup"><span data-stu-id="a9316-161">Symbols</span></span> | <span data-ttu-id="a9316-162">パッケージにソースとシンボルが含まれていることを指定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-162">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="a9316-163">`.nuspec`ファイルと共に使用すると、通常の NuGet パッケージファイルと対応するシンボルパッケージが作成されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-163">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="a9316-164">既定では、[レガシシンボルパッケージ](../../create-packages/Symbol-Packages.md)が作成されます。</span><span class="sxs-lookup"><span data-stu-id="a9316-164">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="a9316-165">シンボル パッケージに推奨される新しい形式は .snupkg です。</span><span class="sxs-lookup"><span data-stu-id="a9316-165">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="a9316-166">「[シンボル パッケージ (.snupkg) の作成](../../create-packages/Symbol-Packages-snupkg.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a9316-166">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span> |
| <span data-ttu-id="a9316-167">Tool</span><span class="sxs-lookup"><span data-stu-id="a9316-167">Tool</span></span> | <span data-ttu-id="a9316-168">プロジェクトの出力ファイルを`tool`フォルダーに配置するように指定します。</span><span class="sxs-lookup"><span data-stu-id="a9316-168">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="a9316-169">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a9316-169">Verbosity</span></span> | <span data-ttu-id="a9316-170">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="a9316-170">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="a9316-171">Version</span><span class="sxs-lookup"><span data-stu-id="a9316-171">Version</span></span> | <span data-ttu-id="a9316-172">`.nuspec`ファイルのバージョン番号をオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="a9316-172">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="a9316-173">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="a9316-173">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="a9316-174">開発の依存関係の除外</span><span class="sxs-lookup"><span data-stu-id="a9316-174">Excluding development dependencies</span></span>

<span data-ttu-id="a9316-175">一部の NuGet パッケージは、独自のライブラリを作成するのに役立つ、開発の依存関係として役に立ちますが、実際のパッケージの依存関係としては必ずしも必要ではありません。</span><span class="sxs-lookup"><span data-stu-id="a9316-175">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="a9316-176">`package` コマンドは`packages.config` 、 `developmentDependency`属性がに`true`設定されているのエントリを無視します。 `pack`</span><span class="sxs-lookup"><span data-stu-id="a9316-176">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="a9316-177">これらのエントリは、作成されたパッケージに依存関係として含まれません。</span><span class="sxs-lookup"><span data-stu-id="a9316-177">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="a9316-178">たとえば、ソースプロジェクトの次`packages.config`のファイルについて考えてみます。</span><span class="sxs-lookup"><span data-stu-id="a9316-178">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="a9316-179">このプロジェクトでは、によって`nuget pack`作成されたパッケージ`jQuery`は`microsoft-web-helpers`とに`netfx-Guard`依存しますが、には依存関係がありません。</span><span class="sxs-lookup"><span data-stu-id="a9316-179">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="a9316-180">使用例</span><span class="sxs-lookup"><span data-stu-id="a9316-180">Examples</span></span>

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
