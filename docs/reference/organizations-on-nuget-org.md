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
ms.locfileid: "34449579"
---
# <a name="organization-on-nugetorg"></a><span data-ttu-id="b1593-103">Nuget.org に組織</span><span class="sxs-lookup"><span data-stu-id="b1593-103">Organization on nuget.org</span></span>

<span data-ttu-id="b1593-104">組織は、企業やオープン ソース プロジェクト単一 nuget.org id を使用してパッケージでの共同作業を有効にします。</span><span class="sxs-lookup"><span data-stu-id="b1593-104">Organizations enable businesses and open-source projects to collaborate on packages using a single nuget.org identity.</span></span> <span data-ttu-id="b1593-105">パッケージのコンシューマーでは、「組織アカウント nuget.org に存在するユーザー アカウントと同じが表示されます。</span><span class="sxs-lookup"><span data-stu-id="b1593-105">For a package consumer, an organization account appears same as an existing user account on nuget.org.</span></span>

## <a name="user-accounts-vs-organization-accounts"></a><span data-ttu-id="b1593-106">組織アカウントとユーザー アカウント</span><span class="sxs-lookup"><span data-stu-id="b1593-106">User accounts vs. organization accounts</span></span>

<span data-ttu-id="b1593-107">自分のユーザー アカウントは、本人 nuget.org で任意の数の組織のメンバーであることができます。</span><span class="sxs-lookup"><span data-stu-id="b1593-107">Your user account is your identity on nuget.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="b1593-108">パッケージは、ユーザー アカウントが所属できることと同じように組織アカウントに属していることができます。</span><span class="sxs-lookup"><span data-stu-id="b1593-108">A package can belong to an organization account like it can belong to a user account.</span></span> <span data-ttu-id="b1593-109">パッケージ使用者は、ユーザー アカウントまたは組織アカウントとの違いを表示されない: パッケージとして表示されます両方`owners`です。</span><span class="sxs-lookup"><span data-stu-id="b1593-109">Package consumers don't see any difference between an user account or the organization account: both appear as package `owners`.</span></span>

<span data-ttu-id="b1593-110">組織アカウントは、1 つまたは複数のユーザー アカウントをメンバーとして持ちます。</span><span class="sxs-lookup"><span data-stu-id="b1593-110">An organization account has one or more user accounts as its members.</span></span> <span data-ttu-id="b1593-111">これらのメンバーは、単一の id の所有権を維持しながら、一連のパッケージを管理できます。</span><span class="sxs-lookup"><span data-stu-id="b1593-111">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="b1593-112">新しい組織を追加します。</span><span class="sxs-lookup"><span data-stu-id="b1593-112">Adding a new organization</span></span>

<span data-ttu-id="b1593-113">新しい組織を追加するには、nuget.org、上のアカウントを選択し、選択、**組織を管理しています.** メニュー コマンド。</span><span class="sxs-lookup"><span data-stu-id="b1593-113">To add a new organization, select your account on nuget.org, then select the **Manage Organizations...** menu command:</span></span>

![Nuget.org のマネージャーの組織のメニュー オプション](media/org-manage-option.png)

<span data-ttu-id="b1593-115">次のページで選択、**新しい組織を追加**ボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b1593-115">On the next page, select the **Add new organization** button:</span></span>

![Nuget.org で新しい組織を作成するにはボタン](media/org-add-new-option.png)

<span data-ttu-id="b1593-117">次のページで、組織の名前と電子メール アドレスを提供します。</span><span class="sxs-lookup"><span data-stu-id="b1593-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="b1593-118">組織アカウントがユーザー アカウントと同じ名前空間を共有するため、組織名がその他の既存の組織またはユーザー アカウントと異なる場合があります。</span><span class="sxs-lookup"><span data-stu-id="b1593-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="b1593-119">電子メール アドレスは、すべてのアカウント間で一意あります。</span><span class="sxs-lookup"><span data-stu-id="b1593-119">The email address must also be unique across all accounts.</span></span>

![Nuget.org の組織の新しいページを追加します。](media/org-add-new-page.png)

