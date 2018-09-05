---
title: NuGet CLI delete コマンド
description: Nuget.exe 削除コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 11eea6e806d7bfe364587db9c7ef8374da1819f9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548511"
---
# <a name="delete-command-nuget-cli"></a>delete コマンド (NuGet CLI)

**適用対象:** パッケージの発行&bullet;**サポートされているバージョン:** すべて

パッケージ ソースからパッケージを一覧から、または削除します。 Nuget.org には、delete コマンドの[パッケージを一覧から](../policies/deleting-packages.md)します。

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
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| ソース | サーバー URL を指定します。 Nuget.org の URL は`https://api.nuget.org/v3/index.json`します。 たとえば、プライベート フィードを置き換えて、ホスト名 *%hostname%/api/v3*します。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
