---
title: シンボル パッケージを NuGet API をプッシュ |Microsoft Docs
author:
- cristinamanum
- kraigb
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 発行サービスは、新しいシンボル パッケージを公開するクライアントを使用します。
keywords: NuGet API プッシュ シンボル パッケージ
ms.reviewer: karann
ms.openlocfilehash: 514ab3683db81da5b2220b005b8b39f1fec8300d
ms.sourcegitcommit: ffbdf147f84f8bd60495d3288dff9a5275491c17
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/13/2018
ms.locfileid: "51580415"
---
# <a name="push-symbol-packages"></a>シンボル パッケージをプッシュします。

シンボル パッケージをプッシュすることができます ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) NuGet V3 API を使用します。
これらの操作は無効の基づいて、`SymbolPackagePublish`リソースで見つかった、[サービス インデックス](service-index.md)します。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                 | メモ
--------------------        | -----
SymbolPackagePublish/4.9.0  | 最初のリリース

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値は、`@id`のプロパティ、`SymbolPackagePublish/4.9.0`パッケージ ソースのリソース[サービス インデックス](service-index.md)します。 次のドキュメントでは、nuget.org の URL を使用します。 検討`https://www.nuget.org/api/v2/symbolpackage`のプレース ホルダーとして、`@id`サービス インデックスにある値。

## <a name="http-methods"></a>HTTP メソッド

`PUT` HTTP メソッドがこのリソースでサポートされています。 

## <a name="push-a-symbol-package"></a>シンボル パッケージをプッシュします。

nuget.org にプッシュの新しいシンボル パッケージ形式がサポートしています ([snupkg](../create-packages/Symbol-Packages-snupkg.md))、次の API を使用します。 

    PUT https://www.nuget.org/api/v2/symbolpackage

シンボル パッケージ ID とバージョンが同じでは、複数回送信できます。 シンボル パッケージは、次の場合に拒否されます。
- 同じ ID とバージョンを使用してパッケージが存在しません。
- シンボル パッケージ ID とバージョンが同じでは、プッシュされたが、まだ公開されていません。
- シンボル パッケージ ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) が無効です (を参照してください[シンボル パッケージ制約](../create-packages/Symbol-Packages-snupkg.md))。

### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | string | 可      | たとえば、`X-NuGet-ApiKey: {USER_API_KEY}`

API キーは、ユーザーがパッケージ ソースから取得し、クライアントに構成されている不透明な文字列です。 特定の文字列形式が必須でありませんが、API キーの長さは、適切な HTTP ヘッダーの値のサイズを超えない必要があります。

### <a name="request-body"></a>要求本文

シンボルのプッシュの要求本文は、パッケージのプッシュ要求の要求の本体と同じ (を参照してください[プッシュをパッケージ化し、削除](package-publish-resource.md))。 

### <a name="response"></a>応答

状態コード | 説明
----------- | -------
201         | シンボル パッケージが正常にプッシュされました。
400         | 指定されたシンボル パッケージが無効です。
401         | ユーザーは、この操作を実行する権限がありません。
404         | 指定された ID とバージョンを使用して対応するパッケージが存在しません。
409         | 指定された ID とバージョンで、シンボル パッケージのプッシュが、これはまだ利用できません。
413         | パッケージが大きすぎます。

