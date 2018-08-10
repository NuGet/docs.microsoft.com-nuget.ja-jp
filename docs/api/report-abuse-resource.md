---
title: レポート不正使用 URL テンプレートは、NuGet API
description: レポートの不正使用 URL テンプレートは、その UI に、不正使用のリンクを表示するクライアントを使用できます。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: b1fd65b12590a6c5eeb23d946eec6ca4a1c661bc
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020441"
---
# <a name="report-abuse-url-template"></a>レポートの不正使用の URL テンプレート

クライアントが特定のパッケージに関する不正使用を報告する、ユーザーが使用できる URL を構築するために可能性があります。 これは、機能は、パッケージ ソースがパッケージ ソースへのレポートの不正使用を委任するすべてのクライアント エクスペリエンス (でもサード パーティ) を有効にするときに便利です。

この URL を構築するために使用されるリソースは、`ReportAbuseUriTemplate`リソースで見つかった、[サービス インデックス](service-index.md)します。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                       | メモ
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 最初のリリース
ReportAbuseUriTemplate/3.0.0-rc   | エイリアス `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL テンプレート

次の API の URL の値である、`@id`前述のリソースのいずれかに関連付けられているプロパティ`@type`値。

## <a name="http-methods"></a>HTTP メソッド

Web ページをサポートする必要がありますが、クライアントは、レポートの URL の不正使用に、ユーザーに代わって要求を行うものではありません、`GET`クリックされた URL を web ブラウザーで簡単に開くことができるようにする方法。

## <a name="construct-the-url"></a>URL を構築します。

既知のパッケージ ID とバージョンを指定すると、クライアントの実装は、web インターフェイスへのアクセスに使用する URL を構築できます。 クライアントの実装では、URL に web ブラウザーを開き、任意の不正使用を必要なレポートを作成するようにユーザーにこの構築された URL (またはリンクのクリック可能な) を表示する必要があります。 不適切な発言の報告書フォームの実装は、サーバーの実装によって決定されます。

値、`@id`は次のプレース ホルダーのトークンのいずれかを含む URL 文字列です。

### <a name="url-placeholders"></a>URL のプレース ホルダー

name        | 種類    | 必須 | メモ
----------- | ------- | -------- | -----
`{id}`      | string  | Ｘ       | 不正使用を報告するパッケージ ID
`{version}` | string  | Ｘ       | パッケージのバージョンの不正使用を報告する

`{id}`と`{version}`サーバーの実装によって解釈される値は、大文字と小文字を区別しないと、バージョンを正規化するかどうかに左右されないをする必要があります。

たとえば、nuget.org のレポートの不正使用のテンプレートは、ようになります。

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

クライアント実装 NuGet.Versioning 4.3.0 のレポートの不正使用をフォームにリンクを表示する場合は、次の URL を生成し、ユーザーに提供します。

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
