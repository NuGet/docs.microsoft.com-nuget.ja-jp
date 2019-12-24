---
title: NuGet Get-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの Get Package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327349"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a>Get-Package (Visual Studio パッケージ マネージャー コンソール)

*このトピックでは、Windows 上の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内のコマンドについて説明します。汎用 PowerShell のパッケージの取得コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*

ローカルリポジトリにインストールされているパッケージの一覧を取得し、-ListAvailable スイッチで使用した場合はパッケージソースから利用可能なパッケージを一覧表示します。または、-Update スイッチで使用した場合は、使用可能な更新プログラムを一覧表示します。

## <a name="syntax"></a>構文

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

パラメーターを使用し`Get-Package`ない場合は、既定のプロジェクトにインストールされているパッケージの一覧が表示されます。

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Source | パッケージの URL またはフォルダーパス。 ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。 省略した`Get-Package`場合、現在選択されているパッケージソースを検索します。 -ListAvailable と共に使用すると、既定で nuget.org に設定されます。 |
| ListAvailable | パッケージソースから利用可能なパッケージを一覧表示し、既定で nuget.org を使用します。-PageSize と/または-First が指定されていない限り、既定の50パッケージが表示されます。 |
| Updates | パッケージソースから利用可能な更新プログラムが含まれているパッケージを一覧表示します。 |
| ProjectName | インストールされているパッケージの取得元となるプロジェクト。 省略した場合、ソリューション全体にインストールされているプロジェクトを返します。 |
| Filter | パッケージ ID、説明、およびタグに適用してパッケージの一覧を絞り込むために使用されるフィルター文字列。 |
| First | リストの先頭から取得するパッケージの数。 指定しない場合、の既定値は50です。 |
| Skip | 表示され&lt;て&gt;いる一覧から最初の int パッケージを除外します。  |
| AllVersions | 最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンを表示します。 |
| IncludePrerelease | 結果にプレリリースパッケージが含まれます。 |
| PageSize | *(3.0 以降)* -ListAvailable (必須) と共に使用する場合は、続行するように求めるメッセージを表示する前に、一覧表示するパッケージの数。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Get-Package`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。

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
