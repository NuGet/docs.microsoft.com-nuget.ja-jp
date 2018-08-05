---
title: NuGet クライアント SDK
description: API は進化し、まだ文書化されたが例としては、Dave Glick のブログでご確認いただけます。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: f814b0c0e7fac719e4221a8d8e945de703348aba
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508063"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="fac4f-103">NuGet クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="fac4f-103">NuGet Client SDK</span></span>

> [!Note]
> <span data-ttu-id="fac4f-104">混同しないように、 [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span><span class="sxs-lookup"><span data-stu-id="fac4f-104">Not to be confused with the [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)</span></span>

<span data-ttu-id="fac4f-105">*NuGet クライアント SDK*を中心とした .NET ライブラリのグループを指す[NuGet.Client](https://www.nuget.org/packages/NuGet.Client)、 [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging)、および[NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span><span class="sxs-lookup"><span data-stu-id="fac4f-105">The *NuGet Client SDK* refers to a group of .NET libraries centered around [NuGet.Client](https://www.nuget.org/packages/NuGet.Client), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="fac4f-106">これらのパッケージが、以前に置き換える[NuGet.Core](https://www.nuget.org/packages/NuGet.Core/)ライブラリ。</span><span class="sxs-lookup"><span data-stu-id="fac4f-106">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

<span data-ttu-id="fac4f-107">すぐに文書化される安定した領域があることに取り組んでいます。</span><span class="sxs-lookup"><span data-stu-id="fac4f-107">We are working on having a stable surface area that we can document soon.</span></span>

## <a name="source-code"></a><span data-ttu-id="fac4f-108">ソース コード</span><span class="sxs-lookup"><span data-stu-id="fac4f-108">Source code</span></span>

<span data-ttu-id="fac4f-109">プロジェクトのソース コードが GitHub で公開されて[NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client)します。</span><span class="sxs-lookup"><span data-stu-id="fac4f-109">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="fac4f-110">サード パーティのドキュメント</span><span class="sxs-lookup"><span data-stu-id="fac4f-110">Third-party documentation</span></span>

<span data-ttu-id="fac4f-111">Dave Glick、2016 を発行して、次のブログ シリーズでは、例、および API の一部のドキュメントを見つけることができます。</span><span class="sxs-lookup"><span data-stu-id="fac4f-111">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="fac4f-112">NuGet v3 ライブラリ、第 1 部: 概要と概念</span><span class="sxs-lookup"><span data-stu-id="fac4f-112">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="fac4f-113">NuGet v3 ライブラリ、パート 2: パッケージを検索</span><span class="sxs-lookup"><span data-stu-id="fac4f-113">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="fac4f-114">NuGet v3 ライブラリ、パート 3: パッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="fac4f-114">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="fac4f-115">次のブログ投稿は、直後に記述された、 **3.4.3**クライアント SDK パッケージがリリースされた NuGet のバージョン。</span><span class="sxs-lookup"><span data-stu-id="fac4f-115">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="fac4f-116">新しいバージョンのパッケージは、ブログの投稿の情報と互換性のあることがあります。</span><span class="sxs-lookup"><span data-stu-id="fac4f-116">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>
