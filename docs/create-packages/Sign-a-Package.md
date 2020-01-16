---
title: NuGet パッケージの署名
description: 署名済みパッケージを使用してコンテンツの整合性の検証を可能にする方法について説明します。
author: rido-min
ms.author: rmpablos
ms.date: 03/06/2018
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 00fe1d5fa81132b5d6826203a0d26e56aa8d4755
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383983"
---
# <a name="signing-nuget-packages"></a>NuGet パッケージの署名

署名付きのパッケージは、コンテンツの整合性を検証し、コンテンツを改ざんから保護します。 また、パッケージの署名は、パッケージの実際の発行元を示す唯一のソースであり、コンシューマー向けにパッケージの信頼性を強化します。 このガイドは、既に[パッケージが作成](creating-a-package.md)済みであること前提にしています。

## <a name="get-a-code-signing-certificate"></a>コード署名証明書を取得する

有効な証明書は、[Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)、[DigiCert](https://www.digicert.com/code-signing/)、[Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)、[Global Sign](https://www.globalsign.com/en/code-signing-certificate/)、[Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)、[Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) などの公的な証明機関から入手できます。Windows によって信頼される証明機関の全一覧は、[http://aka.ms/trustcertpartners](https://aka.ms/trustcertpartners) から入手できます。

テスト目的には、自己発行した証明書を使用できます。 ただし、NuGet.org では自己発行した証明書で署名されたパッケージは許可されていません。詳細については、[テスト証明書の作成](#create-a-test-certificate)に関するページを参照してください。

## <a name="export-the-certificate-file"></a>証明書ファイルをエクスポートする

* 証明書のエクスポート ウィザードを使用すると、既存の証明書をバイナリ DER 形式にエクスポートできます。

  ![証明書のエクスポート ウィザード](../reference/media/CertificateExportWizard.png)

* 証明書は、[Export-Certificate の PowerShell コマンド](/powershell/module/pkiclient/export-certificate)を使用してもエクスポートできます。

## <a name="sign-the-package"></a>パッケージに署名する

> [!note]
> nuget.exe 4.6.0 以降が必要です。 dotnet.exe のサポートは近日提供予定です - [#7939](https://github.com/NuGet/Home/issues/7939)

[nuget sign](../reference/cli-reference/cli-ref-sign.md) を使用してパッケージに署名するには、次を使用します。

```cli
nuget sign MyPackage.nupkg -CertificatePath <PathToTheCertificate> -Timestamper <TimestampServiceURL>
```

> [!Tip]
> 証明書プロバイダーから、上記の省略可能な引数 `Timestamper` に使用できるタイムスタンプ サーバーの URL が提供されることがよくあります。 プロバイダーのドキュメントを参照するか、そのサービスの URL のサポートに問い合わせてください。

* 証明書には、証明書ストアで入手できるものを使用するか、ファイルの証明書を使用できます。 [nuget の sign](../reference/cli-reference/cli-ref-sign.md) の CLI リファレンスを参照してください。
* 署名証明書が期限切れになったときに署名の有効な状態を維持するには、署名済みパッケージにタイムスタンプが含まれている必要があります。 そうでない場合は、署名操作で[警告](../reference/errors-and-warnings/NU3002.md)が生成されます。
* 特定のパッケージの署名の詳細を表示するには、[nuget verify](../reference/cli-reference/cli-ref-verify.md) を使用します。

## <a name="register-the-certificate-on-nugetorg"></a>NuGet.org に証明書を登録する

署名されたパッケージを発行するには、まず NuGet.org に証明書を登録する必要があります。この証明書は、DER 形式の `.cer` ファイルである必要があります。

1. NuGet.org に[サインイン](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。
1. [`Account settings`] に移動します (または、証明書を組織アカウントで登録するには [`Manage Organization`] **>** [`Edit Organziation`] に移動します)。
1. [`Certificates`] セクションを展開し、[`Register new`] を選択します。
1. 前にエクスポートした証明書ファイルを参照し選択します。
  ![登録済みの証明書](../reference/media/registered-certs.png)

**注:**
* 1 人のユーザーが複数の証明書を送信でき、複数のユーザーが同じ証明書を登録できます。
* ユーザーが証明書を登録した場合、以降送信されるすべてのパッケージはそのうちの 1 つの証明書で署名される**必要があります**。 「[NuGet.org でパッケージの署名要件を管理する](#manage-signing-requirements-for-your-package-on-nugetorg)」を参照してください。
* ユーザーはそのアカウントから登録済みの証明書を削除することもできます。 証明書を一度削除すると、その証明書を使用して署名された新しいパッケージの送信時に失敗します。 既存のパッケージには影響はありません。

## <a name="publish-the-package"></a>パッケージを公開する

これで NuGet.org にパッケージを公開する準備ができました。「[パッケージを公開する](../nuget-org/Publish-a-package.md)」を参照してください。

## <a name="create-a-test-certificate"></a>テスト証明書を作成する

テスト目的には、自己発行した証明書を使用できます。 自己発行の証明書を作成するには、[New-SelfSignedCertificate PowerShell コマンド](/powershell/module/pkiclient/new-selfsignedcertificate)を使用します。

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

このコマンドにより、現在のユーザーの個人の証明書ストアにテスト証明書が作成されます。 新規に作成された証明書を参照するには、`certmgr.msc` を実行し、証明書ストアを開きます。

> [!Warning]
> NuGet.org では、自己発行した証明書で署名されたパッケージは許可されていません。

## <a name="manage-signing-requirements-for-your-package-on-nugetorg"></a>NuGet.org でパッケージの署名要件を管理する
1. NuGet.org に[サインイン](https://www.nuget.org/users/account/LogOn?returnUrl=%2F)します。

1. [`Manage Packages`] に移動します。 
   ![パッケージの署名者を構成する](../reference/media/configure-package-signers.png)

* ご自分がパッケージの唯一の所有者である場合、ご自分で署名する必要があります。つまり、登録済みの任意の証明書を使用してパッケージに署名し、NuGet.org に公開します。

* パッケージの所有者が複数いる場合、パッケージの署名には既定で "すべて" の所有者の証明書を使用できます。 ご自分がパッケージの共同所有者である場合、必要な署名者として "すべて" を自分または他の任意の共同所有者でオーバーライドできます。 証明書の登録を行っていない所有者を作成した場合、署名付きでないパッケージが許可されます。 

* 同様に、証明書の登録を 1 人の所有者は行っており、別の所有者は行っていないパッケージで、既定の "すべて" オプションが選択されている場合、NuGet.org では、所有者の 1 人が登録した証明書が使用された署名付きパッケージまたは、署名付きでないパッケージのいずれかを許可します (これは、所有者のうちの 1 人が証明書の登録を行っていないためです)。

## <a name="related-articles"></a>関連記事

- [パッケージ信頼境界を管理する](../consume-packages/installing-signed-packages.md)
- [署名済みパッケージの参照](../reference/Signed-Packages-Reference.md)
