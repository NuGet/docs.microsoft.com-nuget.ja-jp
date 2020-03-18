---
title: 署名済みパッケージ
description: NuGet パッケージの署名の要件。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 7384e8b30cb2ec5fe53ea0fe485858bc1f7b3c43
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428283"
---
# <a name="signed-packages"></a>署名付きパッケージ

*NuGet 4.6.0 + および Visual Studio 2017 バージョン15.6 以降*

NuGet パッケージには、改ざんされたコンテンツからの保護を提供するデジタル署名を含めることができます。 この署名は、x.509 証明書から生成されます。この証明書は、パッケージの実際の配信元に対しても信頼性のある校正を加えます。

署名付きパッケージは、最も強力なエンドツーエンドの検証を提供します。 NuGet 署名には、次の2種類があります。
- **署名を作成**します。 作成者の署名では、パッケージが署名された後にパッケージが変更されていないことが保証されます。これは、どのリポジトリまたはパッケージが配信されたかに関係なく行われます。 また、署名証明書を事前に登録する必要があるため、作成者に署名されたパッケージには、nuget.org 公開パイプラインに対する追加の認証メカニズムが用意されています。 詳細については、「[証明書の登録](#signature-requirements-on-nugetorg)」を参照してください。
- **リポジトリの署名**。 リポジトリ署名は、署名された元のリポジトリとは別の場所からパッケージが取得された場合でも、リポジトリ内の**すべて**のパッケージに対して、署名が作成されたかどうかにかかわらず、整合性の保証を提供します。   

作成者が署名したパッケージの作成の詳細については、「[パッケージに署名](../create-packages/Sign-a-package.md)する」および「 [nuget sign コマンド](../reference/cli-reference/cli-ref-sign.md)」を参照してください。

> [!Important]
> パッケージの署名は、現在 Windows で nuget.exe を使用している場合にのみサポートされます。 [署名付きパッケージの検証は、現在、Windows で nuget.exe または Visual Studio を使用している場合にのみサポートさ](../reference/cli-reference/cli-ref-verify.md)れます。

## <a name="certificate-requirements"></a>証明書の要件

パッケージに署名するには、コード署名証明書が必要です。これは、`id-kp-codeSigning` の目的で有効な特殊な種類の証明書である [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] です。 また、証明書の RSA 公開キーの長さは2048ビット以上である必要があります。

## <a name="timestamp-requirements"></a>タイムスタンプの要件

署名されたパッケージには、パッケージ署名証明書の有効期間を超えて署名が有効であることを確認するために、RFC 3161 タイムスタンプを含める必要があります。 タイムスタンプの署名に使用する証明書は、`id-kp-timeStamping` の目的で有効である必要があります [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 また、証明書の RSA 公開キーの長さは2048ビット以上である必要があります。

技術的な詳細については、「[パッケージ署名技術仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)」を参照してください。

## <a name="signature-requirements-on-nugetorg"></a>NuGet.org の署名の要件

nuget.org には、署名付きパッケージを受け入れるための追加の要件があります。

- プライマリ署名は、作成者の署名である必要があります。
- プライマリ署名には、有効なタイムスタンプが1つ含まれている必要があります。
- X.509 証明書は、作成者の署名とタイムスタンプの署名の両方に使用されます。
  - RSA 公開キー2048ビット以上である必要があります。
  - Nuget.org でのパッケージの検証時に、現在の UTC 時刻ごとに有効期間内である必要があります。
  - は、Windows で既定で信頼されている信頼されたルート証明機関にチェーンする必要があります。 自己発行の証明書で署名されたパッケージは拒否されます。
  - 次の目的で有効である必要があります。 
    - 作成者の署名証明書は、コード署名に対して有効である必要があります。
    - タイムスタンプの証明書は有効である必要があります。
  - 署名時に取り消すことはできません。 (これは送信時に knowable されない場合があるため、nuget.org は定期的に失効状態を検査します)。
  
  
## <a name="related-articles"></a>関連トピック

- [NuGet パッケージの署名](../create-packages/Sign-a-Package.md)
- [パッケージ信頼境界を管理する](../consume-packages/installing-signed-packages.md)
