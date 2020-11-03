---
title: NuGet Open-PackagePage PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Open-PackagePage PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ba90e09c017ec66d73c35a60025474bc77cf65a7
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238063"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>Open-PackagePage (Visual Studio のパッケージマネージャーコンソール)

*3.0 以降では非推奨となりました。Windows の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*

指定されたパッケージのプロジェクト、ライセンス、またはレポート不正使用の URL を使用して、既定のブラウザーを起動します。

## <a name="syntax"></a>構文

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Id | 目的のパッケージのパッケージ ID。 -Id スイッチ自体は省略可能です。 |
| Version | パッケージのバージョン。既定では、最新のバージョンになります。 |
| source | パッケージソース。ソースドロップダウンで選択したソースを既定として選択します。 |
| ライセンス | ブラウザーでパッケージのライセンス URL を開きます。 -License も-ReportAbuse も指定されていない場合、ブラウザーはパッケージのプロジェクト URL を開きます。 |
| ReportAbuse | パッケージの不正行為の URL をブラウザーで開きます。 -License も-ReportAbuse も指定されていない場合、ブラウザーはパッケージのプロジェクト URL を開きます。 |
| PassThru | URL が表示されます。ブラウザーを開くことを抑制するには、-WhatIf と共に使用します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Open-PackagePage` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

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