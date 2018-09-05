---
title: NuGet API、サービスのインデックス
description: サービス インデックスは、NuGet HTTP API のエントリ ポイントであり、サーバーの機能を列挙します。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 478b74f98caafdc7c6b69423b9f9d72890c8d7cb
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545258"
---
# <a name="service-index"></a><span data-ttu-id="1f6ab-103">サービス インデックス</span><span class="sxs-lookup"><span data-stu-id="1f6ab-103">Service index</span></span>

<span data-ttu-id="1f6ab-104">サービスのインデックスは、NuGet パッケージのソースのエントリ ポイントは、パッケージ ソースの機能を確認するクライアント実装できるようにする JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="1f6ab-105">サービスのインデックスは、2 つの必要なプロパティを持つ JSON オブジェクト: `version` (サービス インデックスのスキーマのバージョン) と`resources`(エンドポイントまたはパッケージ ソースの機能)。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="1f6ab-106">nuget.org のサービスのインデックス位置にある`https://api.nuget.org/v3/index.json`します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="1f6ab-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="1f6ab-107">Versioning</span></span>

<span data-ttu-id="1f6ab-108">`version`値は、サービスのインデックスのスキーマ バージョンを示す SemVer 2.0.0 解析可能なバージョン文字列。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="1f6ab-109">API のバージョン文字列でのメジャー バージョン番号を持つことが定められて`3`します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="1f6ab-110">サービス インデックス スキーマには、互換性に影響しない変更が行われるため、バージョン文字列のマイナー バージョンが高くなります。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="1f6ab-111">サービス インデックス内の各リソースはサービス インデックス スキーマのバージョンとは独立してバージョン管理します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="1f6ab-112">現在のスキーマ バージョンは`3.0.0`します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="1f6ab-113">`3.0.0`バージョンは機能的には、古い`3.0.0-beta.1`バージョンが安定した、定義されたスキーマをより明確と通信する際に優先する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="1f6ab-114">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="1f6ab-114">HTTP methods</span></span>

<span data-ttu-id="1f6ab-115">サービスのインデックスは、HTTP メソッドを使用してアクセスできる`GET`と`HEAD`します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="1f6ab-116">リソース</span><span class="sxs-lookup"><span data-stu-id="1f6ab-116">Resources</span></span>

<span data-ttu-id="1f6ab-117">`resources`プロパティには、このパッケージ ソースでサポートされているリソースの配列が含まれます。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="1f6ab-118">リソース</span><span class="sxs-lookup"><span data-stu-id="1f6ab-118">Resource</span></span>

<span data-ttu-id="1f6ab-119">リソース内のオブジェクトとは、`resources`配列。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="1f6ab-120">パッケージ ソースのバージョン管理機能を表します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="1f6ab-121">リソースには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-121">A resource has the following properties:</span></span>

<span data-ttu-id="1f6ab-122">名前</span><span class="sxs-lookup"><span data-stu-id="1f6ab-122">Name</span></span>          | <span data-ttu-id="1f6ab-123">種類</span><span class="sxs-lookup"><span data-stu-id="1f6ab-123">Type</span></span>   | <span data-ttu-id="1f6ab-124">必須</span><span class="sxs-lookup"><span data-stu-id="1f6ab-124">Required</span></span> | <span data-ttu-id="1f6ab-125">メモ</span><span class="sxs-lookup"><span data-stu-id="1f6ab-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="1f6ab-126">string</span><span class="sxs-lookup"><span data-stu-id="1f6ab-126">string</span></span> | <span data-ttu-id="1f6ab-127">可</span><span class="sxs-lookup"><span data-stu-id="1f6ab-127">yes</span></span>      | <span data-ttu-id="1f6ab-128">リソースへの URL</span><span class="sxs-lookup"><span data-stu-id="1f6ab-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="1f6ab-129">string</span><span class="sxs-lookup"><span data-stu-id="1f6ab-129">string</span></span> | <span data-ttu-id="1f6ab-130">可</span><span class="sxs-lookup"><span data-stu-id="1f6ab-130">yes</span></span>      | <span data-ttu-id="1f6ab-131">リソースの種類を表す文字列定数</span><span class="sxs-lookup"><span data-stu-id="1f6ab-131">A string constant representing the resource type</span></span>
<span data-ttu-id="1f6ab-132">コメント</span><span class="sxs-lookup"><span data-stu-id="1f6ab-132">comment</span></span>       | <span data-ttu-id="1f6ab-133">string</span><span class="sxs-lookup"><span data-stu-id="1f6ab-133">string</span></span> | <span data-ttu-id="1f6ab-134">Ｘ</span><span class="sxs-lookup"><span data-stu-id="1f6ab-134">no</span></span>       | <span data-ttu-id="1f6ab-135">リソースの人間の判読できる説明</span><span class="sxs-lookup"><span data-stu-id="1f6ab-135">A human readable description of the resource</span></span>

<span data-ttu-id="1f6ab-136">`@id`は URL を絶対である必要があるあり、いずれかをする必要がありますが、HTTP または HTTPS スキーマです。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="1f6ab-137">`@type`リソースと対話するときに使用する特定のプロトコルを識別するために使用します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="1f6ab-138">リソースの種類は不透明な文字列が、一般に、形式があります。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-138">The type of the resource is an opaque string but generally has the format:</span></span>

    {RESOURCE_NAME}/{RESOURCE_VERSION}

<span data-ttu-id="1f6ab-139">クライアントがハード コードする必要があります、`@type`を理解し、パッケージ ソースのサービス インデックスで検索する値。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="1f6ab-140">正確な`@type`で記載されている個々 のリソースの参照をドキュメントに現在使用中の値が列挙されます、 [API の概要](overview.md#resources-and-schema)します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="1f6ab-141">ため、このドキュメントでは、さまざまなリソースに関するドキュメントは基本的には別にグループ化、`{RESOURCE_NAME}`シナリオでグループ化に似ているサービス インデックス内に存在します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="1f6ab-142">各リソースを一意にする必要はありません`@id`または`@type`します。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="1f6ab-143">他より優先するリソースを識別するクライアント実装の責任です。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="1f6ab-144">1 つの考えられる実装されるリソースと同じ、または互換性の`@type`接続障害やサーバー エラーが発生した場合、ラウンド ロビン方式で使用できます。</span><span class="sxs-lookup"><span data-stu-id="1f6ab-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="1f6ab-145">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="1f6ab-145">Sample request</span></span>

<span data-ttu-id="1f6ab-146">取得 https://api.nuget.org/v3/index.json</span><span class="sxs-lookup"><span data-stu-id="1f6ab-146">GET https://api.nuget.org/v3/index.json</span></span>

### <a name="sample-response"></a><span data-ttu-id="1f6ab-147">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="1f6ab-147">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
