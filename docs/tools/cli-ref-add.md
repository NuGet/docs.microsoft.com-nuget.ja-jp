---
title: NuGet CLI コマンドを追加します。
description: Nuget.exe への参照の追加コマンド
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545835"
---
# <a name="add-command-nuget-cli"></a>addコマンド (NuGet CLI)

**適用対象**: パッケージの発行&bullet;**サポートされているバージョン**: 3.3 以降

パッケージ ID とバージョン番号のフォルダーを作成する場合、階層構造で、HTTP 以外のパッケージ ソース (フォルダーまたは UNC パス) には、指定したパッケージを追加します。 例えば:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

復元またはパッケージのソースに対して更新をするとき、階層構造は、パフォーマンスが著しく向上を提供します。

変換先のパッケージ ソースをパッケージ内のすべてのファイルを展開するには、使用、`-Expand`スイッチします。 これは通常など、変換先に表示されている他のサブフォルダーになります`tools`と`lib`します。

## <a name="usage"></a>使用法

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

場所`<packagePath>`を追加するパッケージへのパス名と`<sourcePath>`パッケージの追加先となるフォルダー ベースのパッケージ ソースを指定します。 HTTP ソースがサポートされていません。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| Expand | パッケージ ソースには、パッケージ内のすべてのファイルを追加します。 |
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
