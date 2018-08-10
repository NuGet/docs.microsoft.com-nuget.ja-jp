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
# <a name="signed-packages"></a>署名済みパッケージ

*NuGet 4.6.0+ と Visual Studio 2017 バージョン 15.6 以降*

NuGet パッケージには、改ざんされたコンテンツに対する保護を提供するデジタル署名を含めることができます。 この署名は、パッケージの実際の配信元にも完全性の認証情報を追加する X.509 証明書から生成されます。

署名付きパッケージは、最も強力なエンド ツー エンドの検証を提供します。 NuGet の署名の 2 つの異なる種類あります。
- **署名の作成**です。 作成者の署名は、作成者からいたとしても、パッケージを署名後に、パッケージが変更されていないことを保証どのリポジトリやトランスポートのパッケージを配信するメソッド。 さらに、パッケージの作成者署名は、署名証明書を事前に登録する必要があるために、nuget.org 発行パイプラインに、追加の認証メカニズムを提供します。 詳細については、次を参照してください。[証明書を登録](#register-certificate-on-nugetorg)します。
- **リポジトリの署名**します。 リポジトリの署名は、整合性の保証を提供します**すべて**場合でも、元のリポジトリがあった場所とは異なる場所から取得したこれらのパッケージは署名されたか、作成者かどうかをリポジトリにパッケージ化。署名されています。   

作成者の署名付きパッケージの作成の詳細については、次を参照してください。[パッケージの署名](../create-packages/Sign-a-package.md)と[記号の nuget コマンド](../tools/cli-ref-sign.md)します。

> [!Important]
> Windows で nuget.exe を使用する場合にのみ、パッケージの署名はサポートされて現在します。 Windows で nuget.exe または Visual Studio を使用する場合にのみ、署名済みパッケージの検証は現在サポートされています。

## <a name="certificate-requirements"></a>証明書の要件

署名証明書は、特殊な種類の有効な証明書は、コード パッケージに署名が必要です、`id-kp-codeSigning`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。

## <a name="get-a-code-signing-certificate"></a>コード署名証明書を取得します。

有効な証明書などの公的証明機関から入手できます。

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [グローバルのサインイン](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Windows によって信頼された証明機関の一覧から取得できます[ http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners)します。

## <a name="create-a-test-certificate"></a>テスト証明書を作成します。

テスト目的で自己発行の証明書を使用することができます。 自己発行の証明書を作成するには、使用、 [New-selfsignedcertificate PowerShell コマンド](/powershell/module/pkiclient/new-selfsignedcertificate.md)します。

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

このコマンドは、現在のユーザーの個人証明書ストアで使用可能なテスト証明書を作成します。 実行して、証明書ストアを開くことができます`certmgr.msc`を新しく作成された証明書を参照してください。

> [!Warning]
> nuget.org には、パッケージは受け入れません。 自己発行された証明書で署名します。

## <a name="timestamp-requirements"></a>タイムスタンプの要件

署名済みパッケージには、パッケージの署名証明書の有効期間を超えて署名検証するために、RFC 3161 タイムスタンプを含める必要があります。 タイムスタンプの署名に使用される証明書が有効である必要があります、`id-kp-timeStamping`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。

技術的な詳細が記載されて、[パッケージの署名の技術的な仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>Nuget.org で署名の要件

nuget.org では、署名付きパッケージを受け入れるための追加の要件があります。

- プライマリ署名は、作成者の署名である必要があります。
- プライマリ署名には、1 つの有効なタイムスタンプが必要です。
- 作成者の署名とそのタイムスタンプの署名の両方の X.509 証明書:
  - 2048 ビット RSA 公開キーが必要以上。
  - Nuget.org でパッケージの検証の時に現在の UTC 時刻ごとの有効期間内である必要があります。
  - Windows 上の既定で信頼されている信頼されたルート証明機関にチェーンする必要があります。 自己発行された証明書で署名されたパッケージは拒否されます。
  - 目的は、有効なはある必要があります。 
    - 署名証明書の作成者は、コード署名に対して有効である必要があります。
    - タイムスタンプ証明書は、タイムスタンプの有効なである必要があります。
  - 署名時に失効いない必要があります。 (この可能性がありますできません knowable 送信時に、nuget.org の失効状態を定期的に再チェックするため)。

## <a name="register-certificate-on-nugetorg"></a>Nuget.org での証明書を登録します。

署名付きパッケージを送信するには、まず nuget.org で、証明書を登録する必要があります。としての証明書を作成する必要があります、`.cer`を DER 形式でバイナリ ファイル。 証明書のエクスポート ウィザードを使用して、DER バイナリ形式を既存の証明書をエクスポートできます。

![証明書のエクスポート ウィザード](media/CertificateExportWizard.png)

高度なユーザーを使用して、証明書をエクスポートすることができます、[証明書のエクスポート PowerShell コマンド](/powershell/module/pkiclient/export-certificate.md)します。

Nuget.org で、証明書を登録するには`Certificates`セクションで`Account settings`ページ (または、組織の設定 ページ) を選択して`Register new certificate`します。

![証明書の登録](media/registered-certs.png)

> [!Tip]
> 1 人のユーザーは、複数のユーザーが複数の証明書と同じ証明書を登録することができますを送信できます。

ユーザーは、証明書登録されると、将来のパッケージのすべての要求送信**する必要があります**証明書のいずれかで署名します。

ユーザーは、アカウントから登録済みの証明書を削除することもできます。 証明書が削除されると、その証明書で署名されたパッケージは、送信に失敗します。 既存のパッケージが影響を受けません。

## <a name="configure-package-signing-requirements"></a>パッケージの署名の要件を構成します。

パッケージの唯一の所有者の場合は、必要な署名者がいます。 パッケージに署名し、nuget.org に送信する登録済みの証明書のいずれかを使用することができます。

既定では、複数の所有者にパッケージされている場合、パッケージに署名する"Any"の所有者の証明書を使用できます。 パッケージの共同所有者は、"Any"を自分でまたは必要な署名者を他の共同所有者をオーバーライドできます。 登録されている任意の証明書を持っていないユーザーを所有者を行うと、署名がないパッケージが許可されます。 

同様に、"Any"オプションを選択する 1 つの所有者が登録された証明書を持つパッケージと別の所有者の既定値は登録されている任意の証明書を持たない場合、nuget.org を受け入れるか、署名付きパッケージ所有者のいずれかによって登録されているシグネチャを持つか、符号なし (登録されている任意の証明書の所有者のいずれかの必要はありません) のためにパッケージ化します。

![パッケージの署名者を構成します。](media/configure-package-signers.png)
