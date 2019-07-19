---
title: NuGet CLI リストコマンド
description: Nuget.exe list コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 61294f4c9d85336dc8b718fd66b236c692bab00e
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327739"
---
# <a name="list-command-nuget-cli"></a>list コマンド(NuGet CLI)

**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン**の発行: すべて

指定されたソースからのパッケージの一覧を表示します。 ソースが指定されていない場合は、グローバル構成ファイル`%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`で定義されているすべてのソースが使用されます。 が`NuGet.Config`ソースを指定しない`list`場合、は既定のフィード (nuget.org) を使用します。

## <a name="usage"></a>使用法

```cli
nuget list [search terms] [options]
```

オプションの検索語句を使用すると、表示される一覧がフィルター処理されます。 Nuget.org で使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前には検索語句が適用されます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AllVersions | パッケージのすべてのバージョンを一覧表示します。 既定では、最新のパッケージバージョンのみが表示されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| IncludeDelisted | *(3.2 +)* 一覧にないパッケージを表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| PreRelease | には、一覧にプレリリースパッケージが含まれています。 |
| Source | 検索するパッケージソースの一覧を指定します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget list

nuget list chinese korean -Verbosity detailed

nuget list couchbase -AllVersions
```
