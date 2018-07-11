---
title: ID プレフィックス予約の参照
description: パッケージ ID プレフィックス予約機能の説明、作成者ガイド。
author: diverdan92
ms.author: diverdan92
manager: unnir
ms.date: 10/09/2017
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 10d017d67cf2bd49812c5d54f9fca063f32cc052
ms.sourcegitcommit: 6cffa6ef59b922df2d87aa9c24034d00542983cd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/10/2018
ms.locfileid: "37948396"
---
# <a name="package-id-prefix-reservation"></a><span data-ttu-id="a865b-103">パッケージ ID プレフィックスの予約</span><span class="sxs-lookup"><span data-stu-id="a865b-103">Package ID prefix reservation</span></span>

<span data-ttu-id="a865b-104">パッケージの所有者では、予約でき、ID のプレフィックスを予約して自分の id を保護することができます。</span><span class="sxs-lookup"><span data-stu-id="a865b-104">Package owners can reserve and protect their identity by reserving ID prefixes.</span></span> <span data-ttu-id="a865b-105">パッケージ利用者は、指定された追加情報を含むパッケージの使用時に使用されているパッケージの識別プロパティで偽装されます。</span><span class="sxs-lookup"><span data-stu-id="a865b-105">Package consumers are provided with additional information when consuming packages that the package they are consuming are not deceptive in their identifying properties.</span></span> 

