---
title: "NuGet CLI コマンドをソース |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "ソースのコマンドを nuget.exe への参照"
keywords: "nuget のソースの参照、コマンドをソース"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a>ソースのコマンド (NuGet CLI)

**適用されます:**パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:**すべて

あるソースの一覧を管理する`%AppData%\NuGet\NuGet.Config`または指定した構成ファイル。

Nuget.org のソース URL は`https://api.nuget.org/v3/index.json`します。

## <a name="usage"></a>使用法

```
nuget sources <operation> -Name <name> -Source <source>
```

ここで`<operation>`の 1 つ*を一覧表示、追加、削除、有効化、無効化、*または*更新*、 `<name>` 、ソースの名前を指定および`<source>`ソースの URL は、します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | *(2.5 +)* NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| 形式 | 適用されます、`list`アクションを指定できます`Detailed`(既定) または`Short`です。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| 非対話型 | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| パスワード | ソースと認証のパスワードを指定します。 |
| StorePasswordInClearText | 暗号化された形式を格納する既定の動作ではなく暗号化されていないテキストでパスワードを保存することを示します。 |
| UserName | ソースと認証のユーザー名を指定します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。 |

> [!Note]
> 必ず、nuget.exe は後でパッケージ ソースへのアクセスに使用されるため、同じユーザーのコンテキストで、ソースのパスワードを追加してください。 パスワードは、config ファイルで暗号化されて格納され、できますのみ復号化、同じユーザー コンテキストで暗号化されていたとします。 したがって、たとえば使用する場合、ビルド サーバー ビルド サーバーのタスクを実行する同じ Windows ユーザーがパスワードを暗号化する必要があります NuGet パッケージを復元します。

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
