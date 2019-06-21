---
title: プロジェクトの NuGet Get PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで GetProject PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550438"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio パッケージ マネージャー コンソール)

*内でのみ使用可能な[NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*

既定値または指定されたプロジェクトについての情報を表示します。 `Get-Project` 具体的には、プロジェクトの Visual Studio DTE (Development Tools Environment) のオブジェクトに参照を返します。

## <a name="syntax"></a>構文

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| 名前 | 既定では、パッケージ マネージャー コンソールで選択されている既定のプロジェクトを表示するには、プロジェクトに指定します。 -Name スイッチが自体の省略可能です。 |
| All | このソリューションですべてのプロジェクトの情報を表示します。プロジェクトの順序は決定論的ではありません。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Get-Project` は次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216) をサポートしています: Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable

## <a name="examples"></a>使用例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```