---
title: NuGet CLI setapikey コマンド
description: nuget.exe setapikey コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780024"
---
# <a name="setapikey-command-nuget-cli"></a>setapikey コマンド (NuGet CLI)

**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン** の発行: すべて

指定されたサーバー URL の API キーをに保存して、 `NuGet.Config` 後続のコマンドに入力する必要がないようにします。

## <a name="usage"></a>使用方法

```cli
nuget setapikey <key> -Source <url> [options]
```

`<source>`はサーバーを識別し、 `<key>` は保存するキーです。 を省略した場合 `<source>` 、nuget.org が想定されます。 

> [!NOTE]
> API キーは、プライベート フィードでの認証には使用されません。 ソースで認証するための資格情報を管理するには、[`nuget sources` コマンド](../cli-reference/cli-ref-sources.md)を参照してください。
> API キーは、個々の NuGet サーバーから取得できます。 Nuget.org の APIKeys を作成して管理するには、 [api キーを取得](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)する

## <a name="options"></a>Options

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-src|-Source`**

  API キーが有効なサーバー URL。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
