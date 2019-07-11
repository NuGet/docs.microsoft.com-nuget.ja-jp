---
title: NuGet.org 上の組織
description: NuGet.org 上の組織は、グループ、チーム、会社環境で公開されるパッケージを管理するのに役立ちます。
author: anangaur
ms.author: anangaur
ms.date: 04/10/2018
ms.topic: conceptual
ms.reviewer:
- kraigb
- camsoper
ms.openlocfilehash: 152de360bfa31a0c8c60fac0b12149748773b13e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427077"
---
# <a name="your-organization-on-nugetorg"></a>NuGet.org 上の組織

組織を利用すると、企業やオープンソース プロジェクトで、単一の NuGet.org ID を使って、パッケージに対する共同作業を行うことができます。 パッケージ コンシューマーの場合、組織アカウントは NuGet.org の既存のユーザー アカウントと同じように表示されます。

## <a name="organization-accounts-vs-individual-accounts"></a>組織アカウントと個人アカウント

組織アカウントには、そのメンバーとして 1 つまたは複数の個人 (ユーザー) アカウントが含まれます。 これらのメンバーは、所有権用の単一の ID を維持しながら一連のパッケージを管理することができます。

個人アカウントは NuGet.org での自分の ID であり、任意の数の組織のメンバーになることができます。 パッケージは、個人アカウントに属することができるのと同様に、組織アカウントに属することもできます。 パッケージ コンシューマーには、個人アカウントと組織アカウントの違いは表示されません。どちらもパッケージ `owners` として表示されます。

## <a name="adding-a-new-organization"></a>新しい組織を追加する

新しい組織を追加するには、NuGet.org でアカウントを選択してから、 **[Manage Organizations...]\(組織の管理...\)** メニュー コマンドを選択します。

![NuGet.org での組織管理のメニュー オプション](media/org-manage-option.png)

次のページで、 **[Add new organization]\(新しい組織の追加\)** ボタンを選択します。

![NuGet.org での新規組織作成ボタン](media/org-add-new-option.png)

次のページで、組織の名前とメール アドレスを指定します。 組織アカウントはユーザー アカウントと同じ名前空間を共有するため、組織名は他の既存の組織アカウントまたはユーザー アカウントと異なるものにする必要があります。 メール アドレスは、すべてのアカウントで一意にする必要があります。

![NuGet.org で新しい組織のページを追加する](media/org-add-new-page.png)

組織アカウントを作成したユーザーは管理者になり、組織にパッケージを送信したり、組織のメンバーを追加したりできます。

### <a name="transform-existing-account-to-an-organization"></a>既存のアカウントを組織に変換する

> [!Warning]
> アカウントの変換を取り消すことはできません。組織を変換してユーザー アカウントに戻すことはできません。

1 つのユーザー アカウントを使ってチームとしてパッケージを管理していて、そのアカウントを組織に変換したい場合は、 **[Manage Organizations]\(組織の管理\)** ページの **[Transform your account to an organization]\(アカウントを組織に変換する\)** オプションを使います。

![既存のアカウントを組織に変換する NuGet.org のオプション](media/org-transform-option.png)

次のページで、組織の管理者として割り当てる別のユーザー アカウントを指定し、 **[Transform]\(変換\)** を選択します。

![ユーザー アカウントを組織に変換するための情報の入力](media/org-transform-page.png)

## <a name="managing-organization-members"></a>組織のメンバーを管理する

組織の管理者は、各メンバーの NuGet.org の "*ユーザー アカウント名*" を指定することで、メンバーを追加できます。メール アドレスは使用できません。 その後、各メンバーを次のアクセス許可を持つコラボレーターまたは管理者として指定します。

| アクセス許可 | コラボレーター | 管理者 |
| --- | --- | --- |
| 組織のパッケージを管理する<br/>(新しいパッケージの送信、既存のパッケージの更新またはリストからの削除) | はい | はい |
| 組織のメタデータを変更する<br/>(メール アドレス、通知の設定) | いいえ | はい |
| 組織のメンバーを管理する | いいえ | はい |
| 組織のパッケージに対する共同所有権を要求または処理する | いいえ | はい |

## <a name="managing-packages"></a>パッケージを管理する

自分のアカウントおよび自分がメンバーになっているすべての組織のすべてのパッケージを、[[Manage Packages]\(パッケージの管理\)](https://www.nuget.org/account/Packages) ページで表示できます。 自分のアカウントまたは特定の組織に固有のパッケージを表示するには、ページの右上にあるアカウント フィルターを使います。

![アカウント フィルターでパッケージを管理する](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a>パッケージを組織に転送する
新しく作成した組織にパッケージの一部を転送する場合は、パッケージを共同所有する組織アカウントを要求した後、所有者としての自分自身を削除することによって実行できます。 組織の管理者の場合は、所有権に同意する確認は必要ありません。 一方、コラボレーターの場合は、所有者として組織を追加するには、管理者の 1 人が所有権に同意する必要があります。

## <a name="publishing-packages"></a>パッケージを公開する

ユーザー アカウントにパッケージを公開するように、組織にパッケージを公開します。そのためには、パッケージを NuGet.org に直接アップロードするか、または CLI コマンドの `nuget push` または `dotnet nuget push` を使用してパッケージをプッシュします。

### <a name="uploading-packages"></a>パッケージをアップロードする

[NuGet.org のアップロード](https://www.nuget.org/packages/manage/upload) ページで新しいパッケージを直接アップロードするときは、パッケージの所有者をユーザー アカウントまたは組織アカウントに割り当てます。

![アカウントでのパッケージ アップロード オプション](media/org-upload-option.png)

### <a name="using-api-keys"></a>API キーを使用する

`nuget push` または `dotnet nuget push` CLI コマンドでパッケージをプッシュするには、それらのコマンドで必要な API キーを取得する必要があります。 詳しくは、「[パッケージを公開する](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)」をご覧ください。

新しい API キーを作成するときは、 **[Package Owner]\(パッケージ所有者\)** ドロップダウンで適切な組織を選択します。 作成した API キーは、選択した組織にのみ適用されます。

![アカウントでの API キー オプション](media/org-apikey-option.png)

## <a name="removing-an-organization"></a>組織を削除する

ユーザーは、組織のメンバーシップによって表示される **[X]** ボタンを選択することで、自分自身を組織から削除できます。

![組織からのユーザー アカウントの削除](media/org-remove-self-option.png)

管理者は、他の管理者も含めて、組織から任意のメンバーを削除できます。 自分が組織の唯一の管理者である場合は、別のメンバーを管理者として追加しない限り、自分自身を削除することはできません。

### <a name="deleting-an-organization-account"></a>組織アカウントを削除する

組織ページに表示される **[Delete]\(削除\)** ボタンをクリックすることによって、組織アカウントを削除できます。

![組織の削除](media/org-delete-option.png)

組織を削除するには、 **[Delete organization]\(組織を削除する\)** 確認ボタンをクリックして確認する必要があります。
