---
title: NuGet のレジスタ TabExpansion PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで登録 TabExpansion PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842480"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>登録 TabExpansion (Visual Studio でパッケージ マネージャー コンソール)

*内でのみ使用可能な[パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*

展開された値が対象のパラメーターの使用可能なオプションとして表示するコマンドを入力するときにタブを使用する場合など、指定されたコマンドのパラメーターにタブ拡張を登録します。 コマンドは、前の展開が上書きされます。

## <a name="syntax"></a>構文

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| 名前 | (必須)拡張を登録するためにコマンド。 -Name スイッチ自体は省略可能です。 |
| 定義 | (必須)構文の引数を表すオブジェクトです。`@{'<parameter>' = {'<value1>', '<value2>', ...}}`場所`<parameter>`を変更するパラメーターとそれぞれの名前を指定`<value>`固有の展開を提供します。 両方一重引用符と二重引用符が受け入れられます。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Register-TabExpansion` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、および WarningVariable します。

## <a name="examples"></a>使用例

EventManager、ユーティリティ、および SpecialParser の 3 つのプロジェクト名を含むソリューションを検討してください。 開発者が頻繁に使用して、`Update-Package`でこれらの各プロジェクトのさまざまなタイミングでコマンド。 便利なことを確認します、`Update-Package`コマンドは、展開を自動補完機能を提供する、`-ProjectName`引数たびにプロジェクト名を入力する必要があるので。 

次のコマンドがの拡張として次に、これら 3 つのプロジェクトの名前を登録、`-ProjectName`パラメーター。

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

入力できる開発者`Update-Package -ProjectName `、Tab キーを押して、オート コンプリート オプションとして提供される拡張を参照してください。

![登録 TabExpansion の使用例](media/Register-TabExpansion-Example.png)
