---
title: 署名付きパッケージ
description: NuGet パッケージの署名の要件。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 72fb1a87c13160c53f632d2ef87a12a4e9bc02a3
ms.sourcegitcommit: 8127dd73ff8481a1a01acd9b7004dd131a9d84e7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/22/2018
---
# <a name="signed-packages"></a><span data-ttu-id="6761d-103">署名付きパッケージ</span><span class="sxs-lookup"><span data-stu-id="6761d-103">Signed packages</span></span>

<span data-ttu-id="6761d-104">*NuGet 4.6.0+ と Visual Studio 2017 15.6 およびそれ以降のバージョン*</span><span class="sxs-lookup"><span data-stu-id="6761d-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="6761d-105">NuGet パッケージは、改ざんされたコンテンツに対する保護を提供するデジタル署名を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="6761d-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="6761d-106">この署名は、パッケージの実際の原因にも信頼性実証を追加する X.509 証明書から生成されます。</span><span class="sxs-lookup"><span data-stu-id="6761d-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="6761d-107">署名付きパッケージは、最も強力なエンド ツー エンド検証を提供します。</span><span class="sxs-lookup"><span data-stu-id="6761d-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="6761d-108">作成者署名作成者かにかかわらずからパッケージを署名するために、パッケージが変更されていないことを保証するどのリポジトリ、またはどのようなトランスポート、パッケージが配信されるメソッド。</span><span class="sxs-lookup"><span data-stu-id="6761d-108">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="6761d-109">さらに、作成者によって署名されたパッケージは、署名証明書を事前登録する必要があるために、nuget.org 発行パイプラインに追加の認証メカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="6761d-109">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="6761d-110">詳細については、次を参照してください。[証明書を登録](#register-certificate-on-nugetorg)です。</span><span class="sxs-lookup"><span data-stu-id="6761d-110">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>

<span data-ttu-id="6761d-111">署名付きパッケージの作成の詳細については、「[パッケージの署名](../create-packages/Sign-a-package.md)と[nuget 記号コマンド](../tools/cli-ref-sign.md)です。</span><span class="sxs-lookup"><span data-stu-id="6761d-111">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="6761d-112">パッケージの署名は現在サポートされて windows nuget.exe を使用する場合のみです。</span><span class="sxs-lookup"><span data-stu-id="6761d-112">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="6761d-113">Windows で nuget.exe または Visual Studio を使用する場合にのみ、署名付きパッケージの検証は現在サポートされています。</span><span class="sxs-lookup"><span data-stu-id="6761d-113">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="6761d-114">証明書の要件</span><span class="sxs-lookup"><span data-stu-id="6761d-114">Certificate requirements</span></span>

<span data-ttu-id="6761d-115">パッケージの署名には、コード署名は特殊な種類の有効な証明書の証明書が必要です、`id-kp-codeSigning`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。</span><span class="sxs-lookup"><span data-stu-id="6761d-115">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="6761d-116">さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。</span><span class="sxs-lookup"><span data-stu-id="6761d-116">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="6761d-117">コード署名証明書の取得します。</span><span class="sxs-lookup"><span data-stu-id="6761d-117">Get a code signing certificate</span></span>

<span data-ttu-id="6761d-118">有効な証明書のような公共の証明機関から取得できます。</span><span class="sxs-lookup"><span data-stu-id="6761d-118">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="6761d-119">Symantec</span><span class="sxs-lookup"><span data-stu-id="6761d-119">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="6761d-120">DigiCert</span><span class="sxs-lookup"><span data-stu-id="6761d-120">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="6761d-121">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="6761d-121">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="6761d-122">グローバルのサインイン</span><span class="sxs-lookup"><span data-stu-id="6761d-122">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="6761d-123">Comodo</span><span class="sxs-lookup"><span data-stu-id="6761d-123">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="6761d-124">Certum</span><span class="sxs-lookup"><span data-stu-id="6761d-124">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="6761d-125">Windows によって信頼された証明機関の一覧から取得できます[ http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners)です。</span><span class="sxs-lookup"><span data-stu-id="6761d-125">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="6761d-126">テスト証明書を作成します。</span><span class="sxs-lookup"><span data-stu-id="6761d-126">Create a test certificate</span></span>

<span data-ttu-id="6761d-127">テスト目的で自己発行された証明書を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="6761d-127">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="6761d-128">自己発行の証明書を作成するには、 [New-selfsignedcertificate PowerShell コマンド](/powershell/module/pkiclient/new-selfsignedcertificate.md)です。</span><span class="sxs-lookup"><span data-stu-id="6761d-128">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

```ps
New-SelfSignedCertificate -Subject "CN=NuGet Test Developer, OU=Use for testing purposes ONLY" `
                          -FriendlyName "NuGetTestDeveloper" `
                          -Type CodeSigning `
                          -KeyUsage DigitalSignature `
                          -KeyLength 2048 `
                          -KeyAlgorithm RSA `
                          -HashAlgorithm SHA256 `
                          -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
                          -CertStoreLocation "Cert:\CurrentUser\My" 
```

<span data-ttu-id="6761d-129">このコマンドは、現在のユーザーの個人証明書ストアで利用可能なテスト証明書を作成します。</span><span class="sxs-lookup"><span data-stu-id="6761d-129">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="6761d-130">実行して、証明書ストアを開くことができます`certmgr.msc`を新しく作成された証明書を参照してください。</span><span class="sxs-lookup"><span data-stu-id="6761d-130">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="6761d-131">パッケージを受け付けない nuget.org 自己発行の証明書で署名します。</span><span class="sxs-lookup"><span data-stu-id="6761d-131">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="6761d-132">タイムスタンプの要件</span><span class="sxs-lookup"><span data-stu-id="6761d-132">Timestamp requirements</span></span>

<span data-ttu-id="6761d-133">署名付きパッケージには、パッケージの署名証明書の有効期間を超えて署名の有効性を確保する、RFC 3161 タイムスタンプを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="6761d-134">タイムスタンプの署名に使用する証明書を有効にする必要があります、`id-kp-timeStamping`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。</span><span class="sxs-lookup"><span data-stu-id="6761d-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="6761d-135">さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。</span><span class="sxs-lookup"><span data-stu-id="6761d-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="6761d-136">技術的な詳細は含まれて、[パッケージの署名の技術的な仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="6761d-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="6761d-137">Nuget.org の署名の要件</span><span class="sxs-lookup"><span data-stu-id="6761d-137">Signature requirements on nuget.org</span></span>

<span data-ttu-id="6761d-138">nuget.org には、署名付きパッケージを受け入れるための他の要件があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-138">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="6761d-139">プライマリ署名は、作成者署名をする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-139">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="6761d-140">プライマリ署名は、1 つの有効なタイムスタンプが必要です。</span><span class="sxs-lookup"><span data-stu-id="6761d-140">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="6761d-141">作成者のシグネチャとその署名のタイムスタンプの両方の X.509 証明書:</span><span class="sxs-lookup"><span data-stu-id="6761d-141">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="6761d-142">2048 ビット RSA パブリック キーが必要か値を超えています。</span><span class="sxs-lookup"><span data-stu-id="6761d-142">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="6761d-143">Nuget.org をパッケージの検証の時に現在の UTC 時刻ごとの有効期間内である必要があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-143">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="6761d-144">Windows では既定で信頼されている信頼されたルート機関にチェーンする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-144">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="6761d-145">自己発行された証明書で署名されたパッケージは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="6761d-145">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="6761d-146">目的は、有効なはする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-146">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="6761d-147">署名証明書の作成者は、コード署名の有効なである必要があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-147">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="6761d-148">タイムスタンプ証明書は、タイムスタンプの有効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-148">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="6761d-149">署名時刻に失効いない必要があります。</span><span class="sxs-lookup"><span data-stu-id="6761d-149">Must not be revoked at signing time.</span></span> <span data-ttu-id="6761d-150">(これではありません knowable の送信時に、nuget.org 失効状態を定期的に再チェックように) します。</span><span class="sxs-lookup"><span data-stu-id="6761d-150">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="6761d-151">Nuget.org の証明書を登録します。</span><span class="sxs-lookup"><span data-stu-id="6761d-151">Register certificate on nuget.org</span></span>

<span data-ttu-id="6761d-152">署名付きパッケージを送信するには、まず nuget.org に証明書を登録する必要があります。として証明書が必要な`.cer`バイナリ DER 形式のファイルです。</span><span class="sxs-lookup"><span data-stu-id="6761d-152">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="6761d-153">既存の証明書は、証明書のエクスポート ウィザードを使用してバイナリ DER 形式にエクスポートできます。</span><span class="sxs-lookup"><span data-stu-id="6761d-153">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![証明書のエクスポート ウィザード](media/CertificateExportWizard.png)

<span data-ttu-id="6761d-155">高度なユーザーを使用して、証明書をエクスポートすることができます、[証明書のエクスポートの PowerShell コマンド](/powershell/module/pkiclient/export-certificate.md)です。</span><span class="sxs-lookup"><span data-stu-id="6761d-155">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="6761d-156">に nuget.org を証明書を登録するには`Certificates`セクションで`Account settings`ページ (または、組織の設定 ページ) を選択して`Register new certificate`です。</span><span class="sxs-lookup"><span data-stu-id="6761d-156">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![証明書の登録](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="6761d-158">1 人のユーザーは、複数のユーザーによって登録できる複数の証明書と同じ証明書を送信できます。</span><span class="sxs-lookup"><span data-stu-id="6761d-158">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="6761d-159">ユーザーは、証明書登録されている、すべての将来のパッケージ送信**必要があります**証明書のいずれかで署名します。</span><span class="sxs-lookup"><span data-stu-id="6761d-159">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="6761d-160">ユーザーは、アカウントから登録された証明書を削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="6761d-160">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="6761d-161">証明書を削除すると、その証明書で署名されたパッケージの送信に失敗します。</span><span class="sxs-lookup"><span data-stu-id="6761d-161">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="6761d-162">既存のパッケージが影響を受けません。</span><span class="sxs-lookup"><span data-stu-id="6761d-162">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="6761d-163">パッケージの署名の要件を構成します。</span><span class="sxs-lookup"><span data-stu-id="6761d-163">Configure package signing requirements</span></span>

<span data-ttu-id="6761d-164">パッケージの唯一の所有者の場合は、必要な署名者としています。</span><span class="sxs-lookup"><span data-stu-id="6761d-164">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="6761d-165">つまり、nuget.org に送信し、パッケージの署名に登録されている証明書のいずれかを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="6761d-165">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="6761d-166">場合は、パッケージは、既定では複数の所有者を持つ、"Any"の所有者の証明書は、パッケージの署名に使用できます。</span><span class="sxs-lookup"><span data-stu-id="6761d-166">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="6761d-167">パッケージの共同所有者は、ユーザーが自分自身を"Any"または必要な署名者であるその他の任意の共同所有者をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="6761d-167">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="6761d-168">登録されている任意の証明書を持っていないユーザー所有者を行うと、署名がないパッケージが許可されます。</span><span class="sxs-lookup"><span data-stu-id="6761d-168">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="6761d-169">同様に、1 つの所有者が登録された証明書を持つパッケージと別の所有者の"Any"オプションが選択されている既定値は登録されている任意の証明書を持たない場合、nuget.org を受け入れるか、署名付きパッケージ所有者のいずれかで登録されているシグネチャを持つまたは符号なし (は、所有者のいずれかがある登録されている任意の証明書) をパッケージ化します。</span><span class="sxs-lookup"><span data-stu-id="6761d-169">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![パッケージの署名を構成します。](media/configure-package-signers.png)
