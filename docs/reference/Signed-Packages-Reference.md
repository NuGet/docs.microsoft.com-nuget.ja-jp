---
title: 署名付きパッケージ
description: NuGet パッケージへの署名の要件。
author: rido-min
ms.author: rmpablos
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 992097281e21cd8cf37edf67fb1968b70c2b359b
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020517"
---
# <a name="signed-packages"></a><span data-ttu-id="264c4-103">署名済みパッケージ</span><span class="sxs-lookup"><span data-stu-id="264c4-103">Signed packages</span></span>

<span data-ttu-id="264c4-104">*NuGet 4.6.0+ と Visual Studio 2017 バージョン 15.6 以降*</span><span class="sxs-lookup"><span data-stu-id="264c4-104">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="264c4-105">NuGet パッケージには、改ざんされたコンテンツに対する保護を提供するデジタル署名を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="264c4-105">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="264c4-106">この署名は、パッケージの実際の配信元にも完全性の認証情報を追加する X.509 証明書から生成されます。</span><span class="sxs-lookup"><span data-stu-id="264c4-106">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="264c4-107">署名付きパッケージは、最も強力なエンド ツー エンドの検証を提供します。</span><span class="sxs-lookup"><span data-stu-id="264c4-107">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="264c4-108">NuGet の署名の 2 つの異なる種類あります。</span><span class="sxs-lookup"><span data-stu-id="264c4-108">There are two different types of NuGet signatures:</span></span>
- <span data-ttu-id="264c4-109">**署名の作成**です。</span><span class="sxs-lookup"><span data-stu-id="264c4-109">**Author Signature**.</span></span> <span data-ttu-id="264c4-110">作成者の署名は、作成者からいたとしても、パッケージを署名後に、パッケージが変更されていないことを保証どのリポジトリやトランスポートのパッケージを配信するメソッド。</span><span class="sxs-lookup"><span data-stu-id="264c4-110">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span> <span data-ttu-id="264c4-111">さらに、パッケージの作成者署名は、署名証明書を事前に登録する必要があるために、nuget.org 発行パイプラインに、追加の認証メカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="264c4-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span> <span data-ttu-id="264c4-112">詳細については、次を参照してください。[証明書を登録](#register-certificate-on-nugetorg)します。</span><span class="sxs-lookup"><span data-stu-id="264c4-112">For more information, see [Register certificates](#register-certificate-on-nugetorg).</span></span>
- <span data-ttu-id="264c4-113">**リポジトリの署名**します。</span><span class="sxs-lookup"><span data-stu-id="264c4-113">**Repository Signature**.</span></span> <span data-ttu-id="264c4-114">リポジトリの署名は、整合性の保証を提供します**すべて**場合でも、元のリポジトリがあった場所とは異なる場所から取得したこれらのパッケージは署名されたか、作成者かどうかをリポジトリにパッケージ化。署名されています。</span><span class="sxs-lookup"><span data-stu-id="264c4-114">Repository signatures provide an integrity guarantee for **all** packages in a repository whether they are author signed or not, even if those packages are obtained from a different location than the original repository where they were signed.</span></span>   

<span data-ttu-id="264c4-115">作成者の署名付きパッケージの作成の詳細については、次を参照してください。[パッケージの署名](../create-packages/Sign-a-package.md)と[記号の nuget コマンド](../tools/cli-ref-sign.md)します。</span><span class="sxs-lookup"><span data-stu-id="264c4-115">For details on creating an author signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="264c4-116">Windows で nuget.exe を使用する場合にのみ、パッケージの署名はサポートされて現在します。</span><span class="sxs-lookup"><span data-stu-id="264c4-116">Package signing is currently supported only when using nuget.exe on Windows.</span></span> <span data-ttu-id="264c4-117">Windows で nuget.exe または Visual Studio を使用する場合にのみ、署名済みパッケージの検証は現在サポートされています。</span><span class="sxs-lookup"><span data-stu-id="264c4-117">Verification of signed packages is currently supported only when using nuget.exe or Visual Studio on Windows.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="264c4-118">証明書の要件</span><span class="sxs-lookup"><span data-stu-id="264c4-118">Certificate requirements</span></span>

<span data-ttu-id="264c4-119">署名証明書は、特殊な種類の有効な証明書は、コード パッケージに署名が必要です、`id-kp-codeSigning`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="264c4-119">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="264c4-120">さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。</span><span class="sxs-lookup"><span data-stu-id="264c4-120">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="264c4-121">コード署名証明書を取得します。</span><span class="sxs-lookup"><span data-stu-id="264c4-121">Get a code signing certificate</span></span>

<span data-ttu-id="264c4-122">有効な証明書などの公的証明機関から入手できます。</span><span class="sxs-lookup"><span data-stu-id="264c4-122">Valid certificates may be obtained from a public certificate authority like:</span></span>

