---
title: "NuGet CLI ミラー コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 190d7010-172e-44b8-8a32-94a2a63be4f3
description: "Nuget.exe ミラー コマンドのリファレンス"
keywords: "nuget ミラー参照、ミラー コマンドです。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 67daa1aa278b42b7974c562ba4097a525e7bb105
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="mirror-command-nuget-cli"></a>[ミラー] (NuGet CLI)

**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:** 3.2 以降で廃止されました

パッケージとターゲットのリポジトリに指定されたソース リポジトリからその依存関係を反映します。

> [!NOTE]
> このコマンドは、NuGet のバージョン 3.2 の前に有効にするには[https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases)を最新の安定版リリースを選択し、ダウンロード`NuGet.ServerExtensions.dll`と`Nuget-Signed.exe`、ローカル ディスクと名前の変更に`Nuget-Signed.exe`に`nuget.exe`.

## <a name="usage"></a>使用方法

```
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

ここで`<packageID>`をミラー化すると、パッケージまたは`<configFilePath>`を識別、`packages.config`をミラー化するパッケージの一覧を含むファイルです。

`<listUrlTarget>`ソース リポジトリを指定し、`<publishUrlTarget>`ターゲットのリポジトリを指定します。

場合は、ターゲットのリポジトリ`https://machine/repo`を実行している[NuGet.Server](../hosting-packages/NuGet-Server.md)、リストとプッシュ url になります`https://machine/repo/nuget`と`https://machine/repo/api/v2/package`、それぞれします。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| apiKey | ターゲットのリポジトリの API キー。 存在しない場合、いずれかで指定されている*%AppData%\NuGet\NuGet.Config*を使用します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NoCache | NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。 |
| noop | 新機能が不要になる行いません; 操作をログに記録します。プッシュ操作に成功した場合を想定しています。 |
| プレリリース版 | ミラーリングの操作では、プレリリースのパッケージが含まれています。 |
| ソース | ミラー化するパッケージ ソースの一覧です。 ものがで定義されているソースが指定されていない場合*%AppData%\NuGet\NuGet.Config*が使用すると、指定がない場合は、nuget.org を既定とします。 |
| Timeout | (秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。 既定では 300 秒 (5 分) です。 |
| Version | インストールするパッケージのバージョン。 指定しない場合、最新バージョンがミラー化されます。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>例

```
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
