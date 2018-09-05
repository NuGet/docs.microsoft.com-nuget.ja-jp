---
title: NuGet CLI setapikey コマンド
description: Nuget.exe setapikey コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549221"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey コマンド (NuGet CLI)

**適用対象:** パッケージの使用、公開&bullet;**サポートされているバージョン:** すべて

特定のサーバー URL の API キーを保存します。`NuGet.Config`後続のコマンドを入力する必要がないようにします。

## <a name="usage"></a>使用法

```cli
nuget setapikey <key> -Source <url> [options]
```

場所`<source>`サーバーを識別および`<key>`はキーまたはパスワードを保存します。 場合`<source>`は省略すると、nuget.org と見なされます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
