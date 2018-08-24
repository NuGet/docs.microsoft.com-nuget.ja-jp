---
title: リポジトリの署名、NuGet API |Microsoft Docs
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 3/2/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: リポジトリのリソースの署名は、クライアントがパッケージ ソースにはリポジトリの署名機能をご案内できます。
keywords: NuGet API リポジトリの署名、署名証明書、nuget.org nuget.org パッケージへの署名
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 32dd2ee19261488a2b1b92724095a11ced69ae68
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/21/2018
ms.locfileid: "42793198"
---
# <a name="repository-signatures"></a><span data-ttu-id="02c7b-104">リポジトリの署名</span><span class="sxs-lookup"><span data-stu-id="02c7b-104">Repository signatures</span></span>

<span data-ttu-id="02c7b-105">パッケージ ソースでは、公開済みのパッケージに追加するリポジトリの署名をサポートする場合をクライアントがパッケージ ソースで使用される署名証明書を判別できます。</span><span class="sxs-lookup"><span data-stu-id="02c7b-105">If a package source supports adding repository signatures to published packages, it is possible for a client to determine the signing certificates that are used by the package source.</span></span> <span data-ttu-id="02c7b-106">このリソースは、パッケージが改ざんされてまたは予期しない署名証明書が、リポジトリが署名されているかどうかを検出するためにクライアントを許可します。</span><span class="sxs-lookup"><span data-stu-id="02c7b-106">This resource allows clients to detect whether a repository signed package has been tampered or has an unexpected signing certificate.</span></span>

<span data-ttu-id="02c7b-107">このリポジトリの署名情報を取得するために使用されるリソースは、`RepositorySignatures`リソースで見つかった、[サービス インデックス](service-index.md)します。</span><span class="sxs-lookup"><span data-stu-id="02c7b-107">The resource used for fetching this repository signature information is the `RepositorySignatures` resource found in the [service index](service-index.md).</span></span>

> [!Note]
> <span data-ttu-id="02c7b-108">NuGet.org 開始の発表、`RepositorySignatures`リソース、近い将来にします。</span><span class="sxs-lookup"><span data-stu-id="02c7b-108">NuGet.org will start announcing the `RepositorySignatures` resource in the near future.</span></span>

## <a name="versioning"></a><span data-ttu-id="02c7b-109">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="02c7b-109">Versioning</span></span>

<span data-ttu-id="02c7b-110">次`@type`値が使用されます。</span><span class="sxs-lookup"><span data-stu-id="02c7b-110">The following `@type` value is used:</span></span>

<span data-ttu-id="02c7b-111">@type の値</span><span class="sxs-lookup"><span data-stu-id="02c7b-111">@type value</span></span>                | <span data-ttu-id="02c7b-112">メモ</span><span class="sxs-lookup"><span data-stu-id="02c7b-112">Notes</span></span>
-------------------------- | -----
<span data-ttu-id="02c7b-113">RepositorySignatures/4.7.0</span><span class="sxs-lookup"><span data-stu-id="02c7b-113">RepositorySignatures/4.7.0</span></span> | <span data-ttu-id="02c7b-114">最初のリリース</span><span class="sxs-lookup"><span data-stu-id="02c7b-114">The initial release</span></span>

## <a name="base-url"></a><span data-ttu-id="02c7b-115">[基本 URL]</span><span class="sxs-lookup"><span data-stu-id="02c7b-115">Base URL</span></span>

<span data-ttu-id="02c7b-116">次の api エントリ ポイントの URL の値である、`@id`前述のリソースに関連付けられたプロパティ`@type`値。</span><span class="sxs-lookup"><span data-stu-id="02c7b-116">The entry point URL for the following APIs is the value of the `@id` property associated with the aforementioned resource `@type` value.</span></span> <span data-ttu-id="02c7b-117">このトピックでは、プレース ホルダー URL を使用して`{@id}`します。</span><span class="sxs-lookup"><span data-stu-id="02c7b-117">This topic uses the placeholder URL `{@id}`.</span></span>

<span data-ttu-id="02c7b-118">なお、その他のリソースとは異なり、 `{@id}` URL が HTTPS 経由で提供する必要です。</span><span class="sxs-lookup"><span data-stu-id="02c7b-118">Note that unlike other resources, the `{@id}` URL is required to be served over HTTPS.</span></span>

## <a name="http-methods"></a><span data-ttu-id="02c7b-119">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="02c7b-119">HTTP methods</span></span>

<span data-ttu-id="02c7b-120">リポジトリの署名のリソースの HTTP のみのサポート メソッドで見つかったすべての Url`GET`と`HEAD`します。</span><span class="sxs-lookup"><span data-stu-id="02c7b-120">All URLs found in the repository signatures resource support only the HTTP methods `GET` and `HEAD`.</span></span>

