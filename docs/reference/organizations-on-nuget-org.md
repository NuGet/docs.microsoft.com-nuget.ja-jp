---
title: Nuget.org 上の組織
description: Nuget.org 上の組織では、グループ、またはチームが、会社の環境で公開されているパッケージを管理できます。
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: ea1ca607f169cd31c0a1b59d575d1a743763420c
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551229"
---
# <a name="organization-on-nugetorg"></a>Nuget.org での組織

組織には、企業や nuget.org の 1 つの id を使用してパッケージでの共同作業のオープン ソース プロジェクトが有効にします。 パッケージのコンシューマーの組織アカウントが nuget.org での既存のユーザー アカウントと同じに表示されます。

## <a name="user-accounts-vs-organization-accounts"></a>組織アカウントとユーザー アカウント

ユーザー アカウントが nuget.org で、id と任意の数の組織のメンバーであることができます。 パッケージは、ユーザー アカウントに属している必要があるように、組織アカウントに属することができます。 パッケージ利用者は、ユーザー アカウントまたは組織アカウントとの違いを表示されない。 両方とも表示パッケージとして`owners`します。

組織アカウントは、そのメンバーとして 1 つまたは複数のユーザー アカウントを持ちます。 これらのメンバーは、所有権を単一の id を維持しながら、一連のパッケージを管理できます。

## <a name="adding-a-new-organization"></a>新しい組織を追加します。

新しい組織を追加するには、nuget.org には、アカウントを選択し、選択、**組織を管理しています.** メニュー コマンド。

![Nuget.org でマネージャーの組織にメニュー オプション](media/org-manage-option.png)

次のページ選択、**組織の新規追加**ボタン。

![Nuget.org で、新しい組織を作成するボタンをクリックします。](media/org-add-new-option.png)

次のページでは、組織の名前と電子メール アドレスを指定します。 組織アカウントがユーザー アカウントと同じ名前空間を共有するため、組織名が他の既存の組織またはユーザー アカウントと異なる場合があります。 電子メール アドレスは、すべてのアカウントで一意であります。

![Nuget.org で新しい組織のページを追加します。](media/org-add-new-page.png)

組織アカウントを作成した後、管理者であると組織用のパッケージを送信して組織のメンバーを追加します。

### <a name="transform-existing-account-to-an-organization"></a>組織に既存のアカウントを変換します。

> [!Warning]
> アカウントの変換は元に戻せる状態ではありません。 ユーザー アカウントに組織を変換することはできません。

1 人のユーザー アカウントを使用して、チームとしてパッケージを管理しているし、そのアカウントを使用して、組織に変換する場合、**組織にアカウントを変換**オプション、 **組織の管理**ページ。

![Nuget.org で組織に既存のアカウントを変換する オプション](media/org-transform-option.png)

次のページで、組織の管理者として割り当てるを選択し、別のユーザー アカウントを指定**変換**します。

![組織のユーザー アカウントを変換するための情報を入力します。](media/org-transform-page.png)

## <a name="managing-organization-members"></a>組織のメンバーを管理します。

各メンバーの nuget.org を提供することでメンバーを追加する、組織の管理者として*ユーザー アカウント名*; 電子メール アドレスを使用することはできません。 共同作業者または次のアクセス許可を持つ管理者として、各メンバーをマークします。

| アクセス許可 | コラボレーター | 管理者 |
| --- | --- | --- |
| 組織のパッケージを管理します。<br/>(新しいパッケージの送信、更新または既存のパッケージを一覧から削除) | はい | はい |
| 組織の変更のメタデータ<br/>(電子メール アドレス、通知の設定) | いいえ | はい |
| 組織のメンバーを管理します。 | いいえ | はい |
| 要求または組織のパッケージを共同で所有する要求操作 | いいえ | はい |

## <a name="managing-packages"></a>パッケージの管理

すべてのパッケージを表示するには、アカウントとすべての組織のメンバーであるうちの間で、[パッケージの管理](https://www.nuget.org/account/Packages)ページ。 自分のアカウントまたは特定の組織に固有のパッケージを表示するには、上に、アカウント フィルターを使用、ページの右。

![アカウントのフィルターを使用してパッケージを管理します。](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>パッケージを組織に転送します。
新しく作成された組織に、パッケージの一部を転送する場合は、パッケージを共同所有する組織アカウントを要求して、自分で所有者として削除することによって実行できます。 組織の管理者の場合は、確認の所有権に同意する必要はありません。 ただし、コラボレーターの場合は、所有者として、組織を追加する必要があります、所有権をそのまま使用する管理者のいずれか。

## <a name="publishing-packages"></a>パッケージを公開する

ユーザー アカウントにパッケージを発行するように、組織にパッケージを発行する: 直接パッケージを nuget.org にアップロードすることで、またはパッケージをプッシュして、`nuget push`または`dotnet nuget push`CLI コマンド。

### <a name="uploading-packages"></a>パッケージをアップロードします。

直接をアップロードするとき、新しいパッケージを[nuget.org アップロード](https://www.nuget.org/packages/manage/upload) ページで、パッケージ所有者に割り当てるユーザーまたは組織アカウント。

![アカウント オプションを使用してパッケージをアップロードします。](media/org-upload-option.png)

### <a name="using-api-keys"></a>API キーを使用します。

パッケージをプッシュする、`nuget push`または`dotnet nuget push`CLI コマンド、これらのコマンドで必要な API キーを取得する必要があります。 詳細については、次を参照してください。[パッケージを発行する](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)します。

新しい API キーを作成するときに、適切な組織でを選択、**パッケージ所有者**ドロップダウンします。 作成する任意の API キーは、選択した組織にのみ適用されます。

![アカウント オプションを使用して API キー](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>組織を削除します。

ユーザーは、自分を削除できます組織からを選択して、`X`組織のメンバーシップによって表示されるボタンをクリックします。

![組織からユーザー アカウントを削除します。](media/org-remove-self-option.png)

管理者は、その他の管理者も含む、組織のすべてのメンバーを削除できます。 唯一の管理者、組織の場合は、自分自身を削除できませんに管理者として別のメンバーを追加しない限り。

### <a name="deleting-an-organization-account"></a>組織アカウントを削除します。

この機能は近日公開予定。
