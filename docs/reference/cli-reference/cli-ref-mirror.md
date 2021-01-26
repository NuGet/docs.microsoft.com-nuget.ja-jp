---
title: NuGet CLI ミラーコマンド
description: nuget.exe mirror コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779179"
---
# <a name="mirror-command-nuget-cli"></a>mirror コマンド (NuGet CLI)

**適用対象:** パッケージ発行が &bullet; **サポートされているバージョン:** 3.2 以降では非推奨です。

指定されたソースリポジトリからターゲットリポジトリにパッケージとその依存関係をミラー化します。

> [!NOTE]
> 以前に NuGet 2.x でこのコマンドをサポートしていた NuGet.ServerExtensions.dll と NuGet-Signed.exe (NuGet-Signed.exe 名前を nuget.exe に変更) は、ダウンロードできなくなりました。 このようなコマンドを使用するには、 [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/)を試してください。

## <a name="usage"></a>使用方法

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

`<packageID>`は、ミラー化するパッケージ、または `<configFilePath>` ミラー化 `packages.config` するパッケージの一覧を示すファイルを指定します。

は `<listUrlTarget>` ソースリポジトリを指定し、は `<publishUrlTarget>` ターゲットリポジトリを指定します。

ターゲットリポジトリが、NuGet を実行しているである場合 `https://machine/repo` 、リストとプッシュ url は[](../../hosting-packages/nuget-server.md) `https://machine/repo/nuget` それぞれと `https://machine/repo/api/v2/package` になります。

## <a name="options"></a>Options

- **`-ApiKey`**

  ターゲットリポジトリの API キー。 存在しない場合は、構成ファイルで指定されているものが使用され `%AppData%\NuGet\NuGet.Config` ます ((Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux))。

- **`-Help`**

  コマンドのヘルプ情報を表示します。

- **`-NoCache`**

  NuGet がキャッシュされたパッケージを使用しないようにします。 「 [グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。

- **`-Noop`**

  実行される処理をログに記録しますが、アクションは実行しません。プッシュ操作の成功を想定します。

- **`-PreRelease`**

  ミラーリング操作にプレリリースパッケージを含めます。

- **`-Source`**

  ミラー化するパッケージソースの一覧。 ソースが指定されていない場合は、構成ファイルで定義されているもの (上記の ApiKey を参照) が使用され、何も指定されていない場合は nuget.org が既定値となります。

- **`-Timeout`**

  サーバーにプッシュするときのタイムアウトを秒単位で指定します。 設定値の既定は 300 秒 (5 分) です。

- **`-Version`**

  インストールするパッケージのバージョン。 指定しない場合、最新バージョンがミラー化されます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
