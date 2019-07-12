---
title: NuGet Get-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで Get-package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d0d25cb6e21f6d0d42389e08340b6f1e1baf8a64
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842518"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio パッケージ マネージャー コンソール)

*このトピックでは、内のコマンドを説明します、[パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。汎用の Get-package の PowerShell コマンドでは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)します。*

ローカル リポジトリにインストールされているパッケージの一覧を取得、- ListAvailable スイッチと共に使用する場合は、パッケージ ソースから使用可能なパッケージを一覧表示または更新スイッチを使用すると、利用可能な更新を一覧表示されます。

## <a name="syntax"></a>構文

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

パラメーターなしで`Get-Package`既定のプロジェクトにインストールされているパッケージの一覧が表示されます。

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Source | パッケージの URL またはフォルダーのパス。 ローカル フォルダー パスには、absolute、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Get-Package`現在選択されているパッケージ ソースを検索します。 -ListAvailable で使用する場合は、nuget.org に既定値です。 |
| ListAvailable | 既定では nuget.org をパッケージ ソースから使用可能なパッケージを一覧表示します。-PageSize や最初が指定されていない場合、既定値は 50 のパッケージを示します。 |
| Updates | パッケージ、パッケージ ソースから使用可能な更新プログラムを一覧表示します。 |
| ProjectName | インストールされているパッケージの取得元のプロジェクトです。 省略した場合は、ソリューション全体のプロジェクトをインストールされている返します。 |
| Filter | パッケージ ID、説明、およびタグに適用して、パッケージの一覧を絞り込むために使用されるフィルター文字列。 |
| First | リストの先頭から返されるパッケージの数。 指定しない場合、既定値は 50 です。 |
| Skip | 最初の省略&lt;int&gt;表示された一覧からパッケージ。  |
| AllVersions | 最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンが表示されます。 |
| IncludePrerelease | 結果には、プレリリース パッケージが含まれています。 |
| PageSize | *(3.0 以降)* 続行を求めるメッセージを渡す前に一覧表示する - ListAvailable (必須)、パッケージの数と使用するとします。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Get-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、および WarningVariable します。

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
