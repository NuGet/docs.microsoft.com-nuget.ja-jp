---
title: プロジェクトの NuGet Get PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで GetProject PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 2ceb1557eafd213c148d3ab870925ef5bbbee145
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842274"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio パッケージ マネージャー コンソール)

*内でのみ使用可能な[パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*

既定値または指定されたプロジェクトについての情報を表示します。 `Get-Project` 具体的には、プロジェクトの Visual Studio DTE (Development Tools Environment) のオブジェクトに参照を返します。

## <a name="syntax"></a>構文

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Name | 既定では、パッケージ マネージャー コンソールで選択されている既定のプロジェクトを表示するには、プロジェクトに指定します。 -Name スイッチ自体は省略可能です。 |
| All | このソリューションですべてのプロジェクトの情報を表示します。プロジェクトの順序は決定論的ではありません。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Get-Project` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、および WarningVariable します。

## <a name="examples"></a>使用例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```