---
title: NuGet Find-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで Find-package PowerShell コマンドのリファレンスです。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 0faf5c5cf9ae99105e3d76a4f5e37f164c4f4ff3
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-package (Visual Studio でパッケージ マネージャー コンソール)

*Version 3.0 以降。このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。一般的な PowerShell Find-package コマンドは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*

パッケージ ソースから指定された ID またはキーワードに一致するリモート パッケージのセットを取得します。

## <a name="syntax"></a>構文

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Id&lt;キーワード&gt; | (必須)パッケージ ソースの検索に使用するキーワードです。 ExactMatch-を使用して、パッケージ ID を持つが、キーワードと一致するパッケージのみを返します。 キーワードが指定されていない場合`Find-Package`によって指定される最初のダウンロード、または番号によって上位 20 のパッケージの一覧を返します。 -Id が省略可能なため、no-op に注意してください。 |
| ソース | 検索するパッケージ ソースの URL またはフォルダーのパス。 ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。 省略した場合、`Find-Package`現在選択されているパッケージ ソースを検索します。 |
| AllVersions | 最新バージョンのみではなく、各パッケージのすべての利用可能なバージョンを表示します。 |
| First | リストの先頭から返されるパッケージの数既定値は 20 です。 |
| Skip | 最初の省略&lt;int&gt;表示される一覧からパッケージです。  |
| IncludePrerelease | 結果にリリース前のパッケージが含まれています。 |
| ExactMatch | 使用する指定された&lt;キーワード&gt;大文字小文字を区別パッケージ ID と |
| 始める | 返します。 パッケージがパッケージ ID が始まる&lt;キーワード&gt;です。 |

これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。

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
