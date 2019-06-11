---
title: NuGet CLI ヘルプ コマンド
description: Nuget.exe の help コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546564"
---
# <a name="help-or--command-nuget-cli"></a>help or ? コマンド (NuGet CLI)

**適用対象:** すべて&bullet;**サポートされているバージョン**: すべて

表示の [全般] では、ヘルプ情報と、特定のコマンドに関するヘルプ情報。

## <a name="usage"></a>使用法

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

[コマンド] で、ヘルプを表示する特定のコマンドを識別する場所。

> [!Warning]
> いくつかのコマンドを使用するを指定することに注意してください*ヘルプ*でとして初めて、 `nuget help install`nuget.org で「ヘルプ」をという名前のパッケージがあるためです。コマンドを指定する場合`nuget install help`、インストール コマンドのヘルプを表示しませんが、代わりにはヘルプをという名前のパッケージをインストールします。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| All | すべての利用可能なコマンドは詳細なヘルプを印刷します。特定のコマンドを指定した場合は無視されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプ、ヘルプ コマンド自体の情報を表示します。 |
| Markdown | Markdown 形式で使用する場合に詳細なヘルプを印刷`-All`します。 それ以外の場合は無視されます。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
