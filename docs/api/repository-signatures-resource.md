---
title: リポジトリの署名、NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: リポジトリのリソースの署名は、クライアントがパッケージ ソースにはリポジトリの署名機能をご案内できます。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 81d32a7011268e45136e00cdb7345a95070aae06
ms.sourcegitcommit: be9c51b4b095aea40ef41bbea7e12ef0a194ee74
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/11/2018
ms.locfileid: "53248443"
---
# <a name="repository-signatures"></a><span data-ttu-id="a98b0-103">リポジトリの署名</span><span class="sxs-lookup"><span data-stu-id="a98b0-103">Repository signatures</span></span>

<span data-ttu-id="a98b0-104">パッケージ ソースでは、公開済みのパッケージに追加するリポジトリの署名をサポートする場合をクライアントがパッケージ ソースで使用される署名証明書を判別できます。</span><span class="sxs-lookup"><span data-stu-id="a98b0-104">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="a98b0-105">このリソースは、パッケージが改ざんされてまたは予期しない署名証明書が、リポジトリが署名されているかどうかを検出するためにクライアントを許可します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-105">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="a98b0-106">このリポジトリの署名情報を取得するために使用されるリソースは、`RepositorySignatures`リソースで見つかった、[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-106">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="a98b0-107">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="a98b0-107">Versioning</span></span>

<span data-ttu-id="a98b0-108">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="a98b0-108">The following `@type` value is used:</span></span>

<span data-ttu-id="a98b0-109">@type の値</span><span class="sxs-lookup"><span data-stu-id="a98b0-109">@type value</span></span>                | <span data-ttu-id="a98b0-110">メモ</span><span class="sxs-lookup"><span data-stu-id="a98b0-110">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="a98b0-111">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="a98b0-111">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="a98b0-112">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="a98b0-112">The initial release</span></span>
<span data-ttu-id="a98b0-113">RepositorySignatures/4.9.0</span><span class="sxs-lookup"><span data-stu-id="a98b0-113">RepositorySignatures/4.9.0</span></span> | <span data-ttu-id="a98b0-114">により、有効にします。 `allRepositorySigned`</span><span class="sxs-lookup"><span data-stu-id="a98b0-114">Allows enabling `allRepositorySigned`</span></span>

## <a name="base-url"></a><span data-ttu-id="a98b0-115">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="a98b0-115">Base URL</span></span>

<span data-ttu-id="a98b0-116">次の api エントリ ポイントの URL の値である、`@id`前述のリソースに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="a98b0-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="a98b0-117">このトピックでは、プレース ホルダー URL を使用して`{@id}`します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="a98b0-118">なお、その他のリソースとは異なり、 `{@id}` URL が HTTPS 経由で提供する必要です。</span><span class="sxs-lookup"><span data-stu-id="a98b0-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="a98b0-119">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="a98b0-119">HTTP methods</span></span>

<span data-ttu-id="a98b0-120">リポジトリの署名のリソースの HTTP のみのサポート メソッドで見つかったすべての Url`GET`と`HEAD`します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="a98b0-121">リポジトリの署名のインデックス</span><span class="sxs-lookup"><span data-stu-id="a98b0-121">Repository signatures index</span></span>

