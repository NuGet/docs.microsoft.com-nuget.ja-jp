---
title: NuGet の登録/タブ拡張の PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの登録タブ拡張 PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384455"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>登録タブ拡張 (Visual Studio のパッケージマネージャーコンソール)

*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*

指定されたコマンドのパラメーターにタブ拡張を登録します。これにより、コマンドを入力するときに Tab キーを使用すると、対象のパラメーターに使用可能なオプションとして展開値が表示されます。 コマンドの以前の展開は上書きされます。

## <a name="syntax"></a>構文

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメータ | 説明 |
| --- | --- |
| [名前] | 必要拡張を登録するコマンド。 -Name スイッチ自体は省略可能です。 |
| Definition | 必要`@{'<parameter>' = {'<value1>', '<value2>', ...}}` 構文の引数を記述するオブジェクト。 `<parameter>` は変更するパラメーターの名前であり、各 `<value>` は特定の拡張を提供します。 単一引用符と二重引用符の両方が受け入れられます。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Register-TabExpansion` 次のサポート[一般的な PowerShell パラメーター](https://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

EventManager、Utilities、および特別なパーサーという3つのプロジェクト名が含まれるソリューションについて考えてみましょう。 開発者は、多くの場合、それぞれのプロジェクトで異なるタイミングで `Update-Package` コマンドを使用します。 `Update-Package` コマンドを使用すると、`-ProjectName` 引数に対してオートコンプリートを展開できるので便利です。そのため、毎回プロジェクト名を入力する必要はありません。 

次のコマンドを実行すると、これら3つのプロジェクト名が `-ProjectName` パラメーターの展開として登録されます。

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

開発者は `Update-Package -ProjectName `を入力し、Tab キーを押して、オートコンプリートオプションとして提供されている展開を確認できます。

![Register TabExpansion の使用例](media/Register-TabExpansion-Example.png)
