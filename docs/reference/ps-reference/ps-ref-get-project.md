---
title: NuGet Get-Project PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの GetProject PowerShell コマンドのリファレンス。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777470"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio のパッケージマネージャーコンソール)

*Windows の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*

既定のプロジェクトまたは指定されたプロジェクトに関する情報を表示します。 `Get-Project` 具体的には、プロジェクトの Visual Studio DTE (開発ツール環境) オブジェクトへの指示を返します。

## <a name="syntax"></a>構文

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| 名前 | 表示するプロジェクトを指定します。既定では、パッケージマネージャーコンソールで選択されている既定のプロジェクトが対象となります。 -Name スイッチ自体はオプションです。 |
| すべて | ソリューション内のすべてのプロジェクトの情報を表示します。プロジェクトの順序は決定的ではありません。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Get-Project` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

## <a name="examples"></a>使用例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```