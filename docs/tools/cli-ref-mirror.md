---
title: ミラーの NuGet CLI コマンド
description: Nuget.exe のミラー コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550207"
---
# <a name="mirror-command-nuget-cli"></a>mirror コマンド (NuGet CLI)

**適用対象:** パッケージの発行&bullet;**サポートされているバージョン:** 3.2 + で非推奨とされます

パッケージをターゲットのリポジトリを指定したソース リポジトリからその依存関係をミラー化します。

> [!NOTE]
> このコマンドは、NuGet のバージョン 3.2 の前に有効にするには[ https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)ダウンロード、最新の安定版リリースを選択`NuGet.ServerExtensions.dll`と`Nuget-Signed.exe`と、ローカル ディスクと名前の変更を`Nuget-Signed.exe`に`nuget.exe`。

## <a name="usage"></a>使用法

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

場所`<packageID>`を反映するには、パッケージまたは`<configFilePath>`識別、`packages.config`ミラー化するパッケージを一覧するファイル。

`<listUrlTarget>` 、ソース リポジトリを指定し、`<publishUrlTarget>`ターゲット リポジトリを指定します。

ターゲットのリポジトリがある場合`https://machine/repo`を実行している[NuGet.Server](../hosting-packages/nuget-server.md)、リストとプッシュの url になります`https://machine/repo/nuget`と`https://machine/repo/api/v2/package`、それぞれします。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットのリポジトリの API キー。 かどうか、存在していない、構成ファイルで指定された 1 つが使用されます (`%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux))。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NoCache | NuGet がキャッシュされたパッケージを使用するを防ぎます。 参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。 |
| Noop | ログに記録内容が行いますが、アクションは行われませんプッシュ操作の成功を前提としています。 |
| プレリリース版 | ミラーリングの操作では、プレリリース パッケージが含まれています。 |
| ソース | ミラー化するパッケージ ソースの一覧。 定義されているソースが指定されていない場合が指定されていない場合、nuget.org を既定値、構成ファイルが使用されます (ApiKey 上記を参照してください)。 |
| Timeout | サーバーにプッシュするための秒単位のタイムアウトを指定します。 既定では 300 秒 (5 分) です。 |
| Version | インストールするパッケージのバージョン。 指定しない場合、最新のバージョンがミラー化します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
