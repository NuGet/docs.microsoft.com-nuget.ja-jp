---
title: NuGet CLI 仕様コマンド
description: Nuget.exe spec コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 68b165751ab6794d2a01d7e466619b1ce4d7ed72
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546450"
---
# <a name="spec-command-nuget-cli"></a>spec コマンド (NuGet CLI)

**適用対象:** パッケージの作成&bullet;**サポートされているバージョン:** すべて

生成、`.nuspec`新しいパッケージのファイル。 プロジェクト ファイルと同じフォルダーで実行された場合 (`.csproj`、 `.vbproj`、 `.fsproj`)、`spec`をトークン化された作成`.nuspec`ファイル。 詳細については、次を参照してください。[パッケージを作成する](../create-packages/creating-a-package.md)します。

## <a name="usage"></a>使用法

```cli
nuget spec [<packageID>] [options]
```

場所`<packageID>`で保存するオプションのパッケージ識別子、`.nuspec`ファイル。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AssemblyPath | メタデータに使用するアセンブリへのパスを指定します。 |
| Force | 既存のすべての上書き`.nuspec`ファイル。 |
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
