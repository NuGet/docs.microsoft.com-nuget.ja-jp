---
title: NuGet CLI コマンドを追加します。
description: コマンドを追加、nuget.exe への参照
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f229ca100463c556f9c4cefc49f52724a9c4ba77
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817611"
---
# <a name="add-command-nuget-cli"></a>addコマンド (NuGet CLI)

**適用されます**: パッケージの発行&bullet;**サポートされているバージョン**: 3.3 +

指定したパッケージをパッケージ ID とバージョン番号のフォルダーを作成する場合、階層構造での HTTP 以外のパッケージ ソース (フォルダーまたは UNC パス) に追加します。 例えば:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

復元すると、パッケージ ソースに対して更新階層構造は、パフォーマンスが著しく向上を提供します。

変換先のパッケージ ソースに、パッケージ内のすべてのファイルを拡張しを使用して、`-Expand`スイッチします。 など、変換先に表示される他のサブフォルダーでこの結果、ほとんど`tools`と`lib`です。

## <a name="usage"></a>使用法

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

ここで`<packagePath>`を追加するためのパッケージへのパス名と`<sourcePath>`パッケージの追加先となるフォルダーに基づくパッケージのソースを指定します。 HTTP ソースはサポートされていません。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| Expand | パッケージ ソースに、パッケージ内のすべてのファイルを追加します。 |
| ForceEnglishOutput | *(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
