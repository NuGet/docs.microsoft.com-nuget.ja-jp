---
title: 個人アカウント
description: パッケージを公開するには、NuGet.org での個人アカウントが必要です
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: e1e31e0534706dab43f8d7b1b0db059cd6f29b80
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427137"
---
# <a name="individual-accounts"></a>個人アカウント

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
