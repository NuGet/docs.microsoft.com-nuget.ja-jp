---
title: NuGet CLI ローカルコマンド
description: nuget.exe のローカルコマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 25feb29c7b96c47681cedd8208b8595952d3ca49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779202"
---
# <a name="locals-command-nuget-cli"></a>[ローカル] コマンド (NuGet CLI)

**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 3.3 以降

*Http キャッシュ*、*グローバルパッケージ* フォルダー、一時フォルダーなどのローカル NuGet リソースをクリアまたは一覧表示します。 また、コマンドを使用して、 `locals` これらの場所の一覧を表示することもできます。 詳細については、「 [グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」を参照してください。

## <a name="usage"></a>使用方法

```cli
nuget locals <folder> [options]
```

ここで、 `<folder>` は `all` 、 `http-cache` 、 `packages-cache` *(3.5 以前)*、 `global-packages` 、 `temp` *(3.4 +)*、および `plugins-cache` *(4.8 +)* のいずれかです。

## <a name="options"></a>Options

- **`-Clear`**

  指定されたフォルダーをクリアします。

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-List`**

  指定したフォルダーの場所、または *すべて* のフォルダーを使用する場合はすべてのフォルダーの場所を一覧表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>例

```cli
nuget locals all -list
nuget locals http-cache -clear
```

その他の例については、「 [グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」を参照してください。
