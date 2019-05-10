---
title: NuGet CLI push コマンド
description: Nuget.exe push コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 4a9460944e2c232e2a72195434a491d26eee3559
ms.sourcegitcommit: 3fc93f7a64be040699fe12125977dd25a7948470
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/29/2019
ms.locfileid: "64877956"
---
# <a name="push-command-nuget-cli"></a>プッシュ コマンド (NuGet CLI)

**適用されます:** パッケージ公開&bullet;**サポートされているバージョン:** すべて; nuget.org に必要な 4.1.0 以降

> [!Important]
> Nuget.org にパッケージをプッシュするを使用する必要があります nuget.exe v4.1.0 以降、実装に必要な[NuGet プロトコル](../api/nuget-protocols.md)します。

パッケージ ソースに、パッケージをプッシュして発行します。

NuGet の既定の構成が読み込むことによって取得`%AppData%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) が、読み込み、`Nuget.Config`または`.nuget\Nuget.Config`ドライブのルートから開始し、現在のディレクトリで終わるファイル (を参照してください[構成NuGet の動作を](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>使用法

```cli
nuget push <packagePath> [options]
```

場所`<packagePath>`サーバーにプッシュするパッケージを識別します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットのリポジトリの API キー。 存在しない場合は、構成ファイルで指定された 1 つが使用されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| DisableBuffering | メモリの使用量を減らす、http (s) サーバーにプッシュするときのバッファリングを無効にします。 注意: このオプションを使用すると、統合 Windows 認証が機能しません。 |
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| シンボルなし | *(3.5 以降)* シンボル パッケージが存在する場合にプッシュされませんシンボル サーバーにします。 |
| ソース | サーバー URL を指定します。 NuGet では、UNC またはローカル フォルダーのソースを識別し、単純に HTTP を使用してプッシュではなく、ファイルの存在をコピーします。  また、NuGet 3.4.2 以降、これは、必須パラメーターしない限り、`NuGet.Config`ファイルを指定します、 *DefaultPushSource*値 (を参照してください[NuGet の構成の動作を](../consume-packages/configuring-nuget-behavior.md))。 |
| SymbolSource | *(3.5 以降)* シンボル サーバーの URL を指定します nuget.org にプッシュするときに nuget.smbsrc.net が使用されます。 |
| SymbolApiKey | *(3.5 以降)* で指定された URL の API キーを指定します`-SymbolSource`します。 |
| Timeout | サーバーにプッシュするための秒単位のタイムアウトを指定します。 既定では 300 秒 (5 分) です。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

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

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/
```
