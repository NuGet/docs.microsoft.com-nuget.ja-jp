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
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "67427077"
---
# <a name="your-organization-on-nugetorg"></a><span data-ttu-id="5b72c-103">NuGet.org 上の組織</span><span class="sxs-lookup"><span data-stu-id="5b72c-103">Your organization on NuGet.org</span></span>

<span data-ttu-id="5b72c-104">組織を利用すると、企業やオープンソース プロジェクトで、単一の NuGet.org ID を使って、パッケージに対する共同作業を行うことができます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-104">Organizations enable businesses and open-source projects to collaborate on packages using a single NuGet.org identity.</span></span> <span data-ttu-id="5b72c-105">パッケージ コンシューマーの場合、組織アカウントは NuGet.org の既存のユーザー アカウントと同じように表示されます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-105">For a package consumer, an organization account appears same as an existing user account on NuGet.org.</span></span>

## <a name="organization-accounts-vs-individual-accounts"></a><span data-ttu-id="5b72c-106">組織アカウントと個人アカウント</span><span class="sxs-lookup"><span data-stu-id="5b72c-106">Organization accounts vs. individual accounts</span></span>

<span data-ttu-id="5b72c-107">組織アカウントには、そのメンバーとして 1 つまたは複数の個人 (ユーザー) アカウントが含まれます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-107">An organization account has one or more individual (user) accounts as its members.</span></span> <span data-ttu-id="5b72c-108">これらのメンバーは、所有権用の単一の ID を維持しながら一連のパッケージを管理することができます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-108">These members can manage a set of packages while maintaining a single identity for ownership.</span></span>

<span data-ttu-id="5b72c-109">個人アカウントは NuGet.org での自分の ID であり、任意の数の組織のメンバーになることができます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-109">Your individual account is your identity on NuGet.org and can be a member of any number of organizations.</span></span> <span data-ttu-id="5b72c-110">パッケージは、個人アカウントに属することができるのと同様に、組織アカウントに属することもできます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-110">A package can belong to an organization account like it can belong to an individual account.</span></span> <span data-ttu-id="5b72c-111">パッケージ コンシューマーには、個人アカウントと組織アカウントの違いは表示されません。どちらもパッケージ `owners` として表示されます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-111">Package consumers don't see any difference between an individual account or the organization account: both appear as package `owners`.</span></span>

## <a name="adding-a-new-organization"></a><span data-ttu-id="5b72c-112">新しい組織を追加する</span><span class="sxs-lookup"><span data-stu-id="5b72c-112">Adding a new organization</span></span>

<span data-ttu-id="5b72c-113">新しい組織を追加するには、NuGet.org でアカウントを選択してから、 **[Manage Organizations...]\(組織の管理...\)** メニュー コマンドを選択します。</span><span class="sxs-lookup"><span data-stu-id="5b72c-113">To add a new organization, select your account on NuGet.org, then select the **Manage Organizations...** menu command:</span></span>

![NuGet.org での組織管理のメニュー オプション](media/org-manage-option.png)

<span data-ttu-id="5b72c-115">次のページで、 **[Add new organization]\(新しい組織の追加\)** ボタンを選択します。</span><span class="sxs-lookup"><span data-stu-id="5b72c-115">On the next page, select the **Add new organization** button:</span></span>

![NuGet.org での新規組織作成ボタン](media/org-add-new-option.png)

<span data-ttu-id="5b72c-117">次のページで、組織の名前とメール アドレスを指定します。</span><span class="sxs-lookup"><span data-stu-id="5b72c-117">On the next page, provide the organization name and email address.</span></span> <span data-ttu-id="5b72c-118">組織アカウントはユーザー アカウントと同じ名前空間を共有するため、組織名は他の既存の組織アカウントまたはユーザー アカウントと異なるものにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5b72c-118">Since organization accounts share the same namespace as user accounts, the organization name must be different from any other existing organization or user accounts.</span></span> <span data-ttu-id="5b72c-119">メール アドレスは、すべてのアカウントで一意にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="5b72c-119">The email address must also be unique across all accounts.</span></span>

![NuGet.org で新しい組織のページを追加する](media/org-add-new-page.png)

