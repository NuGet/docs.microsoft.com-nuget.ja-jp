---
title: NuGet CLI の add コマンド
description: Nuget.exe の add コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 7a72186e1dece082cd200a03849a0b12c751a645
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327859"
---
# <a name="add-command-nuget-cli"></a>add コマンド (NuGet CLI)

**適用対象**: パッケージ発行&bullet;が**サポートされているバージョン**:3.3+

指定されたパッケージを非 HTTP パッケージソース (フォルダーまたは UNC パス) に階層構造で追加します。この場合、パッケージ ID とバージョン番号に対してフォルダーが作成されます。 例えば:

    \\myserver\packages
      └─<packageID>
        └─<version>
          ├─<packageID>.<version>.nupkg
          ├─<packageID>.<version>.nupkg.sha512
          └─<packageID>.nuspec

パッケージソースに対して復元または更新を行う場合、階層レイアウトはパフォーマンスを大幅に向上させます。

パッケージ内のすべてのファイルを目的のパッケージソースに展開するには`-Expand` 、スイッチを使用します。 通常、これにより、 `tools`や`lib`などの追加のサブフォルダーが変換先に表示されます。

## <a name="usage"></a>使用法

```cli
nuget add <packagePath> -Source <sourcePath> [options]
```

は、追加するパッケージのパス名です。は`<sourcePath>` 、パッケージの追加先となるフォルダーベースのパッケージソースを指定します。 `<packagePath>` HTTP ソースはサポートされていません。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| Expand | パッケージ内のすべてのファイルをパッケージソースに追加します。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget add foo.nupkg -Source c:\bar\

nuget add foo.nupkg -Source \\bar\packages\
```
