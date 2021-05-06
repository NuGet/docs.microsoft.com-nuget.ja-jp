---
title: スコープ設定された API キー
description: パッケージをプッシュするために使用する API キーを管理します。
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: a3d2504528249f3545e2eb5d9bce7713029638db
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901591"
---
# <a name="scoped-api-keys"></a><span data-ttu-id="d00fb-103">スコープ設定された API キー</span><span class="sxs-lookup"><span data-stu-id="d00fb-103">Scoped API keys</span></span>

<span data-ttu-id="d00fb-104">NuGet をパッケージ配布用のより安全な環境にするために、スコープを追加して API キーを管理することができます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-104">To make NuGet a more secure environment for package distribution, you can take control of the API keys by adding scopes.</span></span>

<span data-ttu-id="d00fb-105">ご利用の API キーにスコープを指定する機能により、ご利用の API に対する制御性を高めることができます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-105">The ability to provide scope to your API keys give you better control on your APIs.</span></span> <span data-ttu-id="d00fb-106">次のことを実行できます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-106">You can:</span></span>

- <span data-ttu-id="d00fb-107">有効期間が異なるさまざまなパッケージに対して使用できる、スコープ設定された API キーを複数作成する。</span><span class="sxs-lookup"><span data-stu-id="d00fb-107">Create multiple scoped API keys that can be used for different packages with varying expiration timeframes.</span></span>
- <span data-ttu-id="d00fb-108">API キーを安全に取得する。</span><span class="sxs-lookup"><span data-stu-id="d00fb-108">Obtain API keys securely.</span></span>
- <span data-ttu-id="d00fb-109">既存の API キーを編集してパッケージの適用性を変更する。</span><span class="sxs-lookup"><span data-stu-id="d00fb-109">Edit existing API keys to change package applicability.</span></span>
- <span data-ttu-id="d00fb-110">他のキーを使用した操作を妨げることなく、既存の API キーを更新または削除する。</span><span class="sxs-lookup"><span data-stu-id="d00fb-110">Refresh or delete existing API keys without hampering operations using other keys.</span></span>

## <a name="why-do-we-support-scoped-api-keys"></a><span data-ttu-id="d00fb-111">スコープ設定された API キーをサポートする理由</span><span class="sxs-lookup"><span data-stu-id="d00fb-111">Why do we support scoped API keys?</span></span>

<span data-ttu-id="d00fb-112">お客様がより粒度の細かいアクセス許可を持つことができるように、API キーのスコープをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d00fb-112">We support scopes for API keys to allow you to have more fine-grained permissions.</span></span> <span data-ttu-id="d00fb-113">これまで、NuGet ではアカウントに対して単一の API キーが提供されていましたが、この方法には次に示すいくつかの欠点がありました。</span><span class="sxs-lookup"><span data-stu-id="d00fb-113">Previously, NuGet offered a single API key for an account, and that approach had several drawbacks:</span></span>

