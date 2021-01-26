---
title: リポジトリシグネチャ、NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: リポジトリ署名リソースを使用すると、クライアントパッケージソースはリポジトリ署名機能を発表できます。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775339"
---
# <a name="repository-signatures"></a><span data-ttu-id="0cfb3-103">リポジトリの署名</span><span class="sxs-lookup"><span data-stu-id="0cfb3-103">Repository signatures</span></span>

<span data-ttu-id="0cfb3-104">パッケージソースが、公開されたパッケージへのリポジトリ署名の追加をサポートしている場合は、パッケージソースによって使用される署名証明書をクライアントが判断することができます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="0cfb3-105">このリソースを使用すると、クライアントは、リポジトリの署名付きパッケージが改ざんされているか、または予期しない署名証明書を持っているかを検出できます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="0cfb3-106">このリポジトリの署名情報を取得するために使用されるリソースは、 `RepositorySignatures` [サービスインデックス](service-index.md)で検出されたリソースです。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="0cfb3-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="0cfb3-107">Versioning</span></span>

<span data-ttu-id="0cfb3-108">次の `@type` 値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-108">The following `@type` value is used:</span></span>

<span data-ttu-id="0cfb3-109">@type 値</span><span class="sxs-lookup"><span data-stu-id="0cfb3-109">@type value</span></span>                | <span data-ttu-id="0cfb3-110">Notes</span><span class="sxs-lookup"><span data-stu-id="0cfb3-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="0cfb3-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="0cfb3-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="0cfb3-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="0cfb3-112">The initial release</span></span>
<span data-ttu-id="0cfb3-113">RepositorySignatures/4.9.0-</span><span class="sxs-lookup"><span data-stu-id="0cfb3-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="0cfb3-114">NuGet v. 4.9 以降のクライアントでサポートされています</span><span class="sxs-lookup"><span data-stu-id="0cfb3-114">Supported by NuGet v4.9+ clients</span></span>
<span data-ttu-id="0cfb3-115">RepositorySignatures/5.0.0</span><span class="sxs-lookup"><span data-stu-id="0cfb3-115">RepositorySignatures/5.0.0</span></span> | <span data-ttu-id="0cfb3-116">を有効に `allRepositorySigned` します。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-116">Allows enabling `allRepositorySigned`.</span></span> <span data-ttu-id="0cfb3-117">NuGet v1.0 以降のクライアントでサポートされています</span><span class="sxs-lookup"><span data-stu-id="0cfb3-117">Supported by NuGet v5.0+ clients</span></span>

## <a name="base-url"></a><span data-ttu-id="0cfb3-118">ベース URL</span><span class="sxs-lookup"><span data-stu-id="0cfb3-118">Base URL</span></span>

<span data-ttu-id="0cfb3-119">次の Api のエントリポイント URL は、 `@id` 前述のリソース値に関連付けられているプロパティの値です `@type` 。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-119">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="0cfb3-120">このトピックでは、プレースホルダー URL を使用 `{@id}` します。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-120">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="0cfb3-121">他のリソースとは異なり、 `{@id}` URL は HTTPS 経由で提供する必要があることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-121">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="0cfb3-122">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="0cfb3-122">HTTP methods</span></span>

<span data-ttu-id="0cfb3-123">リポジトリ署名リソースで見つかったすべての Url は、HTTP メソッドとだけをサポートし `GET` `HEAD` ます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-123">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="0cfb3-124">リポジトリシグネチャのインデックス</span><span class="sxs-lookup"><span data-stu-id="0cfb3-124">Repository signatures index</span></span>

<span data-ttu-id="0cfb3-125">リポジトリシグネチャのインデックスには、次の2つの情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-125">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="0cfb3-126">ソースで見つかったすべてのパッケージが、このパッケージソースによって署名されたリポジトリであるかどうか。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-126">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="0cfb3-127">パッケージに署名するためにパッケージソースによって使用される証明書の一覧。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-127">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="0cfb3-128">ほとんどの場合、証明書の一覧はのみに追加されます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-128">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="0cfb3-129">以前の署名証明書の有効期限が切れ、パッケージソースが新しい署名証明書を使用して開始する必要がある場合に、新しい証明書が一覧に追加されます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-129">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="0cfb3-130">証明書が一覧から削除された場合は、削除された署名証明書で作成されたすべてのパッケージ署名がクライアントによって有効と見なされなくなります。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-130">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="0cfb3-131">この場合、パッケージの署名は無効です (ただし、必ずしもパッケージではありません)。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-131">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="0cfb3-132">クライアントポリシーでは、パッケージを署名なしとしてインストールできます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-132">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="0cfb3-133">証明書の失効 (キーの侵害など) の場合、パッケージソースは、影響を受けた証明書によって署名されたすべてのパッケージを再署名する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-133">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="0cfb3-134">また、パッケージソースによって、影響を受けた証明書が署名証明書の一覧から削除されます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-134">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="0cfb3-135">次の要求は、リポジトリ署名インデックスをフェッチします。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-135">The following request fetches the repository signatures index.</span></span>

