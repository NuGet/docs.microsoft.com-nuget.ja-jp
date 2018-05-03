---
title: NuGet パッケージの PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで Get-package PowerShell コマンドのリファレンスです。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: c70e60b7391f19026e2dcd502d667fbe1da7e6e2
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-package (Visual Studio でパッケージ マネージャー コンソール)

*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。一般的な PowerShell Get-package コマンドは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*

ローカル リポジトリにインストールされているパッケージの一覧を取得、-listavailable スイッチで使用する場合は、パッケージ ソースから使用可能なパッケージを一覧表示または更新スイッチを使用すると、利用可能な更新を一覧表示します。

## <a name="syntax"></a>構文

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

パラメーターなしで`Get-Package`既定のプロジェクトにインストールされているパッケージの一覧を表示します。

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ソース | パッケージの URL またはフォルダーのパス。 ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Get-Package`現在選択されているパッケージ ソースを検索します。 -Listavailable で使用する場合は、nuget.org を既定値です。 |
| ListAvailable | 既定で nuget.org、パッケージ ソースから使用可能なパッケージを一覧表示します。-PageSize や最初が指定されていない限り、既定値は 50 のパッケージを示しています。 |
| 更新 | パッケージ ソースで更新が提供されているパッケージを一覧表示します。 |
| ProjectName | インストールされているパッケージの取得元のプロジェクトです。 省略した場合、ソリューション全体に対してプロジェクトがインストールを返します。 |
| フィルター | パッケージ ID、説明、およびタグを適用して、パッケージの一覧を絞り込むためのフィルター文字列。 |
| First | リストの先頭から返されるパッケージの数。 指定しない場合、既定値は 50 です。 |
| Skip | 最初の省略&lt;int&gt;表示される一覧からパッケージです。  |
| AllVersions | 最新バージョンのみではなく、各パッケージのすべての利用可能なバージョンを表示します。 |
| IncludePrerelease | 結果にリリース前のパッケージが含まれています。 |
| PageSize | *(3.0 +)* -Listavailable と共に使用 (必須)、パッケージの数を続行するためのプロンプトを許可する前に一覧表示するときにします。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Get-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

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
