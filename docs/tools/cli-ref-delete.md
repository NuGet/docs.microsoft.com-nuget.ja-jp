---
title: NuGet CLI delete コマンド
description: Nuget.exe 削除コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426108"
---
# <a name="delete-command-nuget-cli"></a>delete コマンド (NuGet CLI)

**適用対象:** パッケージの発行&bullet;**サポートされているバージョン:** すべて

パッケージ ソースからパッケージを一覧から、または削除します。 Nuget.org には、delete コマンドの[パッケージを一覧から](../nuget-org/policies/deleting-packages.md)します。

## <a name="usage"></a>使用法

```cli
nuget delete <packageID> <packageVersion> [options]
```

場所`<packageID>`と`<packageVersion>`を削除または一覧から削除する正確なパッケージを識別します。 正確な動作は、ソースによって異なります。 ローカル フォルダーは、たとえば、パッケージを削除します。nuget.org のパッケージが一覧表示されているではありません。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットのリポジトリの API キー。 存在しない場合は、構成ファイルで指定された 1 つが使用されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| Source | サーバー URL を指定します。 Nuget.org の URL は`https://api.nuget.org/v3/index.json`します。 たとえば、プライベート フィードを置き換えて、ホスト名 *%hostname%/api/v3*します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細* |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
