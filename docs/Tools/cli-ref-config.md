---
title: "NuGet CLI config コマンド |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe config コマンドのリファレンス"
keywords: "nuget config 参照、config コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 34d156a29207122bac3c21c3307cbe7373b5f031
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="config-command-nuget-cli"></a>config コマンド (NuGet CLI)

**適用されます:**すべて&bullet;**サポートされているバージョン**: すべて

取得または NuGet の構成値を設定します。 追加の使用率は、次を参照してください。 [NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)です。 使用可能なキー名の詳細についてを参照してください、 [NuGet config ファイル参照](../reference/nuget-config-file.md)です。

## <a name="usage"></a>使用法

```cli
nuget config -Set <name>=[<value>] [<name>=<value> ...] [options]
nuget config -AsPath <name> [options]
```

ここで`<name>`と`<value>`構成で設定するキー/値ペアを指定します。 必要に応じて多くのペアを指定できます。 値を削除するには、名前を指定し、`=`記号が、値はありません。

使用可能なキー名では、次を参照してください。、 [NuGet config ファイル参照](../reference/nuget-config-file.md)です。

NuGet 3.4 以降で`<value>`使える[環境変数](cli-ref-environment-variables.md)です。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| AsPath | 構成は、パスとして値を返しますするときに無視`-Set`を使用します。 |
| ConfigFile | NuGet 構成ファイルを変更します。 指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。 |
| ForceEnglishOutput | *(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |

参照してください[環境変数](cli-ref-environment-variables.md)

### <a name="examples"></a>使用例

```cli
nuget config -Set repositoryPath=c:\packages -configfile c:\my.config

nuget config -Set repositoryPath=

nuget config -Set repositoryPath=%PACKAGE_REPO% -configfile %ProgramData%\NuGet\NuGetDefaults.Config

nuget config -Set HTTP_PROXY=http://127.0.0.1 -set HTTP_PROXY.USER=domain\user
```
