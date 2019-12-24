---
title: パッケージコンテンツ, NuGet API
description: パッケージのベースアドレスは、パッケージ自体をフェッチするための単純なインターフェイスです。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 7aea28d6224a89149aa33be035c82a45db3058f0
ms.sourcegitcommit: 1eda83ab537c86cc27316e7bc67f95a358766e63
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/18/2019
ms.locfileid: "71094121"
---
# <a name="package-content"></a>パッケージコンテンツ

V3 API を使用して、任意のパッケージのコンテンツ (nupkg ファイル) を取得するための URL を生成することができます。 パッケージコンテンツのフェッチに使用されるリソース`PackageBaseAddress`は、[サービスインデックス](service-index.md)で見つかったリソースです。 また、このリソースにより、パッケージのすべてのバージョンの検出、一覧表示、または一覧からの削除が可能になります。

このリソースは、一般に "パッケージベースアドレス" または "フラットコンテナー" と呼ばれます。

## <a name="versioning"></a>バージョン管理

次`@type`の値が使用されます。

@type の値              | メモ
------------------------ | -----
PackageBaseAddress/3.0.0 | 最初のリリース

## <a name="base-url"></a>[基本 URL]

次の api のベース URL は、前述のリソース`@id` `@type`値に関連付けられているプロパティの値です。 次のドキュメントでは、プレースホルダーのベース`{@id}` URL が使用されます。

## <a name="http-methods"></a>HTTP メソッド

登録リソースで見つかったすべての url は、HTTP `GET`メソッド`HEAD`とをサポートしています。

## <a name="enumerate-package-versions"></a>パッケージバージョンの列挙

クライアントがパッケージ ID を認識し、パッケージソースに使用可能なパッケージバージョンを検出する必要がある場合、クライアントは、すべてのパッケージバージョンを列挙するための予測可能な URL を作成できます。 このリストは、以下で説明するパッケージコンテンツ API の "ディレクトリリスト" として使用することを目的としています。

> [!Note]
> この一覧には、一覧表示され、一覧にないパッケージバージョンの両方が含まれます。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求パラメーター

名前     | イン     | 型    | 必須 | メモ
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 可      | パッケージ ID、小文字

この`LOWER_ID`値は、によって実装されたルールを使用して、必要なパッケージ ID を小文字にしたものです。NET の[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。

### <a name="response"></a>応答

パッケージソースに提供されているパッケージ ID のバージョンがない場合は、404状態コードが返されます。

パッケージソースに1つ以上のバージョンがある場合は、200状態コードが返されます。 応答本文は、次のプロパティを持つ JSON オブジェクトです。

Name     | 種類             | 必須 | メモ
-------- | ---------------- | -------- | -----
versions | 文字列の配列 | 可      | 使用可能なバージョン

`versions`配列内の文字列は、すべて小文字で正規化された[NuGet バージョン文字列](../concepts/package-versioning.md#normalized-version-numbers)です。 バージョン文字列に SemVer 2.0.0 ビルドメタデータが含まれていません。

目的は、この配列で見つかったバージョン文字列を、次のエンドポイントに`LOWER_VERSION`あるトークンに対して逐語的に使用できることです。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>パッケージコンテンツのダウンロード (. nupkg)

クライアントがパッケージ ID とバージョンを認識し、パッケージコンテンツをダウンロードする必要がある場合は、次の URL を構築するだけで済みます。

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>要求パラメーター

名前          | イン     | 型   | 必須 | メモ
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 可      | パッケージ ID、小文字
LOWER_VERSION | URL    | string | 可      | パッケージのバージョン、正規化、および小文字

`LOWER_ID` と`LOWER_VERSION`はどちらも、によって実装される規則を使用した小文字です。NET の[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
メソッドをオーバーライドします。

は`LOWER_VERSION` 、NuGet のバージョン[正規化規則](../concepts/package-versioning.md#normalized-version-numbers)を使用して正規化された、必要なパッケージバージョンです。 これは、この場合、SemVer 2.0.0 仕様で許可されているビルドメタデータを除外する必要があることを意味します。

### <a name="response-body"></a>応答本文

パッケージがパッケージソースに存在する場合は、200状態コードが返されます。 応答本文は、パッケージコンテンツ自体になります。

パッケージがパッケージソースに存在しない場合は、404状態コードが返されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>応答のサンプル

. Nupkg (Newtonsoft. Json の 9.0.1) のバイナリストリーム。

## <a name="download-package-manifest-nuspec"></a>パッケージマニフェストのダウンロード (. nuspec)

クライアントがパッケージ ID とバージョンを認識し、パッケージマニフェストをダウンロードする必要がある場合は、次の URL を構築するだけで済みます。

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>要求パラメーター

名前          | イン     | 型   | 必須 | メモ
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 可      | パッケージ ID、小文字
LOWER_VERSION | URL    | string | 可      | パッケージのバージョン、正規化、および小文字

`LOWER_ID` と`LOWER_VERSION`はどちらも、によって実装される規則を使用した小文字です。NET の[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。

は`LOWER_VERSION` 、NuGet のバージョン[正規化規則](../concepts/package-versioning.md#normalized-version-numbers)を使用して正規化された、必要なパッケージバージョンです。 これは、この場合、SemVer 2.0.0 仕様で許可されているビルドメタデータを除外する必要があることを意味します。

### <a name="response-body"></a>応答本文

パッケージがパッケージソースに存在する場合は、200状態コードが返されます。 応答本文はパッケージマニフェストになります。これは、対応する. nupkg に含まれている nuspec です。 Nuspec は XML ドキュメントです。

パッケージがパッケージソースに存在しない場合は、404状態コードが返されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>応答のサンプル

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
