---
title: NuGet CLI 構成コマンド
description: Nuget.exe config コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 384e708187a747221de103720cc51af07acf713e
ms.sourcegitcommit: f9e39ff9ca19ba4a26e52b8a5e01e18eb0de5387
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/24/2019
ms.locfileid: "68433315"
---
# <a name="config-command-nuget-cli"></a>configコマンド (NuGet CLI)

**適用対象:** &bullet; **サポートされている**すべてのバージョン: すべて

NuGet 構成値を取得または設定します。 その他の使用方法については、「 [Common NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。 使用可能なキー名の詳細については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。

## <a name="usage"></a>使用法

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

`<name>` と`<value>`は、構成で設定されるキーと値のペアを指定します。 必要に応じて、ペアをいくつでも指定できます。 値を削除するには、名前と`=`符号を指定しますが、値は指定しません。

使用可能なキー名については、 [NuGet 構成ファイルのリファレンス](../nuget-config-file.md)を参照してください。

NuGet 3.4 以降では`<value>` 、は[環境変数](cli-ref-environment-variables.md)を使用できます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AsPath | 構成値をパスとして返します。 `-Set`が使用されている場合は無視されます。 |
| ConfigFile | 変更する NuGet 構成ファイル。 指定しない場合、既定のファイル (Windows`%AppData%\NuGet\NuGet.Config` ) また`~/.config/NuGet/NuGet.Config`は (Mac/Linux) または`~/.nuget/NuGet/NuGet.Config` (OS の配布によって異なる) が使用されます。|
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed* |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

### <a name="examples"></a>使用例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
