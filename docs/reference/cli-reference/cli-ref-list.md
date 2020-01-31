---
title: NuGet CLI の list コマンド
description: Nuget.exe list コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94228521b3be85277990bca2da69518b7070bbdf
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813339"
---
# <a name="list-command-nuget-cli"></a>list コマンド(NuGet CLI)

**適用対象:** パッケージの使用、発行 &bullet;**サポートされているバージョン:** すべて

指定されたソースからのパッケージの一覧を表示します。 ソースが指定されていない場合は、グローバル構成 `%AppData%\NuGet\NuGet.Config` ファイル (Windows) または `~/.nuget/NuGet/NuGet.Config`で定義されているすべてのソースが使用されます。 `NuGet.Config` がソースを指定しない場合、`list` は既定のフィード (nuget.org) を使用します。

## <a name="usage"></a>使用状況

```cli
nuget list [search terms] [options]
```

オプションの検索語句を使用すると、表示される一覧がフィルター処理されます。 Nuget.org で使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前には検索語句が適用されます。

## <a name="options"></a>[オプション]

| オプション | 説明 |
| --- | --- |
| AllVersions | パッケージのすべてのバージョンを一覧表示します。 既定では、最新のパッケージバージョンのみが表示されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| IncludeDelisted | *(3.2 +)* 一覧にないパッケージを表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| PreRelease | には、一覧にプレリリースパッケージが含まれています。 |
| Source | 検索するパッケージソースの一覧を指定します。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

構成されたフィードからすべてのパッケージを一覧表示する:
```
nuget list
```
詳細な詳細度で Azure 関連パッケージを一覧表示する:
```
nuget list Azure -Verbosity detailed
```
構成済みのフィードから Azure 関連のパッケージのすべてのバージョンを一覧表示します。
```
nuget list Azure -AllVersions
```
指定したソース/フィードから、JSON 関連のパッケージのすべてのバージョンを一覧表示します。
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
複数のソース/フィードから JSON 関連のパッケージを一覧表示する:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```

