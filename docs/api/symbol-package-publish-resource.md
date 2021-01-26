---
title: プッシュシンボルパッケージ、NuGet API |Microsoft Docs
author: cristinamanum
ms.author: cmanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 発行サービスにより、クライアントは新しいシンボルパッケージを発行できます。
keywords: NuGet API プッシュシンボルパッケージ
ms.reviewer: karann
ms.openlocfilehash: 91bb4c9ca77fd7f1ff35831e02eb4f9d65d641c5
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98773894"
---
# <a name="push-symbol-packages"></a>シンボルパッケージのプッシュ

NuGet V3 API を使用してシンボルパッケージ ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) をプッシュすることができます。
これらの操作は、 `SymbolPackagePublish` [サービスインデックス](service-index.md)で検出されたリソースに基づいています。

## <a name="versioning"></a>バージョン管理

次の `@type` 値が使用されます。

@type 値                 | Notes
--------------------        | -----
シンボル Packagepublish/4.9.0-  | 最初のリリース

## <a name="base-url"></a>ベース URL

次の Api のベース URL は、 `@id` `SymbolPackagePublish/4.9.0` パッケージソースの [サービスインデックス](service-index.md)に含まれるリソースのプロパティの値です。 次のドキュメントでは、nuget の URL が使用されます。 `https://www.nuget.org/api/v2/symbolpackage` `@id` サービスインデックスで見つかった値のプレースホルダーとして考慮します。

## <a name="http-methods"></a>HTTP メソッド

`PUT`このリソースでは、HTTP メソッドがサポートされています。 

## <a name="push-a-symbol-package"></a>シンボルパッケージをプッシュする

nuget.org では、次の API を使用した新しいシンボルパッケージ形式 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) のプッシュがサポートされています。 

```
PUT https://www.nuget.org/api/v2/symbolpackage
```

同じ ID とバージョンのシンボルパッケージは、複数回送信できます。 シンボルパッケージは、次の場合には拒否されます。
- 同じ ID とバージョンのパッケージが存在しません。
- 同じ ID とバージョンのシンボルパッケージがプッシュされましたが、まだ発行されていません。
- シンボルパッケージ ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) が無効です (「 [シンボルパッケージの制約](../create-packages/Symbol-Packages-snupkg.md)」を参照してください)。

### <a name="request-parameters"></a>要求パラメーター

名前           | /     | Type   | 必須 | Notes
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | ヘッダー | string | はい      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}` のように指定します。

API キーは、ユーザーによってパッケージソースから得られた非透過文字列であり、クライアントに構成されています。 特定の文字列形式は必須ではありませんが、API キーの長さは HTTP ヘッダー値に対して妥当なサイズを超えることはできません。

### <a name="request-body"></a>要求本文

シンボルプッシュの要求本文は、パッケージプッシュ要求の要求本文と同じです (「 [パッケージプッシュと削除](package-publish-resource.md)」を参照してください)。 

### <a name="response"></a>応答

状態コード | 意味
----------- | -------
201         | シンボルパッケージが正常にプッシュされました。
400         | 指定されたシンボルパッケージは無効です。
401         | この操作を実行する権限がユーザーにありません。
404         | 指定された ID とバージョンの対応するパッケージが存在しません。
409         | 指定された ID とバージョンのシンボルパッケージはプッシュされましたが、まだ使用できません。
413         | パッケージが大きすぎます。

