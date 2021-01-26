---
title: NuGet CLI の削除コマンド
description: nuget.exe delete コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 96c75366ae69b34f5cd1f55feb53087b5d0ea324
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775954"
---
# <a name="delete-command-nuget-cli"></a>delete コマンド (NuGet CLI)

**適用対象:** パッケージ発行の &bullet; **サポートされているバージョン:** すべて

パッケージソースからパッケージを削除または一覧から削除します。 Nuget.org の場合、delete コマンドを実行すると、 [パッケージの一覧](../../nuget-org/policies/deleting-packages.md)が解除されます。

## <a name="usage"></a>使用方法

```cli
nuget delete <packageID> <packageVersion> [options]
```

`<packageID>`と `<packageVersion>` は、削除するパッケージまたは一覧から削除を指定します。 実際の動作は、ソースによって異なります。 たとえば、ローカルフォルダーの場合、パッケージは削除されます。nuget.org の場合、パッケージは一覧から削除されます。

## <a name="options"></a>Options

- **`-ApiKey`**

  ターゲットリポジトリの API キー。 存在しない場合は、構成ファイルで指定されたものが使用されます。

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

 - **`-np|-NoPrompt`**

   削除時にメッセージを表示しません。

 - **`-NoServiceEndpoint`** ソース URL に "api/v2/packages" を追加しません。

- **`-src|-Source`**

  サーバー URL を指定します。 Nuget.org の URL は `https://api.nuget.org/v3/index.json` です。 プライベートフィードの場合は、ホスト名に置き換えます (例 *% hostname%/api/v3*)。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
