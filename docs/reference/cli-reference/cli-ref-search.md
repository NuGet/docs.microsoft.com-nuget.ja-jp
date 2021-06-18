---
title: NuGet CLI 検索コマンド
description: nuget.exe search コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323662"
---
# <a name="search-command-nuget-cli"></a>search コマンド (NuGet CLI)

**適用対象: パッケージ** 消費量 &bullet; **サポートされているバージョン:** 5.8 以上

指定されたクエリ文字列を使用して、特定のソースを検索します。 ソースが指定されていない場合は、%AppData%\NuGet\NuGet.Configソースが使用されます。

## <a name="usage"></a>使用方法

```cli
nuget search [search terms] [options]
```

ここで、検索用語は、パッケージ、タグ、パッケージの説明の名前と同様に、パッケージの名前に適用 nuget.org。

## <a name="options"></a>オプション

| 名前 | 説明 | 使用法 |
| ---  |     ---     |  :-:  |
| プレリリース | プレリリース パッケージは既定では含まれていませんが、この引数を使用して含めできます | -PreRelease |
| source | 既定のソースにクエリを実行する代わりに検索する特定のパッケージ ソースnuget.config | -Source `<Source URL>`|
| Take | 返される結果の数。 既定値は 20 です。 | -Take `<positive integer>` |
| 詳細度 | 出力に表示する詳細レベル。 既定値は通常 _の です_。 (下記の注を参照してください)  | -Verbosity `<quiet|normal|detailed>` |
| Help | コマンドのヘルプ情報を表示します | -Help |

「環境変数 [」も参照してください。](cli-ref-environment-variables.md)

> [!NOTE] 
> 詳細レベル:
> * _quiet_ - パッケージ ID、バージョン
> * _normal_ - パッケージ ID、バージョン、ダウンロード、説明のプレビュー
> * _detailed_ - パッケージ ID、バージョン、ダウンロード、完全な説明、クエリ URL などのその他の情報

## <a name="examples"></a>例

既定のソース *から* ログに関連するパッケージを検索します。
```
nuget search logging
```
詳細な *詳細を* 含むログに関連するパッケージを検索します。
```
nuget search logging -Verbosity detailed
```
ログに *関連する* パッケージを検索し、上位 5 件の結果のみを表示します。
```
nuget search logging -Take 5
```
指定した *ソース/* フィードから、プレリリース バージョンを含む JSON 関連のパッケージを検索します。
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
複数の *ソース/* フィードから JSON 関連のパッケージを検索します。
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
