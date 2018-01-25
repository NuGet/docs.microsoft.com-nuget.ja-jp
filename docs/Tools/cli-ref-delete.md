---
title: "NuGet CLI コマンドの削除 |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe delete コマンドのリファレンス"
keywords: "nuget の参照を削除、パッケージのコマンドを削除"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a>delete コマンド (NuGet CLI)

**適用されます:**パッケージの発行&bullet;**サポートされているバージョン:**すべて

削除またはパッケージ ソースからパッケージを unlists します。 Nuget.org、delete コマンドの[unlists パッケージ](../policies/Deleting-Packages.md)です。

## <a name="usage"></a>使用法

```cli
nuget delete <packageID> <packageVersion> [options]
```

ここで`<packageID>`と`<packageVersion>`非公開または削除する正確なパッケージを識別します。 正確な動作は、ソースによって異なります。 ローカル フォルダー、たとえば、パッケージが削除される;nuget.org パッケージが一覧表示ではありません。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ApiKey | ターゲットのリポジトリの API キー。 存在しない場合、いずれかで指定されている*%AppData%\NuGet\NuGet.Config*を使用します。 |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| ソース | サーバー URL を指定します。 Nuget.org の URL は`https://api.nuget.org/v3/index.json`します。 たとえば、プライベート フィードは、置き換えるホスト名、 *%hostname%/api/v3*です。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
