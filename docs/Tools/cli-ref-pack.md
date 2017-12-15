---
title: "NuGet CLI パック コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Nuget.exe パック コマンドのリファレンス"
keywords: "nuget パックの参照、パック コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 353d5d839d85c04bc315c3a0e9cfe274a361bd15
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="8d565-104">パック コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8d565-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="8d565-105">**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="8d565-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="8d565-106">に基づいて、指定された NuGet パッケージを作成`.nuspec`またはプロジェクト ファイルです。</span><span class="sxs-lookup"><span data-stu-id="8d565-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="8d565-107">`dotnet pack`コマンド (を参照してください[dotnet コマンド](dotnet-Commands.md)) および`msbuild /t:pack`(を参照してください[MSBuild ターゲット](../schema/msbuild-targets.md)) の代替として使用することがあります。</span><span class="sxs-lookup"><span data-stu-id="8d565-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="8d565-108">Mono で、プロジェクト ファイルからパッケージを作成することはサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="8d565-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="8d565-109">内の非ローカル パスを調整する必要があります、 `.nuspec` nuget.exe しない Windows のパス名自体を変換するために、Unix 形式のパスにファイルします。</span><span class="sxs-lookup"><span data-stu-id="8d565-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="8d565-110">使用方法</span><span class="sxs-lookup"><span data-stu-id="8d565-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="8d565-111">ここで`<nuspecPath>`と`<projectPath>`指定、`.nuspec`またはプロジェクト ファイル、それぞれします。</span><span class="sxs-lookup"><span data-stu-id="8d565-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="8d565-112">オプション</span><span class="sxs-lookup"><span data-stu-id="8d565-112">Options</span></span>

