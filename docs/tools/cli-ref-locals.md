---
title: ローカルの NuGet CLI コマンド
description: Nuget.exe の [ローカル] コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ea216c4651ba9619bc3b6a7ab52546fd299b0bb6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545029"
---
# <a name="locals-command-nuget-cli"></a>locals コマンド (NuGet CLI)

**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン:** 3.3 +

クリアまたはローカルの NuGet リソースを一覧表示など、 *http キャッシュ*、*グローバル パッケージ*フォルダー、および一時フォルダーです。 `locals`コマンドがそれらの場所の一覧を表示することもできます。 詳細については、[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)を参照してください。

## <a name="usage"></a>使用法

```cli
nuget locals <folder> [options]
```

場所`<folder>`の 1 つ`all`、 `http-cache`、 `packages-cache` *(3.5 およびそれ以前)* 、 `global-packages`、 `temp` *(3.4 以上)* 、および`plugins-cache` *(4.8 +)* します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| Clear | 指定したフォルダーをクリアします。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| List | 指定したフォルダーの場所またはを使用すると、すべてのフォルダーの場所を一覧表示*すべて*します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

その他の例では、[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)を参照してください。