<span data-ttu-id="5b72c-121">組織アカウントを作成したユーザーは管理者になり、組織にパッケージを送信したり、組織のメンバーを追加したりできます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-121">Once the organization account is created, you are the administrator and can submit packages for the organization and add organization members.</span></span>

### <a name="transform-existing-account-to-an-organization"></a><span data-ttu-id="5b72c-122">既存のアカウントを組織に変換する</span><span class="sxs-lookup"><span data-stu-id="5b72c-122">Transform existing account to an organization</span></span>

> [!Warning]
> <span data-ttu-id="5b72c-123">アカウントの変換を取り消すことはできません。組織を変換してユーザー アカウントに戻すことはできません。</span><span class="sxs-lookup"><span data-stu-id="5b72c-123">Account conversion is irreversible: you cannot transform an organization back to a user account.</span></span>

<span data-ttu-id="5b72c-124">1 つのユーザー アカウントを使ってチームとしてパッケージを管理していて、そのアカウントを組織に変換したい場合は、 **[Manage Organizations]\(組織の管理\)** ページの **[Transform your account to an organization]\(アカウントを組織に変換する\)** オプションを使います。</span><span class="sxs-lookup"><span data-stu-id="5b72c-124">If you're managing packages as a team using a single user account and would like to convert that account into an organization, use the **Transform your account to an organization** option on the **Manage Organizations** page:</span></span>

![既存のアカウントを組織に変換する NuGet.org のオプション](media/org-transform-option.png)

<span data-ttu-id="5b72c-126">次のページで、組織の管理者として割り当てる別のユーザー アカウントを指定し、 **[Transform]\(変換\)** を選択します。</span><span class="sxs-lookup"><span data-stu-id="5b72c-126">On the next page, specify different user account to assign as the administrator of the organization, then select **Transform**.</span></span>

![ユーザー アカウントを組織に変換するための情報の入力](media/org-transform-page.png)

## <a name="managing-organization-members"></a><span data-ttu-id="5b72c-128">組織のメンバーを管理する</span><span class="sxs-lookup"><span data-stu-id="5b72c-128">Managing organization members</span></span>

<span data-ttu-id="5b72c-129">組織の管理者は、各メンバーの NuGet.org の "*ユーザー アカウント名*" を指定することで、メンバーを追加できます。メール アドレスは使用できません。</span><span class="sxs-lookup"><span data-stu-id="5b72c-129">As the organization administrator, you can add members by providing each member's NuGet.org *user account name*; email addresses cannot be used.</span></span> <span data-ttu-id="5b72c-130">その後、各メンバーを次のアクセス許可を持つコラボレーターまたは管理者として指定します。</span><span class="sxs-lookup"><span data-stu-id="5b72c-130">You then mark each member as a collaborator or administrator with the following permissions:</span></span>

