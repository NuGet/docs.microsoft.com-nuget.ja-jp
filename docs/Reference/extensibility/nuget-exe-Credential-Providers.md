---
title: "nuget.exe 資格情報プロバイダー |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "nuget.exe 資格情報プロバイダーを使用して、フィードを使用認証は、特定の規則に従うコマンドライン実行可能ファイルとして実装されます。"
keywords: nuget.exe credential providers, credential provider API, authenticate with feed, authenticate with gallery
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Nuget.exe 資格情報プロバイダーを使用したフィードの認証

*NuGet 3.3 +*

ときに`nuget.exe`フィードとは、認証する資格情報が必要に次のように検索します。

1. NuGet は、資格情報に最初に`Nuget.Config`ファイル。
1. NuGet は、以下の順序に従って、プラグインの資格情報プロバイダーを使用します。 (例、および、 [Visual Studio Team Services 資格情報プロバイダー](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider))。
1. NuGet し、コマンドラインで資格情報をユーザーに求めます。

ここで説明されている資格情報プロバイダーの機能でのみ注`nuget.exe`'dotnet restore' または Visual Studio ではなく、します。 Visual Studio での資格情報プロバイダーは、次を参照してください[nuget.exe for Visual Studio の資格情報プロバイダー。](nuget-credential-providers-for-visual-studio.md)

nuget.exe 資格情報プロバイダーは、3 つの方法で使用できます。

- **グローバル**: 資格情報プロバイダーのすべてのインスタンスに使用できるようにする`nuget.exe`に追加して、現在のユーザーのプロファイルの下で実行`%LocalAppData%\NuGet\CredentialProviders`です。 作成する必要があります、`CredentialProviders`フォルダーです。 ルートにある資格情報プロバイダーをインストールすることができます、`CredentialProviders`フォルダーまたはサブフォルダー内にあります。 資格情報プロバイダーに複数のファイルまたはアセンブリがある場合は、構成プロバイダーを保持するサブフォルダーを使用できます。

- **環境変数から**: 資格情報プロバイダーを任意の場所に格納し、アクセスできるように`nuget.exe`を設定して、`%NUGET_CREDENTIALPROVIDERS_PATH%`プロバイダーの場所を環境変数。 この変数は、セミコロンで区切ったリストを指定できます (たとえば、 `path1;path2`) 複数の場所がある場合。

- **Nuget.exe と共に**: nuget.exe 資格情報プロバイダーと同じフォルダーに配置できる`nuget.exe`です。

資格情報プロバイダーを読み込むときに`nuget.exe`という名前のファイルの順序で、上記の場所が検索`credentialprovider*.exe`、見つかったいる順序でそれらのファイルを読み込みます。 複数の資格情報プロバイダーは、同じフォルダーに存在する場合は、アルファベット順に読み込まれています。

## <a name="creating-a-nugetexe-credential-provider"></a>Nuget.exe 資格情報プロバイダーを作成します。

資格情報プロバイダーは、コマンドラインの実行可能ファイル形式で名前付き`CredentialProvider*.exe`入力の収集、必要に応じて、資格情報を取得して、適切な終了ステータス コードと標準出力を返します。

プロバイダーでは、次の操作を行います必要があります。

- かどうか、資格情報を入力、対象となる URI の資格情報の取得を開始する前に決定します。 それ以外の場合は、状態コード資格情報を持たない 1 を返す必要があります。
- 変更しない`Nuget.Config`(など、資格情報の設定があります)。
- としての独自の NuGet のハンドル HTTP プロキシの構成は、プラグインをプロキシ情報を提供しません。
- 資格情報またはエラーの詳細を返す`nuget.exe`を標準出力に utf-8 エンコードを使用して JSON 応答オブジェクト (下記参照) を記述します。
- 必要に応じて stderr への追加のトレース ログを出力します。 シークレットこれまでに書き込むかない stderr、"normal"または「詳細」の詳細レベルでこれらのトレースは、NuGet によって、コンソールにエコーためです。
- NuGet の将来のバージョンとの上位互換性を提供する、予期しないパラメーターを無視する必要があります。

### <a name="input-parameters"></a>入力パラメーター

| パラメーターまたはスイッチ |説明|
|----------------|-----------|
| Uri {value} | パッケージ ソース URI が必要な資格情報。|
| NonInteractive | 存在する場合、プロバイダーは対話型のプロンプトを発行しません。 |
| IsRetry | 存在する場合、この試行が以前に失敗した試行の再試行ことを示します。 プロバイダーは、このフラグを使用して通常、任意の既存のキャッシュをバイパスし、可能であれば新しい資格情報の入力を求めることを確認してください。|
| 詳細度 {value} | 存在する場合、次の値のいずれかの:"normal"、「サイレント」または「詳細」です。 値が指定されていない場合は、"normal"に既定値です。 プロバイダーとして使用してくださいこれの省略可能なログ レベルを示す値を標準エラー ストリームに出力します。 |

### <a name="exit-codes"></a>終了コード

| コード |結果 | 説明 |
|----------------|-----------|-----------|
| 0 | 成功 | 資格情報は、正常に取得された、stdout に書き込まれています。|
| 1 | ProviderNotApplicable | 現在のプロバイダーは、指定された URI の資格情報を提供していません。|
| 2 | 失敗 | プロバイダーは、適切なプロバイダー、指定された uri が、資格情報を提供することはできません。 この場合、nuget.exe は認証実行は再試行されませんしは失敗します。 典型的な例は、ユーザーが対話型ログインをキャンセルするとします。 |

### <a name="standard-output"></a>標準出力

| プロパティ |メモ|
|----------------|-----------|
| ユーザー名 | 認証された要求のユーザー名。|
| パスワード | 認証された要求のパスワードです。|
| メッセージ | 失敗した場合の詳細を表示するためだけに使用される、応答の省略可能な詳細はします。 |

例の標準出力:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>資格情報プロバイダーのトラブルシューティング

現時点では、NuGet は、カスタム資格情報のプロバイダーのデバッグの程度を直接サポートを提供しません[発行 4598](https://github.com/NuGet/Home/issues/4598)がこの作業を追跡します。

次の操作を実行することもできます。

- Nuget.exe での実行、`-verbosity`に詳しい出力を検査するスイッチです。
- デバッグ メッセージを追加`stdout`適切な場所にします。
- Nuget.exe 3.3 またはそれ以降を使用していることを確認します。
- このコード スニペットの起動時にデバッガーをアタッチします。

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

詳細については、[要求を送信するサポート、nuget.org](https://www.nuget.org/policies/Contact)です。