<span data-ttu-id="b1593-121">組織アカウントが作成されると、管理者であると、組織用のパッケージを送信して組織のメンバーを追加します。</span><span class="sxs-lookup"><span data-stu-id="b1593-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="b1593-122">組織に既存のアカウントを変換します。</span><span class="sxs-lookup"><span data-stu-id="b1593-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="b1593-123">アカウントの変換は元に戻せる状態ではありません。 ユーザー アカウントに、組織を変換することはできません。</span><span class="sxs-lookup"><span data-stu-id="b1593-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="b1593-124">チームの 1 人のユーザー アカウントを使用してパッケージを管理しているし、そのアカウントを使用して、組織に変換する場合、**アカウントは、組織を変換** オプションを選択、 **組織の管理**ページ。</span><span class="sxs-lookup"><span data-stu-id="b1593-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![組織に既存のアカウントを変換する nuget.org でオプション](media/org-transform-option.png)

<span data-ttu-id="b1593-126">次のページで、組織の管理者として割り当てるしを選択する別のユーザー アカウントを指定**変換**です。</span><span class="sxs-lookup"><span data-stu-id="b1593-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![組織にユーザー アカウントを変換するための情報を入力します。](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="b1593-128">組織のメンバーを管理します。</span><span class="sxs-lookup"><span data-stu-id="b1593-128">Managing organization members</span></span>

<span data-ttu-id="b1593-129">組織の管理者として、各メンバーの nuget.org を提供することでメンバーを追加することができます*ユーザー アカウント名*; 電子メール アドレスを使用することはできません。</span><span class="sxs-lookup"><span data-stu-id="b1593-129">As the organization administrator, you can add members by providing each member's nuget.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="b1593-130">各メンバーのコラボレーターまたは次のアクセス許可を持つ管理者としてマークしても。</span><span class="sxs-lookup"><span data-stu-id="b1593-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="b1593-131">アクセス許可</span><span class="sxs-lookup"><span data-stu-id="b1593-131">Permission</span></span> | <span data-ttu-id="b1593-132">コラボレーター</span><span class="sxs-lookup"><span data-stu-id="b1593-132">Collaborator</span></span> | <span data-ttu-id="b1593-133">管理者</span><span class="sxs-lookup"><span data-stu-id="b1593-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1593-134">組織のパッケージを管理します。</span><span class="sxs-lookup"><span data-stu-id="b1593-134">Manage the organization's packages</span></span><br/><span data-ttu-id="b1593-135">新しいパッケージの送信、更新 (既存のパッケージを非公開)</span><span class="sxs-lookup"><span data-stu-id="b1593-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="b1593-136">[はい]</span><span class="sxs-lookup"><span data-stu-id="b1593-136">Yes</span></span> | <span data-ttu-id="b1593-137">[はい]</span><span class="sxs-lookup"><span data-stu-id="b1593-137">Yes</span></span> |
| <span data-ttu-id="b1593-138">組織の変更のメタデータ</span><span class="sxs-lookup"><span data-stu-id="b1593-138">Change organization metadata</span></span><br/><span data-ttu-id="b1593-139">(電子メール アドレス、通知の設定)</span><span class="sxs-lookup"><span data-stu-id="b1593-139">(email address, notification settings)</span></span> | <span data-ttu-id="b1593-140">いいえ</span><span class="sxs-lookup"><span data-stu-id="b1593-140">No</span></span> | <span data-ttu-id="b1593-141">[はい]</span><span class="sxs-lookup"><span data-stu-id="b1593-141">Yes</span></span> |
| <span data-ttu-id="b1593-142">組織のメンバーを管理します。</span><span class="sxs-lookup"><span data-stu-id="b1593-142">Manage organization members</span></span> | <span data-ttu-id="b1593-143">いいえ</span><span class="sxs-lookup"><span data-stu-id="b1593-143">No</span></span> | <span data-ttu-id="b1593-144">[はい]</span><span class="sxs-lookup"><span data-stu-id="b1593-144">Yes</span></span> |
| <span data-ttu-id="b1593-145">要求または組織のパッケージに対して共同で所有する要求操作</span><span class="sxs-lookup"><span data-stu-id="b1593-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="b1593-146">いいえ</span><span class="sxs-lookup"><span data-stu-id="b1593-146">No</span></span> | <span data-ttu-id="b1593-147">[はい]</span><span class="sxs-lookup"><span data-stu-id="b1593-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="b1593-148">パッケージを管理します。</span><span class="sxs-lookup"><span data-stu-id="b1593-148">Managing packages</span></span>

