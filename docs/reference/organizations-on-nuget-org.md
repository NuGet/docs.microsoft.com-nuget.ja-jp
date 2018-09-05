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
# <a name="organization-on-nugetorg"></a><span data-ttu-id="4db21-103">Nuget.org での組織</span><span class="sxs-lookup"><span data-stu-id="4db21-103">Organization on nuget.org</span></span>

<span data-ttu-id="4db21-104">組織には、企業や nuget.org の 1 つの id を使用してパッケージでの共同作業のオープン ソース プロジェクトが有効にします。</span><span class="sxs-lookup"><span data-stu-id="4db21-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="4db21-105">パッケージのコンシューマーの組織アカウントが nuget.org での既存のユーザー アカウントと同じに表示されます。</span><span class="sxs-lookup"><span data-stu-id="4db21-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="4db21-106">組織アカウントとユーザー アカウント</span><span class="sxs-lookup"><span data-stu-id="4db21-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="4db21-107">ユーザー アカウントが nuget.org で、id と任意の数の組織のメンバーであることができます。</span><span class="sxs-lookup"><span data-stu-id="4db21-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="4db21-108">パッケージは、ユーザー アカウントに属している必要があるように、組織アカウントに属することができます。</span><span class="sxs-lookup"><span data-stu-id="4db21-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="4db21-109">パッケージ利用者は、ユーザー アカウントまたは組織アカウントとの違いを表示されない。 両方とも表示パッケージとして`owners`します。</span><span class="sxs-lookup"><span data-stu-id="4db21-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="4db21-110">組織アカウントは、そのメンバーとして 1 つまたは複数のユーザー アカウントを持ちます。</span><span class="sxs-lookup"><span data-stu-id="4db21-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="4db21-111">これらのメンバーは、所有権を単一の id を維持しながら、一連のパッケージを管理できます。</span><span class="sxs-lookup"><span data-stu-id="4db21-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="4db21-112">新しい組織を追加します。</span><span class="sxs-lookup"><span data-stu-id="4db21-112">Adding a new organization</span></span>

<span data-ttu-id="4db21-113">新しい組織を追加するには、nuget.org には、アカウントを選択し、選択、**組織を管理しています.** メニュー コマンド。</span><span class="sxs-lookup"><span data-stu-id="4db21-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Nuget.org でマネージャーの組織にメニュー オプション](media/org-manage-option.png)

<span data-ttu-id="4db21-115">次のページ選択、**組織の新規追加**ボタン。</span><span class="sxs-lookup"><span data-stu-id="4db21-115">On the next page, select the **Add new organization** button:</span></span>

![Nuget.org で、新しい組織を作成するボタンをクリックします。](media/org-add-new-option.png)

<span data-ttu-id="4db21-117">次のページでは、組織の名前と電子メール アドレスを指定します。</span><span class="sxs-lookup"><span data-stu-id="4db21-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="4db21-118">組織アカウントがユーザー アカウントと同じ名前空間を共有するため、組織名が他の既存の組織またはユーザー アカウントと異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="4db21-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="4db21-119">電子メール アドレスは、すべてのアカウントで一意であります。</span><span class="sxs-lookup"><span data-stu-id="4db21-119">The email address must also be unique across all accounts.</span></span>

![Nuget.org で新しい組織のページを追加します。](media/org-add-new-page.png)

<span data-ttu-id="4db21-121">組織アカウントを作成した後、管理者であると組織用のパッケージを送信して組織のメンバーを追加します。</span><span class="sxs-lookup"><span data-stu-id="4db21-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="4db21-122">組織に既存のアカウントを変換します。</span><span class="sxs-lookup"><span data-stu-id="4db21-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="4db21-123">アカウントの変換は元に戻せる状態ではありません。 ユーザー アカウントに組織を変換することはできません。</span><span class="sxs-lookup"><span data-stu-id="4db21-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="4db21-124">1 人のユーザー アカウントを使用して、チームとしてパッケージを管理しているし、そのアカウントを使用して、組織に変換する場合、**組織にアカウントを変換**オプション、 **組織の管理**ページ。</span><span class="sxs-lookup"><span data-stu-id="4db21-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![Nuget.org で組織に既存のアカウントを変換する オプション](media/org-transform-option.png)

