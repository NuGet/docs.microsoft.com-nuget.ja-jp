---
title: nuget.exe 資格情報プロバイダー
description: nuget.exe 資格情報プロバイダーは、フィードで認証し、特定の規則に従うコマンドライン実行可能ファイルとして実装されます。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550190"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Nuget.exe 資格情報プロバイダーでフィードの認証

*NuGet 3.3 以降*

ときに`nuget.exe`フィードで認証する資格情報が必要で、次のように見えます。

1. NuGet は最初に資格情報で`Nuget.Config`ファイル。
1. NuGet は、以下の順序に従って、プラグインの資格情報プロバイダーを使用します。 (例であり、 [Visual Studio Team Services の資格情報プロバイダー](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider))。
1. NuGet は、そのコマンドラインで資格情報のユーザーを求めます。

ここで説明されている資格情報プロバイダーの機能でのみ注`nuget.exe`'dotnet restore' または Visual Studio ではなく、します。 Visual Studio を使用した資格情報プロバイダーは、次を参照してください[nuget.exe for Visual Studio の資格情報プロバイダー。](nuget-credential-providers-for-visual-studio.md)

nuget.exe 資格情報プロバイダーは、3 つの方法で使用できます。

- **グローバルに**: 資格情報プロバイダーのすべてのインスタンスを使用できるように`nuget.exe`を追加してください。 現在のユーザーのプロファイルの下で実行`%LocalAppData%\NuGet\CredentialProviders`します。 作成する必要があります、`CredentialProviders`フォルダー。 ルートにある資格情報プロバイダーをインストールすることができます、`CredentialProviders`フォルダーまたはサブフォルダー内。 資格情報プロバイダーに複数のファイル/アセンブリがある場合は、構成プロバイダーを保持するサブフォルダーを使用できます。

- **環境変数から**: 資格情報プロバイダーを任意の場所に格納しにアクセスできるように`nuget.exe`を設定して、`%NUGET_CREDENTIALPROVIDERS_PATH%`プロバイダーの場所を環境変数。 この変数は、セミコロンで区切ったリストを指定できます (たとえば、 `path1;path2`) 複数の場所がある場合。

- **Nuget.exe と共に**: nuget.exe 資格情報プロバイダーと同じフォルダーに配置できる`nuget.exe`します。

資格情報のプロバイダーの読み込み時に`nuget.exe`という名前のファイルの順序で上記の場所を検索`credentialprovider*.exe`、後に記載してある順序でこれらのファイルを読み込みます。 複数の資格情報プロバイダーは、同じフォルダーに存在する場合は、アルファベット順に読み込まれています。

## <a name="creating-a-nugetexe-credential-provider"></a>Nuget.exe 資格情報プロバイダーを作成します。

資格情報プロバイダーは、コマンドライン実行可能ファイル形式で名前`CredentialProvider*.exe`入力を収集、必要に応じて、資格情報を取得して、適切な終了ステータス コードと標準出力を返します。

プロバイダーでは、次の操作を行う必要があります。

- かどうかを対象となる URI の資格情報が提供資格情報の取得を開始する前に決定します。 必要でない場合は、状態コードを資格情報なしの 1 を返す必要があります。
- 変更しない`Nuget.Config`(など、資格情報の設定があります)。
- としての独自の NuGet のハンドル HTTP プロキシの構成では、プラグインにプロキシ情報は提供されません。
- 資格情報またはエラーの詳細を返す`nuget.exe`標準出力に utf-8 エンコードを使用して JSON 応答オブジェクト (下記参照) を記述しています。
- 必要に応じて stderr に別のトレース ログを出力します。 シークレットする必要がありますこれまでに書き込まれません stderr、"normal"または「詳細」の詳細レベルでこのようなトレースは、コンソールにエコー NuGet ではあるためです。
- NuGet の将来のバージョンと上位互換性を提供する、予期しないパラメーターを無視する必要があります。

### <a name="input-parameters"></a>入力パラメーター

| パラメーターまたはスイッチ |説明|
|----------------|-----------|
| Uri {value} | パッケージはソース URI が必要な資格情報です。|
| NonInteractive | 存在する場合、プロバイダーは対話型のプロンプトを発行しません。 |
| IsRetry | 存在する場合、この試行が以前に失敗した試行の再試行をことを示します。 通常、プロバイダーではこのフラグを使用して、任意の既存のキャッシュをバイパスして、可能であれば新しい資格情報を要求できるようにします。|
| 詳細度 {value} | 存在する場合、次の値のいずれか:"normal"、「サイレント」または「詳細」。 値が指定されていない場合は、"normal"を既定値です。 プロバイダーはこれを使用しての省略可能なログ レベルを示す値として標準エラー ストリームに出力します。 |

### <a name="exit-codes"></a>終了コード

| コード |結果 | 説明 |
|----------------|-----------|-----------|
| 0 | 成功 | 資格情報が正常に取得された、stdout に書き込まれました。|
| 1 | ProviderNotApplicable | 現在のプロバイダーでは、指定された uri の資格情報は提供されません。|
| 2 | 失敗 | プロバイダーが、指定された uri では、適切なプロバイダーが資格情報を提供することはできません。 この場合は、nuget.exe が認証を再試行しません、失敗します。 典型的な例は、ユーザーが対話型ログインをキャンセルするとします。 |

### <a name="standard-output"></a>標準出力

| プロパティ |メモ|
|----------------|-----------|
| [ユーザー名] | 認証された要求のユーザー名。|
| [Password] | 認証された要求のパスワードです。|
| メッセージ | 障害発生時の追加の詳細を表示するためだけに使用される、応答詳細を省略します。 |

例の標準出力:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>資格情報プロバイダーのトラブルシューティング

現時点では、NuGet は、カスタム資格情報プロバイダーをデバッグするため多くダイレクトのサポートを提供しません[発行 4598](https://github.com/NuGet/Home/issues/4598)がこの作業を追跡します。

次の操作を実行することもできます。

- Nuget.exe の実行、`-verbosity`に詳しい出力を検査するスイッチ。
- デバッグ メッセージを追加`stdout`適切な場所にします。
- 3.3 またはそれ以降の nuget.exe を使用していることを確認します。
- このコード スニペットにより、起動時にデバッガーをアタッチするには。

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

詳細については、[サポート リクエストを nuget.org 送信](https://www.nuget.org/policies/Contact)します。