- <span data-ttu-id="d00fb-114">**1 つの API キーですべてのパッケージを制御する**。</span><span class="sxs-lookup"><span data-stu-id="d00fb-114">**One API key to control all packages**.</span></span> <span data-ttu-id="d00fb-115">すべてのパッケージを管理するために使用される単一の API キーの場合は、複数の開発者がさまざまなパッケージに関与していてるときやそれらの開発者が公開元アカウントを共有するときに、キーを安全に共有することが困難です。</span><span class="sxs-lookup"><span data-stu-id="d00fb-115">With a single API key that is used to manage all packages, it is difficult to securely share the key when multiple developers are involved with different packages, and when they share a publisher account.</span></span>
- <span data-ttu-id="d00fb-116">**すべてのアクセス許可、または何もない**。</span><span class="sxs-lookup"><span data-stu-id="d00fb-116">**All permissions or none**.</span></span> <span data-ttu-id="d00fb-117">API キーへのアクセス権を持つすべての人に、そのパッケージに対するすべての許可 (公開、プッシュ、およびリスト解除) が与えられます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-117">Anyone with access to the API key has all permissions (publish, push and un-list) on the packages.</span></span> <span data-ttu-id="d00fb-118">これは、多くの場合、複数のチームが存在する環境では望ましくありません。</span><span class="sxs-lookup"><span data-stu-id="d00fb-118">This is often not desirable in environment with multiple teams.</span></span>
- <span data-ttu-id="d00fb-119">**単一地点での障害**。</span><span class="sxs-lookup"><span data-stu-id="d00fb-119">**Single point of failure**.</span></span> <span data-ttu-id="d00fb-120">単一の API キーでは、単一障害点も発生します。</span><span class="sxs-lookup"><span data-stu-id="d00fb-120">A single API key also means a single point of failure.</span></span> <span data-ttu-id="d00fb-121">キーが侵害されると、そのアカウントに関連付けられているすべてのパッケージが侵害される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="d00fb-121">If the key is compromised, all packages associated with the account could potentially be compromised.</span></span> <span data-ttu-id="d00fb-122">API キーを更新することが、リークを塞ぎ、ご利用の CI/CD ワークフローの中断を回避する唯一の方法です。</span><span class="sxs-lookup"><span data-stu-id="d00fb-122">Refreshing the API key is the only way to plug the leak and avoid an interruption to your CI/CD workflow.</span></span> <span data-ttu-id="d00fb-123">さらに、個人を対象にして API キーへのアクセスを無効にしたい場合があります (たとえば、従業員が離職した場合など)。</span><span class="sxs-lookup"><span data-stu-id="d00fb-123">In addition, there may be cases when you want to revoke access to the API key for an individual (for example, when an employee leaves the organization).</span></span> <span data-ttu-id="d00fb-124">現在、これを処理する適切な方法はありません。</span><span class="sxs-lookup"><span data-stu-id="d00fb-124">There isn’t a clean way to handle this today.</span></span>

<span data-ttu-id="d00fb-125">Microsoft では、スコープ設定された API キーによって、既存のワークフローのいずれも中断することなくこれらの問題に対処することを試みています。</span><span class="sxs-lookup"><span data-stu-id="d00fb-125">With scoped API keys, we try to address these problems while making sure that none of the existing workflows break.</span></span>

## <a name="acquire-an-api-key"></a><span data-ttu-id="d00fb-126">API キーの取得</span><span class="sxs-lookup"><span data-stu-id="d00fb-126">Acquire an API key</span></span>

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a><span data-ttu-id="d00fb-127">スコープ設定された API キーの作成</span><span class="sxs-lookup"><span data-stu-id="d00fb-127">Create scoped API keys</span></span>

<span data-ttu-id="d00fb-128">ご自分の要件に基づいて複数の API キーを作成できます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-128">You can create multiple API keys based on your requirements.</span></span> <span data-ttu-id="d00fb-129">API キーは 1 つまたは複数のパッケージに適用できます。また、API キーには特定の特権を付与するさまざまなスコープを設定し、有効期限を関連付けることができます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-129">An API key can apply to one or more packages, have varying scopes that grant specific privileges, and have an expiration date associated with it.</span></span>

<span data-ttu-id="d00fb-130">次の例では、有効期間が 365 日の `Contoso service CI` という名前の API キーを持っています。これを使用して特定の `Contoso.Service` パッケージに対してパッケージをプッシュすることができます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-130">In the following example, you have an API key named `Contoso service CI` that can be used to push packages for specific `Contoso.Service` packages, and is valid for 365 days.</span></span> <span data-ttu-id="d00fb-131">これは、同じ組織内でさまざまなチームがそれぞれ異なるパッケージで作業していて、チームのメンバーには担当のパッケージに対してのみ特権を付与するキーが提供されるという典型的なシナリオです。</span><span class="sxs-lookup"><span data-stu-id="d00fb-131">This is a typical scenario where different teams within the same organization work on different packages, and the members of the team are provided the key that grants them privileges only for the package they are working on.</span></span> <span data-ttu-id="d00fb-132">有効期限は、キーが古くなったり忘れられたりするのを防ぐためのメカニズムとして機能します。</span><span class="sxs-lookup"><span data-stu-id="d00fb-132">The expiration serves as a mechanism to prevent stale or forgotten keys.</span></span>

