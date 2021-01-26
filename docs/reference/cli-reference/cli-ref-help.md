---
title: NuGet CLI のヘルプコマンド
description: nuget.exe ヘルプコマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5d91638c4a6f167ea8a04e5dfa2905cb55084ddd
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779353"
---
# <a name="help-or--command-nuget-cli"></a>help または ? コマンド (NuGet CLI)

**適用対象:** &bullet; **サポートされている** すべてのバージョン: すべて

特定のコマンドに関する一般的なヘルプ情報とヘルプ情報を表示します。

## <a name="usage"></a>使用方法

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

ここで [command] は、ヘルプを表示する特定のコマンドを識別します。

> [!Warning]
> 一部のコマンドでは、  `nuget help install` nuget.org に "help" という名前のパッケージが存在するので、最初にヘルプを指定することに注意してください。コマンドを指定した場合 `nuget install help` 、install コマンドのヘルプは表示されませんが、help という名前のパッケージがインストールされます。

## <a name="options"></a>Options

- **`-All`**

  使用可能なすべてのコマンドの詳細なヘルプを印刷します。特定のコマンドが指定されている場合は無視されます。

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-Markdown`**

  で使用する場合は、markdown 形式の詳細なヘルプを印刷 `-All` します。 それ以外の場合は無視されます。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
