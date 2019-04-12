---
title: リポジトリの署名、NuGet API |Microsoft Docs
author: joelverhagen
ms.author: jver
ms.date: 3/2/2018
ms.topic: reference
description: リポジトリのリソースの署名は、クライアントがパッケージ ソースにはリポジトリの署名機能をご案内できます。
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: ea318446c41a0d85d3fbf959dd38c929a0d0e9a1
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/11/2019
ms.locfileid: "59509023"
---
# <a name="repository-signatures"></a>リポジトリの署名

パッケージ ソースでは、公開済みのパッケージに追加するリポジトリの署名をサポートする場合をクライアントがパッケージ ソースで使用される署名証明書を判別できます。 このリソースは、パッケージが改ざんされてまたは予期しない署名証明書が、リポジトリが署名されているかどうかを検出するためにクライアントを許可します。

このリポジトリの署名情報を取得するために使用されるリソースは、`RepositorySignatures`リソースで見つかった、[サービス インデックス](service-index.md)します。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                | メモ
-------------------------- | -----
RepositorySignatures/4.7.0 | 最初のリリース
RepositorySignatures/4.9.0 | NuGet v4.9 + クライアントでサポートされています。
RepositorySignatures/5.0.0 | により、有効にする`allRepositorySigned`します。 NuGet v5.0 + クライアントでサポートされています。

## <a name="base-url"></a>[基本 URL]

次の api エントリ ポイントの URL の値である、`@id`前述のリソースに関連付けられたプロパティ`@type`値。 このトピックでは、プレース ホルダー URL を使用して`{@id}`します。

なお、その他のリソースとは異なり、 `{@id}` URL が HTTPS 経由で提供する必要です。

## <a name="http-methods"></a>HTTP メソッド

リポジトリの署名のリソースの HTTP のみのサポート メソッドで見つかったすべての Url`GET`と`HEAD`します。

## <a name="repository-signatures-index"></a>リポジトリの署名のインデックス

リポジトリの署名のインデックスには、2 つの情報が含まれています。

1. すべてのパッケージがソースで検出されたかどうかは、このパッケージ ソースで署名されたリポジトリです。
1. パッケージ ソースでパッケージの署名に使用される証明書の一覧。

ほとんどの場合は証明書の一覧にしか追加されます。 以前の署名証明書の有効期限が切れたパッケージ ソースが新しい署名証明書の使用を開始する必要がある場合は、一覧に新しい証明書を追加するは。 一覧から証明書を削除する場合、署名証明書の削除で作成されたすべてのパッケージの署名する必要がありますされなく有効と見なされる、クライアントによってを意味します。 この場合、パッケージの署名 (ただし、必ずしもパッケージ) が無効です。 クライアント ポリシーには、符号なしとしてパッケージをインストールすることができます。

証明書の失効 (例: キーの侵害) の場合は、影響を受ける証明書によって署名されたすべてのパッケージを再署名するパッケージ ソースが必要です。 さらに、パッケージ ソースでは、署名証明書のリストから影響を受けるの証明書を削除する必要があります。

次の要求は、リポジトリの署名のインデックスをフェッチします。

    GET {@id}

リポジトリ署名のインデックスは、次のプロパティを持つオブジェクトを含む JSON ドキュメントです。

名前                | 種類             | 必須 | メモ
------------------- | ---------------- | -------- | -----
allRepositorySigned | boolean          | 可      | 必要があります`false`4.7.0 と 4.9.0 リソース
signingCertificates | オブジェクトの配列 | 可      | 

`allRepositorySigned`パッケージ ソースの一部のパッケージ リポジトリの署名がない場合、ブール値が false に設定します。 ソースで説明されている署名証明書のいずれかによって生成されるリポジトリ シグネチャをいる必要があります、ブール値が true で入手できるすべてのパッケージに設定されている場合`signingCertificates`します。

> [!Warning]
> `allRepositorySigned`ブール 4.7.0 と 4.9.0 リソースに対して false である必要があります。 NuGet v4.7、v4.8、v4.9 クライアントがソースからパッケージをインストールできません`allRepositorySigned`を true に設定します。

内の 1 つまたは複数の署名証明書が必要があります、`signingCertificates`配列の場合、`allRepositorySigned`ブール値の設定を true にします。 配列が空の場合と`allRepositorySigned`に設定が true の場合、元のすべてのパッケージが無効と見なされるもクライアント ポリシーをパッケージの使用を許可可能性がありますがします。 この配列内の各要素は、次のプロパティを持つ JSON オブジェクトです。

名前         | 種類   | 必須 | メモ
------------ | ------ | -------- | -----
contentUrl   | string | 可      | DER でエンコードされた公開証明書への絶対 URL
指紋 | object | 可      |
件名      | string | 可      | 証明書からサブジェクト識別名
issuer       | string | 可      | 証明書の発行者の識別名
notBefore    | string | 可      | 証明書の有効期間の開始タイムスタンプ
notAfter     | string | 可      | 証明書の有効期間の終了のタイムスタンプ

なお、 `contentUrl` HTTPS 経由で提供するために必要です。 この URL は、特定の URL パターンがないので、このリポジトリの署名のインデックスのドキュメントを使用して動的に検出する必要があります。 

このオブジェクトのすべてのプロパティ (出てくる`contentUrl`) にある証明書から派生可能である必要があります`contentUrl`します。
これらの派生可能プロパティは、ラウンド トリップを最小限に抑えるに便利な機能として提供されます。

`fingerprints`オブジェクトは、次のプロパティ。

名前                   | 種類   | 必須 | メモ
---------------------- | ------ | -------- | -----
2.16.840.1.101.3.4.2.1 | string | 可      | SHA 256 フィンガー プリント

キー名`2.16.840.1.101.3.4.2.1`sha-256 ハッシュ アルゴリズムの oid。

すべてのハッシュ値は、ハッシュのダイジェストの小文字、16 進エンコードされた文字列形式にする必要があります。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-index/repository-signatures/index.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [repository-signatures-index.json](./_data/repository-signatures-index.json)]
