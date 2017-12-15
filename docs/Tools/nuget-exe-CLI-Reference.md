---
title: "NuGet の参照をコマンド ライン インターフェイス (CLI) |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: d777c424-0cf3-4bc0-8abd-7ca16c22192b
description: "Nuget.exe CLI のコマンド ライン リファレンス インデックス"
keywords: "nuget.exe 参照インデックス、nuget.exe コマンド ライン インターフェイス、nuget.exe CLI、nuget コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3d1c3585d8bbf4c9bd9b50c8167e860594a42055
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-cli-reference"></a>NuGet CLI 参照

NuGet コマンド ライン インターフェイス (CLI)、 `nuget.exe`NuGet の機能をインストール、作成、発行、およびプロジェクト ファイルに変更を加えずにパッケージの管理のすべての範囲を提供します。

いずれかのコマンドを使用するコマンド ウィンドウを開き、または bash シェルを実行`nuget`の後に、コマンドと、適切なオプションなど`nuget help pack`(ヘルプを表示するパック コマンドで)。

## <a name="installing-nugetexe"></a>Nuget.exe をインストールします。

[!INCLUDE[install-cli](../includes/install-cli.md)]

## <a name="availability"></a>可用性

- すべてのコマンドは、Windows で使用可能です。
- すべてのコマンドを使用[Mono で実行されている nuget.exe](../guides/install-nuget.md#mac-osx-and-linux)示されている場合を除き`pack`、 `restore`、および`update`です。
- `pack`、 `restore`、 `delete`、 `locals`、および`push`コマンドは、Mac および Linux での使用も、 [dotnet CLI](dotnet-Commands.md)です。 

## <a name="commands-and-applicability"></a>コマンドと適用性

使用可能なコマンドとパッケージの作成、パッケージの消費量、およびパッケージを発行するホストへの適用性:

| 一般的なコマンド | 適用可能なロール | NuGet のバージョン | 説明 | 
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 作成 | 2.7+ | NuGet パッケージを作成、`.nuspec`またはプロジェクト ファイルです。 モノラルでを実行するときに、プロジェクト ファイルからパッケージの作成はサポートされていません。 |
| [push](cli-ref-push.md) | 置換 | すべて | パッケージ ソースにパッケージを発行します。 |
| [構成](cli-ref-config.md) | すべて | すべて | 取得または NuGet の構成値を設定します。 |
| [役立ちますか?](cli-ref-help.md) | すべて | すべて | ヘルプ情報や、コマンドのヘルプを表示します。 |
| [[ローカル]](cli-ref-locals.md) | 消費量 | 3.3+ | 消去またはさまざまなキャッシュまたはグローバルのパッケージ フォルダーで、パッケージが一覧表示またはそれらのフォルダーを識別します。 |
| [restore](cli-ref-restore.md) | 消費量 | 2.7+ | 使用中のパッケージ参照の形式によって参照されるすべてのパッケージを復元します。 モノラルでを実行するときに、PackageReference 形式を使用してパッケージを復元はサポートされていません。 | 
| [setapikey](cli-ref-setapikey.md) | 発行、消費量 | すべて | パッケージ ソースのアクセス キーが必要な場合は、特定のパッケージ ソースの API キーを保存します。 |
| [仕様](cli-ref-spec.md) | 作成 | すべて | 生成、`.nuspec`ファイル、Visual Studio プロジェクトからファイルを生成する場合は、トークンを使用します。 |


| セカンダリ コマンド | 適用可能なロール | NuGet のバージョン | 説明 | 
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 置換 | 3.3+ | 階層構造を使用して HTTP 以外のパッケージ ソースにパッケージを追加します。 HTTP ソースを使用して*プッシュ*です。 |
| [delete](cli-ref-delete.md) | 置換 | すべて | 削除するか、パッケージ ソースからパッケージを unlists します。 |
| [init](cli-ref-init.md) | 作成 | 3.3+ | 階層的なレイアウトを使用してパッケージ ソース フォルダーからパッケージを追加します。 |
| [インストールします。](cli-ref-install.md) | 消費量 | すべて | 現在のパッケージをインストール プロジェクトしますが、ありませんプロジェクトを変更するかファイルを参照します。 |
| [list](cli-ref-list.md) | 消費量、おそらくの発行 | すべて | 指定されたソースからパッケージを表示します。 |
| [ミラー](cli-ref-mirror.md) | 置換 | 3.2 以降で廃止されました | パッケージと、ターゲットのリポジトリにソースからその依存関係を反映します。 |
| [ソース](cli-ref-sources.md) | 消費量、発行 | すべて | 構成ファイル内のパッケージ ソースを管理します。 |
| [更新プログラム](cli-ref-update.md) | 消費量 | すべて | プロジェクトのパッケージを使用可能な最新バージョンに更新されます。 Mono で実行されているときに、サポートされていません。 |

別のコマンドのためのさまざまな使用[環境変数](cli-ref-environment-variables.md)です。

適用可能なロールで NuGet CLI コマンド。

| ロール | コマンド |
| --- | --- |
| 消費量 | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` | 
| 作成 | `config`, `help`, `init`, `pack`, `spec` |
| 置換 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

開発者は、パッケージの使用にのみ関係など、必要があるだけを理解する NuGet コマンドのサブセットに含まれる。

> [!Note]
> コマンド オプション名では区別されません。 廃止されたオプションはなど、この参照に含まれません`NoPrompt`(置き換え`NonInteractive`) と`Verbose`(置き換え`Verbosity`)。
