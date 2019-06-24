---
title: NuGet Find-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールでの検索パッケージの PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: c6797e3778c7095a9abfc6cd87e2337313988c20
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550979"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-package (Visual Studio パッケージ マネージャー コンソール)

*バージョン 3.0 以降。このトピックでは、内のコマンドを説明します、 [NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。汎用の Find-package の PowerShell コマンドでは、、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*

パッケージ ソースから指定された ID またはキーワードを含むリモート パッケージのセットを取得します。

## <a name="syntax"></a>構文

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Id&lt;キーワード&gt; | (必須)パッケージ ソースの検索に使用するキーワードです。 -"Exactmatch"を使用して、パッケージ ID を持つキーワードに一致するパッケージのみを返します。 キーワードが指定されない場合`Find-Package`によって指定される最初のダウンロード、または数によって上位 20 のパッケージの一覧を返します。 Id が省略可能なことに注意してくださいれません。 |
| Source | 検索するパッケージ ソースの URL またはフォルダーのパス。 ローカル フォルダー パスには、absolute、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Find-Package`現在選択されているパッケージ ソースを検索します。 |
| AllVersions | 最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンが表示されます。 |
| First | リストの先頭から返すパッケージ数既定では 20 です。 |
| Skip | 最初の省略&lt;int&gt;表示された一覧からパッケージ。  |
| IncludePrerelease | 結果には、プレリリース パッケージが含まれています。 |
| "Exactmatch" | 使用する指定された&lt;キーワード&gt;大文字のパッケージ id |
| StartWith | 返します。 パッケージがパッケージの ID が始まる&lt;キーワード&gt;します。 |

これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

## <a name="common-parameters"></a>共通パラメーター

`Find-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。

## <a name="examples"></a>使用例

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```
