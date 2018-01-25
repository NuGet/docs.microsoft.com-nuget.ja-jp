---
title: "NuGet v3 クライアントと NuGetGallery Api |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "NuGet および NuGetGallery Api は進化し続けるとまだ文書化された、ですが例としては、Dave Glick のブログでご確認いただけます。"
keywords: NuGet API, NuGetGallery API, NuGet v3 libraries
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3eeb4d4df06c235e3b6af50859899c12db3f8f18
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="15c9f-104">NuGet Client SDK</span><span class="sxs-lookup"><span data-stu-id="15c9f-104">NuGet Client SDK</span></span>

<span data-ttu-id="15c9f-105">NuGet v3 クライアントと NuGetGallery Api は、絶えず進化をすぐに文書化される安定した領域を持つに取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="15c9f-105">The NuGet v3 Client and NuGetGallery APIs are constantly evolving and we are working on having a stable surface area that we can document soon.</span></span>

<span data-ttu-id="15c9f-106">その間は、Dave Glick によって次のブログ シリーズの例と、API の一部のドキュメントを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="15c9f-106">In the meantime, you can find examples and documentation for some of the API in the following blog series by Dave Glick:</span></span>

- [<span data-ttu-id="15c9f-107">NuGet v3 ライブラリ、第 1 部: 概要と概念</span><span class="sxs-lookup"><span data-stu-id="15c9f-107">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="15c9f-108">NuGet v3 ライブラリ、パート 2: パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="15c9f-108">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="15c9f-109">NuGet v3 ライブラリ、パート 3: パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="15c9f-109">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="15c9f-110">次のブログ投稿がすぐに書き込まれた、 **3.4.3**クライアント SDK パッケージがリリースされた NuGet のバージョン。</span><span class="sxs-lookup"><span data-stu-id="15c9f-110">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="15c9f-111">パッケージの新しいバージョンが、ブログ記事の情報と互換性ない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="15c9f-111">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>
