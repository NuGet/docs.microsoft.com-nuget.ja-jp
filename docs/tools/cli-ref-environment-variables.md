---
title: NuGet CLI 環境変数
description: Nuget.exe の環境変数への参照
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: fd5824d1c5e05df08301dac1cf656ba1d5ca75cd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551739"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 環境変数

Nuget.exe CLI の動作は、さまざまな環境変数、コンピューター全体、ユーザーの nuget.exe に影響を与えるか、またはレベルの処理が構成できます。 環境変数は、常に任意の設定をオーバーライド`NuGet.Config`ファイルがすべてのファイルを変更することがなく適切な設定を変更するサーバーを構築します。

一般に、コマンドラインで直接または NuGet 構成ファイルで指定されたオプションの優先順位がのいくつかの例外として*FORCE_NUGET_EXE_INTERACTIVE*します。 異なるコンピューター間で異なる動作をその nuget.exe 場合は、環境変数が原因になります。 たとえば、Azure Web アプリの Kudu (デプロイ時に使用される) は*NUGET_XMLDOC_MODE*に設定*スキップ*パッケージ復元のパフォーマンスを高速化し、ディスク領域を節約します。

| 変数 | 説明 | Remarks |
| --- | --- | --- |
| http_proxy | NuGet HTTP 操作に使用される http プロキシ。 | これは、として指定`http://<username>:<password>@proxy.com`します。 |
| no_proxy | プロキシの使用をバイパスするドメインを構成します。 | コンマ (,) で区切られたドメインとして指定します。 |
| EnableNuGetPackageRestore | NuGet に暗黙的に付与する必要あります同意パッケージの復元に必要なかどうかがある場合は、フラグします。 | 指定したフラグとして扱われます*true*または*1*、設定されていないその他の値をフラグとして扱われます。 |
| NUGET_EXE_NO_PROMPT | 資格情報の入力を求めるの exe をできないようにします。 | セット/true このフラグを任意の値を除き、null または空の文字列として扱われます。 |
| FORCE_NUGET_EXE_INTERACTIVE | 対話モードを強制的にグローバル環境変数です。 | セット/true このフラグを任意の値を除き、null または空の文字列として扱われます。 |
| NUGET_PACKAGES | パスを*グローバル パッケージ*フォルダーの説明に従って[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。 | 絶対パスとして指定します。 |
| NUGET_FALLBACK_PACKAGES | フォールバックのグローバル パッケージ フォルダー。 | セミコロン (;) で区切られたフォルダーへの絶対パス。 |
| NUGET_HTTP_CACHE_PATH | パスを*http キャッシュ*フォルダーの説明に従って[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。 | 絶対パスとして指定します。 |
| NUGET_PERSIST_DG | 配布グループのファイル (MSBuild から収集されたデータ) を永続化する場合を示すフラグします。 | として指定された*true*または*false* (既定)、NUGET_PERSIST_DG_PATH が設定されていない場合は、一時ディレクトリ (現在の環境の一時ディレクトリの NuGetScratch フォルダー) に格納されます。 |
| NUGET_PERSIST_DG_PATH | 配布グループのファイルを保持するパス。 | 絶対パスとして指定すると、このオプションは、場合にのみ使用*NUGET_PERSIST_DG*設定が true に設定します。 |
| NUGET_RESTORE_MSBUILD_ARGS | 追加の MSBuild 引数を設定します。 | |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild ログの詳細を設定します。 | 既定値は*quiet* ("/v q:")。 使用可能な値*q [uiet]*、 *m [inimal]*、 *n [ormal]*、 *d [etailed]*、および*diag [nostic]* します。 |
| NUGET_SHOW_STACK | ユーザーに (スタック トレースを含む) 完全な例外を表示するかどうかを判断します。 | として指定された*true*または*false* (既定値)。 |
| NUGET_XMLDOC_MODE | アセンブリの XML ドキュメント ファイルの抽出を処理する方法を決定します。 | サポートされているモードは*スキップ*(XML ドキュメント ファイルを展開しないでください、)*圧縮*(zip アーカイブとして XML ドキュメント ファイルを保存) または*none* (既定値、正規表現として XML ドキュメント ファイルを扱うファイルの場合)。 |
| NUGET_CERT_REVOCATION_MODE | パッケージに署名するために使用する証明書の失効状態を確認する方法を決定します pefromed は署名付きパッケージをインストールまたは復元します。 設定しない場合、既定値は`online`します。| 使用可能な値*オンライン*(既定)、*オフライン*します。  関連する[NU3028](../reference/errors-and-warnings/NU3028.md) |
