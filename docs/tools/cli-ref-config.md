---
title: NuGet CLI config コマンド
description: Nuget.exe の config コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 376b69186ad22d4d94a1df51146b833a1f6f9bd9
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546479"
---
# <a name="config-command-nuget-cli"></a>configコマンド (NuGet CLI)

**適用対象:** すべて&bullet;**サポートされているバージョン**: すべて

取得または NuGet の構成値を設定します。 追加の使用状況は、[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)を参照してください。 詳細については、使用可能なキー名を参照してください、 [NuGet 構成ファイル リファレンス](../reference/nuget-config-file.md)します。

## <a name="usage"></a>使用法

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

場所`<name>`と`<value>`構成で設定するキー/値ペアを指定します。 必要に応じて、多くのペアを指定できます。 値を削除するには、名前を指定し、`=`記号が、値はありません。

使用可能なキー名では、、 [NuGet 構成ファイル リファレンス](../reference/nuget-config-file.md)を参照してください。

NuGet 3.4 以降で`<value>`使える[環境変数](cli-ref-environment-variables.md)します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AsPath | ときに、パスとして、構成の値を返しますが無視されます`-Set`使用されます。 |
| ConfigFile | NuGet 構成ファイルを変更します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

### <a name="examples"></a>使用例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
