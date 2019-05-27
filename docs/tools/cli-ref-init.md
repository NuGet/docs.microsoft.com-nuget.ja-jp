---
title: NuGet CLI init コマンド
description: Nuget.exe の init コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551411"
---
# <a name="init-command-nuget-cli"></a>init コマンド (NuGet CLI)

**適用対象:** パッケージの作成&bullet;**サポートされているバージョン:** 3.3 以降

説明に従って、階層構造を使用して目的のフォルダーにフラットなフォルダーからすべてのパッケージをコピー、[コマンドを追加](cli-ref-add.md)します。 使用して、`init`を使用すると、`add`フォルダー内の各パッケージにコマンド。

同様`add`、変換先がローカル フォルダーまたは UNC パスのいずれかにする必要がありますNuget.org やプライベート サーバーなどの HTTP パッケージ リポジトリがサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget init <source> <destination> [options]
```

場所`<source>`パッケージを含むフォルダーと`<destination>`ローカル フォルダーまたはパッケージのコピー先となる UNC パス名です。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Expand | パッケージのソースに追加される各パッケージ内のすべてのファイルを追加します。同じ`-Expand`で、`add`コマンド。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細* |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
