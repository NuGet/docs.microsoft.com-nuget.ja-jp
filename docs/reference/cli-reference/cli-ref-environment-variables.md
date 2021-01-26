---
title: NuGet CLI 環境変数
description: nuget.exe 環境変数のリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: a688382420633916e81a000ba6095ff83e036cf9
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779378"
---
# <a name="nuget-cli-environment-variables"></a>NuGet CLI 環境変数

nuget.exe CLI の動作は、さまざまな環境変数を使用して構成できます。これは、コンピューター全体、ユーザー、またはプロセスレベルで nuget.exe に影響します。 環境変数は、ファイル内の設定を常にオーバーライドし `NuGet.Config` ます。ビルドサーバーは、ファイルを変更することなく適切な設定を変更できます。

一般に、コマンドラインまたは NuGet 構成ファイルで直接指定されたオプションの方が優先されますが、 *FORCE_NUGET_EXE_INTERACTIVE* など、いくつかの例外があります。 異なるコンピューター間で nuget.exe の動作が異なる場合は、環境変数が原因である可能性があります。 たとえば、Azure Web Apps Kudu (デプロイ中に使用される) では、パッケージの復元のパフォーマンスを高速化し、ディスク領域を節約するために *スキップ* するように *NUGET_XMLDOC_MODE* 設定されています。

NuGet CLI は、MSBuild を使用してプロジェクトファイルを読み取ります。 すべての環境変数は、MSBuild 評価中に [プロパティ](/visualstudio/msbuild/msbuild-command-line-reference) として使用できます。
「 [MSBuild ターゲットとしての NuGet パックと復元](../msbuild-targets.md#restore-properties) 」に記載されているプロパティの一覧は、環境変数として設定することもできます。

| 変数 | 説明 | 解説 |
| --- | --- | --- |
| http_proxy | NuGet HTTP 操作に使用される http プロキシ。 | これは、として指定され `http://<username>:<password>@proxy.com` ます。 |
| no_proxy | プロキシを使用しないようにドメインを構成します。 | コンマ (,) で区切られたドメインとして指定されます。 |
| EnableNuGetPackageRestore | 復元時にパッケージで必要な場合に、NuGet が暗黙的に同意を付与する必要があるかどうかを示すフラグです。 | 指定されたフラグは、 *true* または *1* として扱われます。その他の値はフラグが設定されていません。 |
| NUGET_EXE_NO_PROMPT | 実行可能ファイルの資格情報を要求しないようにします。 | Null または空の文字列を除くすべての値は、このフラグが設定されるか true として扱われます。 |
| FORCE_NUGET_EXE_INTERACTIVE | 対話モードを強制するグローバル環境変数。 | Null または空の文字列を除くすべての値は、このフラグが設定されるか true として扱われます。 |
| NUGET_PACKAGES | 「[グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」で説明されているように、*グローバルパッケージ* フォルダーに使用するパス。 | 絶対パスとして指定されます。 |
| NUGET_FALLBACK_PACKAGES | グローバルフォールバックパッケージフォルダー。 | セミコロン (;) で区切られた絶対フォルダーパス。 |
| NUGET_HTTP_CACHE_PATH | 「[グローバルパッケージとキャッシュフォルダーの管理](../../consume-packages/managing-the-global-packages-and-cache-folders.md)」で説明されているように、 *http キャッシュ* フォルダーに使用するパス。 | 絶対パスとして指定されます。 |
| NUGET_PERSIST_DG | Dg ファイル (MSBuild から収集されたデータ) を永続化する必要があるかどうかを示すフラグです。 | *True* または *false* (既定値) として指定されます NUGET_PERSIST_DG_PATH 設定されていない場合は、一時ディレクトリ (現在の環境の一時ディレクトリの NuGetScratch フォルダー) に格納されます。 |
| NUGET_PERSIST_DG_PATH | Dg ファイルを永続化するためのパス。 | 絶対パスとして指定します。このオプションは、 *NUGET_PERSIST_DG* が true に設定されている場合にのみ使用されます。 |
| NUGET_RESTORE_MSBUILD_ARGS | 追加の MSBuild 引数を設定します。 | 引数を msbuild.exe に渡す方法と同じにします。 コマンドラインから値バーにプロジェクトプロパティ Foo を設定する例は、/p: Foo = Bar です。 |
| NUGET_RESTORE_MSBUILD_VERBOSITY | MSBuild ログの詳細度を設定します。 | 既定値は *quiet* ("/v: q") です。 使用できる値は、 *q [uiet]*、 *m [inimal]*、 *n [ormal]*、 *d [etailed]*、および *diag [nostic]* です。 |
| NUGET_SHOW_STACK | 完全な例外 (スタックトレースを含む) をユーザーに表示するかどうかを決定します。 | *True* または *false* (既定値) として指定されます。 |
| NUGET_XMLDOC_MODE | アセンブリ XML ドキュメントファイルの抽出をどのように処理するかを決定します。 | サポートされているモードは、 *skip* (xml ドキュメントファイルを抽出しない)、 *圧縮* (xml ドキュメントファイルを zip アーカイブとして格納)、または *none* (既定では、xml ドキュメントファイルを通常のファイルとして扱います) です。 |
| NUGET_CERT_REVOCATION_MODE | 署名されたパッケージのインストールまたは復元時に、パッケージの署名に使用される証明書の失効ステータスチェックを実行する方法を指定します。 設定しない場合、の既定値はに `online` なります。| 有効値は *オンライン* (既定)、 *オフライン* です。  [NU3028](../errors-and-warnings/NU3028.md)に関連 |