![API キーの作成](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a><span data-ttu-id="d00fb-134">glob パターンの使用</span><span class="sxs-lookup"><span data-stu-id="d00fb-134">Use glob patterns</span></span>

<span data-ttu-id="d00fb-135">複数のパッケージで作業していて、管理すべきパッケージのリストが大きくなっている場合は、glob パターンを使用して複数のパッケージをまとめて選択する方法を選択できます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-135">If you are working on multiple packages and have a large list of packages to manage, you can choose to use globbing patterns to select multiple packages together.</span></span> <span data-ttu-id="d00fb-136">たとえば、ID が `Fabrikam.Service` で始まるすべてのパッケージに対するキーに特定のスコープを付与したい場合は、**[Glob パターン]** テキスト ボックスに `fabrikam.service.*` と指定することでそれを行うことが可能です。</span><span class="sxs-lookup"><span data-stu-id="d00fb-136">For example, if you wish to grant specific scopes to a key for all packages whose ID starts with `Fabrikam.Service`, you could do this by specifying `fabrikam.service.*` in the **Glob pattern** text box.</span></span>

![API キーの作成 - 2](media/scoped-api-keys-glob-pattern.png)

<span data-ttu-id="d00fb-138">glob パターンを使用して API キーのアクセス許可を決定する方法は、glob パターンに一致する新しいパッケージにも適用されます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-138">Using glob patterns to determine API key permissions also applies to new packages matching the glob pattern.</span></span> <span data-ttu-id="d00fb-139">たとえば、`Fabrikam.Service.Framework` という名前の新しいパッケージをプッシュしようとしている場合、以前に作成したキーを使用してそれを行うことができます。これは、そのパッケージが glob パターン `fabrikam.service.*` に一致しているためです。</span><span class="sxs-lookup"><span data-stu-id="d00fb-139">For example, if you try to push a new package named `Fabrikam.Service.Framework`, you can do that with the key created previously, since the package matches the glob pattern `fabrikam.service.*`.</span></span>

## <a name="obtain-api-keys-securely"></a><span data-ttu-id="d00fb-140">API キーを安全に取得</span><span class="sxs-lookup"><span data-stu-id="d00fb-140">Obtain API keys securely</span></span>

<span data-ttu-id="d00fb-141">セキュリティ保護のため、新しく作成されたキーは画面上には決して表示されず、**[コピー]** ボタンを使用することでのみ利用できます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-141">For security, a newly created key is never shown on the screen and is only available using the **Copy** button.</span></span> <span data-ttu-id="d00fb-142">同様に、ページが更新された後にキーにアクセスすることはできません。</span><span class="sxs-lookup"><span data-stu-id="d00fb-142">Similarly, the key is not accessible after the page is refreshed.</span></span>

![API キーの作成 - 3](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a><span data-ttu-id="d00fb-144">既存の API キーの編集</span><span class="sxs-lookup"><span data-stu-id="d00fb-144">Edit existing API keys</span></span>

<span data-ttu-id="d00fb-145">キー自体は変更せずにキーのアクセス許可とスコープを更新したい場合もあります。</span><span class="sxs-lookup"><span data-stu-id="d00fb-145">You may also want to update the key permissions and scopes without changing the key itself.</span></span> <span data-ttu-id="d00fb-146">単一のパッケージに対して特定のスコープが設定されたキーがある場合、1 つまたは複数の他のパッケージに同じスコープを適用することを選択できます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-146">If you have a key with specific scope(s) for a single package, you can choose to apply the same scope(s) on one or many other packages.</span></span>

![API キーの作成 - 4](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a><span data-ttu-id="d00fb-148">既存の API キーの更新または削除</span><span class="sxs-lookup"><span data-stu-id="d00fb-148">Refresh or delete existing API keys</span></span>

<span data-ttu-id="d00fb-149">アカウントの所有者はキーを更新することを選択できます。その場合、アクセス許可 (パッケージに対する)、スコープ、および有効期限は変わりありませんが、新しいキーが発行されて古いキーは使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="d00fb-149">The account owner can choose to refresh the key, in which case the permission (on packages), scope, and expiry remain the same, but a new key is issued making the old key unusable.</span></span> <span data-ttu-id="d00fb-150">これは、古いキーを管理する場合や、API キーが漏洩する可能性がある場合に役立ちます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-150">This is helpful in managing stale keys or where there is any potential for an API key leakage.</span></span>

![API キーの作成 - 5](media/scoped-api-keys-refresh.png)

<span data-ttu-id="d00fb-152">これらのキーが不要になった場合は、それらの削除を選択することもできます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-152">You may also choose to delete these keys if they are not needed anymore.</span></span> <span data-ttu-id="d00fb-153">キーを削除すると、そのキーは削除されて使用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="d00fb-153">Deleting a key removes the key and makes it unusable.</span></span>

## <a name="faqs"></a><span data-ttu-id="d00fb-154">FAQ</span><span class="sxs-lookup"><span data-stu-id="d00fb-154">FAQs</span></span>

### <a name="what-happens-to-my-old-legacy-api-key"></a><span data-ttu-id="d00fb-155">古い (レガシ) API キーはどうなりますか?</span><span class="sxs-lookup"><span data-stu-id="d00fb-155">What happens to my old (legacy) API key?</span></span>

<span data-ttu-id="d00fb-156">ご利用の古い (レガシ) API キーは引き続き機能し、ご自分が希望する限りは、機能させることができます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-156">Your old API key (legacy) continues to work and can work as long as you want it to work.</span></span> <span data-ttu-id="d00fb-157">ただし、それらのキーを使用してパッケージをプッシュしていない期間が 365 日を経過した場合、それらは廃止されます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-157">However, these keys will be retired if they have not been used for more than 365 days to push a package.</span></span> <span data-ttu-id="d00fb-158">詳細については、ブログ記事「[Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html)」(期限切れが近い API キーに対する変更点) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d00fb-158">For more details, see the blog post [Changes to expiring API keys](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html).</span></span> <span data-ttu-id="d00fb-159">このキーは更新ができなくなっています。</span><span class="sxs-lookup"><span data-stu-id="d00fb-159">You can no longer refresh this key.</span></span> <span data-ttu-id="d00fb-160">レガシ キーを削除し、スコープ設定された新しいキーを代わりに作成する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d00fb-160">You need to delete the legacy key and create a new scoped key instead.</span></span>

> [!NOTE]
> <span data-ttu-id="d00fb-161">このキーはすべてのパッケージに対するすべての権限を備え、期限切れになることはありません。</span><span class="sxs-lookup"><span data-stu-id="d00fb-161">This key has all permissions on all the packages and it never expires.</span></span> <span data-ttu-id="d00fb-162">このキーを削除し、スコープ設定されたアクセス許可と明確な有効期限を備えた新しいキーを作成することを検討する必要があります。</span><span class="sxs-lookup"><span data-stu-id="d00fb-162">You should consider deleting this key and creating new keys with scoped permissions and definite expiry.</span></span>

### <a name="how-many-api-keys-can-i-create"></a><span data-ttu-id="d00fb-163">API キーはいくつ作成できますか? </span><span class="sxs-lookup"><span data-stu-id="d00fb-163">How many API keys can I create?</span></span>

<span data-ttu-id="d00fb-164">作成できる API キーの数に制限はありません。</span><span class="sxs-lookup"><span data-stu-id="d00fb-164">There is no limit on the number of API keys you can create.</span></span> <span data-ttu-id="d00fb-165">ただし、どこで誰が使用しているのかが把握されていない古いキーが多くなってしまわないように、管理可能な個数に抑えることをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="d00fb-165">However, we advise you to keep it to a manageable count so that you do not end up having many stale keys with no knowledge of where and who is using them.</span></span>

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a><span data-ttu-id="d00fb-166">自分のレガシ API キーを削除したり、今すぐ使用を中止したりできますか?</span><span class="sxs-lookup"><span data-stu-id="d00fb-166">Can I delete my legacy API key or discontinue using now?</span></span>

<span data-ttu-id="d00fb-167">はい。</span><span class="sxs-lookup"><span data-stu-id="d00fb-167">Yes.</span></span> <span data-ttu-id="d00fb-168">ご自分のレガシ API キーは削除することができますし、おそらくそうする必要があります。</span><span class="sxs-lookup"><span data-stu-id="d00fb-168">You can--and you probably should--delete your legacy API key.</span></span>

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a><span data-ttu-id="d00fb-169">誤って削除した自分の API キーを取り戻すことはできますか?</span><span class="sxs-lookup"><span data-stu-id="d00fb-169">Can I get back my API key that I deleted by mistake?</span></span>

<span data-ttu-id="d00fb-170">いいえ。</span><span class="sxs-lookup"><span data-stu-id="d00fb-170">No.</span></span> <span data-ttu-id="d00fb-171">削除されたら、新しいキーを作成するしかありません。</span><span class="sxs-lookup"><span data-stu-id="d00fb-171">Once deleted, you can only create new keys.</span></span> <span data-ttu-id="d00fb-172">誤って削除したキーを元に戻すことはできません。</span><span class="sxs-lookup"><span data-stu-id="d00fb-172">There is no recovery possible for accidentally deleted keys.</span></span>

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a><span data-ttu-id="d00fb-173">古い API キーは、API キーの更新を行っても引き続き機能しますか?</span><span class="sxs-lookup"><span data-stu-id="d00fb-173">Does the old API key continue to work upon API key refresh?</span></span>

<span data-ttu-id="d00fb-174">いいえ。</span><span class="sxs-lookup"><span data-stu-id="d00fb-174">No.</span></span> <span data-ttu-id="d00fb-175">キーを更新すると、古いキーと同じスコープ、アクセス許可、および有効期限を持つ新しいキーが生成されます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-175">Once you refresh a key, a new key gets generated that has the same scope, permission, and expiry as the old one.</span></span> <span data-ttu-id="d00fb-176">古いキー自体は存在しなくなります。</span><span class="sxs-lookup"><span data-stu-id="d00fb-176">The old key ceases to exist.</span></span>

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a><span data-ttu-id="d00fb-177">既存の API キーにさらにアクセス許可を付与することはできますか?</span><span class="sxs-lookup"><span data-stu-id="d00fb-177">Can I give more permissions to an existing API key?</span></span>

<span data-ttu-id="d00fb-178">スコープを変更することはできませんが、それが適用可能なパッケージ リストを編集することはできます。</span><span class="sxs-lookup"><span data-stu-id="d00fb-178">You cannot modify the scope, but you can edit the package list it is applicable to.</span></span>

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a><span data-ttu-id="d00fb-179">自分のキーのいずれかが期限切れになっているかどうか、期限が近づいているかどうかは、どうすればわかりますか?</span><span class="sxs-lookup"><span data-stu-id="d00fb-179">How do I know if any of my keys expired or are getting expired?</span></span>

<span data-ttu-id="d00fb-180">いずれかのキーが期限切れになった場合は、ページ上部に警告メッセージを表示してお知らせします。</span><span class="sxs-lookup"><span data-stu-id="d00fb-180">If any key expires, we will let you know through a warning message at the top of the page.</span></span> <span data-ttu-id="d00fb-181">また、キーの有効期限が切れる 10 日前にアカウントの所有者に警告の電子メールを送信し、事前に対処できるようにしています。</span><span class="sxs-lookup"><span data-stu-id="d00fb-181">We also send a warning e-mail to the account holder ten days before the expiration of the key so that you can act on it well in advance.</span></span>