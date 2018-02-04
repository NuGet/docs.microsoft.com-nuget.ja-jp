---
title: "NuGet CLI リスト コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 一覧のコマンドのリファレンス"
keywords: "nuget の一覧の参照、パッケージの一覧表示コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5a1f68aaffd26a0f903aa3a7a4a450a0121191c3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="list-command-nuget-cli"></a>list コマンド (NuGet CLI)

**適用されます:**パッケージ消費、パブリッシング&bullet;**サポートされているバージョン:**すべて

指定されたソースからのパッケージの一覧を表示します。 すべてのソースが、グローバル構成ファイルで定義されているソースが指定されていない場合`%AppData%\NuGet\NuGet.Config`、使用されます。 場合`NuGet.Config`し、ソースを指定しません`list`既定のフィード (nuget.org) を使用します。

## <a name="usage"></a>使用法

```cli
nuget list [search terms] [options]
```

ここで、省略可能な検索用語は、表示される一覧にフィルターされます。 検索語句は、パッケージ、タグ、およびパッケージの説明の名前に適用されます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AllVersions | パッケージのすべてのバージョンを一覧表示します。 既定では、最新のバージョンのパッケージのみが表示されます。 |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| IncludeDelisted | *(3.2 +)*一覧にないパッケージを表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| PreRelease | 一覧には、プレリリースのパッケージが含まれています。 |
| ソース | 検索するパッケージ ソースの一覧を指定します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget list

nuget list -Verbosity detailed -AllVersions
```
