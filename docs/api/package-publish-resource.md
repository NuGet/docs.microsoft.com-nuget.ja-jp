---
title: プッシュと削除、NuGet API
description: 発行サービスを使用すると、クライアントは新しいパッケージを公開したり、既存のパッケージを一覧から削除または削除したりできます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 0a79266011433d5adc1341a8e250838988c84d13
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773916"
---
# <a name="push-and-delete"></a>プッシュと削除

サーバーの実装に応じてプッシュ、削除 (または一覧から削除) を実行し、NuGet V3 API を使用してパッケージの一覧を再設定することができます。 これらの操作は、 `PackagePublish` [サービスインデックス](service-index.md)で検出されたリソースに基づいています。

## <a name="versioning"></a>バージョン管理

次の `@type` 値が使用されます。

@type 値          | Notes
-------------------- | -----
PackagePublish/2.0.0 | 最初のリリース

## <a name="base-url"></a>ベース URL

次の Api のベース URL は、 `@id` `PackagePublish/2.0.0` パッケージソースの [サービスインデックス](service-index.md)に含まれるリソースのプロパティの値です。 次のドキュメントでは、nuget の URL が使用されます。 `https://www.nuget.org/api/v2/package` `@id` サービスインデックスで見つかった値のプレースホルダーとして考慮します。

この URL は、プロトコルが同じであるため、従来の V2 プッシュエンドポイントと同じ場所を指していることに注意してください。

## <a name="http-methods"></a>HTTP メソッド

`PUT`、、 `POST` および `DELETE` HTTP メソッドは、このリソースでサポートされています。 各エンドポイントでサポートされるメソッドについては、以下を参照してください。

## <a name="push-a-package"></a>パッケージをプッシュする

> [!Note]
> nuget.org には、プッシュエンドポイントと対話するための [追加の要件](NuGet-Protocols.md) があります。

nuget.org では、次の API を使用した新しいパッケージのプッシュがサポートされています。 指定された ID とバージョンのパッケージが既に存在する場合、nuget.org はプッシュを拒否します。 他のパッケージソースでは、既存のパッケージの置換がサポートされている場合があります。

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>要求パラメーター

名前           | /     | Type   | 必須 | Notes
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | ヘッダー | string | はい      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。

API キーは、ユーザーによってパッケージソースから得られた非透過文字列であり、クライアントに構成されています。 特定の文字列形式は必須ではありませんが、API キーの長さは HTTP ヘッダー値に対して妥当なサイズを超えることはできません。

### <a name="request-body"></a>要求本文

要求本文は次の形式にする必要があります。

#### <a name="multipart-form-data"></a>マルチパート フォーム データ

要求ヘッダーはで、 `Content-Type` `multipart/form-data` 要求本文の最初の項目は、の未加工のバイトです。 nupkg プッシュされます。 マルチパート本体の後続の項目は無視されます。 ファイル名またはマルチパート項目のその他のヘッダーは無視されます。

### <a name="response"></a>応答

状態コード | 意味
----------- | -------
201、202    | パッケージが正常にプッシュされました
400         | 指定されたパッケージは無効です
409         | 指定された ID とバージョンのパッケージは既に存在します

サーバーの実装は、パッケージが正常にプッシュされたときに返される成功状態コードによって異なります。

## <a name="delete-a-package"></a>パッケージを削除する

nuget.org は、"一覧から削除" としてパッケージの削除要求を解釈します。 つまり、パッケージの既存のコンシューマーはパッケージを引き続き使用できますが、パッケージは検索結果または web インターフェイスに表示されなくなります。 このプラクティスの詳細については、「 [削除されたパッケージ](../nuget-org/policies/deleting-packages.md) ポリシー」を参照してください。 その他のサーバー実装では、この信号をハード削除、論理的な削除、または一覧から削除として解釈できます。 たとえば、Nuget.exe (以前の V2 API のみをサポートするサーバー実装) は、この要求を構成オプションに基づいて一覧から削除またはハード削除として処理することをサポートしています[。](https://www.nuget.org/packages/NuGet.Server)

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>要求パラメーター

名前           | /     | Type   | 必須 | Notes
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | はい      | 削除するパッケージの ID
VERSION        | URL    | string | はい      | 削除するパッケージのバージョン
X-NuGet-ApiKey | ヘッダー | string | はい      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。

### <a name="response"></a>応答

状態コード | 意味
----------- | -------
204         | パッケージが削除されました
404         | 指定された `ID` と `VERSION` 存在するパッケージはありません

## <a name="relist-a-package"></a>パッケージを一覧に再記載する

パッケージが一覧から削除されている場合は、"relist" エンドポイントを使用して、そのパッケージが検索結果に再び表示されるようにすることができます。 このエンドポイントには、 [delete (一覧から削除) エンドポイント](#delete-a-package) と同じ図形がありますが、 `POST` メソッドの代わりに HTTP メソッドが使用され `DELETE` ます。

パッケージが既に表示されている場合でも、要求は成功します。

```
POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

### <a name="request-parameters"></a>要求パラメーター

名前           | /     | Type   | 必須 | Notes
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | はい      | 再一覧表示するパッケージの ID
VERSION        | URL    | string | はい      | 再一覧表示するパッケージのバージョン
X-NuGet-ApiKey | ヘッダー | string | はい      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。

### <a name="response"></a>応答

状態コード | 意味
----------- | -------
200         | パッケージが表示されるようになりました。
404         | 指定された `ID` と `VERSION` 存在するパッケージはありません
