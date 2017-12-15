---
title: "プッシュ モードと NuGet API を削除します |。Microsoft ドキュメント"
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
ms.assetid: 1eaa403a-5c13-4c05-9352-2f791b98aa7e
description: "発行サービスは、クライアントが新しいパッケージを公開および非公開または既存のパッケージを削除できます。"
keywords: "NuGet API プッシュ パッケージ、パッケージを削除する NuGet API、NuGet API は、パッケージ、NuGet API アップロード パッケージを非公開、API の NuGet パッケージの作成"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 1fa3c0e1698a11208d9ef29fdf26a4980cb60cf5
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="push-and-delete"></a>プッシュ モードと削除

プッシュし削除 (またはサーバーの実装によって、非公開) することは NuGet V3 API を使用してパッケージ化します。
両方の操作は無効の基づいて、`PackagePublish`リソースで見つかった、[サービス インデックス](service-index.md)です。

## <a name="versioning"></a>バージョン管理

次`@type`値を使用します。

@type の値          | メモ
-------------------- | -----
PackagePublish/2.0.0 | 最初のリリース

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値、`@id`のプロパティ、`PackagePublish/2.0.0`パッケージ ソースのリソース[サービス インデックス](service-index.md)です。 次のドキュメントでは、nuget.org の URL が使用されます。 検討`https://www.nuget.org/api/v2/package`のプレース ホルダーとして、`@id`サービス インデックス内の値で見つかった。

プロトコルが同じであるために、この URL がレガシ V2 プッシュ エンドポイントと同じ場所を指していることを注意してください。

## <a name="http-methods"></a>HTTP メソッド

`PUT`と`DELETE`HTTP メソッドは、このリソースでサポートされています。 各エンドポイントでは、どのメソッドがサポートされている、次を参照してください。

## <a name="push-a-package"></a>パッケージをプッシュします。

nuget.org には、次の API を使用してプッシュの新しいパッケージがサポートされています。 指定された ID とバージョンのパッケージが既に存在する場合、nuget.org は、プッシュを拒否します。 他のパッケージ ソースでは、既存のパッケージの交換をサポートできます。

```
PUT https://www.nuget.org/api/v2/package
```

### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | string | 可      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`

API キーは、ユーザーがパッケージ ソースから取得し、クライアントに構成されている非透過の文字列です。 特定の文字列形式が必須でありませんが、API キーの長さは、適切な HTTP ヘッダーの値のサイズを超えない必要があります。

### <a name="request-body"></a>要求本文

要求本文で、次の形式でなければなりません。

#### <a name="multipart-form-data"></a>マルチパート フォーム データ

要求ヘッダー`Content-Type`は`multipart/form-data`要求本文の最初の項目は、これはプッシュされる .nupkg の生のバイトとします。 マルチパート ボディ内の後続の項目は無視されます。 ファイルの名前またはマルチパートの項目の他のヘッダーが無視されます。

### <a name="response"></a>応答

状態コード | 説明
----------- | -------
201, 202    | パッケージが正常にプッシュされます。
400         | 指定したパッケージが正しくありません。
409         | 指定された ID とバージョンを使用してパッケージが既に存在します。

サーバーの実装は、パッケージが正常にプッシュされたときに返される成功ステータス コードによって異なります。

## <a name="delete-a-package"></a>パッケージを削除します。

nuget.org としてパッケージの削除要求では、解釈「非公開」にします。 つまり、パッケージは、パッケージの既存のコンシューマーを引き続き使用できますが、パッケージで検索結果または web インターフェイスが表示されなくなります。 この方法の詳細については、次を参照してください。、[パッケージの削除](../policies/deleting-packages.md)ポリシー。 その他のサーバーの実装では、ハード削除としてこの信号を解釈し、論理削除、または、非公開に解放されます。 たとえば、 [NuGet.Server](https://www.nuget.org/packages/NuGet.Server) (するサーバーの実装だけ古い V2 API をサポート)、unlist または構成オプションに基づくハード delete のいずれかとしてこの要求の処理をサポートしています。

```
DELETE https://www.nuget.org/api/v2/package/{ID}/{VERSION}
```

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
404         | 指定されたパッケージに含まれない`ID`と`VERSION`が存在します。
