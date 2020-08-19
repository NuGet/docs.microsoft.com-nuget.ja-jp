---
title: NuGet CLI 検索コマンド
description: nuget.exe search コマンドのリファレンス
author: advay26
ms.author: t-adtand
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 35e4906960534299418cb2a17c190476708b2634
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623253"
---
# <a name="search-command-nuget-cli"></a>search コマンド (NuGet CLI)

**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 5.8 +

指定されたクエリ文字列を使用して、指定されたソースを検索します。 ソースが指定されていない場合は、% AppData% \NuGet\NuGet.config で定義されているすべてのソースが使用されます。

## <a name="usage"></a>使用法

```cli
nuget search [search terms] [options]
```

ここでは、nuget.org で使用する場合と同じように、パッケージ、タグ、およびパッケージの説明の名前に検索語句が適用されます。

## <a name="options"></a>Options

| 名前 | 説明 | 使用法 |
| ---  |     ---     |  :-:  |
| リリース | プレリリースパッケージは既定では含まれていませんが、この引数を使用して含めることができます。 | -プレリリース |
| source | __nuget.config__の既定のソースに対してクエリを実行するのではなく、検索する特定のパッケージソース | -ソース `<Source URL>`|
| Take | 返される結果の数。 既定値は 20 です。 | -Take `<positive integer>` |
| 詳細度 | 出力に表示する詳細のレベル。 既定値は _normal_です。 (下のメモを参照してください)  | -詳細度 `<quiet\|normal\|detailed>` |
| Help | コマンドのヘルプ情報を表示します。 | -ヘルプ |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

__注__

詳細レベル:

* _quiet_ -パッケージ ID、バージョン
* _通常_ -パッケージ ID、バージョン、ダウンロード、説明のプレビュー
* _詳細_ -パッケージ ID、バージョン、ダウンロード、完全な説明、クエリ URL などのその他の情報

## <a name="examples"></a>例

既定のソースから *ログ*関連パッケージを検索する:
```
nuget search logging
```
詳細な詳細情報を含む *ログ*関連パッケージを検索します。
```
nuget search logging -Verbosity detailed
```
*ログ*関連パッケージを検索し、上位5件の結果のみを表示します。
```
nuget search logging -Take 5
```
指定したソース/フィードから、プレリリースバージョンを含む *JSON*関連パッケージを検索します。
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
複数のソース/フィードから *JSON*関連のパッケージを検索します。
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
