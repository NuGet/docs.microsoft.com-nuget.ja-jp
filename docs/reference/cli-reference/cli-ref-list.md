---
title: NuGet CLI リストコマンド
description: nuget.exe list コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a6a4ee434c43ad4865dba12f039b5d545a90d3c4
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238167"
---
# <a name="list-command-nuget-cli"></a>list コマンド (NuGet CLI)

**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン** の発行: すべて

指定されたソースからのパッケージの一覧を表示します。 ソースが指定されていない場合は、グローバル構成ファイル (Windows) またはで定義されているすべてのソース `%AppData%\NuGet\NuGet.Config` `~/.nuget/NuGet/NuGet.Config` が使用されます。 が `NuGet.Config` ソースを指定しない場合、は `list` 既定のフィード (nuget.org) を使用します。

## <a name="usage"></a>使用

```cli
nuget list [search terms] [options]
```

オプションの検索語句を使用すると、表示される一覧がフィルター処理されます。 Nuget.org で使用する場合と同様に、パッケージ、タグ、およびパッケージの説明の名前には[検索語句](../../consume-packages/finding-and-choosing-packages.md#search-syntax)が適用されます。 

## <a name="options"></a>オプション

- **`-AllVersions`**

  パッケージのすべてのバージョンを一覧表示します。 既定では、最新のパッケージバージョンのみが表示されます。

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-IncludeDelisted`**

  *(3.2 +)* 一覧にないパッケージを表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-PreRelease`**

  には、一覧にプレリリースパッケージが含まれています。

- **`-Source`**

  検索するパッケージソースの一覧を指定します。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>例

構成されたフィードからすべてのパッケージを一覧表示する:
```
nuget list
```
詳細な詳細度で Azure 関連パッケージを一覧表示する:
```
nuget list Azure -Verbosity detailed
```
構成済みのフィードから Azure 関連のパッケージのすべてのバージョンを一覧表示します。
```
nuget list Azure -AllVersions
```
指定したソース/フィードから、JSON 関連のパッケージのすべてのバージョンを一覧表示します。
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
複数のソース/フィードから JSON 関連のパッケージを一覧表示する:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```