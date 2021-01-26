---
title: NuGet CLI 構成コマンド
description: nuget.exe config コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3d50c12e34f71d7a62fe177da1dbb33eb702347a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775956"
---
# <a name="config-command-nuget-cli"></a>config コマンド (NuGet CLI)

**適用対象:** &bullet; **サポートされている** すべてのバージョン: すべて

NuGet 構成値を取得または設定します。 その他の使用方法については、「 [Common NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。 使用可能なキー名の詳細については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。

## <a name="usage"></a>使用方法

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

とは、 `<name>` `<value>` 構成で設定されるキーと値のペアを指定します。 必要に応じて、ペアをいくつでも指定できます。 値を削除するには、名前と符号を指定しますが、値は指定し `=` ません。

使用可能なキー名については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。

NuGet 3.4 以降で `<value>` は、は [環境変数](cli-ref-environment-variables.md)を使用できます。

## <a name="options"></a>Options


- **`AsPath`**

  構成値をパスとして返し `-Set` ます。が使用されている場合は無視されます。

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-Set`**

  1つは config で設定されるキーと値のペアの数です。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

### <a name="examples"></a>使用例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
