---
title: "NuGet の更新プログラム パッケージの PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで更新プログラム パッケージの PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、更新プログラム パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 293d9a7fdcce633eb5a97e5f76398deb5c13bdb4
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>更新プログラム パッケージ (Visual Studio でパッケージ マネージャー コンソール)

*内でのみ使用可能な[NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。*

パッケージとその依存関係またはプロジェクトでは、すべてのパッケージを新しいバージョンに更新されます。

## <a name="syntax"></a>構文

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 + で`Update-Package`プロジェクトで既存のパッケージをダウン グレードすることできます。 たとえば、Microsoft.AspNet.MVC 5.1.0-rc1 がインストールされている場合は、次のコマンドはへのダウン グレードに 5.0.0 以降。

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>パラメーター

|  パラメーター | 説明 |
| --- | --- |
| ID | 更新するパッケージの識別子。 省略した場合は、すべてのパッケージを更新します。 -Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | パッケージの依存関係の更新をスキップします。 |
| ProjectName | プロジェクトを更新するパッケージを含む、すべてのプロジェクトには、既定の名前。 |
| Version | アップグレードは、既定で最新バージョンを使用するバージョンです。 NuGet 3.0 以降で、バージョンの値はのいずれかのことがあります*Lowest、最高、HighestMinor*、または*HighestPatch* (Safe に相当)。 |
| セーフ | 現在インストールされているパッケージと同じメジャーおよびマイナー バージョンの唯一のバージョンにアップグレードするように制約します。 |
| ソース | 検索するパッケージ ソースの URL またはフォルダーのパス。 ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Uninstall-Package`現在選択されているパッケージ ソースを検索します。 |
| IncludePrerelease | プレリリースのパッケージ更新プログラムにはが含まれます。 |
| 再インストール | Resintalls パッケージが、現在インストールされているバージョンを使用します。 「[パッケージの再インストールと更新](../consume-packages/reinstalling-and-updating-packages.md)」をご覧ください。 |
| FileConflictAction | 上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクション。 指定できる値は*上書き、Ignore、None、OverwriteAll*、および*ignoreall です*(3.0 以降)。 |
| DependencyVersion | 次のいずれかを使用する依存関係パッケージ バージョン:<br/><ul><li>*最小*(既定値): 最小バージョン</li><li>*HighestPatch*: 最小メジャー、マイナー最小、最高の修正プログラムのバージョン</li><li>*HighestMinor*: 主要な最小のバージョン、最高のマイナー、最上位の修正プログラム</li><li>*最も高い*(パラメーターなしで更新プログラム パッケージの既定): 最上位バージョン</li></ul>使用して、既定値を設定することができます、 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。 |
| ToHighestPatch | 現在インストールされているパッケージとマイナー バージョンが同じでバージョンのみへのアップグレードを制約します。 |
| ToHighestMinor | 現在インストールされているパッケージと同じメジャー バージョンのバージョンのみへのアップグレードを制約します。 |
| WhatIf | 実際には、更新プログラムを実行せず、コマンドを実行している場合にどうなるかを示します。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

### <a name="common-parameters"></a>共通パラメーター

`Update-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

### <a name="examples"></a>使用例

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```