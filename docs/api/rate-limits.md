---
title: レート制限、NuGet API
description: NuGet Api で、不正使用を防ぐために転送率の制限が適用されたされます。
author: cmanu
ms.author: cmanu
ms.date: 03/20/2018
ms.topic: reference
ms.reviewer:
- skofman
- anangaur
- kraigb
ms.openlocfilehash: 70b478ae17cd10b17f9d6ecb0f5776c1effcea58
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548678"
---
# <a name="rate-limits"></a>速度の制限

NuGet.org の API は、不正使用を防ぐレートの制限を適用します。 レート制限を超える要求には、次のエラーが返されます。 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

要求の調整も、レート制限、一部の Api を使用するだけでなく、クォータを適用します。 クォータを超える要求には、次のエラーが返されます。

  ~~~
    {
      "statusCode": 403,
      "message": "Quota exceeded."
    }
  ~~~

次の表では、NuGet.org の API のレート制限を一覧表示します。

## <a name="package-search"></a>パッケージの検索

> [!Note]
> NuGet.org の使用をお勧め[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)現在はパフォーマンスの高いを持たない検索の制限します。 V1 と V2 の search Api、followins 制限が適用されます。


| API | 制限の種類 | 制限値 | API のユースケース |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000/分 | V1 の OData を使用して NuGet パッケージのメタデータを照会`Packages`コレクション |
**GET** `/api/v1/Search()` | IP | 3000/分 | V1 Search エンドポイント経由での NuGet パッケージを検索します。 | 
**GET** `/api/v2/Packages` | IP | 20000/分 | V2 の OData を使用して NuGet パッケージのメタデータを照会`Packages`コレクション | 
**GET** `/api/v2/Packages/$count` | IP | 100/分 | V2 の OData を使用して NuGet パッケージの数を照会`Packages`コレクション | 

## <a name="package-push-and-unlist"></a>パッケージをプッシュし、一覧から削除します。

| API | 制限の種類 | 制限値 | API のユースケース | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API キー | 250/時間 | V2 プッシュ エンドポイントを経由して、新しい NuGet パッケージ (バージョン) をアップロードします。 
**DELETE** `/api/v2/package/{id}/{version}` | API キー | 250/時間 | V2 エンドポイントを使用して NuGet パッケージ (バージョン) を一覧から削除します。 
