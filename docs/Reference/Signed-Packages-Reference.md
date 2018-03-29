---
title: パッケージの参照を署名 |Microsoft ドキュメント
author: rido-min
ms.author: rido-min
manager: unniravindranathan
ms.date: 03/06/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: パッケージ機能の説明を署名します。
keywords: NuGet パッケージの署名、署名、証明書
ms.reviewer:
- ananguar
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: a2a338596f7d98ded11da6fb02bafba3521249ab
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="signed-packages"></a><span data-ttu-id="a755f-104">署名付きパッケージ</span><span class="sxs-lookup"><span data-stu-id="a755f-104">Signed packages</span></span>

<span data-ttu-id="a755f-105">*NuGet 4.6.0+ と Visual Studio 2017 15.6 およびそれ以降のバージョン*</span><span class="sxs-lookup"><span data-stu-id="a755f-105">*NuGet 4.6.0+ and Visual Studio 2017 version 15.6 and later*</span></span>

<span data-ttu-id="a755f-106">NuGet パッケージは、改ざんされたコンテンツに対する保護を提供するデジタル署名を含めることができます。</span><span class="sxs-lookup"><span data-stu-id="a755f-106">NuGet packages can include a digital signature that provides protection against tampered content.</span></span> <span data-ttu-id="a755f-107">この署名は、パッケージの実際の原因にも信頼性実証を追加する X.509 証明書から生成されます。</span><span class="sxs-lookup"><span data-stu-id="a755f-107">This signature is produced from an X.509 certificate that also adds authenticity proofs to the actual origin of the package.</span></span>

<span data-ttu-id="a755f-108">署名付きパッケージは、最も強力なエンド ツー エンド検証を提供します。</span><span class="sxs-lookup"><span data-stu-id="a755f-108">Signed packages provide the strongest end-to-end validation.</span></span> <span data-ttu-id="a755f-109">作成者署名作成者かにかかわらずからパッケージを署名するために、パッケージが変更されていないことを保証するどのリポジトリ、またはどのようなトランスポート、パッケージが配信されるメソッド。</span><span class="sxs-lookup"><span data-stu-id="a755f-109">An author signature guarantees that the package has not been modified since the author signed the package, no matter from which repository or what transport method the package is delivered.</span></span>

<span data-ttu-id="a755f-110">ロックダウン環境を必要とするコンシューマーは、特定の作成者の証明書で署名されたパッケージを要求できます。</span><span class="sxs-lookup"><span data-stu-id="a755f-110">Consumers who demand a locked-down environment can require packages signed with a specific author certificate.</span></span>

<span data-ttu-id="a755f-111">さらに、作成者によって署名されたパッケージは、署名証明書を事前登録する必要があるために、nuget.org 発行パイプラインに追加の認証メカニズムを提供します。</span><span class="sxs-lookup"><span data-stu-id="a755f-111">Additionally, author-signed packages provide an extra authentication mechanism to the nuget.org publishing pipeline because the signing certificate must be registered ahead of time.</span></span>

<span data-ttu-id="a755f-112">署名付きパッケージの作成の詳細については、「[パッケージの署名](../create-packages/Sign-a-package.md)と[nuget 記号コマンド](../tools/cli-ref-sign.md)です。</span><span class="sxs-lookup"><span data-stu-id="a755f-112">For details on creating a signed package, see [Signing Packages](../create-packages/Sign-a-package.md) and the [nuget sign command](../tools/cli-ref-sign.md).</span></span>

> [!Important]
> <span data-ttu-id="a755f-113">nuget.org 現在受け付けない署名付きパッケージ。</span><span class="sxs-lookup"><span data-stu-id="a755f-113">nuget.org does not presently accept signed packages.</span></span> <span data-ttu-id="a755f-114">カスタム フィードに公開する場合はパッケージに署名することができます。</span><span class="sxs-lookup"><span data-stu-id="a755f-114">You can sign packages for publishing to custom feeds.</span></span>

## <a name="certificate-requirements"></a><span data-ttu-id="a755f-115">証明書の要件</span><span class="sxs-lookup"><span data-stu-id="a755f-115">Certificate requirements</span></span>

