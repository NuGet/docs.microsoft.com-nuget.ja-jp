---
title: NuGet CLI プッシュ コマンド
description: Nuget.exe プッシュ コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817192"
---
# <a name="push-command-nuget-cli"></a>push コマンド (NuGet CLI)

**適用されます:** パッケージの発行&bullet;**サポートされているバージョン:** すべて; nuget.org に必要な 4.1.0+

> [!Important]
> Nuget.org をパッケージにプッシュするを使用する必要があります nuget.exe v4.1.0 以降、必須を実装する[NuGet プロトコル](../api/nuget-protocols.md)です。

パッケージをパッケージ ソースにプッシュし、それを公開します。

NuGet の既定の構成を読み込むことにより取得`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) が、読み込み、`Nuget.Config`または`.nuget\Nuget.Config`ドライブのルートから開始し、現在のディレクトリで終わるファイル (を参照してください[構成NuGet 動作](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>使用法

```cli
nuget push <packagePath> [options]
```

ここで`<packagePath>`サーバーにプッシュするパッケージを識別します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットのリポジトリの API キー。 存在しない場合は、構成ファイルで指定されているが使用されます。 |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| DisableBuffering | メモリの使用量を削減する http (s) サーバーへのプッシュ時にバッファー処理を無効にします。 注意: このオプションを使用すると、統合 Windows 認証動かないことがあります。 |
| ForceEnglishOutput | *(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| シンボルなし | *(3.5 +)* シンボル パッケージが存在する場合にプッシュされませんシンボル サーバーにします。 |
| ソース | サーバー URL を指定します。 NuGet は、UNC またはローカル フォルダーのソースを識別し、単に HTTP を使用して、プッシュされずにあるファイルをコピーします。  また、NuGet 3.4.2 から始めて、これは必須のパラメーターを除いて、`NuGet.Config`ファイルを指定します、 *DefaultPushSource*値 (を参照してください[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md))。 |
| SymbolSource | *(3.5 +)* シンボル サーバーの URL を指定します; は、プッシュ nuget.org するときに使用する nuget.smbsrc.net |
| SymbolApiKey | *(3.5 +)* で指定された URL では、API キーを指定`-SymbolSource`です。 |
| Timeout | (秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。 既定では 300 秒 (5 分) です。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