## <a name="repository-signatures-index"></a><span data-ttu-id="02c7b-121">リポジトリの署名のインデックス</span><span class="sxs-lookup"><span data-stu-id="02c7b-121">Repository signatures index</span></span>

<span data-ttu-id="02c7b-122">リポジトリの署名のインデックスには、2 つの情報が含まれています。</span><span class="sxs-lookup"><span data-stu-id="02c7b-122">The repository signatures index contains two pieces of information:</span></span>

1. <span data-ttu-id="02c7b-123">すべてのパッケージがソースで検出されたかどうかは、このパッケージ ソースで署名されたリポジトリです。</span><span class="sxs-lookup"><span data-stu-id="02c7b-123">Whether or not all packages found on the source are repository signed by this package source.</span></span>
1. <span data-ttu-id="02c7b-124">パッケージ ソースでパッケージの署名に使用される証明書の一覧。</span><span class="sxs-lookup"><span data-stu-id="02c7b-124">The list of certificates used by the package source to sign packages.</span></span>

<span data-ttu-id="02c7b-125">ほとんどの場合は証明書の一覧にしか追加されます。</span><span class="sxs-lookup"><span data-stu-id="02c7b-125">In most cases, the list of certificates will only ever be appended to.</span></span> <span data-ttu-id="02c7b-126">以前の署名証明書の有効期限が切れたパッケージ ソースが新しい署名証明書の使用を開始する必要がある場合は、一覧に新しい証明書を追加するは。</span><span class="sxs-lookup"><span data-stu-id="02c7b-126">New certificates would be added to the list when the previous signing certificate has expired and the package source needs to start using a new signing certificate.</span></span> <span data-ttu-id="02c7b-127">一覧から証明書を削除する場合、署名証明書の削除で作成されたすべてのパッケージの署名する必要がありますされなく有効と見なされる、クライアントによってを意味します。</span><span class="sxs-lookup"><span data-stu-id="02c7b-127">If a certificate is removed from the list, that means that all package signatures created with the removed signing certificate should no longer be considered valid by the client.</span></span> <span data-ttu-id="02c7b-128">この場合、パッケージの署名 (ただし、必ずしもパッケージ) が無効です。</span><span class="sxs-lookup"><span data-stu-id="02c7b-128">In this case, the package signature (but not necessarily the package) is invalid.</span></span> <span data-ttu-id="02c7b-129">クライアント ポリシーには、符号なしとしてパッケージをインストールすることができます。</span><span class="sxs-lookup"><span data-stu-id="02c7b-129">A client policy may allow installing the package as unsigned.</span></span>

<span data-ttu-id="02c7b-130">証明書の失効 (例: キーの侵害) の場合は、影響を受ける証明書によって署名されたすべてのパッケージを再署名するパッケージ ソースが必要です。</span><span class="sxs-lookup"><span data-stu-id="02c7b-130">In the case of certificate revocation (e.g. key compromise), the package source is expected to re-sign all packages signed by the affected certificate.</span></span> <span data-ttu-id="02c7b-131">さらに、パッケージ ソースでは、署名証明書のリストから影響を受けるの証明書を削除する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02c7b-131">Additionally, the package source should remove the affected certificate from the signing certificate list.</span></span>

<span data-ttu-id="02c7b-132">次の要求は、リポジトリの署名のインデックスをフェッチします。</span><span class="sxs-lookup"><span data-stu-id="02c7b-132">The following request fetches the repository signatures index.</span></span>

    GET {@id}

<span data-ttu-id="02c7b-133">リポジトリ署名のインデックスは、次のプロパティを持つオブジェクトを含む JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="02c7b-133">The repository signature index is a JSON document that contains an object with the following properties:</span></span>

<span data-ttu-id="02c7b-134">name</span><span class="sxs-lookup"><span data-stu-id="02c7b-134">Name</span></span>                | <span data-ttu-id="02c7b-135">種類</span><span class="sxs-lookup"><span data-stu-id="02c7b-135">Type</span></span>             | <span data-ttu-id="02c7b-136">必須</span><span class="sxs-lookup"><span data-stu-id="02c7b-136">Required</span></span>
------------------- | ---------------- | --------
<span data-ttu-id="02c7b-137">allRepositorySigned</span><span class="sxs-lookup"><span data-stu-id="02c7b-137">allRepositorySigned</span></span> | <span data-ttu-id="02c7b-138">boolean</span><span class="sxs-lookup"><span data-stu-id="02c7b-138">boolean</span></span>          | <span data-ttu-id="02c7b-139">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-139">yes</span></span>
<span data-ttu-id="02c7b-140">signingCertificates</span><span class="sxs-lookup"><span data-stu-id="02c7b-140">signingCertificates</span></span> | <span data-ttu-id="02c7b-141">オブジェクトの配列</span><span class="sxs-lookup"><span data-stu-id="02c7b-141">array of objects</span></span> | <span data-ttu-id="02c7b-142">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-142">yes</span></span>

