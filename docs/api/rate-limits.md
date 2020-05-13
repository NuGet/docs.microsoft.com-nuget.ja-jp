---
title: レート制限、NuGet API
description: NuGet Api では、誤用を防ぐためにレート制限が適用されます。
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 372304255bf8849693947b22539e012ccdd48966
ms.sourcegitcommit: 0a63956bf12aaf1b1b45e680bc8e90f97347988c
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/13/2020
ms.locfileid: "83367935"
---
# <a name="rate-limits"></a>速度の制限

NuGet.org API は、誤用を防ぐためにレート制限を適用します。 転送率の制限を超える要求では、次のエラーが返されます。 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

レート制限を使用した要求の調整に加えて、一部の Api もクォータを適用します。 クォータを超える要求では、次のエラーが返されます。

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

次の表は、NuGet.org API のレート制限を示しています。

## <a name="package-search"></a>パッケージの検索

> [!Note]
> 現在、レートが制限されていないため、NuGet の[V3 検索 api](search-query-service-resource.md)を使用することをお勧めします。 V1 と V2 の検索 Api では、次の制限が適用されます。

| API | 制限の種類 | 制限値 | API ユースケース |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000/分 | V1 OData コレクションを使用した NuGet パッケージメタデータのクエリ `Packages` |
**GET** `/api/v1/Search()` | IP | 3000/分 | V1 検索エンドポイント経由で NuGet パッケージを検索する | 
**GET** `/api/v2/Packages` | IP | 2万/分 | V2 OData コレクションを使用した NuGet パッケージメタデータのクエリ `Packages` | 
**GET** `/api/v2/Packages/$count` | IP | 100/分 | V2 OData コレクションを使用した NuGet パッケージ数の照会 `Packages` | 

## <a name="package-push-and-unlist"></a>Package Push and 一覧から削除

| API | 制限の種類 | 制限値 | API ユースケース | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API キー | 350/時間 | V2 プッシュエンドポイント経由で新しい NuGet パッケージ (バージョン) をアップロードする 
**削除**`/api/v2/package/{id}/{version}` | API キー | 250/時間 | V2 エンドポイントを使用した NuGet パッケージ (バージョン) の一覧から削除 

## <a name="nugetorg-website-page-views"></a>nuget.org web サイトのページビュー

プログラムによって nuget.org web ページにアクセスする場合は、ドキュメント化された[V3 api](overview.md)を調査することを検討してください。 これらのエンドポイントを使用すると、パッケージのメタデータとコンテンツに簡単にアクセスできます。 V3 API は可用性が向上し、web ブラウザーとの対話用に設計された NuGet ギャラリー web ページにアクセスするよりもパフォーマンスが向上しています。

| API | 制限の種類 | 制限値 | API ユースケース | 
|:---|:---|:---|:--- |
**GET** `/package/{id}/{version}` | IP | 50/分 | [パッケージ (バージョン) の詳細] ページを表示します。 
