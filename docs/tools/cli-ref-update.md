---
title: NuGet CLI の更新コマンド
description: Nuget.exe の update コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: ded9b571324d810c2f0e1a46ea76375a28940406
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145606"
---
# <a name="update-command-nuget-cli"></a>update コマンド (NuGet CLI)

**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン:** すべて

プロジェクト内のすべてのパッケージの更新 (を使用して`packages.config`) を使用可能な最新のバージョン。 実行することをお勧め['restore'](cli-ref-restore.md)実行する前に、`update`します。 (個々 のパッケージを更新する[ `nuget install` ](cli-ref-install.md)大文字と小文字の NuGet が最新バージョンをインストールするバージョン番号を指定することがなく)。

注: `update` PackageReference 形式を使用する場合は、Mono (Mac OSX または Linux) で、またはを実行して、CLI では機能しません。

`update`コマンドはプロジェクト ファイル内のアセンブリ参照を更新することも、存在するものを参照して既に提供します。 新しい参照は、更新されたパッケージに追加されたアセンブリがある場合は、*いない*を追加します。 新しいパッケージの依存関係は、追加のアセンブリ参照も必要はありません。 更新プログラムの一部としてこれらの操作を含めるには、パッケージ マネージャー UI またはパッケージ マネージャー コンソールを使用して Visual Studio でパッケージを更新します。

このコマンドが nuget.exe 自体を更新することもできますを使用して、 *-セルフ*フラグ。

## <a name="usage"></a>使用法

```cli
nuget update <configPath> [options]
```

場所`<configPath>`いずれかを識別、`packages.config`またはソリューション ファイルをプロジェクトの依存関係を一覧表示します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。|
| FileConflictAction | 上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められる場合に実行するアクションを指定します。 値は*で上書きし、無視する場合に、none*します。 |
| ForceEnglishOutput | *(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| ID | パッケージを更新する Id の一覧を指定します。 |
| MSBuildPath | *(4.0 以降)* よりも優先、コマンドで使用する MSBuild のパスを示す`-MSBuildVersion`します。 |
| MSBuildVersion | *(3.2 以降)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされている値とは、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 パスに MSBuild が取得される、既定でそれ以外の場合、既定値 MSBuild の最上位のインストールされているバージョンです。 |
| NonInteractive | ユーザー入力や確認のプロンプトを抑制します。 |
| PreRelease | プレリリース バージョンに更新を許可します。 既にインストールされているプレリリースのパッケージを更新するときに、このフラグは必要ありません。 |
| RepositoryPath | パッケージがインストールされているローカル フォルダーを指定します。 |
| Safe | のみを更新する同じメジャーおよびマイナーのバージョン内で使用可能な最上位バージョンにインストールされているパッケージはインストールされているを指定します。 |
| self | Nuget.exe を最新のバージョンに更新します。その他のすべての引数は無視されます。 |
| Source | (Url) として、更新に使用するパッケージ ソースの一覧を指定します。 コマンドを省略すると、構成ファイルで提供されるソースを使用して、参照してください[NuGet の構成の動作を](../consume-packages/configuring-nuget-behavior.md)します。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。 |
| Version | 1 つのパッケージ ID と共に使用すると、更新するパッケージのバージョンを指定します。 |

参照してください[環境変数](cli-ref-environment-variables.md)

## <a name="examples"></a>使用例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
