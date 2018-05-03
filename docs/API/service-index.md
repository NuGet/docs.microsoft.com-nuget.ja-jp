---
title: サービス インデックス、NuGet API
description: サービス インデックスは、NuGet HTTP API のエントリ ポイントであり、サーバーの機能を列挙します。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 84e623e8480e4d17edad2ec3b2da6dcb6e53d21b
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="service-index"></a><span data-ttu-id="c2595-103">サービスのインデックス</span><span class="sxs-lookup"><span data-stu-id="c2595-103">Service index</span></span>

<span data-ttu-id="c2595-104">サービス インデックスは、NuGet パッケージのソースのエントリ ポイントであり、パッケージ ソースの機能を検出するクライアントの実装は、ある JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="c2595-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="c2595-105">サービス インデックスは、次の 2 つの必須プロパティを持つ JSON オブジェクト: `version` (サービスのインデックスのスキーマ バージョン) と`resources`(エンドポイントまたはパッケージ ソースの機能)。</span><span class="sxs-lookup"><span data-stu-id="c2595-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="c2595-106">nuget.org のサービスのインデックスにある`https://api.nuget.org/v3/index.json`です。</span><span class="sxs-lookup"><span data-stu-id="c2595-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="c2595-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="c2595-107">Versioning</span></span>

<span data-ttu-id="c2595-108">`version`値は、サービスのインデックスのスキーマ バージョンを示す SemVer 2.0.0 解析可能なバージョン文字列。</span><span class="sxs-lookup"><span data-stu-id="c2595-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="c2595-109">この API でのメジャー バージョン番号をバージョン文字列であることが必須で`3`です。</span><span class="sxs-lookup"><span data-stu-id="c2595-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="c2595-110">サービス インデックス スキーマに重要ではない変更が加えられると、バージョン文字列のマイナー バージョンが増加します。</span><span class="sxs-lookup"><span data-stu-id="c2595-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="c2595-111">サービス インデックス内の各リソースはサービス インデックス スキーマのバージョンから独立してバージョン管理されたです。</span><span class="sxs-lookup"><span data-stu-id="c2595-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="c2595-112">現在のスキーマのバージョンが`3.0.0`です。</span><span class="sxs-lookup"><span data-stu-id="c2595-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="c2595-113">`3.0.0`バージョンは機能的には、古い`3.0.0-beta.1`バージョンが安定で定義されているスキーマをより明確と通信する際に優先する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2595-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="c2595-114">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="c2595-114">HTTP methods</span></span>

<span data-ttu-id="c2595-115">サービス インデックスは、HTTP メソッドを使用してアクセス`GET`と`HEAD`です。</span><span class="sxs-lookup"><span data-stu-id="c2595-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="c2595-116">リソース</span><span class="sxs-lookup"><span data-stu-id="c2595-116">Resources</span></span>

<span data-ttu-id="c2595-117">`resources`プロパティには、このパッケージ ソースでサポートされているリソースの配列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="c2595-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="c2595-118">リソース</span><span class="sxs-lookup"><span data-stu-id="c2595-118">Resource</span></span>

<span data-ttu-id="c2595-119">リソース内のオブジェクトとは、`resources`配列。</span><span class="sxs-lookup"><span data-stu-id="c2595-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="c2595-120">これは、パッケージ ソースのバージョン管理機能を表します。</span><span class="sxs-lookup"><span data-stu-id="c2595-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="c2595-121">リソースには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="c2595-121">A resource has the following properties:</span></span>

<span data-ttu-id="c2595-122">名前</span><span class="sxs-lookup"><span data-stu-id="c2595-122">Name</span></span>          | <span data-ttu-id="c2595-123">種類</span><span class="sxs-lookup"><span data-stu-id="c2595-123">Type</span></span>   | <span data-ttu-id="c2595-124">必須</span><span class="sxs-lookup"><span data-stu-id="c2595-124">Required</span></span> | <span data-ttu-id="c2595-125">メモ</span><span class="sxs-lookup"><span data-stu-id="c2595-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="c2595-126">string</span><span class="sxs-lookup"><span data-stu-id="c2595-126">string</span></span> | <span data-ttu-id="c2595-127">可</span><span class="sxs-lookup"><span data-stu-id="c2595-127">yes</span></span>      | <span data-ttu-id="c2595-128">リソースへの URL</span><span class="sxs-lookup"><span data-stu-id="c2595-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="c2595-129">string</span><span class="sxs-lookup"><span data-stu-id="c2595-129">string</span></span> | <span data-ttu-id="c2595-130">可</span><span class="sxs-lookup"><span data-stu-id="c2595-130">yes</span></span>      | <span data-ttu-id="c2595-131">リソースの種類を表す文字列定数</span><span class="sxs-lookup"><span data-stu-id="c2595-131">A string constant representing the resource type</span></span>
<span data-ttu-id="c2595-132">コメント</span><span class="sxs-lookup"><span data-stu-id="c2595-132">comment</span></span>       | <span data-ttu-id="c2595-133">string</span><span class="sxs-lookup"><span data-stu-id="c2595-133">string</span></span> | <span data-ttu-id="c2595-134">Ｘ</span><span class="sxs-lookup"><span data-stu-id="c2595-134">no</span></span>       | <span data-ttu-id="c2595-135">リソースの人間の判読できる説明</span><span class="sxs-lookup"><span data-stu-id="c2595-135">A human readable description of the resource</span></span>

<span data-ttu-id="c2595-136">`@id`が HTTP または HTTPS スキーマには、URL を絶対にする必要があるあり、かする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c2595-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="c2595-137">`@type`リソースと対話するときに使用する特定のプロトコルを識別するために使用します。</span><span class="sxs-lookup"><span data-stu-id="c2595-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="c2595-138">リソースの種類は不透明な文字列が、一般に、形式があります。</span><span class="sxs-lookup"><span data-stu-id="c2595-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="c2595-139">クライアントはハード コードとして予想される、`@type`を理解し、パッケージ ソースのサービスのインデックスで検索する値。</span><span class="sxs-lookup"><span data-stu-id="c2595-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="c2595-140">正確な`@type`に記載されている個々 のリソースの参照ドキュメントで現在使用している値が列挙された、 [API の概要](overview.md#resources-and-schema)です。</span><span class="sxs-lookup"><span data-stu-id="c2595-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="c2595-141">ここではこのドキュメントでは、さまざまなリソースについてのドキュメントは基本的には別にグループ化、`{RESOURCE_NAME}`シナリオでグループ化に似ているサービスのインデックスに存在します。</span><span class="sxs-lookup"><span data-stu-id="c2595-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="c2595-142">各リソースを一意にする必要がない`@id`または`@type`です。</span><span class="sxs-lookup"><span data-stu-id="c2595-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="c2595-143">他よりも優先するリソースを決定する、クライアントの実装の責任です。</span><span class="sxs-lookup"><span data-stu-id="c2595-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="c2595-144">1 つの可能な実装は同じまたは互換性のあるリソース`@type`障害やサーバーの接続エラーが発生した場合にラウンド ロビン方式で使用できます。</span><span class="sxs-lookup"><span data-stu-id="c2595-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="c2595-145">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="c2595-145">Sample request</span></span>

<span data-ttu-id="c2595-146">取得 https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="c2595-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="c2595-147">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="c2595-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
