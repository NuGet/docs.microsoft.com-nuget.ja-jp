---
title: NuGet 更新プログラム-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの更新プログラムパッケージ PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 57e50ed805496b3511bc3b808f89da6f7ad413fc
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327269"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a>Update-Package (Visual Studio パッケージ マネージャー コンソール)

*Windows の Visual Studio の[NuGet パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*

パッケージとその依存関係、またはプロジェクト内のすべてのパッケージを新しいバージョンに更新します。

## <a name="syntax"></a>構文

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 以降では`Update-Package` 、を使用して、プロジェクト内の既存のパッケージをダウングレードできます。 たとえば、次のコマンドでは、Microsoft の AspNet. MVC 5.1.0-rc1 がインストールされている場合、それを5.0.0 にダウングレードします。

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>パラメーター

|  パラメーター | 説明 |
| --- | --- |
| ID | 更新するパッケージの識別子。 省略すると、すべてのパッケージが更新されます。 -Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | パッケージの依存関係の更新をスキップします。 |
| ProjectName | 更新するパッケージが含まれているプロジェクトの名前。既定ではすべてのプロジェクトになります。 |
| Version | アップグレードに使用するバージョン。既定では、最新バージョンが使用されます。 NuGet 3.0 以降では、バージョンの値は、*最低、最高、HighestMinor*、または*HighestPatch*のいずれかである必要があります (これはセーフに相当します)。 |
| セーフ | は、現在インストールされているパッケージと同じメジャーバージョンとマイナーバージョンを持つバージョンにのみアップグレードを制限します。 |
| Source | 検索するパッケージソースの URL またはフォルダーパス。 ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。 省略した`Update-Package`場合、現在選択されているパッケージソースを検索します。 |
| IncludePrerelease | 更新プログラムのプレリリースパッケージが含まれます。 |
| Reinstall | 現在インストールされているバージョンを使用してパッケージを Resintalls します。 「[パッケージの再インストールと更新](../../consume-packages/reinstalling-and-updating-packages.md)」をご覧ください。 |
| FileConflictAction | プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクション。 指定できる値は *、Overwrite、Ignore、None、OverwriteAll*、および*ignoreall* (3.0 +) です。 |
| DependencyVersion | 使用する依存関係パッケージのバージョン。次のいずれかになります。<br/><ul><li>*最低*(既定): 最も低いバージョン</li><li>*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</li><li>*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</li><li>*最高*(パラメーターのない更新プログラム-パッケージの既定値): 最高のバージョン</li></ul>`Nuget.Config`ファイルの[`dependencyVersion`](../nuget-config-file.md#config-section)設定を使用して、既定値を設定できます。 |
| ToHighestPatch | -Safe と同等です。 |
| ToHighestMinor | は、現在インストールされているパッケージと同じメジャーバージョンのバージョンにのみアップグレードを制限します。 |
| WhatIf | 実際に更新を実行せずにコマンドを実行した場合の動作を示します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

### <a name="common-parameters"></a>共通パラメーター

`Update-Package`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。

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
