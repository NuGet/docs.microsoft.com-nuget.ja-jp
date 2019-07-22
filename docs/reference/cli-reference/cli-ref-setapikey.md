---
title: NuGet CLI setapikey コマンド
description: Nuget.exe setapikey コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327609"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey コマンド (NuGet CLI)

**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン**の発行: すべて

指定されたサーバー URL の API キーを`NuGet.Config`に保存して、後続のコマンドに入力する必要がないようにします。

## <a name="usage"></a>使用法

```cli
nuget setapikey <key> -Source <url> [options]
```

はサーバーを`<key>`識別し、は保存するキーまたはパスワードです。 `<source>` を`<source>`省略した場合、nuget.org が想定されます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、 *quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
