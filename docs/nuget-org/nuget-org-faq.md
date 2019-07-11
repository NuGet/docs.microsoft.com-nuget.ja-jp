---
title: NuGet.org に関してよく寄せられる質問
description: NuGet ギャラリーの使用に関する一般的な質問と回答
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: c2fc11c0f5dd5d98c40c8b97f9d5a72c4a334b79
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427287"
---
# <a name="nugetorg-frequently-asked-questions"></a>NuGet.org に関してよく寄せられる質問

## <a name="license-terms"></a>ライセンス条項

**パッケージで特定のライセンス情報が提供されない場合の既定のライセンス条項は何ですか?**

各パッケージには、パッケージに含まれている条項が適用されます。 パッケージのアクセス、ダウンロード、または取得の前に、適用される条項を確認する必要があります。 nuget.org で、パッケージ ページの **[ライセンス情報]** リンクを使用します。

パッケージでライセンス条項が指定されていない場合は、nuget.org パッケージ ページの **[Contact owners]\(所有者に問い合わせる\)** リンクを使用して、パッケージ所有者に直接問い合わせてください。 Microsoft はサードパーティのパッケージ プロバイダーを通じてユーザーに知的財産ライセンスを付与することはありません。また、サードパーティによって提供される情報について責任を負いません。

## <a name="managing-packages-on-nugetorg"></a>NuGet.org でのパッケージの管理

**パッケージ メタデータをアップロードしてから編集することはできますか?**

NuGet では、すべてのパッケージに署名することをお勧めしています。 パッケージ署名の設計原理は、署名付きパッケージ コンテンツ (nuspec を含む) は不変でなければならないということです。 パッケージ メタデータを編集すると、nuspec が変更され、既存の署名が無効になります。 パッケージが作成された後にパッケージ メタデータの編集が必要とならないように、既存のワークフローを変更することをお勧めします。

パッケージに対してリストされる依存関係は、パッケージ自体から自動的に生成されるものであり、編集できないことに注意してください。

