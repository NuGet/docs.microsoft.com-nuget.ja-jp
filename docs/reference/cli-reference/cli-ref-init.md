---
title: NuGet CLI の init コマンド
description: Nuget.exe init コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4441dc3cc35a96736b51867c196313fc9ccfdac2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327779"
---
# <a name="init-command-nuget-cli"></a>init コマンド (NuGet CLI)

**適用対象:** パッケージ作成&bullet;で**サポートされているバージョン:** 3.3+

[add コマンド](cli-ref-add.md)の説明に従って階層構造を使用して、フラットフォルダーのすべてのパッケージをコピー先フォルダーにコピーします。 つまり、を使用`init`することは、フォルダー `add`内の各パッケージに対してコマンドを使用することと同じです。

と`add`同様に、コピー先はローカルフォルダーまたは UNC パスである必要があります。Nuget.org やプライベートサーバーなどの HTTP パッケージリポジトリはサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget init <source> <destination> [options]
```

ここ`<source>`で、は`<destination>`パッケージを含むフォルダーで、はパッケージのコピー先のローカルフォルダーまたは UNC パス名です。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Expand | パッケージソースに追加された各パッケージ内のすべてのファイルを追加します。`-Expand` コマンド`add`と同じです。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
