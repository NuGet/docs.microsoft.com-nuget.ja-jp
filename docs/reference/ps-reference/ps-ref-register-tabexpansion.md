---
title: NuGet の登録/タブ拡張の PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの登録タブ拡張 PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327299"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a>登録タブ拡張 (Visual Studio のパッケージマネージャーコンソール)

*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*

指定されたコマンドのパラメーターにタブ拡張を登録します。これにより、コマンドを入力するときに Tab キーを使用すると、対象のパラメーターに使用可能なオプションとして展開値が表示されます。 コマンドの以前の展開は上書きされます。

## <a name="syntax"></a>構文

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| 名前 | 必要拡張を登録するコマンド。 -Name スイッチ自体は省略可能です。 |
| 定義 | 必要構文`@{'<parameter>' = {'<value1>', '<value2>', ...}}`の引数を記述するオブジェクト。ここ`<parameter>`で、は変更するパラメーターの名前であり`<value>` 、それぞれに特定の展開が用意されています。 単一引用符と二重引用符の両方が受け入れられます。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Register-TabExpansion`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。

## <a name="examples"></a>使用例

EventManager、Utilities、および特別なパーサーという3つのプロジェクト名が含まれるソリューションについて考えてみましょう。 開発者は、多く`Update-Package`の場合、各プロジェクトで異なるタイミングでコマンドを使用します。 この`Update-Package`コマンドを使用すると、 `-ProjectName`引数のオートコンプリートを展開できるので便利です。そのため、毎回プロジェクト名を入力する必要はありません。 

次のコマンドを実行すると、これら3つのプロジェクト名が`-ProjectName`パラメーターの展開として登録されます。

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

開発者は、「 `Update-Package -ProjectName `」と入力し、tab キーを押して、オートコンプリートオプションとして提供されている展開を確認できます。

![Register TabExpansion の使用例](media/Register-TabExpansion-Example.png)
