---
title: nuget.org プロトコル
description: NuGet クライアントと対話する進化 nuget.org プロトコル。
author: anangaur
ms.author: anangaur
ms.date: 10/30/2017
ms.topic: conceptual
ms.reviewer: kraigb
ms.openlocfilehash: d0add777040dbb8bcde6d8e385a4feab568e5cdd
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547274"
---
# <a name="nugetorg-protocols"></a>nuget.org プロトコル

Nuget.org をやり取りするには、クライアントは特定のプロトコルに従う必要があります。 これらのプロトコル、進化、ために、クライアントは、特定 nuget.org の Api を呼び出すときに使用するプロトコルのバージョンを識別する必要があります。 これにより、古いクライアントの互換性に影響しない方法で変更を導入する nuget.org ができます。

> [!Note]
> このページに記載されている Api は nuget.org に固有と、これらの Api を導入するその他の NuGet サーバーの実装に対する期待はありません。 

NuGet エコシステム全体で広く実装されている NuGet API については、、 [API の概要](overview.md)を参照してください。

このトピックでは、としてさまざまなプロトコルと存在に来たときに一覧表示します。

## <a name="nuget-protocol-version-410"></a>プロトコルのバージョンの NuGet 4.1.0

4\.1.0 プロトコルを nuget.org には、nuget.org アカウントに対して、パッケージを検証する以外のサービスと対話することを確認スコープのキーの使用量を指定します。 なお、`4.1.0`バージョン数値が不透明な文字列が、このプロトコルがサポートされている公式の NuGet クライアントの最初のバージョンと同時に発生します。

検証では、ユーザーが作成した API キーは、nuget.org でのみ使用され、その他の検証またはサード パーティのサービスからの検証は、1 回だけ使用確認スコープ キーを介して処理されことを確認します。 パッケージを nuget.org で特定のユーザー (アカウント) が属していることを検証することを確認スコープのこれらのキーを使用できます。

### <a name="client-requirement"></a>クライアントの要件

クライアントは、API の呼び出しを行ったときに、次のヘッダーを渡す必要**プッシュ**nuget.org にパッケージ。

    X-NuGet-Protocol-Version: 4.1.0

なお、`X-NuGet-Client-Version`ヘッダーのような意味を持ちますが、公式の NuGet クライアントでのみ使用される予約されています。 サード パーティのクライアントを使用する必要があります、`X-NuGet-Protocol-Version`ヘッダーと値。

**プッシュ**プロトコル自体がドキュメントで説明されている、 [ `PackagePublish`リソース](package-publish-resource.md)します。

クライアントは、外部のサービスおよびパッケージは、特定のユーザー (アカウント) が属しているかどうかを検証する必要があると対話するを次のプロトコルを使用し、使用して、検証スコープ キーと nuget.org から API キーではありません。

### <a name="api-to-request-a-verify-scope-key"></a>API スコープを確認してくださいキーを要求するには

この API を使用して、につきによって所有されているパッケージを検証する nuget.org 作成者のスコープを確認してくださいキーを取得します。

    POST api/v2/package/create-verification-key/{ID}/{VERSION}

#### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------- | ------ | ------ | -------- | -----
ID             | URL    | string | 可      | 確認のスコープのキーを要求する対象のパッケージ identidier
VERSION        | URL    | string | Ｘ       | パッケージのバージョン
X-NuGet-ApiKey | Header | string | 可      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`

#### <a name="response"></a>応答

```json
{
    "Key": "{Verify scope key from nuget.org}",
    "Expires": "{Date}"
}
```

### <a name="api-to-verify-the-verify-scope-key"></a>API を確認のスコープのキーを確認します。

この API は、nuget.org の作成者によって所有されているパッケージの検証スコープ キーの検証に使用されます。

    GET api/v2/verifykey/{ID}/{VERSION}

#### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------  | ------ | ------ | -------- | -----
ID             | URL    | string | 可      | 確認のスコープのキーを要求する対象のパッケージ識別子
VERSION        | URL    | string | Ｘ       | パッケージのバージョン
X-NuGet-ApiKey | Header | string | 可      | たとえば、`X-NuGet-ApiKey: {VERIFY_SCOPE_KEY}`

> [!Note]
> この確認スコープ API キーの有効期限は 1 日の時間または初めて使用する、どちらかに最初に発生します。

#### <a name="response"></a>応答

状態コード | 説明
----------- | -------
200         | API キーは無効です。
403         | API キーが無効であるか、パッケージをプッシュする権限がありません。
404         | によって参照されるパッケージ`ID`と`VERSION`(省略可能) は存在しません
