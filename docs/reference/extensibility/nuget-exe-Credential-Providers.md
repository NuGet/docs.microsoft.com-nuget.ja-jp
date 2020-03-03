---
title: nuget.exe 資格情報プロバイダー
description: nuget.exe 資格情報プロバイダーはフィードで認証され、特定の規則に従うコマンドライン実行可能ファイルとして実装されます。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230786"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Nuget.exe 資格情報プロバイダーを使用したフィードの認証

バージョン `3.3` `nuget.exe` 特定の資格情報プロバイダーのサポートが追加されました。 その後、バージョン `4.8` では、すべてのコマンドラインシナリオ (`nuget.exe`、`dotnet.exe`、`msbuild.exe`) で機能する[資格情報プロバイダーのサポート](NuGet-Cross-Platform-Authentication-Plugin.md)が追加されました。

`nuget.exe` のすべての認証方法の詳細については、「認証された[フィードからのパッケージ](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)の使用」を参照してください。

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exe 資格情報プロバイダーの検出

nuget.exe 資格情報プロバイダーは、次の3つの方法で使用できます。

- **グローバル**: 現在のユーザーのプロファイルで実行 `nuget.exe` のすべてのインスタンスで資格情報プロバイダーを使用できるようにするには、それを `%LocalAppData%\NuGet\CredentialProviders`に追加します。 `CredentialProviders` フォルダーの作成が必要になる場合があります。 資格情報プロバイダーは、`CredentialProviders` フォルダーのルートまたはサブフォルダー内にインストールできます。 資格情報プロバイダーに複数のファイル/アセンブリがある場合は、サブフォルダーを使用して、プロバイダーを整理したままにすることができます。

- **環境変数から**: 資格情報プロバイダーを任意の場所に格納し、`nuget.exe` にアクセスできるようにするには、`%NUGET_CREDENTIALPROVIDERS_PATH%` 環境変数をプロバイダーの場所に設定します。 複数の場所がある場合は、この変数をセミコロンで区切ったリスト (`path1;path2`など) にすることができます。

- **Nuget.exe と共**に、nuget.exe 資格情報プロバイダーを `nuget.exe`と同じフォルダーに配置できます。

資格情報プロバイダーを読み込むときに、`nuget.exe` は `credentialprovider*.exe`という名前のファイルについて、上記の場所を順に検索し、見つかった順にそれらのファイルを読み込みます。 複数の資格情報プロバイダーが同じフォルダーに存在する場合は、アルファベット順に読み込まれます。

## <a name="creating-a-nugetexe-credential-provider"></a>Nuget.exe 資格情報プロバイダーを作成する

資格情報プロバイダーは、`CredentialProvider*.exe`という形式で指定されたコマンドライン実行可能ファイルで、入力を収集し、必要に応じて資格情報を取得して、適切な終了ステータスコードと標準出力を返します。

プロバイダーは次の操作を行う必要があります。

- 資格情報の取得を開始する前に、対象の URI の資格情報を提供できるかどうかを判断します。 そうでない場合は、資格情報なしのステータスコード1が返されます。
- `Nuget.Config` を変更しません (ここで資格情報を設定するなど)。
- NuGet がプラグインにプロキシ情報を提供しないため、HTTP プロキシの構成を独自に処理します。
- UTF-8 エンコーディングを使用して、JSON 応答オブジェクト (下記参照) を stdout に書き込むことによって、資格情報またはエラーの詳細を `nuget.exe` に返します。
- 必要に応じて、追加のトレースログを stderr に出力します。 詳細レベルの "標準" または "詳細" のトレースが NuGet によってコンソールにエコーされるため、stderr にシークレットを書き出す必要はありません。
- 将来のバージョンの NuGet との上位互換性を提供するため、予期しないパラメーターは無視する必要があります。

### <a name="input-parameters"></a>入力パラメーター

| パラメーター/スイッチ |説明|
|----------------|-----------|
| Uri {value} | 資格情報を必要とするパッケージソース URI。|
| NonInteractive | 存在する場合、プロバイダーは対話型プロンプトを発行しません。 |
| IsRetry | 存在する場合は、この試行が前回失敗した試行の再試行であることを示します。 通常、プロバイダーはこのフラグを使用して、既存のキャッシュをバイパスし、可能であれば新しい資格情報の入力を求めます。|
| Verbosity {value} | 存在する場合は、"normal"、"quiet"、または "detailed" のいずれかの値を指定します。 値が指定されていない場合、は既定で "normal" になります。 プロバイダーはこれを、標準エラーストリームに出力するオプションのログ記録のレベルを示す値として使用する必要があります。 |

### <a name="exit-codes"></a>終了コード

| コード |結果 | 説明 |
|----------------|-----------|-----------|
| 0 | 成功 | 資格情報が正常に取得され、stdout に書き込まれました。|
| 1 | ProviderNotApplicable | 現在のプロバイダーは、指定された URI の資格情報を提供しません。|
| 2 | 障害 | プロバイダーは、指定された URI の正しいプロバイダーですが、資格情報を提供することはできません。 この場合、nuget.exe は認証を再試行せず、失敗します。 一般的な例として、ユーザーが対話型ログインをキャンセルした場合があります。 |

### <a name="standard-output"></a>標準出力

| プロパティ |説明|
|----------------|-----------|
| ユーザー名 | 認証された要求のユーザー名。|
| Password | 認証された要求のパスワード。|
| Message | 応答に関するオプションの詳細。失敗した場合に追加の詳細を表示するためにのみ使用されます。 |

Stdout の例:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>資格情報プロバイダーのトラブルシューティング

現時点では、NuGet はカスタム資格情報プロバイダーをデバッグするための直接的なサポートを提供していません。[問題 4598](https://github.com/NuGet/Home/issues/4598)はこの作業を追跡しています。

次の操作を行うこともできます。

- `-verbosity` スイッチを使用して nuget.exe を実行し、詳細な出力を検査します。
- 適切な場所で `stdout` にデバッグメッセージを追加します。
- Nuget.exe 3.3 以降を使用していることを確認してください。
- 起動時にデバッガーをアタッチするには、次のコードスニペットを使用します。

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
