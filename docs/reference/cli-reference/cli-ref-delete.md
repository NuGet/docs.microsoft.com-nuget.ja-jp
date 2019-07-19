---
title: NuGet CLI の削除コマンド
description: Nuget.exe delete コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327839"
---
# <a name="delete-command-nuget-cli"></a>delete コマンド (NuGet CLI)

**適用対象:** パッケージ発行&bullet;の**サポートされているバージョン:** すべて

パッケージソースからパッケージを削除または一覧から削除します。 Nuget.org の場合、delete コマンドを実行すると、[パッケージの一覧](../../nuget-org/policies/deleting-packages.md)が解除されます。

## <a name="usage"></a>使用法

```cli
nuget delete <packageID> <packageVersion> [options]
```

`<packageID>` と`<packageVersion>`は、削除するパッケージまたは一覧から削除を指定します。 実際の動作は、ソースによって異なります。 たとえば、ローカルフォルダーの場合、パッケージは削除されます。nuget.org の場合、パッケージは一覧から削除されます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットリポジトリの API キー。 存在しない場合は、構成ファイルで指定されたものが使用されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Source | サーバー URL を指定します。 Nuget.org の URL は`https://api.nuget.org/v3/index.json`です。 プライベートフィードの場合は、ホスト名に置き換えます (例 *% hostname%/api/v3*)。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
