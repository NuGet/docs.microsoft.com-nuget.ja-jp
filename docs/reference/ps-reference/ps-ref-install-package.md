---
title: NuGet インストール-パッケージ PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでのインストールパッケージ PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327339"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio パッケージ マネージャー コンソール)

*このトピックでは、Windows 上の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内のコマンドについて説明します。汎用 PowerShell のインストールパッケージコマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*

パッケージとその依存関係をプロジェクトにインストールします。

## <a name="syntax"></a>構文

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 以降では`Install-Package` 、はプロジェクト内の既存のパッケージをダウングレードできます。 たとえば、次のコマンドでは、Microsoft の AspNet. MVC 5.1.0-rc1 がインストールされている場合、それを5.0.0 にダウングレードします。

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | 必要インストールするパッケージの識別子。 (*3.0 以降*)識別子には、 `packages.config`ファイル`.nupkg`またはファイルのパスまたは URL を指定できます。 -Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | 依存関係ではなく、このパッケージのみをインストールします。 |
| ProjectName | パッケージのインストール先となるプロジェクト。既定のプロジェクトが既定のプロジェクトになります。 |
| Source | 検索するパッケージソースの URL またはフォルダーパス。 ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。 省略した`Install-Package`場合、現在選択されているパッケージソースを検索します。 |
| Version | インストールするパッケージのバージョン。既定では、最新バージョンが対象となります。 |
| IncludePrerelease | インストールのプレリリースパッケージを検討します。 省略した場合、安定したパッケージだけが考慮されます。 |
| FileConflictAction | プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクション。 指定できる値は *、Overwrite、Ignore、None、OverwriteAll*、 *(3.0 +)* *ignoreall*です。 |
| DependencyVersion | 使用する依存関係パッケージのバージョン。次のいずれかになります。<br/><ul><li>*最低*(既定): 最も低いバージョン</li><li>*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</li><li>*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</li><li>*最高*(パラメーターのない更新プログラム-パッケージの既定値): 最高のバージョン</li></ul>`Nuget.Config`ファイルの[`dependencyVersion`](../nuget-config-file.md#config-section)設定を使用して、既定値を設定できます。 |
| WhatIf | 実際にインストールを実行せずにコマンドを実行した場合の動作を示します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Install-Package`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。

## <a name="examples"></a>使用例

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
