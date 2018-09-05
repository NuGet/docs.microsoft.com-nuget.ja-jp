---
title: NuGet CLI pack コマンド
description: Nuget.exe パック コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: db236b0eaac34ca9f6f67fd15ca3ad6884f6a18d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549097"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="78152-103">pack コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="78152-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="78152-104">**適用対象:** パッケージの作成&bullet;**サポートされているバージョン:** 2.7 以降</span><span class="sxs-lookup"><span data-stu-id="78152-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="78152-105">に基づいて、指定された NuGet パッケージを作成します。`.nuspec`またはプロジェクト ファイル。</span><span class="sxs-lookup"><span data-stu-id="78152-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="78152-106">`dotnet pack`コマンド (を参照してください[dotnet コマンド](dotnet-Commands.md)) と`msbuild /t:pack`(を参照してください[MSBuild ターゲット](../reference/msbuild-targets.md)) の代替として使用することがあります。</span><span class="sxs-lookup"><span data-stu-id="78152-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="78152-107">Mono で、プロジェクト ファイルからパッケージを作成することはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="78152-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="78152-108">非ローカル パスを調整する必要があります、 `.nuspec` Unix 形式のパスにファイルの nuget.exe が Windows パス名自体を変換しません。</span><span class="sxs-lookup"><span data-stu-id="78152-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="78152-109">使用法</span><span class="sxs-lookup"><span data-stu-id="78152-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="78152-110">場所`<nuspecPath>`と`<projectPath>`指定、`.nuspec`またはプロジェクト ファイルをそれぞれします。</span><span class="sxs-lookup"><span data-stu-id="78152-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="78152-111">オプション</span><span class="sxs-lookup"><span data-stu-id="78152-111">Options</span></span>