<span data-ttu-id="a755f-116">パッケージの署名には、コード署名は特殊な種類の有効な証明書の証明書が必要です、`id-kp-codeSigning`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。</span><span class="sxs-lookup"><span data-stu-id="a755f-116">Package signing requires a code signing certificate, which is a special type of certificate that is valid for the `id-kp-codeSigning` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="a755f-117">さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。</span><span class="sxs-lookup"><span data-stu-id="a755f-117">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="a755f-118">コード署名証明書の取得します。</span><span class="sxs-lookup"><span data-stu-id="a755f-118">Get a code signing certificate</span></span>

<span data-ttu-id="a755f-119">有効な証明書のようにパブリック証明機関から取得できます。</span><span class="sxs-lookup"><span data-stu-id="a755f-119">Valid certificates may be obtained from public certificate authorities like:</span></span>

- [<span data-ttu-id="a755f-120">Symantec</span><span class="sxs-lookup"><span data-stu-id="a755f-120">Symantec</span></span>](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [<span data-ttu-id="a755f-121">DigiCert</span><span class="sxs-lookup"><span data-stu-id="a755f-121">DigiCert</span></span>](https://www.digicert.com/code-signing/)
- [<span data-ttu-id="a755f-122">Go Daddy</span><span class="sxs-lookup"><span data-stu-id="a755f-122">Go Daddy</span></span>](https://www.godaddy.com/web-security/code-signing-certificate)
- [<span data-ttu-id="a755f-123">グローバルのサインイン</span><span class="sxs-lookup"><span data-stu-id="a755f-123">Global Sign</span></span>](https://www.globalsign.com/en/code-signing-certificate/)
- [<span data-ttu-id="a755f-124">Comodo</span><span class="sxs-lookup"><span data-stu-id="a755f-124">Comodo</span></span>](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [<span data-ttu-id="a755f-125">Certum</span><span class="sxs-lookup"><span data-stu-id="a755f-125">Certum</span></span>](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

<span data-ttu-id="a755f-126">Windows によって信頼された証明機関の一覧から取得できます[ http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners)です。</span><span class="sxs-lookup"><span data-stu-id="a755f-126">The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="a755f-127">テスト証明書を作成します。</span><span class="sxs-lookup"><span data-stu-id="a755f-127">Create a test certificate</span></span>

<span data-ttu-id="a755f-128">テスト目的で自己発行された証明書を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="a755f-128">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="a755f-129">自己発行の証明書を作成するには、 [New-selfsignedcertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell コマンド。</span><span class="sxs-lookup"><span data-stu-id="a755f-129">To create a self-issued certificate, use the [New-SelfSignedCertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell command.</span></span>

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

<span data-ttu-id="a755f-130">このコマンドは、現在のユーザーの個人証明書ストアで利用可能なテスト証明書を作成します。</span><span class="sxs-lookup"><span data-stu-id="a755f-130">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="a755f-131">実行して、証明書ストアを開くことができます`certmgr.msc`を新しく作成された証明書を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a755f-131">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

## <a name="timestamp-requirements"></a><span data-ttu-id="a755f-132">タイムスタンプの要件</span><span class="sxs-lookup"><span data-stu-id="a755f-132">Timestamp requirements</span></span>

<span data-ttu-id="a755f-133">署名付きパッケージには、パッケージの署名証明書の有効期間を超えて署名の有効性を確保する、RFC 3161 タイムスタンプを含める必要があります。</span><span class="sxs-lookup"><span data-stu-id="a755f-133">Signed packages should include an RFC 3161 timestamp to ensure signature validity beyond the package signing certificate's validity period.</span></span> <span data-ttu-id="a755f-134">タイムスタンプの署名に使用する証明書を有効にする必要があります、`id-kp-timeStamping`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。</span><span class="sxs-lookup"><span data-stu-id="a755f-134">The certificate used to sign the timestamp must be valid for the `id-kp-timeStamping` purpose [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)].</span></span> <span data-ttu-id="a755f-135">さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。</span><span class="sxs-lookup"><span data-stu-id="a755f-135">Additionally, the certificate must have an RSA public key length of 2048 bits or higher.</span></span>

<span data-ttu-id="a755f-136">技術的な詳細は含まれて、[パッケージの署名の技術的な仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。</span><span class="sxs-lookup"><span data-stu-id="a755f-136">Additional technical details can be found in the [package signature technical specs](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub).</span></span>
