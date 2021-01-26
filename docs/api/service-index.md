---
title: サービスインデックス, NuGet API
description: サービスインデックスは、NuGet HTTP API のエントリポイントであり、サーバーの機能を列挙します。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775353"
---
# <a name="service-index"></a><span data-ttu-id="e34a1-103">サービス インデックス</span><span class="sxs-lookup"><span data-stu-id="e34a1-103">Service index</span></span>

<span data-ttu-id="e34a1-104">サービスインデックスは、NuGet パッケージソースのエントリポイントである JSON ドキュメントであり、クライアント実装でパッケージソースの機能を検出できます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-104">The service index is a JSON document that is the entry point for a NuGet package source and allows a client implementation to discover the package source's capabilities.</span></span> <span data-ttu-id="e34a1-105">サービスインデックスは、2つの必須プロパティ `version` (サービスインデックスのスキーマバージョン) と `resources`  (パッケージソースのエンドポイントまたは機能) を持つ JSON オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="e34a1-105">The service index is a JSON object with two required properties: `version` (the schema version of the service index) and `resources`  (the endpoints or capabilities of the package source).</span></span>

<span data-ttu-id="e34a1-106">nuget. 組織のサービスインデックスはにあり `https://api.nuget.org/v3/index.json` ます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-106">nuget.org's service index is located at `https://api.nuget.org/v3/index.json`.</span></span>

## <a name="versioning"></a><span data-ttu-id="e34a1-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="e34a1-107">Versioning</span></span>

<span data-ttu-id="e34a1-108">`version`値は、サービスインデックスのスキーマバージョンを示す SemVer 2.0.0 解析バージョン文字列です。</span><span class="sxs-lookup"><span data-stu-id="e34a1-108">The `version` value is a SemVer 2.0.0 parseable version string which indicates the schema version of the service index.</span></span> <span data-ttu-id="e34a1-109">API は、バージョン文字列のメジャーバージョン番号がであることを指定し `3` ます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-109">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="e34a1-110">サービスインデックススキーマに重大でない変更が加えられると、バージョン文字列のマイナーバージョンが増加します。</span><span class="sxs-lookup"><span data-stu-id="e34a1-110">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="e34a1-111">サービスインデックスの各リソースは、サービスインデックスのスキーマバージョンとは別にバージョン管理されます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-111">Each resource in the service index is versioned independently from the service index schema version.</span></span>

<span data-ttu-id="e34a1-112">現在のスキーマのバージョンは `3.0.0` です。</span><span class="sxs-lookup"><span data-stu-id="e34a1-112">The current schema version is `3.0.0`.</span></span> <span data-ttu-id="e34a1-113">バージョンは、 `3.0.0` 以前のバージョンと機能的に同等です `3.0.0-beta.1` が、安定した定義済みのスキーマをより明確に伝えるため、推奨されます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-113">The `3.0.0` version is functionally equivalent to the older `3.0.0-beta.1` version but should be preferred as it more clearly communicates the stable, defined schema.</span></span>

## <a name="http-methods"></a><span data-ttu-id="e34a1-114">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="e34a1-114">HTTP methods</span></span>

<span data-ttu-id="e34a1-115">サービスインデックスには、HTTP メソッドおよびを使用してアクセスでき `GET` `HEAD` ます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-115">The service index is accessible using HTTP methods `GET` and `HEAD`.</span></span>

## <a name="resources"></a><span data-ttu-id="e34a1-116">リソース</span><span class="sxs-lookup"><span data-stu-id="e34a1-116">Resources</span></span>

<span data-ttu-id="e34a1-117">プロパティは、 `resources` このパッケージソースによってサポートされるリソースの配列を格納します。</span><span class="sxs-lookup"><span data-stu-id="e34a1-117">The `resources` property contains an array of resources supported by this package source.</span></span>

### <a name="resource"></a><span data-ttu-id="e34a1-118">リソース</span><span class="sxs-lookup"><span data-stu-id="e34a1-118">Resource</span></span>

<span data-ttu-id="e34a1-119">リソースは、配列内のオブジェクトです `resources` 。</span><span class="sxs-lookup"><span data-stu-id="e34a1-119">A resource is an object in the `resources` array.</span></span> <span data-ttu-id="e34a1-120">これは、パッケージソースのバージョン管理された機能を表します。</span><span class="sxs-lookup"><span data-stu-id="e34a1-120">It represents a versioned capability of a package source.</span></span> <span data-ttu-id="e34a1-121">リソースには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="e34a1-121">A resource has the following properties:</span></span>

