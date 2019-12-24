---
title: NuGet Get-プロジェクト PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの GetProject PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 830746f032bb4eb916508ef320c5b3d0486b89a4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327359"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio パッケージ マネージャー コンソール)

*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*

既定のプロジェクトまたは指定されたプロジェクトに関する情報を表示します。 `Get-Project`具体的には、プロジェクトの Visual Studio DTE (開発ツール環境) オブジェクトへの指示を返します。

## <a name="syntax"></a>構文

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Name | 既定では、パッケージ マネージャー コンソールで選択されている既定のプロジェクトを表示するには、プロジェクトに指定します。 -Name スイッチ自体は省略可能です。 |
| All | ソリューション内のすべてのプロジェクトの情報を表示します。プロジェクトの順序は決定的ではありません。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Get-Project`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。

## <a name="examples"></a>使用例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```