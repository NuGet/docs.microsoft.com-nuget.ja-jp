---
title: オートコンプリート、NuGet API
description: 検索オートコンプリートサービスでは、パッケージ Id とバージョンの対話型検出がサポートされています。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 2893e13ff7b070844a2bdd5722da3aa1f123538d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773961"
---
# <a name="autocomplete"></a>オートコンプリート

V3 API を使用して、パッケージ ID とバージョンのオートコンプリートエクスペリエンスを構築することができます。 オートコンプリートクエリを作成するために使用されるリソースは、 `SearchAutocompleteService` [サービスインデックス](service-index.md)で検出されたリソースです。

## <a name="versioning"></a>バージョン管理

次の `@type` 値が使用されます。

@type 値                          | Notes
------------------------------------ | -----
SearchAutocompleteService            | 最初のリリース
SearchAutocompleteService/3.0.0-ベータ | エイリアス `SearchAutocompleteService`
SearchAutocompleteService/3.0.0   | エイリアス `SearchAutocompleteService`
SearchAutocompleteService/3.5.0      | クエリパラメーターのサポートを含む `packageType`

### <a name="searchautocompleteservice350"></a>SearchAutocompleteService/3.5.0
このバージョン `packageType` では、クエリパラメーターのサポートが導入されており、作成者が定義したパッケージの種類でフィルター処理できます。 に対するクエリと完全に下位互換性が `SearchAutocompleteService` あります。

## <a name="base-url"></a>ベース URL

次の Api のベース URL は、 `@id` 前述のいずれかのリソース値に関連付けられているプロパティの値です `@type` 。 次のドキュメントでは、プレースホルダーのベース URL `{@id}` が使用されます。

## <a name="http-methods"></a>HTTP メソッド

登録リソースで見つかったすべての Url は、HTTP メソッドとをサポートして `GET` `HEAD` います。

## <a name="search-for-package-ids"></a>パッケージ Id の検索

最初のオートコンプリート API は、パッケージ ID 文字列の一部の検索をサポートしています。 これは、NuGet パッケージソースと統合されたユーザーインターフェイスで package 先行入力機能を提供する場合に適しています。

一覧にないバージョンのみを含むパッケージは、結果に表示されません。

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>要求パラメーター

名前        | /     | Type    | 必須 | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | パッケージ Id と比較する文字列
skip        | URL    | integer | いいえ       | 改ページ位置の自動修正のためにスキップする結果の数
take        | URL    | integer | いいえ       | 改ページ位置の自動修正の対象となる結果の数
リリース  | URL    | boolean | いいえ       | `true`または `false` [プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する
semVerLevel | URL    | string  | no       | SemVer 1.0.0 のバージョン文字列 
packageType | URL    | string  | no       | パッケージをフィルター処理するために使用するパッケージの種類 (で追加 `SearchAutocompleteService/3.5.0` )

オートコンプリートクエリ `q` は、サーバー実装によって定義された方法で解析されます。 nuget.org では、パッケージ ID トークンのプレフィックスのクエリをサポートしています。これは、元の文字を camel 形式と記号で表現して生成された ID の一部です。

`skip`パラメーターの既定値は0です。

パラメーターには、 `take` 0 より大きい整数を指定してください。 サーバーの実装では、最大値が適用される場合があります。

が指定されて `prerelease` いない場合、プレリリースパッケージは除外されます。

`semVerLevel`クエリパラメーターは、 [semver 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)にオプトインするために使用されます。
このクエリパラメーターを除外すると、SemVer 1.0.0 互換バージョンのパッケージ Id のみが返されます (4 つの整数部分を持つバージョン文字列など、NuGet のバージョン管理に関する [標準的](../concepts/package-versioning.md) な注意点があります)。
を指定した場合 `semVerLevel=2.0.0` 、semver 1.0.0 と semver 2.0.0 互換性のあるパッケージの両方が返されます。 詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) を参照してください。

パラメーターを使用して、 `packageType` オートコンプリートの結果をさらにフィルター処理して、パッケージの種類名と一致するパッケージの種類が少なくとも1つあるパッケージのみを表示します。
指定されたパッケージの種類が、 [パッケージの種類のドキュメント](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)で定義されている有効なパッケージの種類ではない場合は、空の結果が返されます。
指定されたパッケージの種類が空の場合、フィルターは適用されません。 つまり、パラメーターに値を渡さないと、パラメーターが渡されなかった `packageType` かのように動作します。

### <a name="response"></a>応答

応答は、オートコンプリートの結果を含む JSON ドキュメントです `take` 。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | Type             | 必須 | Notes
--------- | ---------------- | -------- | -----
totalHits | integer          | はい      | 一致の合計数、無視 `skip` と `take`
data      | 文字列の配列 | はい      | 要求に一致するパッケージ Id

### <a name="sample-request"></a>要求のサンプル

```
GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true
```

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>パッケージバージョンの列挙

前の API を使用してパッケージ ID が検出されると、クライアントは autocomplete API を使用して、指定されたパッケージ ID のパッケージバージョンを列挙できます。

一覧から削除されたパッケージのバージョンは、結果に表示されません。

```
GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}
```

### <a name="request-parameters"></a>要求パラメーター

名前        | /     | Type    | 必須 | Notes
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | はい      | バージョンをフェッチするパッケージ ID
リリース  | URL    | boolean | いいえ       | `true`または `false` [プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する
semVerLevel | URL    | string  | no       | SemVer 2.0.0 バージョン文字列 

が指定されて `prerelease` いない場合、プレリリースパッケージは除外されます。

`semVerLevel`クエリパラメーターは、SemVer 2.0.0 パッケージにオプトインするために使用されます。 このクエリパラメーターを除外すると、SemVer 1.0.0 のバージョンのみが返されます。 を指定した場合は `semVerLevel=2.0.0` 、semver 1.0.0 と semver 2.0.0 の両方のバージョンが返されます。 詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) を参照してください。

### <a name="response"></a>応答

応答は、指定されたパッケージ ID のすべてのパッケージバージョンを含む JSON ドキュメントで、指定されたクエリパラメーターによってフィルター処理されます。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | Type             | 必須 | Notes
--------- | ---------------- | -------- | -----
data      | 文字列の配列 | はい      | 要求に一致するパッケージのバージョン

`data` `1.0.0+metadata` `semVerLevel=2.0.0` がクエリ文字列に指定されている場合、配列内のパッケージバージョンに semver 2.0.0 build メタデータ (など) が含まれている可能性があります。

### <a name="sample-request"></a>要求のサンプル

```
GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true
```

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
