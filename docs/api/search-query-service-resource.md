---
title: 検索、NuGet API
description: 検索サービスを使用すると、クライアントは、キーワードによってパッケージを照会し、特定のパッケージフィールドの結果をフィルター処理できます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: be25e9bf72b9115de8ae55f6296195fed3152f10
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235115"
---
# <a name="search"></a>検索

V3 API を使用して、パッケージソースで利用可能なパッケージを検索することができます。 検索に使用されるリソースは`SearchQueryService` 、[サービスインデックス](service-index.md)で検出されたリソースです。

## <a name="versioning"></a>バージョン管理

次`@type`の値が使用されます。

@type の値                   | メモ
----------------------------- | -----
SearchQueryService            | 最初のリリース
SearchQueryService/3.0.0-beta | エイリアス`SearchQueryService`
SearchQueryService/3.0.0-rc   | エイリアス`SearchQueryService`

## <a name="base-url"></a>[基本 URL]

次の API のベース URL は、前述のいずれか`@id`のリソース`@type`値に関連付けられているプロパティの値です。 次のドキュメントでは、プレースホルダーのベース`{@id}` URL が使用されます。

## <a name="http-methods"></a>HTTP メソッド

登録リソースで見つかったすべての url は、HTTP `GET`メソッド`HEAD`とをサポートしています。

## <a name="search-for-packages"></a>パッケージの検索

検索 API を使用すると、クライアントは、指定された検索クエリに一致するパッケージのページを照会できます。 検索クエリの解釈 (検索用語のトークン化など) はサーバーの実装によって決定されますが、一般的には、検索クエリがパッケージ Id、タイトル、説明、タグの照合に使用されることを想定しています。 その他のパッケージメタデータフィールドも考慮することができます。

一覧にないパッケージは、検索結果に表示されません。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

名前        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Ｘ       | パッケージをフィルター処理するために使用する検索語句
skip        | URL    | integer | Ｘ       | 改ページ位置の自動修正のためにスキップする結果の数
take        | URL    | integer | Ｘ       | 改ページ位置の自動修正の対象となる結果の数
prerelease  | URL    | boolean | Ｘ       | `true`また`false`は[プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する
semVerLevel | URL    | string  | Ｘ       | SemVer 1.0.0 のバージョン文字列 

検索クエリ`q`は、サーバー実装によって定義された方法で解析されます。 nuget.org では、さまざまな[フィールド](../consume-packages/finding-and-choosing-packages.md#search-syntax)に対する基本的なフィルター処理がサポートされています。 `q`が指定されていない場合は、skip および take によって設定された境界内で、すべてのパッケージが返される必要があります。 これにより、NuGet Visual Studio エクスペリエンスの [参照] タブが有効になります。

パラメーター `skip`の既定値は0です。

パラメーター `take`には、0より大きい整数を指定してください。 サーバーの実装では、最大値が適用される場合があります。

が`prerelease`指定されていない場合、プレリリースパッケージは除外されます。

クエリ`semVerLevel`パラメーターは、 [semver 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)にオプトインするために使用されます。
このクエリパラメーターを除外すると、SemVer 1.0.0 互換バージョンのパッケージのみが返されます (4 つの整数部分を持つバージョン文字列など、NuGet のバージョン管理に関する[標準的](../concepts/package-versioning.md)な注意点があります)。
を`semVerLevel=2.0.0`指定した場合、semver 1.0.0 と semver 2.0.0 互換性のあるパッケージの両方が返されます。 詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)を参照してください。

### <a name="response"></a>応答

応答は、最大検索結果を`take`含む JSON ドキュメントです。 検索結果はパッケージ ID 別にグループ化されます。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
totalHits | integer          | 可      | 一致の合計数、無視`skip`と`take`
data      | オブジェクトの配列 | 可      | 要求に一致する検索結果

### <a name="search-result"></a>検索結果

`data`配列の各項目は、同じパッケージ ID を共有するパッケージバージョンのグループで構成される JSON オブジェクトです。
オブジェクトには、次のプロパティがあります。

名前           | 種類                       | 必須 | メモ
-------------- | -------------------------- | -------- | -----
id             | string                     | 可      | 一致したパッケージの ID
version        | string                     | 可      | パッケージの完全な SemVer 2.0.0 バージョン文字列 (ビルドメタデータを含む可能性があります)
description    | string                     | Ｘ       | 
versions       | オブジェクトの配列           | 可      | パラメーターに`prerelease`一致するパッケージのすべてのバージョン
authors        | 文字列または文字列の配列 | Ｘ       | 
iconUrl        | string                     | Ｘ       | 
licenseUrl     | string                     | Ｘ       | 
owners         | 文字列または文字列の配列 | Ｘ       | 
projectUrl     | string                     | Ｘ       | 
registration   | string                     | Ｘ       | 関連付けられている[登録インデックス](registration-base-url-resource.md#registration-index)の絶対 URL
summary        | string                     | Ｘ       | 
tags           | 文字列または文字列の配列 | Ｘ       | 
title          | string                     | Ｘ       | 
totalDownloads | integer                    | Ｘ       | この値は、 `versions`配列内のダウンロードの合計によって推論できます。
verified       | boolean                    | Ｘ       | パッケージが[検証](../nuget-org/id-prefix-reservation.md)されているかどうかを示す JSON ブール値

Nuget.org では、検証済みのパッケージとは、予約済みの ID プレフィックスに一致し、予約済みのプレフィックスの所有者によって所有されているパッケージ ID を持つパッケージのことです。 詳細については、 [ID プレフィックスの予約に関するドキュメント](../reference/id-prefix-reservation.md)を参照してください。

検索結果オブジェクトに含まれるメタデータは、最新のパッケージバージョンから取得されます。 `versions`配列内の各項目は、次のプロパティを持つ JSON オブジェクトです。

名前      | 種類    | 必須 | メモ
--------- | ------- | -------- | -----
@id       | string  | 可      | 関連付けられている[登録リーフ](registration-base-url-resource.md#registration-leaf)への絶対 URL
version   | string  | 可      | パッケージの完全な SemVer 2.0.0 バージョン文字列 (ビルドメタデータを含む可能性があります)
downloads | integer | 可      | この特定のパッケージバージョンのダウンロード回数

### <a name="sample-request"></a>要求のサンプル

    GET https://azuresearch-usnc.nuget.org/query?q=NuGet.Versioning&prerelease=false&semVerLevel=2.0.0

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [search-result.json](./_data/search-result.json)]
