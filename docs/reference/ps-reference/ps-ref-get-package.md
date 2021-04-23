---
title: NuGet Get-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Get-Package PowerShell コマンドのリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7c91faecaac2967c7a01dd81e72b9097e7bd6cae
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901734"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio のパッケージマネージャーコンソール)

*このトピックでは、Windows 上の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内のコマンドについて説明します。汎用 PowerShell Get-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement)を参照してください。*

ローカルリポジトリにインストールされているパッケージの一覧を取得し、-ListAvailable スイッチで使用した場合はパッケージソースから利用可能なパッケージを一覧表示します。または、-Update スイッチで使用した場合は、使用可能な更新プログラムを一覧表示します。

## <a name="syntax"></a>構文

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

パラメーターを使用しない場合は、 `Get-Package` 既定のプロジェクトにインストールされているパッケージの一覧が表示されます。

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| source | パッケージの URL またはフォルダーパス。 ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。 省略した場合、 `Get-Package` 現在選択されているパッケージソースを検索します。 -ListAvailable と共に使用すると、既定で nuget.org に設定されます。 |
| ListAvailable | パッケージソースから利用可能なパッケージを一覧表示し、既定で nuget.org を使用します。-PageSize と/または-First が指定されていない限り、既定の50パッケージが表示されます。 |
| 更新プログラム | パッケージソースから利用可能な更新プログラムが含まれているパッケージを一覧表示します。 |
| ProjectName | インストールされているパッケージの取得元となるプロジェクト。 省略した場合、ソリューション全体にインストールされているプロジェクトを返します。 |
| フィルター | パッケージ ID、説明、およびタグに適用してパッケージの一覧を絞り込むために使用されるフィルター文字列。 |
| First | リストの先頭から取得するパッケージの数。 指定しない場合、の既定値は50です。 |
| スキップ | &lt; &gt; 表示されている一覧から最初の int パッケージを除外します。  |
| AllVersions | 最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンを表示します。 |
| IncludePrerelease リリース | 結果にプレリリースパッケージが含まれます。 |
| PageSize | *(3.0 以降)* -ListAvailable (必須) と共に使用する場合は、続行するように求めるメッセージを表示する前に、一覧表示するパッケージの数。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Get-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

## <a name="examples"></a>使用例

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```