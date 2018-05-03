---
title: レポートの不正使用を URL テンプレート、NuGet API
description: レポートの不正使用を URL テンプレートは、その UI に、不正使用のリンクを表示するクライアントを使用できます。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 15cf0953391489d9dd9b5d609c3f4c8f66748f19
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="report-abuse-url-template"></a>レポートの不正使用を URL テンプレート

クライアント ユーザーが特定のパッケージの不正使用を報告に使用できる URL を作成することができます。 これは、機能は、パッケージ ソースがパッケージ ソースへのレポートの不正使用を委任するすべてのクライアント エクスペリエンス (でもサード パーティ) を有効にするときに便利です。

パッケージの内容をフェッチするために使用されるリソースは、`ReportAbuseUriTemplate`リソースで見つかった、[サービス インデックス](service-index.md)です。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                       | メモ
--------------------------------- | -----
ReportAbuseUriTemplate/3.0.0-beta | 最初のリリース
ReportAbuseUriTemplate/3.0.0-rc   | エイリアス `ReportAbuseUriTemplate/3.0.0-beta`

## <a name="url-template"></a>URL テンプレート

次の API の URL がの値、`@id`前述のリソースのいずれかに関連付けられたプロパティ`@type`値。

## <a name="http-methods"></a>HTTP メソッド

Web ページをサポートする必要があります、クライアントは、ユーザーの代理として、レポートの不正使用を URL に要求をするものではありません、ただし、`GET`を簡単に web ブラウザーで開くクリックされた url を入力できるようにするメソッド。

## <a name="construct-the-url"></a>URL を構築します。

クライアントの実装は、既知のパッケージ ID とバージョンを指定するには、web インターフェイスへのアクセスに使用する URL を構築できます。 クライアント実装では、URL に web ブラウザーを開き、任意の不正使用を必要なレポートを作成するようにユーザーにこの構築された URL (またはクリック可能なリンク) を表示します。 不正使用を報告書フォームの実装は、サーバーの実装によって決定されます。

値、`@id`は、次のプレース ホルダーのトークンのいずれかを含む URL 文字列。

### <a name="url-placeholders"></a>URL のプレース ホルダー

名前        | 種類    | 必須 | メモ
----------- | ------- | -------- | -----
`{id}`      | string  | Ｘ       | 不正使用を報告するパッケージ ID
`{version}` | string  | Ｘ       | パッケージのバージョンの不正使用を報告する

`{id}`と`{version}`サーバー実装により解釈される値は、大文字小文字を区別し、バージョンを正規化するかどうかに左右されないをする必要があります。

たとえば、nuget.org のレポートの不正使用のテンプレートは、これのようになります。

    https://www.nuget.org/packages/{id}/{version}/ReportAbuse

クライアント実装では、レポートの不正使用をフォームに NuGet.Versioning 4.3.0 のリンクを表示する場合は、次の URL を生成は、ユーザーに提供します。

    https://www.nuget.org/packages/NuGet.Versioning/4.3.0/ReportAbuse
