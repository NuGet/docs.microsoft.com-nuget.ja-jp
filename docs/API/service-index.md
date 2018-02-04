---
title: "サービス インデックスでは、NuGet API |Microsoft ドキュメント"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "サービス インデックスは、NuGet HTTP API のエントリ ポイントであり、サーバーの機能を列挙します。"
keywords: "NuGet API エントリ ポイント、NuGetA PI エンドポイントの検出"
ms.reviewer:
- karann
- unnir
ms.openlocfilehash: 9d0bb421c163520df4a1f0e9f3f71aab823aace3
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="service-index"></a>サービスのインデックス

サービス インデックスは、NuGet パッケージのソースのエントリ ポイントであり、パッケージ ソースの機能を検出するクライアントの実装は、ある JSON ドキュメントです。 サービス インデックスは、次の 2 つの必須プロパティを持つ JSON オブジェクト: `version` (サービスのインデックスのスキーマ バージョン) と`resources`(エンドポイントまたはパッケージ ソースの機能)。

nuget.org のサービスのインデックスにある`https://api.nuget.org/v3/index.json`です。

## <a name="versioning"></a>バージョン管理

`version`値は、サービスのインデックスのスキーマ バージョンを示す SemVer 2.0.0 解析可能なバージョン文字列。
この API でのメジャー バージョン番号をバージョン文字列であることが必須で`3`です。 サービス インデックス スキーマに重要ではない変更が加えられると、バージョン文字列のマイナー バージョンが増加します。

サービス インデックス内の各リソースはサービス インデックス スキーマのバージョンから独立してバージョン管理されたです。

現在のスキーマのバージョンが`3.0.0-beta.1`です。

## <a name="http-methods"></a>HTTP メソッド

サービス インデックスは、HTTP メソッドを使用してアクセス`GET`と`HEAD`です。

## <a name="resources"></a>リソース

`resources`プロパティには、このパッケージ ソースでサポートされているリソースの配列が含まれています。

### <a name="resource"></a>リソース

リソース内のオブジェクトとは、`resources`配列。 これは、パッケージ ソースのバージョン管理機能を表します。 リソースには、次のプロパティがあります。

name          | 種類   | 必須 | メモ
------------- | ------ | -------- | -----
@id           | string | 可      | リソースへの URL
@type         | string | 可      | リソースの種類を表す文字列定数
コメント       | string | Ｘ       | リソースの人間の判読できる説明

`@id`が HTTP または HTTPS スキーマには、URL を絶対にする必要があるあり、かする必要があります。

`@type`リソースと対話するときに使用する特定のプロトコルを識別するために使用します。 リソースの種類は不透明な文字列が、一般に、形式があります。

    {RESOURCE_NAME}/{RESOURCE_VERSION}

クライアントはハード コードとして予想される、`@type`を理解し、パッケージ ソースのサービスのインデックスで検索する値。 正確な`@type`に記載されている個々 のリソースの参照ドキュメントで現在使用している値が列挙された、 [API の概要](overview.md#resources-and-schema)です。

ここではこのドキュメントでは、さまざまなリソースについてのドキュメントは基本的には別にグループ化、`{RESOURCE_NAME}`シナリオでグループ化に似ているサービスのインデックスに存在します。 

各リソースを一意にする必要がない`@id`または`@type`です。 他よりも優先するリソースを決定する、クライアントの実装の責任です。 1 つの可能な実装は同じまたは互換性のあるリソース`@type`障害やサーバーの接続エラーが発生した場合にラウンド ロビン方式で使用できます。

### <a name="sample-request"></a>要求のサンプル

GET https://api.nuget.org/v3/index.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [service-index.json](./_data/service-index.json)]
