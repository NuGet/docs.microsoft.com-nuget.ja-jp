---
title: NuGet Install-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Install-Package PowerShell コマンドのリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901695"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a>Install-Package (Visual Studio のパッケージマネージャーコンソール)

*このトピックでは、Windows 上の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内のコマンドについて説明します。汎用 PowerShell Install-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement)を参照してください。*

パッケージとその依存関係をプロジェクトにインストールします。

## <a name="syntax"></a>構文

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

NuGet 2.8 以降では、は `Install-Package` プロジェクト内の既存のパッケージをダウングレードできます。 たとえば、次のコマンドでは、Microsoft の AspNet. MVC 5.1.0-rc1 がインストールされている場合、それを5.0.0 にダウングレードします。

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Id | 必要インストールするパッケージの識別子。 (*3.0 以降*)識別子には、ファイルまたはファイルのパスまたは URL を指定でき `packages.config` `.nupkg` ます。 -Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | 依存関係ではなく、このパッケージのみをインストールします。 |
| ProjectName | パッケージのインストール先となるプロジェクト。既定のプロジェクトが既定のプロジェクトになります。 |
| source | 検索するパッケージソースの URL またはフォルダーパス。 ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。 省略した場合、 `Install-Package` 現在選択されているパッケージソースを検索します。 |
| Version | インストールするパッケージのバージョン。既定では、最新バージョンが対象となります。 |
| IncludePrerelease リリース | インストールのプレリリースパッケージを検討します。 省略した場合、安定版パッケージのみが考慮されます。 |
| FileConflictAction | プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクション。 指定できる値は *、Overwrite、Ignore、None、OverwriteAll*、 *(3.0 +)* *ignoreall* です。 |
| DependencyVersion | 使用する依存関係パッケージのバージョン。次のいずれかになります。<br/><ul><li>*最低* (既定): 最も低いバージョンです。</li><li>*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</li><li>*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</li><li>*最高* (パラメーターのない Update-Package の既定値): 最高バージョン</li></ul>ファイルの設定を使用して、既定値を設定でき [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` ます。 |
| WhatIf | 実際にインストールを実行せずにコマンドを実行した場合の動作を示します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Install-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

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