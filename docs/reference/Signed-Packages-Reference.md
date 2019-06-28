---
title: 署名付きパッケージ
description: NuGet パッケージへの署名の要件。
author: rido-min
ms.author: rmpablos
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 952256a24246543ecd4c37285cd001622aa2bc46
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426172"
---
# <a name="signed-packages"></a>署名付きパッケージ

*NuGet 4.6.0+ と Visual Studio 2017 バージョン 15.6 以降*

NuGet パッケージには、改ざんされたコンテンツに対する保護を提供するデジタル署名を含めることができます。 この署名は、パッケージの実際の配信元にも完全性の認証情報を追加する X.509 証明書から生成されます。

署名付きパッケージは、最も強力なエンド ツー エンドの検証を提供します。 NuGet の署名の 2 つの異なる種類あります。
- **署名の作成**です。 作成者の署名は、作成者からいたとしても、パッケージを署名後に、パッケージが変更されていないことを保証どのリポジトリやトランスポートのパッケージを配信するメソッド。 さらに、パッケージの作成者署名は、署名証明書を事前に登録する必要があるために、nuget.org 発行パイプラインに、追加の認証メカニズムを提供します。 詳細については、次を参照してください。[証明書を登録](#signature-requirements-on-nugetorg)します。
- **リポジトリの署名**します。 リポジトリの署名は、整合性の保証を提供します**すべて**場合でも、元のリポジトリがあった場所とは異なる場所から取得したこれらのパッケージは署名されたか、作成者かどうかをリポジトリにパッケージ化。署名されています。   

作成者の署名付きパッケージの作成の詳細については、次を参照してください。[パッケージの署名](../create-packages/Sign-a-package.md)と[記号の nuget コマンド](../tools/cli-ref-sign.md)します。

> [!Important]
> Windows で nuget.exe を使用する場合にのみ、パッケージの署名はサポートされて現在します。 Windows で nuget.exe または Visual Studio を使用する場合にのみ、署名済みパッケージの検証は現在サポートされています。

## <a name="certificate-requirements"></a>証明書の要件

署名証明書は、特殊な種類の有効な証明書は、コード パッケージに署名が必要です、`id-kp-codeSigning`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。

## <a name="timestamp-requirements"></a>タイムスタンプの要件

署名済みパッケージには、パッケージの署名証明書の有効期間を超えて署名検証するために、RFC 3161 タイムスタンプを含める必要があります。 タイムスタンプの署名に使用される証明書が有効である必要があります、`id-kp-timeStamping`目的 [[RFC 5280 セクション 4.2.1.12](https://tools.ietf.org/html/rfc5280#section-4.2.1.12)]。 さらに、証明書には、RSA 公開キーの長さ 2048 ビット以上が必要です。

技術的な詳細が記載されて、[パッケージの署名の技術的な仕様](https://github.com/NuGet/Home/wiki/Package-Signatures-Technical-Details)(GitHub)。

## <a name="signature-requirements-on-nugetorg"></a>NuGet.org で署名の要件

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
  
  
## <a name="related-articles"></a>関連記事

- [NuGet パッケージの署名](../create-packages/Sign-a-Package.md)
- [信頼境界のパッケージを管理します。](../consume-packages/installing-signed-packages.md)