<span data-ttu-id="b1593-149">すべてのパッケージを表示するには、アカウントとそのうちのメンバーであるすべての組織間で、[パッケージの管理](https://www.nuget.org/account/Packages)ページ。</span><span class="sxs-lookup"><span data-stu-id="b1593-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="b1593-150">自分のアカウントまたはその特定の組織に固有のパッケージを表示するには、上にアカウント フィルターを使用、ページの右。</span><span class="sxs-lookup"><span data-stu-id="b1593-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![アカウントのフィルターを使用してパッケージを管理します。](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="b1593-152">組織にパッケージを転送します。</span><span class="sxs-lookup"><span data-stu-id="b1593-152">Transferring packages to an organization</span></span>
<span data-ttu-id="b1593-153">新しく作成した組織に、パッケージの一部を転送する場合は、これを行う併置パッケージを所有する組織アカウントを要求し、自分で、所有者として削除することです。</span><span class="sxs-lookup"><span data-stu-id="b1593-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="b1593-154">管理者は、組織の場合は、確認の所有権に同意する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b1593-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="b1593-155">ただし、コラボレーター場合は、所有者として、組織を追加する必要があります、所有権を受け入れるように管理者のいずれか。</span><span class="sxs-lookup"><span data-stu-id="b1593-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="b1593-156">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="b1593-156">Publishing packages</span></span>

<span data-ttu-id="b1593-157">ユーザー アカウントにパッケージを公開するように、組織にパッケージを公開する: 直接 nuget.org をパッケージをアップロードまたは、パッケージをプッシュして、`nuget push`または`dotnet nuget push`CLI コマンド。</span><span class="sxs-lookup"><span data-stu-id="b1593-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to nuget.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="b1593-158">パッケージをアップロードします。</span><span class="sxs-lookup"><span data-stu-id="b1593-158">Uploading packages</span></span>

<span data-ttu-id="b1593-159">直接アップロードした、新しいパッケージに、 [nuget.org アップロード](https://www.nuget.org/packages/manage/upload) ページで、パッケージの所有者に割り当てるユーザーまたは組織のアカウント。</span><span class="sxs-lookup"><span data-stu-id="b1593-159">When you directly upload a new package on the [nuget.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![アカウント オプションを使用してパッケージをアップロードします。](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="b1593-161">API キーを使用します。</span><span class="sxs-lookup"><span data-stu-id="b1593-161">Using API keys</span></span>

<span data-ttu-id="b1593-162">、パッケージをプッシュする、`nuget push`または`dotnet nuget push`CLI コマンドをそれらのコマンドで必要な API キーを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b1593-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="b1593-163">詳細については、「[パッケージ発行](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)です。</span><span class="sxs-lookup"><span data-stu-id="b1593-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="b1593-164">新しい API キーを作成するときに組織を選択して、適切なで、**パッケージ所有者**ドロップダウンします。</span><span class="sxs-lookup"><span data-stu-id="b1593-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="b1593-165">作成する任意の API キーは、選択した組織にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="b1593-165">Any API key you create is applicable only to the chosen organization:</span></span>

![アカウント オプションを持つ API キー](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="b1593-167">組織の削除</span><span class="sxs-lookup"><span data-stu-id="b1593-167">Removing an organization</span></span>

<span data-ttu-id="b1593-168">ユーザーは、自分を削除できます組織からを選択して、`X`お客様の組織アカウントで表示されるボタンをクリックします。</span><span class="sxs-lookup"><span data-stu-id="b1593-168">As a user, you can remove yourself from an organization by selecting the `X` button shown by your organization membership:</span></span>

![組織のユーザー アカウントを削除します。](media/org-remove-self-option.png)

<span data-ttu-id="b1593-170">管理者は、組織に属するその他の管理者を含む任意のメンバーを削除できます。</span><span class="sxs-lookup"><span data-stu-id="b1593-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="b1593-171">組織の唯一の管理者の場合、自分自身を削除できません、管理者として他のメンバーを追加しない限り、します。</span><span class="sxs-lookup"><span data-stu-id="b1593-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="b1593-172">組織アカウントを削除します。</span><span class="sxs-lookup"><span data-stu-id="b1593-172">Deleting an organization account</span></span>

<span data-ttu-id="b1593-173">この機能は近日公開予定です。</span><span class="sxs-lookup"><span data-stu-id="b1593-173">This feature is coming soon.</span></span>
