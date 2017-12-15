---
title: "NuGet CLI プッシュ コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: a9709eee-add2-47fb-98e6-eec0697087f6
description: "Nuget.exe プッシュ コマンドのリファレンス"
keywords: "nuget プッシュ参照、プッシュ コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2828cdc41903d8a948870155b23721724bfa781e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="push-command-nuget-cli"></a>push コマンド (NuGet CLI)

**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:**すべて; nuget.org に必要な 4.1.0+

> [!Important]
> Nuget.org をパッケージにプッシュするを使用する必要があります nuget.exe v4.1.0 以降、必須を実装する[NuGet プロトコル](../api/nuget-protocols.md)です。

パッケージをパッケージ ソースにプッシュし、それを公開します。

NuGet の既定の構成を読み込むことにより取得`%AppData%\NuGet\NuGet.Config`、読み込み時、`Nuget.Config`または`.nuget\Nuget.Config`ドライブのルートから開始し、現在のディレクトリで終わるファイル (を参照してください[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>使用方法

```
nuget push <packagePath> [options]
```

ここで`<packagePath>`サーバーにプッシュするパッケージを識別します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| apiKey | ターゲットのリポジトリの API キー。 存在しない場合、いずれかで指定されている*%AppData%\NuGet\NuGet.Config*を使用します。 |
| ConfigFile | *(2.5 +)* NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| DisableBuffering | メモリの使用量を削減する http (s) サーバーへのプッシュ時にバッファー処理を無効にします。 注意: このオプションを使用すると、統合 Windows 認証動かないことがあります。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| 非対話型 | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| シンボルなし | *(3.5 +)*シンボル パッケージが存在する場合にプッシュされませんシンボル サーバーにします。 |
| ソース | サーバー URL を指定します。 NuGet 2.5 以降を使用 NuGet は UNC またはローカル フォルダーのソースを特定し、単に HTTP を使用して、プッシュされずにあるファイルをコピーします。  また、NuGet 3.4.2 から始めて、これは必須のパラメーターを除いて、`NuGet.Config`ファイルを指定します、 *DefaultPushSource*値 (を参照してください[構成 NuGet 動作](../Consume-Packages/Configuring-NuGet-Behavior.md))。 |
| SymbolSource | *(3.5 +)*シンボル サーバーの URL を指定します; は、プッシュ nuget.org するときに使用する nuget.smbsrc.net |
| SymbolApiKey | *(3.5 +)*で指定された URL では、API キーを指定`-SymbolSource`です。 |
| Timeout | (秒単位) をサーバーにプッシュするためのタイムアウト値を指定します。 既定では 300 秒 (5 分) です。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>例

```
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
