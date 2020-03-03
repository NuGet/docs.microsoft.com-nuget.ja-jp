---
title: NuGet CLI setapikey コマンド
description: Nuget.exe setapikey コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231228"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey コマンド (NuGet CLI)

**適用対象:** パッケージの使用、発行 &bullet;**サポートされているバージョン:** すべて

指定されたサーバー URL の API キーを `NuGet.Config` に保存して、後続のコマンドに入力する必要がないようにします。

## <a name="usage"></a>使用法

```cli
nuget setapikey <key> -Source <url> [options]
```

`<source>` はサーバーを識別し、`<key>` は保存するキーです。 `<source>` を省略した場合、nuget.org が想定されます。 

> [!NOTE]
> API キーは、プライベートフィードでの認証には使用されません。 ソースで認証するための資格情報を管理するには、 [`nuget sources` のコマンド](../cli-reference/cli-ref-sources.md)を参照してください。
> API キーは、個々の NuGet サーバーから取得できます。 Nuget.org の APIKeys を作成および管理するには、「[発行 api キー](../../quickstart/includes/publish-api-key.md) 」を参照してください。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| 詳細度 | 出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。 |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
