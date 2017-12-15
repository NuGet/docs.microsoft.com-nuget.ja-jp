---
title: "NuGet API のメタデータをパッケージ化 |Microsoft ドキュメント"
author:
- joelverhagen
- kraigb
ms.author:
- joelverhagen
- kraigb
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 96b07019-c2e1-4f40-9290-f65ad71af3b1
description: "パッケージの登録ベース URL は、パッケージに関するメタデータをフェッチできます。"
keywords: "NuGet API パッケージ メタデータ、NuGet API の登録を NuGet API 一覧にないパッケージ"
ms.reviewer:
- karann
- unniravindranathan
ms.openlocfilehash: 15d3c836a5748497fe33dadc17e5a44846b4a8c0
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="package-metadata"></a>パッケージのメタデータ

NuGet V3 API を使用して、パッケージ ソースで使用可能なパッケージに関するメタデータの取得を行うことができます。 使用して、このメタデータをフェッチすることができます、`RegistrationsBaseUrl`リソースで見つかった、[サービス インデックス](service-index.md)です。

ドキュメントのコレクション`RegistrationsBaseUrl`「登録」または"登録 blob"も呼ばれます。 単一のドキュメントのセット`RegistrationsBaseUrl`「登録ハイブ」と呼びます。 登録 hive には、パッケージ ソースで利用可能な各パッケージに関するすべてのメタデータが含まれています。

## <a name="versioning"></a>バージョン管理

次`@type`値が使用されます。

@type の値                     | メモ
------------------------------- | -----
RegistrationsBaseUrl            | 最初のリリース
RegistrationsBaseUrl/3.0.0-beta | エイリアス`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | エイリアス`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip 圧縮された応答
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 パッケージが含まれています

これは、さまざまなクライアントのバージョンの使用可能な 3 つの個別の登録ハイブを表します。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

これらの登録は圧縮されていない (つまり、それらを暗黙的な使用`Content-Encoding: identity`)。 SemVer 2.0.0 パッケージは、**除外**このハイブからです。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

これらの登録は、圧縮されて`Content-Encoding: gzip`です。 SemVer 2.0.0 パッケージは、**除外**このハイブからです。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

これらの登録は、圧縮されて`Content-Encoding: gzip`です。 SemVer 2.0.0 パッケージは、**含まれている**このハイブにします。
SemVer 2.0.0 の詳細については、次を参照してください。 [nuget.org の SemVer 2.0.0 サポート](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)です。

## <a name="base-url"></a>[基本 URL]

次の Api のベース URL の値、`@id`前述のリソースに関連付けられたプロパティ`@type`値。 次のドキュメントでは、プレース ホルダー ベース URL`{@id}`使用されます。

## <a name="http-methods"></a>HTTP メソッド

HTTP メソッドを登録リソースのサポートで見つかったすべての Url`GET`と`HEAD`です。

## <a name="registration-index"></a>登録のインデックス

登録のリソース グループがパッケージ ID でメタデータをパッケージ化します。 一度に 1 つ以上のパッケージ ID に関するデータを取得することはできません。 このリソースに機能をパッケージ Id を検出する方法はありません。 代わりに、クライアントに必要なパッケージ ID を既に知っていると見なされます 各パッケージのバージョンに関する利用可能なメタデータは、サーバーの実装によって異なります。 パッケージ登録の blob では、次の階層構造があります。

- **インデックス**: 同じパッケージ ID を持つソースのすべてのパッケージで共有される、パッケージのメタデータのエントリ ポイント
- **ページ**: パッケージのバージョンのグループ化します。 ページのパッケージのバージョンの数は、サーバーの実装によって定義されます。
- **リーフ**: ドキュメントの 1 つのパッケージのバージョンに固有です。

登録インデックスの URL が予測し、パッケージ ID と登録リソースのクライアントで決定できます`@id`サービス インデックスからの値。 登録ページとリーフの Url が登録インデックスを調べることによって検出されます。

### <a name="registration-pages-and-leaves"></a>登録ページや

格納するサーバーの実装の必須ではありませんが、個別の登録ページのドキュメントでリーフ式の登録、クライアント側のメモリを節約することをお勧めします。 代わりにインライン展開のすべての登録のまま、インデックスまたはページのドキュメントにリーフをすぐに格納する、サーバーの実装が 2 つのパッケージのバージョンの番号に基づいた方法を選択するなんらかのヒューリスティックを定義することをお勧めまたはパッケージの累積的なサイズのままにします。

すべてのパッケージ バージョンを格納する (のまま) 登録インデックス保存 HTTP 要求の数にフェッチ パッケージ メタデータが、大きなドキュメントをダウンロードする必要がありより多くのクライアントのメモリを割り当てる必要があることを意味するために必要です。 その一方で、サーバーの実装では、別のページ ドキュメント内登録まますぐに保存する場合、クライアントに必要な情報を取得する HTTP 要求を実行する必要があります。