<span data-ttu-id="02c7b-143">`allRepositorySigned`パッケージ ソースの一部のパッケージ リポジトリの署名がない場合、ブール値が false に設定します。</span><span class="sxs-lookup"><span data-stu-id="02c7b-143">The `allRepositorySigned` boolean is set to false if the package source has some packages that have no repository signature.</span></span> <span data-ttu-id="02c7b-144">ソースで説明されている署名証明書のいずれかによって生成されるリポジトリ シグネチャをいる必要があります、ブール値が true で入手できるすべてのパッケージに設定されている場合`signingCertificates`します。</span><span class="sxs-lookup"><span data-stu-id="02c7b-144">If the boolean is set to true, all packages available on the source must have a repository signature produced by one of the signing certificates mentioned in `signingCertificates`.</span></span>

<span data-ttu-id="02c7b-145">内の 1 つまたは複数の署名証明書が必要があります、`signingCertificates`配列の場合、`allRepositorySigned`ブール値の設定を true にします。</span><span class="sxs-lookup"><span data-stu-id="02c7b-145">There should be one or more signing certificates in the `signingCertificates` array if the `allRepositorySigned` boolean is set to true.</span></span> <span data-ttu-id="02c7b-146">配列が空の場合と`allRepositorySigned`に設定が true の場合、元のすべてのパッケージが無効と見なされるもクライアント ポリシーをパッケージの使用を許可可能性がありますがします。</span><span class="sxs-lookup"><span data-stu-id="02c7b-146">If the array is empty and `allRepositorySigned` is set to true, all packages from the source should be considered invalid, although a client policy may still allow consumption of packages.</span></span> <span data-ttu-id="02c7b-147">この配列内の各要素は、次のプロパティを持つ JSON オブジェクトです。</span><span class="sxs-lookup"><span data-stu-id="02c7b-147">Each element in this array is a JSON object with the following properties.</span></span>

<span data-ttu-id="02c7b-148">name</span><span class="sxs-lookup"><span data-stu-id="02c7b-148">Name</span></span>         | <span data-ttu-id="02c7b-149">種類</span><span class="sxs-lookup"><span data-stu-id="02c7b-149">Type</span></span>   | <span data-ttu-id="02c7b-150">必須</span><span class="sxs-lookup"><span data-stu-id="02c7b-150">Required</span></span> | <span data-ttu-id="02c7b-151">メモ</span><span class="sxs-lookup"><span data-stu-id="02c7b-151">Notes</span></span>
------------ | ------ | -------- | -----
<span data-ttu-id="02c7b-152">contentUrl</span><span class="sxs-lookup"><span data-stu-id="02c7b-152">contentUrl</span></span>   | <span data-ttu-id="02c7b-153">string</span><span class="sxs-lookup"><span data-stu-id="02c7b-153">string</span></span> | <span data-ttu-id="02c7b-154">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-154">yes</span></span>      | <span data-ttu-id="02c7b-155">DER でエンコードされた公開証明書への絶対 URL</span><span class="sxs-lookup"><span data-stu-id="02c7b-155">Absolute URL to the DER-encoded public certificate</span></span>
<span data-ttu-id="02c7b-156">指紋</span><span class="sxs-lookup"><span data-stu-id="02c7b-156">fingerprints</span></span> | <span data-ttu-id="02c7b-157">object</span><span class="sxs-lookup"><span data-stu-id="02c7b-157">object</span></span> | <span data-ttu-id="02c7b-158">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-158">yes</span></span>      |
<span data-ttu-id="02c7b-159">件名</span><span class="sxs-lookup"><span data-stu-id="02c7b-159">subject</span></span>      | <span data-ttu-id="02c7b-160">string</span><span class="sxs-lookup"><span data-stu-id="02c7b-160">string</span></span> | <span data-ttu-id="02c7b-161">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-161">yes</span></span>      | <span data-ttu-id="02c7b-162">証明書からサブジェクト識別名</span><span class="sxs-lookup"><span data-stu-id="02c7b-162">The subject distinguished name from the certificate</span></span>
<span data-ttu-id="02c7b-163">issuer</span><span class="sxs-lookup"><span data-stu-id="02c7b-163">issuer</span></span>       | <span data-ttu-id="02c7b-164">string</span><span class="sxs-lookup"><span data-stu-id="02c7b-164">string</span></span> | <span data-ttu-id="02c7b-165">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-165">yes</span></span>      | <span data-ttu-id="02c7b-166">証明書の発行者の識別名</span><span class="sxs-lookup"><span data-stu-id="02c7b-166">The distinguished name of the certificate's issuer</span></span>
<span data-ttu-id="02c7b-167">notBefore</span><span class="sxs-lookup"><span data-stu-id="02c7b-167">notBefore</span></span>    | <span data-ttu-id="02c7b-168">string</span><span class="sxs-lookup"><span data-stu-id="02c7b-168">string</span></span> | <span data-ttu-id="02c7b-169">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-169">yes</span></span>      | <span data-ttu-id="02c7b-170">証明書の有効期間の開始タイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="02c7b-170">The starting timestamp of the certificate's validity period</span></span>
<span data-ttu-id="02c7b-171">notAfter</span><span class="sxs-lookup"><span data-stu-id="02c7b-171">notAfter</span></span>     | <span data-ttu-id="02c7b-172">string</span><span class="sxs-lookup"><span data-stu-id="02c7b-172">string</span></span> | <span data-ttu-id="02c7b-173">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-173">yes</span></span>      | <span data-ttu-id="02c7b-174">証明書の有効期間の終了のタイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="02c7b-174">The ending timestamp of the certificate's validity period</span></span>

