---
title: NuGet API、サービスのインデックス
description: サービス インデックスは、NuGet HTTP API のエントリ ポイントであり、サーバーの機能を列挙します。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1dcfb87690b728280b494d4434f9c1d7ee7a7e74
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324722"
---
# <a name="service-index"></a>サービス インデックス

サービスのインデックスは、NuGet パッケージのソースのエントリ ポイントは、パッケージ ソースの機能を確認するクライアント実装できるようにする JSON ドキュメントです。 サービスのインデックスは、2 つの必要なプロパティを持つ JSON オブジェクト: `version` (サービス インデックスのスキーマのバージョン) と`resources`(エンドポイントまたはパッケージ ソースの機能)。

nuget.org のサービスのインデックス位置にある`https://api.nuget.org/v3/index.json`します。

## <a name="versioning"></a>バージョン管理

`version`値は、サービスのインデックスのスキーマ バージョンを示す SemVer 2.0.0 解析可能なバージョン文字列。 API のバージョン文字列でのメジャー バージョン番号を持つことが定められて`3`します。 サービス インデックス スキーマには、互換性に影響しない変更が行われるため、バージョン文字列のマイナー バージョンが高くなります。

サービス インデックス内の各リソースはサービス インデックス スキーマのバージョンとは独立してバージョン管理します。

現在のスキーマ バージョンは`3.0.0`します。 `3.0.0`バージョンは機能的には、古い`3.0.0-beta.1`バージョンが安定した、定義されたスキーマをより明確と通信する際に優先する必要があります。

## <a name="http-methods"></a>HTTP メソッド

サービスのインデックスは、HTTP メソッドを使用してアクセスできる`GET`と`HEAD`します。

## <a name="resources"></a>リソース

`resources`プロパティには、このパッケージ ソースでサポートされているリソースの配列が含まれます。

### <a name="resource"></a>リソース

リソース内のオブジェクトとは、`resources`配列。 パッケージ ソースのバージョン管理機能を表します。 リソースには、次のプロパティがあります。

名前          | 種類   | 必須 | メモ
------------- | ------ | -------- | -----
@id           | string | 可      | リソースへの URL
@type         | string | 可      | リソースの種類を表す文字列定数
comment       | string | Ｘ       | リソースの人間の判読できる説明

`@id`は URL を絶対である必要があるあり、いずれかをする必要がありますが、HTTP または HTTPS スキーマです。

`@type`リソースと対話するときに使用する特定のプロトコルを識別するために使用します。 リソースの種類は不透明な文字列が、一般に、形式があります。

    {RESOURCE_NAME}/{RESOURCE_VERSION}

クライアントがハード コードする必要があります、`@type`を理解し、パッケージ ソースのサービス インデックスで検索する値。 正確な`@type`で記載されている個々 のリソースの参照をドキュメントに現在使用中の値が列挙されます、 [API の概要](overview.md#resources-and-schema)します。

ため、このドキュメントでは、さまざまなリソースに関するドキュメントは基本的には別にグループ化、`{RESOURCE_NAME}`シナリオでグループ化に似ているサービス インデックス内に存在します。 

各リソースを一意にする必要はありません`@id`または`@type`します。 他より優先するリソースを識別するクライアント実装の責任です。 1 つの考えられる実装されるリソースと同じ、または互換性の`@type`接続障害やサーバー エラーが発生した場合、ラウンド ロビン方式で使用できます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [service-index.json](./_data/service-index.json)]
