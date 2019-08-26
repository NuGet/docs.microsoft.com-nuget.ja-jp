---
title: NuGet 用 .NET Compiler Platform のアナライザーの形式
description: API またはライブラリを実装する NuGet パッケージにパッケージ化され配布される、.NET アナライザーの規則です。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 0a8db9f6c55b7e79f9b338119e0b3ac6cb7a1e35
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69520512"
---
# <a name="analyzer-nuget-formats"></a>アナライザーの NuGet の形式

("Roslyn" としても知られている) .NET Compiler Platform では、開発者がコードを記述する際に構文ツリーとセマンティクスが検証される[アナライザー](https://github.com/dotnet/roslyn/wiki/How-To-Write-a-C%23-Analyzer-and-Code-Fix)を作成できます。 これにより、開発者は、特定の API またはライブラリの使用の助けとなるドメイン固有の分析ツールを作成できるようになります。 詳細については、[.NET/Roslyn](https://github.com/dotnet/roslyn/wiki) GitHub wiki を参照してください。 MSDN マガジンの「[Roslyn を使用した API 向けライブ コード アナライザーの作成](https://msdn.microsoft.com/magazine/dn879356.aspx)」の記事も参照してください。

アナライザー自体は、通常、問題となっている API またはライブラリを実装する NuGet パッケージの一部としてパッケージ化され配布されています。

適切な例については、「[System.Runtime.Analyzers](https://www.nuget.org/packages/System.Runtime.Analyzers)」パッケージを参照してください。内容は次のとおりです。

- analyzers\dotnet\System.Runtime.Analyzers.dll
- analyzers\dotnet\cs\System.Runtime.CSharp.Analyzers.dll
- analyzers\dotnet\vb\System.Runtime.VisualBasic.Analyzers.dll
- build\System.Runtime.Analyzers.Common.props
- build\System.Runtime.Analyzers.props
- build\System.Runtime.CSharp.Analyzers.props
- build\System.Runtime.VisualBasic.Analyzers.props
- tools\install.ps1
- tools\uninstall.ps1

ご確認できるとおり、アナライザーの DLL はパッケージの `analyzers` フォルダーに配置します。

アナライザーの実装を優先し、古い FxCop 規則を無効にするために含まれる props ファイルは、`build` フォルダーに配置します。

`packages.config` を使用するプロジェクトをサポートするインストールおよびアンインストール スクリプトは、`tools` に配置します。

また、このパッケージには、プラットフォーム固有の要件がないため、`platform` フォルダーは省かれます。


## <a name="analyzers-path-format"></a>アナライザーのパスの形式

`analyzers` フォルダーの用途は、パスの指定子がビルド時間ではなく、開発ホストの依存関係であることを除き、[ターゲット フレームワーク](../create-packages/supporting-multiple-target-frameworks.md)で使用されるのと類似しています。 一般的な形式は次のとおりです。

    $/analyzers/{framework_name}{version}/{supported_architecture}/{supported_language}/{analyzer_name}.dll

- **framework_name**: 含まれている DLL を実行する必要がある .NET Framework の*省略可能な* API サーフェス領域。 Roslyn がアナライザーを実行できる唯一のホストであるため、`dotnet` は、現在唯一の有効な値です。 ターゲットを指定しない場合、DLL は*すべて*のターゲットに適用されると見なされます。
- **supported_language**: `cs` (C#)、`vb` (Visual Basic)、および `fs` (F#) の DLL のいずれかの言語です。 この言語は、その言語を使用するプロジェクトに対してのみ、アナライザーが読み込まれる必要があることを示します。 言語を指定しない場合、DLL はアナライザーでサポートされる "*すべて*" の言語に適用されると想定されます。
- **analyzer_name**: アナライザーの DLL を指定します。 DLL 以外にもファイルが必要な場合は、ターゲットまたはプロパティ ファイルを介して含める必要があります。


## <a name="install-and-uninstall-scripts"></a>インストールおよびアンインストール スクリプト

ユーザーのプロジェクトで `packages.config` が使用される場合、アナライザーを取得する MSBuild スクリプトが動作しないため、以下に示すコンテンツを含む `install.ps1` と `uninstall.ps1` を `tools` フォルダーに配置する必要があります。

**install.ps1 ファイルの内容**

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


**uninstall.ps1 ファイルの内容**

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
