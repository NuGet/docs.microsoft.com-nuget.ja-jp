---
title: NuGet 用 .NET Compiler Platform のアナライザーの形式
description: API またはライブラリを実装する NuGet パッケージにパッケージ化され配布される、.NET アナライザーの規則です。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 9de890d14747a74a13a660109a3b6812a5e08acc
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237920"
---
# <a name="analyzer-nuget-formats"></a><span data-ttu-id="8241f-103">アナライザーの NuGet の形式</span><span class="sxs-lookup"><span data-stu-id="8241f-103">Analyzer NuGet formats</span></span>

<span data-ttu-id="8241f-104">("Roslyn" としても知られている) .NET Compiler Platform では、開発者がコードを記述する際に構文ツリーとセマンティクスが検証される[アナライザー](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)を作成できます。</span><span class="sxs-lookup"><span data-stu-id="8241f-104">The .NET Compiler Platform (also known as "Roslyn") allows developers to create [analyzers](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix) that examine the syntax tree and semantics of code as it's being written.</span></span> <span data-ttu-id="8241f-105">これにより、開発者は、特定の API またはライブラリの使用の助けとなるドメイン固有の分析ツールを作成できるようになります。</span><span class="sxs-lookup"><span data-stu-id="8241f-105">This provides developers with a way to create domain-specific analysis tools, such as those that would help guide the use of a particular API or library.</span></span> <span data-ttu-id="8241f-106">詳細については、[.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8241f-106">You can find more information on the [.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki.</span></span> <span data-ttu-id="8241f-107">MSDN マガジンの「[Roslyn を使用した API 向けライブ コード アナライザーの作成](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api)」の記事も参照してください。</span><span class="sxs-lookup"><span data-stu-id="8241f-107">Also see the article, [Use Roslyn to Write a Live Code Analyzer for your API](/archive/msdn-magazine/2014/special-issue/csharp-and-visual-basic-use-roslyn-to-write-a-live-code-analyzer-for-your-api) in MSDN Magazine.</span></span>

<span data-ttu-id="8241f-108">アナライザー自体は、通常、問題となっている API またはライブラリを実装する NuGet パッケージの一部としてパッケージ化され配布されています。</span><span class="sxs-lookup"><span data-stu-id="8241f-108">Analyzers themselves are typically packaged and distributed as part of the NuGet packages that implement the API or library in question.</span></span>

<span data-ttu-id="8241f-109">適切な例については、「[System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers)」パッケージを参照してください。内容は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8241f-109">For a good example, see the [System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers) package, which has the following contents:</span></span>

- <span data-ttu-id="8241f-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="8241f-110">analyzers\dotnet\System.Runtime.Analyzers.dll</span></span>
- <span data-ttu-id="8241f-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="8241f-111">analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll</span></span>
- <span data-ttu-id="8241f-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span><span class="sxs-lookup"><span data-stu-id="8241f-112">analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll</span></span>
- <span data-ttu-id="8241f-113">build\System.Runtime.Analyzers.Common.props</span><span class="sxs-lookup"><span data-stu-id="8241f-113">build\System.Runtime.Analyzers.Common.props</span></span>
- <span data-ttu-id="8241f-114">build\System.Runtime.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="8241f-114">build\System.Runtime.Analyzers.props</span></span>
- <span data-ttu-id="8241f-115">build\System.Runtime.CSharp.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="8241f-115">build\System.Runtime.CSharp.Analyzers.props</span></span>
- <span data-ttu-id="8241f-116">build\System.Runtime.VisualBasic.Analyzers.props</span><span class="sxs-lookup"><span data-stu-id="8241f-116">build\System.Runtime.VisualBasic.Analyzers.props</span></span>
- <span data-ttu-id="8241f-117">tools\install.ps1</span><span class="sxs-lookup"><span data-stu-id="8241f-117">tools\install.ps1</span></span>
- <span data-ttu-id="8241f-118">tools\uninstall.ps1</span><span class="sxs-lookup"><span data-stu-id="8241f-118">tools\uninstall.ps1</span></span>

<span data-ttu-id="8241f-119">ご確認できるとおり、アナライザーの DLL はパッケージの `analyzers` フォルダーに配置します。</span><span class="sxs-lookup"><span data-stu-id="8241f-119">As you can see, you place the analyzer DLLs into an `analyzers` folder in the package.</span></span>

<span data-ttu-id="8241f-120">アナライザーの実装を優先し、古い FxCop 規則を無効にするために含まれる props ファイルは、`build` フォルダーに配置します。</span><span class="sxs-lookup"><span data-stu-id="8241f-120">Props files, which are included to disable legacy FxCop rules in favor of the analyzer implementation, are placed in the `build` folder.</span></span>

<span data-ttu-id="8241f-121">`packages.config` を使用するプロジェクトをサポートするインストールおよびアンインストール スクリプトは、`tools` に配置します。</span><span class="sxs-lookup"><span data-stu-id="8241f-121">Install and uninstall scripts that support projects using `packages.config` are placed in `tools`.</span></span>

<span data-ttu-id="8241f-122">また、このパッケージには、プラットフォーム固有の要件がないため、`platform` フォルダーは省かれます。</span><span class="sxs-lookup"><span data-stu-id="8241f-122">Also note that because this package has no platform-specific requirements, the `platform` folder is omitted.</span></span>


## <a name="analyzers-path-format"></a><span data-ttu-id="8241f-123">アナライザーのパスの形式</span><span class="sxs-lookup"><span data-stu-id="8241f-123">Analyzers path format</span></span>

