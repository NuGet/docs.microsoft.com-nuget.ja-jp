---
title: 署名付きパッケージ
description: NuGet パッケージへの署名の要件。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 486bf4032e156168f9b2fef57ccdae0c372b2eff
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977512"
---
# <a name="signed-packages"></a><span data-ttu-id="59208-103">署名済みパッケージ</span><span class="sxs-lookup"><span data-stu-id="59208-103">Signed packages</span></span>

<span data-ttu-id="59208-104">*NuGet 4.6.0+ と Visual Studio 2017 バージョン 15.6 以降*</span><span class="sxs-lookup"><span data-stu-id="59208-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="59208-105">NuGet パッケージには、改ざんされたコンテンツに対する保護を提供するデジタル署名を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="59208-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="59208-106">この署名は、パッケージの実際の配信元にも完全性の認証情報を追加する X.509 証明書から生成されます。</span><span class="sxs-lookup"><span data-stu-id="59208-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="59208-107">署名付きパッケージは、最も強力なエンド ツー エンドの検証を提供します。</span><span class="sxs-lookup"><span data-stu-id="59208-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="59208-108">NuGet の署名の 2 つの異なる種類あります。</span><span class="sxs-lookup"><span data-stu-id="59208-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="59208-109">**署名の作成**です。</span><span class="sxs-lookup"><span data-stu-id="59208-109">**Author Signature**.</span></span> <span data-ttu-id="59208-110">作成者の署名は、作成者からいたとしても、パッケージを署名後に、パッケージが変更されていないことを保証どのリポジトリやトランスポートのパッケージを配信するメソッド。</span><span class="sxs-lookup"><span data-stu-id="59208-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="59208-111">さらに、パッケージの作成者署名は、署名証明書を事前に登録する必要があるために、nuget.org 発行パイプラインに、追加の認証メカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="59208-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="59208-112">詳細については、[証明書を登録](#register-certificate-on-nugetorg)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="59208-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="59208-113">**リポジトリの署名**します。</span><span class="sxs-lookup"><span data-stu-id="59208-113">**Repository Signature**.</span></span> <span data-ttu-id="59208-114">リポジトリの署名は、整合性の保証を提供します**すべて**場合でも、元のリポジトリがあった場所とは異なる場所から取得したこれらのパッケージは署名されたか、作成者かどうかをリポジトリにパッケージ化。署名されています。</span><span class="sxs-lookup"><span data-stu-id="59208-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="59208-115">作成者の署名付きパッケージの作成の詳細については、[パッケージの署名](../create-packages/Sign-a-package.md)と[記号の nuget コマンド](../tools/cli-ref-sign.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="59208-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="59208-116">Windows で nuget.exe を使用する場合にのみ、パッケージの署名はサポートされて現在します。</span><span class="sxs-lookup"><span data-stu-id="59208-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="59208-117">Windows で nuget.exe または Visual Studio を使用する場合にのみ、署名済みパッケージの検証は現在サポートされています。</span><span class="sxs-lookup"><span data-stu-id="59208-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="59208-118">証明書の要件</span><span class="sxs-lookup"><span data-stu-id="59208-118">Certificate requirements</span></span>

<span data-ttu-id="59208-119">署名証明書は、特殊な種類の有効な証明書は、コード パッケージに署名が必要です、`id-kp-codeSigning`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="59208-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="59208-120">さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。</span><span class="sxs-lookup"><span data-stu-id="59208-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="59208-121">タイムスタンプの要件</span><span class="sxs-lookup"><span data-stu-id="59208-121">Timestamp requirements</span></span>

<span data-ttu-id="59208-122">署名済みパッケージには、パッケージの署名証明書の有効期間を超えて署名検証するために、RFC 3161 タイムスタンプを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="59208-122">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="59208-123">タイムスタンプの署名に使用される証明書が有効である必要があります、`id-kp-timeStamping`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="59208-123">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="59208-124">さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。</span><span class="sxs-lookup"><span data-stu-id="59208-124">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="59208-125">技術的な詳細が記載されて、[パッケージの署名の技術的な仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="59208-125">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="59208-126">NuGet.org で署名の要件</span><span class="sxs-lookup"><span data-stu-id="59208-126">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="59208-127">nuget.org では、署名付きパッケージを受け入れるための追加の要件があります。</span><span class="sxs-lookup"><span data-stu-id="59208-127">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="59208-128">プライマリ署名は、作成者の署名である必要があります。</span><span class="sxs-lookup"><span data-stu-id="59208-128">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="59208-129">プライマリ署名には、1 つの有効なタイムスタンプが必要です。</span><span class="sxs-lookup"><span data-stu-id="59208-129">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="59208-130">作成者の署名とそのタイムスタンプの署名の両方の X.509 証明書:</span><span class="sxs-lookup"><span data-stu-id="59208-130">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="59208-131">2048 ビット RSA 公開キーが必要以上。</span><span class="sxs-lookup"><span data-stu-id="59208-131">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="59208-132">Nuget.org でパッケージの検証の時に現在の UTC 時刻ごとの有効期間内である必要があります。</span><span class="sxs-lookup"><span data-stu-id="59208-132">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="59208-133">Windows 上の既定で信頼されている信頼されたルート証明機関にチェーンする必要があります。</span><span class="sxs-lookup"><span data-stu-id="59208-133">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="59208-134">自己発行された証明書で署名されたパッケージは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="59208-134">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="59208-135">目的は、有効なはある必要があります。</span><span class="sxs-lookup"><span data-stu-id="59208-135">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="59208-136">署名証明書の作成者は、コード署名に対して有効である必要があります。</span><span class="sxs-lookup"><span data-stu-id="59208-136">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="59208-137">タイムスタンプ証明書は、タイムスタンプの有効なである必要があります。</span><span class="sxs-lookup"><span data-stu-id="59208-137">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="59208-138">署名時に失効いない必要があります。</span><span class="sxs-lookup"><span data-stu-id="59208-138">Must not be revoked at signing time.</span></span> <span data-ttu-id="59208-139">(この可能性がありますできません knowable 送信時に、nuget.org の失効状態を定期的に再チェックするため)。</span><span class="sxs-lookup"><span data-stu-id="59208-139">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="59208-140">関連記事</span><span class="sxs-lookup"><span data-stu-id="59208-140">Related articles</span></span>

- [<span data-ttu-id="59208-141">NuGet パッケージの署名</span><span class="sxs-lookup"><span data-stu-id="59208-141">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="59208-142">署名済みパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="59208-142">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
