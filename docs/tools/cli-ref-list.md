---
title: NuGet CLI の一覧表示コマンド
description: Nuget.exe list コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549802"
---
# <a name="list-command-nuget-cli"></a>list コマンド(NuGet CLI)

**適用対象:** パッケージの使用、公開&bullet;**サポートされているバージョン:** すべて

指定したソースからのパッケージの一覧を表示します。 すべてのソースが、グローバル構成ファイルで定義されているソースが指定されていない場合`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`、使用されます。 場合`NuGet.Config`し、ソースを指定しません`list`(nuget.org) の既定のフィードを使用します。

## <a name="usage"></a>使用法

```cli
nuget list [search terms] [options]
```

省略可能な検索語句は、表示される一覧にフィルターされます。 検索語句は、nuget.org でそれらを使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前に適用されます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AllVersions | パッケージのすべてのバージョンを一覧表示します。 既定では、最新のバージョンのパッケージのみが表示されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| IncludeDelisted | *(3.2 以降)* 一覧から削除されたパッケージが表示されます。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| PreRelease | 一覧には、プレリリース パッケージが含まれています。 |
| Source | 検索するパッケージ ソースの一覧を指定します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
