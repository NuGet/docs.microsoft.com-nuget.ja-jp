---
title: "サービス インデックスでは、NuGet API |Microsoft ドキュメント"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "サービス インデックスは、NuGet HTTP API のエントリ ポイントであり、サーバーの機能を列挙します。"
keywords: "NuGet API エントリ ポイント、NuGetA PI エンドポイントの検出"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 8de0bc15edc358d091d84da54b8b67c085f29645
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="service-index"></a><span data-ttu-id="3400a-104">サービスのインデックス</span><span class="sxs-lookup"><span data-stu-id="3400a-104">Service index</span></span>

<span data-ttu-id="3400a-105">サービス インデックスは、NuGet パッケージのソースのエントリ ポイントであり、パッケージ ソースの機能を検出するクライアントの実装は、ある JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="3400a-105">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="3400a-106">サービス インデックスは、次の 2 つの必須プロパティを持つ JSON オブジェクト: `version` (サービスのインデックスのスキーマ バージョン) と`resources`(エンドポイントまたはパッケージ ソースの機能)。</span><span class="sxs-lookup"><span data-stu-id="3400a-106">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="3400a-107">nuget.org のサービスのインデックスにある`https://api.nuget.org/v3/index.json`です。</span><span class="sxs-lookup"><span data-stu-id="3400a-107">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="3400a-108">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="3400a-108">Versioning</span></span>

<span data-ttu-id="3400a-109">`version`値は、サービスのインデックスのスキーマ バージョンを示す SemVer 2.0.0 解析可能なバージョン文字列。</span><span class="sxs-lookup"><span data-stu-id="3400a-109">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="3400a-110">この API でのメジャー バージョン番号をバージョン文字列であることが必須で`3`です。</span><span class="sxs-lookup"><span data-stu-id="3400a-110">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="3400a-111">サービス インデックス スキーマに重要ではない変更が加えられると、バージョン文字列のマイナー バージョンが増加します。</span><span class="sxs-lookup"><span data-stu-id="3400a-111">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="3400a-112">サービス インデックス内の各リソースはサービス インデックス スキーマのバージョンから独立してバージョン管理されたです。</span><span class="sxs-lookup"><span data-stu-id="3400a-112">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="3400a-113">現在のスキーマのバージョンが`3.0.0`です。</span><span class="sxs-lookup"><span data-stu-id="3400a-113">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="3400a-114">`3.0.0`バージョンは機能的には、古い`3.0.0-beta.1`バージョンが安定で定義されているスキーマをより明確と通信する際に優先する必要があります。</span><span class="sxs-lookup"><span data-stu-id="3400a-114">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="3400a-115">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="3400a-115">HTTP methods</span></span>

<span data-ttu-id="3400a-116">サービス インデックスは、HTTP メソッドを使用してアクセス`GET`と`HEAD`です。</span><span class="sxs-lookup"><span data-stu-id="3400a-116">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="3400a-117">リソース</span><span class="sxs-lookup"><span data-stu-id="3400a-117">Resources</span></span>

<span data-ttu-id="3400a-118">`resources`プロパティには、このパッケージ ソースでサポートされているリソースの配列が含まれています。</span><span class="sxs-lookup"><span data-stu-id="3400a-118">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="3400a-119">リソース</span><span class="sxs-lookup"><span data-stu-id="3400a-119">Resource</span></span>

<span data-ttu-id="3400a-120">リソース内のオブジェクトとは、`resources`配列。</span><span class="sxs-lookup"><span data-stu-id="3400a-120">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="3400a-121">これは、パッケージ ソースのバージョン管理機能を表します。</span><span class="sxs-lookup"><span data-stu-id="3400a-121">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="3400a-122">リソースには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="3400a-122">A resource has the following properties:</span></span>

