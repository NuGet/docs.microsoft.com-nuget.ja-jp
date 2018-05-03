---
title: NuGet パッケージの参照の署名
description: NuGet パッケージの署名の要件。
author: rido-min
ms.author: rido-min
manager: unnir
ms.date: 04/24/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 751a8ff14bdc3a647985da4f908ad1a0fd0def9a
ms.sourcegitcommit: 5fcd6d664749aa720359104ef7a66d38aeecadc2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/27/2018
---
# <a name="signed-packages"></a>署名付きパッケージ

*NuGet 4.6.0+ と Visual Studio 2017 15.6 およびそれ以降のバージョン*

NuGet パッケージは、改ざんされたコンテンツに対する保護を提供するデジタル署名を含めることができます。 この署名は、パッケージの実際の原因にも信頼性実証を追加する X.509 証明書から生成されます。

署名付きパッケージは、最も強力なエンド ツー エンド検証を提供します。 作成者署名作成者かにかかわらずからパッケージを署名するために、パッケージが変更されていないことを保証するどのリポジトリ、またはどのようなトランスポート、パッケージが配信されるメソッド。

ロックダウン環境を必要とするコンシューマーは、特定の作成者の証明書で署名されたパッケージを要求できます。

さらに、作成者によって署名されたパッケージは、署名証明書を事前登録する必要があるために、nuget.org 発行パイプラインに追加の認証メカニズムを提供します。

署名付きパッケージの作成の詳細については、「[パッケージの署名](../create-packages/Sign-a-package.md)と[nuget 記号コマンド](../tools/cli-ref-sign.md)です。

> [!Important]
> nuget.org 現在受け付けない署名付きパッケージ。 カスタム フィードに公開する場合はパッケージに署名することができます。

> [!Important]
> パッケージの署名は現在サポートされて windows nuget.exe を使用する場合のみです。 Windows で nuget.exe または Visual Studio を使用する場合にのみ、署名付きパッケージの検証は現在サポートされています。

## <a name="certificate-requirements"></a>証明書の要件

パッケージの署名には、コード署名は特殊な種類の有効な証明書の証明書が必要です、`id-kp-codeSigning`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。 さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。

## <a name="get-a-code-signing-certificate"></a>コード署名証明書の取得します。

有効な証明書のようにパブリック証明機関から取得できます。

- [Symantec](https://trustcenter.websecurity.symantec.com/process/trust/productOptions?productType=SoftwareValidationClass3)
- [DigiCert](https://www.digicert.com/code-signing/)
- [Go Daddy](https://www.godaddy.com/web-security/code-signing-certificate)
- [グローバルのサインイン](https://www.globalsign.com/en/code-signing-certificate/)
- [Comodo](https://www.comodo.com/e-commerce/code-signing/code-signing-certificate.php)
- [Certum](https://www.certum.eu/certum/cert,offer_en_open_source_cs.xml) 

Windows によって信頼された証明機関の一覧から取得できます[ http://aka.ms/trustcertpartners](http://aka.ms/trustcertpartners)です。

## <a name="create-a-test-certificate"></a>テスト証明書を作成します。

テスト目的で自己発行された証明書を使用することができます。 自己発行の証明書を作成するには、 [New-selfsignedcertificate](https://docs.microsoft.com/en-us/powershell/module/pkiclient/new-selfsignedcertificate) PowerShell コマンド。

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

## <a name="timestamp-requirements"></a>タイムスタンプの要件

署名付きパッケージには、パッケージの署名証明書の有効期間を超えて署名の有効性を確保する、RFC 3161 タイムスタンプを含める必要があります。 タイムスタンプの署名に使用する証明書を有効にする必要があります、`id-kp-timeStamping`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。 さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。

技術的な詳細は含まれて、[パッケージの署名の技術的な仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。
