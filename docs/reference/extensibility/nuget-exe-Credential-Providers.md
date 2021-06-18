---
title: nuget.exe資格情報プロバイダー
description: nuget.exe資格情報プロバイダーはフィードで認証され、特定の規則に従うコマンド ライン実行可能ファイルとして実装されます。
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323831"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>資格情報プロバイダーを使用nuget.exeの認証

バージョンでは `3.3` 、特定の資格情報プロバイダーに `nuget.exe` 対するサポートが追加されました。 それ以降、バージョンでは、すべてのコマンド ライン シナリオ (、、) で動作する資格情報プロバイダー `4.8` [](NuGet-Cross-Platform-Authentication-Plugin.md) `nuget.exe` `dotnet.exe` `msbuild.exe` のサポートが追加されました。

すべての [認証方法の詳細については、「](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) 認証されたフィードからのパッケージの使用」を参照してください。 `nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>nuget.exeプロバイダーの検出

nuget.exeプロバイダーは、次の 3 つの方法で使用できます。

- **グローバル:** 資格情報プロバイダーを現在のユーザーのプロファイルで実行のすべてのインスタンスで使用するには、 に `nuget.exe` 追加します `%LocalAppData%\NuGet\CredentialProviders` 。 フォルダーの作成が必要な場合 `CredentialProviders` があります。 資格情報プロバイダーは、フォルダーのルートまたはサブフォルダー `CredentialProviders`  内にインストールできます。 資格情報プロバイダーに複数のファイル/アセンブリがある場合は、サブフォルダーを使用してプロバイダーを整理することができます。

- **環境変数から:** 資格情報プロバイダーは、任意の場所に格納し、環境変数をプロバイダーの場所に設定することで `nuget.exe` `%NUGET_CREDENTIALPROVIDERS_PATH%` 、 にアクセスできます。 複数の場所がある場合、この変数はセミコロンで区切られたリスト (例 `path1;path2` : ) にできます。

- **と共nuget.exe:** nuget.exe資格情報プロバイダーは、 と同じフォルダーに配置できます `nuget.exe` 。

資格情報プロバイダーを読み込むときに、上記の場所を順に検索し、 という名前のファイルを検索し、検出された順序でそれらのファイル `nuget.exe` `credentialprovider*.exe` を読み込めます。 同じフォルダーに複数の資格情報プロバイダーが存在する場合は、アルファベット順に読み込まれます。

## <a name="creating-a-nugetexe-credential-provider"></a>資格情報プロバイダーnuget.exe作成する

資格情報プロバイダーは、 という形式のコマンド ライン実行可能ファイルです。入力を収集し、必要に応じて資格情報を取得し、適切な終了状態コードと標準出力を返 `CredentialProvider*.exe` します。

プロバイダーは次の操作を行う必要があります。

- 資格情報の取得を開始する前に、ターゲット URI の資格情報を提供できるかどうかを判断します。 ない場合は、資格情報を使用しない状態コード 1 を返す必要があります。
- 変更しない `NuGet.Config` (資格情報の設定など)。
- NuGet ではプラグインにプロキシ情報が提供されないので、HTTP プロキシ構成を独自に処理します。
- UTF-8 エンコードを使用して、JSON 応答オブジェクト (下記参照) を stdout に書き込み、資格情報またはエラーの詳細 `nuget.exe` を に返します。
- 必要に応じて、追加のトレース ログを stderr に出力します。 詳細レベルでは "通常" または "詳細" なトレースが NuGet によってコンソールにエコーされるので、シークレットを stderr に書き込む必要はありません。
- 予期しないパラメーターは無視して、将来のバージョンの NuGet との前方互換性を提供する必要があります。

### <a name="input-parameters"></a>入力パラメーター

| パラメーター/スイッチ |説明|
|----------------|-----------|
| Uri {value} | 資格情報を必要とするパッケージ ソース URI。|
| NonInteractive | 存在する場合、プロバイダーは対話型プロンプトを発行します。 |
| IsRetry | 存在する場合は、この試行が以前に失敗した試行の再試行を示します。 プロバイダーは通常、このフラグを使用して、既存のキャッシュをバイパスし、可能であれば新しい資格情報を要求します。|
| 詳細度 {value} | 存在する場合は、"normal"、"quiet"、または "detailed" のいずれかの値を指定します。 値が指定されていない場合、既定値は "normal" になります。 プロバイダーは、標準エラー ストリームに出力するオプションのログ記録のレベルを示す値として、これを使用する必要があります。 |

### <a name="exit-codes"></a>終了コード

| コード |結果 | 説明 |
|----------------|-----------|-----------|
| 0 | 成功 | 資格情報が正常に取得され、stdout に書き込まれた。|
| 1 | ProviderNotApplicable | 現在のプロバイダーは、指定された URI の資格情報を提供します。|
| 2 | 障害 | プロバイダーは、指定された URI の正しいプロバイダーですが、資格情報を指定することはできません。 この場合、nuget.exe認証は再試行され、失敗します。 一般的な例は、ユーザーが対話型ログインを取り消す場合です。 |

### <a name="standard-output"></a>標準出力

| プロパティ |Notes|
|----------------|-----------|
| ユーザー名 | 認証された要求のユーザー名。|
| Password | 認証された要求のパスワード。|
| Message | 応答に関する省略可能な詳細。エラーが発生した場合に追加の詳細を表示するためにのみ使用されます。 |

stdout の例:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>資格情報プロバイダーのトラブルシューティング

現時点では、NuGet では、カスタム資格情報プロバイダーのデバッグを直接サポートする機能はあまり提供されていません。 [問題 4598](https://github.com/NuGet/Home/issues/4598) は、この作業を追跡しています。

次の操作を実行することもできます。

- スイッチnuget.exeを実行 `-verbosity` して、詳細な出力を検査します。
- 適切な場所にデバッグ `stdout` メッセージを追加します。
- 3.3 以上のnuget.exeしてください。
- 次のコード スニペットを使用して、起動時にデバッガーをアタッチします。

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
