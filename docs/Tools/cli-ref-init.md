---
title: "NuGet CLI init コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe init コマンドのリファレンス"
keywords: "nuget init 参照、init コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 6d7710cd024e2c2956fb73aa767c3be55b9fb0f9
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="init-command-nuget-cli"></a>init コマンド (NuGet CLI)

**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:** 3.3 +

説明に従って、階層構造を使用して目的のフォルダーにフラット フォルダーからすべてのパッケージをコピー、[コマンド追加](cli-ref-add.md)です。 使用して、`init`を使用すると、`add`フォルダー内の各パッケージにコマンド。

同様に`add`、変換先がローカル フォルダーまたは UNC パスのいずれかにする必要がありますNuget.org またはプライベート サーバーなどのパッケージ リポジトリの HTTP はサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget init <source> <destination> [options]
```

ここで`<source>`パッケージを含むフォルダーと`<destination>`は、ローカル フォルダーまたは UNC のパス名が、パッケージのコピー先となります。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Expand | パッケージ ソースに追加される各パッケージ内のすべてのファイルを追加します。同じ`-Expand`で、`add`コマンド。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
