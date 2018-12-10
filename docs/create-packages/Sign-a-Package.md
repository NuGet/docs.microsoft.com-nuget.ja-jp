---
title: NuGet パッケージの署名
description: 署名済みパッケージを使用してコンテンツの整合性の検証を可能にする方法について説明します。
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: e8955f9d46bab235c8755d5654814a4291d542d6
ms.sourcegitcommit: 673e580ae749544a4a071b4efe7d42fd2bb6d209
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/06/2018
ms.locfileid: "52977564"
---
# <a name="signing-nuget-packages"></a><span data-ttu-id="b92d0-103">NuGet パッケージの署名</span><span class="sxs-lookup"><span data-stu-id="b92d0-103">Signing NuGet Packages</span></span>

<span data-ttu-id="b92d0-104">署名付きのパッケージは、コンテンツの整合性を検証し、コンテンツを改ざんから保護します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-104">Signed packages allows for content integrity verification checks which provides protection against content tampering.</span></span> <span data-ttu-id="b92d0-105">また、パッケージの署名は、パッケージの実際の発行元を示す唯一のソースであり、コンシューマー向けにパッケージの信頼性を強化します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-105">The package signature also serves as the single source of truth about the actual origin of the package and bolsters package authenticity for the consumer.</span></span> <span data-ttu-id="b92d0-106">このガイドは、既に[パッケージが作成](creating-a-package.md)済みであること前提にしています。</span><span class="sxs-lookup"><span data-stu-id="b92d0-106">This guide assumes you have already [created a package](creating-a-package.md).</span></span>

## <a name="get-a-code-signing-certificate"></a><span data-ttu-id="b92d0-107">コード署名証明書を取得する</span><span class="sxs-lookup"><span data-stu-id="b92d0-107">Get a code signing certificate</span></span>

