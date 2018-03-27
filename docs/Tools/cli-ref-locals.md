---
title: "NuGet CLI ローカル コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe [ローカル] コマンドのリファレンス"
keywords: "nuget ローカル変数の参照、[ローカル] コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="locals-command-nuget-cli"></a>[ローカル] コマンド (NuGet CLI)

**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 3.3 +

消去または http 要求のキャッシュ、パッケージ キャッシュ、および、コンピューター全体のグローバル パッケージ フォルダーなどのローカルの NuGet リソースを一覧表示します。 `locals`コマンドを使用してこれらの場所の一覧を表示することもできます。 詳細については、次を参照してください。 [NuGet キャッシュを管理する](../consume-packages/managing-the-nuget-cache.md)です。

## <a name="usage"></a>使用法

```cli
nuget locals <cache> [options]
```

ここで`<cache>`の 1 つ`all`、 `http-cache`、 `packages-cache`、 `global-packages`、および`temp` *(3.4 以降)*です。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| Clear | 指定されたキャッシュをクリアします。 |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| リスト | 指定されたキャッシュの場所またはを使用すると、すべてのキャッシュの場所を一覧表示*すべて*です。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget locals all -list
nuget locals http-cache -clear
```
