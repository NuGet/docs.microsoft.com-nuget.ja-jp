---
title: NuGet CLI ソースコマンド
description: nuget.exe sources コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e9cbdd089c5c0f66d25e7588ece504feae63f2f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780008"
---
# <a name="sources-command-nuget-cli"></a>sources コマンド (NuGet CLI)

**適用対象:** パッケージの使用、 &bullet; **サポートされるバージョン** の発行: すべて

ユーザースコープ構成ファイルまたは指定された構成ファイルにあるソースの一覧を管理します。 ユーザースコープ構成ファイルは、 `%appdata%\NuGet\NuGet.Config` (Windows) と `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) にあります。

ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。

## <a name="usage"></a>使用方法

```cli
nuget sources <operation> -Name <name> -Source <source>
```

ここで `<operation>` 、は *List、Add、Remove、Enable、Disable、* または *Update* のいずれかで、は `<name>` ソースの名前、 `<source>` はソースの URL です。 操作できるソースは一度に1つだけです。

## <a name="options"></a>Options

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-Format`**

  アクションに適用され、 `list` `Detailed` (既定値) またはにすることができ `Short` ます。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-Name`**

  ソースの名前。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-Password`**

  ソースでの認証に使用するパスワードを指定します。

- **`-src|-Source`**

  パッケージソースへのパス。

- **`-StorePasswordInClearText`**

  暗号化されたフォームを格納する既定の動作ではなく、暗号化されていないテキストにパスワードを格納することを示します。

- **`-UserName`**

  ソースでの認証に使用するユーザー名を指定します。

- **`-ValidAuthenticationTypes`**

  このソースに対して有効な認証の種類のコンマ区切りのリスト。 既定では、すべての認証の種類が有効です。 例: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

> [!Note]
> 後でパッケージソースへのアクセスに使用する nuget.exe と同じユーザーコンテキストで、ソースのパスワードを追加してください。 パスワードは暗号化されて構成ファイルに格納され、暗号化されたときと同じユーザーコンテキストでのみ暗号化を解除できます。 たとえば、ビルドサーバーを使用して NuGet パッケージを復元する場合、ビルドサーバータスクを実行するのと同じ Windows ユーザーでパスワードを暗号化する必要があります。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
