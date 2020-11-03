---
title: NuGet CLI の更新コマンド
description: nuget.exe update コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 106c4027f03d8e8c1d19545b3ca9b6cd5263830e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236790"
---
# <a name="update-command-nuget-cli"></a>update コマンド (NuGet CLI)

**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** すべて

利用できる最も新しいバージョンに (`packages.config` を使用する) プロジェクトのすべてのパッケージを更新します。 を実行する前に [' restore '](cli-ref-restore.md) を実行することをお勧め `update` します。 (個々のパッケージを更新するには、 [`nuget install`](cli-ref-install.md) バージョン番号を指定せずにを使用します。この場合、NuGet は最新バージョンをインストールします)。

注: `update` は、Mono (MAC OSX または Linux) で実行される CLI、または PackageReference 形式を使用する場合には機能しません。

`update`また、これらの参照が既に存在する場合は、プロジェクトファイル内のアセンブリ参照も更新されます。 更新されたパッケージにアセンブリが追加されている場合、新しい参照は追加され *ません* 。 新しいパッケージの依存関係では、アセンブリ参照も追加されません。 これらの操作を更新プログラムの一部として含めるには、パッケージマネージャー UI またはパッケージマネージャーコンソールを使用して、Visual Studio でパッケージを更新します。

このコマンドは、 *-self* フラグを使用して nuget.exe 自体を更新するためにも使用できます。

## <a name="usage"></a>使用

```cli
nuget update <configPath> [options]
```

ここ `<configPath>` `packages.config` では、プロジェクトの依存関係を一覧表示するまたはソリューションファイルを指定します。

## <a name="options"></a>オプション

- **`-ConfigFile`**

  適用する NuGet 構成ファイル。 指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  使用する依存関係パッケージのバージョンを指定します。次のいずれかになります。<br/><ul><li>*最低* (既定): 最も低いバージョンです。</li><li>*HighestPatch* : 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</li><li>*HighestMinor* : 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</li><li>*最高* : 最高バージョン</li><li>*無視* : 依存関係パッケージは使用されません</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  ターゲットプロジェクトにパッケージのファイルが既に存在する場合の既定のアクションを指定します。 常にファイルを上書きする場合はに設定し `Overwrite` ます。 ファイルをスキップするには、に設定し `Ignore` ます。

  `PromptUser`既定では、またはが指定されていない限り、 `OverwriteAll` 他のすべての `IgnoreAll` ファイルに適用されます。

- **`-ForceEnglishOutput`**

  *(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。

- **`-?|-help`**

  コマンドのヘルプ情報を表示します。

- **`-Id`**

  更新するパッケージ Id の一覧を指定します。

- **`-MSBuildPath`**

  *(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これはよりも優先さ `-MSBuildVersion` れます。

- **`-MSBuildVersion`**

  *(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。 サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。 既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。

- **`-NonInteractive`**

  ユーザーの入力または確認のプロンプトを表示しません。

- **`-PreRelease`**

  プレリリースバージョンに更新できます。 既にインストールされているプレリリースパッケージを更新する場合、このフラグは必要ありません。

- **`-RepositoryPath`**

  パッケージがインストールされているローカルフォルダーを指定します。

- **`-Safe`**

  インストールされているパッケージと同じメジャーバージョンとマイナーバージョン内で利用可能な最新バージョンの更新プログラムのみをインストールするように指定します。

- **`-Self`**

  最新バージョンに nuget.exe を更新します。その他のすべての引数は無視されます。

- **`-Source`**

  更新に使用するパッケージソースの一覧を Url として指定します。 省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。

- **`-Verbosity [normal|quiet|detailed]`**

  出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。

- **`-Version`**

  1つのパッケージ ID と共に使用する場合は、更新するパッケージのバージョンを指定します。

「[環境変数](cli-ref-environment-variables.md)」も参照してください。

## <a name="examples"></a>使用例

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
