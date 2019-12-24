---
title: NuGet Open-PackagePage PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで開く-PackagePage PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327379"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio パッケージ マネージャー コンソール)

*3.0 以降では非推奨となりました。Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*

指定されたパッケージのプロジェクト、ライセンス、またはレポート不正使用の URL を使用して、既定のブラウザーを起動します。

## <a name="syntax"></a>構文

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | 目的のパッケージのパッケージ ID。 -Id スイッチ自体は省略可能です。 |
| Version | パッケージのバージョン。既定では、最新のバージョンになります。 |
| Source | パッケージソース。ソースドロップダウンで選択したソースを既定として選択します。 |
| License | ブラウザーでパッケージのライセンス URL を開きます。 -License も-ReportAbuse も指定されていない場合、ブラウザーはパッケージのプロジェクト URL を開きます。 |
| ReportAbuse | パッケージの不正行為の URL をブラウザーで開きます。 -License も-ReportAbuse も指定されていない場合、ブラウザーはパッケージのプロジェクト URL を開きます。 |
| PassThru | URL が表示されます。ブラウザーを開くことを抑制するには、-WhatIf と共に使用します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Open-PackagePage`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。

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