```
GET {@id}
```

<span data-ttu-id="0cfb3-136">リポジトリシグネチャインデックスは、次のプロパティを持つオブジェクトを含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-136">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="0cfb3-137">名前</span><span class="sxs-lookup"><span data-stu-id="0cfb3-137">Name</span></span>                | <span data-ttu-id="0cfb3-138">Type</span><span class="sxs-lookup"><span data-stu-id="0cfb3-138">Type</span></span>             | <span data-ttu-id="0cfb3-139">必須</span><span class="sxs-lookup"><span data-stu-id="0cfb3-139">Required</span></span> | <span data-ttu-id="0cfb3-140">Notes</span><span class="sxs-lookup"><span data-stu-id="0cfb3-140">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="0cfb3-141">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="0cfb3-141">allRepositorySigned</span></span> | <span data-ttu-id="0cfb3-142">boolean</span><span class="sxs-lookup"><span data-stu-id="0cfb3-142">boolean</span></span>          | <span data-ttu-id="0cfb3-143">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-143">yes</span></span>      | <span data-ttu-id="0cfb3-144">`false`4.7.0 および 4.9.0-リソース上にある必要があります</span><span class="sxs-lookup"><span data-stu-id="0cfb3-144">Must be `false` on 4.7.0 and 4.9.0 resources</span></span>
<span data-ttu-id="0cfb3-145">signingCertificates 書</span><span class="sxs-lookup"><span data-stu-id="0cfb3-145">signingCertificates</span></span> | <span data-ttu-id="0cfb3-146">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="0cfb3-146">array of objects</span></span> | <span data-ttu-id="0cfb3-147">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-147">yes</span></span>      | 