<span data-ttu-id="02c7b-175">なお、 `contentUrl` HTTPS 経由で提供するために必要です。</span><span class="sxs-lookup"><span data-stu-id="02c7b-175">Note that the `contentUrl` is required to be served over HTTPS.</span></span> <span data-ttu-id="02c7b-176">この URL は、特定の URL パターンがないので、このリポジトリの署名のインデックスのドキュメントを使用して動的に検出する必要があります。</span><span class="sxs-lookup"><span data-stu-id="02c7b-176">This URL has no specific URL pattern and must be dynamically discovered using this repository signatures index document.</span></span> 

<span data-ttu-id="02c7b-177">このオブジェクトのすべてのプロパティ (出てくる`contentUrl`) にある証明書から派生可能である必要があります`contentUrl`します。</span><span class="sxs-lookup"><span data-stu-id="02c7b-177">All properties in this object (aside from `contentUrl`) must be derivable from the certificate found at `contentUrl`.</span></span>
<span data-ttu-id="02c7b-178">これらの派生可能プロパティは、ラウンド トリップを最小限に抑えるに便利な機能として提供されます。</span><span class="sxs-lookup"><span data-stu-id="02c7b-178">These derivable properties are provided as a convenience to minimize round trips.</span></span>

<span data-ttu-id="02c7b-179">`fingerprints`オブジェクトは、次のプロパティ。</span><span class="sxs-lookup"><span data-stu-id="02c7b-179">The `fingerprints` object has the following properties:</span></span>

<span data-ttu-id="02c7b-180">name</span><span class="sxs-lookup"><span data-stu-id="02c7b-180">Name</span></span>                   | <span data-ttu-id="02c7b-181">種類</span><span class="sxs-lookup"><span data-stu-id="02c7b-181">Type</span></span>   | <span data-ttu-id="02c7b-182">必須</span><span class="sxs-lookup"><span data-stu-id="02c7b-182">Required</span></span> | <span data-ttu-id="02c7b-183">メモ</span><span class="sxs-lookup"><span data-stu-id="02c7b-183">Notes</span></span>
---------------------- | ------ | -------- | -----
<span data-ttu-id="02c7b-184">2.16.840.1.101.3.4.2.1</span><span class="sxs-lookup"><span data-stu-id="02c7b-184">2.16.840.1.101.3.4.2.1</span></span> | <span data-ttu-id="02c7b-185">string</span><span class="sxs-lookup"><span data-stu-id="02c7b-185">string</span></span> | <span data-ttu-id="02c7b-186">可</span><span class="sxs-lookup"><span data-stu-id="02c7b-186">yes</span></span>      | <span data-ttu-id="02c7b-187">SHA 256 フィンガー プリント</span><span class="sxs-lookup"><span data-stu-id="02c7b-187">The SHA-256 fingerprint</span></span>

<span data-ttu-id="02c7b-188">キー名`2.16.840.1.101.3.4.2.1`sha-256 ハッシュ アルゴリズムの oid。</span><span class="sxs-lookup"><span data-stu-id="02c7b-188">The key name `2.16.840.1.101.3.4.2.1` is the OID of the SHA-256 hash algorithm.</span></span>

<span data-ttu-id="02c7b-189">すべてのハッシュ値は、ハッシュのダイジェストの小文字、16 進エンコードされた文字列形式にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="02c7b-189">All hash values must be lowercase, hex-encoded string representations of the hash digest.</span></span>

### <a name="sample-request"></a><span data-ttu-id="02c7b-190">要求のサンプル</span><span class="sxs-lookup"><span data-stu-id="02c7b-190">Sample request</span></span>

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a><span data-ttu-id="02c7b-191">応答のサンプル</span><span class="sxs-lookup"><span data-stu-id="02c7b-191">Sample response</span></span>

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
