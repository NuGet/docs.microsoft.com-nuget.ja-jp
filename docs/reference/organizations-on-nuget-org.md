---
title: Nuget.org 上で、組織
description: Nuget.org 上で、組織では、チームでは、会社の環境またはグループによって公開されているパッケージを管理するのに役立ちます。
author: anangaur
ms.author: anangaur
manager: unnir
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 7f40654a08ac221c5ec3a90c86387b6760b28994
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2018
---
# <a name="organization-on-nugetorg"></a>Nuget.org に組織

組織は、企業やオープン ソース プロジェクト単一 nuget.org id を使用してパッケージでの共同作業を有効にします。 パッケージのコンシューマーでは、「組織アカウント nuget.org に存在するユーザー アカウントと同じが表示されます。

## <a name="user-accounts-vs-organization-accounts"></a>組織アカウントとユーザー アカウント

自分のユーザー アカウントは、本人 nuget.org で任意の数の組織のメンバーであることができます。 パッケージは、ユーザー アカウントが所属できることと同じように組織アカウントに属していることができます。 パッケージ使用者は、ユーザー アカウントまたは組織アカウントとの違いを表示されない: パッケージとして表示されます両方`owners`です。

組織アカウントは、1 つまたは複数のユーザー アカウントをメンバーとして持ちます。 これらのメンバーは、単一の id の所有権を維持しながら、一連のパッケージを管理できます。

## <a name="adding-a-new-organization"></a>新しい組織を追加します。

新しい組織を追加するには、nuget.org、上のアカウントを選択し、選択、**組織を管理しています.** メニュー コマンド。

![Nuget.org のマネージャーの組織のメニュー オプション](media/org-manage-option.png)

次のページで選択、**新しい組織を追加**ボタンをクリックします。

![Nuget.org で新しい組織を作成するにはボタン](media/org-add-new-option.png)

次のページで、組織の名前と電子メール アドレスを提供します。 組織アカウントがユーザー アカウントと同じ名前空間を共有するため、組織名がその他の既存の組織またはユーザー アカウントと異なる場合があります。 電子メール アドレスは、すべてのアカウント間で一意あります。

![Nuget.org の組織の新しいページを追加します。](media/org-add-new-page.png)

組織アカウントが作成されると、管理者であると、組織用のパッケージを送信して組織のメンバーを追加します。

### <a name="transform-existing-account-to-an-organization"></a>組織に既存のアカウントを変換します。

> [!Warning]
> アカウントの変換は元に戻せる状態ではありません。 ユーザー アカウントに、組織を変換することはできません。

チームの 1 人のユーザー アカウントを使用してパッケージを管理しているし、そのアカウントを使用して、組織に変換する場合、**アカウントは、組織を変換** オプションを選択、 **組織の管理**ページ。

![組織に既存のアカウントを変換する nuget.org でオプション](media/org-transform-option.png)

次のページで、組織の管理者として割り当てるしを選択する別のユーザー アカウントを指定**変換**です。

![組織にユーザー アカウントを変換するための情報を入力します。](media/org-transform-page.png)

## <a name="managing-organization-members"></a>組織のメンバーを管理します。

組織の管理者として、各メンバーの nuget.org を提供することでメンバーを追加することができます*ユーザー アカウント名*; 電子メール アドレスを使用することはできません。 各メンバーのコラボレーターまたは次のアクセス許可を持つ管理者としてマークしても。

| アクセス許可 | コラボレーター | 管理者 |
| --- | --- | --- |
| 組織のパッケージを管理します。<br/>新しいパッケージの送信、更新 (既存のパッケージを非公開) | [はい] | [はい] |
| 組織の変更のメタデータ<br/>(電子メール アドレス、通知の設定) | いいえ | [はい] |
| 組織のメンバーを管理します。 | いいえ | [はい] |
| 要求または組織のパッケージに対して共同で所有する要求操作 | いいえ | [はい] |

## <a name="managing-packages"></a>パッケージを管理します。

すべてのパッケージを表示するには、アカウントとそのうちのメンバーであるすべての組織間で、[パッケージの管理](https://www.nuget.org/account/Packages)ページ。 自分のアカウントまたはその特定の組織に固有のパッケージを表示するには、上にアカウント フィルターを使用、ページの右。

![アカウントのフィルターを使用してパッケージを管理します。](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>組織にパッケージを転送します。
新しく作成した組織に、パッケージの一部を転送する場合は、これを行う併置パッケージを所有する組織アカウントを要求し、自分で、所有者として削除することです。 管理者は、組織の場合は、確認の所有権に同意する必要はありません。 ただし、コラボレーター場合は、所有者として、組織を追加する必要があります、所有権を受け入れるように管理者のいずれか。

## <a name="publishing-packages"></a>パッケージを公開する

ユーザー アカウントにパッケージを公開するように、組織にパッケージを公開する: 直接 nuget.org をパッケージをアップロードまたは、パッケージをプッシュして、`nuget push`または`dotnet nuget push`CLI コマンド。

### <a name="uploading-packages"></a>パッケージをアップロードします。

直接アップロードした、新しいパッケージに、 [nuget.org アップロード](https://www.nuget.org/packages/manage/upload) ページで、パッケージの所有者に割り当てるユーザーまたは組織のアカウント。

![アカウント オプションを使用してパッケージをアップロードします。](media/org-upload-option.png)

### <a name="using-api-keys"></a>API キーを使用します。

、パッケージをプッシュする、`nuget push`または`dotnet nuget push`CLI コマンドをそれらのコマンドで必要な API キーを取得する必要があります。 詳細については、「[パッケージ発行](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)です。

新しい API キーを作成するときに組織を選択して、適切なで、**パッケージ所有者**ドロップダウンします。 作成する任意の API キーは、選択した組織にのみ適用されます。

![アカウント オプションを持つ API キー](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>組織の削除

ユーザーは、自分を削除できます組織からを選択して、`X`お客様の組織アカウントで表示されるボタンをクリックします。

![組織のユーザー アカウントを削除します。](media/org-remove-self-option.png)

管理者は、組織に属するその他の管理者を含む任意のメンバーを削除できます。 組織の唯一の管理者の場合、自分自身を削除できません、管理者として他のメンバーを追加しない限り、します。

### <a name="deleting-an-organization-account"></a>組織アカウントを削除します。

この機能は近日公開予定です。
