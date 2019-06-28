---
title: NuGet CLI config コマンド
description: Nuget.exe の config コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: c0497c7b99a2de6bee37d6d0ead8b055578e60b7
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426069"
---
# <a name="config-command-nuget-cli"></a>configコマンド (NuGet CLI)

**適用対象:** すべて&bullet;**サポートされているバージョン**: すべて

取得または NuGet の構成値を設定します。 追加の使用状況は、次を参照してください。[一般的な NuGet 構成](../consume-packages/configuring-nuget-behavior.md)します。 詳細については、使用可能なキー名を参照してください、 [NuGet 構成ファイル リファレンス](../reference/nuget-config-file.md)します。

## <a name="usage"></a>使用法

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

場所`<name>`と`<value>`構成で設定するキー/値ペアを指定します。 必要に応じて、多くのペアを指定できます。 値を削除するには、名前を指定し、`=`記号が、値はありません。

使用可能なキー名では、次を参照してください。、 [NuGet 構成ファイル リファレンス](../reference/nuget-config-file.md)します。

NuGet 3.4 以降で`<value>`使える[環境変数](cli-ref-environment-variables.md)します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AsPath | ときに、パスとして、構成の値を返しますが無視されます`-Set`使用されます。 |
| ConfigFile | NuGet 構成ファイルを変更します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *静か*、*詳細* |

参照してください[環境変数](cli-ref-environment-variables.md)

### <a name="examples"></a>使用例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
