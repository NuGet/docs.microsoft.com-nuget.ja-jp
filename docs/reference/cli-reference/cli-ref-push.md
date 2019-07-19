---
title: NuGet CLI プッシュコマンド
description: Nuget.exe push コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 40b2b2970934bae82c46cbe69156948e90746f97
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327629"
---
# <a name="push-command-nuget-cli"></a>push コマンド (NuGet CLI)

**適用対象:** パッケージ発行&bullet;が**サポートされているバージョン:** すべて。 nuget.org には、4.1.0 以降が必要です。

> [!Important]
> パッケージを nuget.org にプッシュするには、必要な[nuget プロトコル](../../api/nuget-protocols.md)を実装する nuget.exe v2.0 を使用する必要があります。

パッケージをパッケージソースにプッシュして発行します。

NuGet の既定の構成を取得する`%AppData%\NuGet\NuGet.Config`には`.nuget\Nuget.Config` 、( `~/.nuget/NuGet/NuGet.Config` Windows) または (Mac/Linux `Nuget.Config` ) を読み込み、ドライブのルートから開始し、現在のディレクトリで終了します ([一般的な nuget を参照してください)。構成](../../consume-packages/configuring-nuget-behavior.md))

## <a name="usage"></a>使用法

```cli
nuget push <packagePath> [options]
```

は、サーバーにプッシュするパッケージを識別します。`<packagePath>`

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットリポジトリの API キー。 存在しない場合は、構成ファイルで指定されたものが使用されます。 |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| DisableBuffering | メモリ使用量を減らすために HTTP (s) サーバーにプッシュするときのバッファー処理を無効にします。 注意: このオプションを使用すると、統合 Windows 認証が機能しない可能性があります。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| NoSymbols | *(3.5 +)* シンボルパッケージが存在する場合は、シンボルサーバーにプッシュされません。 |
| Source | サーバー URL を指定します。 NuGet は UNC またはローカルフォルダーソースを識別し、HTTP を使用してプッシュするのではなく、そこにファイルをコピーするだけです。  また、nuget 3.4.2 以降では、ファイルで`NuGet.Config` *defaultpushsource*値が指定されていない限り、これは必須パラメーターです (「 [NuGet の動作の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください)。 |
| SkipDuplicate | *(5.1 以降)* パッケージとバージョンが既に存在する場合は、スキップして、プッシュ時に次のパッケージを続行します (存在する場合)。 |
| SymbolSource | *(3.5 +)* シンボルサーバーの URL を指定します。nuget.smbsrc.net は、nuget.org にプッシュするときに使用されます。 |
| SymbolApiKey | *(3.5 +)* で`-SymbolSource`指定された URL の API キーを指定します。 |
| Timeout | サーバーにプッシュするときのタイムアウトを秒単位で指定します。 既定値は300秒 (5 分) です。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

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

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