<span data-ttu-id="b92d0-108">有効な証明書は、[Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)、[DigiCert](https://www.digicert.com/code-signing/)、[Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)、[Global Sign](https://www.globalsign.com/en/code-signing-certificate/)、[Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)、[Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) などの公的な証明機関から入手できます。Windows によって信頼される証明機関の全一覧は、[http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners) から入手できます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-108">Valid certificates may be obtained from a public certificate authority such as [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3), [DigiCert](https://www.digicert.com/code-signing/), [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate), [Global Sign](https://www.globalsign.com/en/code-signing-certificate/), [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php), [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml), etc. The complete list of certification authorities trusted by Windows can be obtained from [http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners).</span></span>

<span data-ttu-id="b92d0-109">テスト目的には、自己発行した証明書を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-109">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="b92d0-110">ただし、NuGet.org では自己発行した証明書で署名されたパッケージは許可されていません。詳細については、[テスト証明書の作成](#create-a-test-certificate)に関するページを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b92d0-110">However, packages signed using self-issued certificates are not accepted by NuGet.org. Learn more about [creating a test certificate](#create-a-test-certificate)</span></span>

## <a name="export-the-certificate-file"></a><span data-ttu-id="b92d0-111">証明書ファイルをエクスポートする</span><span class="sxs-lookup"><span data-stu-id="b92d0-111">Export the certificate file</span></span>

* <span data-ttu-id="b92d0-112">証明書のエクスポート ウィザードを使用すると、既存の証明書をバイナリ DER 形式にエクスポートできます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-112">You can export an existing certificate to a binary DER format by using the Certificate Export Wizard.</span></span>

  ![証明書のエクスポート ウィザード](../reference/media/CertificateExportWizard.png)

* <span data-ttu-id="b92d0-114">証明書は、[Export-Certificate の PowerShell コマンド](/powershell/module/pkiclient/export-certificate.md)を使用してもエクスポートできます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-114">You can also export the certificate using the [Export-Certificate PowerShell command](/powershell/module/pkiclient/export-certificate.md).</span></span>

## <a name="sign-the-package"></a><span data-ttu-id="b92d0-115">パッケージに署名する</span><span class="sxs-lookup"><span data-stu-id="b92d0-115">Sign the package</span></span>

> [!note]
> <span data-ttu-id="b92d0-116">nuget.exe 4.6.0 以降が必要です。</span><span class="sxs-lookup"><span data-stu-id="b92d0-116">Requires nuget.exe 4.6.0 or later</span></span>

<span data-ttu-id="b92d0-117">[nuget sign](../tools/cli-ref-sign.md) を使用してパッケージに署名するには、次を使用します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-117">Sign the package using [nuget sign](../tools/cli-ref-sign.md):</span></span>

```cli
nuget sign MyPackage.nupkg -CertificateFilePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

* <span data-ttu-id="b92d0-118">証明書には、証明書ストアで入手できるものを使用するか、ファイルの証明書を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-118">You can use a certificate available in the certificate store or use a certificate from a file.</span></span> <span data-ttu-id="b92d0-119">[nuget の sign](../tools/cli-ref-sign.md) の CLI リファレンスを参照してください。</span><span class="sxs-lookup"><span data-stu-id="b92d0-119">See CLI reference for [nuget sign](../tools/cli-ref-sign.md).</span></span>
* <span data-ttu-id="b92d0-120">署名証明書が期限切れになったときに署名の有効な状態を維持するには、署名済みパッケージにタイムスタンプが含まれている必要があります。</span><span class="sxs-lookup"><span data-stu-id="b92d0-120">Signed packages should include a timestamp to make sure the signature remains valid when the signing certificate has expired.</span></span> <span data-ttu-id="b92d0-121">そうでない場合は、署名操作で[警告](../reference/errors-and-warnings/NU3002.md)が生成されます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-121">Else the sign operation will produce a [warning](../reference/errors-and-warnings/NU3002.md).</span></span>
* <span data-ttu-id="b92d0-122">特定のパッケージの署名の詳細を表示するには、[nuget verify](../tools/cli-ref-verify.md) を使用します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-122">You can see the signature details of a given package using [nuget verify](../tools/cli-ref-verify.md).</span></span>

## <a name="register-the-certificate-on-nugetorg"></a><span data-ttu-id="b92d0-123">NuGet.org に証明書を登録する</span><span class="sxs-lookup"><span data-stu-id="b92d0-123">Register the certificate on NuGet.org</span></span>

<span data-ttu-id="b92d0-124">署名されたパッケージを発行するには、まず NuGet.org に証明書を登録する必要があります。この証明書は、DER 形式の `.cer` ファイルである必要があります。</span><span class="sxs-lookup"><span data-stu-id="b92d0-124">To publish a signed package, you must first register the certificate with NuGet.org. You need the certificate as a `.cer` file in a binary DER format.</span></span>

1. <span data-ttu-id="b92d0-125">NuGet.org に[サインイン](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-125">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>
1. <span data-ttu-id="b92d0-126">[`Account settings`] に移動します (または、証明書を組織アカウントで登録するには [`Manage Organization`] **>** [`Edit Organziation`] に移動します)。</span><span class="sxs-lookup"><span data-stu-id="b92d0-126">Go to `Account settings` (or `Manage Organization` **>** `Edit Organziation` if you would like to register the certificate with an Organization account).</span></span>
1. <span data-ttu-id="b92d0-127">[`Certificates`] セクションを展開し、[`Register new`] を選択します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-127">Expand the `Certificates` section and select `Register new`.</span></span>
1. <span data-ttu-id="b92d0-128">前にエクスポートした証明書ファイルを参照し選択します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-128">Browse and select the certficate file that was exported earlier.</span></span>
  <span data-ttu-id="b92d0-129">![登録済みの証明書](../reference/media/registered-certs.png)</span><span class="sxs-lookup"><span data-stu-id="b92d0-129">![Registered Certificates](../reference/media/registered-certs.png)</span></span>

<span data-ttu-id="b92d0-130">**注:**</span><span class="sxs-lookup"><span data-stu-id="b92d0-130">**Note**</span></span>
* <span data-ttu-id="b92d0-131">1 人のユーザーが複数の証明書を送信でき、複数のユーザーが同じ証明書を登録できます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-131">One user can submit multiple certificates and the same certificate can be registered by multiple users.</span></span>
* <span data-ttu-id="b92d0-132">ユーザーが証明書を登録した場合、以降送信されるすべてのパッケージはそのうちの 1 つの証明書で署名される**必要があります**。</span><span class="sxs-lookup"><span data-stu-id="b92d0-132">Once a user has a certificate registered, all future package submissions **must** be signed with one of the certificates.</span></span> <span data-ttu-id="b92d0-133">「[NuGet.org でパッケージの署名要件を管理する](#manage-signing-requirements-for-your-package-on-nugetorg)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b92d0-133">See [Manage signing requirements for your package on NuGet.org](#manage-signing-requirements-for-your-package-on-nugetorg)</span></span>
* <span data-ttu-id="b92d0-134">ユーザーはそのアカウントから登録済みの証明書を削除することもできます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-134">Users can also remove a registered certificate from the account.</span></span> <span data-ttu-id="b92d0-135">証明書を一度削除すると、その証明書を使用して署名された新しいパッケージの送信時に失敗します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-135">Once a certificate is removed, new packages signed with that certificate will fail at submission.</span></span> <span data-ttu-id="b92d0-136">既存のパッケージには影響はありません。</span><span class="sxs-lookup"><span data-stu-id="b92d0-136">Existing packages aren't affected.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="b92d0-137">パッケージを公開する</span><span class="sxs-lookup"><span data-stu-id="b92d0-137">Publish the package</span></span>

<span data-ttu-id="b92d0-138">これで NuGet.org にパッケージを公開する準備ができました。「[パッケージを公開する](Publish-a-package.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="b92d0-138">You are now ready to publish the package to NuGet.org. See [Publishing packages](Publish-a-package.md).</span></span>

## <a name="create-a-test-certificate"></a><span data-ttu-id="b92d0-139">テスト証明書を作成する</span><span class="sxs-lookup"><span data-stu-id="b92d0-139">Create a test certificate</span></span>

<span data-ttu-id="b92d0-140">テスト目的には、自己発行した証明書を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-140">You can use self-issued certificates for testing purposes.</span></span> <span data-ttu-id="b92d0-141">自己発行の証明書を作成するには、[New-SelfSignedCertificate PowerShell コマンド](/powershell/module/pkiclient/new-selfsignedcertificate.md)を使用します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-141">To create a self-issued certificate, use the [New-SelfSignedCertificate PowerShell command](/powershell/module/pkiclient/new-selfsignedcertificate.md).</span></span>

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

<span data-ttu-id="b92d0-142">このコマンドにより、現在のユーザーの個人の証明書ストアにテスト証明書が作成されます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-142">This command creates a testing certificate available in the current user's personal certificate store.</span></span> <span data-ttu-id="b92d0-143">新規に作成された証明書を参照するには、`certmgr.msc` を実行し、証明書ストアを開きます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-143">You can open the certificate store by running `certmgr.msc` to see the newly created certificate.</span></span>

> [!Warning]
> <span data-ttu-id="b92d0-144">NuGet.org では、自己発行した証明書で署名されたパッケージは許可されていません。</span><span class="sxs-lookup"><span data-stu-id="b92d0-144">NuGet.org does not accept packages signed with self-issued certificates.</span></span>

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a><span data-ttu-id="b92d0-145">NuGet.org でパッケージの署名要件を管理する</span><span class="sxs-lookup"><span data-stu-id="b92d0-145">Manage signing requirements for your package on NuGet.org</span></span>
1. <span data-ttu-id="b92d0-146">NuGet.org に[サインイン](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-146">[Sign in](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) to NuGet.org.</span></span>

1. <span data-ttu-id="b92d0-147">[`Manage Packages`] に移動します。 
   ![パッケージの署名者を構成する](../reference/media/configure-package-signers.png)</span><span class="sxs-lookup"><span data-stu-id="b92d0-147">Go to `Manage Packages` 
![Configure package signers](../reference/media/configure-package-signers.png)</span></span>

* <span data-ttu-id="b92d0-148">ご自分がパッケージの唯一の所有者である場合、ご自分で署名する必要があります。つまり、登録済みの任意の証明書を使用してパッケージに署名し、NuGet.org に公開します。</span><span class="sxs-lookup"><span data-stu-id="b92d0-148">If you are the sole owner of a package, you are the required signer i.e. you can use any of the registered certificates to sign and publish your packages to NuGet.org.</span></span>

* <span data-ttu-id="b92d0-149">パッケージの所有者が複数いる場合、パッケージの署名には既定で "すべて" の所有者の証明書を使用できます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-149">If a package has multiple owners, by default, "Any" owner's certificates can be used to sign the package.</span></span> <span data-ttu-id="b92d0-150">ご自分がパッケージの共同所有者である場合、必要な署名者として "すべて" を自分または他の任意の共同所有者でオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-150">As a co-owner of the package, you can override "Any" with yourself or any other co-owner to be the required signer.</span></span> <span data-ttu-id="b92d0-151">証明書の登録を行っていない所有者を作成した場合、署名付きでないパッケージが許可されます。</span><span class="sxs-lookup"><span data-stu-id="b92d0-151">If you make an owner  who does not have any certificate registered, then unsigned packages will be allowed.</span></span> 

* <span data-ttu-id="b92d0-152">同様に、証明書の登録を 1 人の所有者は行っており、別の所有者は行っていないパッケージで、既定の "すべて" オプションが選択されている場合、NuGet.org では、所有者の 1 人が登録した証明書が使用された署名付きパッケージまたは、署名付きでないパッケージのいずれかを許可します (これは、所有者のうちの 1 人が証明書の登録を行っていないためです)。</span><span class="sxs-lookup"><span data-stu-id="b92d0-152">Similarly, if the default "Any" option is selected for a package where one owner has a certificate registered and another owner does not have any certificate registered, then NuGet.org accepts either a signed package with a signature registered by one of its owners or an unsigned package (because one of the owners does not have any certificate registered).</span></span>

## <a name="related-articles"></a><span data-ttu-id="b92d0-153">関連記事</span><span class="sxs-lookup"><span data-stu-id="b92d0-153">Related articles</span></span>

- [<span data-ttu-id="b92d0-154">署名付きパッケージのインストール</span><span class="sxs-lookup"><span data-stu-id="b92d0-154">Installing signed packages</span></span>](../consume-packages/installing-signed-packages.md)
- [<span data-ttu-id="b92d0-155">署名済みパッケージの参照</span><span class="sxs-lookup"><span data-stu-id="b92d0-155">Signed Packages Reference</span></span>](../reference/Signed-Packages-Reference.md)
