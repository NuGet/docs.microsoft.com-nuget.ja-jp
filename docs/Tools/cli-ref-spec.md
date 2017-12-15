---
title: "NuGet CLI 仕様コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Nuget.exe spec コマンドのリファレンス"
keywords: "nuget spec 参照、spec コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>spec コマンド (NuGet CLI)

**適用されます:**パッケージの作成&bullet;**サポートされているバージョン:**すべて

生成、`.nuspec`新しいパッケージのファイルです。 プロジェクト ファイルと同じフォルダーで実行された場合 (`.csproj`、 `.vbproj`、 `.fsproj`)、 `spec` 、トークン化された作成`.nuspec`ファイル。 詳細については、次を参照してください。[パッケージを作成する](../create-packages/creating-a-package.md)です。

## <a name="usage"></a>使用方法

```
nuget spec [<packageID>] [options]
```

ここで`<packageID>`で保存する省略可能なパッケージ識別子、`.nuspec`ファイル。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AssemblyPath | メタデータに使用するアセンブリへのパスを指定します。 |
| Force | 既存のすべてを上書き`.nuspec`ファイル。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| 非対話型 | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>例

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
