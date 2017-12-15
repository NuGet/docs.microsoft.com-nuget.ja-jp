---
title: "NuGet CLI コマンドの削除 |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Nuget.exe delete コマンドのリファレンス"
keywords: "nuget の参照を削除、パッケージのコマンドを削除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a>delete コマンド (NuGet CLI)

**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:**すべて

削除またはパッケージ ソースからパッケージを unlists します。 Nuget.org、delete コマンドの[unlists パッケージ](../policies/Deleting-Packages.md)です。

## <a name="usage"></a>使用方法

```
nuget delete <packageID> <packageVersion> [options]
```

ここで`<packageID>`と`<packageVersion>`非公開または削除する正確なパッケージを識別します。 正確な動作は、ソースによって異なります。 ローカル フォルダー、たとえば、パッケージが削除される;nuget.org パッケージが一覧表示ではありません。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| apiKey | ターゲットのリポジトリの API キー。 存在しない場合、いずれかで指定されている*%AppData%\NuGet\NuGet.Config*を使用します。 |
| ConfigFile | *(2.5 +)* NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| 非対話型 | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| ソース | サーバー URL を指定します。 Nuget.org の URL は`https://api.nuget.org/v3/index.json`します。 たとえば、プライベート フィードは、置き換えるホスト名、 *%hostname%/api/v3*です。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>例

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
