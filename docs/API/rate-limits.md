---
title: 転送率の制限値 |Microsoft ドキュメント
author:
- cmanu
- anangaur
ms.author:
- cmanu
manager: skofman
ms.date: 03/20/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: NuGet Api によって、不正使用を防ぐために転送率の制限が適用されたされます。
keywords: NuGet API、率を制限します。
ms.reviewer:
- skofman
- anangaur
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: f7891d5e4c008219d9f4808f223f3e5e7ae06ced
ms.sourcegitcommit: fa40be739d093a37d5f7072b62ebdb4f595f4110
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/30/2018
---
# <a name="rate-limits"></a>速度の制限

NuGet.org API は、不正使用を防ぐためのレート制限を強制します。 レート制限を超える要求は、次のエラーを返します。 

  ~~~
    {
      "statusCode": 429,
      "message": "Rate limit is exceeded. Try again in 56 seconds."
    }
  ~~~

次の表では、NuGet.org API の転送率の制限が一覧表示します。

## <a name="package-search"></a>パッケージの検索

> [!Note]
> NuGet.org の使用をお勧め[V3 Api](https://docs.microsoft.com/nuget/api/search-query-service-resource)現在検索パフォーマンスの高いは、いずれかがないことを制限します。 V1 と V2 の検索 Api、followins 制限を適用します。


| API | 制限の種類 | 制限値 | API usecase |
|:---|:---|:---|:---|
**GET** `/api/v1/Packages` | IP | 1000/分 | V1 の OData を使用して NuGet パッケージのメタデータを照会する`Packages`コレクション |
**GET** `/api/v1/Search()` | IP | 3000/分 | V1 検索 endpoint を使用して NuGet パッケージの検索 | 
**GET** `/api/v2/Packages` | IP | 20000/分 | V2 の OData を使用して NuGet パッケージのメタデータを照会する`Packages`コレクション | 
**GET** `/api/v2/Packages/$count` | IP | 100/分 | V2 の OData を使用して NuGet パッケージの数を照会`Packages`コレクション | 

## <a name="package-push-and-unlist"></a>パッケージ プッシュ モードと非公開

| API | 制限の種類 | 制限値 | APU usecase | 
|:---|:---|:---|:--- |
**PUT** `/api/v2/package` | API キー | 100/分 | V2 プッシュ endpoint を使用して新しい NuGet パッケージ (バージョン) をアップロードします。 
**DELETE** `/api/v2/package/{id}/{version}` | API キー | 100/分 | 非公開 v2 endpoint を使用して NuGet パッケージ (バージョン) 
