---
title: NuGet 同期パッケージの PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで同期パッケージの PowerShell コマンドのリファレンスです。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 424c4fbe3ff4b61c665bf7353976d4fb09268185
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a>Sync-Package (Visual Studio パッケージ マネージャー コンソール)

*Version 3.0 以降。内でのみ使用可能な[NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。*

指定した (または既定値) からインストールされているパッケージのバージョンを取得では、プロジェクトし、ソリューション内のプロジェクトの残りの部分をバージョンを同期します。

## <a name="syntax"></a>構文

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | (必須)同期するパッケージの識別子。-Id スイッチ自体は省略可能です。 |
| IgnoreDependencies | このパッケージのみを依存関係は含めずをインストールします。 |
| ProjectName | 既定で、既定のプロジェクトから、パッケージを同期するプロジェクトです。 |
| Version | 同期するには、パッケージのバージョン、現在インストールされているバージョンを既定とします。 |
| ソース | 検索するパッケージ ソースの URL またはフォルダーのパス。 ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Sync-Package`現在選択されているパッケージ ソースを検索します。 |
| IncludePrerelease | 同期では、プレリリースのパッケージが含まれています。 |
| FileConflictAction | 上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクション。 指定できる値は*上書き、Ignore、None、OverwriteAll*、および *(3.0 以降)* *ignoreall です*です。 |
| DependencyVersion | 次のいずれかを使用する依存関係パッケージ バージョン:<br/><ul><li>*最小*(既定値): 最小バージョン</li><li>*HighestPatch*: 最小メジャー、マイナー最小、最高の修正プログラムのバージョン</li><li>*HighestMinor*: 主要な最小のバージョン、最高のマイナー、最上位の修正プログラム</li><li>*最も高い*(パラメーターなしで更新プログラム パッケージの既定): 最上位バージョン</li></ul>使用して、既定値を設定することができます、 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。 |
| WhatIf | 実際には、同期を実行せず、コマンドを実行している場合にどうなるかを示します。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Sync-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

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