<span data-ttu-id="4db21-126">次のページで、組織の管理者として割り当てるを選択し、別のユーザー アカウントを指定**変換**します。</span><span class="sxs-lookup"><span data-stu-id="4db21-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![組織のユーザー アカウントを変換するための情報を入力します。](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="4db21-128">組織のメンバーを管理します。</span><span class="sxs-lookup"><span data-stu-id="4db21-128">Managing organization members</span></span>

<span data-ttu-id="4db21-129">各メンバーの nuget.org を提供することでメンバーを追加する、組織の管理者として*ユーザー アカウント名*; 電子メール アドレスを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="4db21-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="4db21-130">共同作業者または次のアクセス許可を持つ管理者として、各メンバーをマークします。</span><span class="sxs-lookup"><span data-stu-id="4db21-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="4db21-131">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="4db21-131">Permission</span></span> | <span data-ttu-id="4db21-132">コラボレーター</span><span class="sxs-lookup"><span data-stu-id="4db21-132">Collaborator</span></span> | <span data-ttu-id="4db21-133">管理者</span><span class="sxs-lookup"><span data-stu-id="4db21-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4db21-134">組織のパッケージを管理します。</span><span class="sxs-lookup"><span data-stu-id="4db21-134">Manage the organization's packages</span></span><br/><span data-ttu-id="4db21-135">(新しいパッケージの送信、更新または既存のパッケージを一覧から削除)</span><span class="sxs-lookup"><span data-stu-id="4db21-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="4db21-136">はい</span><span class="sxs-lookup"><span data-stu-id="4db21-136">Yes</span></span> | <span data-ttu-id="4db21-137">はい</span><span class="sxs-lookup"><span data-stu-id="4db21-137">Yes</span></span> |
| <span data-ttu-id="4db21-138">組織の変更のメタデータ</span><span class="sxs-lookup"><span data-stu-id="4db21-138">Change organization metadata</span></span><br/><span data-ttu-id="4db21-139">(電子メール アドレス、通知の設定)</span><span class="sxs-lookup"><span data-stu-id="4db21-139">(email address, notification settings)</span></span> | <span data-ttu-id="4db21-140">いいえ</span><span class="sxs-lookup"><span data-stu-id="4db21-140">No</span></span> | <span data-ttu-id="4db21-141">はい</span><span class="sxs-lookup"><span data-stu-id="4db21-141">Yes</span></span> |
| <span data-ttu-id="4db21-142">組織のメンバーを管理します。</span><span class="sxs-lookup"><span data-stu-id="4db21-142">Manage organization members</span></span> | <span data-ttu-id="4db21-143">いいえ</span><span class="sxs-lookup"><span data-stu-id="4db21-143">No</span></span> | <span data-ttu-id="4db21-144">はい</span><span class="sxs-lookup"><span data-stu-id="4db21-144">Yes</span></span> |
| <span data-ttu-id="4db21-145">要求または組織のパッケージを共同で所有する要求操作</span><span class="sxs-lookup"><span data-stu-id="4db21-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="4db21-146">いいえ</span><span class="sxs-lookup"><span data-stu-id="4db21-146">No</span></span> | <span data-ttu-id="4db21-147">はい</span><span class="sxs-lookup"><span data-stu-id="4db21-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="4db21-148">パッケージの管理</span><span class="sxs-lookup"><span data-stu-id="4db21-148">Managing packages</span></span>

