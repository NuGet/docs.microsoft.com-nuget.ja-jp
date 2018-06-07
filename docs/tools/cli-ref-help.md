---
title: NuGet CLI help コマンド
description: Nuget.exe help コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818257"
---
# <a name="help-or--command-nuget-cli"></a>help or ? コマンド (NuGet CLI)

**適用されます:** すべて&bullet;**サポートされているバージョン**: すべて

ヘルプ情報と、特定のコマンドに関するヘルプ情報する一般的な表示にします。

## <a name="usage"></a>使用法

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

ここで [コマンド] は、ヘルプを表示する対象の特定のコマンドを識別します。

> [!Warning]
> いくつかのコマンドで指定を考慮する*ヘルプ*first、としての`nuget help install`nuget.org に"help"をという名前のパッケージがあるため、します。コマンドを付ける場合`nuget install help`、-install コマンドのヘルプを表示しませんが、ヘルプをという名前のパッケージを代わりにインストールされます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| すべて | すべての利用可能なコマンドは詳細なヘルプを表示します。特定のコマンドを指定した場合は無視されます。 |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| ForceEnglishOutput | *(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンド自体の情報のヘルプを表示します。 |
| Markdown | マークダウン形式で使用する場合の詳細なヘルプを印刷`-All`です。 それ以外の場合は無視されます。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
