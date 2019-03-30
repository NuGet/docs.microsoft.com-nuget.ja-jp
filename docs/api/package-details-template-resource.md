---
title: パッケージの詳細 URL テンプレートは、NuGet API
description: パッケージの詳細 URL テンプレートでは、パッケージの詳細へのリンクを web UI に表示するクライアントを使用できます。
author: joelverhagen
ms.author: jver
ms.date: 3/1/2019
ms.topic: reference
ms.reviewer: ananguar
ms.openlocfilehash: c01fd35c5d96c44279c9d0254f89d8b1b9fe59d8
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2019
ms.locfileid: "58638075"
---
# <a name="package-details-url-template"></a>パッケージの詳細 URL テンプレート

クライアント web ブラウザーでのパッケージ詳細を表示、ユーザーが使用できる URL を構築することができます。 これは、機能は、パッケージ ソースが、NuGet クライアント アプリケーションに表示される内容のスコープ内に収まらない可能性がありますパッケージに関する追加情報を表示するときに便利です。

この URL を構築するために使用されるリソースは、`PackageDetailsUriTemplate`リソースで見つかった、[サービス インデックス](service-index.md)します。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                     | メモ
------------------------------- | -----
PackageDetailsUriTemplate/5.1.0 | 最初のリリース

## <a name="url-template"></a>URL テンプレート

次の API の URL の値である、`@id`前述のリソースのいずれかに関連付けられているプロパティ`@type`値。

## <a name="http-methods"></a>HTTP メソッド

Web ページをサポートする必要がありますが、クライアントは、ユーザーの代理として、パッケージの詳細 URL に対して要求を行うものではありません、`GET`クリックされた URL を web ブラウザーで簡単に開くことができるようにする方法。

## <a name="construct-the-url"></a>URL を構築します。

既知のパッケージ ID とバージョンを指定すると、クライアントの実装は、web インターフェイスへのアクセスに使用する URL を構築できます。 クライアントの実装では、URL に web ブラウザーを開くと、パッケージの詳細についてようにユーザーにこの構築された URL (またはリンクのクリック可能な) を表示する必要があります。 パッケージ詳細ページの内容は、サーバーの実装によって決定されます。

絶対 URL である必要があります、URL と (protocol) スキームが HTTPS にする必要があります。

値、`@id`サービス インデックスは、次のプレース ホルダーのトークンのいずれかを含む URL 文字列。

### <a name="url-placeholders"></a>URL のプレース ホルダー

名前        | 型    | 必須 | メモ
----------- | ------- | -------- | -----
`{id}`      | string  | Ｘ       | 詳細を取得するパッケージ ID
`{version}` | string  | Ｘ       | パッケージのバージョンの詳細を取得するには

サーバーが受け入れる必要があります`{id}`と`{version}`任意の大文字と小文字の値。 さらに、サーバーすることはできません、バージョンがいるかどうかに機密性の高い[正規化された](https://docs.microsoft.com/en-us/nuget/reference/package-versioning#normalized-version-numbers)します。 つまり、このサーバーが受け入れる正規化されていないバージョンでも使用できます。

たとえば、nuget.org のパッケージ詳細のテンプレートは、ようになります。

    https://www.nuget.org/packages/{id}/{version}

クライアントの実装、パッケージの詳細を NuGet.Versioning 4.3.0 のリンクを表示する場合は、次の URL を生成し、ユーザーに提供します。

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0
