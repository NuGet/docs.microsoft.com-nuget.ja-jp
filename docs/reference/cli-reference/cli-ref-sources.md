---
title: NuGet CLI source コマンド
description: Nuget.exe の source コマンドリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327599"
---
# <a name="sources-command-nuget-cli"></a>NuGet CLI source コマンド

**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン**の発行: すべて

ユーザースコープ構成ファイルまたは指定された構成ファイルにあるソースの一覧を管理します。 ユーザースコープ構成ファイルは、(Windows `%appdata%\NuGet\NuGet.Config` ) と`~/.nuget/NuGet/NuGet.Config` (Mac/Linux) にあります。

ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。

## <a name="usage"></a>使用法

```cli
nuget sources <operation> -Name <name> -Source <source>
```

ここ`<operation>`で、は*List、Add、Remove、Enable、Disable、* または Update `<name>`のいずれかで、はソース`<source>`の名前、はソースの URL です。 操作できるソースは一度に1つだけです。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Format | `list`アクションに適用され、 `Detailed` (既定値) または`Short`にすることができます。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Password | ソースでの認証に使用するパスワードを指定します。 |
| StorePasswordInClearText | 暗号化されたフォームを格納する既定の動作ではなく、暗号化されていないテキストにパスワードを格納することを示します。 |
| UserName | ソースでの認証に使用するユーザー名を指定します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

> [!Note]
> Nuget を後で使用してパッケージソースにアクセスするのと同じユーザーコンテキストで、ソースのパスワードを追加してください。 パスワードは暗号化されて構成ファイルに格納され、暗号化されたときと同じユーザーコンテキストでのみ暗号化を解除できます。 たとえば、ビルドサーバーを使用して NuGet パッケージを復元する場合、ビルドサーバータスクを実行するのと同じ Windows ユーザーでパスワードを暗号化する必要があります。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
