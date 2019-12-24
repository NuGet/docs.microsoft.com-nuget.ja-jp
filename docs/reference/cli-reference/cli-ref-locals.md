---
title: NuGet CLI の locals コマンド
description: Nuget.exe locals コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327809"
---
# <a name="locals-command-nuget-cli"></a>locals コマンド (NuGet CLI)

**適用対象:** パッケージの使用3&bullet;が**サポートされているバージョン:** 3.3+

*Http キャッシュ*、*グローバルパッケージ*フォルダー、一時フォルダーなどのローカル NuGet リソースをクリアまたは一覧表示します。 また`locals` 、コマンドを使用して、これらの場所の一覧を表示することもできます。 詳細については、「[グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」を参照してください。

## <a name="usage"></a>使用法

```cli
nuget locals <folder> [options]
```

ここ`<folder>`で、は`all`、 `http-cache` `temp` `global-packages` `plugins-cache`、(3.5 以前)、、(3.4 +)、および (4.8 +) のいずれかです。 `packages-cache`

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| Clear | 指定されたフォルダーをクリアします。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| List | 指定したフォルダーの場所、または*すべて*のフォルダーを使用する場合はすべてのフォルダーの場所を一覧表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

その他の例については、「[グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」を参照してください。