- [<span data-ttu-id="264c4-123">Symantec</span><span class="sxs-lookup"><span data-stu-id="264c4-123">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="264c4-124">DigiCert</span><span class="sxs-lookup"><span data-stu-id="264c4-124">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="264c4-125">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="264c4-125">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="264c4-126">グローバルのサインイン</span><span class="sxs-lookup"><span data-stu-id="264c4-126">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="264c4-127">Comodo</span><span class="sxs-lookup"><span data-stu-id="264c4-127">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="264c4-128">Certum</span><span class="sxs-lookup"><span data-stu-id="264c4-128">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="264c4-129">Windows によって信頼された証明機関の一覧から取得できます[ http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners)します。</span><span class="sxs-lookup"><span data-stu-id="264c4-129">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="264c4-130">テスト証明書を作成します。</span><span class="sxs-lookup"><span data-stu-id="264c4-130">Create a test certificate</span></span>

<span data-ttu-id="264c4-131">テスト目的で自己発行の証明書を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="264c4-131">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="264c4-132">自己発行の証明書を作成するには、使用、 [New-selfsignedcertificate PowerShell コマンド](/powershell/module/pkiclient/new-selfsignedcertificate.md)します。</span><span class="sxs-lookup"><span data-stu-id="264c4-132">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="264c4-133">このコマンドは、現在のユーザーの個人証明書ストアで使用可能なテスト証明書を作成します。</span><span class="sxs-lookup"><span data-stu-id="264c4-133">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="264c4-134">実行して、証明書ストアを開くことができます`certmgr.msc`を新しく作成された証明書を参照してください。</span><span class="sxs-lookup"><span data-stu-id="264c4-134">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="264c4-135">nuget.org には、パッケージは受け入れません。 自己発行された証明書で署名します。</span><span class="sxs-lookup"><span data-stu-id="264c4-135">nuget.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="264c4-136">タイムスタンプの要件</span><span class="sxs-lookup"><span data-stu-id="264c4-136">Timestamp requirements</span></span>

<span data-ttu-id="264c4-137">署名済みパッケージには、パッケージの署名証明書の有効期間を超えて署名検証するために、RFC 3161 タイムスタンプを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-137">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="264c4-138">タイムスタンプの署名に使用される証明書が有効である必要があります、`id-kp-timeStamping`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。</span><span class="sxs-lookup"><span data-stu-id="264c4-138">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="264c4-139">さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。</span><span class="sxs-lookup"><span data-stu-id="264c4-139">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="264c4-140">技術的な詳細が記載されて、[パッケージの署名の技術的な仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="264c4-140">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>

## <a name="signature-requirements-on-nugetorg"></a><span data-ttu-id="264c4-141">Nuget.org で署名の要件</span><span class="sxs-lookup"><span data-stu-id="264c4-141">Signature requirements on nuget.org</span></span>

<span data-ttu-id="264c4-142">nuget.org では、署名付きパッケージを受け入れるための追加の要件があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-142">nuget.org has additional requirements for accepting a signed package:</span></span>

- <span data-ttu-id="264c4-143">プライマリ署名は、作成者の署名である必要があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-143">The primary signature must be an author signature.</span></span>
- <span data-ttu-id="264c4-144">プライマリ署名には、1 つの有効なタイムスタンプが必要です。</span><span class="sxs-lookup"><span data-stu-id="264c4-144">The primary signature must have a single valid timestamp.</span></span>
- <span data-ttu-id="264c4-145">作成者の署名とそのタイムスタンプの署名の両方の X.509 証明書:</span><span class="sxs-lookup"><span data-stu-id="264c4-145">The X.509 certificates for both the author signature and its timestamp signature:</span></span>
  - <span data-ttu-id="264c4-146">2048 ビット RSA 公開キーが必要以上。</span><span class="sxs-lookup"><span data-stu-id="264c4-146">Must have an RSA public key 2048 bits or greater.</span></span>
  - <span data-ttu-id="264c4-147">Nuget.org でパッケージの検証の時に現在の UTC 時刻ごとの有効期間内である必要があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-147">Must be within its validity period per current UTC time at time of package validation on nuget.org.</span></span>
  - <span data-ttu-id="264c4-148">Windows 上の既定で信頼されている信頼されたルート証明機関にチェーンする必要があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-148">Must chain to a trusted root authority that is trusted by default on Windows.</span></span> <span data-ttu-id="264c4-149">自己発行された証明書で署名されたパッケージは拒否されます。</span><span class="sxs-lookup"><span data-stu-id="264c4-149">Packages signed with self-issued certificates are rejected.</span></span>
  - <span data-ttu-id="264c4-150">目的は、有効なはある必要があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-150">Must be valid for its purpose:</span></span> 
    - <span data-ttu-id="264c4-151">署名証明書の作成者は、コード署名に対して有効である必要があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-151">The author signing certificate must be valid for code signing.</span></span>
    - <span data-ttu-id="264c4-152">タイムスタンプ証明書は、タイムスタンプの有効なである必要があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-152">The timestamp certificate must be valid for timestamping.</span></span>
  - <span data-ttu-id="264c4-153">署名時に失効いない必要があります。</span><span class="sxs-lookup"><span data-stu-id="264c4-153">Must not be revoked at signing time.</span></span> <span data-ttu-id="264c4-154">(この可能性がありますできません knowable 送信時に、nuget.org の失効状態を定期的に再チェックするため)。</span><span class="sxs-lookup"><span data-stu-id="264c4-154">(This may not be knowable at submission time, so nuget.org periodically rechecks revocation status).</span></span>

## <a name="register-certificate-on-nugetorg"></a><span data-ttu-id="264c4-155">Nuget.org での証明書を登録します。</span><span class="sxs-lookup"><span data-stu-id="264c4-155">Register certificate on nuget.org</span></span>

<span data-ttu-id="264c4-156">署名付きパッケージを送信するには、まず nuget.org で、証明書を登録する必要があります。としての証明書を作成する必要があります、`.cer`を DER 形式でバイナリ ファイル。</span><span class="sxs-lookup"><span data-stu-id="264c4-156">To submit a signed package, you must first register the certificate with nuget.org. You need the certificate as a `.cer` file in a binary DER format.</span></span> <span data-ttu-id="264c4-157">証明書のエクスポート ウィザードを使用して、DER バイナリ形式を既存の証明書をエクスポートできます。</span><span class="sxs-lookup"><span data-stu-id="264c4-157">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

![証明書のエクスポート ウィザード](media/CertificateExportWizard.png)

<span data-ttu-id="264c4-159">高度なユーザーを使用して、証明書をエクスポートすることができます、[証明書のエクスポート PowerShell コマンド](/powershell/module/pkiclient/export-certificate.md)します。</span><span class="sxs-lookup"><span data-stu-id="264c4-159">Advanced users can export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

<span data-ttu-id="264c4-160">Nuget.org で、証明書を登録するには`Certificates`セクションで`Account settings`ページ (または、組織の設定 ページ) を選択して`Register new certificate`します。</span><span class="sxs-lookup"><span data-stu-id="264c4-160">To register the certificate with nuget.org, go to `Certificates` section on `Account settings` page (or the Organization's settings page) and select `Register new certificate`.</span></span>

![証明書の登録](media/registered-certs.png)

> [!Tip]
> <span data-ttu-id="264c4-162">1 人のユーザーは、複数のユーザーが複数の証明書と同じ証明書を登録することができますを送信できます。</span><span class="sxs-lookup"><span data-stu-id="264c4-162">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>

<span data-ttu-id="264c4-163">ユーザーは、証明書登録されると、将来のパッケージのすべての要求送信**する必要があります**証明書のいずれかで署名します。</span><span class="sxs-lookup"><span data-stu-id="264c4-163">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span>

<span data-ttu-id="264c4-164">ユーザーは、アカウントから登録済みの証明書を削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="264c4-164">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="264c4-165">証明書が削除されると、その証明書で署名されたパッケージは、送信に失敗します。</span><span class="sxs-lookup"><span data-stu-id="264c4-165">Once a certificate is removed, packages signed with that certificate fail at submission.</span></span> <span data-ttu-id="264c4-166">既存のパッケージが影響を受けません。</span><span class="sxs-lookup"><span data-stu-id="264c4-166">Existing packages aren't affected.</span></span>

## <a name="configure-package-signing-requirements"></a><span data-ttu-id="264c4-167">パッケージの署名の要件を構成します。</span><span class="sxs-lookup"><span data-stu-id="264c4-167">Configure package signing requirements</span></span>

<span data-ttu-id="264c4-168">パッケージの唯一の所有者の場合は、必要な署名者がいます。</span><span class="sxs-lookup"><span data-stu-id="264c4-168">If you are the sole owner of a package, you are the required signer.</span></span> <span data-ttu-id="264c4-169">パッケージに署名し、nuget.org に送信する登録済みの証明書のいずれかを使用することができます。</span><span class="sxs-lookup"><span data-stu-id="264c4-169">That is, you can use any of the registered certificates to sign your packages and submit to nuget.org.</span></span>

<span data-ttu-id="264c4-170">既定では、複数の所有者にパッケージされている場合、パッケージに署名する"Any"の所有者の証明書を使用できます。</span><span class="sxs-lookup"><span data-stu-id="264c4-170">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="264c4-171">パッケージの共同所有者は、"Any"を自分でまたは必要な署名者を他の共同所有者をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="264c4-171">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="264c4-172">登録されている任意の証明書を持っていないユーザーを所有者を行うと、署名がないパッケージが許可されます。</span><span class="sxs-lookup"><span data-stu-id="264c4-172">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

<span data-ttu-id="264c4-173">同様に、"Any"オプションを選択する 1 つの所有者が登録された証明書を持つパッケージと別の所有者の既定値は登録されている任意の証明書を持たない場合、nuget.org を受け入れるか、署名付きパッケージ所有者のいずれかによって登録されているシグネチャを持つか、符号なし (登録されている任意の証明書の所有者のいずれかの必要はありません) のためにパッケージ化します。</span><span class="sxs-lookup"><span data-stu-id="264c4-173">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then nuget.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

![パッケージの署名者を構成します。](media/configure-package-signers.png)