<span data-ttu-id="e34a1-122">名前</span><span class="sxs-lookup"><span data-stu-id="e34a1-122">Name</span></span>          | <span data-ttu-id="e34a1-123">Type</span><span class="sxs-lookup"><span data-stu-id="e34a1-123">Type</span></span>   | <span data-ttu-id="e34a1-124">必須</span><span class="sxs-lookup"><span data-stu-id="e34a1-124">Required</span></span> | <span data-ttu-id="e34a1-125">Notes</span><span class="sxs-lookup"><span data-stu-id="e34a1-125">Notes</span></span>
------------- | ------ | -------- | -----
@id           | <span data-ttu-id="e34a1-126">string</span><span class="sxs-lookup"><span data-stu-id="e34a1-126">string</span></span> | <span data-ttu-id="e34a1-127">はい</span><span class="sxs-lookup"><span data-stu-id="e34a1-127">yes</span></span>      | <span data-ttu-id="e34a1-128">リソースへの URL</span><span class="sxs-lookup"><span data-stu-id="e34a1-128">The URL to the resource</span></span>
@type         | <span data-ttu-id="e34a1-129">string</span><span class="sxs-lookup"><span data-stu-id="e34a1-129">string</span></span> | <span data-ttu-id="e34a1-130">はい</span><span class="sxs-lookup"><span data-stu-id="e34a1-130">yes</span></span>      | <span data-ttu-id="e34a1-131">リソースの種類を表す文字列定数。</span><span class="sxs-lookup"><span data-stu-id="e34a1-131">A string constant representing the resource type</span></span>
<span data-ttu-id="e34a1-132">コメント</span><span class="sxs-lookup"><span data-stu-id="e34a1-132">comment</span></span>       | <span data-ttu-id="e34a1-133">string</span><span class="sxs-lookup"><span data-stu-id="e34a1-133">string</span></span> | <span data-ttu-id="e34a1-134">no</span><span class="sxs-lookup"><span data-stu-id="e34a1-134">no</span></span>       | <span data-ttu-id="e34a1-135">人間が判読できるリソースの説明</span><span class="sxs-lookup"><span data-stu-id="e34a1-135">A human readable description of the resource</span></span>

<span data-ttu-id="e34a1-136">は絶対 URI である必要があり、 `@id` HTTP または HTTPS のいずれかのスキーマを持つ必要があります。</span><span class="sxs-lookup"><span data-stu-id="e34a1-136">The `@id` is a URL that must be absolute and must either have the HTTP or HTTPS schema.</span></span>

<span data-ttu-id="e34a1-137">は、 `@type` リソースと対話するときに使用する特定のプロトコルを識別するために使用されます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-137">The `@type` is used to identify the specific protocol to use when interacting with resource.</span></span> <span data-ttu-id="e34a1-138">リソースの型は不透明な文字列ですが、一般的には次の形式です。</span><span class="sxs-lookup"><span data-stu-id="e34a1-138">The type of the resource is an opaque string but generally has the format:</span></span>

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

<span data-ttu-id="e34a1-139">クライアントは、 `@type` 認識している値をハードコーディングし、パッケージソースのサービスインデックスで検索します。</span><span class="sxs-lookup"><span data-stu-id="e34a1-139">Clients are expected to hard code the `@type` values that they understand and look them up in a package source's service index.</span></span> <span data-ttu-id="e34a1-140">`@type`現在使用中の正確な値は、 [API の概要](overview.md#resources-and-schema)に記載されている個々のリソース参照ドキュメントで列挙されます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-140">The exact `@type` values in use today are enumerated on the individual resource reference documents listed in the [API overview](overview.md#resources-and-schema).</span></span>

<span data-ttu-id="e34a1-141">このドキュメントでは、さまざまなリソースに関するドキュメントは基本的に、「 `{RESOURCE_NAME}` シナリオ別のグループ化」に似たサービスインデックスによってグループ化されます。</span><span class="sxs-lookup"><span data-stu-id="e34a1-141">For the sake of this documentation, the documentation about different resources will essentially be grouped by the `{RESOURCE_NAME}` found in the service index which is analogous to grouping by scenario.</span></span> 

<span data-ttu-id="e34a1-142">各リソースに一意のまたはがあるという要件はありません `@id` `@type` 。</span><span class="sxs-lookup"><span data-stu-id="e34a1-142">There is no requirement that each resource has a unique `@id` or `@type`.</span></span> <span data-ttu-id="e34a1-143">どのリソースを優先するかは、クライアントの実装によって決まります。</span><span class="sxs-lookup"><span data-stu-id="e34a1-143">It is up to the client implementation to determine which resource to prefer over another.</span></span> <span data-ttu-id="e34a1-144">考えられる1つの実装は、接続エラーやサーバーエラーが発生した場合に、同じまたは互換性のあるリソースを `@type` ラウンドロビン方式で使用できることです。</span><span class="sxs-lookup"><span data-stu-id="e34a1-144">One possible implementation is that resources of the same or compatible `@type` can be used in a round-robin fashion in case of connection failure or server error.</span></span>

### <a name="sample-request"></a><span data-ttu-id="e34a1-145">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="e34a1-145">Sample request</span></span>

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a><span data-ttu-id="e34a1-146">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="e34a1-146">Sample response</span></span>

[!code-JSON [service-index.json](./_data/service-index.json)]
