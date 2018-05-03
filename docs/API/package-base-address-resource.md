---
title: パッケージのコンテンツを NuGet API
description: パッケージのベース アドレスは、パッケージ自体をフェッチするための単純なインターフェイスです。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a6ac40368f30d33f35d4ca0b6cc18ce4bd6efee5
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="package-content"></a>パッケージの内容

V3 API を使用して任意のパッケージのコンテンツ (これは .nupkg ファイル) をフェッチする URL を生成することができます。 パッケージの内容をフェッチするために使用されるリソースは、`PackageBaseAddress`リソースで見つかった、[サービス インデックス](service-index.md)です。 このリソースに表示される、パッケージのすべてのバージョンの探索を有効にも一覧にないか。

このリソースはいずれかの"パッケージ ベース アドレスとして"または「フラット コンテナー」として一般的に呼ばれます。

## <a name="versioning"></a>バージョン管理

次`@type`値を使用します。

@type の値              | メモ
------------------------ | -----
PackageBaseAddress/3.0.0 | 最初のリリース

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値、`@id`前述のリソースに関連付けられたプロパティ`@type`値。 次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。

## <a name="http-methods"></a>HTTP メソッド

HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。

## <a name="enumerate-package-versions"></a>パッケージのバージョンを列挙します。

場合は、クライアントがパッケージ ID を知っているし、するパッケージのバージョンのパッケージを検出するソースが利用可能なクライアントは、すべてのパッケージ バージョンを列挙する予測可能な URL を構築できます。 この一覧は目的として「ディレクトリの一覧」パッケージのコンテンツ api 以下に説明します。

> [!Note]
> この一覧には、両方の一覧表示され、一覧にないパッケージ バージョンが含まれています。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求パラメーター

名前     | イン     | 型    | 必須 | メモ
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 可      | パッケージ ID、小文字

`LOWER_ID`値は小文字によって実装される規則を使用して、目的のパッケージ ID。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。

### <a name="response"></a>応答

指定されたパッケージ ID のバージョンのパッケージ ソースがない場合は、状態コード 404 が返されます。

パッケージ ソースに 1 つまたは複数のバージョンがある場合は、200 ステータス コードが返されます。 応答本文は、次のプロパティを使用して、JSON オブジェクトを示します。

名前     | 種類             | 必須 | メモ
-------- | ---------------- | -------- | -----
バージョン | 文字列の配列 | 可      | パッケージに使用できる Id

内の文字列、`versions`配列は、すべて小文字、 [NuGet のバージョン文字列を正規化](../reference/package-versioning.md#normalized-version-numbers)です。 バージョン文字列では、SemVer 2.0.0 ビルド メタデータは含まれません。

この配列内で見つかったバージョン文字列をそのまま使用することができますが、目的、`LOWER_VERSION`のトークンが、次のエンドポイント。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/owin/index.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-base-address-index.json](./_data/package-base-address-index.json)]

## <a name="download-package-content-nupkg"></a>パッケージのコンテンツ (これは .nupkg) のダウンロードします。

のみ、クライアントがパッケージ ID とバージョンを把握して、パッケージ コンテンツをダウンロードする場合は、それらを次の URL を構築する必要があります。

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.{LOWER_VERSION}.nupkg

### <a name="request-parameters"></a>要求パラメーター

名前          | イン     | 型   | 必須 | メモ
------------- | ------ | ------ | -------- | -----
LOWER_ID      | URL    | string | 可      | パッケージ ID、小文字
LOWER_VERSION | URL    | string | 可      | パッケージのバージョンが正規化され、小文字

両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用している小文字です。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。

`LOWER_VERSION`目的のパッケージのバージョンを使用して正規化 NuGet のバージョン[正規化規則](../reference/package-versioning.md#normalized-version-numbers)です。 つまり、SemVer 2.0.0 の仕様によって許可されているメタデータをビルドするをここでは除外する必要があります。

### <a name="response-body"></a>応答本文

パッケージがパッケージ ソースに存在する場合は、200 ステータス コードが返されます。 応答本文は、パッケージのコンテンツそのものになります。

パッケージがパッケージ ソースに存在しない場合は、状態コード 404 が返されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/9.0.1/newtonsoft.json.9.0.1.nupkg

### <a name="sample-response"></a>応答のサンプル

これは、Newtonsoft.Json 9.0.1 の .nupkg であるバイナリ ストリーム。

## <a name="download-package-manifest-nuspec"></a>パッケージ マニフェスト (.nuspec) をダウンロードします。

のみ、クライアントがパッケージ ID とバージョンを把握して、パッケージ マニフェストをダウンロードする場合は、それらを次の URL を構築する必要があります。

    GET {@id}/{LOWER_ID}/{LOWER_VERSION}/{LOWER_ID}.nuspec

### <a name="request-parameters"></a>要求パラメーター

名前          | イン     | 型    | 必須 | メモ
------------- | ------ | ------- | -------- | -----
LOWER_ID      | URL    | string  | 可      | パッケージ ID、小文字
LOWER_VERSION | URL    | 整数 | 可      | パッケージのバージョンが正規化され、小文字

両方`LOWER_ID`と`LOWER_VERSION`によって実装される規則を使用している小文字です。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッドです。

`LOWER_VERSION`目的のパッケージのバージョンを使用して正規化 NuGet のバージョン[正規化規則](../reference/package-versioning.md#normalized-version-numbers)です。 つまり、SemVer 2.0.0 の仕様によって許可されているメタデータをビルドするをここでは除外する必要があります。

### <a name="response-body"></a>応答本文

パッケージがパッケージ ソースに存在する場合は、200 ステータス コードが返されます。 応答本文は、パッケージ マニフェストでは、これは、対応する .nupkg に含まれている .nuspec になります。 .Nuspec は、XML ドキュメントです。

パッケージがパッケージ ソースに存在しない場合は、状態コード 404 が返されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3-flatcontainer/newtonsoft.json/6.0.4/newtonsoft.json.nuspec

### <a name="sample-response"></a>応答のサンプル

[!code-XML [newtonsoft.json.6.0.4.xml](./_data/newtonsoft.json.6.0.4.xml)]
