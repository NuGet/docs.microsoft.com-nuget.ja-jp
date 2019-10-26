---
title: NuGet クライアント SDK
description: API は進化していますが、まだ文書化されていませんが、例については Dave Glick のブログを参照してください。
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 873bde467a39653b818b49173d53bc983e99d1b9
ms.sourcegitcommit: f9645fc5f49c18978e12a292a3f832e162e069d5
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/25/2019
ms.locfileid: "72924613"
---
# <a name="nuget-client-sdk"></a><span data-ttu-id="bab5a-103">NuGet クライアント SDK</span><span class="sxs-lookup"><span data-stu-id="bab5a-103">NuGet Client SDK</span></span>

<span data-ttu-id="bab5a-104">Nuget*クライアント SDK*は、 [nuget を中心](https://www.nuget.org/packages/NuGet.Packaging)に配置[された](https://www.nuget.org/packages/NuGet.Protocol)nuget パッケージのグループを参照[します](https://www.nuget.org/packages/NuGet.Commands)。</span><span class="sxs-lookup"><span data-stu-id="bab5a-104">The *NuGet Client SDK* refers to a group of NuGet packages centered around [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [NuGet.Packaging](https://www.nuget.org/packages/NuGet.Packaging), and [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol).</span></span> <span data-ttu-id="bab5a-105">これらのパッケージは、以前の[NuGet のコア](https://www.nuget.org/packages/NuGet.Core/)ライブラリに代わるものです。</span><span class="sxs-lookup"><span data-stu-id="bab5a-105">These packages replace the earlier [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) library.</span></span>

> [!Note]
>  <span data-ttu-id="bab5a-106">NuGet サーバープロトコルに関するドキュメントについては、 [Nuget サーバー API](~/api/overview.md)に関するドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="bab5a-106">For documentation on the NuGet server protocol, please refer to the [NuGet Server API](~/api/overview.md).</span></span>

## <a name="source-code"></a><span data-ttu-id="bab5a-107">ソースコード</span><span class="sxs-lookup"><span data-stu-id="bab5a-107">Source code</span></span>

<span data-ttu-id="bab5a-108">ソースコードは、プロジェクト[nuget/nuget. Client](https://github.com/NuGet/NuGet.Client)で GitHub に公開されています。</span><span class="sxs-lookup"><span data-stu-id="bab5a-108">The source code is published on GitHub in the project [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).</span></span>

## <a name="third-party-documentation"></a><span data-ttu-id="bab5a-109">サードパーティのドキュメント</span><span class="sxs-lookup"><span data-stu-id="bab5a-109">Third-party documentation</span></span>

<span data-ttu-id="bab5a-110">API の一部の例とドキュメントは、次のブログシリーズで、発行済み2016を使用して確認できます。</span><span class="sxs-lookup"><span data-stu-id="bab5a-110">You can find examples and documentation for some of the API in the following blog series by Dave Glick, published 2016:</span></span>

- [<span data-ttu-id="bab5a-111">NuGet v3 ライブラリの調査、パート 1: 概要と概念</span><span class="sxs-lookup"><span data-stu-id="bab5a-111">Exploring the NuGet v3 Libraries, Part 1: Introduction and concepts</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [<span data-ttu-id="bab5a-112">NuGet v3 ライブラリの調査、パート 2: パッケージの検索</span><span class="sxs-lookup"><span data-stu-id="bab5a-112">Exploring the NuGet v3 Libraries, Part 2: Searching for packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [<span data-ttu-id="bab5a-113">NuGet v3 ライブラリの調査、パート 3: パッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="bab5a-113">Exploring the NuGet v3 Libraries, Part 3: Installing packages</span></span>](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> <span data-ttu-id="bab5a-114">これらのブログ投稿は、 **3.4.3**バージョンの NUGET クライアント SDK パッケージがリリースされた直後に作成されました。</span><span class="sxs-lookup"><span data-stu-id="bab5a-114">These blog posts were written shortly after the **3.4.3** version of the NuGet client SDK packages were released.</span></span>
> <span data-ttu-id="bab5a-115">新しいバージョンのパッケージは、ブログの投稿の情報と互換性がない可能性があります。</span><span class="sxs-lookup"><span data-stu-id="bab5a-115">Newer versions of the packages may be incompatible with the information in the blog posts.</span></span>

<span data-ttu-id="bab5a-116">Martin Björkström は、次のように、nuget パッケージをインストールするための NuGet クライアント SDK の使用に関する別のアプローチを導入した、彼のブログシリーズを作成しました。</span><span class="sxs-lookup"><span data-stu-id="bab5a-116">Martin Björkström did a follow-up blog post to Dave Glick's blog series where he introduces a different approach on using the NuGet Client SDK for installing NuGet packages:</span></span>

- [<span data-ttu-id="bab5a-117">NuGet v3 ライブラリの再度</span><span class="sxs-lookup"><span data-stu-id="bab5a-117">Revisiting the NuGet v3 Libraries</span></span>](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
