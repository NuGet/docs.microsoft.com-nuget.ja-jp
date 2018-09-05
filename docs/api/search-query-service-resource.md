---
title: 検索、NuGet API
description: 検索サービスでは、キーワードでパッケージを照会して、パッケージの特定のフィールドでフィルターの結果をクライアントを使用します。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: f04c6a62fc3b5056ad82930447b8ba46a8797fd2
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548092"
---
# <a name="search"></a>検索

V3 API を使用してパッケージ ソースで使用可能なパッケージを検索することになります。 検索に使用されるリソースは、`SearchQueryService`リソースで見つかった、[サービス インデックス](service-index.md)します。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                   | メモ
----------------------------- | -----
SearchQueryService            | 最初のリリース
SearchQueryService/3.0.0-beta | エイリアス `SearchQueryService`
SearchQueryService/3.0.0-rc   | エイリアス `SearchQueryService`

## <a name="base-url"></a>[基本 URL]

次の API のベース URL の値は、`@id`前述のリソースのいずれかに関連付けられているプロパティ`@type`値。 次のドキュメントで、プレース ホルダーのベース URL`{@id}`使用されます。

## <a name="http-methods"></a>HTTP メソッド

HTTP メソッドの登録のリソースのサポートで検出されたすべての Url`GET`と`HEAD`します。

## <a name="search-for-packages"></a>パッケージの検索

Search API では、指定した検索クエリに一致するパッケージのページのクエリにクライアントができます。 検索クエリ (検索語句のトークン化など) の解釈は、サーバーの実装によって決まりますが、パッケージ Id、タイトル、説明、およびタグを照合する検索クエリを使用することが一般的な期待されます。 その他のパッケージのメタデータ フィールドも考慮することがあります。

一覧から削除されたパッケージを検索結果に配置しないでください。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

名前        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Ｘ       | パッケージをフィルターするために使用する検索用語
スキップ        | URL    | 整数 | Ｘ       | 改ページをスキップする結果の数
Take        | URL    | 整数 | Ｘ       | 結果を返すには、改ページの数
プレリリース版  | URL    | boolean | Ｘ       | `true` または`false`含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Ｘ       | SemVer 1.0.0 バージョン文字列 

検索クエリ`q`サーバー実装で定義されている方法で解析されます。 nuget.org で基本的なフィルター処理をサポートする、[さまざまなフィールド](../consume-packages/finding-and-choosing-packages.md#search-syntax)します。 ない場合は`q`skip と take によって課される境界内のすべてのパッケージを返す必要がある提供されます。 これにより、Visual Studio の NuGet のエクスペリエンスで、[参照] タブ。

`skip`パラメーターの既定値を 0 にします。

`take`パラメーターは 0 より大きい整数である必要があります。 サーバーの実装では、最大値をかける場合があります。

場合`prerelease`が提供されていない場合、プレリリース パッケージが除外されます。

`semVerLevel`クエリ パラメーターの使用をオプトインする[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)します。
このクエリ パラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージのみが返されます (で、 [NuGet バージョン管理の標準](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。
場合`semVerLevel=2.0.0`が指定されて、SemVer 1.0.0 および SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。 参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。

### <a name="response"></a>応答

応答は JSON ドキュメントを含む最大`take`結果を検索します。 検索結果がパッケージ ID でグループ化します。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
totalHits | 整数          | 可      | 無視すると、一致の合計数`skip`と `take`
[データ]      | オブジェクトの配列 | 可      | 要求に一致する検索結果

### <a name="search-result"></a>検索結果

内の各項目、`data`配列が同じパッケージ ID を共有パッケージのバージョンのグループから成る JSON オブジェクト
オブジェクトには、次のプロパティがあります。

名前           | 種類                       | 必須 | メモ
-------------- | -------------------------- | -------- | -----
ID             | string                     | 可      | 一致するパッケージの ID
version        | string                     | 可      | (ビルド メタデータを含む可能性があります)、パッケージの完全な SemVer 2.0.0 バージョン文字列
説明    | string                     | Ｘ       | 
バージョン       | オブジェクトの配列           | 可      | すべての一致するパッケージのバージョン、`prerelease`パラメーター
作成者        | 文字列または文字列の配列 | Ｘ       | 
iconUrl        | string                     | Ｘ       | 
licenseUrl     | string                     | Ｘ       | 
owners         | 文字列または文字列の配列 | Ｘ       | 
projectUrl     | string                     | Ｘ       | 
登録   | string                     | Ｘ       | 絶対 URL、関連付けられている[登録インデックス](registration-base-url-resource.md#registration-index)
概要        | string                     | Ｘ       | 
タグ           | 文字列または文字列の配列 | Ｘ       | 
タイトル          | string                     | Ｘ       | 
totalDownloads | 整数                    | Ｘ       | ダウンロードの合計でこの値を推測できなければ、`versions`配列
検証済み       | boolean                    | Ｘ       | パッケージは、かどうかを示すブール値を JSON[検証](../reference/id-prefix-reservation.md)

Nuget.org には、検証済みのパッケージとは、予約済み ID のプレフィックスに一致するパッケージ ID があり、いずれかの予約された名前空間の所有者が所有する 1 つです。 詳細については、次を参照してください。、 [ID プレフィックスの予約に関するドキュメント](../reference/id-prefix-reservation.md)します。

検索結果のオブジェクトに含まれるメタデータは、最新バージョンのパッケージから取得されます。 内の各項目、`versions`配列は、次のプロパティを持つ JSON オブジェクト。

名前      | 種類    | 必須 | メモ
--------- | ------- | -------- | -----
@id       | string  | 可      | 絶対 URL、関連付けられている[登録リーフ](registration-base-url-resource.md#registration-leaf)
version   | string  | 可      | (ビルド メタデータを含む可能性があります)、パッケージの完全な SemVer 2.0.0 バージョン文字列
ダウンロード | 整数 | 可      | この特定のパッケージ バージョンのダウンロード数

### <a name="sample-request"></a>要求のサンプル

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [search-result.json](./_data/search-result.json)]
