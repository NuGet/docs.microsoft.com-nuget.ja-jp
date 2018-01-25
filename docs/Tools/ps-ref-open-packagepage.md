---
title: "NuGet 開く PackagePage PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで開く PackagePage PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、開く PackagePage"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 389bad37940f05dd864adfc06080bf746464365d
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a>開く PackagePage (Visual Studio でパッケージ マネージャー コンソール)

*3.0 +; で使用されていません内でのみ使用可能な[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。*

プロジェクト、ライセンス、または指定したパッケージの不正使用を URL のレポートで既定のブラウザーを起動します。

## <a name="syntax"></a>構文

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| ID | 目的のパッケージのパッケージ ID。 -Id スイッチ自体は省略可能です。 |
| Version | 既定の最新バージョンに、パッケージのバージョン。 |
| ソース | パッケージ ソースは、ソース ドロップダウンで選択したソースを既定とします。 |
| ライセンス | パッケージのライセンス URL をブラウザーが開きます。 -ライセンスも - ReportAbuse が指定されている、パッケージのプロジェクトの URL をブラウザーが開きます。 |
| ReportAbuse | パッケージの不正使用を URL にレポートをブラウザーが開きます。 -ライセンスも - ReportAbuse が指定されている、パッケージのプロジェクトの URL をブラウザーが開きます。 |
| PassThru | URL を表示します。-whatif を使用して、抑制する状況、ブラウザーを起動します。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Open-PackagePage`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

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