---
title: NuGet CLI [ローカル] コマンド
description: Nuget.exe [ローカル] コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818202"
---
# <a name="locals-command-nuget-cli"></a>locals コマンド (NuGet CLI)

**適用されます:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 3.3 +

消去または NuGet のローカル リソースを一覧表示など、 *http キャッシュ*、*グローバル パッケージ*フォルダー、および一時フォルダーです。 `locals`コマンドを使用してこれらの場所の一覧を表示することもできます。 詳細については、次を参照してください。[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。

## <a name="usage"></a>使用法

```cli
nuget locals <folder> [options]
```

ここで`<folder>`の 1 つ`all`、 `http-cache`、 `packages-cache` *(3.5 およびそれ以前)*、 `global-packages`、および`temp` *(3.4 以降)* です。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| Clear | 指定したフォルダーを消去します。 |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| ForceEnglishOutput | *(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| リスト | 指定したフォルダーの場所またはを使用すると、すべてのフォルダーの場所を一覧表示*すべて*です。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

その他の例では、次を参照してください。[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。
