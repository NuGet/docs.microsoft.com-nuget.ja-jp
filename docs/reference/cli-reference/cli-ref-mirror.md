---
title: NuGet CLI の mirror コマンド
description: Nuget.exe mirror コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327669"
---
# <a name="mirror-command-nuget-cli"></a>mirror コマンド (NuGet CLI)

**適用対象:** パッケージ発行&bullet;が**サポートされているバージョン:** 3.2 以降では非推奨です。

指定されたソースリポジトリからターゲットリポジトリにパッケージとその依存関係をミラー化します。

> [!NOTE]
> 3\.2 より前のバージョンの NuGet でこのコマンドを有効[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)にするには、にアクセスして`Nuget-Signed.exe` 最新の安定版リリースを選択し、をダウンロードしてローカルディスクにダウンロード`NuGet.ServerExtensions.dll` し、名前をに`nuget.exe` 変更`Nuget-Signed.exe` します。

## <a name="usage"></a>使用法

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

は、ミラー化するパッケージ、また`<configFilePath>`はミラー `packages.config`化するパッケージの一覧を示すファイルを指定します。 `<packageID>`

は`<listUrlTarget>`ソースリポジトリ`<publishUrlTarget>`を指定し、はターゲットリポジトリを指定します。

ターゲットリポジトリが、 [NuGet](../../hosting-packages/nuget-server.md)を`https://machine/repo`実行しているである場合、リストと`https://machine/repo/nuget`プッシュ url はそれぞれと`https://machine/repo/api/v2/package`になります。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットリポジトリの API キー。 存在しない場合は、構成ファイルで指定されている`%AppData%\NuGet\NuGet.Config`ものが使用さ`~/.nuget/NuGet/NuGet.Config`れます ((Windows) または (Mac/Linux))。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NoCache | NuGet がキャッシュされたパッケージを使用しないようにします。 「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。 |
| Noop | 実行される処理をログに記録しますが、アクションは実行しません。プッシュ操作の成功を想定します。 |
| PreRelease | ミラーリング操作にプレリリースパッケージを含めます。 |
| Source | ミラー化するパッケージソースの一覧。 ソースが指定されていない場合は、構成ファイルで定義されているもの (上記の ApiKey を参照) が使用され、何も指定されていない場合は nuget.org が既定値となります。 |
| Timeout | サーバーにプッシュするときのタイムアウトを秒単位で指定します。 既定値は300秒 (5 分) です。 |
| Version | インストールするパッケージのバージョン。 指定しない場合、最新バージョンがミラー化されます。 |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
