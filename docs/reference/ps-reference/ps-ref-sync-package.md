---
title: NuGet Sync-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Sync-Package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc4c875b5dcb0b90e4d048daf5984ed265370090
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238050"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio のパッケージマネージャーコンソール)

*バージョン 3.0 +;Windows の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*

指定された (または既定の) プロジェクトからインストールされているパッケージのバージョンを取得し、そのバージョンをソリューション内の残りのプロジェクトと同期します。

## <a name="syntax"></a>構文

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Id | 必要同期するパッケージの識別子。-Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | 依存関係ではなく、このパッケージのみをインストールします。 |
| ProjectName | パッケージの同期元のプロジェクト。既定のプロジェクトが既定のプロジェクトになります。 |
| Version | 同期するパッケージのバージョンです。既定では、現在インストールされているバージョンが対象となります。 |
| source | 検索するパッケージソースの URL またはフォルダーパス。 ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。 省略した場合、 `Sync-Package` 現在選択されているパッケージソースを検索します。 |
| IncludePrerelease リリース | には、同期のプレリリースパッケージが含まれています。 |
| FileConflictAction | プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクション。 指定できる値は *、Overwrite、Ignore、None、OverwriteAll* 、 *(3.0 +)* *ignoreall* です。 |
| DependencyVersion | 使用する依存関係パッケージのバージョン。次のいずれかになります。<br/><ul><li>*最低* (既定): 最も低いバージョンです。</li><li>*HighestPatch* : 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</li><li>*HighestMinor* : 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</li><li>*最高* (パラメーターのない Update-Package の既定値): 最高バージョン</li></ul>ファイルの設定を使用して、既定値を設定でき [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` ます。 |
| WhatIf | 実際に同期を実行せずにコマンドを実行した場合の動作を示します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Sync-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

## <a name="examples"></a>使用例

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```