<span data-ttu-id="0cfb3-148">`allRepositorySigned`パッケージソースにリポジトリ署名のないパッケージが含まれている場合、ブール値は false に設定されます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-148">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="0cfb3-149">ブール値が true に設定されている場合、ソースで使用できるすべてのパッケージには、「」で説明されているいずれかの署名証明書によって生成されたリポジトリ署名が必要 `signingCertificates` です。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-149">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="0cfb3-150">`allRepositorySigned`4.7.0 と 4.9.0-のリソースでは、ブール値を false にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-150">The `allRepositorySigned` boolean must be false on the 4.7.0 and 4.9.0 resources.</span></span> <span data-ttu-id="0cfb3-151">NuGet v1.0、4.8、および v2.0 クライアントでは、が true に設定されているソースからパッケージをインストールすることはできません `allRepositorySigned` 。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-151">NuGet v4.7, v4.8, and v4.9 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="0cfb3-152">`signingCertificates` `allRepositorySigned` ブール値が true に設定されている場合、配列には1つ以上の署名証明書が必要です。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-152">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="0cfb3-153">配列が空で、が true に設定されている場合は、 `allRepositorySigned` ソースのすべてのパッケージが無効と見なされます。ただし、クライアントポリシーでは引き続きパッケージの使用が許可される場合があります。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-153">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="0cfb3-154">この配列の各要素は、次のプロパティを持つ JSON オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-154">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="0cfb3-155">名前</span><span class="sxs-lookup"><span data-stu-id="0cfb3-155">Name</span></span>         | <span data-ttu-id="0cfb3-156">Type</span><span class="sxs-lookup"><span data-stu-id="0cfb3-156">Type</span></span>   | <span data-ttu-id="0cfb3-157">必須</span><span class="sxs-lookup"><span data-stu-id="0cfb3-157">Required</span></span> | <span data-ttu-id="0cfb3-158">Notes</span><span class="sxs-lookup"><span data-stu-id="0cfb3-158">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="0cfb3-159">contentUrl</span><span class="sxs-lookup"><span data-stu-id="0cfb3-159">contentUrl</span></span>   | <span data-ttu-id="0cfb3-160">string</span><span class="sxs-lookup"><span data-stu-id="0cfb3-160">string</span></span> | <span data-ttu-id="0cfb3-161">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-161">yes</span></span>      | <span data-ttu-id="0cfb3-162">DER でエンコードされた公開証明書への絶対 URL</span><span class="sxs-lookup"><span data-stu-id="0cfb3-162">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="0cfb3-163">行っ</span><span class="sxs-lookup"><span data-stu-id="0cfb3-163">fingerprints</span></span> | <span data-ttu-id="0cfb3-164">object</span><span class="sxs-lookup"><span data-stu-id="0cfb3-164">object</span></span> | <span data-ttu-id="0cfb3-165">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-165">yes</span></span>      |
<span data-ttu-id="0cfb3-166">subject</span><span class="sxs-lookup"><span data-stu-id="0cfb3-166">subject</span></span>      | <span data-ttu-id="0cfb3-167">string</span><span class="sxs-lookup"><span data-stu-id="0cfb3-167">string</span></span> | <span data-ttu-id="0cfb3-168">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-168">yes</span></span>      | <span data-ttu-id="0cfb3-169">証明書のサブジェクト識別名</span><span class="sxs-lookup"><span data-stu-id="0cfb3-169">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="0cfb3-170">発行者</span><span class="sxs-lookup"><span data-stu-id="0cfb3-170">issuer</span></span>       | <span data-ttu-id="0cfb3-171">string</span><span class="sxs-lookup"><span data-stu-id="0cfb3-171">string</span></span> | <span data-ttu-id="0cfb3-172">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-172">yes</span></span>      | <span data-ttu-id="0cfb3-173">証明書の発行者の識別名</span><span class="sxs-lookup"><span data-stu-id="0cfb3-173">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="0cfb3-174">notBefore</span><span class="sxs-lookup"><span data-stu-id="0cfb3-174">notBefore</span></span>    | <span data-ttu-id="0cfb3-175">string</span><span class="sxs-lookup"><span data-stu-id="0cfb3-175">string</span></span> | <span data-ttu-id="0cfb3-176">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-176">yes</span></span>      | <span data-ttu-id="0cfb3-177">証明書の有効期間の開始タイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="0cfb3-177">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="0cfb3-178">notAfter</span><span class="sxs-lookup"><span data-stu-id="0cfb3-178">notAfter</span></span>     | <span data-ttu-id="0cfb3-179">string</span><span class="sxs-lookup"><span data-stu-id="0cfb3-179">string</span></span> | <span data-ttu-id="0cfb3-180">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-180">yes</span></span>      | <span data-ttu-id="0cfb3-181">証明書の有効期間の終了タイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="0cfb3-181">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="0cfb3-182">を HTTPS 経由で提供する必要があることに注意して `contentUrl` ください。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-182">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="0cfb3-183">この URL には特定の URL パターンがないため、このリポジトリ署名インデックスドキュメントを使用して動的に検出する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-183">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="0cfb3-184">このオブジェクトのすべてのプロパティ (を除く `contentUrl` ) は、で見つかった証明書の派生である必要があり `contentUrl` ます。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-184">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="0cfb3-185">これらの派生プロパティは、ラウンドトリップを最小限に抑えるために便利です。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-185">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="0cfb3-186">`fingerprints` オブジェクトには、次のプロパティがあります。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-186">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="0cfb3-187">名前</span><span class="sxs-lookup"><span data-stu-id="0cfb3-187">Name</span></span>                   | <span data-ttu-id="0cfb3-188">Type</span><span class="sxs-lookup"><span data-stu-id="0cfb3-188">Type</span></span>   | <span data-ttu-id="0cfb3-189">必須</span><span class="sxs-lookup"><span data-stu-id="0cfb3-189">Required</span></span> | <span data-ttu-id="0cfb3-190">Notes</span><span class="sxs-lookup"><span data-stu-id="0cfb3-190">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="0cfb3-191">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="0cfb3-191">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="0cfb3-192">string</span><span class="sxs-lookup"><span data-stu-id="0cfb3-192">string</span></span> | <span data-ttu-id="0cfb3-193">はい</span><span class="sxs-lookup"><span data-stu-id="0cfb3-193">yes</span></span>      | <span data-ttu-id="0cfb3-194">SHA-256 フィンガープリント</span><span class="sxs-lookup"><span data-stu-id="0cfb3-194">The SHA-256 fingerprint</span></span>

<span data-ttu-id="0cfb3-195">キー名 `2.16.840.1.101.3.4.2.1` は、SHA-256 ハッシュアルゴリズムの OID です。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-195">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="0cfb3-196">すべてのハッシュ値は、小文字でエンコードされたハッシュダイジェストの文字列形式である必要があります。</span><span class="sxs-lookup"><span data-stu-id="0cfb3-196">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="0cfb3-197">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="0cfb3-197">Sample request</span></span>

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a><span data-ttu-id="0cfb3-198">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="0cfb3-198">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
