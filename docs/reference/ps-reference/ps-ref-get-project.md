---
title: NuGet Get-プロジェクト PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの GetProject PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384621"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a>Get-Project (Visual Studio パッケージ マネージャー コンソール)

*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*

既定のプロジェクトまたは指定されたプロジェクトに関する情報を表示します。 `Get-Project` は、プロジェクトの Visual Studio DTE (開発ツール環境) オブジェクトに対して明示的にを返します。

## <a name="syntax"></a>構文

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメータ | 説明 |
| --- | --- |
| [名前] | 既定では、パッケージ マネージャー コンソールで選択されている既定のプロジェクトを表示するには、プロジェクトに指定します。 -Name スイッチ自体は省略可能です。 |
| すべての | ソリューション内のすべてのプロジェクトの情報を表示します。プロジェクトの順序は決定的ではありません。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Get-Project` 次のサポート[一般的な PowerShell パラメーター](https://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```