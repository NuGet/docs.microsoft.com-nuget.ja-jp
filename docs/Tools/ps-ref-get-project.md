---
title: "プロジェクトの NuGet Get PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで GetProject PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、Get プロジェクト"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c347a6104d89bb29626ad7c2f33bec150eb38cd2
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get プロジェクト (Visual Studio でパッケージ マネージャー コンソール)

*内でのみ使用可能な[NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。*

既定値または指定したプロジェクトについての情報を表示します。 `Get-Project` 具体的には、プロジェクトの Visual Studio DTE (Development Tools Environment) のオブジェクトに参照を返します。

## <a name="syntax"></a>構文

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| name | 既定のパッケージ マネージャー コンソールで選択された既定のプロジェクトを表示するには、プロジェクトに指定します。 -Name スイッチは、それ自体の省略可能です。 |
| すべて | このソリューションでのすべてのプロジェクトの情報を表示プロジェクトの順序は確定的ではありません。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Get-Project` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```