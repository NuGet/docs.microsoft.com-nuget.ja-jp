---
title: 不正行為の URL テンプレート、NuGet API
description: レポートの不正使用 URL テンプレートを使用すると、クライアントは UI に不正使用のリンクを表示できます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b36058c9c841e2cca6eb61121ada8275f1525a8f
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775228"
---
# <a name="report-abuse-url-template"></a>不正を報告する URL テンプレート

クライアントは、特定のパッケージに関する誤用を報告するためにユーザーが使用できる URL を作成することができます。 これは、パッケージソースがすべてのクライアントエクスペリエンス (サードパーティでも) を有効にして、不正使用レポートをパッケージソースに委任する場合に便利です。

この URL の作成に使用されるリソースは、 `ReportAbuseUriTemplate` [サービスインデックス](service-index.md)で検出されたリソースです。

## <a name="versioning"></a>バージョン管理

次の `@type` 値が使用されます。

@type 値                       | Notes
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-ベータ | 最初のリリース
ReportAbuseUriTemplate/3.0.0-rc   | エイリアス `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL テンプレート

次の API の URL は、 `@id` 前述のいずれかのリソース値に関連付けられているプロパティの値です `@type` 。

## <a name="http-methods"></a>HTTP メソッド

クライアントは、ユーザーの代わりにレポートの不正使用の URL に要求を送信することを意図していませんが、web ページでは、クリックした `GET` url を web ブラウザーで簡単に開くことができるように、メソッドをサポートする必要があります。

## <a name="construct-the-url"></a>URL を作成する

既知のパッケージ ID とバージョンを指定すると、クライアント実装は、web インターフェイスにアクセスするために使用する URL を作成できます。 クライアントの実装では、この構築された URL (またはクリック可能なリンク) をユーザーに表示して、ユーザーが URL に対して web ブラウザーを開いて、必要な不正使用レポートを作成できるようにする必要があります。 誤用レポートフォームの実装は、サーバーの実装によって決まります。

の値は、 `@id` 次のプレースホルダートークンのいずれかを含む URL 文字列です。

### <a name="url-placeholders"></a>URL プレースホルダー

名前        | Type    | 必須 | Notes
----------- | ------- | -------- | -----
`{id}`      | string  | no       | 不正使用を報告するパッケージ ID
`{version}` | string  | no       | 不正使用を報告するパッケージのバージョン

`{id}`サーバーの `{version}` 実装で解釈されるおよび値は、バージョンが正規化されているかどうかにかかわらず、大文字と小文字が区別されないようにする必要があります。

たとえば、nuget.exe のレポートの不正使用テンプレートは次のようになります。

```
https://www.nuget.org/packages/{id}/{version}/ReportAbuse
```

クライアントの実装で、NuGet のレポート不正使用フォームへのリンクを表示する必要がある場合、バージョン4.3.0 では次の URL が生成され、ユーザーに提供されます。

```
https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
```
