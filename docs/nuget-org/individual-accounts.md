---
title: 個人アカウント - NuGet.org
description: パッケージを公開するには、NuGet.org での個人アカウントが必要です
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 7951b3db0cdcaee0a1eb955a5bf6fedce24c79c9
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428631"
---
# <a name="individual-accounts-on-nugetorg"></a>NuGet.org での個人アカウント

NuGet.org でパッケージを公開して管理するには、個人アカウントを作成する必要があります。

## <a name="individual-accounts-vs-organization-accounts"></a>個人アカウントと組織アカウント

個人 (ユーザー) アカウントは NuGet.org での自分の ID であり、任意の数の組織のメンバーになることができます。 パッケージは、個人アカウントに属することができるのと同様に、組織アカウントに属することもできます。 パッケージ コンシューマーには、個人アカウントと組織アカウントの違いは表示されません。どちらもパッケージ `owners` として表示されます。

組織アカウントには、そのメンバーとして 1 つまたは複数の個人アカウントが含まれます。 これらのメンバーは、所有権用の単一の ID を維持しながら一連のパッケージを管理することができます。

## <a name="add-a-new-individual-account"></a>新しい個人アカウントを追加する

NuGet.org アカウントを作成するには、個人の Microsoft アカウント (MSA) または Azure Active Directory (AAD) アカウントが必要です。 nuget.org アカウントをお持ちでない場合は、[作成](https://signup.live.com)できます。 MSA アカウントまたは AAD アカウントがある場合は、次の手順に従います。

1. [NuGet.org のログイン ページ](https://www.nuget.org/users/account/LogOn)に移動します。

1. **[Sign in with Microsoft]\(Microsoft アカウントでサインイン\)** ボタンをクリックします。

1. Microsoft アカウントまたは Azure Active Directory アカウントの詳細を入力します。

1. **[はい]** をクリックして、*NuGet.org* アプリケーションにアクセス許可を与えることに同意してください。

   ![NuGet.org へのアクセス許可の付与](media/nuget-org-permissions.png)

1. *nuget.org* にリダイレクトされ、ユーザー名を登録するように求められます。

1. 入力ボックスに、ユーザー名を指定します。 ユーザー名は大文字と小文字が**区別され**、後から変更できないことに注意してください。

   ![NuGet.org でユーザー名を指定する](media/nuget-org-register.png) 

1. **[Register]\(登録\)** ボタンをクリックします。

これで NuGet.org アカウントが作成されました。 [アカウント設定](https://www.nuget.org/account)ページで、アカウントの管理を実行できます。

## <a name="enable-two-factor-authentication-2fa"></a>2 要素認証を有効にする (2FA)

2 要素認証 (2FA) は、Web サイトまたはアプリにログインするときに使用されるセキュリティの追加のレイヤーです。 2FA を使用する場合は、Microsoft アカウント (MSA) を使用してログインし、自分だけが知っているかアクセスできる別の形式の認証を指定する必要があります。 アカウントの保護を強化するには、2 要素認証を有効にします (推奨)。

1. アカウントにログインしたら、プロファイルを開き、 **[ログイン アカウント]** で **[有効にする]** を選択します。

   ![2FA を有効にする](media/nuget-org-register-2fa.png)

   *nuget.org* への次回サインイン時に追加の資格情報の入力を求められることを示すメッセージが表示されます。

2. この時点で認証を完了するには、サインアウトしてからもう一度サインインします。

3. サインインする際に、2 番目の認証形式としてテキストまたは電子メールを選択します。

   Microsoft アカウントに既に関連付けられている電話番号または電子メールを確認します。 アカウントの新しい電話番号または電子メール アドレスを入力する必要がある場合があります。 その場合は、指示に従って必要な情報を入力し、 **[次へ]** をクリックします。

   ![2FA を有効にする](media/nuget-org-sign-in-2fa.png)

4. デバイスまたは電子メールアカウントを確認し、先ほど送信したコードを入力します。

   ![2FA を有効にする](media/nuget-org-enter-code-2fa.png)

5. 追加の指示に従って、2 要素認証を完了します。

> [!Tip]
> NuGet.org アカウントに対して 2FA を有効にしても、NuGet.org へのログインに使用する Microsoft アカウントにリンクされている可能性のある他のアカウントまたはサービスの認証設定は影響を受けません。

## <a name="delete-a-nugetorg-account"></a>NuGet.org アカウントを削除する

NuGet.org アカウントの削除など、アカウント関連のその他のタスクについては、「[NuGet.org のアカウント管理](nuget-org-faq.md#nugetorg-account-management)」を参照してください。
