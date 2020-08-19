---
title: NuGet CLI spec コマンド
description: nuget.exe spec コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17603fa30a75c7906f867c96c5d77f31732eaa59
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622565"
---
# <a name="spec-command-nuget-cli"></a>spec コマンド (NuGet CLI)

**適用対象:** パッケージ作成で &bullet; **サポートされているバージョン:** すべて

`.nuspec`新しいパッケージのファイルを生成します。 プロジェクトファイルと同じフォルダー (、、) で実行すると `.csproj` `.vbproj` 、はトークン化 `.fsproj` `spec` されたファイルを作成し `.nuspec` ます。 詳細については、「 [パッケージの作成](../../create-packages/creating-a-package.md)」を参照してください。

## <a name="usage"></a>使用法

```cli
nuget spec [<packageID>] [options]
```

ここ `<packageID>` で、は、ファイルに保存するオプションのパッケージ識別子です `.nuspec` 。

## <a name="options"></a>Options

- **`-AssemblyPath`**

  メタデータに使用するアセンブリへのパスを指定します。

- **`-Force`**

  既存の `.nuspec` ファイルを上書きします。


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
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
