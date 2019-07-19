---
title: NuGet CLI の更新コマンド
description: Nuget.exe update コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327509"
---
# <a name="update-command-nuget-cli"></a>update コマンド (NuGet CLI)

**適用対象:** パッケージの&bullet;使用量が**サポートされているバージョン:** すべて

利用できる最も新しいバージョンに (`packages.config` を使用する) プロジェクトのすべてのパッケージを更新します。 を`update`実行する前に[' restore '](cli-ref-restore.md)を実行することをお勧めします。 (個々のパッケージを更新するに[`nuget install`](cli-ref-install.md)は、バージョン番号を指定せずにを使用します。この場合、NuGet は最新バージョンをインストールします)。

注: `update`は、Mono (Mac OSX または Linux) で実行される CLI、または PackageReference 形式を使用する場合には機能しません。

`update`また、これらの参照が既に存在する場合は、プロジェクトファイル内のアセンブリ参照も更新されます。 更新されたパッケージにアセンブリが追加されている場合、新しい参照は追加され*ません*。 新しいパッケージの依存関係では、アセンブリ参照も追加されません。 これらの操作を更新プログラムの一部として含めるには、パッケージマネージャー UI またはパッケージマネージャーコンソールを使用して、Visual Studio でパッケージを更新します。

このコマンドは、 *-self*フラグを使用して nuget.exe 自体を更新するためにも使用できます。

## <a name="usage"></a>使用法

```cli
nuget update <configPath> [options]
```

ここ`<configPath>`では、 `packages.config`プロジェクトの依存関係を一覧表示するまたはソリューションファイルを指定します。

## <a name="options"></a>オプション

| オプション | 説明 |
| --- | --- |
| ConfigFile | 適用する NuGet 構成ファイル。 指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。|
| FileConflictAction | プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクションを指定します。 値は*overwrite、ignore、none*です。 |
| ForceEnglishOutput | *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。 |
| Help | ヘルプのコマンドの情報を表示します。 |
| ID | 更新するパッケージ Id の一覧を指定します。 |
| MSBuildPath | *(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これは`-MSBuildVersion`よりも優先されます。 |
| MSBuildVersion | *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。 |
| NonInteractive | ユーザーの入力または確認のプロンプトを表示しません。 |
| PreRelease | プレリリースバージョンに更新できます。 既にインストールされているプレリリースパッケージを更新する場合、このフラグは必要ありません。 |
| RepositoryPath | パッケージがインストールされているローカルフォルダーを指定します。 |
| セーフ | インストールされているパッケージと同じメジャーバージョンとマイナーバージョン内で利用可能な最新バージョンの更新プログラムのみをインストールするように指定します。 |
| 自身 | Nuget.exe を最新バージョンに更新します。その他のすべての引数は無視されます。 |
| Source | 更新に使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。 |
| Verbosity | 出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細* |
| Version | 1つのパッケージ ID と共に使用する場合は、更新するパッケージのバージョンを指定します。 |

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
