---
title: NuGet CLI spec コマンド
description: Nuget.exe spec コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327569"
---
# <a name="spec-command-nuget-cli"></a>spec コマンド (NuGet CLI)

**適用対象:** パッケージ作成&bullet;で**サポートされているバージョン:** すべて

新しいパッケージ`.nuspec`のファイルを生成します。 プロジェクトファイルと同じフォルダー (`.csproj`、 `.vbproj`、 `.fsproj`) で実行すると、 `spec`はトークン`.nuspec`化されたファイルを作成します。 詳細については、「[パッケージの作成](../../create-packages/creating-a-package.md)」を参照してください。

## <a name="usage"></a>使用法

```cli
nuget spec [<packageID>] [options]
```

ここ`<packageID>`で、は、 `.nuspec`ファイルに保存するオプションのパッケージ識別子です。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AssemblyPath | メタデータに使用するアセンブリへのパスを指定します。 |
| 必ず | 既存`.nuspec`のファイルを上書きします。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
