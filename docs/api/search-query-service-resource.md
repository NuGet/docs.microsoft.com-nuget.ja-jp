---
title: 検索、NuGet API
description: 検索サービスを使用すると、クライアントは、キーワードによってパッケージを照会し、特定のパッケージフィールドの結果をフィルター処理できます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7047dfd48b7f93756bbb1491de1b7e65da2c12b4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775408"
---
# <a name="search"></a>検索

V3 API を使用して、パッケージソースで利用可能なパッケージを検索することができます。 検索に使用されるリソースは、 `SearchQueryService` [サービスインデックス](service-index.md)で検出されたリソースです。

## <a name="versioning"></a>バージョン管理

次の `@type` 値が使用されます。

@type 値                   | Notes
----------------------------- | -----
SearchQueryService            | 最初のリリース
SearchQueryService/3.0.0-ベータ | エイリアス `SearchQueryService`
SearchQueryService/3.0.0   | エイリアス `SearchQueryService`
SearchQueryService/3.5.0      | クエリパラメーターのサポートを含む `packageType`

### <a name="searchqueryservice350"></a>SearchQueryService/3.5.0
このバージョンでは、 `packageType` クエリパラメーターと応答プロパティのサポートが導入されており `packageTypes` 、作成者が定義したパッケージの種類でフィルター処理できます。 に対するクエリと完全に下位互換性が `SearchQueryService` あります。

## <a name="base-url"></a>ベース URL

次の API のベース URL は、 `@id` 前述のいずれかのリソース値に関連付けられているプロパティの値です `@type` 。 次のドキュメントでは、プレースホルダーのベース URL `{@id}` が使用されます。

## <a name="http-methods"></a>HTTP メソッド

登録リソースで見つかったすべての Url は、HTTP メソッドとをサポートして `GET` `HEAD` います。

## <a name="search-for-packages"></a>パッケージの検索

検索 API を使用すると、クライアントは、指定された検索クエリに一致するパッケージのページを照会できます。 検索クエリの解釈 (検索用語のトークン化など) はサーバーの実装によって決定されますが、一般的には、検索クエリがパッケージ Id、タイトル、説明、タグの照合に使用されることを想定しています。 その他のパッケージメタデータフィールドも考慮することができます。

一覧にないパッケージは、検索結果に表示されません。

```
GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}&packageType={PACKAGETYPE}
```

### <a name="request-parameters"></a>要求パラメーター