| <span data-ttu-id="78152-112">オプション</span><span class="sxs-lookup"><span data-stu-id="78152-112">Option</span></span> | <span data-ttu-id="78152-113">説明</span><span class="sxs-lookup"><span data-stu-id="78152-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78152-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="78152-114">BasePath</span></span> | <span data-ttu-id="78152-115">定義されているファイルの基本パスを設定、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="78152-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="78152-116">ビルド</span><span class="sxs-lookup"><span data-stu-id="78152-116">Build</span></span> | <span data-ttu-id="78152-117">パッケージを構築する前に、プロジェクトをビルドすることを指定します。</span><span class="sxs-lookup"><span data-stu-id="78152-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="78152-118">除外</span><span class="sxs-lookup"><span data-stu-id="78152-118">Exclude</span></span> | <span data-ttu-id="78152-119">パッケージを作成するときに除外する 1 つまたは複数のワイルドカード パターンを指定します。</span><span class="sxs-lookup"><span data-stu-id="78152-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="78152-120">1 つ以上のパターンを指定するには、繰り返し除外するフラグ。</span><span class="sxs-lookup"><span data-stu-id="78152-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="78152-121">次の例を参照してください。</span><span class="sxs-lookup"><span data-stu-id="78152-121">See example below.</span></span> |
| <span data-ttu-id="78152-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="78152-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="78152-123">パッケージを作成するときに、空のディレクトリを含めることをできないようにします。</span><span class="sxs-lookup"><span data-stu-id="78152-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="78152-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="78152-124">ForceEnglishOutput</span></span> | <span data-ttu-id="78152-125">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="78152-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="78152-126">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="78152-126">Help</span></span> | <span data-ttu-id="78152-127">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="78152-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="78152-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="78152-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="78152-129">依存関係として、または、パッケージの一部として、ビルドされたパッケージに参照されるプロジェクトを含める必要がありますを示します。</span><span class="sxs-lookup"><span data-stu-id="78152-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="78152-130">参照先プロジェクトが、対応する`.nuspec`をその参照先プロジェクトが依存関係として追加し、プロジェクトと同じ名前を持つファイル。</span><span class="sxs-lookup"><span data-stu-id="78152-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="78152-131">それ以外の場合、参照先のプロジェクトは、パッケージの一部として追加されます。</span><span class="sxs-lookup"><span data-stu-id="78152-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="78152-132">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="78152-132">MinClientVersion</span></span> | <span data-ttu-id="78152-133">設定、 *minClientVersion*作成したパッケージの属性。</span><span class="sxs-lookup"><span data-stu-id="78152-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="78152-134">この値は、既存の値をオーバーライド*minClientVersion* (あれば) 属性、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="78152-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="78152-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="78152-135">MSBuildPath</span></span> | <span data-ttu-id="78152-136">*(4.0 以降)* よりも優先、コマンドで使用する MSBuild のパスを示す`-MSBuildVersion`します。</span><span class="sxs-lookup"><span data-stu-id="78152-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="78152-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="78152-137">MSBuildVersion</span></span> | <span data-ttu-id="78152-138">*(3.2 以降)* このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="78152-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="78152-139">サポートされている値は、4、12、14、15 です。</span><span class="sxs-lookup"><span data-stu-id="78152-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="78152-140">パスに MSBuild が取得される、既定でそれ以外の場合、既定値 MSBuild の最上位のインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="78152-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="78152-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="78152-141">NoDefaultExcludes</span></span> | <span data-ttu-id="78152-142">NuGet の既定の除外をできないようにファイルとフォルダーなど、ドットで始まるファイルをパッケージ化`.svn`と`.gitignore`します。</span><span class="sxs-lookup"><span data-stu-id="78152-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="78152-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="78152-143">NoPackageAnalysis</span></span> | <span data-ttu-id="78152-144">パッケージのビルド後に、パックでパッケージの分析を実行しないことを指定します。</span><span class="sxs-lookup"><span data-stu-id="78152-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="78152-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="78152-145">OutputDirectory</span></span> | <span data-ttu-id="78152-146">作成したパッケージが格納されているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="78152-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="78152-147">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="78152-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="78152-148">プロパティ</span><span class="sxs-lookup"><span data-stu-id="78152-148">Properties</span></span> | <span data-ttu-id="78152-149">その他のオプションの後に、コマンドラインの最後は表示されます。</span><span class="sxs-lookup"><span data-stu-id="78152-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="78152-150">は、プロジェクト ファイル内の値をオーバーライドするプロパティの一覧を指定します参照してください[MSBuild プロジェクトの共通プロパティ](/visualstudio/msbuild/common-msbuild-project-properties)プロパティ名。</span><span class="sxs-lookup"><span data-stu-id="78152-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="78152-151">プロパティの引数をここでは、トークンのリスト = 値のペアをセミコロンで区切った、出現するたび`$token$`で、`.nuspec`ファイルが指定した値と置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="78152-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="78152-152">値は引用符で囲まれた文字列を指定できます。</span><span class="sxs-lookup"><span data-stu-id="78152-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="78152-153">「構成」プロパティの既定値は"Debug"に注意してください。</span><span class="sxs-lookup"><span data-stu-id="78152-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="78152-154">リリース構成を変更するには、使用`-Properties Configuration=Release`します。</span><span class="sxs-lookup"><span data-stu-id="78152-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="78152-155">サフィックス</span><span class="sxs-lookup"><span data-stu-id="78152-155">Suffix</span></span> | <span data-ttu-id="78152-156">*(3.4.4+)* 内部的に生成されたバージョン番号、ビルドまたはその他のプレリリース版の識別子を追加するために通常使用するサフィックスを追加します。</span><span class="sxs-lookup"><span data-stu-id="78152-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="78152-157">たとえばを使用して`-suffix nightly`などの数字のバージョンでパッケージを作成`1.2.3-nightly`です。</span><span class="sxs-lookup"><span data-stu-id="78152-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="78152-158">サフィックスは、警告、エラー、およびさまざまなバージョンの NuGet、NuGet パッケージ マネージャーの潜在的な非互換性を回避するために文字で始まる必要があります。</span><span class="sxs-lookup"><span data-stu-id="78152-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="78152-159">シンボル</span><span class="sxs-lookup"><span data-stu-id="78152-159">Symbols</span></span> | <span data-ttu-id="78152-160">ソースとシンボル パッケージに含まれることを指定します。</span><span class="sxs-lookup"><span data-stu-id="78152-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="78152-161">使用すると、`.nuspec`正規の NuGet パッケージ ファイルが作成されますファイル、および対応するシンボル パッケージ。</span><span class="sxs-lookup"><span data-stu-id="78152-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="78152-162">ツール</span><span class="sxs-lookup"><span data-stu-id="78152-162">Tool</span></span> | <span data-ttu-id="78152-163">プロジェクトの出力ファイルが配置されることを指定します、`tool`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="78152-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="78152-164">詳細度</span><span class="sxs-lookup"><span data-stu-id="78152-164">Verbosity</span></span> | <span data-ttu-id="78152-165">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="78152-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="78152-166">Version</span><span class="sxs-lookup"><span data-stu-id="78152-166">Version</span></span> | <span data-ttu-id="78152-167">バージョン番号をオーバーライド、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="78152-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="78152-168">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="78152-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="78152-169">開発の依存関係を除外</span><span class="sxs-lookup"><span data-stu-id="78152-169">Excluding development dependencies</span></span>

<span data-ttu-id="78152-170">NuGet パッケージの一部は、独自のライブラリを作成できますが、実際のパッケージの依存関係としては必ずしも必要ありません開発依存関係として役立ちます。</span><span class="sxs-lookup"><span data-stu-id="78152-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="78152-171">`pack`コマンドは無視されます`package`エントリ`packages.config`がある、`developmentDependency`属性に設定`true`します。</span><span class="sxs-lookup"><span data-stu-id="78152-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="78152-172">これらのエントリは、作成したパッケージの依存関係として含まれません。</span><span class="sxs-lookup"><span data-stu-id="78152-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="78152-173">たとえば、次`packages.config`ソース プロジェクト ファイル。</span><span class="sxs-lookup"><span data-stu-id="78152-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="78152-174">このプロジェクトでパッケージを作成して`nuget pack`依存関係になります`jQuery`と`microsoft-web-helpers`なく`netfx-Guard`します。</span><span class="sxs-lookup"><span data-stu-id="78152-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="78152-175">使用例</span><span class="sxs-lookup"><span data-stu-id="78152-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
