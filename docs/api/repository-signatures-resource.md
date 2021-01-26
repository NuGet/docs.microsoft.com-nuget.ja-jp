---
title: リポジトリシグネチャ、NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: リポジトリ署名リソースを使用すると、クライアントパッケージソースはリポジトリ署名機能を発表できます。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: bfdbbb3a11de3be3f2258a3a289c0188740cdfce
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775339"
---
# <a name="repository-signatures"></a>リポジトリの署名

パッケージソースが、公開されたパッケージへのリポジトリ署名の追加をサポートしている場合は、パッケージソースによって使用される署名証明書をクライアントが判断することができます。 このリソースを使用すると、クライアントは、リポジトリの署名付きパッケージが改ざんされているか、または予期しない署名証明書を持っているかを検出できます。

このリポジトリの署名情報を取得するために使用されるリソースは、 `RepositorySignatures` [サービスインデックス](service-index.md)で検出されたリソースです。

## <a name="versioning"></a>バージョン管理

次の `@type` 値が使用されます。

@type 値                | Notes
-------------------------- | -----
RepositorySignatures/4.7.0 | 最初のリリース
RepositorySignatures/4.9.0- | NuGet v. 4.9 以降のクライアントでサポートされています
RepositorySignatures/5.0.0 | を有効に `allRepositorySigned` します。 NuGet v1.0 以降のクライアントでサポートされています

## <a name="base-url"></a>ベース URL

次の Api のエントリポイント URL は、 `@id` 前述のリソース値に関連付けられているプロパティの値です `@type` 。 このトピックでは、プレースホルダー URL を使用 `{@id}` します。

他のリソースとは異なり、 `{@id}` URL は HTTPS 経由で提供する必要があることに注意してください。

## <a name="http-methods"></a>HTTP メソッド

リポジトリ署名リソースで見つかったすべての Url は、HTTP メソッドとだけをサポートし `GET` `HEAD` ます。

## <a name="repository-signatures-index"></a>リポジトリシグネチャのインデックス

リポジトリシグネチャのインデックスには、次の2つの情報が含まれています。

1. ソースで見つかったすべてのパッケージが、このパッケージソースによって署名されたリポジトリであるかどうか。
1. パッケージに署名するためにパッケージソースによって使用される証明書の一覧。

ほとんどの場合、証明書の一覧はのみに追加されます。 以前の署名証明書の有効期限が切れ、パッケージソースが新しい署名証明書を使用して開始する必要がある場合に、新しい証明書が一覧に追加されます。 証明書が一覧から削除された場合は、削除された署名証明書で作成されたすべてのパッケージ署名がクライアントによって有効と見なされなくなります。 この場合、パッケージの署名は無効です (ただし、必ずしもパッケージではありません)。 クライアントポリシーでは、パッケージを署名なしとしてインストールできます。

証明書の失効 (キーの侵害など) の場合、パッケージソースは、影響を受けた証明書によって署名されたすべてのパッケージを再署名する必要があります。 また、パッケージソースによって、影響を受けた証明書が署名証明書の一覧から削除されます。

次の要求は、リポジトリ署名インデックスをフェッチします。

```
GET {@id}
```

リポジトリシグネチャインデックスは、次のプロパティを持つオブジェクトを含む JSON ドキュメントです。

名前                | Type             | 必須 | Notes
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | はい      | `false`4.7.0 および 4.9.0-リソース上にある必要があります
signingCertificates 書 | オブジェクトの配列 | はい      | 

`allRepositorySigned`パッケージソースにリポジトリ署名のないパッケージが含まれている場合、ブール値は false に設定されます。 ブール値が true に設定されている場合、ソースで使用できるすべてのパッケージには、「」で説明されているいずれかの署名証明書によって生成されたリポジトリ署名が必要 `signingCertificates` です。

> [!Warning]
> `allRepositorySigned`4.7.0 と 4.9.0-のリソースでは、ブール値を false にする必要があります。 NuGet v1.0、4.8、および v2.0 クライアントでは、が true に設定されているソースからパッケージをインストールすることはできません `allRepositorySigned` 。

`signingCertificates` `allRepositorySigned` ブール値が true に設定されている場合、配列には1つ以上の署名証明書が必要です。 配列が空で、が true に設定されている場合は、 `allRepositorySigned` ソースのすべてのパッケージが無効と見なされます。ただし、クライアントポリシーでは引き続きパッケージの使用が許可される場合があります。 この配列の各要素は、次のプロパティを持つ JSON オブジェクトです。

名前         | Type   | 必須 | Notes
------------ | ------ | -------- | -----
contentUrl   | string | はい      | DER でエンコードされた公開証明書への絶対 URL
行っ | object | はい      |
subject      | string | はい      | 証明書のサブジェクト識別名
発行者       | string | はい      | 証明書の発行者の識別名
notBefore    | string | はい      | 証明書の有効期間の開始タイムスタンプ
notAfter     | string | はい      | 証明書の有効期間の終了タイムスタンプ

を HTTPS 経由で提供する必要があることに注意して `contentUrl` ください。 この URL には特定の URL パターンがないため、このリポジトリ署名インデックスドキュメントを使用して動的に検出する必要があります。 

このオブジェクトのすべてのプロパティ (を除く `contentUrl` ) は、で見つかった証明書の派生である必要があり `contentUrl` ます。
これらの派生プロパティは、ラウンドトリップを最小限に抑えるために便利です。

`fingerprints` オブジェクトには、次のプロパティがあります。

名前                   | Type   | 必須 | Notes
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | はい      | SHA-256 フィンガープリント

キー名 `2.16.840.1.101.3.4.2.1` は、SHA-256 ハッシュアルゴリズムの OID です。

すべてのハッシュ値は、小文字でエンコードされたハッシュダイジェストの文字列形式である必要があります。

### <a name="sample-request"></a>要求のサンプル

```
GET https://api.nuget.org/v3-index/repository-signatures/index.json
```

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
