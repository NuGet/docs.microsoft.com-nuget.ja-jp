---
title: NuGet の同期パッケージ PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで同期パッケージの PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: de0b612e1335cafdcd6a0b802d54f2182d27ad22
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842247"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio パッケージ マネージャー コンソール)

*バージョン 3.0 以降。内でのみ使用可能な[パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*

指定した (または既定値) からインストールされているパッケージのバージョンを取得しますはプロジェクトし、ソリューション内のプロジェクトの他のバージョンを同期します。

## <a name="syntax"></a>構文

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | (必須)同期するパッケージの識別子です。-Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | このパッケージのみとその依存関係のないをインストールします。 |
| ProjectName | 既定では、既定のプロジェクトから、パッケージを同期するプロジェクトです。 |
| Version | 同期するには、パッケージのバージョン、現在インストールされているバージョンを既定値します。 |
| Source | 検索するパッケージ ソースの URL またはフォルダーのパス。 ローカル フォルダー パスには、absolute、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Sync-Package`現在選択されているパッケージ ソースを検索します。 |
| IncludePrerelease | 同期では、プレリリース パッケージが含まれています。 |
| FileConflictAction | 上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められる場合に実行するアクション。 指定できる値は*上書き、Ignore、None、OverwriteAll*、および *(3.0 +)* *ignoreall です*します。 |
| DependencyVersion | 次のいずれかの値を使用する依存関係パッケージのバージョン:<br/><ul><li>*最も低い*(既定値): 最小バージョン</li><li>*HighestPatch*: 最高レベルの最も大きなを最低軽微な修正プログラムのバージョン</li><li>*HighestMinor*: 主要な最小のバージョン、マイナー、最高の最高の修正プログラム</li><li>*最も高い*(パラメーターなしの更新プログラム パッケージの既定): 最上位のバージョン</li></ul>使用して、既定値を設定することができます、 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。 |
| WhatIf | 実際には、同期を実行することがなく、コマンドを実行するときに何が起こるかを示します。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Sync-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、および WarningVariable します。

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