| <span data-ttu-id="8d565-113">オプション</span><span class="sxs-lookup"><span data-stu-id="8d565-113">Option</span></span> | <span data-ttu-id="8d565-114">説明</span><span class="sxs-lookup"><span data-stu-id="8d565-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8d565-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="8d565-115">BasePath</span></span> | <span data-ttu-id="8d565-116">定義されているファイルのベース パスを設定、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="8d565-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="8d565-117">ビルド</span><span class="sxs-lookup"><span data-stu-id="8d565-117">Build</span></span> | <span data-ttu-id="8d565-118">パッケージを構築する前に、プロジェクトをビルドすることを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d565-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="8d565-119">除外</span><span class="sxs-lookup"><span data-stu-id="8d565-119">Exclude</span></span> | <span data-ttu-id="8d565-120">パッケージを作成するときに除外する 1 つまたは複数のワイルドカード パターンを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d565-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> |
| <span data-ttu-id="8d565-121">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="8d565-121">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="8d565-122">パッケージを作成するときに、空のディレクトリを含めることを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="8d565-122">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="8d565-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8d565-123">ForceEnglishOutput</span></span> | <span data-ttu-id="8d565-124">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="8d565-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8d565-125">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="8d565-125">Help</span></span> | <span data-ttu-id="8d565-126">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="8d565-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="8d565-127">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="8d565-127">IncludeReferencedProjects</span></span> | <span data-ttu-id="8d565-128">依存関係として、またはパッケージの一部として、ビルド、パッケージに参照先のプロジェクトを含める必要がありますを示します。</span><span class="sxs-lookup"><span data-stu-id="8d565-128">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="8d565-129">参照先プロジェクトに対応する`.nuspec`をその参照先プロジェクトが、依存関係として追加し、プロジェクトと同じ名前を持つファイルです。</span><span class="sxs-lookup"><span data-stu-id="8d565-129">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="8d565-130">それ以外の場合、参照先プロジェクトは、パッケージの一部として追加されます。</span><span class="sxs-lookup"><span data-stu-id="8d565-130">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="8d565-131">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="8d565-131">MinClientVersion</span></span> | <span data-ttu-id="8d565-132">設定、 *minClientVersion*作成されたパッケージの属性です。</span><span class="sxs-lookup"><span data-stu-id="8d565-132">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="8d565-133">この値は、既存の値をオーバーライド*minClientVersion*で属性 (該当する場合)、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="8d565-133">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="8d565-134">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="8d565-134">MSBuildPath</span></span> | <span data-ttu-id="8d565-135">*(4.0 以降)*よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。</span><span class="sxs-lookup"><span data-stu-id="8d565-135">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="8d565-136">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="8d565-136">MSBuildVersion</span></span> | <span data-ttu-id="8d565-137">*(3.2 +)*このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d565-137">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="8d565-138">サポートされている値は、4、12、14、15 です。</span><span class="sxs-lookup"><span data-stu-id="8d565-138">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="8d565-139">既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="8d565-139">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="8d565-140">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="8d565-140">NoDefaultExcludes</span></span> | <span data-ttu-id="8d565-141">により、NuGet の既定の除外ファイルおよびファイルとフォルダーには、ピリオドなどの開始をパッケージ化`.svn`と`.gitignore`です。</span><span class="sxs-lookup"><span data-stu-id="8d565-141">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="8d565-142">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="8d565-142">NoPackageAnalysis</span></span> | <span data-ttu-id="8d565-143">パッケージのビルド後に、パックでパッケージの分析を実行しないことを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d565-143">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="8d565-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="8d565-144">OutputDirectory</span></span> | <span data-ttu-id="8d565-145">作成されたパッケージが格納されているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d565-145">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="8d565-146">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="8d565-146">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="8d565-147">プロパティ</span><span class="sxs-lookup"><span data-stu-id="8d565-147">Properties</span></span> | <span data-ttu-id="8d565-148">プロジェクト ファイル内の値をオーバーライドするプロパティの一覧を指定します参照してください[MSBuild プロジェクトの共通プロパティ](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties)プロパティ名にします。</span><span class="sxs-lookup"><span data-stu-id="8d565-148">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="8d565-149">プロパティ引数をここでは、トークンのリスト = 値のペアをセミコロンで区切られた場所のたびに`$token$`で、`.nuspec`ファイルは指定した値に置き換えられます。</span><span class="sxs-lookup"><span data-stu-id="8d565-149">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="8d565-150">値は、引用符で囲まれた文字列にすることができます。</span><span class="sxs-lookup"><span data-stu-id="8d565-150">Values can be strings in quotation marks.</span></span> <span data-ttu-id="8d565-151">"Configuration"プロパティの既定値がある"Debug"に注意してください。</span><span class="sxs-lookup"><span data-stu-id="8d565-151">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="8d565-152">リリース構成を変更するには、使用`-Properties Configuration=Release`です。</span><span class="sxs-lookup"><span data-stu-id="8d565-152">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="8d565-153">サフィックス</span><span class="sxs-lookup"><span data-stu-id="8d565-153">Suffix</span></span> | <span data-ttu-id="8d565-154">*(3.4.4+)*内部的に生成されたバージョン番号、ビルドまたはその他のプレリリース版の識別子を追加するために使用される通常にサフィックスを追加します。</span><span class="sxs-lookup"><span data-stu-id="8d565-154">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="8d565-155">たとえばを使用して`-suffix nightly`バージョン番号 like でパッケージを作成`1.2.3-nightly`です。</span><span class="sxs-lookup"><span data-stu-id="8d565-155">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="8d565-156">サフィックスは、警告、エラー、およびさまざまなバージョンの NuGet と NuGet パッケージ マネージャーの潜在的な非互換性を回避するのには文字で始める必要があります。</span><span class="sxs-lookup"><span data-stu-id="8d565-156">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="8d565-157">シンボル</span><span class="sxs-lookup"><span data-stu-id="8d565-157">Symbols</span></span> | <span data-ttu-id="8d565-158">パッケージには、ソースとシンボルが含まれているを指定します。</span><span class="sxs-lookup"><span data-stu-id="8d565-158">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="8d565-159">使用すると、`.nuspec`ファイル、通常の NuGet パッケージ ファイルが作成され、対応するシンボル パッケージです。</span><span class="sxs-lookup"><span data-stu-id="8d565-159">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="8d565-160">ツール</span><span class="sxs-lookup"><span data-stu-id="8d565-160">Tool</span></span> | <span data-ttu-id="8d565-161">プロジェクトの出力ファイルを配置する必要がありますを指定します、`tool`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="8d565-161">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="8d565-162">詳細度</span><span class="sxs-lookup"><span data-stu-id="8d565-162">Verbosity</span></span> | <span data-ttu-id="8d565-163">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="8d565-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="8d565-164">Version</span><span class="sxs-lookup"><span data-stu-id="8d565-164">Version</span></span> | <span data-ttu-id="8d565-165">バージョン番号よりも優先、`.nuspec`ファイル。</span><span class="sxs-lookup"><span data-stu-id="8d565-165">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="8d565-166">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8d565-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="8d565-167">開発の依存関係を除外</span><span class="sxs-lookup"><span data-stu-id="8d565-167">Excluding development dependencies</span></span>

<span data-ttu-id="8d565-168">一部の NuGet パッケージは、独自のライブラリを作成できますが、必ずしも実際のパッケージの依存関係として必要のない開発依存関係として役立ちます。</span><span class="sxs-lookup"><span data-stu-id="8d565-168">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="8d565-169">`pack`コマンドは無視されます`package`エントリ`packages.config`がある、`developmentDependency`属性に設定`true`です。</span><span class="sxs-lookup"><span data-stu-id="8d565-169">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="8d565-170">これらのエントリは、作成されたパッケージ内の依存関係としては含まれません。</span><span class="sxs-lookup"><span data-stu-id="8d565-170">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="8d565-171">たとえば、次`packages.config`ソース プロジェクト ファイル。</span><span class="sxs-lookup"><span data-stu-id="8d565-171">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="8d565-172">このプロジェクトのパッケージを作成して`nuget pack`依存関係を持つ`jQuery`と`microsoft-web-helpers`ではなく`netfx-Guard`です。</span><span class="sxs-lookup"><span data-stu-id="8d565-172">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="8d565-173">例</span><span class="sxs-lookup"><span data-stu-id="8d565-173">Examples</span></span>

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5
```
