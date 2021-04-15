---
title: 署名済みパッケージ
description: NuGet パッケージの署名の要件。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 85fdf7a41cc033d92bbd0326648142aec27a9970
ms.sourcegitcommit: 1462f9f42ae36b3c990762ad4f02e38ab799ad09
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/15/2021
ms.locfileid: "107508801"
---
# <a name="signed-packages"></a>署名付きパッケージ

*NuGet 4.6.0 + および Visual Studio 2017 バージョン15.6 以降*

NuGet パッケージには、改ざんされたコンテンツからの保護を提供するデジタル署名を含めることができます。 この署名は、x.509 証明書から生成されます。この証明書は、パッケージの実際の配信元に対しても信頼性のある校正を加えます。

署名付きパッケージは、最も強力なエンドツーエンドの検証を提供します。 NuGet 署名には、次の2種類があります。
- **署名を作成** します。 作成者の署名では、パッケージが署名された後にパッケージが変更されていないことが保証されます。これは、どのリポジトリまたはパッケージが配信されたかに関係なく行われます。 また、署名証明書を事前に登録する必要があるため、作成者に署名されたパッケージには、nuget.org 公開パイプラインに対する追加の認証メカニズムが用意されています。 詳細については、「 [証明書の登録](#signature-requirements-on-nugetorg)」を参照してください。
- **リポジトリの署名**。 リポジトリ署名は、署名された元のリポジトリとは別の場所からパッケージが取得された場合でも、リポジトリ内の **すべて** のパッケージに対して、署名が作成されたかどうかにかかわらず、整合性の保証を提供します。   

作成者が署名したパッケージの作成の詳細については、「 [パッケージに署名](../create-packages/Sign-a-package.md) する」および「 [nuget sign コマンド](../reference/cli-reference/cli-ref-sign.md)」を参照してください。 [Dotnet nuget verify](/dotnet/core/tools/dotnet-nuget-verify)コマンドまたは[nuget verify](../reference/cli-reference/cli-ref-verify.md)コマンドを使用して、パッケージの署名を確認できます。

> [!Important]
> 作成者署名パッケージは、現時点では Windows の nuget.exe でのみサポートされています。 ただし、nuget.org にアップロードされたすべてのパッケージは、自動的にリポジトリに署名されます。

## <a name="certificate-requirements"></a>証明書の要件

パッケージの署名にはコード署名証明書が必要です。これは、 `id-kp-codeSigning` [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] の目的で有効な特別な種類の証明書です。 また、証明書の RSA 公開キーの長さは2048ビット以上である必要があります。

## <a name="timestamp-requirements"></a>タイムスタンプの要件

署名されたパッケージには、パッケージ署名証明書の有効期間を超えて署名が有効であることを確認するために、RFC 3161 タイムスタンプを含める必要があります。 タイムスタンプの署名に使用する証明書は、 `id-kp-timeStamping` [[RFC 5280 section 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)] の目的で有効である必要があります。 また、証明書の RSA 公開キーの長さは2048ビット以上である必要があります。

技術的な詳細については、「 [パッケージ署名技術仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details) (GitHub)」を参照してください。

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
  
  
## <a name="related-articles"></a>関連記事

- [NuGet パッケージの署名](../create-packages/Sign-a-Package.md)
- [Dotnet CLI を使用して署名されたパッケージを検証する](/dotnet/core/tools/dotnet-nuget-verify)
- [nuget.exeを使用して署名されたパッケージを検証する ](../reference/cli-reference/cli-ref-verify.md)
- [パッケージ信頼境界を管理する](../consume-packages/installing-signed-packages.md)
