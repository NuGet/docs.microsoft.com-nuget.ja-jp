---
title: NuGet CLI コマンドをソースします。
description: ソースのコマンドを nuget.exe への参照
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d588ff09075ad75b76b7dd3645f3cdff29f6f093
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="sources-command-nuget-cli"></a>ソースのコマンド (NuGet CLI)

**適用されます:** パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:** すべて

ユーザー スコープの構成ファイルまたは指定された構成ファイル内にあるソースの一覧を管理します。 ユーザー スコープの構成ファイルにある`%appdata%\NuGet\NuGet.Config`(Windows) と`~/.nuget/NuGet/NuGet.Config`(Mac または Linux)。

ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。

## <a name="usage"></a>使用法

```cli
nuget sources <operation> -Name <name> -Source <source>
```

ここで`<operation>`の 1 つ*を一覧表示、追加、削除、有効化、無効化、*または*更新*、 `<name>` 、ソースの名前を指定および`<source>`ソースの URL は、します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| ForceEnglishOutput | *(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| 形式 | 適用されます、`list`アクションを指定できます`Detailed`(既定) または`Short`です。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| パスワード | ソースと認証のパスワードを指定します。 |
| StorePasswordInClearText | 暗号化された形式を格納する既定の動作ではなく暗号化されていないテキストでパスワードを保存することを示します。 |
| UserName | ソースと認証のユーザー名を指定します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

> [!Note]
> 必ず、nuget.exe は後でパッケージ ソースへのアクセスに使用されるため、同じユーザーのコンテキストで、ソースのパスワードを追加してください。 パスワードは、config ファイルで暗号化されて格納され、できますのみ復号化、同じユーザー コンテキストで暗号化されていたとします。 したがって、たとえば使用する場合、ビルド サーバー ビルド サーバーのタスクを実行する同じ Windows ユーザーがパスワードを暗号化する必要があります NuGet パッケージを復元します。

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
