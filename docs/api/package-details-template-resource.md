---
title: パッケージの詳細 URL テンプレート、NuGet API
description: パッケージの詳細の URL テンプレートを使用すると、クライアントの UI に、より多くのパッケージ詳細への web リンクを表示できます。
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: 6657536ea6c699a834f57494c66b2a7d741dfcb7
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488176"
---
# <a name="package-details-url-template"></a>パッケージの詳細の URL テンプレート

クライアントは、web ブラウザーでより多くのパッケージの詳細を表示するためにユーザーが使用できる URL を作成することができます。 これは、パッケージソースが、NuGet クライアントアプリケーションで表示される内容の範囲内に含まれない可能性があるパッケージに関する追加情報を表示する場合に便利です。

この URL の作成に使用されるリソース`PackageDetailsUriTemplate`は、[サービスインデックス](service-index.md)で検出されたリソースです。

## <a name="versioning"></a>バージョン管理

次`@type`の値が使用されます。

@type の値                     | メモ
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | 最初のリリース

## <a name="url-template"></a>URL テンプレート

次の API の URL は、前述のいずれか`@id`のリソース`@type`値に関連付けられているプロパティの値です。

## <a name="http-methods"></a>HTTP メソッド

クライアントは、ユーザーの代わりにパッケージの詳細 url に要求を送信することを意図していませんが、 `GET` web ページでは、クリックした url を web ブラウザーで簡単に開くことができるように、メソッドをサポートする必要があります。

## <a name="construct-the-url"></a>URL を作成する

既知のパッケージ ID とバージョンを指定すると、クライアント実装は、web インターフェイスにアクセスするために使用する URL を作成できます。 クライアントの実装では、この構築された URL (またはクリック可能なリンク) をユーザーに表示して、URL に対して web ブラウザーを開いてパッケージの詳細を確認できるようにする必要があります。 パッケージの詳細ページの内容は、サーバーの実装によって決まります。

URL は絶対 URL にする必要があり、スキーム (プロトコル) は HTTPS である必要があります。

サービスインデックスのの`@id`値は、次のプレースホルダートークンのいずれかを含む URL 文字列です。

### <a name="url-placeholders"></a>URL プレースホルダー

名前        | 種類    | 必須 | メモ
----------- | ------- | -------- | -----
`{id}`      | string  | Ｘ       | 詳細を取得するパッケージ ID
`{version}` | string  | Ｘ       | 詳細を取得するパッケージのバージョン

サーバーは、と`{id}`の`{version}`大文字と小文字を区別して値を受け入れます。 また、バージョンが[正規化](https://docs.microsoft.com/en-us/nuget/concepts/package-versioning#normalized-version-numbers)されているかどうかはサーバーに依存しないようにしてください。 つまり、サーバーは、正規化されていないバージョンも受け入れる必要があります。

たとえば、nuget の [パッケージの詳細] テンプレートは次のようになります。

    https://www.nuget.org/packages/{id}/{version}

クライアント実装で NuGet のパッケージ詳細へのリンクを表示する必要がある場合、バージョン4.3.0 では次の URL が生成され、ユーザーに提供されます。

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