| <span data-ttu-id="5b72c-131">権限</span><span class="sxs-lookup"><span data-stu-id="5b72c-131">Permission</span></span> | <span data-ttu-id="5b72c-132">コラボレーター</span><span class="sxs-lookup"><span data-stu-id="5b72c-132">Collaborator</span></span> | <span data-ttu-id="5b72c-133">管理者</span><span class="sxs-lookup"><span data-stu-id="5b72c-133">Administrator</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5b72c-134">組織のパッケージを管理する</span><span class="sxs-lookup"><span data-stu-id="5b72c-134">Manage the organization's packages</span></span><br/><span data-ttu-id="5b72c-135">(新しいパッケージの送信、既存のパッケージの更新またはリストからの削除)</span><span class="sxs-lookup"><span data-stu-id="5b72c-135">(submit new packages, update or unlist existing packages)</span></span> | <span data-ttu-id="5b72c-136">はい</span><span class="sxs-lookup"><span data-stu-id="5b72c-136">Yes</span></span> | <span data-ttu-id="5b72c-137">はい</span><span class="sxs-lookup"><span data-stu-id="5b72c-137">Yes</span></span> |
| <span data-ttu-id="5b72c-138">組織のメタデータを変更する</span><span class="sxs-lookup"><span data-stu-id="5b72c-138">Change organization metadata</span></span><br/><span data-ttu-id="5b72c-139">(メール アドレス、通知の設定)</span><span class="sxs-lookup"><span data-stu-id="5b72c-139">(email address, notification settings)</span></span> | <span data-ttu-id="5b72c-140">いいえ</span><span class="sxs-lookup"><span data-stu-id="5b72c-140">No</span></span> | <span data-ttu-id="5b72c-141">はい</span><span class="sxs-lookup"><span data-stu-id="5b72c-141">Yes</span></span> |
| <span data-ttu-id="5b72c-142">組織のメンバーを管理する</span><span class="sxs-lookup"><span data-stu-id="5b72c-142">Manage organization members</span></span> | <span data-ttu-id="5b72c-143">いいえ</span><span class="sxs-lookup"><span data-stu-id="5b72c-143">No</span></span> | <span data-ttu-id="5b72c-144">はい</span><span class="sxs-lookup"><span data-stu-id="5b72c-144">Yes</span></span> |
| <span data-ttu-id="5b72c-145">組織のパッケージに対する共同所有権を要求または処理する</span><span class="sxs-lookup"><span data-stu-id="5b72c-145">Request or act on co-ownership requests for organization packages</span></span> | <span data-ttu-id="5b72c-146">いいえ</span><span class="sxs-lookup"><span data-stu-id="5b72c-146">No</span></span> | <span data-ttu-id="5b72c-147">はい</span><span class="sxs-lookup"><span data-stu-id="5b72c-147">Yes</span></span> |

## <a name="managing-packages"></a><span data-ttu-id="5b72c-148">パッケージを管理する</span><span class="sxs-lookup"><span data-stu-id="5b72c-148">Managing packages</span></span>

