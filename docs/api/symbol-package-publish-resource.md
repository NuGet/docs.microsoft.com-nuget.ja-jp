---
title: プッシュシンボルパッケージ、NuGet API |Microsoft Docs
author: cristinamanum
ms.author:
- cmanu
- kraigb
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: 発行サービスにより、クライアントは新しいシンボルパッケージを発行できます。
keywords: NuGet API プッシュシンボルパッケージ
ms.reviewer: karann
ms.openlocfilehash: 27e557bf15ce31152243a409eddc4112eeb6c38b
ms.sourcegitcommit: ac9a00ccaf90e539a381e92b650074910b21eb0d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/03/2019
ms.locfileid: "70235109"
---
# <a name="push-symbol-packages"></a>シンボルパッケージのプッシュ

NuGet V3 API を使用してシンボルパッケージ ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) をプッシュすることができます。
これらの操作は、 `SymbolPackagePublish` [サービスインデックス](service-index.md)で検出されたリソースに基づいています。

## <a name="versioning"></a>バージョン管理

次`@type`の値が使用されます。

@type の値                 | メモ
--------------------        | -----
シンボル Packagepublish/4.9.0-  | 最初のリリース

## <a name="base-url"></a>[基本 URL]

次の api のベース URL は、パッケージソースの`@id` [サービスインデックス](service-index.md)に含ま`SymbolPackagePublish/4.9.0`れるリソースのプロパティの値です。 次のドキュメントでは、nuget の URL が使用されます。 サービス`https://www.nuget.org/api/v2/symbolpackage`インデックスで見つかった`@id`値のプレースホルダーとして考慮します。

## <a name="http-methods"></a>HTTP メソッド

この`PUT`リソースでは、HTTP メソッドがサポートされています。 

## <a name="push-a-symbol-package"></a>シンボルパッケージをプッシュする

nuget.org では、次の API を使用した新しいシンボルパッケージ形式 ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) のプッシュがサポートされています。 

    PUT https://www.nuget.org/api/v2/symbolpackage

同じ ID とバージョンのシンボルパッケージは、複数回送信できます。 シンボルパッケージは、次の場合には拒否されます。
- 同じ ID とバージョンのパッケージが存在しません。
- 同じ ID とバージョンのシンボルパッケージがプッシュされましたが、まだ発行されていません。
- シンボルパッケージ ([snupkg](../create-packages/Symbol-Packages-snupkg.md)) が無効です (「[シンボルパッケージの制約](../create-packages/Symbol-Packages-snupkg.md)」を参照してください)。

### <a name="request-parameters"></a>要求パラメーター

名前           | イン     | 型   | 必須 | メモ
-------------- | ------ | ------ | -------- | -----
X-NuGet-ApiKey | Header | string | 可      | 例、`X-NuGet-ApiKey: {USER_API_KEY}`

API キーは、ユーザーによってパッケージソースから得られた非透過文字列であり、クライアントに構成されています。 特定の文字列形式は必須ではありませんが、API キーの長さは HTTP ヘッダー値に対して妥当なサイズを超えることはできません。

### <a name="request-body"></a>要求本文

シンボルプッシュの要求本文は、パッケージプッシュ要求の要求本文と同じです (「[パッケージプッシュと削除](package-publish-resource.md)」を参照してください)。 

### <a name="response"></a>応答

状態コード | 説明
----------- | -------
201         | シンボルパッケージが正常にプッシュされました。
400         | 指定されたシンボルパッケージは無効です。
401         | この操作を実行する権限がユーザーにありません。
404         | 指定された ID とバージョンの対応するパッケージが存在しません。
409         | 指定された ID とバージョンのシンボルパッケージはプッシュされましたが、まだ使用できません。
413         | パッケージが大きすぎます。

