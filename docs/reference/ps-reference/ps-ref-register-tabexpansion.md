---
title: NuGet Register-TabExpansion PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Register-TabExpansion PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 9d5bae2878cb6bf0848bca9a5ed9af0fee61bb85
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237154"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>Register-TabExpansion (Visual Studio のパッケージマネージャーコンソール)

*Windows の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*

指定されたコマンドのパラメーターにタブ拡張を登録します。これにより、コマンドを入力するときに Tab キーを使用すると、対象のパラメーターに使用可能なオプションとして展開値が表示されます。 コマンドの以前の展開は上書きされます。

## <a name="syntax"></a>構文

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Name | 必要拡張を登録するコマンド。 -Name スイッチ自体は省略可能です。 |
| 定義 | 必要構文の引数を記述するオブジェクト。 `@{'<parameter>' = {'<value1>', '<value2>', ...}}` ここで、 `<parameter>` は変更するパラメーターの名前であり、それぞれに `<value>` 特定の展開が用意されています。 単一引用符と二重引用符の両方が受け入れられます。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Register-TabExpansion` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

## <a name="examples"></a>例

EventManager、Utilities、および特別なパーサーという3つのプロジェクト名が含まれるソリューションについて考えてみましょう。 開発者は、多く `Update-Package` の場合、各プロジェクトで異なるタイミングでコマンドを使用します。 このコマンドを使用すると、 `Update-Package` 引数のオートコンプリートを展開できるので便利 `-ProjectName` です。そのため、毎回プロジェクト名を入力する必要はありません。 

次のコマンドを実行すると、これら3つのプロジェクト名がパラメーターの展開として登録され `-ProjectName` ます。

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

開発者は、「」と入力し、 `Update-Package -ProjectName ` tab キーを押して、オートコンプリートオプションとして提供されている展開を確認できます。

![Register-TabExpansion の使用例](media/Register-TabExpansion-Example.png)