<span data-ttu-id="5b72c-149">自分のアカウントおよび自分がメンバーになっているすべての組織のすべてのパッケージを、[[Manage Packages]\(パッケージの管理\)](https://www.nuget.org/account/Packages) ページで表示できます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-149">You can view all the packages across your account and all organizations of which you're a member on the [Manage Packages](https://www.nuget.org/account/Packages) page.</span></span> <span data-ttu-id="5b72c-150">自分のアカウントまたは特定の組織に固有のパッケージを表示するには、ページの右上にあるアカウント フィルターを使います。</span><span class="sxs-lookup"><span data-stu-id="5b72c-150">To view the packages specific to your account or any specific organization, use the accounts filter on the top right of the page.</span></span>

![アカウント フィルターでパッケージを管理する](media/org-manage-packages-option.png)

### <a name="transferring-packages-to-an-organization"></a><span data-ttu-id="5b72c-152">パッケージを組織に転送する</span><span class="sxs-lookup"><span data-stu-id="5b72c-152">Transferring packages to an organization</span></span>
<span data-ttu-id="5b72c-153">新しく作成した組織にパッケージの一部を転送する場合は、パッケージを共同所有する組織アカウントを要求した後、所有者としての自分自身を削除することによって実行できます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-153">If you wish to transfer some of your packages to a newly created organization, you can do so by requesting the organization account to co-own the package and then removing yourself as the owner.</span></span> <span data-ttu-id="5b72c-154">組織の管理者の場合は、所有権に同意する確認は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="5b72c-154">If you are an administrator of the organization, there is no confirmation required to accept the ownership.</span></span> <span data-ttu-id="5b72c-155">一方、コラボレーターの場合は、所有者として組織を追加するには、管理者の 1 人が所有権に同意する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5b72c-155">However, if you are a collaborator, adding the organization as an owner requires one of the administrators to accept the ownership.</span></span>

## <a name="publishing-packages"></a><span data-ttu-id="5b72c-156">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="5b72c-156">Publishing packages</span></span>

<span data-ttu-id="5b72c-157">ユーザー アカウントにパッケージを公開するように、組織にパッケージを公開します。そのためには、パッケージを NuGet.org に直接アップロードするか、または CLI コマンドの `nuget push` または `dotnet nuget push` を使用してパッケージをプッシュします。</span><span class="sxs-lookup"><span data-stu-id="5b72c-157">You publish packages to an organization like you publish packages to a user account: by directly uploading the package to NuGet.org or by pushing the package through the `nuget push` or `dotnet nuget push` CLI commands.</span></span>

### <a name="uploading-packages"></a><span data-ttu-id="5b72c-158">パッケージをアップロードする</span><span class="sxs-lookup"><span data-stu-id="5b72c-158">Uploading packages</span></span>

<span data-ttu-id="5b72c-159">[NuGet.org のアップロード](https://www.nuget.org/packages/manage/upload) ページで新しいパッケージを直接アップロードするときは、パッケージの所有者をユーザー アカウントまたは組織アカウントに割り当てます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-159">When you directly upload a new package on the [NuGet.org Upload](https://www.nuget.org/packages/manage/upload) page, you assign the package owner to a user or organization account :</span></span>

![アカウントでのパッケージ アップロード オプション](media/org-upload-option.png)

### <a name="using-api-keys"></a><span data-ttu-id="5b72c-161">API キーを使用する</span><span class="sxs-lookup"><span data-stu-id="5b72c-161">Using API keys</span></span>

<span data-ttu-id="5b72c-162">`nuget push` または `dotnet nuget push` CLI コマンドでパッケージをプッシュするには、それらのコマンドで必要な API キーを取得する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5b72c-162">To push a package through the `nuget push` or `dotnet nuget push` CLI commands, you must obtain an API key needed by those commands.</span></span> <span data-ttu-id="5b72c-163">詳しくは、「[パッケージを公開する](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package)」をご覧ください。</span><span class="sxs-lookup"><span data-stu-id="5b72c-163">For details, see [Publish a package](../quickstart/create-and-publish-a-package-using-visual-studio.md#publish-the-package).</span></span>

<span data-ttu-id="5b72c-164">新しい API キーを作成するときは、 **[Package Owner]\(パッケージ所有者\)** ドロップダウンで適切な組織を選択します。</span><span class="sxs-lookup"><span data-stu-id="5b72c-164">When creating a new API key, select the appropriate organization in the **Package Owner** drop down.</span></span> <span data-ttu-id="5b72c-165">作成した API キーは、選択した組織にのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-165">Any API key you create is applicable only to the chosen organization:</span></span>

![アカウントでの API キー オプション](media/org-apikey-option.png)

## <a name="removing-an-organization"></a><span data-ttu-id="5b72c-167">組織を削除する</span><span class="sxs-lookup"><span data-stu-id="5b72c-167">Removing an organization</span></span>

<span data-ttu-id="5b72c-168">ユーザーは、組織のメンバーシップによって表示される **[X]** ボタンを選択することで、自分自身を組織から削除できます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-168">As a user, you can remove yourself from an organization by selecting the **X** button shown by your organization membership:</span></span>

![組織からのユーザー アカウントの削除](media/org-remove-self-option.png)

<span data-ttu-id="5b72c-170">管理者は、他の管理者も含めて、組織から任意のメンバーを削除できます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-170">Administrators can remove any member from the organization, including other administrators.</span></span> <span data-ttu-id="5b72c-171">自分が組織の唯一の管理者である場合は、別のメンバーを管理者として追加しない限り、自分自身を削除することはできません。</span><span class="sxs-lookup"><span data-stu-id="5b72c-171">If you're the sole administrator for an organization, you cannot remove yourself unless you add another member as an administrator.</span></span>

### <a name="deleting-an-organization-account"></a><span data-ttu-id="5b72c-172">組織アカウントを削除する</span><span class="sxs-lookup"><span data-stu-id="5b72c-172">Deleting an organization account</span></span>

<span data-ttu-id="5b72c-173">組織ページに表示される **[Delete]\(削除\)** ボタンをクリックすることによって、組織アカウントを削除できます。</span><span class="sxs-lookup"><span data-stu-id="5b72c-173">You can delete an organization account by clicking the **Delete** button shown in your organization page.</span></span>

![組織の削除](media/org-delete-option.png)

<span data-ttu-id="5b72c-175">組織を削除するには、 **[Delete organization]\(組織を削除する\)** 確認ボタンをクリックして確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="5b72c-175">To delete the organizaiton, you must confirm it by clicking the **Delete organization** confirmation button.</span></span>
