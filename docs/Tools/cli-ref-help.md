---
title: "NuGet CLI help コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 780d7f52-d6c6-45cd-8a62-218ff8c0b270
description: "Nuget.exe help コマンドのリファレンス"
keywords: "nuget ヘルプ リファレンス、コマンドのヘルプします。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 55dc263fedd7ed5a3e48b76dbc9a3ccc220655cf
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="help-or--command-nuget-cli"></a>役立ちますか? コマンド (NuGet CLI)

**適用されます:**すべて&bullet;**サポートされているバージョン**: すべて

ヘルプ情報と、特定のコマンドに関するヘルプ情報する一般的な表示にします。

## <a name="usage"></a>使用方法

```
nuget help [command] [options]
nuget ? [command] [options]
```

ここで [コマンド] は、ヘルプを表示する対象の特定のコマンドを識別します。

> [!Warning]
> いくつかのコマンドで指定を考慮する*ヘルプ*first、としての`nuget help install`nuget.org に"help"をという名前のパッケージがあるため、します。コマンドを付ける場合`nuget install help`、-install コマンドのヘルプを取得できませんされますが、ヘルプをという名前のパッケージを代わりにインストールされます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| すべて | すべての利用可能なコマンドは詳細なヘルプを表示します。特定のコマンドを指定した場合は無視されます。 |
| ConfigFile | *(2.5 +)* NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンド自体の情報のヘルプを表示します。 |
| Markdown | マークダウン形式で使用する場合の詳細なヘルプを印刷`-All`です。 それ以外の場合は無視されます。 |
| 非対話型 | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>例

```
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
