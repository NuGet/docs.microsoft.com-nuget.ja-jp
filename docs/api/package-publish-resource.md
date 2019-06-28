---
title: プッシュし、削除、NuGet API
description: Publish サービスは、クライアントが新しいパッケージを公開し、一覧から削除または既存のパッケージを削除できます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 6e81055796e20186c5769d2ec39849e6c551ff87
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426722"
---
# <a name="push-and-delete"></a>プッシュし、削除

プッシュ、削除 (またはサーバーの実装によって、一覧から削除) することは、NuGet V3 API を使用してパッケージを一覧に再記載するとします。 これらの操作は無効の基づいて、`PackagePublish`リソースで見つかった、[サービス インデックス](service-index.md)します。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値          | メモ
-------------------- | -----
PackagePublish/2.0.0 | 最初のリリース

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値は、`@id`のプロパティ、`PackagePublish/2.0.0`パッケージ ソースのリソース[サービス インデックス](service-index.md)します。 次のドキュメントでは、nuget.org の URL を使用します。 検討`https://www.nuget.org/api/v2/package`のプレース ホルダーとして、`@id`サービス インデックスにある値。

プロトコルは同じであるために、この URL が、レガシ V2 プッシュ エンドポイントと同じ場所を指しているに注意してください。

## <a name="http-methods"></a>HTTP メソッド

`PUT`、`POST`と`DELETE`HTTP メソッドがこのリソースでサポートされています。 各エンドポイントでは、どのメソッドがサポートされている、次を参照してください。

## <a name="push-a-package"></a>パッケージをプッシュします。

> [!Note]
> nuget.org が[追加要件](NuGet-Protocols.md)プッシュ エンドポイントと対話するためです。

nuget.org には、次の API を使用して新しいパッケージをプッシュがサポートされています。 指定された ID とバージョンでパッケージが既に存在する場合、nuget.org は、プッシュを拒否します。 その他のパッケージ ソースでは、既存のパッケージの置き換えをサポート可能性があります。

    PUT https://www.nuget.org/api/v2/package

### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | string | 可      | 例、`X-NuGet-ApiKey: {USER_API_KEY}`

API キーは、ユーザーがパッケージ ソースから取得し、クライアントに構成されている不透明な文字列です。 特定の文字列形式が必須でありませんが、API キーの長さは、適切な HTTP ヘッダーの値のサイズを超えない必要があります。

### <a name="request-body"></a>要求本文

次の形式で要求本文があります。

#### <a name="multipart-form-data"></a>マルチパート フォーム データ

要求ヘッダー`Content-Type`は`multipart/form-data`要求本文の最初の項目がプッシュされる .nupkg の生バイトとします。 マルチパート ボディ内の後続の項目は無視されます。 ファイルの名前またはマルチパートの項目の他のヘッダーは無視されます。

### <a name="response"></a>応答

状態コード | 説明
----------- | -------
201, 202    | パッケージが正常にプッシュされました
400         | 指定されたパッケージが無効です。
409         | 指定された ID とバージョンを使用してパッケージが既に存在します

サーバーの実装は、パッケージが正常にプッシュされたときに返される成功ステータス コードによって異なります。

## <a name="delete-a-package"></a>パッケージを削除します。

nuget.org にパッケージの削除要求の解釈を「非公開」。 つまり、パッケージは、パッケージの既存のコンシューマーを引き続き使用できますが、パッケージで検索結果で、または web インターフェイスが表示されなくなります。 この方法の詳細については、次を参照してください。、[パッケージの削除](../nuget-org/policies/deleting-packages.md)ポリシー。 その他のサーバーの実装のハード削除としてこのシグナルの解釈、論理的な削除、または一覧から削除することができます。 たとえば、 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (古い V2 API のみをサポートしているサーバー実装) は、一覧からの削除、または構成オプションに基づくハード delete のいずれかとしてこの要求の処理をサポートしています。

    DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 可      | 削除するパッケージの ID
VERSION        | URL    | string | 可      | 削除するパッケージのバージョン
X-NuGet-ApiKey | Header | string | 可      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>応答

状態コード | 説明
----------- | -------
204         | パッケージが削除されました
404         | 指定したパッケージに含まれない`ID`と`VERSION`が存在します。

## <a name="relist-a-package"></a>パッケージ一覧に再記載します。

パッケージが一覧表示されている場合、そのパッケージを「一覧に再記載」エンドポイントを使用して検索結果にもう一度表示されるようにすることです。 このエンドポイントと同じ形には、[削除 (非公開) エンドポイント](#delete-a-package)が使用して、 `POST` HTTP メソッドの代わりに、`DELETE`メソッド。

パッケージが既に表示されている場合でも、要求は成功します。

    POST https://www.nuget.org/api/v2/package/{ID}/{VERSION}

### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 可      | 一覧に再記載するパッケージの ID
VERSION        | URL    | string | 可      | 一覧に再記載するパッケージのバージョン
X-NuGet-ApiKey | Header | string | 可      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`

### <a name="response"></a>応答

状態コード | 説明
----------- | -------
200         | パッケージが表示されます。
404         | 指定したパッケージに含まれない`ID`と`VERSION`が存在します。
