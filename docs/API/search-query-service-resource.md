---
title: "検索では、NuGet API |Microsoft ドキュメント"
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
description: "Search サービスでは、キーワードでパッケージを照会して、パッケージの特定のフィールドにフィルターの結果にクライアントを許可します。"
keywords: "NuGet 検索 API では、NuGet パッケージ、NuGet パッケージを照会する、API であり、NuGet パッケージを参照する API の検出します。"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 612ce0f46b654335a29bb36a64b27525994162ed
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/02/2018
---
# <a name="search"></a>検索

V3 API を使用して、パッケージ ソースで使用可能なパッケージを検索することができます。 検索に使用されるリソースは、`SearchQueryService`リソースで見つかった、[サービス インデックス](service-index.md)です。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                   | メモ
----------------------------- | -----
SearchQueryService            | 最初のリリース
SearchQueryService/3.0.0-beta | エイリアス`SearchQueryService`
SearchQueryService/3.0.0-rc   | エイリアス`SearchQueryService`

## <a name="base-url"></a>[基本 URL]

次の API のベース URL の値、`@id`前述のリソースのいずれかに関連付けられたプロパティ`@type`値。 次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。

## <a name="http-methods"></a>HTTP メソッド

HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。

## <a name="search-for-packages"></a>パッケージの検索

検索 API では、指定した検索クエリに一致するパッケージのページのクエリにクライアントができます。 検索クエリ (検索語句のトークン化など) の解釈は、サーバーの実装によって決まりますが、検索クエリがパッケージ Id、タイトル、説明、およびタグのマッチングに使用することは、一般的な予想です。 その他のパッケージ メタデータ フィールドも考慮することがあります。

一覧にないパッケージは、検索結果に表示する必要があることはありません。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

name        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Ｘ       | パッケージをフィルターするために使用する検索用語
スキップ        | URL    | 整数 | Ｘ       | 改ページをスキップします。 結果の数
take        | URL    | 整数 | Ｘ       | 結果を返すには、改ページの数
プレリリース版  | URL    | boolean | Ｘ       | `true`または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Ｘ       | SemVer 1.0.0 バージョン文字列 

検索クエリ`q`はサーバーの実装で定義されている方法で解析します。 nuget.org の基本的なフィルタ リングをサポートしている、[さまざまなフィールド](../consume-packages/finding-and-choosing-packages.md#search-syntax)です。 ない場合は`q`は、提供、skip と take によって課される境界内のすべてのパッケージを返す必要があります。 これにより、NuGet の Visual Studio エクスペリエンスでは、「参照」タブです。

`skip`パラメーターの既定値を 0 にします。

`take`パラメーターは 0 より大きい整数である必要があります。 サーバーの実装では、最大値をかける場合があります。

場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。

`semVerLevel`クエリ パラメーターを使用するオプトイン[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)です。
このクエリのパラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージのみが返されます (で、[標準の NuGet バージョン管理](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。
場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。 参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。

### <a name="response"></a>応答

応答は最大含む JSON ドキュメント`take`結果を検索します。 検索結果はパッケージ ID でグループ化します。

ルートの JSON オブジェクトには、次のプロパティがあります。

name      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
totalHits | 整数          | 可      | 無視すると、一致の合計数`skip`と`take`
[データ]      | オブジェクトの配列 | 可      | 要求に一致する検索結果

### <a name="search-result"></a>検索結果

内の各項目、`data`配列が同じパッケージ ID を共有するパッケージのバージョンのグループの構成された JSON オブジェクト
オブジェクトには、次のプロパティがあります。

name           | 種類                       | 必須 | メモ
-------------- | -------------------------- | -------- | -----
ID             | string                     | 可      | 一致するパッケージの ID
version        | string                     | 可      | (ビルドのメタデータを含む可能性があります)、パッケージの完全な SemVer 2.0.0 バージョン文字列
説明    | string                     | Ｘ       | 
バージョン       | オブジェクトの配列           | 可      | すべての一致するパッケージのバージョン、`prerelease`パラメーター
作成者        | 文字列または文字列の配列 | Ｘ       | 
iconUrl        | string                     | Ｘ       | 
licenseUrl     | string                     | Ｘ       | 
owners         | 文字列または文字列の配列 | Ｘ       | 
projectUrl     | string                     | Ｘ       | 
登録   | string                     | Ｘ       | 関連付けられたへの絶対 URL[登録インデックス](registration-base-url-resource.md#registration-index)
概要        | string                     | Ｘ       | 
タグ           | 文字列または文字列の配列 | Ｘ       | 
タイトル          | string                     | Ｘ       | 
totalDownloads | 整数                    | Ｘ       | ダウンロード中の合計でこの値を推測できなければ、`versions`配列
検証済み       | boolean                    | Ｘ       | パッケージがかどうかを示すブール値を JSON[検証](../reference/id-prefix-reservation.md)

Nuget.org、検証済みのパッケージは予約済み ID のプレフィックスに一致するパッケージ ID があり、予約された名前空間の所有者のいずれかによって所有されています。 詳細については、次を参照してください。、 [ID プレフィックスの予約に関するドキュメント](../reference/id-prefix-reservation.md)です。

検索結果のオブジェクトに含まれるメタデータは、最新バージョンのパッケージから取得されます。 内の各項目、`versions`配列は、次のプロパティを使用して、JSON オブジェクト。

name      | 種類    | 必須 | メモ
--------- | ------- | -------- | -----
@id       | string  | 可      | 関連付けられたへの絶対 URL[登録リーフ](registration-base-url-resource.md#registration-leaf)
version   | string  | 可      | (ビルドのメタデータを含む可能性があります)、パッケージの完全な SemVer 2.0.0 バージョン文字列
ダウンロード | 整数 | 可      | この特定のパッケージのバージョンのダウンロードの数

### <a name="sample-request"></a>要求のサンプル

    GET https://api-v2v3search-0.nuget.org/query?q=NuGet.Versioning&prerelease=false

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [search-result.json](./_data/search-result.json)]
