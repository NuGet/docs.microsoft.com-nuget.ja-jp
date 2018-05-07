---
title: NuGet CLI ミラー コマンド
description: Nuget.exe ミラー コマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5ba13196d385abf42a5af2faa3fe6f0e80fb59d8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="mirror-command-nuget-cli"></a>mirror コマンド (NuGet CLI)

**適用されます:** パッケージの発行&bullet;**サポートされているバージョン:** 3.2 以降で廃止されました

パッケージとターゲットのリポジトリに指定されたソース リポジトリからその依存関係を反映します。

> [!NOTE]
> このコマンドは、NuGet のバージョン 3.2 の前に有効にするには[ https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)を最新の安定版リリースを選択し、ダウンロード`NuGet.ServerExtensions.dll`と`Nuget-Signed.exe`、ローカル ディスクと名前の変更に`Nuget-Signed.exe`に`nuget.exe`。

## <a name="usage"></a>使用法

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

ここで`<packageID>`をミラー化すると、パッケージまたは`<configFilePath>`を識別、`packages.config`をミラー化するパッケージの一覧を含むファイルです。

`<listUrlTarget>`ソース リポジトリを指定し、`<publishUrlTarget>`ターゲットのリポジトリを指定します。

場合は、ターゲットのリポジトリ`https://machine/repo`を実行している[NuGet.Server](../hosting-packages/nuget-server.md)、リストとプッシュ url になります`https://machine/repo/nuget`と`https://machine/repo/api/v2/package`、それぞれします。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットのリポジトリの API キー。 かどうか、存在していない構成ファイルで指定した期間が使用 (`%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux))。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NoCache | NuGet がキャッシュされているパッケージを使用するを防ぎます。 参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。 |
| noop | 新機能が不要になる行いません; 操作をログに記録します。プッシュ操作に成功した場合を想定しています。 |
| プレリリース版 | ミラーリングの操作では、プレリリースのパッケージが含まれています。 |
| ソース | ミラー化するパッケージ ソースの一覧です。 ものがで定義されているソースが指定されていない場合 nuget.org に既定の指定がない場合、構成ファイルを使用、(ApiKey 上記を参照してください)。 |
| Timeout | (秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。 既定では 300 秒 (5 分) です。 |
| Version | インストールするパッケージのバージョン。 指定しない場合、最新バージョンがミラー化されます。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
