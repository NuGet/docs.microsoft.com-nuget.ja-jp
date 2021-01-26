---
title: サービスインデックス, NuGet API
description: サービスインデックスは、NuGet HTTP API のエントリポイントであり、サーバーの機能を列挙します。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: c2d4d23313c80c24b537b1df227a9cea6784ef6e
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775353"
---
# <a name="service-index"></a>サービス インデックス

サービスインデックスは、NuGet パッケージソースのエントリポイントである JSON ドキュメントであり、クライアント実装でパッケージソースの機能を検出できます。 サービスインデックスは、2つの必須プロパティ `version` (サービスインデックスのスキーマバージョン) と `resources`  (パッケージソースのエンドポイントまたは機能) を持つ JSON オブジェクトです。

nuget. 組織のサービスインデックスはにあり `https://api.nuget.org/v3/index.json` ます。

## <a name="versioning"></a>バージョン管理

`version`値は、サービスインデックスのスキーマバージョンを示す SemVer 2.0.0 解析バージョン文字列です。 API は、バージョン文字列のメジャーバージョン番号がであることを指定し `3` ます。 サービスインデックススキーマに重大でない変更が加えられると、バージョン文字列のマイナーバージョンが増加します。

サービスインデックスの各リソースは、サービスインデックスのスキーマバージョンとは別にバージョン管理されます。

現在のスキーマのバージョンは `3.0.0` です。 バージョンは、 `3.0.0` 以前のバージョンと機能的に同等です `3.0.0-beta.1` が、安定した定義済みのスキーマをより明確に伝えるため、推奨されます。

## <a name="http-methods"></a>HTTP メソッド

サービスインデックスには、HTTP メソッドおよびを使用してアクセスでき `GET` `HEAD` ます。

## <a name="resources"></a>リソース

プロパティは、 `resources` このパッケージソースによってサポートされるリソースの配列を格納します。

### <a name="resource"></a>リソース

リソースは、配列内のオブジェクトです `resources` 。 これは、パッケージソースのバージョン管理された機能を表します。 リソースには、次のプロパティがあります。

名前          | Type   | 必須 | Notes
------------- | ------ | -------- | -----
@id           | string | はい      | リソースへの URL
@type         | string | はい      | リソースの種類を表す文字列定数。
コメント       | string | no       | 人間が判読できるリソースの説明

は絶対 URI である必要があり、 `@id` HTTP または HTTPS のいずれかのスキーマを持つ必要があります。

は、 `@type` リソースと対話するときに使用する特定のプロトコルを識別するために使用されます。 リソースの型は不透明な文字列ですが、一般的には次の形式です。

```
{RESOURCE_NAME}/{RESOURCE_VERSION}
```

クライアントは、 `@type` 認識している値をハードコーディングし、パッケージソースのサービスインデックスで検索します。 `@type`現在使用中の正確な値は、 [API の概要](overview.md#resources-and-schema)に記載されている個々のリソース参照ドキュメントで列挙されます。

このドキュメントでは、さまざまなリソースに関するドキュメントは基本的に、「 `{RESOURCE_NAME}` シナリオ別のグループ化」に似たサービスインデックスによってグループ化されます。 

各リソースに一意のまたはがあるという要件はありません `@id` `@type` 。 どのリソースを優先するかは、クライアントの実装によって決まります。 考えられる1つの実装は、接続エラーやサーバーエラーが発生した場合に、同じまたは互換性のあるリソースを `@type` ラウンドロビン方式で使用できることです。

### <a name="sample-request"></a>要求のサンプル

```
GET https://api.nuget.org/v3/index.json
```

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [service-index.json](./_data/service-index.json)]