Nuget.org の用途は、次のように、ヒューリスティック: 128 以上のバージョンのパッケージがある場合は、サイズ 64 のページをリーフを分割します。 128 未満のバージョンがある場合は、登録のインデックスにすべてのインラインままにします。

```
GET {@id}/{LOWER_ID}/index.json
```

### <a name="request-parameters"></a>要求パラメーター

名前     | イン     | 型    | 必須 | メモ
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 可      | パッケージ ID は、小文字

`LOWER_ID`値は小文字によって実装される規則を使用して、目的のパッケージ ID。NET の[ `System.String.ToLowerInvariant()` ](https://msdn.microsoft.com/en-us/library/system.string.tolowerinvariant.aspx)メソッドです。

### <a name="response"></a>応答

応答は、ルート オブジェクトが、次のプロパティを JSON ドキュメントを示します。

名前  | 種類             | 必須 | メモ
----- | ---------------- | -------- | -----
count | 整数          | 可      | インデックス内の登録ページの数
項目 | オブジェクトの配列 | 可      | 登録ページの配列

インデックス オブジェクトの内の各項目`items`配列登録ページを表す JSON オブジェクトです。

#### <a name="registration-page-object"></a>登録ページ オブジェクト

登録インデックス内で見つかった登録ページのオブジェクトには、次のプロパティがあります。

名前   | 種類             | 必須 | メモ
------ | ---------------- | -------- | -----
@id    | string           | 可      | [登録] ページの URL
count  | 整数          | 可      | 登録の数のままにします ページ
項目  | オブジェクトの配列 | Ｘ       | 登録のままと関連付けるメタデータの配列
低い  | string           | 可      | (包括) のページで、最小 SemVer 2.0.0 バージョン
親 | string           | Ｘ       | 登録インデックスへの URL
上限  | string           | 可      | (包括) のページの最上位の SemVer 2.0.0 バージョン

`lower`と`upper`ページ オブジェクトの境界は、特定のページのバージョンのメタデータが必要な場合に便利です。
これらの境界は、必要な唯一の登録ページを取り出そう使用できます。 バージョン文字列に従う[NuGet のバージョンのルール](../reference/package-versioning.md)です。 バージョン文字列は、正規化され、ビルドのメタデータを含めないでください。 使用して NuGet エコシステム内のすべてのバージョンでバージョン文字列の比較が実装されて[SemVer 2.0.0's バージョンの優先順位規則](http://semver.org/spec/v2.0.0.html#spec-item-11)です。

`parent`プロパティは、登録ページ オブジェクトがある場合にのみ表示されます、`items`プロパティです。

場合、`items`プロパティが登録 page オブジェクトに存在しないで指定された URL、`@id`個々 のパッケージのバージョンに関するメタデータをフェッチするために使用する必要があります。 `items`最適化の手法として、page オブジェクトから配列が除外される場合があります。 1 つのパッケージ ID のバージョンの数が非常に大きい場合、登録インデックス ドキュメントされます massive と特定のバージョンまたはバージョンの小さな範囲に配慮してのみ、クライアントのプロセスに無駄です。

されている場合、`items`プロパティが含まれている、`@id`プロパティ必要がある、使用しないでインライン展開のすべてのページ データはいないため、`items`プロパティです。

Page オブジェクトの内の各項目`items`配列が登録リーフを表す JSON オブジェクトとメタデータが関連付けられています。

#### <a name="registration-leaf-object-in-a-page"></a>ページのリーフ オブジェクトの登録

登録ページで見つかった登録リーフ オブジェクトには、次のプロパティがあります。

名前           | 種類   | 必須 | メモ
-------------- | ------ | -------- | -----
@id            | string | 可      | 登録リーフへの URL
catalogEntry   | object | 可      | パッケージのメタデータを含むカタログのエントリ
packageContent | string | 可      | パッケージのコンテンツ (これは .nupkg) への URL

各登録リーフ オブジェクトは、1 つのパッケージのバージョンに関連付けられているデータを表します。

#### <a name="catalog-entry"></a>カタログのエントリ

`catalogEntry`登録リーフ オブジェクトのプロパティでは、次のプロパティ。

名前                     | 種類                       | 必須 | メモ
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | 可      | このオブジェクトを生成するために使用するドキュメントの URL
作成者                  | 文字列または文字列の配列 | Ｘ       | 
dependencyGroups         | オブジェクトの配列           | Ｘ       | パッケージのコンテンツ (これは .nupkg) への URL
説明              | string                     | Ｘ       | 
iconUrl                  | string                     | Ｘ       | 
ID                       | string                     | 可      | パッケージの ID
licenseUrl               | string                     | Ｘ       | 
一覧                   | boolean                    | Ｘ       | 存在しない場合に表示されていると見なされる必要があります。
Minclientversion は         | string                     | Ｘ       | 
projectUrl               | string                     | Ｘ       | 
発行                | string                     | Ｘ       | パッケージが発行された時間の ISO 8601 形式のタイムスタンプを含む文字列
requireLicenseAcceptance | boolean                    | Ｘ       | 
概要                  | string                     | Ｘ       | 
タグ                     | 文字列または文字列の配列  | Ｘ       | 
タイトル                    | string                     | Ｘ       | 
version                  | string                     | 可      | パッケージのバージョン

`dependencyGroups`プロパティは、ターゲット フレームワークでグループ化、パッケージの依存関係を表すオブジェクトの配列。 パッケージの依存関係があるない場合、`dependencyGroups`プロパティが見つからないか、空の配列、または`dependencies`すべてのグループのプロパティが空か存在しません。

#### <a name="package-dependency-group"></a>パッケージの依存関係グループ

依存関係グループの各オブジェクトには、次のプロパティがあります。

名前            | 種類             | 必須 | メモ
--------------- | ---------------- | -------- | -----
targetFramework | string           | Ｘ       | これらの依存関係に適用される対象のフレームワーク
依存関係    | オブジェクトの配列 | Ｘ       |

`targetFramework`文字列の NuGet の .NET ライブラリによって実装される形式は[NuGet.Frameworks](https://www.nuget.org/packages/NuGet.Frameworks/)です。 ない場合は`targetFramework`が指定されているすべてのターゲット フレームワークに依存関係グループが適用されます。

`dependencies`プロパティは、現在のパッケージのパッケージの依存関係を表す、オブジェクトの配列。

#### <a name="package-dependency"></a>パッケージの依存関係

各パッケージの依存関係には、次のプロパティがあります。

名前         | 種類   | 必須 | メモ
------------ | ------ | -------- | -----
ID           | string | 可      | パッケージの依存関係の ID
range        | object | Ｘ       | 許可される[バージョン範囲](../reference/package-versioning.md#version-ranges-and-wildcards)依存関係の
登録 | string | Ｘ       | この依存関係の登録インデックスへの URL

場合、`range`プロパティを除外するか、またはクライアントが空の文字列バージョンの範囲を既定`(, )`です。 つまり、任意のバージョンの依存関係が許可されます。

### <a name="sample-request"></a>要求のサンプル

```
GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json
```

### <a name="sample-response"></a>応答のサンプル 

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

この特定のケースでは、登録インデックスは、個々 のパッケージのバージョンに関するメタデータをフェッチする余分な要求が必要ないために、インライン関数の登録ページを持っています。

## <a name="registration-page"></a>[登録] ページ

[登録] ページには、登録リーフが含まれています。 登録ページを取り出そう URL はによって決定されます、`@id`プロパティに、[登録ページ オブジェクト](#registration-page-object)上記で説明しました。

ときに、`items`登録インデックスでは、配列は提供されていない、HTTP GET 要求、`@id`値は、ルート オブジェクトのある JSON ドキュメントを返します。 オブジェクトには、次のプロパティがあります。

名前   | 種類             | 必須 | メモ
------ | ---------------- | -------- | -----
@id    | string           | 可      | [登録] ページの URL
count  | 整数          | 可      | 登録の数のままにします ページ
項目  | オブジェクトの配列 | 可      | 登録のままと関連付けるメタデータの配列
低い  | string           | 可      | (包括) のページで、最小 SemVer 2.0.0 バージョン
親 | string           | 可      | 登録インデックスへの URL
上限  | string           | 可      | (包括) のページの最上位の SemVer 2.0.0 バージョン

登録リーフ オブジェクトの形状は、登録のインデックスと同じ[上](#registration-leaf-object-in-a-page)です。

## <a name="sample-request"></a>要求のサンプル

```
GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json
```

## <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>登録リーフ

登録リーフには、特定のパッケージ ID とバージョンに関する情報が含まれています。 特定のバージョンに関するメタデータは、このドキュメントで使用できない可能性があります。 パッケージのメタデータをフェッチする必要があります、[登録インデックス](#registration-index)または[登録ページ](#registration-page)(が検出された登録インデックスを使用して)。

登録リーフをフェッチする URL がから取得した、`@id`インデックスの登録または登録 ページで登録リーフ オブジェクトのプロパティです。

登録リーフでは、次のプロパティを持つルート オブジェクトで JSON ドキュメントを示します。

名前           | 種類    | 必須 | メモ
-------------- | ------- | -------- | -----
@id            | string  | 可      | 登録リーフへの URL
catalogEntry   | string  | Ｘ       | これらのリーフを生成したカタログ エントリへの URL
一覧         | boolean | Ｘ       | 存在しない場合に表示されていると見なされる必要があります。
packageContent | string  | Ｘ       | パッケージのコンテンツ (これは .nupkg) への URL
発行      | string  | Ｘ       | パッケージが発行された時間の ISO 8601 形式のタイムスタンプを含む文字列
登録   | string  | Ｘ       | 登録インデックスへの URL

> [!Note]
> Nuget.org、上、`published`値は、パッケージが一覧表示された場合 1900 年に設定します。

### <a name="sample-request"></a>要求のサンプル

```
GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json
```

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