<span data-ttu-id="3400a-123">name</span><span class="sxs-lookup"><span data-stu-id="3400a-123">Name</span></span>          | <span data-ttu-id="3400a-124">種類</span><span class="sxs-lookup"><span data-stu-id="3400a-124">Type</span></span>   | <span data-ttu-id="3400a-125">必須</span><span class="sxs-lookup"><span data-stu-id="3400a-125">Required</span></span> | <span data-ttu-id="3400a-126">メモ</span><span class="sxs-lookup"><span data-stu-id="3400a-126">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="3400a-127">string</span><span class="sxs-lookup"><span data-stu-id="3400a-127">string</span></span> | <span data-ttu-id="3400a-128">可</span><span class="sxs-lookup"><span data-stu-id="3400a-128">yes</span></span>      | <span data-ttu-id="3400a-129">リソースへの URL</span><span class="sxs-lookup"><span data-stu-id="3400a-129">The URL to the resource</span></span>
@type         | <span data-ttu-id="3400a-130">string</span><span class="sxs-lookup"><span data-stu-id="3400a-130">string</span></span> | <span data-ttu-id="3400a-131">可</span><span class="sxs-lookup"><span data-stu-id="3400a-131">yes</span></span>      | <span data-ttu-id="3400a-132">リソースの種類を表す文字列定数</span><span class="sxs-lookup"><span data-stu-id="3400a-132">A string constant representing the resource type</span></span>
<span data-ttu-id="3400a-133">コメント</span><span class="sxs-lookup"><span data-stu-id="3400a-133">comment</span></span>       | <span data-ttu-id="3400a-134">string</span><span class="sxs-lookup"><span data-stu-id="3400a-134">string</span></span> | <span data-ttu-id="3400a-135">Ｘ</span><span class="sxs-lookup"><span data-stu-id="3400a-135">no</span></span>       | <span data-ttu-id="3400a-136">リソースの人間の判読できる説明</span><span class="sxs-lookup"><span data-stu-id="3400a-136">A human readable description of the resource</span></span>

<span data-ttu-id="3400a-137">`@id`が HTTP または HTTPS スキーマには、URL を絶対にする必要があるあり、かする必要があります。</span><span class="sxs-lookup"><span data-stu-id="3400a-137">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="3400a-138">`@type`リソースと対話するときに使用する特定のプロトコルを識別するために使用します。</span><span class="sxs-lookup"><span data-stu-id="3400a-138">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="3400a-139">リソースの種類は不透明な文字列が、一般に、形式があります。</span><span class="sxs-lookup"><span data-stu-id="3400a-139">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="3400a-140">クライアントはハード コードとして予想される、`@type`を理解し、パッケージ ソースのサービスのインデックスで検索する値。</span><span class="sxs-lookup"><span data-stu-id="3400a-140">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="3400a-141">正確な`@type`に記載されている個々 のリソースの参照ドキュメントで現在使用している値が列挙された、 [API の概要](overview.md#resources-and-schema)です。</span><span class="sxs-lookup"><span data-stu-id="3400a-141">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="3400a-142">ここではこのドキュメントでは、さまざまなリソースについてのドキュメントは基本的には別にグループ化、`{RESOURCE_NAME}`シナリオでグループ化に似ているサービスのインデックスに存在します。</span><span class="sxs-lookup"><span data-stu-id="3400a-142">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="3400a-143">各リソースを一意にする必要がない`@id`または`@type`です。</span><span class="sxs-lookup"><span data-stu-id="3400a-143">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="3400a-144">他よりも優先するリソースを決定する、クライアントの実装の責任です。</span><span class="sxs-lookup"><span data-stu-id="3400a-144">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="3400a-145">1 つの可能な実装は同じまたは互換性のあるリソース`@type`障害やサーバーの接続エラーが発生した場合にラウンド ロビン方式で使用できます。</span><span class="sxs-lookup"><span data-stu-id="3400a-145">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="3400a-146">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="3400a-146">Sample request</span></span>

<span data-ttu-id="3400a-147">GET https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="3400a-147">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="3400a-148">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="3400a-148">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
