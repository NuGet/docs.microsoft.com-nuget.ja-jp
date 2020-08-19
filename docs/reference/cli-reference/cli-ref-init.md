---
title: NuGet CLI の init コマンド
description: nuget.exe init コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3b830d678a473c917b70bd46900bdb0206d3652e
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623085"
---
# <a name="init-command-nuget-cli"></a>init コマンド (NuGet CLI)

**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** 3.3 以降

[ [追加] コマンド](cli-ref-add.md)の説明に従って階層構造を使用して、フラットフォルダーのすべてのパッケージをコピー先フォルダーにコピーします。 つまり、を使用 `init` することは、 `add` フォルダー内の各パッケージに対してコマンドを使用することと同じです。

と同様に、 `add` コピー先はローカルフォルダーまたは UNC パスである必要があります。Nuget.org やプライベートサーバーなどの HTTP パッケージリポジトリはサポートされていません。

## <a name="usage"></a>使用法

```cli
nuget init <source> <destination> [options]
```

ここで、 `<source>` はパッケージを含むフォルダーで、 `<destination>` はパッケージのコピー先のローカルフォルダーまたは UNC パス名です。

## <a name="options"></a>Options

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-Expand`**

  パッケージソースに追加された各パッケージ内のすべてのファイルを追加します。コマンドと同じ `-Expand` `add` です。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget init c:\foo c:\bar
nuget init \\foo\packages \\bar\packages -Expand
```
