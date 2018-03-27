---
title: "NuGet の参照をコマンド ライン インターフェイス (CLI) |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe CLI のコマンド ライン リファレンス インデックス"
keywords: "nuget.exe 参照インデックス、nuget.exe コマンド ライン インターフェイス、nuget.exe CLI、nuget コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8b1ee17702f5a54a77dc2cd663e13729a9b4a39f
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-cli-reference"></a>NuGet CLI 参照

NuGet コマンド ライン インターフェイス (CLI)、 `nuget.exe`NuGet の機能をインストール、作成、発行、およびプロジェクト ファイルに変更を加えずにパッケージの管理のすべての範囲を提供します。

いずれかのコマンドを使用するコマンド ウィンドウを開き、または bash シェルを実行`nuget`の後に、コマンドと、適切なオプションなど`nuget help pack`(ヘルプを表示するパック コマンドで)。

このドキュメントでは、NuGet CLI の最新バージョンを反映します。 詳細については正確な使用している特定のバージョンについては、実行`nuget help`の目的のコマンド。

## <a name="installing-nugetexe"></a>Nuget.exe をインストールします。

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Tip]
> NuGet CLI を使用可能にパッケージ マネージャー コンソール内で Visual Studio で、次を参照してください。[コンソールで nuget.exe CLI を使用して](package-manager-console.md#using-the-nugetexe-cli-in-the-console)です。

## <a name="availability"></a>可用性

参照してください[機能の可用性](../install-nuget-client-tools.md#feature-availability)詳細については正確です。

- すべてのコマンドは、Windows で使用可能です。
- Nuget.exe に対して指定された場所を除く、Mono で実行されているすべてのコマンドを使用`pack`、 `restore`、および`update`です。
- `pack`、 `restore`、 `delete`、 `locals`、および`push`コマンドは、CLI dotnet Mac および Linux で使用します。

## <a name="commands-and-applicability"></a>コマンドと適用性

使用可能なコマンドとパッケージの作成、パッケージの消費量、およびパッケージを発行するホストへの適用性:

| 一般的なコマンド | 適用可能なロール | NuGet のバージョン | 説明 |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | 作成 | 2.7+ | NuGet パッケージを作成、`.nuspec`またはプロジェクト ファイルです。 モノラルでを実行するときに、プロジェクト ファイルからパッケージの作成はサポートされていません。 |
| [push](cli-ref-push.md) | 置換 | すべて | パッケージ ソースにパッケージを発行します。 |
| [config](cli-ref-config.md) | すべて | すべて | 取得または NuGet の構成値を設定します。 |
| [help または ?](cli-ref-help.md) | すべて | すべて | ヘルプ情報や、コマンドのヘルプを表示します。 |
| [locals](cli-ref-locals.md) | 利用 | 3.3+ | 消去またはさまざまなキャッシュまたはグローバルのパッケージ フォルダーで、パッケージが一覧表示またはそれらのフォルダーを識別します。 |
| [restore](cli-ref-restore.md) | 利用 | 2.7+ | 使用中のパッケージ参照の形式によって参照されるすべてのパッケージを復元します。 モノラルでを実行するときに、PackageReference 形式を使用してパッケージを復元はサポートされていません。 |
| [setapikey](cli-ref-setapikey.md) | 発行、消費量 | すべて | パッケージ ソースのアクセス キーが必要な場合は、特定のパッケージ ソースの API キーを保存します。 |
| [spec](cli-ref-spec.md) | 作成 | すべて | 生成、`.nuspec`ファイル、Visual Studio プロジェクトからファイルを生成する場合は、トークンを使用します。 |

| セカンダリ コマンド | 適用可能なロール | NuGet のバージョン | 説明 |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | 置換 | 3.3+ | 階層構造を使用して HTTP 以外のパッケージ ソースにパッケージを追加します。 HTTP ソースを使用して*プッシュ*です。 |
| [delete](cli-ref-delete.md) | 置換 | すべて | 削除するか、パッケージ ソースからパッケージを unlists します。 |
| [init](cli-ref-init.md) | 作成 | 3.3+ | 階層的なレイアウトを使用してパッケージ ソース フォルダーからパッケージを追加します。 |
| [install](cli-ref-install.md) | 利用 | すべて | 現在のパッケージをインストール プロジェクトしますが、ありませんプロジェクトを変更するかファイルを参照します。 |
| [list](cli-ref-list.md) | 消費量、おそらくの発行 | すべて | 指定されたソースからパッケージを表示します。 |
| [mirror](cli-ref-mirror.md) | 置換 | 3.2 以降で廃止されました | パッケージと、ターゲットのリポジトリにソースからその依存関係を反映します。 |
| [sources](cli-ref-sources.md) | 消費量、発行 | すべて | 構成ファイル内のパッケージ ソースを管理します。 |
| [update](cli-ref-update.md) | 利用 | すべて | プロジェクトのパッケージを使用可能な最新バージョンに更新されます。 Mono で実行されているときに、サポートされていません。 |

別のコマンドのためのさまざまな使用[環境変数](cli-ref-environment-variables.md)です。

適用可能なロールで NuGet CLI コマンド。

| ロール | コマンド |
| --- | --- |
| 利用 | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| 作成 | `config`, `help`, `init`, `pack`, `spec` |
| 置換 | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

開発者は、パッケージの使用にのみ関係など、必要があるだけを理解する NuGet コマンドのサブセットに含まれる。

> [!Note]
> コマンド オプション名では区別されません。 廃止されたオプションはなど、この参照に含まれません`NoPrompt`(置き換え`NonInteractive`) と`Verbose`(置き換え`Verbosity`)。
