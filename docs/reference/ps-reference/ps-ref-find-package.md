---
title: NuGet 検索-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで、[パッケージの検索] PowerShell コマンドを参照してください。
author: karann-msft
ms.author: karann
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 4bb6d090b97dd55fc1be0625855aab27a0d181c4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327389"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a>Find-package (Visual Studio パッケージ マネージャー コンソール)

*バージョン 3.0 +;このトピックでは、Windows 上の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内のコマンドについて説明します。汎用 PowerShell 検索パッケージコマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*

パッケージソースから指定された ID またはキーワードを持つリモートパッケージのセットを取得します。

## <a name="syntax"></a>構文

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a>パラメーター

| パラメーター | 説明 |
| --- | --- |
| Id &lt;キーワード&gt; | 必要パッケージソースの検索時に使用するキーワード。 パッケージ ID がキーワードと一致するパッケージのみを返すには、-"Exactmatch" を使用します。 キーワードが指定されて`Find-Package`いない場合は、ダウンロードによって上位20個のパッケージの一覧が返されます。または、-First で指定した数が返されます。 -Id は省略可能であり、no op であることに注意してください。 |
| Source | 検索するパッケージソースの URL またはフォルダーパス。 ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。 省略した`Find-Package`場合、現在選択されているパッケージソースを検索します。 |
| AllVersions | 最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンを表示します。 |
| First | リストの先頭から取得するパッケージの数。既定値は20です。 |
| Skip | 表示され&lt;て&gt;いる一覧から最初の int パッケージを除外します。  |
| IncludePrerelease | 結果にプレリリースパッケージが含まれます。 |
| "Exactmatch" | 大文字小文字&lt;を&gt;区別するパッケージ ID としてキーワードを使用するように指定します。 |
| StartWith | パッケージ ID がキーワード&lt;&gt;で始まるパッケージを返します。 |

これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。

## <a name="common-parameters"></a>共通パラメーター

`Find-Package`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。

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
