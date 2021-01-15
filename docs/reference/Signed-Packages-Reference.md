---
title: 署名済みパッケージ
description: NuGet パッケージの署名の要件。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: ac9efadc1d29bec86ca9b7821d5587e0171613aa
ms.sourcegitcommit: 323a107c345c7cb4e344a6e6d8de42c63c5188b7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/15/2021
ms.locfileid: "98235712"
---
# <a name="signed-packages"></a><span data-ttu-id="e8723-103">署名付きパッケージ</span><span class="sxs-lookup"><span data-stu-id="e8723-103">Signed packages</span></span>

<span data-ttu-id="e8723-104">*NuGet 4.6.0 + および Visual Studio 2017 バージョン15.6 以降*</span><span class="sxs-lookup"><span data-stu-id="e8723-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="e8723-105">NuGet パッケージには、改ざんされたコンテンツからの保護を提供するデジタル署名を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="e8723-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="e8723-106">この署名は、x.509 証明書から生成されます。この証明書は、パッケージの実際の配信元に対しても信頼性のある校正を加えます。</span><span class="sxs-lookup"><span data-stu-id="e8723-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="e8723-107">署名付きパッケージは、最も強力なエンドツーエンドの検証を提供します。</span><span class="sxs-lookup"><span data-stu-id="e8723-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="e8723-108">NuGet 署名には、次の2種類があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="e8723-109">**署名を作成** します。</span><span class="sxs-lookup"><span data-stu-id="e8723-109">**Author signature**.</span></span> <span data-ttu-id="e8723-110">作成者の署名では、パッケージが署名された後にパッケージが変更されていないことが保証されます。これは、どのリポジトリまたはパッケージが配信されたかに関係なく行われます。</span><span class="sxs-lookup"><span data-stu-id="e8723-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="e8723-111">また、署名証明書を事前に登録する必要があるため、作成者に署名されたパッケージには、nuget.org 公開パイプラインに対する追加の認証メカニズムが用意されています。</span><span class="sxs-lookup"><span data-stu-id="e8723-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="e8723-112">詳細については、「 [証明書の登録](#signature-requirements-on-nugetorg)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e8723-112">For more information, see [Register certificates](#signature-requirements-on-nugetorg).</span></span>
- <span data-ttu-id="e8723-113">**リポジトリの署名**。</span><span class="sxs-lookup"><span data-stu-id="e8723-113">**Repository signature**.</span></span> <span data-ttu-id="e8723-114">リポジトリ署名は、署名された元のリポジトリとは別の場所からパッケージが取得された場合でも、リポジトリ内の **すべて** のパッケージに対して、署名が作成されたかどうかにかかわらず、整合性の保証を提供します。</span><span class="sxs-lookup"><span data-stu-id="e8723-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="e8723-115">作成者が署名したパッケージの作成の詳細については、「 [パッケージに署名](../create-packages/Sign-a-package.md) する」および「 [nuget sign コマンド](../reference/cli-reference/cli-ref-sign.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e8723-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../reference/cli-reference/cli-ref-sign.md).</span></span> <span data-ttu-id="e8723-116">[Dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify.md)コマンドまたは[nuget verify](../reference/cli-reference/cli-ref-verify.md)コマンドを使用して、パッケージの署名を確認できます。</span><span class="sxs-lookup"><span data-stu-id="e8723-116">You can verify packages' signatures using the [dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify.md) or [nuget verify](../reference/cli-reference/cli-ref-verify.md) commands.</span></span>

> [!Important]
> <span data-ttu-id="e8723-117">作成者署名パッケージは、現時点では Windows の nuget.exe でのみサポートされています。</span><span class="sxs-lookup"><span data-stu-id="e8723-117">Author signing packages is only supported by nuget.exe on Windows at this time.</span></span> <span data-ttu-id="e8723-118">ただし、nuget.org にアップロードされたすべてのパッケージは、自動的にリポジトリに署名されます。</span><span class="sxs-lookup"><span data-stu-id="e8723-118">However, all packages uploaded to nuget.org are automatically repository signed.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="e8723-119">証明書の要件</span><span class="sxs-lookup"><span data-stu-id="e8723-119">Certificate requirements</span></span>

<span data-ttu-id="e8723-120">パッケージの署名にはコード署名証明書が必要です。これは、 `id-kp-codeSigning` [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] の目的で有効な特別な種類の証明書です。</span><span class="sxs-lookup"><span data-stu-id="e8723-120">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="e8723-121">また、証明書の RSA 公開キーの長さは2048ビット以上である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-121">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="e8723-122">タイムスタンプの要件</span><span class="sxs-lookup"><span data-stu-id="e8723-122">Timestamp requirements</span></span>

<span data-ttu-id="e8723-123">署名されたパッケージには、パッケージ署名証明書の有効期間を超えて署名が有効であることを確認するために、RFC 3161 タイムスタンプを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-123">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="e8723-124">タイムスタンプの署名に使用する証明書は、 `id-kp-timeStamping` [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] の目的で有効である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-124">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="e8723-125">また、証明書の RSA 公開キーの長さは2048ビット以上である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-125">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="e8723-126">技術的な詳細については、「 [パッケージ署名技術仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="e8723-126">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="e8723-127">NuGet.org の署名の要件</span><span class="sxs-lookup"><span data-stu-id="e8723-127">Signature requirements on NuGet.org</span></span>

<span data-ttu-id="e8723-128">nuget.org には、署名付きパッケージを受け入れるための追加の要件があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-128">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="e8723-129">プライマリ署名は、作成者の署名である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-129">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="e8723-130">プライマリ署名には、有効なタイムスタンプが1つ含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-130">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="e8723-131">X.509 証明書は、作成者の署名とタイムスタンプの署名の両方に使用されます。</span><span class="sxs-lookup"><span data-stu-id="e8723-131">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="e8723-132">RSA 公開キー2048ビット以上である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-132">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="e8723-133">Nuget.org でのパッケージの検証時に、現在の UTC 時刻ごとに有効期間内である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-133">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="e8723-134">は、Windows で既定で信頼されている信頼されたルート証明機関にチェーンする必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-134">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="e8723-135">自己発行の証明書で署名されたパッケージは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="e8723-135">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="e8723-136">次の目的で有効である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-136">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="e8723-137">作成者の署名証明書は、コード署名に対して有効である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-137">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="e8723-138">タイムスタンプの証明書は有効である必要があります。</span><span class="sxs-lookup"><span data-stu-id="e8723-138">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="e8723-139">署名時に取り消すことはできません。</span><span class="sxs-lookup"><span data-stu-id="e8723-139">Must not be revoked at signing time.</span></span> <span data-ttu-id="e8723-140">(これは送信時に knowable されない場合があるため、nuget.org は定期的に失効状態を検査します)。</span><span class="sxs-lookup"><span data-stu-id="e8723-140">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>
  
  
## <a name="related-articles"></a><span data-ttu-id="e8723-141">関連記事</span><span class="sxs-lookup"><span data-stu-id="e8723-141">Related articles</span></span>

- [<span data-ttu-id="e8723-142">NuGet パッケージの署名</span><span class="sxs-lookup"><span data-stu-id="e8723-142">Signing NuGet Packages</span></span>](../create-packages/Sign-a-Package.md)
- [<span data-ttu-id="e8723-143">Dotnet CLI を使用して署名されたパッケージを検証する</span><span class="sxs-lookup"><span data-stu-id="e8723-143">Verify signed packages using the dotnet CLI</span></span>](/dotnet/core/tools/dotnet-nuget-verify.md)
- [<span data-ttu-id="e8723-144">nuget.exeを使用して署名されたパッケージを検証する </span><span class="sxs-lookup"><span data-stu-id="e8723-144">Verify signed packages using nuget.exe</span></span>](../reference/cli-reference/cli-ref-verify.md)
- [<span data-ttu-id="e8723-145">パッケージ信頼境界を管理する</span><span class="sxs-lookup"><span data-stu-id="e8723-145">Manage package trust boundaries</span></span>](../consume-packages/installing-signed-packages.md)
