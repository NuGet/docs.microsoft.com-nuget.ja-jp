---
title: NuGet パッケージ名の争いを解決する
description: ブランド、商標、その他の競合状況に関連する、NuGet パッケージ発行元間の争いを解決するためのプロセス。
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: a2f1fed578f1635296892ab925219f0f27883c02
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426937"
---
# <a name="resolving-disputes-over-nuget-package-names"></a><span data-ttu-id="589dd-103">NuGet パッケージ名に関する争いを解決する</span><span class="sxs-lookup"><span data-stu-id="589dd-103">Resolving disputes over NuGet package names</span></span>

<span data-ttu-id="589dd-104">この記事では、他の NuGet 発行元との争いの解決を求めるコミュニティ メンバーに推奨される解決プロセスについて説明します。</span><span class="sxs-lookup"><span data-stu-id="589dd-104">This article provides a recommended resolution process for community members to resolve disputes with other NuGet publishers.</span></span>

<span data-ttu-id="589dd-105">たとえば、Northwind Traders がその Web サイトからダウンロードできる MSI としてドライバーをクライアントに提供する CRM システムを作るとします。</span><span class="sxs-lookup"><span data-stu-id="589dd-105">For example, suppose that Northwind Traders makes a CRM system for which they provide client drivers as a downloadable MSI from their website.</span></span> <span data-ttu-id="589dd-106">個人開発者の Nancy は Northwind のクライアント ライブラリを使いやすくしたいため、`NorthwindTraders.Client` という名前の NuGet パッケージに変えます。</span><span class="sxs-lookup"><span data-stu-id="589dd-106">Nancy, an independent developer, wants to make it easier to use Northwind's client library, and turns it into a NuGet package called `NorthwindTraders.Client`.</span></span> <span data-ttu-id="589dd-107">その後、Northwind はそのクライアント ライブラリに独自の公式 NuGet パッケージを作りたくなり、パッケージ名に対する Nancy の所有権と争いになります。</span><span class="sxs-lookup"><span data-stu-id="589dd-107">Later, Northwind wants to produce an official NuGet package of their own for their client library, and would thus like to dispute Nancy's ownership of the package name.</span></span>

<span data-ttu-id="589dd-108">このシナリオでは、Nancy には悪意がないように見え、それどころか、自分の時間を使ってコードを作り、Northwind のツールや顧客をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="589dd-108">In this scenario, Nancy does not appear to be acting with bad intentions, but is rather supporting Northwind's tools and customers by contributing her own time and code.</span></span> <span data-ttu-id="589dd-109">とは言え、Northwind 名の正当な所有者は Northwind です。</span><span class="sxs-lookup"><span data-stu-id="589dd-109">At the same time, Northwind is the legitimate owner of the Northwind name.</span></span>

<span data-ttu-id="589dd-110">以下のプロセスに従うことで、Northwind と Nancy はしかるべき解決に向かい協力し合うことができます。いずれの当事者も開発者コミュニティに貢献することが目的であるからです。</span><span class="sxs-lookup"><span data-stu-id="589dd-110">By following the process below, Northwind and Nancy can work together to a suitable resolution, because both are interested in serving the developer community.</span></span> <span data-ttu-id="589dd-111">一般的に、NuGet チームが関与する必要はありません。通常、当事者同士、互いの協力があれば問題なく解決します。</span><span class="sxs-lookup"><span data-stu-id="589dd-111">It's typically not necessary for the NuGet team to become involved; collaboration usually works out best.</span></span> <span data-ttu-id="589dd-112">事実、NuGet チームがこれまで注目したどの争いにおいても、チームが判断することなく解決しています。</span><span class="sxs-lookup"><span data-stu-id="589dd-112">In fact, every dispute brought to the NuGet team's attention to date has been worked out without the team needing to pass judgment.</span></span>

## <a name="process"></a><span data-ttu-id="589dd-113">Process</span><span class="sxs-lookup"><span data-stu-id="589dd-113">Process</span></span>

1. <span data-ttu-id="589dd-114">パッケージ詳細ページの **[所有者に連絡]** リンクを使用し、争いの相手であるパッケージの所有者に連絡します。</span><span class="sxs-lookup"><span data-stu-id="589dd-114">Contact the owners of the package you have the dispute with using the **Contact Owners** link on the package details page.</span></span> <span data-ttu-id="589dd-115">丁寧かつ明確に問題を説明します。</span><span class="sxs-lookup"><span data-stu-id="589dd-115">Explain your issue in a kind and direct manner.</span></span>
2. <span data-ttu-id="589dd-116">[support@nuget.org](mailto:support@nuget.org) にメッセージのコピーを送信し、NuGet と .NET Foundation に争いについて知らせます。</span><span class="sxs-lookup"><span data-stu-id="589dd-116">Send a copy of your message to [support@nuget.org](mailto:support@nuget.org) so that NuGet and the .NET Foundation are aware of your dispute.</span></span>
3. <span data-ttu-id="589dd-117">解決まで最大 30 日待ちます。それが過ぎたら、[support@nuget.org](mailto:support@nuget.org) に再度通知します。</span><span class="sxs-lookup"><span data-stu-id="589dd-117">Wait a maximum of 30 days for a resolution, then notify [support@nuget.org](mailto:support@nuget.org) again.</span></span> <span data-ttu-id="589dd-118">nuget.org サポート チームが関与し、両当事者と共に解決に努めます。</span><span class="sxs-lookup"><span data-stu-id="589dd-118">The nuget.org support team will get involved and try to work through the dispute with both parties.</span></span>
