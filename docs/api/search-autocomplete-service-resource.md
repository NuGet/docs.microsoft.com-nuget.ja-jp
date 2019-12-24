---
title: オートコンプリート、NuGet API
description: 検索オートコンプリートサービスでは、パッケージ Id とバージョンの対話型検出がサポートされています。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1179ad649da560766f28c18ab6fa670fd8fa6d8b
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488306"
---
# <a name="autocomplete"></a>オートコンプリート

V3 API を使用して、パッケージ ID とバージョンのオートコンプリートエクスペリエンスを構築することができます。 オートコンプリートクエリを作成するために使用`SearchAutocompleteService`されるリソースは、[サービスインデックス](service-index.md)で検出されたリソースです。

## <a name="versioning"></a>バージョン管理

次`@type`の値が使用されます。

@type の値                          | メモ
------------------------------------ | -----
SearchAutocompleteService            | 最初のリリース
SearchAutocompleteService/3.0.0-ベータ | エイリアス`SearchAutocompleteService`
SearchAutocompleteService/3.0.0-rc   | エイリアス`SearchAutocompleteService`

## <a name="base-url"></a>[基本 URL]

次の api のベース URL は、前述のいずれか`@id`のリソース`@type`値に関連付けられているプロパティの値です。 次のドキュメントでは、プレースホルダーのベース`{@id}` URL が使用されます。

## <a name="http-methods"></a>HTTP メソッド

登録リソースで見つかったすべての url は、HTTP `GET`メソッド`HEAD`とをサポートしています。

## <a name="search-for-package-ids"></a>パッケージ Id の検索

最初のオートコンプリート API は、パッケージ ID 文字列の一部の検索をサポートしています。 これは、NuGet パッケージソースと統合されたユーザーインターフェイスで package 先行入力機能を提供する場合に適しています。

一覧にないバージョンのみを含むパッケージは、結果に表示されません。

    GET {@id}?q={QUERY}&skip={SKIP}&take={TAKE}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

名前        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
q           | URL    | string  | Ｘ       | パッケージ Id と比較する文字列
skip        | URL    | integer | Ｘ       | 改ページ位置の自動修正のためにスキップする結果の数
take        | URL    | integer | Ｘ       | 改ページ位置の自動修正の対象となる結果の数
prerelease  | URL    | boolean | Ｘ       | `true`また`false`は[プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する
semVerLevel | URL    | string  | Ｘ       | SemVer 1.0.0 のバージョン文字列 

オートコンプリートクエリ`q`は、サーバー実装によって定義された方法で解析されます。 nuget.org では、パッケージ ID トークンのプレフィックスのクエリをサポートしています。これは、元の文字を camel 形式と記号で表現して生成された ID の一部です。

パラメーター `skip`の既定値は0です。

パラメーター `take`には、0より大きい整数を指定してください。 サーバーの実装では、最大値が適用される場合があります。

が`prerelease`指定されていない場合、プレリリースパッケージは除外されます。

クエリ`semVerLevel`パラメーターは、 [semver 2.0.0 パッケージ](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29#identifying-semver-v200-packages)にオプトインするために使用されます。
このクエリパラメーターを除外すると、SemVer 1.0.0 互換バージョンのパッケージ Id のみが返されます (4 つの整数部分を持つバージョン文字列など、NuGet のバージョン管理に関する[標準的](../concepts/package-versioning.md)な注意点があります)。
を`semVerLevel=2.0.0`指定した場合、semver 1.0.0 と semver 2.0.0 互換性のあるパッケージの両方が返されます。 詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)を参照してください。

### <a name="response"></a>応答

応答は、オートコンプリートの結果を`take`含む JSON ドキュメントです。

ルート JSON オブジェクトには、次のプロパティがあります。

名前      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
totalHits | integer          | 可      | 一致の合計数、無視`skip`と`take`
data      | 文字列の配列 | 可      | 要求に一致するパッケージ Id

### <a name="sample-request"></a>要求のサンプル

    GET https://api-v2v3search-0.nuget.org/autocomplete?q=storage&prerelease=true

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [autocomplete-id-result.json](./_data/autocomplete-id-result.json)]

## <a name="enumerate-package-versions"></a>パッケージバージョンの列挙

前の API を使用してパッケージ ID が検出されると、クライアントは autocomplete API を使用して、指定されたパッケージ ID のパッケージバージョンを列挙できます。

一覧から削除されたパッケージのバージョンは、結果に表示されません。

    GET {@id}?id={ID}&prerelease={PRERELEASE}&semVerLevel={SEMVERLEVEL}

### <a name="request-parameters"></a>要求パラメーター

名前        | イン     | 型    | 必須 | メモ
----------- | ------ | ------- | -------- | -----
id          | URL    | string  | 可      | バージョンをフェッチするパッケージ ID
prerelease  | URL    | boolean | Ｘ       | `true`また`false`は[プレリリースパッケージ](../create-packages/prerelease-packages.md)を含めるかどうかを判断する
semVerLevel | URL    | string  | Ｘ       | SemVer 2.0.0 バージョン文字列 

が`prerelease`指定されていない場合、プレリリースパッケージは除外されます。

クエリ`semVerLevel`パラメーターは、semver 2.0.0 パッケージにオプトインするために使用されます。 このクエリパラメーターを除外すると、SemVer 1.0.0 のバージョンのみが返されます。 を`semVerLevel=2.0.0`指定した場合は、semver 1.0.0 と semver 2.0.0 の両方のバージョンが返されます。 詳細については、 [nuget.org の Semver 2.0.0 のサポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)を参照してください。

### <a name="response"></a>応答

応答は、指定されたパッケージ ID のすべてのパッケージバージョンを含む JSON ドキュメントで、指定されたクエリパラメーターによってフィルター処理されます。

ルート JSON オブジェクトには、次のプロパティがあります。

Name      | 種類             | 必須 | メモ
--------- | ---------------- | -------- | -----
data      | 文字列の配列 | 可      | 要求に一致するパッケージのバージョン

がクエリ文字列に指定`data`されている場合、配列内のパッケージバージョン`1.0.0+metadata`に semver 2.0.0 build メタデータ (など) が含まれている可能性があります。 `semVerLevel=2.0.0`

### <a name="sample-request"></a>要求のサンプル

    GET https://api-v2v3search-0.nuget.org/autocomplete?id=nuget.protocol&prerelease=true

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [autocomplete-version-result.json](./_data/autocomplete-version-result.json)]
