---
title: パッケージ メタデータ、NuGet API
description: パッケージ登録の基本 URL は、パッケージに関するメタデータをフェッチできます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 19a1f48164f65f1ff805e036e55abb110247aa72
ms.sourcegitcommit: 6ea2ff8aaf7743a6f7c687c8a9400b7b60f21a52
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/16/2019
ms.locfileid: "54324865"
---
# <a name="package-metadata"></a>パッケージ メタデータ

NuGet V3 API を使用してパッケージ ソースで使用可能なパッケージに関するメタデータをフェッチすることになります。 使用して、このメタデータをフェッチすることができます、`RegistrationsBaseUrl`リソースで見つかった、[サービス インデックス](service-index.md)します。

下にあるドキュメントのコレクション`RegistrationsBaseUrl`「登録」または"登録 blob"とも呼ばれます。 単一のドキュメントのセット`RegistrationsBaseUrl`「登録ハイブ」と呼びます。 登録の hive には、パッケージ ソースで使用可能な各パッケージに関するすべてのメタデータが含まれています。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                     | メモ
------------------------------- | -----
RegistrationsBaseUrl            | 最初のリリース
RegistrationsBaseUrl/3.0.0-beta | エイリアス `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | エイリアス `RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip 圧縮された応答
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 パッケージが含まれています

これは、さまざまなクライアントのバージョンの使用可能な 3 つの個別登録ハイブを表します。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

これらの登録は圧縮されていない (つまり、暗黙的な使用`Content-Encoding: identity`)。 SemVer 2.0.0 パッケージは**除外**このハイブからです。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

これらの登録を使用して圧縮`Content-Encoding: gzip`します。 SemVer 2.0.0 パッケージは**除外**このハイブからです。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

これらの登録を使用して圧縮`Content-Encoding: gzip`します。 SemVer 2.0.0 パッケージは**に含まれる**このハイブにします。
SemVer 2.0.0 の詳細については、[nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)を参照してください。

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値は、`@id`前述のリソースに関連付けられたプロパティ`@type`値。 次のドキュメントで、プレース ホルダーのベース URL`{@id}`使用されます。

## <a name="http-methods"></a>HTTP メソッド

HTTP メソッドの登録のリソースのサポートで検出されたすべての Url`GET`と`HEAD`します。

## <a name="registration-index"></a>登録のインデックス

登録のリソース グループがパッケージ ID でメタデータをパッケージ化します。 場合によっては、一度に 1 つ以上のパッケージ ID に関するデータを取得することはできません。 このリソースには、パッケージ Id を検出する方法はありません。 代わりに、クライアントに必要なパッケージ ID を知っていると見なされます 使用可能なメタデータ パッケージの各バージョンについては、サーバーの実装によって異なります。 パッケージ登録の blob では、次の階層構造があります。

- **インデックス**: パッケージ メタデータは、同じパッケージ ID を持つソース上のすべてのパッケージで共有のエントリ ポイント
- **ページ**: パッケージのバージョンのグループ化します。 ページのパッケージのバージョンの数は、サーバーの実装によって定義されます。
- **リーフ**: 1 つのパッケージ バージョンに固有のドキュメント。

登録のインデックスの URL は予測とパッケージ ID と登録のリソースのクライアントで決定できます`@id`サービス インデックスからの値。 登録ページやリーフの Url は、登録のインデックスを調べることによって検出されます。

### <a name="registration-pages-and-leaves"></a>登録ページとリーフ

厳密には、必要なサーバーの実装を格納する個別の登録ページのドキュメントで登録が葉配列は、クライアント側のメモリを節約するために推奨される方法です。 代わりにインライン展開のすべての登録のままに、インデックスまたはページのドキュメントにリーフをすぐに格納する、サーバーの実装がなんらかのヒューリスティックをパッケージのバージョンの数に基づいて 2 つの方法の選択を定義することをお勧めまたはパッケージの累積的なサイズのままになります。

すべてのパッケージ バージョンを格納する (ままに) 登録インデックスの保存の HTTP 要求の数にパッケージ メタデータをフェッチし、大きなドキュメントをダウンロードする必要がありより多くのクライアントのメモリを割り当てる必要があることを意味します。 その一方で、サーバーの実装は、すぐに別のページのドキュメントで登録のリーフを保存する場合、クライアントは必要な情報を取得するための HTTP 要求を実行する必要があります。

Nuget.org の用途は次のように、ヒューリスティック: 128 以上のバージョンのパッケージがある場合は、サイズ 64 のページに、リーフを分割します。 128 未満のバージョンがある場合は、登録のインデックスにすべてのインラインままにします。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求パラメーター

名前     | イン     | 型    | 必須 | メモ
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 可      | パッケージ ID は、小文字

