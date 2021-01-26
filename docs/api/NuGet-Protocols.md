---
title: nuget.org プロトコル
description: NuGet クライアントと対話するための進化する nuget.org プロトコル。
author: anangaur
ms.author: anangaur
ms.date: 01/21/2021
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: ea072484c896c4862e47b2c03a1b177f196b0aad
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773979"
---
# <a name="nugetorg-protocols"></a>nuget.org プロトコル

Nuget.org と対話するには、クライアントは特定のプロトコルに従う必要があります。 これらのプロトコルは進化し続けるため、クライアントは、特定の nuget.org Api を呼び出すときに使用するプロトコルのバージョンを識別する必要があります。 これにより、nuget.org は古いクライアントに対して互換性のない方法で変更を加えることができます。

> [!Note]
> このページに記載されている Api は nuget.org に固有のものであり、他の NuGet サーバー実装でこれらの Api を導入することは期待されていません。 

NuGet エコシステム全体で広く実装されている NuGet API の詳細については、 [API の概要](overview.md)に関するトピックを参照してください。

このトピックでは、さまざまなプロトコルが存在する場合に、それらのプロトコルを示します。

## <a name="nuget-protocol-version-410"></a>NuGet プロトコルバージョン4.1.0

4.1.0 プロトコルは、nuget.org 以外のサービスと対話するための検証スコープキーの使用法を指定し、nuget.org アカウントに対してパッケージを検証します。 `4.1.0`バージョン番号は不透明な文字列ですが、このプロトコルをサポートしている公式の NuGet クライアントの最初のバージョンと一致することに注意してください。

検証によって、ユーザーが作成した API キーは nuget.org でのみ使用され、サードパーティのサービスからのその他の検証や検証は、1回限りの使用確認スコープのキーによって処理されます。 これらの検証スコープキーを使用して、パッケージが nuget.org の特定のユーザー (アカウント) に属していることを検証できます。

### <a name="client-requirement"></a>クライアントの要件

クライアントは、API を呼び出して nuget.org にパッケージを **プッシュ** するときに、次のヘッダーを渡す必要があります。

```
X-NuGet-Protocol-Version: 4.1.0
```

ヘッダーのセマンティクスは似てい `X-NuGet-Client-Version` ますが、公式の NuGet クライアントでのみ使用されるように予約されています。 サードパーティのクライアントは、ヘッダーと値を使用する必要があり `X-NuGet-Protocol-Version` ます。

**プッシュ** プロトコル自体については、 [ `PackagePublish` リソース](package-publish-resource.md)のドキュメントを参照してください。

クライアントが外部サービスとやり取りし、パッケージが特定のユーザー (アカウント) に属しているかどうかを検証する必要がある場合、次のプロトコルを使用し、nuget.org からの API キーではなく、検証スコープのキーを使用する必要があります。

### <a name="api-to-request-a-verify-scope-key"></a>検証スコープキーを要求する API

この API は、nuget.org の作成者が所有しているパッケージを検証するための検証スコープキーを取得するために使用されます。

```
POST api/v2/package/create-verification-key/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>要求パラメーター

名前           | /     | Type   | 必須 | Notes
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | はい      | 検証スコープキーが要求されているパッケージの識別子
VERSION        | URL    | string | no       | パッケージのバージョン
X-NuGet-ApiKey | ヘッダー | string | はい      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。

#### <a name="response"></a>応答

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>検証スコープキーを検証する API

この API は、nuget.org の作成者が所有するパッケージの検証スコープキーを検証するために使用されます。

```
GET api/v2/verifykey/{ID}/{VERSION}
```

#### <a name="request-parameters"></a>要求パラメーター

名前           | /     | Type   | 必須 | Notes
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | はい      | スコープの検証キーが要求されたパッケージの識別子
VERSION        | URL    | string | no       | パッケージのバージョン
X-NuGet-ApiKey | ヘッダー | string | はい      | たとえば、`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}` のように指定します。

> [!Note]
> この検証スコープ API キーは、1日の時間に有効期限が切れるか、最初の使用時に、いずれか早い方で期限切れになります。

#### <a name="response"></a>応答

状態コード | 意味
----------- | -------
200         | API キーが有効です
403         | API キーが無効であるか、パッケージに対するプッシュが許可されていません
404         | とによって参照 `ID` されるパッケージ `VERSION` (省略可能) は存在しません
