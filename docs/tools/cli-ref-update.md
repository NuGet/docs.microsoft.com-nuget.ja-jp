---
title: NuGet CLI 更新コマンド
description: Nuget.exe 更新コマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a>update コマンド (NuGet CLI)

**適用されます:** 消費をパッケージ化&bullet;**サポートされているバージョン:** すべて

プロジェクト内のすべてのパッケージを更新 (を使用して`packages.config`) を使用可能な最新のバージョン。 実行することをお勧め['restore'](cli-ref-restore.md)実行する前に、`update`です。 (個々 のパッケージを更新する[ `nuget install` ](cli-ref-install.md)ケースの NuGet が最新バージョンをインストール、バージョン番号を指定することがなくです)。

注: `update` PackageReference 形式を使用する場合は、Mono (Mac os X または Linux) で、またはを実行している CLI では機能しません。

`update`コマンドもプロジェクト ファイル内のアセンブリ参照を更新すると、それらの参照が既に提供が存在します。 新しい参照は、更新されたパッケージに追加されたアセンブリがある場合は、*いない*を追加します。 新しいパッケージの依存関係も追加のアセンブリ参照がありません。 更新プログラムの一部としてこれらの操作を含めるには、パッケージ マネージャー UI またはパッケージ マネージャー コンソールを使用して Visual Studio でパッケージを更新します。

このコマンドは、nuget.exe 自体の更新にも使用できますを使用して、 *-自己*フラグ。

## <a name="usage"></a>使用法

```cli
nuget update <configPath> [options]
```

ここで`<configPath>`いずれかを識別、`packages.config`またはソリューション ファイルがプロジェクトの依存関係を一覧表示されます。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | NuGet 構成ファイルを適用します。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。|
| FileConflictAction | 上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクションを指定します。 値は*で上書きし、無視する場合に、none*です。 |
| ForceEnglishOutput | *(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| ヘルプ | ヘルプ コマンドに関する情報を表示します。 |
| ID | パッケージを更新する Id の一覧を指定します。 |
| MSBuildPath | *(4.0 以降)* よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。 |
| MSBuildVersion | *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされている値は、4、12、14、15 です。 既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。 |
| NonInteractive | ユーザー入力または確認を要求するプロンプトを抑制します。 |
| プレリリース版 | プレリリース バージョンを更新できるようにします。 このフラグは既にインストールされているプレリリースのパッケージを更新するときに必要ありません。 |
| RepositoryPath | パッケージがインストールされているローカル フォルダーを指定します。 |
| セーフ | のみを更新する最高のバージョンが同じメジャーおよびマイナー バージョン内で使用できるようにインストールされているパッケージがインストールされるように指定します。 |
| Self | Nuget.exe、最新のバージョンに更新です。その他のすべての引数は無視されます。 |
| ソース | (Url) として、更新プログラムを使用するパッケージ ソースの一覧を指定します。 コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)です。 |
| 詳細度 | 出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。 |
| Version | 1 つのパッケージ ID に使用する場合は、更新するパッケージのバージョンを指定します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
