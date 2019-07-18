---
title: オートコンプリートを NuGet API
description: 検索のオートコンプリートのサービスでは、パッケージ Id の対話型の検出とバージョンをサポートします。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: fdc3ad8aa239a42d8a4c169a757715e856bdcb41
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911050"
---
# <a name="autocomplete"></a>オートコンプリート

V3 API を使用してパッケージ ID とバージョンをオートコンプリート エクスペリエンス構築することになります。 オートコンプリート クエリを行うために使用されるリソースは、`SearchAutocompleteService`リソースで見つかった、[サービス インデックス](service-index.md)します。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                          | メモ
------------------------------------ | -----
SearchAutocompleteService            | 最初のリリース
SearchAutocompleteService/3.0.0-beta | エイリアス `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | エイリアス `SearchAutocompleteService`

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値は、`@id`前述のリソースのいずれかに関連付けられているプロパティ`@type`値。 次のドキュメントで、プレース ホルダーのベース URL`{@id}`使用されます。

## <a name="http-methods"></a>HTTP メソッド

HTTP メソッドの登録のリソースのサポートで検出されたすべての Url`GET`と`HEAD`します。

## <a name="search-for-package-ids"></a>パッケージ Id を検索

最初のオートコンプリート API では、パッケージの ID 文字列の一部の検索をサポートします。 これは、操作は、NuGet パッケージのソースと統合ユーザー インターフェイスで、パッケージの先行入力機能を提供したい場合に優れたです。

一覧から削除されたバージョンのみを持つパッケージは、結果には表示されません。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

名前        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Ｘ       | パッケージ Id と比較する文字列
skip        | URL    | integer | Ｘ       | 改ページをスキップする結果の数
take        | URL    | integer | Ｘ       | 結果を返すには、改ページの数
prerelease  | URL    | boolean | Ｘ       | `true` または`false`含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Ｘ       | SemVer 1.0.0 バージョン文字列 

オートコンプリート クエリ`q`サーバー実装で定義されている方法で解析されます。 nuget.org では、キャメル ケースと記号の文字で、元のパッケージ ID トークンは、ページの分割によって生成された ID の断片のプレフィックスにクエリをサポートします。

`skip`パラメーターの既定値を 0 にします。

`take`パラメーターは 0 より大きい整数である必要があります。 サーバーの実装では、最大値をかける場合があります。

場合`prerelease`が提供されていない場合、プレリリース パッケージが除外されます。

`semVerLevel`クエリ パラメーターの使用をオプトインする[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)します。
このクエリ パラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージ Id のみが返されます (で、 [NuGet バージョン管理の標準](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。
場合`semVerLevel=2.0.0`が指定されて、SemVer 1.0.0 および SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。 参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。

### <a name="response"></a>応答

応答は JSON ドキュメントを含む最大`take`オートコンプリートの結果。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
totalHits | 整数          | 可      | 無視すると、一致の合計数`skip`と `take`
data      | 文字列の配列 | 可      | 要求によって、パッケージ Id が一致します。

### <a name="sample-request"></a>要求のサンプル

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>パッケージのバージョンを列挙します。

以前の API を使用してパッケージ ID が検出されると、クライアントが指定されたパッケージ ID のパッケージのバージョンを列挙するのにオートコンプリート API を使用できます。

表示されているパッケージのバージョンは、結果には表示されません。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

名前        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | 可      | バージョンをフェッチするパッケージ ID
prerelease  | URL    | boolean | Ｘ       | `true` または`false`含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Ｘ       | A SemVer 2.0.0 version string 

場合`prerelease`が提供されていない場合、プレリリース パッケージが除外されます。

`semVerLevel` SemVer 2.0.0 パッケージにオプトインするクエリ パラメーターを使用します。 このクエリ パラメーターを含めない場合は、SemVer 1.0.0 バージョンのみが返されます。 場合`semVerLevel=2.0.0`が指定されて、SemVer 1.0.0 および SemVer 2.0.0 バージョンの両方が返されます。 参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。

### <a name="response"></a>応答

応答は、指定されたパッケージ ID は、指定されたクエリ パラメーターでフィルター処理のすべてのパッケージ バージョンを含む JSON ドキュメントです。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
data      | 文字列の配列 | 可      | 要求に一致するパッケージのバージョン

パッケージのバージョンを`data`配列は SemVer 2.0.0 ビルド メタデータを含めることができます (例: `1.0.0+metadata`) 場合、`semVerLevel=2.0.0`クエリ文字列で提供されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