<span data-ttu-id="8241f-124">`analyzers` フォルダーの用途は、パスの指定子がビルド時間ではなく、開発ホストの依存関係であることを除き、[ターゲット フレームワーク](../create-packages/supporting-multiple-target-frameworks.md)で使用されるのと類似しています。</span><span class="sxs-lookup"><span data-stu-id="8241f-124">The use of the `analyzers` folder is similar to that used for [target frameworks](../create-packages/supporting-multiple-target-frameworks.md), except the specifiers in the path describe development host dependencies instead of build-time.</span></span> <span data-ttu-id="8241f-125">一般的な形式は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="8241f-125">The general format is as follows:</span></span>

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- <span data-ttu-id="8241f-126">**framework_name** および **version** : 含まれている DLL を実行する必要がある .NET Framework の " *省略可能な* " API サーフェス領域。</span><span class="sxs-lookup"><span data-stu-id="8241f-126">**framework_name** and **version** : the *optional* API surface area of the .NET Framework that the contained DLLs need to run.</span></span> <span data-ttu-id="8241f-127">Roslyn がアナライザーを実行できる唯一のホストであるため、`dotnet` は、現在唯一の有効な値です。</span><span class="sxs-lookup"><span data-stu-id="8241f-127">`dotnet` is presently the only valid value because Roslyn is the only host that can run analyzers.</span></span> <span data-ttu-id="8241f-128">ターゲットを指定しない場合、DLL は *すべて* のターゲットに適用されると見なされます。</span><span class="sxs-lookup"><span data-stu-id="8241f-128">If no target is specified, DLLs are assumed to apply to *all* targets.</span></span>
- <span data-ttu-id="8241f-129">**supported_language** : `cs` (C#)、`vb` (Visual Basic)、および `fs` (F#) の DLL のいずれかの言語です。</span><span class="sxs-lookup"><span data-stu-id="8241f-129">**supported_language** : the language for which the DLL applies, one of `cs` (C#) and `vb` (Visual Basic), and `fs` (F#).</span></span> <span data-ttu-id="8241f-130">この言語は、その言語を使用するプロジェクトに対してのみ、アナライザーが読み込まれる必要があることを示します。</span><span class="sxs-lookup"><span data-stu-id="8241f-130">The language indicates that the analyzer should be loaded only for a project using that language.</span></span> <span data-ttu-id="8241f-131">言語を指定しない場合、DLL はアナライザーでサポートされる " *すべて* " の言語に適用されると想定されます。</span><span class="sxs-lookup"><span data-stu-id="8241f-131">If no language is specified then the DLL is assumed to apply to *all* languages that support analyzers.</span></span>
- <span data-ttu-id="8241f-132">**analyzer_name** : アナライザーの DLL を指定します。</span><span class="sxs-lookup"><span data-stu-id="8241f-132">**analyzer_name** : specifies the DLLs of the analyzer.</span></span> <span data-ttu-id="8241f-133">DLL 以外にもファイルが必要な場合は、ターゲットまたはプロパティ ファイルを介して含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="8241f-133">If you need additional files beyond DLLs, they must be included through a targets or properties files.</span></span>


## <a name="install-and-uninstall-scripts"></a><span data-ttu-id="8241f-134">インストールおよびアンインストール スクリプト</span><span class="sxs-lookup"><span data-stu-id="8241f-134">Install and uninstall scripts</span></span>

<span data-ttu-id="8241f-135">ユーザーのプロジェクトで `packages.config` が使用される場合、アナライザーを取得する MSBuild スクリプトが動作しないため、以下に示すコンテンツを含む `install.ps1` と `uninstall.ps1` を `tools` フォルダーに配置する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8241f-135">If the user's project is using `packages.config`, the MSBuild script that picks up the analyzer does not come into play, so you should place `install.ps1` and `uninstall.ps1` in the `tools` folder with the contents that are described below.</span></span>

<span data-ttu-id="8241f-136">**install.ps1 ファイルの内容**</span><span class="sxs-lookup"><span data-stu-id="8241f-136">**install.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Install the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Install language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Add($analyzerFilePath.FullName)
            }
        }
    }
}
```


<span data-ttu-id="8241f-137">**uninstall.ps1 ファイルの内容**</span><span class="sxs-lookup"><span data-stu-id="8241f-137">**uninstall.ps1 file contents**</span></span>

```ps
param($installPath, $toolsPath, $package, $project)

$analyzersPaths = Join-Path (Join-Path (Split-Path -Path $toolsPath -Parent) "analyzers" ) * -Resolve

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall the language agnostic analyzers.
    if (Test-Path $analyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $analyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
            }
        }
    }
}

$project.Type # gives the language name like (C# or VB.NET)
$languageFolder = ""
if($project.Type -eq "C#")
{
    $languageFolder = "cs"
}
if($project.Type -eq "VB.NET")
{
    $languageFolder = "vb"
}
if($languageFolder -eq "")
{
    return
}

foreach($analyzersPath in $analyzersPaths)
{
    # Uninstall language specific analyzers.
    $languageAnalyzersPath = join-path $analyzersPath $languageFolder
    if (Test-Path $languageAnalyzersPath)
    {
        foreach ($analyzerFilePath in Get-ChildItem $languageAnalyzersPath -Filter *.dll)
        {
            if($project.Object.AnalyzerReferences)
            {
                try
                {
                    $project.Object.AnalyzerReferences.Remove($analyzerFilePath.FullName)
                }
                catch
                {

                }
            }
        }
    }
}
```