また、パッケージを [int.nugettest.org](https://int.nugettest.org) にアップロードすることは、パブリック ギャラリーでパッケージを使用できるようにせずに、パッケージをテストして検証する優れた方法です。 API エンドポイント: https://apiint.nugettest.org/v3/index.json

**NuGet.org に発行されたパッケージを削除することはできますか?**

一般に、NuGet.org に発行されたパッケージの削除はサポートしていません。詳細については、[パッケージの削除のポリシー](policies/deleting-packages.md)を参照してください。

**今後発行されるパッケージの名前を予約することはできますか?**

はい。 ご使用のアカウントのパッケージ ID プレフィックスを要求することで、[nuget.org](https://www.nuget.org/) でパッケージの ID を予約できます。 パッケージ ID プレフィックスを要求するには、[ドキュメント](id-prefix-reservation.md)の指示に従ってください。

**パッケージの所有権はどのように要求するのですか?**

「[nuget.org でパッケージ所有者を管理する](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg)」を参照してください。

**ソフトウェア ライセンスに違反しているパッケージ所有者にはどのように対処するのですか?**

NuGet コミュニティと協力して、パッケージ所有者と他のソフトウェアの所有者間で発生する可能性のある紛争を解決することをお勧めします。 [紛争解決プロセス](policies/dispute-resolution.md)が作成されています。nuget.org 管理者に仲裁を求める前にこのプロセスに従ってください。

**nuget.org に自分のテスト パッケージをアップロードするよう勧めされていますか?**

テスト目的で、[int.nugettest.org](https://int.nugettest.org) を使用することができます。また、[myget.org](https://myget.org) や [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/) などの別のパブリック NuGet サーバーを使用することもできます。

int.nugettest.org にアップロードされたパッケージは保持されない場合があることに注意してください。

**nuget.org にアップロードできるパッケージの最大サイズは何ですか?**

nuget.org では最大 250 MB のパッケージをアップロードできますが、可能な場合はパッケージを 1 MB 未満に保ち、依存関係を使用してパッケージを相互にリンクさせることをお勧めします。 一般に、競合を避けるため、パッケージにはアセンブリを 1 つだけ含めます。

NuGet では HTTP を使用してパッケージをダウンロードするため、パッケージが大きいと、小さいパッケージよりもインストールに失敗する可能性が高くなります。

複数のパッケージ間で依存関係を共有することはできます。これにより、NuGet パッケージのコンシューマーの合計ダウンロード サイズが小さくなります。

依存関係は、ほとんどの場合、静的なものであり、変わることはありません。 コードでバグを修正するときは、依存関係の更新が必要ない場合があります。 依存関係をバンドルする場合、結局は毎回大きなパッケージを再配布することになります。 NuGet パッケージを関連する依存関係に分割することで、パッケージのコンシューマーに応じて、アップグレードをより細かく行うことができます。

## <a name="nugetorg-not-accessible"></a>nuget.org にアクセスできない

**nuget.org でパッケージのダウンロードやアップロードができないのはなぜですか?**

まず、最新バージョンの NuGet を使用していることを確認してください。 そのバージョンでも失敗する場合は、[サポートに問い合わせて](https://www.nuget.org/policies/Contact)、次の内容を含む、追加の接続のトラブルシューティングに関する情報を提供してください。

- 使用している NuGet のバージョン
- 使用しているパッケージ ソース
- 詳細な復元ログ
- MTR または Fiddler のトレース (下記参照)
- 地理的地域
- コンピューターがプロキシとファイアウォールのどちらの背後にあるのか?
- コンピューターがクラウド プロバイダーのデータ センター (Azure、AWS など) に配置されているか? 配置されている場合は、プロバイダーの名前とリージョン指定してください。

*MTR をキャプチャするには:*

- [http://winmtr.net/download/](http://winmtr.net/) から WinMTR をダウンロードします
- ホスト名として「`api.nuget.org`」を入力して、 **[開始]** をクリックします。
- **[送信]** 列が 100 以上になるまで待ちます。

    ![MTR のキャプチャ](media/mtr.png)

- クリップボードにテキストをコピーします。

*Fiddler をキャプチャするには:*

- 最新バージョンの [Fiddler](http://www.telerik.com/download/fiddler) をインストールします。
- Fiddler を起動し、 **[ファイル]、[Capture Traffic]\(トラフィックのキャプチャ\)** メニューを使用してトラフィックのキャプチャを無効にします。
- すべてのセッションを削除します (リストのすべての項目を選択して、**Delete** キーを押します)。
- **[ツール]、[Fiddler Options...]\(Fiddler オプション...\)** メニューの **[HTTPS]** タブにある **[Decrypt HTTPS traffic]\(HTTPS トラフィックの暗号化解除\)** をオフにして、HTTPS トラフィックをキャプチャするように Fiddler を構成します。
- Visual Studio を閉じます。
- **[ファイル]、[Capture Traffic]\(トラフィックのキャプチャ\)** メニューを有効にします。
- Visual Studio または nuget.exe を起動して、機能していないアクションを実行します。 これらのアクションによって生成されるトラフィックは Fiddler に表示されます。
- アクションが実行されたら、 **[ファイル]、[保存]、[すべてのセッション]** を使用して、キャプチャされたセッションを保存します。

注: Fiddler を介して NuGet トラフィックをルーティングするために、`HTTP_PROXY` 環境変数を `http://127.0.0.1:8888` に設定する必要がある場合があります。

これが失敗した場合は、[この StackOverflow の投稿に記載されているヒント](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall)を試してください。

## <a name="nugetorg-account-management"></a>nuget.org のアカウント管理

### <a name="how-to-recover-nugetorg-password-login"></a>nuget.org のパスワード ログインを復旧するにはどうすればよいですか?

[nuget.org パスワード ログインは廃止されており](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html)、nuget.org にログインする唯一の方法は、個人の Microsoft アカウント (MSA) または Azure Active Directory (AAD) アカウントを使用することです。 ただし、関連付けられている MSA/AAD アカウントにアクセスできない場合は、nuget.org アカウントを復旧するためにパスワード ログインを使用する必要があります。 このような場合は、次の手順に従います。
- **必要条件:** パスワードを復旧する必要があるアカウントに関連付けられている電子メールに対してアクセス権を持つ必要があります。
- [[Forgot password]\(パスワードを忘れた場合\) ページ](https://www.nuget.org/account/ForgotPassword)に移動します。
- 復旧する nuget.org アカウントに関連付けられている**メール** アドレスを入力します。
- **[Send]** ボタンをクリックします。
- 指定したメール アドレス アカウントに、パスワードをリセットするためのリンクが含まれた電子メールが送信されます。 このリンクをクリックして、新しいパスワードを設定します。 メールが見つからない場合は、迷惑メール フォルダーを確認してください。
- 完了すると、ユーザー名/パスワードを使って NuGet でログインできるようになります。
- ユーザー名/パスワードでログインするには、[nuget.org ログイン ページ](https://www.nuget.org/users/account/LogOn)の **[Sign in using Nuget.org account]\(Nuget.org アカウントを使用してサインインする\)** のリンクを使用します。

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>どの Microsoft アカウントが自分の nuget.org アカウントにリンクされていますか?

どの Microsoft アカウントがご自分の nuget.org アカウントに関連付けられているか忘れてしまった場合は、次の手順に従ってサポートを受けることができます。
1. [nuget.org ログイン ページ](https://www.nuget.org/users/account/LogOn)に移動して、 **[Need assistance signing in?]\(サインイン サポートが必要ですか?\)** リンクをクリックします。
1. サポートのためのポップアップ ダイアログ ボックスが表示されます。 このダイアログ ボックスの手順に従って、ご自分の nuget.org アカウントに関連付けられている Microsoft アカウントを確認します。

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>nuget.org のログインに使用している Microsoft アカウントを変更するにはどうすればよいですか?
nuget.org ユーザーの Microsoft アカウントを変更する場合は、次の手順に従います。 メール アドレス `account1@outlook.com` を持つ Microsoft アカウントが、ユーザー名 `MyNuGetAccount` を持つ nuget.org アカウントに関連付けられているとします。 ログインをメール アドレス `account2@outlook.com` を持つ別の Microsoft アカウントに変更するとします。
1. **[Sign in with Microsoft]\(Microsoft アカウントでサインイン\)** をクリックしてから、[ログイン ページ](https://www.nuget.org/users/account/LogOn)で**現在関連付けられている Microsoft アカウント** (`account1@outlook.com`) を使用してサインインしてください。
1. ログインしたら、[アカウント設定](https://www.nuget.org/account)ページに移動します。
1. **[ログイン アカウント]** セクションを展開します。 **[アカウントの変更]** ボタンをクリックします。
1. Microsoft のログイン ページにリダイレクトされます。 関連付けを `account2@outlook.com` などに変更するアカウントでサインインしてください。**注**: 別の Microsoft アカウントでログインできるようにするには、サインイン フロー中に **[Sign out and sign in with different account]\(サインアウトして別のアカウントでサインインする\)** をクリックする必要がある場合があります。
1. 次のようなエラーが表示された場合は、「[別の nuget.org アカウントにリンクされている Microsoft アカウント](#microsoft-account-is-linked-with-another-nugetorg-account)」で詳細をご覧ください。
    >_'account2 <account2@outlook.com>' で Microsoft アカウントの更新に失敗しました。これは、このアカウントが別の NuGet アカウントに既にリンクされている場合に発生する場合があります。詳細についてはサポートにお問い合わせください。_

1. 2 番目のアカウントで正常にサインインすると、元の nuget.org アカウント設定ページにリダイレクトされます。ここには、ログイン アカウントとして関連付けられた新しい Microsoft アカウントが表示されているはずです。 今後は、nuget.org にサインインするときに、このアカウントを使用する必要があります。

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Microsoft アカウントが別の nuget.org アカウントにリンクされています。

Microsoft ログインを変更しようとすると、次のエラーが表示されました。
> _'account2 <account2@outlook.com>' で Microsoft アカウントの更新に失敗しました。これは、このアカウントが別の NuGet アカウントに既にリンクされている場合に発生する場合があります。詳細についてはサポートにお問い合わせください。_

ユーザー名が `MyNuGetAccount1` の nuget.org ユーザーの Microsoft アカウント ログインを `account1@outlook.com` から、メール アドレスが `account2@outlook.com` の Microsoft アカウントに変更しようとしたとします。 すると、上記のエラーが表示されます。

**上記のエラーはどのような意味ですか?**

このエラーは、変更しようとしている変更先の Microsoft アカウントに関連付けられている別の nuget.org アカウントがあることを意味しています。上記の例では、メール アドレスが `<account2@outlook.com>` の Microsoft アカウントが、たとえば、ユーザー名 `MyNuGetAccount2` を持つ別の nuget.org アカウントに関連付けられています。

別の nuget.org アカウントにリンクされている Microsoft アカウントに関連付けられたログインを変更することはできません。

**自分が別の nuget.org アカウント持っていたことを忘れてしまいした。それがどの nuget.org アカウントだったかを見つけるにはどうしたらよいですか?**

[ログイン ページ](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "ログイン ページ")で 2 番目の Microsoft アカウントを使ってログインします。 これにより 2 番目の Microsoft アカウントに現在関連付けられている nuget.org アカウントにログインします。 次に、アップロードされたパッケージを表示して、このアカウントでアカウント管理を実行できます。

**この 2 番目の nuget.org アカウントには関心がありませんが、最初の nuget.org アカウントのログインを 2 番目の Microsoft アカウントで変更したいのですが、どうしたらよいですか?**

2 番目の nuget.org アカウントに関心はないが、メール アドレス `account2@outlook.com` を持つ関連付けられた Microsoft アカウントを再利用したい場合、 

nuget.org アカウントを削除して、Microsoft アカウントと nuget.org アカウント間の関連付けを解放することができます。
1. 2 番目の nuget.org アカウント `MyNuGetAccount2` の[ユーザーを削除](#how-to-delete-my-nugetorg-account)する手順に従います。 
1. このアカウントを削除すると、[Microsoft アカウント ログインの変更](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login)手順を再試行できます。

**この 2 番目のアカウントにも関心があります。このアカウントを失わずに、最初のアカウントの関連付けられているアカウント ログインを変更するにはどうすればよいですか。**

たとえば、メール アドレスが `account3@outlook.com` の 3 番目の Microsoft アカウントを作成または使用する必要があります。 
1. まず、nuget.org で 2 番目の Microsoft アカウント `account2@outlook.com` を使ってログインします。上記の手順に従って関連付けられているログインを変更し、3 番目の Microsoft アカウントをこの nuget.org アカウントに関連付けます。
1. 完了すると、メール アドレス `account2@outlook.com` を持つ 2 番目の Microsoft アカウントが解放され、最初の nuget.org アカウント `MyNuGetAccount1` に関連付けることができます。 上記の同じ手順に従って、Microsoft ログインを 2 番目の Microsoft アカウントに変更します。

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Microsoft アカウントでサインインすると、自分のメール アドレスが別の Microsoft アカウントにリンクされていることが示されます

たとえばメール アドレス `account1@outlook.com` を持つ Microsoft アカウントでサインインしようとすると、次のようなエラーが表示されます。
> _メール アドレス 'account1@outlook.com' を持つアカウントは別の Microsoft アカウントにリンクされています。_
>
> _リンクされている Microsoft アカウントを更新したい場合は、アカウント設定ページから実行することができます。_

**上記のエラーはどのような意味ですか?**

nuget.org でアカウントが作成されると、そのアカウントに関連付けられた通信用のメール アドレスがあります。 これは通常、関連付けられた Microsoft アカウントに使用されているメール アドレスと同じです。 ただし、通信用に別のメール アドレスを指定することもできます。 そのため、技術的には、`account1@outlook.com` として通信用のメール アドレスを持つ nuget.org アカウントにリンクされている、たとえば `account2@outlook.com` を持つ別の Microsoft アカウントを持つことができます。

したがって上記のエラーは、通信用のメール アドレス `account1@outlook.com` を持つ nuget.org アカウントが既に存在しているが、`account1@outlook.com` **以外**のメール アドレスを持つ別の Microsoft アカウントに関連付けられていることを意味します。

**この nuget.org アカウントにリンクされているのがどの Microsoft アカウントかを調べるにはどうしたらよいですか**

どの Microsoft アカウントがメール アドレスが `account1@outlook.com` の nuget.org アカウントにリンクされているかを調べるには、[サインイン アシスタンス](#which-microsoft-account-is-linked-to-my-nugetorg-account) フローを使用する必要があります。

**そのアカウントを自分の Microsoft アカウントでオーバーライドしたい**

「[Microsoft ログインを使用できません。nuget.org アカウントを復旧する方法を教えてください](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)」セクションの手順に従って、ご自分の Microsoft アカウントを既存の nuget.org アカウントに関連付けます。

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Microsoft ログインを使用できません。nuget.org アカウントを復旧するにはどうすればよいですか?

[サインイン アシスタンス](#which-microsoft-account-is-linked-to-my-nugetorg-account)を使用しようとして、nuget.org アカウントに関連付けられている Microsoft アカウントへのアクセス権がなかった場合は、次の手順に従って、新しい Microsoft アカウントを nuget.org アカウントにリンクしてください。
1. **必要条件**:既存のどの nuget.org アカウントにも関連付けられていない Microsoft アカウントへのアクセス権が必要です。 nuget.org アカウントをお持ちでない場合は、[作成](https://signup.live.com)できます。
2. nuget.org アカウントのユーザー名とパスワードを忘れてしまった場合は、[パスワード ログインを復旧する手順](#how-to-recover-nugetorg-password-login)に従います。
3. ユーザー名/パスワード ログインを使用して、[nuget.org にログイン](https://www.nuget.org/users/account/LogOnNuGetAccount)します。
4. ログインすると、次のようなポップアップ ダイアログが表示されます。 これは、パスワードの終了ダイアログ ボックスです。
5. **注**: 指定された Microsoft アカウントでログインするという指示は無視してください。 これで nuget.org アカウントを他の任意の Microsoft のログインにリンクできます。
6. **[Sign in with Microsoft]\(Microsoft アカウントでサインイン\)** ボタンをクリックして、手順 1 で説明したように、アクセス権がある Microsoft アカウントでログインします。
7. アカウントが新しい Microsoft アカウントにリンクされます。今後は、このアカウントを使用して nuget.org にログインできます。

    ![MSA のリンクのダイアログ](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>自分の nuget.org アカウントを組織に変換するにはどうすればよいですか?

ご自分のアカウントが既に Microsoft アカウント ログインに関連付けられていて、このアカウントを組織に変換する場合は、「[Organizations on nuget org](organizations-on-nuget-org.md)」 (nuget org での組織) のドキュメントに記載されている手順に従ってください。

ただし、nuget.org アカウントが Microsoft アカウントに関連付けられていない、またはリンクされていない場合、次の手順に従ってこのアカウントを組織に変換することができます。
1. **必要条件**:org アカウントで管理者として使用される nuget.org で最初に作成された個人アカウントがある必要あります。 ない場合は、[新しい nuget.org アカウントを作成](individual-accounts.md)してください。
2. nuget.org アカウント用のパスワード ログインがない場合は、[パスワード ログインを復旧する手順](#how-to-recover-nugetorg-password-login)に従います。ある場合は、この手順をスキップします。
3. ユーザー名/パスワード ログインを使用して、[nuget.org にログイン](https://www.nuget.org/users/account/LogOnNuGetAccount)します。
4. ログインすると、次のようなポップアップ ダイアログが表示されます。 これは、パスワードの終了ダイアログ ボックスです。 
    > [!Important]
    > このダイアログ ボックスは無視してください。 **[Microsoft アカウントでサインイン]** ボタンをクリック**しないでください**。

5. [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform) に移動します。 これで Microsoft アカウントにリンクしなくても、nuget.org アカウントを組織に変換できます。
6. 個人の nuget.org アカウントまたは手順 1 で作成したアカウントの管理者ユーザー名を指定します。
7. 指示に従って、このアカウントの組織への変換を完了します。

    ![MSA のリンクのダイアログ](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>管理対象外のテナントでの AAD アカウントの nuget.org ログイン問題とは何ですか?

ご自分のメール アカウント ドメイン (@yourdomain.com) を使用してログイン フロー中に次のようなエラーが表示された場合は、nuget.org アカウントを復旧する次の手順を参照してください。

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**ログイン時のこの管理対象外の状態は何ですか?なぜ今、これが発生するのでしょうか?** 

ご使用のアカウントは、以前に個人の Microsoft アカウントとして登録され、正常に機能していたようですが、現在、このアカウントは Azure Active Directory (Microsoft アカウントを認証するために使用する ID サービス) で "管理対象外" テナントとして登録されているようです。 

これは、自分または組織内の (@yourdomain.com メール アドレスを持つ) ユーザーが AAD 統合サービスのいずれかに登録するか、[Azure Active Directory のセルフサービス サインアップ](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup)を行った場合に発生する可能性があります。これらの操作により、使用した Microsoft アカウント ドメイン (ご自身の @yourdomain.com) に対してこのような "管理対象外" テナントが作成されるからです。 

**自分のアカウントを復旧するにはどうすればよいですか?**

現時点では、nuget.org では、Azure Active Directory でこのような "管理対象外" テナント アカウントを持つアカウントを認証する方法はありません。 このようなアカウントを認証するためのよりよい方法を模索しています。

ご自分の Microsoft アカウント (@yourdomain.com) を使用して nuget.org にログインする場合は、ご自分で (または会社の管理者が) メール アドレス "@yourdomain.com" を持つユーザーを認証するための DNS 検証を行うことで、AAD の所有権を要求する必要があります。 Azure Active Directory で文書化されている[ドメイン管理者の引き継ぎ](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover)手順に従ってください。 これが完了すると、通常のログインが機能し始めるはずです。

**すべては実行したくありません。アカウントを復旧する他の方法はありますか?**

(@yourdomain.com に関連付けられて**いない**メール アドレスを使用して) 新しい Microsoft アカウントを[作成](https://www.microsoft.com/en-us/account)できます。 [nuget.org アカウントの復旧](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account)セクションの手順に従います。

### <a name="how-do-i-change-my-nugetorg-account-username"></a>nuget.org アカウントのユーザー名を変更するにはどうすればよいですか?

変更できません。 ポリシーの問題として、今のところまだユーザー名の変更は許可していません。 ユーザー名を変更する唯一の方法は、目的のユーザー名を使用して新しいアカウントを作成することです。 新しいアカウントを作成する前に、既存アカウントを削除することをお勧めします。削除しないと、登録済みの Microsoft アカウントを再利用できなくなります。
> [!Important]
> ユーザーを削除しても、その `username` は**予約**されたままです。 同じユーザー名をもう一度再利用することはできません。**これには大文字/小文字の変更も含まれます**。 例として、ユーザー名 `mycoolname` を持つユーザーを作成し、これを `MyCoolName` (大文字と小文字の変更) に変更する場合、ユーザーを削除すると変更できなくなります。

[nuget.org アカウントの削除](#how-to-delete-my-nugetorg-account)セクションに記載されている手順に従って、正しいユーザー名を使用して[新しいアカウントを登録](individual-accounts.md)します。

### <a name="how-to-delete-my-nugetorg-account"></a>nuget.org アカウントを削除するにはどうすればよいですか?

アカウントを削除するには、ご自分が唯一の所有者である任意のパッケージの所有権を委譲することをお勧めします。 この方法の詳細については、[パッケージ所有者を管理する](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg)をご覧ください。 これは Microsoft がお客様からの要求に迅速に対応するのにも役立ちます。

> [!Important]
> ユーザーを削除すると、次のことが発生します。
>  1. 関連付けられている API キーが取り消されます。 
>  2. 任意の子パッケージの所有者として、アカウントが削除されます。
>  3. このアカウントに以前から存在するすべての ID プレフィックス予約の関連付けが解除されます。
>  4. 任意の組織のメンバーとしてアカウントが削除されます。
>  5. ユーザー名が予約され、そのユーザーの許可なしでは誰もそのユーザー名を再使用できなくなります。

アカウントの削除を続行するには、次の手順に従います。
1. 削除するアカウントを使用して [nuget.org にログイン](https://www.nuget.org/users/account/LogOn)します。
2. この URL ([https://www.nuget.org/account/delete](https://www.nuget.org/account/delete)) をクリックして、アカウントを削除するための要求を送信する手順に従います。

Microsoft のカスタマー サポートがこの要求を処理し、アカウントの削除を実行します。