<span data-ttu-id="a98b0-122">リポジトリの署名のインデックスには、2 つの情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a98b0-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="a98b0-123">すべてのパッケージがソースで検出されたかどうかは、このパッケージ ソースで署名されたリポジトリです。</span><span class="sxs-lookup"><span data-stu-id="a98b0-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="a98b0-124">パッケージ ソースでパッケージの署名に使用される証明書の一覧。</span><span class="sxs-lookup"><span data-stu-id="a98b0-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="a98b0-125">ほとんどの場合は証明書の一覧にしか追加されます。</span><span class="sxs-lookup"><span data-stu-id="a98b0-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="a98b0-126">以前の署名証明書の有効期限が切れたパッケージ ソースが新しい署名証明書の使用を開始する必要がある場合は、一覧に新しい証明書を追加するは。</span><span class="sxs-lookup"><span data-stu-id="a98b0-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="a98b0-127">一覧から証明書を削除する場合、署名証明書の削除で作成されたすべてのパッケージの署名する必要がありますされなく有効と見なされる、クライアントによってを意味します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="a98b0-128">この場合、パッケージの署名 (ただし、必ずしもパッケージ) が無効です。</span><span class="sxs-lookup"><span data-stu-id="a98b0-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="a98b0-129">クライアント ポリシーには、符号なしとしてパッケージをインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="a98b0-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="a98b0-130">証明書の失効 (例: キーの侵害) の場合は、影響を受ける証明書によって署名されたすべてのパッケージを再署名するパッケージ ソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="a98b0-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="a98b0-131">さらに、パッケージ ソースでは、署名証明書のリストから影響を受けるの証明書を削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a98b0-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="a98b0-132">次の要求は、リポジトリの署名のインデックスをフェッチします。</span><span class="sxs-lookup"><span data-stu-id="a98b0-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="a98b0-133">リポジトリ署名のインデックスは、次のプロパティを持つオブジェクトを含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="a98b0-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="a98b0-134">名前</span><span class="sxs-lookup"><span data-stu-id="a98b0-134">Name</span></span>                | <span data-ttu-id="a98b0-135">種類</span><span class="sxs-lookup"><span data-stu-id="a98b0-135">Type</span></span>             | <span data-ttu-id="a98b0-136">必須</span><span class="sxs-lookup"><span data-stu-id="a98b0-136">Required</span></span> | <span data-ttu-id="a98b0-137">メモ</span><span class="sxs-lookup"><span data-stu-id="a98b0-137">Notes</span></span>
------------------- | ---------------- | -------- | -----
<span data-ttu-id="a98b0-138">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="a98b0-138">allRepositorySigned</span></span> | <span data-ttu-id="a98b0-139">boolean</span><span class="sxs-lookup"><span data-stu-id="a98b0-139">boolean</span></span>          | <span data-ttu-id="a98b0-140">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-140">yes</span></span>      | <span data-ttu-id="a98b0-141">必要があります`false`4.7.0 のリソース</span><span class="sxs-lookup"><span data-stu-id="a98b0-141">Must be `false` on 4.7.0 resource</span></span>
<span data-ttu-id="a98b0-142">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="a98b0-142">signingCertificates</span></span> | <span data-ttu-id="a98b0-143">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="a98b0-143">array of objects</span></span> | <span data-ttu-id="a98b0-144">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-144">yes</span></span>      | 

<span data-ttu-id="a98b0-145">`allRepositorySigned`パッケージ ソースの一部のパッケージ リポジトリの署名がない場合、ブール値が false に設定します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-145">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="a98b0-146">ソースで説明されている署名証明書のいずれかによって生成されるリポジトリ シグネチャをいる必要があります、ブール値が true で入手できるすべてのパッケージに設定されている場合`signingCertificates`します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-146">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

> [!Warning]
> <span data-ttu-id="a98b0-147">`allRepositorySigned`ブール、4.7.0 で false である必要がありますリソース。</span><span class="sxs-lookup"><span data-stu-id="a98b0-147">The `allRepositorySigned` boolean must be false on the 4.7.0 resource.</span></span> <span data-ttu-id="a98b0-148">NuGet v4.7 と v4.8 クライアントがソースからパッケージをインストールことはできません`allRepositorySigned`を true に設定します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-148">NuGet v4.7 and v4.8 clients cannot install packages from sources that have `allRepositorySigned` set to true.</span></span>

