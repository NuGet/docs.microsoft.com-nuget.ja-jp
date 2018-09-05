---
title: NuGet のインストール パッケージの PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで Install-package の PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546027"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio パッケージ マネージャー コンソール)

*このトピックでは、内のコマンドを説明します、 [NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。一般的な PowerShell のインストール パッケージ コマンドは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)します。*

プロジェクトにパッケージとその依存関係をインストールします。

## <a name="syntax"></a>構文

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 以降で`Install-Package`プロジェクトに既存のパッケージをダウン グレードできます。 たとえば、Microsoft.AspNet.MVC 5.1.0-rc1 がインストールされている場合は、次のコマンドはダウン グレード 5.0.0。

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | (必須)インストールするパッケージの識別子。 (*3.0 +*) 識別子は、パスまたは URL の`packages.config`ファイルまたは`.nupkg`ファイル。 -Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | このパッケージのみとその依存関係のないをインストールします。 |
| ProjectName | 既定では、既定のプロジェクト、パッケージをインストールするプロジェクトです。 |
| ソース | 検索するパッケージ ソースの URL またはフォルダーのパス。 ローカル フォルダー パスには、absolute、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Install-Package`現在選択されているパッケージ ソースを検索します。 |
| Version | バージョンをインストールするパッケージの既定の最新バージョンになります。 |
| IncludePrerelease | プレリリース パッケージのインストールを検討します。 省略した場合は、安定版パッケージのみが考慮されます。 |
| FileConflictAction | 上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められる場合に実行するアクション。 指定できる値は*上書き、Ignore、None、OverwriteAll*、および *(3.0 +)* *ignoreall です*します。 |
| DependencyVersion | 次のいずれかの値を使用する依存関係パッケージのバージョン:<br/><ul><li>*最も低い*(既定値): 最小バージョン</li><li>*HighestPatch*: 最高レベルの最も大きなを最低軽微な修正プログラムのバージョン</li><li>*HighestMinor*: 主要な最小のバージョン、マイナー、最高の最高の修正プログラム</li><li>*最も高い*(パラメーターなしの更新プログラム パッケージの既定): 最上位のバージョン</li></ul>使用して、既定値を設定することができます、 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。 |
| WhatIf | 実際には、インストールを実行せず、コマンドを実行するときに何が起こるかを示します。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Install-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
