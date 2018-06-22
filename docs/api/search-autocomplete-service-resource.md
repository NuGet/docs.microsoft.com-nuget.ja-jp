---
title: オートコンプリートを NuGet API
description: 検索のオートコンプリート機能のサービスは、パッケージ Id の対話型の検出とバージョンをサポートします。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: d5e1936c6c5406a1a376c16b2bad5351320dfb4f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
ms.locfileid: "31822137"
---
# <a name="autocomplete"></a>オートコンプリート

パッケージ ID とバージョン オートコンプリート エクスペリエンスを V3 API を使用して行うことができます。 オートコンプリート クエリを実行するためのシステム リソースが、`SearchAutocompleteService`リソースで見つかった、[サービス インデックス](service-index.md)です。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                          | メモ
------------------------------------ | -----
SearchAutocompleteService            | 最初のリリース
SearchAutocompleteService/3.0.0-beta | エイリアス `SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | エイリアス `SearchAutocompleteService`

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値、`@id`前述のリソースのいずれかに関連付けられたプロパティ`@type`値。 次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。

## <a name="http-methods"></a>HTTP メソッド

HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。

## <a name="search-for-package-ids"></a>パッケージ Id を検索

最初のオートコンプリート機能 API は、パッケージ ID 文字列の一部の検索をサポートします。 これは、操作は、NuGet パッケージのソースと統合されてユーザー インターフェイスでのパッケージは入力行機能を提供する場合に優れたです。

一覧にないバージョンのみを使用してパッケージは、結果には表示されません。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

名前        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Ｘ       | パッケージ Id と比較する文字列
スキップ        | URL    | 整数 | Ｘ       | 改ページをスキップします。 結果の数
take        | URL    | 整数 | Ｘ       | 結果を返すには、改ページの数
プレリリース版  | URL    | boolean | Ｘ       | `true` または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Ｘ       | SemVer 1.0.0 バージョン文字列 

オートコンプリート クエリ`q`はサーバーの実装で定義されている方法で解析します。 nuget.org は camel 形式の大文字と記号の文字で元の spliting によって生成される ID の部分は、パッケージ ID のトークンのプレフィックスのクエリをサポートします。

`skip`パラメーターの既定値を 0 にします。

`take`パラメーターは 0 より大きい整数である必要があります。 サーバーの実装では、最大値をかける場合があります。

場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。

`semVerLevel`クエリ パラメーターを使用するオプトイン[SemVer 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)です。
このクエリのパラメーターを除外すると場合、SemVer 1.0.0 の互換性のあるバージョンのパッケージ Id のみが返されます (で、[標準の NuGet バージョン管理](../reference/package-versioning.md)4 の整数部分でバージョン文字列などの注意事項)。
場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 の互換性のあるパッケージの両方が返されます。 参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。

### <a name="response"></a>応答

応答は最大含む JSON ドキュメント`take`オートコンプリートの結果。

ルートの JSON オブジェクトには、次のプロパティがあります。

名前      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
totalHits | 整数          | 可      | 無視すると、一致の合計数`skip`と `take`
[データ]      | 文字列の配列 | 可      | パッケージ Id と一致した要求

### <a name="sample-request"></a>要求のサンプル

取得 https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>パッケージのバージョンを列挙します。

クライアントが提供されたパッケージ ID のパッケージのバージョンを列挙するのに API オートコンプリート機能を使用できます、前の API を使用して、パッケージ ID が検出されると、

一覧にあるパッケージのバージョンは、結果には表示されません。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

名前        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
ID          | URL    | string  | 可      | バージョンを取得するパッケージ ID
プレリリース版  | URL    | boolean | Ｘ       | `true` または`false`に含めるかどうかを決定する[プレリリース パッケージ](../create-packages/prerelease-packages.md)
semVerLevel | URL    | string  | Ｘ       | SemVer 2.0.0 バージョン文字列 

場合`prerelease`が提供されていない場合、プレリリース版パッケージが除外されます。

`semVerLevel` SemVer 2.0.0 パッケージにオプトインするクエリ パラメーターを使用します。 このクエリのパラメーターを除外すると、SemVer 1.0.0 バージョンのみが返されます。 場合`semVerLevel=2.0.0`が SemVer 1.0.0 と SemVer 2.0.0 のバージョンの両方が返されます。 参照してください、 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)詳細についてはします。

### <a name="response"></a>応答

応答は、指定されたパッケージの ID を指定されたクエリ パラメーターでフィルター処理のすべてのパッケージ バージョンを含む JSON ドキュメントです。

ルートの JSON オブジェクトには、次のプロパティがあります。

名前      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
[データ]      | 文字列の配列 | 可      | 要求に一致するパッケージのバージョン

パッケージのバージョンを`data`配列が SemVer 2.0.0 ビルド メタデータを含む可能性があります (例: `1.0.0+metadata`) 場合、`semVerLevel=2.0.0`クエリ文字列で提供されました。

### <a name="sample-request"></a>要求のサンプル

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