<span data-ttu-id="a865b-106">[nuget.org](https://www.nuget.org/) Visual Studio 2017 バージョン 15.4 以降、パッケージが予約済みの ID と一致する限り、予約済みのパッケージ ID プレフィックスを持つ所有者によって送信されたパッケージの名前付けパターンのプレフィックスの視覚的なインジケーターを表示するとします。</span><span class="sxs-lookup"><span data-stu-id="a865b-106">[nuget.org](https://www.nuget.org/) and Visual Studio 2017 version 15.4 or later show a visual indicator for packages that are submitted by owners with a reserved package ID prefix, as long as the package matches the reserved ID prefix naming pattern.</span></span> <span data-ttu-id="a865b-107">以下の参照 ID プレフィックス予約伴います、ID のプレフィックスの所有者を適用する方法について説明します。</span><span class="sxs-lookup"><span data-stu-id="a865b-107">The below reference explains what the ID prefix reservation entails, and how an owner can apply for an ID prefix.</span></span>

## <a name="id-prefix-reservation-details"></a><span data-ttu-id="a865b-108">ID プレフィックス予約の詳細</span><span class="sxs-lookup"><span data-stu-id="a865b-108">ID prefix reservation details</span></span>

<span data-ttu-id="a865b-109">ことが起こります。 パッケージ ID プレフィックスを予約する場合、 [nuget.org](https://www.nuget.org/)ギャラリーも Visual Studio のようにします。</span><span class="sxs-lookup"><span data-stu-id="a865b-109">When a package ID prefix is reserved, several things happen on the [nuget.org](https://www.nuget.org/) gallery, as well as in Visual Studio.</span></span> <span data-ttu-id="a865b-110">さらに、プレフィックスのサブセットを複数の所有者に委任する 'public' としてのプレフィックスを設定するなど、ID プレフィックス予約によってサポートされるシナリオ、上級です。</span><span class="sxs-lookup"><span data-stu-id="a865b-110">In addition, there are advanced scenarios that are supported by ID prefix reservations, such as setting a prefix as 'public', delegating prefix subsets to multiple owners.</span></span>

### <a name="id-prefix-reservation-on-nugetorg"></a><span data-ttu-id="a865b-111">Nuget.org で ID プレフィックスの予約</span><span class="sxs-lookup"><span data-stu-id="a865b-111">ID prefix reservation on nuget.org</span></span>

<span data-ttu-id="a865b-112">プレフィックスを予約するときに[nuget.org](https://www.nuget.org/)次が実行されます。</span><span class="sxs-lookup"><span data-stu-id="a865b-112">When a prefix is reserved on [nuget.org](https://www.nuget.org/), the following will happen:</span></span>

1. <span data-ttu-id="a865b-113">プレフィックスの予約が所有者または一連の所有者に関連付けられている[nuget.org](https://www.nuget.org/)します。</span><span class="sxs-lookup"><span data-stu-id="a865b-113">A prefix reservation is associated with an owner or set of owners on [nuget.org](https://www.nuget.org/).</span></span>

1. <span data-ttu-id="a865b-114">パッケージに送信するたびに[nuget.org](https://www.nuget.org/) ID プレフィックス予約されている人の所有者から発生する場合を除き、予約済み ID のプレフィックスに一致する ID を持つパッケージが拒否されました。</span><span class="sxs-lookup"><span data-stu-id="a865b-114">Whenever a package is submitted to [nuget.org](https://www.nuget.org/) with an ID that matches the reserved ID prefix, the package is rejected unless it originates from the owner(s) that reserved the ID prefix.</span></span>

1. <span data-ttu-id="a865b-115">任意のパッケージ ID プレフィックス予約されている人の所有者から予約済み ID のプレフィックスに一致する必要がありますが視覚的および Visual Studio 2017 バージョン 15.4 以降で[nuget.org](https://www.nuget.org/)パッケージがあることを示す予約済み ID のプレフィックス。</span><span class="sxs-lookup"><span data-stu-id="a865b-115">Any package that matches the reserved ID prefix and originates from the owner(s) that reserved the ID prefix will have a visual indicator in Visual Studio 2017 version 15.4 or later, and on [nuget.org](https://www.nuget.org/) indicating that the package is under a reserved ID prefix.</span></span> <span data-ttu-id="a865b-116">これは、所有者の下の既存のパッケージだけでなく、新しいパッケージの送信の場合は true。</span><span class="sxs-lookup"><span data-stu-id="a865b-116">This is true for both new package submissions as well as existing packages under the owner(s).</span></span> <span data-ttu-id="a865b-117">**注:** 単一フィードがパッケージのソースとして選択されている場合にのみ、Visual Studio でのインジケーターが表示されます。</span><span class="sxs-lookup"><span data-stu-id="a865b-117">**Note:** The indicator in Visual Studio appears only if a single feed is selected as the package source.</span></span>

1. <span data-ttu-id="a865b-118">予約済みの ID のプレフィックスに一致するすべての既存のパッケージは*いない*予約済みの所有者によって所有されているプレフィックスは変更されません (、一覧にないことはできませんが、視覚的なインジケーターを持っていないも)。</span><span class="sxs-lookup"><span data-stu-id="a865b-118">All previously existing packages that match the reserved ID prefix, but are *not* owned by the owner of the reserved prefix will remain unchanged (they will not be unlisted, but they will also not have the visual indicator).</span></span> <span data-ttu-id="a865b-119">さらに、これらのパッケージの所有者は、パッケージの新しいバージョンを送信できます。</span><span class="sxs-lookup"><span data-stu-id="a865b-119">In addition, owners of these packages will still be able to submit new versions to the package.</span></span>

<span data-ttu-id="a865b-120">これらの変更は、次の条件に基づいており、いくつかの追加制限します。</span><span class="sxs-lookup"><span data-stu-id="a865b-120">These changes are based on the following conditions and impose several additional restrictions:</span></span>

- <span data-ttu-id="a865b-121">パッケージの 1 つだけの所有者には、(複数所有者とパッケージ) に表示する視覚インジケータの予約済みのプレフィックスが必要です。</span><span class="sxs-lookup"><span data-stu-id="a865b-121">Only one owner of a package needs to have the reserved prefix for the visual indicator to appear (for packages with multiple-owners).</span></span>

- <span data-ttu-id="a865b-122">場所は、予約済みのプレフィックスを 1 つまたは複数の所有者と、1 つまたは複数の所有者には、予約済みのプレフィックスはありません。 パッケージの 1 つ以上の所有者がある場合、予約済みのプレフィックスには所有者だけは予約済みのプレフィックスを持つその他の人の所有者を削除できます。</span><span class="sxs-lookup"><span data-stu-id="a865b-122">If there is more than one owner of a package where one or more owners has the reserved prefix and one or more owners does not have the reserved prefix, then only the owner(s) with the reserved prefix can remove other owner(s) with a reserved prefix.</span></span> <span data-ttu-id="a865b-123">予約済みのプレフィックスを持たない所有者は、予約済みのプレフィックスで所有者を削除できません。</span><span class="sxs-lookup"><span data-stu-id="a865b-123">The owners who do not have the prefix reserved cannot remove owners with the prefix reserved.</span></span> <span data-ttu-id="a865b-124">予約済みのプレフィックスはありませんが、他の所有者を削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="a865b-124">They can still remove other owners that also do not have the prefix reserved.</span></span>

- <span data-ttu-id="a865b-125">パッケージが、視覚的なインジケーターを持つ、*常に*視覚インジケーターがある (予約済みのプレフィックスを持つ少なくとも 1 つその所有者の保証は常に、所有者)</span><span class="sxs-lookup"><span data-stu-id="a865b-125">Once a package has the visual indicator, it should *always* have the visual indicator (guaranteeing that at least one owner with the reserved prefix will always remain an owner)</span></span>

### <a name="advanced-prefix-reservation-scenarios"></a><span data-ttu-id="a865b-126">高度なプレフィックスの予約のシナリオ</span><span class="sxs-lookup"><span data-stu-id="a865b-126">Advanced prefix reservation scenarios</span></span>

<span data-ttu-id="a865b-127">以下に示す subprefix 委任、および public としてマークするプレフィックスを含むいくつかのより高度なプレフィックス予約シナリオがあります。</span><span class="sxs-lookup"><span data-stu-id="a865b-127">There are several more advanced prefix reservation scenarios described below, including subprefix delegation, and marking prefixes as public.</span></span> <span data-ttu-id="a865b-128">可能なより高度なプレフィックスの予約を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a865b-128">Below are the more advanced prefix reservations that can be made.</span></span> 

- <span data-ttu-id="a865b-129">プレフィックスの予約の中に、所有者は、その他の所有者にプレフィックスのサブセットの委任 (またはプリフィックス) を要求できます。</span><span class="sxs-lookup"><span data-stu-id="a865b-129">During prefix reservation, the owner can request delegation of prefix subsets (or the prefix) to other owners.</span></span> <span data-ttu-id="a865b-130">たとえば場合、'[Microsoft](https://www.nuget.org/profiles/microsoft)'を所有する' Microsoft.\*'が'[aspnet](https://www.nuget.org/profiles/aspnet)'席の予約' Microsoft.AspNet\*'、'[Microsoft](https://www.nuget.org/profiles/microsoft)' ことができます。デリゲートを ' Microsoft.AspNet します。\*' に、 [aspnet](https://www.nuget.org/profiles/aspnet)アカウント。</span><span class="sxs-lookup"><span data-stu-id="a865b-130">For example, if '[Microsoft](https://www.nuget.org/profiles/microsoft)' owns 'Microsoft.\*', but '[aspnet](https://www.nuget.org/profiles/aspnet)' wants to reserve 'Microsoft.AspNet.\*', '[Microsoft](https://www.nuget.org/profiles/microsoft)' can choose to delegate 'Microsoft.AspNet.\*' to the [aspnet](https://www.nuget.org/profiles/aspnet) account.</span></span>

- <span data-ttu-id="a865b-131">プレフィックスの予約には、所有者は、プレフィックスを公開して選択できます。</span><span class="sxs-lookup"><span data-stu-id="a865b-131">During prefix reservation, the owner can choose to make a prefix public.</span></span> <span data-ttu-id="a865b-132">これもことができますになりますが予約済みのプレフィックスから、パッケージの発生元を示す視覚インジケータ**いない**任意の所有者のプレフィックスに将来のパッケージの送信をブロックします。</span><span class="sxs-lookup"><span data-stu-id="a865b-132">This will still give them the visual indicator showing that the package originates from a reserved prefix, but it will **not** block future package submissions on the prefix for any owner.</span></span> <span data-ttu-id="a865b-133">これは多くの共同作成者でのオープン ソース プロジェクトに役立ちます - 上部またはコアの共同作成者は、予約されているプレフィックスを持つことができますが、すべてのコントリビューターに開いてでしょう。</span><span class="sxs-lookup"><span data-stu-id="a865b-133">This is useful for open source projects with many contributors - the top or core contributors can have the prefix reserved, but it can still be open to all contributors.</span></span> 

### <a name="prefix-reservation-visual-indicator"></a><span data-ttu-id="a865b-134">プレフィックスの予約の視覚インジケーター</span><span class="sxs-lookup"><span data-stu-id="a865b-134">Prefix reservation visual indicator</span></span>

<span data-ttu-id="a865b-135">パッケージは、予約済みのプレフィックスからは、表示、視覚的なインジケーターの下、 [nuget.org](https://www.nuget.org/)ギャラリーと Visual Studio 2017 バージョン 15.4 以降で。</span><span class="sxs-lookup"><span data-stu-id="a865b-135">When a package comes from a reserved prefix, you see the below visual indicators on the [nuget.org](https://www.nuget.org/) gallery and in Visual Studio 2017 version 15.4 or later:</span></span>

<span data-ttu-id="a865b-136">**nuget.org ギャラリー**
![nuget.org ギャラリー](media/nuget-gallery-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="a865b-136">**nuget.org Gallery**
![nuget.org Gallery](media/nuget-gallery-reserved-prefix.png)</span></span>

<span data-ttu-id="a865b-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span><span class="sxs-lookup"><span data-stu-id="a865b-137">**Visual Studio**
![Visual Studio](media/visual-studio-reserved-prefix.png)</span></span>

## <a name="id-prefix-reservation-application-process"></a><span data-ttu-id="a865b-138">ID プレフィックス予約アプリケーション プロセス</span><span class="sxs-lookup"><span data-stu-id="a865b-138">ID prefix reservation application process</span></span>

1. <span data-ttu-id="a865b-139">同意を確認[プレフィックス ID の予約するための条件](#id-prefix-reservation-criteria)します。</span><span class="sxs-lookup"><span data-stu-id="a865b-139">Review the acceptance [criteria for prefix ID reservation](#id-prefix-reservation-criteria).</span></span>

2. <span data-ttu-id="a865b-140">いずれかだけでなく、予約する名前空間を決定[プレフィックス予約シナリオを高度な](#advanced-prefix-reservation-scenarios)が必要になります。</span><span class="sxs-lookup"><span data-stu-id="a865b-140">Determine the namespaces you want to reserve, in addition to any [advanced prefix reservation scenarios](#advanced-prefix-reservation-scenarios) you may require.</span></span>

3. <span data-ttu-id="a865b-141">メールを送信[ account@nuget.org ](mailto:account@nuget.org)の表示名の所有者と[nuget.org](https://www.nuget.org/)、予約済みのプレフィックスを要求するいるとします。</span><span class="sxs-lookup"><span data-stu-id="a865b-141">Send a mail to [account@nuget.org](mailto:account@nuget.org) with the owner display name on [nuget.org](https://www.nuget.org/), as well as any reserved prefixes you are requesting.</span></span> <span data-ttu-id="a865b-142">プレフィックスのサブセットを複数の所有者に委任する場合は、すべての所有者の表示名を説明し、サブセットのプレフィックスを確認します。</span><span class="sxs-lookup"><span data-stu-id="a865b-142">If you are delegating prefix subsets to multiple owners, make sure you mention all owner display names and prefix subsets.</span></span>

<span data-ttu-id="a865b-143">アプリケーションが送信された後の受理または拒否 (拒否の原因となった条件) で通知されます。</span><span class="sxs-lookup"><span data-stu-id="a865b-143">After the application is submitted, you are notified of acceptance or rejection (with the criteria that caused rejection).</span></span> <span data-ttu-id="a865b-144">所有者の身元を確認する追加の識別に関する質問をしたりすることがあります。</span><span class="sxs-lookup"><span data-stu-id="a865b-144">We may need to ask additional identifying questions to confirm owner identity.</span></span>

### <a name="id-prefix-reservation-criteria"></a><span data-ttu-id="a865b-145">ID プレフィックス予約条件</span><span class="sxs-lookup"><span data-stu-id="a865b-145">ID prefix reservation criteria</span></span>

<span data-ttu-id="a865b-146">ID プレフィックスの予約のすべてのアプリケーションをレビューするとき、 [nuget.org](https://www.nuget.org/)チームに対してアプリケーションを評価する、以下の条件。</span><span class="sxs-lookup"><span data-stu-id="a865b-146">When reviewing any application for ID prefix reservation, the [nuget.org](https://www.nuget.org/) team will evaluate the application against the below criteria.</span></span> <span data-ttu-id="a865b-147">すべての条件が、予約されているプレフィックスが満たされている必要がありますが (で指定された説明) が満たされている条件の大幅な証拠がない場合、アプリケーションが拒否された可能性があります。</span><span class="sxs-lookup"><span data-stu-id="a865b-147">Not all criteria needs to be met for a prefix to be reserved, but the application may be denied if there is not substantial evidence of the criteria being met (with an explanation given):</span></span>

1. <span data-ttu-id="a865b-148">パッケージ ID プレフィックス適切かつ明確に識別、パッケージ所有者にしますか。</span><span class="sxs-lookup"><span data-stu-id="a865b-148">Does the package ID prefix properly and clearly identify the package owner?</span></span>

1. <span data-ttu-id="a865b-149">パッケージ ID プレフィックスの下の所有者によって多数のパッケージが既に送信されているか?</span><span class="sxs-lookup"><span data-stu-id="a865b-149">Are a significant number of the packages that have already been submitted by the owner under the package ID prefix?</span></span>

1. <span data-ttu-id="a865b-150">パッケージ ID プレフィックスをすべての所有者や組織に属する必要がありますしない共通のものですか。</span><span class="sxs-lookup"><span data-stu-id="a865b-150">Is the package ID prefix something common that should not belong to any individual owner or organization?</span></span>

1. <span data-ttu-id="a865b-151">*いない*あいまいさとコミュニティの混乱が発生する、パッケージ ID プレフィックスを予約しますか?</span><span class="sxs-lookup"><span data-stu-id="a865b-151">Would *not* reserving the package ID prefix cause ambiguity and confusion for the community?</span></span>

1. <span data-ttu-id="a865b-152">パッケージ ID プレフィックス明確かつ一貫した (特にパッケージの作成者) に一致するパッケージの識別プロパティか?</span><span class="sxs-lookup"><span data-stu-id="a865b-152">Are the identifying properties of the packages that match the package ID prefix clear and consistent (especially the package author)?</span></span>

## <a name="third-party-feed-provider-scenarios"></a><span data-ttu-id="a865b-153">サード パーティ プロバイダー シナリオのフィード</span><span class="sxs-lookup"><span data-stu-id="a865b-153">Third party feed provider scenarios</span></span>

<span data-ttu-id="a865b-154">フィード プロバイダー サード パーティがプレフィックスの予約を提供する独自のサービスを実装する目的の場合は、NuGet V3 で search サービスのプロバイダーのフィードを変更してを行うことができます。</span><span class="sxs-lookup"><span data-stu-id="a865b-154">If a third party feed provider is interested in implementing their own service to provide prefix reservations, you can do so by modifying the search service in the NuGet V3 feed providers.</span></span> <span data-ttu-id="a865b-155">フィードの検索サービスの追加は、追加する、*検証*V3 フィードは、次の例でのプロパティ。</span><span class="sxs-lookup"><span data-stu-id="a865b-155">The addition in the feed search service is to add the *verified* property, with examples for the V3 feeds below.</span></span> <span data-ttu-id="a865b-156">NuGet クライアントは、フィード、V2 で追加されたプロパティをサポートしていません。</span><span class="sxs-lookup"><span data-stu-id="a865b-156">The NuGet client will not support the added property in the V2 feed.</span></span>

<span data-ttu-id="a865b-157">詳細については、次を参照してください。、 [API の検索サービスに関するドキュメント](../api/search-query-service-resource.md)します。</span><span class="sxs-lookup"><span data-stu-id="a865b-157">For more information, see the [documentation about the API's search service](../api/search-query-service-resource.md).</span></span>

## <a name="package-id-prefix-reservation-dispute-policy"></a><span data-ttu-id="a865b-158">パッケージ ID プレフィックス予約争議ポリシー</span><span class="sxs-lookup"><span data-stu-id="a865b-158">Package ID Prefix Reservation Dispute Policy</span></span>
<span data-ttu-id="a865b-159">所有者と思う場合[NuGet.org](https://www.nuget.org)を上記の一覧表示されている条件に反しますまたはください電子メールの著作権、商標またはを侵害するパッケージ ID プレフィックスの予約が割り当てられた[ support@nuget.org ](mailto:support@nuget.org)問題 ID プレフィックス、ID のプレフィックスと割り当てられているプレフィックスの予約を争議の理由の所有者を使用します。</span><span class="sxs-lookup"><span data-stu-id="a865b-159">If you believe an owner on [NuGet.org](https://www.nuget.org) was assigned a package ID prefix reservation that goes against the above listed criteria, or infringes on any trademarks or copyrights, please email [support@nuget.org](mailto:support@nuget.org) with the ID prefix in question, the owner of the ID prefix, and the reason for disputing the assigned prefix reservation.</span></span>

