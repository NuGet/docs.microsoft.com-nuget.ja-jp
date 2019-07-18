---
title: NuGet のオープン PackagePage PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで開く PackagePage PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fd738f15b461051c4e9413b3035456c687979b97
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842265"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio パッケージ マネージャー コンソール)

*3.0 +; で非推奨とされます。内でのみ使用可能な[パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*

プロジェクト、ライセンス、またはレポートの指定したパッケージの URL の不正使用の既定のブラウザーを起動します。

## <a name="syntax"></a>構文

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | 目的のパッケージのパッケージ ID。 -Id スイッチ自体は省略可能です。 |
| Version | 既定では、最新バージョンのパッケージのバージョン。 |
| Source | パッケージ ソースで既定のソースのドロップダウン リストで選択したソースになります。 |
| License | パッケージのライセンス URL をブラウザーが開きます。 -ライセンスも - ReportAbuse が指定されて、パッケージのプロジェクトの URL をブラウザーが開きます。 |
| ReportAbuse | パッケージのレポートの URL の不正使用にブラウザーを開きます。 -ライセンスも - ReportAbuse が指定されて、パッケージのプロジェクトの URL をブラウザーが開きます。 |
| PassThru | URL を表示します。-whatif を使用すると、ブラウザーを開いてを抑制します。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Open-PackagePage` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、および WarningVariable します。

## <a name="examples"></a>使用例

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```