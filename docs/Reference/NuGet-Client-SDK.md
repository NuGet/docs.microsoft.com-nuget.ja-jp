---
title: "NuGet v3 クライアントと NuGetGallery Api |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: d1a393b7-51b1-4840-b1a8-fdd76455077d
description: "NuGet および NuGetGallery Api は進化し続けるとまだ文書化された、ですが例としては、Dave Glick のブログでご確認いただけます。"
keywords: "NuGet API で NuGetGallery API NuGet v3 ライブラリ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 43a2e569b64f5e9d6e93cc6c279faf91a6dda9ee
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="6d9cf-104">NuGet クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="6d9cf-104">NuGet Client SDK</span></span>

<span data-ttu-id="6d9cf-105">NuGet v3 クライアントと NuGetGallery Api は、絶えず進化をすぐに文書化される安定した領域を持つに取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="6d9cf-105">The NuGet v3 Client and NuGetGallery APIs are constantly evolving and we are working on having a stable surface area that we can document soon.</span></span>

<span data-ttu-id="6d9cf-106">その間は、Dave Glick によって次のブログ シリーズの例と、API の一部のドキュメントを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="6d9cf-106">In the meantime, you can find examples and documentation for some of the API in the following blog series by Dave Glick:</span></span>

- [<span data-ttu-id="6d9cf-107">NuGet v3 ライブラリ、第 1 部: 概要と概念</span><span class="sxs-lookup"><span data-stu-id="6d9cf-107">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="6d9cf-108">NuGet v3 ライブラリ、パート 2: パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="6d9cf-108">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="6d9cf-109">NuGet v3 ライブラリ、パート 3: パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="6d9cf-109">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="6d9cf-110">次のブログ投稿がすぐに書き込まれた、 **3.4.3**クライアント SDK パッケージがリリースされた NuGet のバージョン。</span><span class="sxs-lookup"><span data-stu-id="6d9cf-110">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="6d9cf-111">パッケージの新しいバージョンが、ブログ記事の情報と互換性ない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="6d9cf-111">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>
