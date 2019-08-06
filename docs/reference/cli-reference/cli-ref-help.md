---
title: NuGet CLI の help コマンド
description: Nuget.exe help コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327799"
---
# <a name="help-or--command-nuget-cli"></a>help or ? コマンド (NuGet CLI)

**適用対象:** &bullet; **サポートされている**すべてのバージョン: すべて

特定のコマンドに関する一般的なヘルプ情報とヘルプ情報を表示します。

## <a name="usage"></a>使用法

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

ここで [command] は、ヘルプを表示する特定のコマンドを識別します。

> [!Warning]
> 一部のコマンドでは、nuget.org に "help" という`nuget help install`名前のパッケージが存在するので、最初にヘルプを指定することに注意してください。コマンド`nuget install help`を指定した場合、install コマンドのヘルプは表示されませんが、help という名前のパッケージがインストールされます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| All | 使用可能なすべてのコマンドの詳細なヘルプを印刷します。特定のコマンドが指定されている場合は無視されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプコマンド自体のヘルプ情報を表示します。 |
| Markdown | で`-All`使用する場合は、markdown 形式の詳細なヘルプを印刷します。 それ以外の場合は無視されます。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Verbosity | 出力に表示される詳細データの量を指定します: *normal*、*quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
