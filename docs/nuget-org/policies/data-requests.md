---
title: ユーザー データ要求
description: ユーザー データのエクスポートと削除を要求することに関する方針
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775721"
---
# <a name="user-data-requests"></a><span data-ttu-id="442f9-103">ユーザー データ要求</span><span class="sxs-lookup"><span data-stu-id="442f9-103">User Data Requests</span></span>

<span data-ttu-id="442f9-104">nuget.org ユーザーは、[nuget.org](https://www.nuget.org) 経由で情報の削除要求とエクスポート要求を送信できます。いずれの要求もサポート要求として送信され、nuget.org 管理者が 30 日以内に実行します。</span><span class="sxs-lookup"><span data-stu-id="442f9-104">nuget.org users can submit information delete requests and information export requests through [nuget.org](https://www.nuget.org). Both types are submitted in the form of support requests and are be executed by the nuget.org administrators within 30 days.</span></span>

<span data-ttu-id="442f9-105">次のユーザー データには nuget.org から直接アクセスできます。</span><span class="sxs-lookup"><span data-stu-id="442f9-105">The following user data is directly accessible through nuget.org:</span></span>

* <span data-ttu-id="442f9-106">メール アドレス、ログイン アカウント、プロファイルの写真、メール通知設定など、アカウント関連のデータ</span><span class="sxs-lookup"><span data-stu-id="442f9-106">Account related data such as email address, login account, profile picture, and email notification settings</span></span>
* <span data-ttu-id="442f9-107">所有している API キー</span><span class="sxs-lookup"><span data-stu-id="442f9-107">Owned API Keys</span></span>
* <span data-ttu-id="442f9-108">所有しているパッケージの一覧</span><span class="sxs-lookup"><span data-stu-id="442f9-108">List of owned packages</span></span>

<span data-ttu-id="442f9-109">このデータは、サポート要求でエクスポートされるデータに含まれません。</span><span class="sxs-lookup"><span data-stu-id="442f9-109">This data is not included in data exported through the support request.</span></span>

## <a name="identifying-customer-data"></a><span data-ttu-id="442f9-110">顧客データを識別する</span><span class="sxs-lookup"><span data-stu-id="442f9-110">Identifying customer data</span></span>

<span data-ttu-id="442f9-111">顧客データは nuget.org ユーザーアカウント名として識別できます。</span><span class="sxs-lookup"><span data-stu-id="442f9-111">Customer data can be identified as nuget.org user account names.</span></span>

## <a name="deleting-customer-data"></a><span data-ttu-id="442f9-112">顧客データを削除する</span><span class="sxs-lookup"><span data-stu-id="442f9-112">Deleting customer data</span></span>

<span data-ttu-id="442f9-113">nuget.org からユーザー データを削除することを要求するには:</span><span class="sxs-lookup"><span data-stu-id="442f9-113">To request deleting user data from nuget.org:</span></span>

1. <span data-ttu-id="442f9-114">ユーザーは [nuget.org](https://www.nuget.org) にサインインする必要があります</span><span class="sxs-lookup"><span data-stu-id="442f9-114">The user must sign-in to [nuget.org](https://www.nuget.org)</span></span>
1. <span data-ttu-id="442f9-115">ユーザーはアカウントの削除要求を提出する必要があります [nuget.org/account/delete](https://www.nuget.org/account/delete)</span><span class="sxs-lookup"><span data-stu-id="442f9-115">The user must submit a request for their account to be deleted [nuget.org/account/delete](https://www.nuget.org/account/delete)</span></span>

<span data-ttu-id="442f9-116">ユーザーがパッケージの唯一の所有者である場合、アカウントの削除を要求する前に新しい所有者を探すことをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="442f9-116">Users that are sole owners of packages are encouraged to find new owners before asking to have their account deleted.</span></span> <span data-ttu-id="442f9-117">パッケージの所有権が譲渡されない場合、その NuGet パッケージは一覧から外れます。結果的に、Visual Studio や nuget.org Web サイトの検索クエリで利用できなくなります。</span><span class="sxs-lookup"><span data-stu-id="442f9-117">If package ownership is not transferred, the NuGet package is unlisted and, as a result, it is no longer available in search queries in Visual Studio or on the nuget.org website.</span></span> <span data-ttu-id="442f9-118">アカウントを削除する前に、nuget.org 管理者はユーザーと協力し、ユーザーが所有しているパッケージの新しい所有者を探します。</span><span class="sxs-lookup"><span data-stu-id="442f9-118">Before deleting the account, the nuget.org administrators work with the user to find new owners for the packages they own.</span></span>

<span data-ttu-id="442f9-119">アカウントの削除アクションは、要求日から 30 日以内に nuget.org 管理者によって完了します。</span><span class="sxs-lookup"><span data-stu-id="442f9-119">The account delete action is completed by the nuget.org administrator within 30 days from the date of the request.</span></span>

<span data-ttu-id="442f9-120">アカウントの削除をもって、すべてのユーザー データが nuget.org システムから削除され、次のアクションが行われます。</span><span class="sxs-lookup"><span data-stu-id="442f9-120">Upon account deletion, all of the user's data is be removed from the nuget.org system and the following actions are taken:</span></span>

* <span data-ttu-id="442f9-121">削除したアカウントが nuget.org で登録解除になる</span><span class="sxs-lookup"><span data-stu-id="442f9-121">The deleted account becomes unregistered with nuget.org</span></span>
* <span data-ttu-id="442f9-122">所有しているすべての API キーが削除される</span><span class="sxs-lookup"><span data-stu-id="442f9-122">All owned API Keys are deleted</span></span>
* <span data-ttu-id="442f9-123">予約されていたすべての名前空間が解放される</span><span class="sxs-lookup"><span data-stu-id="442f9-123">All reserved namespaces are released</span></span>
* <span data-ttu-id="442f9-124">あらゆるパッケージ所有権が削除される</span><span class="sxs-lookup"><span data-stu-id="442f9-124">Any package ownership are removed</span></span>

<span data-ttu-id="442f9-125">所有しているパッケージは削除 *されません*。</span><span class="sxs-lookup"><span data-stu-id="442f9-125">The owned packages are *not* deleted.</span></span> <span data-ttu-id="442f9-126">所有しているパッケージは検索結果の一覧からは外れますが、それに依存しているプロジェクトでは、パッケージの復元で引き続き利用できます。</span><span class="sxs-lookup"><span data-stu-id="442f9-126">Though unlisted from search results, they remain available through package restore to projects that depend on them.</span></span>

## <a name="exporting-customer-data"></a><span data-ttu-id="442f9-127">顧客データをエクスポートする</span><span class="sxs-lookup"><span data-stu-id="442f9-127">Exporting customer data</span></span>

<span data-ttu-id="442f9-128">nuget.org にサインイン後、ユーザーは [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) からエクスポート要求を提出できます。</span><span class="sxs-lookup"><span data-stu-id="442f9-128">After sign-in to nuget.org, a user can submit an export request through [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact)</span></span>

<span data-ttu-id="442f9-129">ユーザーはエクスポートされたデータを Azure BLOB から 48 時間ダウンロードできます。</span><span class="sxs-lookup"><span data-stu-id="442f9-129">The data exported is made available for 48 hours to the user for download through an Azure Blob.</span></span> <span data-ttu-id="442f9-130">48 時間後にアクセスの有効期限が切れます。ユーザーは、必要であれば、新しいエクスポート要求を提出する必要があります。</span><span class="sxs-lookup"><span data-stu-id="442f9-130">After 48 hours, access expires and the user must submit a new export request as needed.</span></span>

<span data-ttu-id="442f9-131">次のデータがエクスポートされます。</span><span class="sxs-lookup"><span data-stu-id="442f9-131">The exported data includes:</span></span>

* <span data-ttu-id="442f9-132">ユーザーのサポート要求</span><span class="sxs-lookup"><span data-stu-id="442f9-132">The user's support requests</span></span>
* <span data-ttu-id="442f9-133">監査ログに残っているユーザーのアクション (パッケージの公開、アカウントの作成)</span><span class="sxs-lookup"><span data-stu-id="442f9-133">The user's actions (publish package, create account) as persisted in the audit logs</span></span>
* <span data-ttu-id="442f9-134">IIS ログに残っているユーザー情報</span><span class="sxs-lookup"><span data-stu-id="442f9-134">Any user information as persisted in the IIS logs</span></span>
