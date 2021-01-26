---
title: NuGet Find-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Find-Package PowerShell コマンドのリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 83d0d62bbda07d07ea1e3b58e531447e2001b680
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777506"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-Package (Visual Studio のパッケージマネージャーコンソール)

*バージョン 3.0 +;このトピックでは、Windows 上の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内のコマンドについて説明します。汎用 PowerShell Find-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*

パッケージソースから指定された ID またはキーワードを持つリモートパッケージのセットを取得します。

## <a name="syntax"></a>構文

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Id &lt; キーワード&gt; | 必要パッケージソースの検索時に使用するキーワード。 パッケージ ID がキーワードと一致するパッケージのみを返すには、-"Exactmatch" を使用します。 キーワードが指定されていない場合 `Find-Package` は、ダウンロードによって上位20個のパッケージの一覧が返されます。または、-First で指定した数が返されます。 -Id は省略可能であり、no op であることに注意してください。 |
| source | 検索するパッケージソースの URL またはフォルダーパス。 ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。 省略した場合、 `Find-Package` 現在選択されているパッケージソースを検索します。 |
| AllVersions | 最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンを表示します。 |
| First | リストの先頭から取得するパッケージの数。既定値は20です。 |
| スキップ | &lt; &gt; 表示されている一覧から最初の int パッケージを除外します。  |
| IncludePrerelease リリース | 結果にプレリリースパッケージが含まれます。 |
| ExactMatch | &lt; &gt; 大文字小文字を区別するパッケージ ID としてキーワードを使用するように指定します。 |
| StartWith | パッケージ ID がキーワードで始まるパッケージを返し &lt; &gt; ます。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Find-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。

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