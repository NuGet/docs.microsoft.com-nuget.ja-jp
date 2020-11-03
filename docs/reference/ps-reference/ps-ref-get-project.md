---
title: NuGet Get-Project PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの GetProject PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 6d9e1d48c8e1838f193878cab3483b1bfba7d7f0
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238076"
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
| Name | 表示するプロジェクトを指定します。既定では、パッケージマネージャーコンソールで選択されている既定のプロジェクトが対象となります。 -Name スイッチ自体はオプションです。 |
| All | ソリューション内のすべてのプロジェクトの情報を表示します。プロジェクトの順序は決定的ではありません。 |

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