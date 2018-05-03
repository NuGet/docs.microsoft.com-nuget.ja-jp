---
title: NuGet CLI 環境変数
description: Nuget.exe 環境変数の参照
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: adeacd917fd775c6eed431df9c0f74e591ad793e
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/28/2018
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 環境変数

Nuget.exe CLI の動作は、コンピューター全体のユーザーに nuget.exe に影響するか、レベルを処理する環境変数の数を構成できます。 環境変数の設定を常にオーバーライドする`NuGet.Config`を許可するファイルのビルド サーバーをすべてのファイルを変更することがなく適切な設定を変更します。

一般に、コマンドラインに直接または NuGet の構成ファイルで指定されたオプションの優先順位がなど、いくつかの例外がある*FORCE_NUGET_EXE_INTERACTIVE*です。 異なるコンピューター間で異なる動作をその nuget.exe 場合は、環境変数が原因で可能性があります。 たとえば、Azure Web アプリの Kudu (配置時に使用される) は*NUGET_XMLDOC_MODE*に設定*スキップ*をパッケージの復元のパフォーマンスを高速化し、ディスク領域を節約します。

| 変数 | 説明 | コメント |
| --- | --- | --- |
| http_proxy | Http プロキシが NuGet HTTP 操作に使用します。 | これが指定されたとして`http://<username>:<password>@proxy.com`です。 |
| no_proxy | プロキシの使用をバイパスするドメインを構成します。 | コンマ (,) で区切られたドメインとして指定します。 |
| EnableNuGetPackageRestore | NuGet は暗黙的に同意を許可復元時にパッケージで必要となるかどうかがある場合は、フラグします。 | 指定されたフラグとして扱われます*true*または*1*、設定されていないその他の値をフラグとして扱われます。 |
| NUGET_EXE_NO_PROMPT | Exe 資格情報の確認をしないようにします。 | 任意の値を null または空の文字列として扱われます点を除いてこれはフラグ セット/true です。 |
| FORCE_NUGET_EXE_INTERACTIVE | 対話モードを強制的にグローバル環境変数です。 | 任意の値を null または空の文字列として扱われます点を除いてこれはフラグ セット/true です。 |
| NUGET_PACKAGES | パスを*グローバル パッケージ*フォルダーの定義に従って[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。 | 絶対パスとして指定します。 |
| NUGET_FALLBACK_PACKAGES | グローバル フォールバックは、フォルダーをパッケージ化します。 | セミコロン (;) で区切られたフォルダーへの絶対パス。 |
| NUGET_HTTP_CACHE_PATH | パスを*http キャッシュ*フォルダーの定義に従って[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。 | 絶対パスとして指定します。 |
| NUGET_PERSIST_DG | Dg ファイル (MSBuild から収集されたデータ) を永続化すべきかを示すフラグです。 | として指定された*true*または*false* (既定)、NUGET_PERSIST_DG_PATH が設定されていない場合は、一時ディレクトリ (現在の環境の一時ディレクトリの NuGetScratch フォルダー) に格納されます。 |
| NUGET_PERSIST_DG_PATH | Dg ファイルを保持するパス。 | 絶対パスとして指定すると、このオプションは、場合にのみ使用*NUGET_PERSIST_DG*設定が true に設定します。 |
| NUGET_RESTORE_MSBUILD_ARGS | 追加の MSBuild 引数を設定します。 | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild のログの詳細レベルを設定します。 | 既定値は*quiet* ("/v: q") です。 使用可能な値*q [uiet]*、 *m [inimal]*、 *n [ormal]*、*は*、および*diag [nostic]* です。 |
| NUGET_SHOW_STACK | ユーザーに (スタック トレースを含む)、完全な例外を表示するかどうかを判断します。 | として指定された*true*または*false* (既定値)。 |
| NUGET_XMLDOC_MODE | アセンブリ XML ドキュメント ファイルの展開を処理する方法を決定します。 | サポートされているモードは*スキップ*(XML ドキュメント ファイルを抽出しないでください、)*圧縮*(zip アーカイブとして XML ドキュメント ファイルを保存) または*なし*(既定を XML ドキュメント ファイルを標準として扱うファイル)。 |