名前        | /     | Type    | 必須 | Notes
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | no       | パッケージをフィルター処理するために使用する検索語句
skip        | URL    | integer | いいえ       | 改ページ位置の自動修正のためにスキップする結果の数
take        | URL    | integer | いいえ       | 改ページ位置の自動修正の対象となる結果の数
リリース  | URL    | boolean | いいえ       | `true`または `false` [プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する
semVerLevel | URL    | string  | no       | SemVer 1.0.0 のバージョン文字列 
packageType | URL    | string  | no       | パッケージをフィルター処理するために使用するパッケージの種類 (で追加 `SearchQueryService/3.5.0` )

検索クエリは、 `q` サーバー実装によって定義された方法で解析されます。 nuget.org では、さまざまな [フィールド](../consume-packages/finding-and-choosing-packages.md#search-syntax)に対する基本的なフィルター処理がサポートされています。 が指定されていない場合は、 `q` skip および take によって設定された境界内で、すべてのパッケージが返される必要があります。 これにより、NuGet Visual Studio エクスペリエンスの [参照] タブが有効になります。

`skip`パラメーターの既定値は0です。

パラメーターには、 `take` 0 より大きい整数を指定してください。 サーバーの実装では、最大値が適用される場合があります。

が指定されて `prerelease` いない場合、プレリリースパッケージは除外されます。

`semVerLevel`クエリパラメーターは、 [semver 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)にオプトインするために使用されます。
このクエリパラメーターを除外すると、SemVer 1.0.0 互換バージョンのパッケージのみが返されます (4 つの整数部分を持つバージョン文字列など、NuGet のバージョン管理に関する [標準的](../concepts/package-versioning.md) な注意点があります)。
を指定した場合 `semVerLevel=2.0.0` 、semver 1.0.0 と semver 2.0.0 互換性のあるパッケージの両方が返されます。 詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29) を参照してください。

パラメーターを使用すると、パッケージの種類 `packageType` 名と一致するパッケージの種類が少なくとも1つあるパッケージのみに検索結果をさらに絞り込むことができます。
指定されたパッケージの種類が、 [パッケージの種類のドキュメント](https://github.com/NuGet/Home/wiki/Package-Type-%5BPacking%5D)で定義されている有効なパッケージの種類ではない場合は、空の結果が返されます。
指定されたパッケージの種類が空の場合、フィルターは適用されません。 つまり、packageType パラメーターに値を渡さないと、パラメーターが渡されなかったかのように動作します。

### <a name="response"></a>応答

応答は、最大検索結果を含む JSON ドキュメントです `take` 。 検索結果はパッケージ ID 別にグループ化されます。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | Type             | 必須 | Notes
--------- | ---------------- | -------- | -----
totalHits | integer          | はい      | 一致の合計数、無視 `skip` と `take`
data      | オブジェクトの配列 | はい      | 要求に一致する検索結果

### <a name="search-result"></a>Search result

配列の各項目 `data` は、同じパッケージ ID を共有するパッケージバージョンのグループで構成される JSON オブジェクトです。
このオブジェクトには、以下のプロパティがあります。

名前           | Type                       | 必須 | Notes
-------------- | -------------------------- | -------- | -----
id             | string                     | はい      | 一致したパッケージの ID
version        | string                     | はい      | パッケージの完全な SemVer 2.0.0 バージョン文字列 (ビルドメタデータを含む可能性があります)
description    | string                     | no       | 
versions       | オブジェクトの配列           | はい      | パラメーターに一致するパッケージのすべてのバージョン `prerelease`
作成者        | 文字列または文字列の配列 | いいえ       | 
iconUrl        | string                     | no       | 
licenseUrl     | string                     | no       | 
owners         | 文字列または文字列の配列 | いいえ       | 
projectUrl     | string                     | no       | 
登録   | string                     | no       | 関連付けられている[登録インデックス](registration-base-url-resource.md#registration-index)の絶対 URL
まとめ        | string                     | no       | 
tags           | 文字列または文字列の配列 | いいえ       | 
title          | string                     | no       | 
totalDownloads | integer                    | いいえ       | この値は、配列内のダウンロードの合計によって推論できます。 `versions`
れ       | boolean                    | いいえ       | パッケージが[検証](../nuget-org/id-prefix-reservation.md)されているかどうかを示す JSON ブール値
packageTypes   | オブジェクトの配列           | はい      | パッケージ作成者によって定義されたパッケージの種類 (で追加 `SearchQueryService/3.5.0` )

Nuget.org では、検証済みのパッケージとは、予約済みの ID プレフィックスに一致し、予約済みのプレフィックスの所有者によって所有されているパッケージ ID を持つパッケージのことです。 詳細については、 [ID プレフィックスの予約に関するドキュメント](../nuget-org/id-prefix-reservation.md)を参照してください。

検索結果オブジェクトに含まれるメタデータは、最新のパッケージバージョンから取得されます。 配列内の各項目 `versions` は、次のプロパティを持つ JSON オブジェクトです。

名前      | Type    | 必須 | Notes
--------- | ------- | -------- | -----
@id       | string  | はい      | 関連付けられている[登録リーフ](registration-base-url-resource.md#registration-leaf)への絶対 URL
version   | string  | はい      | パッケージの完全な SemVer 2.0.0 バージョン文字列 (ビルドメタデータを含む可能性があります)
ダウンロード | integer | はい      | この特定のパッケージバージョンのダウンロード回数

配列は、 `packageTypes` 常に少なくとも1つの項目で構成されます。 特定のパッケージ ID のパッケージの種類は、他の検索パラメーターに関して、パッケージの最新バージョンで定義されているパッケージの種類と見なされます。 配列内の各項目 `packageTypes` は、次のプロパティを持つ JSON オブジェクトです。

名前      | Type    | 必須 | Notes
--------- | ------- | -------- | -----
name      | string  | はい      | パッケージの種類の名前。

### <a name="sample-request"></a>要求のサンプル

```
GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0
```

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [search-result.json](./_data/search-result.json)]