<span data-ttu-id="a98b0-149">内の 1 つまたは複数の署名証明書が必要があります、`signingCertificates`配列の場合、`allRepositorySigned`ブール値の設定を true にします。</span><span class="sxs-lookup"><span data-stu-id="a98b0-149">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="a98b0-150">配列が空の場合と`allRepositorySigned`に設定が true の場合、元のすべてのパッケージが無効と見なされるもクライアント ポリシーをパッケージの使用を許可可能性がありますがします。</span><span class="sxs-lookup"><span data-stu-id="a98b0-150">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="a98b0-151">この配列内の各要素は、次のプロパティを持つ JSON オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="a98b0-151">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="a98b0-152">名前</span><span class="sxs-lookup"><span data-stu-id="a98b0-152">Name</span></span>         | <span data-ttu-id="a98b0-153">種類</span><span class="sxs-lookup"><span data-stu-id="a98b0-153">Type</span></span>   | <span data-ttu-id="a98b0-154">必須</span><span class="sxs-lookup"><span data-stu-id="a98b0-154">Required</span></span> | <span data-ttu-id="a98b0-155">メモ</span><span class="sxs-lookup"><span data-stu-id="a98b0-155">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="a98b0-156">contentUrl</span><span class="sxs-lookup"><span data-stu-id="a98b0-156">contentUrl</span></span>   | <span data-ttu-id="a98b0-157">string</span><span class="sxs-lookup"><span data-stu-id="a98b0-157">string</span></span> | <span data-ttu-id="a98b0-158">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-158">yes</span></span>      | <span data-ttu-id="a98b0-159">DER でエンコードされた公開証明書への絶対 URL</span><span class="sxs-lookup"><span data-stu-id="a98b0-159">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="a98b0-160">指紋</span><span class="sxs-lookup"><span data-stu-id="a98b0-160">fingerprints</span></span> | <span data-ttu-id="a98b0-161">object</span><span class="sxs-lookup"><span data-stu-id="a98b0-161">object</span></span> | <span data-ttu-id="a98b0-162">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-162">yes</span></span>      |
<span data-ttu-id="a98b0-163">件名</span><span class="sxs-lookup"><span data-stu-id="a98b0-163">subject</span></span>      | <span data-ttu-id="a98b0-164">string</span><span class="sxs-lookup"><span data-stu-id="a98b0-164">string</span></span> | <span data-ttu-id="a98b0-165">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-165">yes</span></span>      | <span data-ttu-id="a98b0-166">証明書からサブジェクト識別名</span><span class="sxs-lookup"><span data-stu-id="a98b0-166">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="a98b0-167">issuer</span><span class="sxs-lookup"><span data-stu-id="a98b0-167">issuer</span></span>       | <span data-ttu-id="a98b0-168">string</span><span class="sxs-lookup"><span data-stu-id="a98b0-168">string</span></span> | <span data-ttu-id="a98b0-169">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-169">yes</span></span>      | <span data-ttu-id="a98b0-170">証明書の発行者の識別名</span><span class="sxs-lookup"><span data-stu-id="a98b0-170">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="a98b0-171">notBefore</span><span class="sxs-lookup"><span data-stu-id="a98b0-171">notBefore</span></span>    | <span data-ttu-id="a98b0-172">string</span><span class="sxs-lookup"><span data-stu-id="a98b0-172">string</span></span> | <span data-ttu-id="a98b0-173">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-173">yes</span></span>      | <span data-ttu-id="a98b0-174">証明書の有効期間の開始タイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="a98b0-174">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="a98b0-175">notAfter</span><span class="sxs-lookup"><span data-stu-id="a98b0-175">notAfter</span></span>     | <span data-ttu-id="a98b0-176">string</span><span class="sxs-lookup"><span data-stu-id="a98b0-176">string</span></span> | <span data-ttu-id="a98b0-177">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-177">yes</span></span>      | <span data-ttu-id="a98b0-178">証明書の有効期間の終了のタイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="a98b0-178">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="a98b0-179">なお、 `contentUrl` HTTPS 経由で提供するために必要です。</span><span class="sxs-lookup"><span data-stu-id="a98b0-179">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="a98b0-180">この URL は、特定の URL パターンがないので、このリポジトリの署名のインデックスのドキュメントを使用して動的に検出する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a98b0-180">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="a98b0-181">このオブジェクトのすべてのプロパティ (出てくる`contentUrl`) にある証明書から派生可能である必要があります`contentUrl`します。</span><span class="sxs-lookup"><span data-stu-id="a98b0-181">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="a98b0-182">これらの派生可能プロパティは、ラウンド トリップを最小限に抑えるに便利な機能として提供されます。</span><span class="sxs-lookup"><span data-stu-id="a98b0-182">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="a98b0-183">`fingerprints`オブジェクトは、次のプロパティ。</span><span class="sxs-lookup"><span data-stu-id="a98b0-183">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="a98b0-184">名前</span><span class="sxs-lookup"><span data-stu-id="a98b0-184">Name</span></span>                   | <span data-ttu-id="a98b0-185">種類</span><span class="sxs-lookup"><span data-stu-id="a98b0-185">Type</span></span>   | <span data-ttu-id="a98b0-186">必須</span><span class="sxs-lookup"><span data-stu-id="a98b0-186">Required</span></span> | <span data-ttu-id="a98b0-187">メモ</span><span class="sxs-lookup"><span data-stu-id="a98b0-187">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="a98b0-188">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="a98b0-188">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="a98b0-189">string</span><span class="sxs-lookup"><span data-stu-id="a98b0-189">string</span></span> | <span data-ttu-id="a98b0-190">可</span><span class="sxs-lookup"><span data-stu-id="a98b0-190">yes</span></span>      | <span data-ttu-id="a98b0-191">SHA 256 フィンガー プリント</span><span class="sxs-lookup"><span data-stu-id="a98b0-191">The SHA-256 fingerprint</span></span>

<span data-ttu-id="a98b0-192">キー名`2.16.840.1.101.3.4.2.1`sha-256 ハッシュ アルゴリズムの oid。</span><span class="sxs-lookup"><span data-stu-id="a98b0-192">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="a98b0-193">すべてのハッシュ値は、ハッシュのダイジェストの小文字、16 進エンコードされた文字列形式にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a98b0-193">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="a98b0-194">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="a98b0-194">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="a98b0-195">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="a98b0-195">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
