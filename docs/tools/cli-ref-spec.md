---
title: NuGet CLI 仕様コマンド
description: Nuget.exe spec コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817087"
---
# <a name="spec-command-nuget-cli"></a>spec コマンド (NuGet CLI)

**適用されます:** パッケージの作成&bullet;**サポートされているバージョン:** すべて

生成、`.nuspec`新しいパッケージのファイルです。 プロジェクト ファイルと同じフォルダーで実行された場合 (`.csproj`、 `.vbproj`、 `.fsproj`)、 `spec` 、トークン化された作成`.nuspec`ファイル。 詳細については、次を参照してください。[パッケージを作成する](../create-packages/creating-a-package.md)です。

## <a name="usage"></a>使用法

```cli
nuget spec [<packageID>] [options]
```

ここで`<packageID>`で保存する省略可能なパッケージ識別子、`.nuspec`ファイル。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AssemblyPath | メタデータに使用するアセンブリへのパスを指定します。 |
| Force | 既存のすべてを上書き`.nuspec`ファイル。 |
| ForceEnglishOutput | *(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
