---
title: NuGet API、パッケージの内容
description: パッケージのベース アドレスは、パッケージ自体を取得するための単純なインターフェイスです。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 740defc34077793b81fb35db73a2eee393ae3bac
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547155"
---
# <a name="package-content"></a>パッケージのコンテンツ

V3 API を使用して、任意のパッケージのコンテンツ (.nupkg ファイル) をフェッチする URL を生成することになります。 パッケージのコンテンツを取得するために使用されるリソースは、`PackageBaseAddress`リソースで見つかった、[サービス インデックス](service-index.md)します。 このリソースも表示されているパッケージのすべてのバージョンの探索を有効にまたは一覧から削除されました。

このリソースが、いずれかの"パッケージ ベース アドレスとして"または"フラット container"よくと呼ばれます。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値              | メモ
------------------------ | -----
PackageBaseAddress/3.0.0 | 最初のリリース

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値は、`@id`前述のリソースに関連付けられたプロパティ`@type`値。 次のドキュメントで、プレース ホルダーのベース URL`{@id}`使用されます。

## <a name="http-methods"></a>HTTP メソッド

HTTP メソッドの登録のリソースのサポートで検出されたすべての Url`GET`と`HEAD`します。

## <a name="enumerate-package-versions"></a>パッケージのバージョンを列挙します。

クライアントがパッケージ ID を知っているし、するパッケージのバージョンのパッケージを検出したい場合は、ソースで使用できるように、クライアントは、すべてのパッケージ バージョンを列挙するために予測可能な URL を構築できます。 この一覧は「ディレクトリの一覧」をパッケージのコンテンツ api を以下に説明したもの。

> [!Note]
> この一覧には、両方の一覧と一覧にないパッケージのバージョンが含まれています。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求パラメーター

名前     | イン     | 型    | 必須 | メモ
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 可      | パッケージ ID、小文字

`LOWER_ID`値は小文字で実装されたルールを使用して、目的のパッケージ ID。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。

### <a name="response"></a>応答

指定されたパッケージ ID のバージョンのパッケージ ソースがない場合は、404 状態コードが返されます。

パッケージ ソースに 1 つまたは複数のバージョンがある場合は、200 ステータス コードが返されます。 応答本文では、次のプロパティを持つ JSON オブジェクトです。

名前     | 種類             | 必須 | メモ
-------- | ---------------- | -------- | -----
バージョン | 文字列の配列 | 可      | パッケージに使用できる Id

内の文字列、`versions`配列はすべて小文字、 [NuGet バージョン文字列を正規化](../reference/package-versioning.md#normalized-version-numbers)します。 バージョン文字列では、SemVer 2.0.0 ビルド メタデータは含まれません。

この配列内で見つかったバージョン文字列をそのまま使用できることが目的の`LOWER_VERSION`のトークンが、次のエンドポイント。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>パッケージ コンテンツ (.nupkg) のダウンロードします。

のみ、クライアントがパッケージ ID とバージョンを把握してパッケージ コンテンツをダウンロードする必要がある場合、次の URL を作成する必要があります。

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>要求パラメーター

名前          | イン     | 型   | 必須 | メモ
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 可      | パッケージ ID、小文字
LOWER_VERSION | URL    | string | 可      | パッケージのバージョンが正規化され、小文字

両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用しては小文字です。NET [`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)
メソッドをオーバーライドします。

`LOWER_VERSION`目的のパッケージ バージョン正規化は、NuGet のバージョンを使用して[正規化ルール](../reference/package-versioning.md#normalized-version-numbers)します。 つまり、SemVer 2.0.0 仕様によって許可されているビルド メタデータをここで除外する必要があります。

### <a name="response-body"></a>応答本文

パッケージ ソースで、パッケージが存在する場合は、200 ステータス コードが返されます。 応答本文は、パッケージ コンテンツ自体になります。

パッケージ ソースのパッケージが存在しない場合は 404 状態コードが返されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>応答のサンプル

Newtonsoft.Json 9.0.1 の .nupkg をあるバイナリ ストリーム。

## <a name="download-package-manifest-nuspec"></a>パッケージ マニフェスト (.nuspec) のダウンロードします。

のみクライアントがパッケージ ID とバージョンを把握して、パッケージ マニフェストをダウンロードする場合、次の URL を作成する必要があります。

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>要求パラメーター

名前          | イン     | 型    | 必須 | メモ
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | string  | 可      | パッケージ ID、小文字
LOWER_VERSION | URL    | 整数 | 可      | パッケージのバージョンが正規化され、小文字

両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用しては小文字です。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。

`LOWER_VERSION`目的のパッケージ バージョン正規化は、NuGet のバージョンを使用して[正規化ルール](../reference/package-versioning.md#normalized-version-numbers)します。 つまり、SemVer 2.0.0 仕様によって許可されているビルド メタデータをここで除外する必要があります。

### <a name="response-body"></a>応答本文

パッケージ ソースで、パッケージが存在する場合は、200 ステータス コードが返されます。 応答本文は、これは、対応する .nupkg に含まれている .nuspec パッケージ マニフェストになります。 .Nuspec は、XML ドキュメントです。

パッケージ ソースのパッケージが存在しない場合は 404 状態コードが返されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>応答のサンプル

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
