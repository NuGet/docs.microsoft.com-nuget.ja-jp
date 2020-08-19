---
title: NuGet CLI の追加コマンド
description: nuget.exe add コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 89d268946243e8eae07e482db48e809a15260c38
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622903"
---
# <a name="add-command-nuget-cli"></a>コマンドの追加 (NuGet CLI)

**適用対象**: パッケージ発行が &bullet; **サポートされているバージョン**: 3.3 以降

指定されたパッケージを非 HTTP パッケージソース (フォルダーまたは UNC パス) に階層構造で追加します。この場合、パッケージ ID とバージョン番号に対してフォルダーが作成されます。 次に例を示します。

```
\\myserver\packages
  └─<packageID>
    └─<version>
      ├─<packageID>.<version>.nupkg
      ├─<packageID>.<version>.nupkg.sha512
      └─<packageID>.nuspec
```

パッケージソースに対して復元または更新を行う場合、階層レイアウトはパフォーマンスを大幅に向上させます。

パッケージ内のすべてのファイルを目的のパッケージソースに展開するには、スイッチを使用し `-Expand` ます。 通常、これにより、やなどの追加のサブフォルダーが変換先に表示され `tools` `lib` ます。

## <a name="usage"></a>使用法

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

`<packagePath>`は、追加するパッケージのパス名です。は、 `<sourcePath>` パッケージの追加先となるフォルダーベースのパッケージソースを指定します。 HTTP ソースはサポートされていません。

## <a name="options"></a>Options

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-Expand`**

  パッケージ内のすべてのファイルをパッケージソースに追加します。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。
不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-src|-Source`**

   Nupkg を追加するフォルダーまたは UNC 共有のパッケージソースを指定します。 Http ソースはサポートされていません。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