`LOWER_ID`値は小文字で実装されたルールを使用して、目的のパッケージ ID。NET の[ `System.String.ToLowerInvariant()` ](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。

### <a name="response"></a>応答

次のプロパティを使用して、ルート オブジェクトを持つ JSON ドキュメントを応答には。

名前  | 種類             | 必須 | メモ
----- | ---------------- | -------- | -----
count | 整数          | 可      | インデックス内の登録ページの数
項目 | オブジェクトの配列 | 可      | 登録ページの配列

インデックス オブジェクトの内の各項目`items`配列は、登録ページを表す JSON オブジェクト。

#### <a name="registration-page-object"></a>登録ページ オブジェクト

登録のインデックス内で見つかった登録ページのオブジェクトには、次のプロパティがあります。

名前   | 種類             | 必須 | メモ
------ | ---------------- | -------- | -----
@id    | string           | 可      | 登録ページ URL
count  | 整数          | 可      | 登録の数、ページのままになります
項目  | オブジェクトの配列 | Ｘ       | 登録のリーフとその関連メタデータの配列
低い  | string           | 可      | (包括) のページで、最小 SemVer 2.0.0 バージョン
親 | string           | Ｘ       | 登録のインデックスへの URL
上限  | string           | 可      | (包括) のページの最上位の SemVer 2.0.0 バージョン

`lower`と`upper`ページ オブジェクトの境界は、特定のページのバージョンのメタデータが必要な場合に便利です。
これらの境界は、必要な唯一の登録ページを取り出そう使用できます。 バージョン文字列に準拠して[NuGet のバージョンのルール](../reference/package-versioning.md)します。 バージョン文字列を正規化して、ビルド メタデータが含まれていません。 使用して NuGet エコシステムのすべてのバージョンでは、バージョン文字列の比較が実装されると[SemVer 2.0.0's バージョンの優先順位規則](http://semver.org/spec/v2.0.0.html#spec-item-11)します。

`parent`登録ページのオブジェクトがある場合にのみプロパティが表示されます、`items`プロパティ。

場合、`items`プロパティは、登録ページのオブジェクトで指定された URL、`@id`個々 のパッケージのバージョンに関するメタデータをフェッチするために使用する必要があります。 `items`最適化として page オブジェクトから配列が除外される場合があります。 1 つのパッケージ ID のバージョンの数が非常に大きい場合は、大規模かつ無駄だけを特定のバージョンまたはバージョンの小さな範囲について考慮するクライアントのプロセスにし、登録のインデックスのドキュメントになります。

されている場合、`items`プロパティが存在する、`@id`プロパティ必要がある、使用しないでインライン展開のすべてのページのデータがないため、`items`プロパティ。

ページ オブジェクトの内の各項目`items`配列は、登録のリーフを表す JSON オブジェクトとそれに関連付けられたメタデータ。

#### <a name="registration-leaf-object-in-a-page"></a>ページのリーフ オブジェクトの登録

登録ページにある登録リーフ オブジェクトには、次のプロパティがあります。

名前           | 種類   | 必須 | メモ
-------------- | ------ | -------- | -----
@id            | string | 可      | 登録のリーフの URL
catalogEntry   | object | 可      | パッケージ メタデータを含むカタログ エントリ
packageContent | string | 可      | パッケージ コンテンツ (.nupkg) への URL

各登録リーフ オブジェクトは、1 つのパッケージ バージョンに関連付けられているデータを表します。

#### <a name="catalog-entry"></a>カタログのエントリ

`catalogEntry`登録リーフ オブジェクトのプロパティは、次のプロパティ。

名前                     | 種類                       | 必須 | メモ
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | 可      | このオブジェクトを生成するために使用されるドキュメントの URL
作成者                  | 文字列または文字列の配列 | Ｘ       | 
dependencyGroups         | オブジェクトの配列           | Ｘ       | ターゲット フレームワーク別にグループ化、パッケージの依存関係
説明              | string                     | Ｘ       | 
iconUrl                  | string                     | Ｘ       | 
ID                       | string                     | 可      | パッケージの ID
licenseUrl               | string                     | Ｘ       |
licenseExpression        | string                     | Ｘ       | 
一覧                   | boolean                    | Ｘ       | 存在しない場合に表示されていると見なす必要があります。
minClientVersion         | string                     | Ｘ       | 
projectUrl               | string                     | Ｘ       | 
公開                | string                     | Ｘ       | パッケージが公開された場合の ISO 8601 のタイムスタンプを含む文字列
requireLicenseAcceptance | boolean                    | Ｘ       | 
概要                  | string                     | Ｘ       | 
タグ                     | 文字列または文字列の配列  | Ｘ       | 
タイトル                    | string                     | Ｘ       | 
version                  | string                     | 可      | 正規化した後、完全なバージョン文字列

パッケージ`version`プロパティでは、完全なバージョン文字列を正規化後。 意味 SemVer 2.0.0 ビルド データは含まれていますここでします。

`dependencyGroups`プロパティは、ターゲット フレームワーク別にグループ化、パッケージの依存関係を表すオブジェクトの配列。 パッケージの依存関係があるない場合、`dependencyGroups`プロパティがない、空の配列、または`dependencies`すべてのグループのプロパティが空または見つかりません。

値、`licenseExpression`プロパティに準拠している[NuGet ライセンス式の構文](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)します。

#### <a name="package-dependency-group"></a>パッケージの依存関係グループ

各依存関係グループ オブジェクトには、次のプロパティがあります。

名前            | 種類             | 必須 | メモ
--------------- | ---------------- | -------- | -----
targetFramework | string           | Ｘ       | これらの依存関係に適用されるターゲット フレームワーク
依存関係    | オブジェクトの配列 | Ｘ       |

`targetFramework`文字列の NuGet の .NET ライブラリによって実装される形式は[NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)します。 ない場合は`targetFramework`を指定すると、すべてのターゲット フレームワークに依存関係グループが適用されます。

`dependencies`プロパティは、現在のパッケージのパッケージの依存関係を表す、オブジェクトの配列。

#### <a name="package-dependency"></a>パッケージの依存関係

各パッケージの依存関係では、次のプロパティがあります。

名前         | 種類   | 必須 | メモ
------------ | ------ | -------- | -----
ID           | string | 可      | パッケージの依存関係の ID
range        | object | Ｘ       | 許可されている[バージョン範囲](../reference/package-versioning.md#version-ranges-and-wildcards)依存関係の
登録 | string | Ｘ       | この依存関係の登録のインデックスへの URL

場合、`range`プロパティを除外または空の文字列バージョン範囲に、クライアントはデフォルト`(, )`します。 つまり、任意のバージョンの依存関係が許可されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

このケースでは、登録のインデックスは、個々 のパッケージのバージョンに関するメタデータをフェッチする余分な要求は必要ありませんのでに、インラインの登録ページを持っています。

## <a name="registration-page"></a>登録ページ

登録ページには、登録リーフが含まれています。 登録ページをフェッチする URL はによって決定されます、`@id`プロパティ、[登録ページ オブジェクト](#registration-page-object)上記のようにします。

ときに、`items`の HTTP GET 要求を登録インデックスで配列が指定されていない、`@id`値は、ルート オブジェクトを持つ JSON ドキュメントを返します。 オブジェクトには、次のプロパティがあります。

名前   | 種類             | 必須 | メモ
------ | ---------------- | -------- | -----
@id    | string           | 可      | 登録ページ URL
count  | 整数          | 可      | 登録の数、ページのままになります
項目  | オブジェクトの配列 | 可      | 登録のリーフとその関連メタデータの配列
低い  | string           | 可      | (包括) のページで、最小 SemVer 2.0.0 バージョン
親 | string           | 可      | 登録のインデックスへの URL
上限  | string           | 可      | (包括) のページの最上位の SemVer 2.0.0 バージョン

登録のリーフ オブジェクトの形状は、登録のインデックスと同じ[上](#registration-leaf-object-in-a-page)します。

## <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>登録のリーフ

登録のリーフには、特定のパッケージ ID とバージョンに関する情報が含まれています。 特定のバージョンについてのメタデータは、このドキュメントでできない場合があります。 パッケージのメタデータをフェッチする必要があります、[登録インデックス](#registration-index)または[登録ページ](#registration-page)(検出された場合は、登録のインデックスを使用)。

登録のリーフをフェッチする URL がから取得した、`@id`インデックスの登録または登録ページのいずれかで登録リーフ オブジェクトのプロパティ。

登録のリーフでは、次のプロパティを使用して、ルート オブジェクトを持つ JSON ドキュメントを示します。

名前           | 種類    | 必須 | メモ
-------------- | ------- | -------- | -----
@id            | string  | 可      | 登録のリーフの URL
catalogEntry   | string  | Ｘ       | これらのリーフを生成したカタログ エントリへの URL
一覧         | boolean | Ｘ       | 存在しない場合に表示されていると見なす必要があります。
packageContent | string  | Ｘ       | パッケージ コンテンツ (.nupkg) への URL
公開      | string  | Ｘ       | パッケージが公開された場合の ISO 8601 のタイムスタンプを含む文字列
登録   | string  | Ｘ       | 登録のインデックスへの URL

> [!Note]
> Nuget.org で、`published`値が、パッケージが一覧表示されている場合の 1900 年に設定します。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
