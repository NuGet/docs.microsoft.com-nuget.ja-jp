---
title: NuGet CLI コマンドをソースします。
description: ソースのコマンドを nuget.exe への参照
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7ef856f783c8e11cdb40edb0d1c1458730d87262
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548109"
---
# <a name="sources-command-nuget-cli"></a>ソースのコマンド (NuGet CLI)

**適用対象:** パッケージの使用、公開&bullet;**サポートされているバージョン:** すべて

ユーザー スコープの構成ファイルまたは指定した構成ファイル内にあるソースの一覧を管理します。 ユーザー スコープの構成ファイルは`%appdata%\NuGet\NuGet.Config`(Windows) と`~/.nuget/NuGet/NuGet.Config`(Mac/linux)。

ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。

## <a name="usage"></a>使用法

```cli
nuget sources <operation> -Name <name> -Source <source>
```

場所`<operation>`の 1 つです*を一覧表示、追加、削除、有効にする、無効化、* または*更新*、 `<name>` 、ソースの名前を指定および`<source>`はソースの URL です。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| 形式 | 適用されます、`list`アクションを指定できます`Detailed`(既定値) または`Short`します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| [Password] | ソースと認証のパスワードを指定します。 |
| StorePasswordInClearText | 暗号化された形式を格納する既定の動作ではなく暗号化されていないテキストでパスワードを保存することを示します。 |
| UserName | ソースと認証のユーザー名を指定します。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

> [!Note]
> 必ず、nuget.exe が後でパッケージ ソースへのアクセスに使用されるため、同じユーザー コンテキストでのソースのパスワードを追加してください。 パスワードは、構成ファイルで暗号化して保存してが暗号化されたために、同じユーザー コンテキストで解除のみできます。 そのため、たとえば使用する場合、ビルド サーバー、ビルド サーバーのタスクを実行する同じ Windows ユーザーがパスワードを暗号化する必要があります NuGet パッケージを復元します。

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
