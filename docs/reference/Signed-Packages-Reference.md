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
ms.locfileid: "34449592"
---
# <a name="signed-packages"></a>署名付きパッケージ

*NuGet 4.6.0+ と Visual Studio 2017 15.6 およびそれ以降のバージョン*

NuGet パッケージは、改ざんされたコンテンツに対する保護を提供するデジタル署名を含めることができます。 この署名は、パッケージの実際の原因にも信頼性実証を追加する X.509 証明書から生成されます。

署名付きパッケージは、最も強力なエンド ツー エンド検証を提供します。 作成者署名作成者かにかかわらずからパッケージを署名するために、パッケージが変更されていないことを保証するどのリポジトリ、またはどのようなトランスポート、パッケージが配信されるメソッド。

さらに、作成者によって署名されたパッケージは、署名証明書を事前登録する必要があるために、nuget.org 発行パイプラインに追加の認証メカニズムを提供します。 詳細については、次を参照してください。[証明書を登録](#register-certificate-on-nugetorg)です。

署名付きパッケージの作成の詳細については、「[パッケージの署名](../create-packages/Sign-a-package.md)と[nuget 記号コマンド](../tools/cli-ref-sign.md)です。

> [!Important]
> パッケージの署名は現在サポートされて windows nuget.exe を使用する場合のみです。 Windows で nuget.exe または Visual Studio を使用する場合にのみ、署名付きパッケージの検証は現在サポートされています。

## <a name="certificate-requirements"></a>証明書の要件

パッケージの署名には、コード署名は特殊な種類の有効な証明書の証明書が必要です、`id-kp-codeSigning`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。 さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。

## <a name="get-a-code-signing-certificate"></a>コード署名証明書の取得します。

有効な証明書のような公共の証明機関から取得できます。

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [グローバルのサインイン](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Windows によって信頼された証明機関の一覧から取得できます[ http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners)です。

## <a name="create-a-test-certificate"></a>テスト証明書を作成します。

テスト目的で自己発行された証明書を使用することができます。 自己発行の証明書を作成するには、 [New-selfsignedcertificate PowerShell コマンド](/powershell/module/pkiclient/new-selfsignedcertificate.md)です。

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

このコマンドは、現在のユーザーの個人証明書ストアで利用可能なテスト証明書を作成します。 実行して、証明書ストアを開くことができます`certmgr.msc`を新しく作成された証明書を参照してください。

> [!Warning]
> パッケージを受け付けない nuget.org 自己発行の証明書で署名します。

## <a name="timestamp-requirements"></a>タイムスタンプの要件

署名付きパッケージには、パッケージの署名証明書の有効期間を超えて署名の有効性を確保する、RFC 3161 タイムスタンプを含める必要があります。 タイムスタンプの署名に使用する証明書を有効にする必要があります、`id-kp-timeStamping`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。 さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。

技術的な詳細は含まれて、[パッケージの署名の技術的な仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>Nuget.org の署名の要件

nuget.org には、署名付きパッケージを受け入れるための他の要件があります。

- プライマリ署名は、作成者署名をする必要があります。
- プライマリ署名は、1 つの有効なタイムスタンプが必要です。
- 作成者のシグネチャとその署名のタイムスタンプの両方の X.509 証明書:
  - 2048 ビット RSA パブリック キーが必要か値を超えています。
  - Nuget.org をパッケージの検証の時に現在の UTC 時刻ごとの有効期間内である必要があります。
  - Windows では既定で信頼されている信頼されたルート機関にチェーンする必要があります。 自己発行された証明書で署名されたパッケージは拒否されます。
  - 目的は、有効なはする必要があります。 
    - 署名証明書の作成者は、コード署名の有効なである必要があります。
    - タイムスタンプ証明書は、タイムスタンプの有効にする必要があります。
  - 署名時刻に失効いない必要があります。 (これではありません knowable の送信時に、nuget.org 失効状態を定期的に再チェックように) します。

## <a name="register-certificate-on-nugetorg"></a>Nuget.org の証明書を登録します。

署名付きパッケージを送信するには、まず nuget.org に証明書を登録する必要があります。として証明書が必要な`.cer`バイナリ DER 形式のファイルです。 既存の証明書は、証明書のエクスポート ウィザードを使用してバイナリ DER 形式にエクスポートできます。

![証明書のエクスポート ウィザード](media/CertificateExportWizard.png)

高度なユーザーを使用して、証明書をエクスポートすることができます、[証明書のエクスポートの PowerShell コマンド](/powershell/module/pkiclient/export-certificate.md)です。

に nuget.org を証明書を登録するには`Certificates`セクションで`Account settings`ページ (または、組織の設定 ページ) を選択して`Register new certificate`です。

![証明書の登録](media/registered-certs.png)

> [!Tip]
> 1 人のユーザーは、複数のユーザーによって登録できる複数の証明書と同じ証明書を送信できます。

ユーザーは、証明書登録されている、すべての将来のパッケージ送信**必要があります**証明書のいずれかで署名します。

ユーザーは、アカウントから登録された証明書を削除することもできます。 証明書を削除すると、その証明書で署名されたパッケージの送信に失敗します。 既存のパッケージが影響を受けません。

## <a name="configure-package-signing-requirements"></a>パッケージの署名の要件を構成します。

パッケージの唯一の所有者の場合は、必要な署名者としています。 つまり、nuget.org に送信し、パッケージの署名に登録されている証明書のいずれかを使用することができます。

場合は、パッケージは、既定では複数の所有者を持つ、"Any"の所有者の証明書は、パッケージの署名に使用できます。 パッケージの共同所有者は、ユーザーが自分自身を"Any"または必要な署名者であるその他の任意の共同所有者をオーバーライドできます。 登録されている任意の証明書を持っていないユーザー所有者を行うと、署名がないパッケージが許可されます。 

同様に、1 つの所有者が登録された証明書を持つパッケージと別の所有者の"Any"オプションが選択されている既定値は登録されている任意の証明書を持たない場合、nuget.org を受け入れるか、署名付きパッケージ所有者のいずれかで登録されているシグネチャを持つまたは符号なし (は、所有者のいずれかがある登録されている任意の証明書) をパッケージ化します。

![パッケージの署名を構成します。](media/configure-package-signers.png)