<span data-ttu-id="4db21-149">すべてのパッケージを表示するには、アカウントとすべての組織のメンバーであるうちの間で、[パッケージの管理](https://www.nuget.org/account/Packages)ページ。</span><span class="sxs-lookup"><span data-stu-id="4db21-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="4db21-150">自分のアカウントまたは特定の組織に固有のパッケージを表示するには、上に、アカウント フィルターを使用、ページの右。</span><span class="sxs-lookup"><span data-stu-id="4db21-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![アカウントのフィルターを使用してパッケージを管理します。](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="4db21-152">パッケージを組織に転送します。</span><span class="sxs-lookup"><span data-stu-id="4db21-152">Transferring packages to an organization</span></span>
<span data-ttu-id="4db21-153">新しく作成された組織に、パッケージの一部を転送する場合は、パッケージを共同所有する組織アカウントを要求して、自分で所有者として削除することによって実行できます。</span><span class="sxs-lookup"><span data-stu-id="4db21-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="4db21-154">組織の管理者の場合は、確認の所有権に同意する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="4db21-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="4db21-155">ただし、コラボレーターの場合は、所有者として、組織を追加する必要があります、所有権をそのまま使用する管理者のいずれか。</span><span class="sxs-lookup"><span data-stu-id="4db21-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="4db21-156">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="4db21-156">Publishing packages</span></span>

<span data-ttu-id="4db21-157">ユーザー アカウントにパッケージを発行するように、組織にパッケージを発行する: 直接パッケージを nuget.org にアップロードすることで、またはパッケージをプッシュして、`nuget push`または`dotnet nuget push`CLI コマンド。</span><span class="sxs-lookup"><span data-stu-id="4db21-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="4db21-158">パッケージをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="4db21-158">Uploading packages</span></span>

<span data-ttu-id="4db21-159">直接をアップロードするとき、新しいパッケージを[nuget.org アップロード](https://www.nuget.org/packages/manage/upload) ページで、パッケージ所有者に割り当てるユーザーまたは組織アカウント。</span><span class="sxs-lookup"><span data-stu-id="4db21-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![アカウント オプションを使用してパッケージをアップロードします。](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="4db21-161">API キーを使用します。</span><span class="sxs-lookup"><span data-stu-id="4db21-161">Using API keys</span></span>

<span data-ttu-id="4db21-162">パッケージをプッシュする、`nuget push`または`dotnet nuget push`CLI コマンド、これらのコマンドで必要な API キーを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4db21-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="4db21-163">詳細については、次を参照してください。[パッケージを発行する](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)します。</span><span class="sxs-lookup"><span data-stu-id="4db21-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="4db21-164">新しい API キーを作成するときに、適切な組織でを選択、**パッケージ所有者**ドロップダウンします。</span><span class="sxs-lookup"><span data-stu-id="4db21-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="4db21-165">作成する任意の API キーは、選択した組織にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="4db21-165">Any API key you create is applicable only to the chosen organization:</span></span>

![アカウント オプションを使用して API キー](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="4db21-167">組織を削除します。</span><span class="sxs-lookup"><span data-stu-id="4db21-167">Removing an organization</span></span>

<span data-ttu-id="4db21-168">ユーザーは、自分を削除できます組織からを選択して、`X`組織のメンバーシップによって表示されるボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="4db21-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![組織からユーザー アカウントを削除します。](media/org-remove-self-option.png)

<span data-ttu-id="4db21-170">管理者は、その他の管理者も含む、組織のすべてのメンバーを削除できます。</span><span class="sxs-lookup"><span data-stu-id="4db21-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="4db21-171">唯一の管理者、組織の場合は、自分自身を削除できませんに管理者として別のメンバーを追加しない限り。</span><span class="sxs-lookup"><span data-stu-id="4db21-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="4db21-172">組織アカウントを削除します。</span><span class="sxs-lookup"><span data-stu-id="4db21-172">Deleting an organization account</span></span>

<span data-ttu-id="4db21-173">この機能は近日公開予定。</span><span class="sxs-lookup"><span data-stu-id="4db21-173">This feature is coming soon.</span></span>
