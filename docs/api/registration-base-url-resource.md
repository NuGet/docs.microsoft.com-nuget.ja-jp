---
title: パッケージメタデータ、NuGet API
description: パッケージ登録ベース URL を使用すると、パッケージに関するメタデータを取得できます。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: 1a2e98ab36c8dc08e5f14b19b57f5ea0d790524c
ms.sourcegitcommit: 7441f12f06ca380feb87c6192ec69f6108f43ee3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/15/2019
ms.locfileid: "69488316"
---
# <a name="package-metadata"></a>パッケージ メタデータ

NuGet V3 API を使用して、パッケージソースで利用可能なパッケージに関するメタデータを取得することができます。 このメタデータは、 `RegistrationsBaseUrl` [サービスインデックス](service-index.md)で検出されたリソースを使用してフェッチできます。

に含ま`RegistrationsBaseUrl`れるドキュメントのコレクションは、"登録" または "登録 blob" と呼ばれることがよくあります。 1つ`RegistrationsBaseUrl`の内のドキュメントのセットは、"登録ハイブ" と呼ばれます。 登録ハイブには、パッケージソースで使用可能なすべてのパッケージに関するすべてのメタデータが含まれます。

## <a name="versioning"></a>バージョン管理

次`@type`の値が使用されます。

@type の値                     | メモ
------------------------------- | -----
RegistrationsBaseUrl            | 最初のリリース
RegistrationsBaseUrl/3.0.0-beta | エイリアス`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.0.0-rc   | エイリアス`RegistrationsBaseUrl`
RegistrationsBaseUrl/3.4.0      | Gzip による応答
RegistrationsBaseUrl/3.6.0      | SemVer 2.0.0 パッケージが含まれます

これは、さまざまなクライアントバージョンで使用可能な3つの個別登録ハイブを表します。

### <a name="registrationsbaseurl"></a>RegistrationsBaseUrl

これらの登録は圧縮されません (つまり`Content-Encoding: identity`、暗黙的なを使用します)。 この hive から SemVer 2.0.0 パッケージは**除外**されています。

### <a name="registrationsbaseurl340"></a>RegistrationsBaseUrl/3.4.0

これらの登録は、 `Content-Encoding: gzip`を使用して圧縮されます。 この hive から SemVer 2.0.0 パッケージは**除外**されています。

### <a name="registrationsbaseurl360"></a>RegistrationsBaseUrl/3.6.0

これらの登録は、 `Content-Encoding: gzip`を使用して圧縮されます。 この hive には、SemVer 2.0.0 パッケージが**含まれて**います。
SemVer 2.0.0 の詳細については、「 [semver 2.0.0 support for nuget.org](https://github.com/NuGet/Home/wiki/SemVer2-support-for-nuget.org-%28server-side%29)」を参照してください。

## <a name="base-url"></a>[基本 URL]

次の api のベース URL は、前述のリソース`@id` `@type`値に関連付けられているプロパティの値です。 次のドキュメントでは、プレースホルダーのベース`{@id}` URL が使用されます。

## <a name="http-methods"></a>HTTP メソッド

登録リソースで見つかったすべての url は、HTTP `GET`メソッド`HEAD`とをサポートしています。

## <a name="registration-index"></a>登録インデックス

登録リソースはパッケージ ID でパッケージメタデータをグループ化します。 一度に複数のパッケージ ID に関するデータを取得することはできません。 このリソースは、パッケージ Id を検出する方法を提供しません。 代わりに、クライアントは必要なパッケージ ID を既に把握していると見なされます。 各パッケージバージョンに関する利用可能なメタデータは、サーバーの実装によって異なります。 パッケージ登録 blob の階層構造は次のとおりです。

- **インデックス**: パッケージメタデータのエントリポイント。同じパッケージ ID を持つソースのすべてのパッケージによって共有されます。
- **Page**: パッケージのバージョンをグループ化します。 ページ内のパッケージバージョンの数は、サーバー実装によって定義されます。
- **リーフ**: 1 つのパッケージバージョンに固有のドキュメント。

登録インデックスの URL は予測可能であり、クライアントがサービスインデックスからパッケージ ID と登録リソースの`@id`値を指定して特定できます。 登録ページとリーフの Url は、登録インデックスを調べることによって検出されます。

### <a name="registration-pages-and-leaves"></a>登録ページとリーフ

個別の登録ページドキュメントに登録リーフを格納するために、サーバーの実装では厳密には必須ではありませんが、クライアント側のメモリを節約することをお勧めします。 すべての登録リーフをインデックスにインライン展開するか、直ちにページドキュメントにリーフを格納するのではなく、サーバー実装で、パッケージバージョンの数に基づいて2つの方法のいずれかを選択するためのヒューリスティックを定義することをお勧めします。パッケージリーフの累積サイズ。

登録インデックスにすべてのパッケージバージョン (リーフ) を格納すると、パッケージメタデータをフェッチするために必要な HTTP 要求の数が保存されますが、大きなドキュメントをダウンロードする必要があり、より多くのクライアントメモリを割り当てる必要があることを意味します。 一方、サーバーの実装では、登録リーフを別のページドキュメントに直ちに格納する場合、クライアントは必要な情報を取得するためにより多くの HTTP 要求を実行する必要があります。

Nuget.org が使用するヒューリスティックは次のとおりです。128以上のバージョンのパッケージがある場合は、そのリーフをサイズ64のページに分割します。 バージョンが128未満の場合、インラインのすべてが登録インデックスに残ります。

    GET {@id}/{LOWER_ID}/index.json

### <a name="request-parameters"></a>要求パラメーター

名前     | イン     | 型    | 必須 | メモ
-------- | ------ | ------- | -------- | -----
LOWER_ID | URL    | string  | 可      | パッケージ ID、小文字

この`LOWER_ID`値は、によって実装されたルールを使用して、必要なパッケージ ID を小文字にしたものです。NET の[`System.String.ToLowerInvariant()`](/dotnet/api/system.string.tolowerinvariant?view=netstandard-2.0#System_String_ToLowerInvariant)メソッド。

### <a name="response"></a>応答

応答は、次のプロパティを持つルートオブジェクトを含む JSON ドキュメントです。

名前  | 種類             | 必須 | メモ
----- | ---------------- | -------- | -----
count | integer          | 可      | インデックス内の登録ページ数
items | オブジェクトの配列 | 可      | 登録ページの配列

インデックスオブジェクトの`items`配列内の各項目は、登録ページを表す JSON オブジェクトです。

#### <a name="registration-page-object"></a>登録ページオブジェクト

登録インデックスで見つかった登録ページオブジェクトには、次のプロパティがあります。

名前   | 種類             | 必須 | メモ
------ | ---------------- | -------- | -----
@id    | string           | 可      | 登録ページの URL
count  | integer          | 可      | ページ内の登録リーフの数
items  | オブジェクトの配列 | Ｘ       | 登録リーフの配列とそれらのメタデータの関連付け
lower  | string           | 可      | ページ内の最小の SemVer 2.0.0 バージョン (包括的)
parent | string           | Ｘ       | 登録インデックスの URL
upper  | string           | 可      | ページ内の最大 SemVer 2.0.0 バージョン (包括)

ページオブジェクト`upper`のおよびの境界は、特定のページバージョンのメタデータが必要な場合に便利です。`lower`
これらの境界を使用して、必要な登録ページのみを取得できます。 バージョン文字列は、 [NuGet のバージョン規則](../concepts/package-versioning.md)に準拠しています。 バージョン文字列は正規化され、ビルドメタデータは含まれません。 NuGet エコシステムのすべてのバージョンと同様に、バージョン文字列の比較は、 [Semver 2.0.0 のバージョン優先順位ルール](http://semver.org/spec/v2.0.0.html#spec-item-11)を使用して実装されます。

プロパティは、登録ページオブジェクト`items`にプロパティがある場合にのみ表示されます。 `parent`

プロパティが登録ページオブジェクト内に存在しない場合は、に指定され`@id`た URL を使用して個々のパッケージバージョンに関するメタデータを取得する必要があります。 `items` 配列`items`は、最適化としてページオブジェクトから除外されることがあります。 1つのパッケージ ID のバージョン数が非常に大きい場合、登録インデックスドキュメントは、特定のバージョンまたは少数のバージョンのみを必要とするクライアントに対して処理するための大規模で無駄になります。

プロパティが存在する`items`場合は、すべての`@id`ページデータ`items`が既にプロパティにインライン化されているため、プロパティを使用する必要はないことに注意してください。

ページオブジェクトの`items`配列内の各項目は、登録リーフを表す JSON オブジェクトであり、それに関連付けられたメタデータです。

#### <a name="registration-leaf-object-in-a-page"></a>ページ内の登録リーフオブジェクト

登録ページで見つかった登録リーフオブジェクトには、次のプロパティがあります。

名前           | 種類   | 必須 | メモ
-------------- | ------ | -------- | -----
@id            | string | 可      | 登録リーフの URL
catalogEntry   | object | 可      | パッケージメタデータを含むカタログエントリ
packageContent | string | 可      | パッケージコンテンツへの URL (. nupkg)

各登録リーフオブジェクトは、1つのパッケージバージョンに関連付けられたデータを表します。

#### <a name="catalog-entry"></a>カタログエントリ

登録リーフオブジェクトのプロパティには、次のプロパティがあります。`catalogEntry`

名前                     | 種類                       | 必須 | メモ
------------------------ | -------------------------- | -------- | -----
@id                      | string                     | 可      | このオブジェクトを生成するために使用されるドキュメントの URL
authors                  | 文字列または文字列の配列 | Ｘ       | 
dependencyGroups         | オブジェクトの配列           | Ｘ       | ターゲットフレームワーク別にグループ化されたパッケージの依存関係
deprecation              | オブジェクト                     | Ｘ       | パッケージに関連付けられている非推奨
description              | string                     | Ｘ       | 
iconUrl                  | string                     | Ｘ       | 
id                       | string                     | 可      | パッケージの ID
licenseUrl               | string                     | Ｘ       |
licenseExpression        | string                     | Ｘ       | 
listed                   | boolean                    | Ｘ       | 存在しない場合は、一覧として考慮する必要があります
minClientVersion         | string                     | Ｘ       | 
projectUrl               | string                     | Ｘ       | 
published                | string                     | Ｘ       | パッケージが発行されたときの ISO 8601 タイムスタンプを含む文字列
requireLicenseAcceptance | boolean                    | Ｘ       | 
summary                  | string                     | Ｘ       | 
tags                     | 文字列または文字列の配列  | Ｘ       | 
title                    | string                     | Ｘ       | 
version                  | string                     | 可      | 正規化後の完全なバージョン文字列

パッケージ`version`プロパティは、正規化後の完全なバージョン文字列です。 これは、ここに SemVer 2.0.0 build データを含めることができることを意味します。

`dependencyGroups`プロパティは、ターゲットフレームワークによってグループ化された、パッケージの依存関係を表すオブジェクトの配列です。 パッケージに依存関係`dependencyGroups`がない場合、プロパティが存在しないか、空の配列であるか、 `dependencies`またはすべてのグループのプロパティが空であるか、または存在しません。

`licenseExpression`プロパティの値は、 [NuGet ライセンス式の構文](https://docs.microsoft.com/en-us/nuget/reference/nuspec#license)に準拠しています。

#### <a name="package-dependency-group"></a>パッケージ依存関係グループ

各依存関係グループオブジェクトには、次のプロパティがあります。

名前            | 種類             | 必須 | メモ
--------------- | ---------------- | -------- | -----
targetFramework | string           | Ｘ       | これらの依存関係が適用されるターゲットフレームワーク
dependencies    | オブジェクトの配列 | Ｘ       |

この`targetFramework`文字列は、nuget の .net ライブラリの[nuget フレームワーク](https://www.nuget.org/packages/NuGet.Frameworks/)によって実装された形式を使用します。 `targetFramework`が指定されていない場合、依存関係グループはすべてのターゲットフレームワークに適用されます。

`dependencies`プロパティは、オブジェクトの配列であり、それぞれが現在のパッケージのパッケージの依存関係を表します。

#### <a name="package-dependency"></a>パッケージの依存関係

各パッケージの依存関係には、次のプロパティがあります。

名前         | 種類   | 必須 | メモ
------------ | ------ | -------- | -----
id           | string | 可      | パッケージの依存関係の ID
range        | object | Ｘ       | 依存関係の許可されている[バージョン範囲](../concepts/package-versioning.md#version-ranges-and-wildcards)
registration | string | Ｘ       | この依存関係の登録インデックスの URL

プロパティが`range`除外されている場合、または空の文字列の場合、クライアント`(, )`は既定のバージョン範囲を指定する必要があります。 つまり、依存関係のすべてのバージョンが許可されます。

#### <a name="package-deprecation"></a>パッケージの非推奨

廃止された各パッケージには、次のプロパティがあります。

名前             | 種類             | 必須 | メモ
---------------- | ---------------- | -------- | -----
reasons          | 文字列の配列 | 可      | パッケージが非推奨とされた理由
message          | string           | Ｘ       | この廃止に関する追加の詳細情報
alternatePackage | オブジェクト           | Ｘ       | 代わりに使用するパッケージの依存関係

プロパティ`reasons`には、少なくとも1つの文字列が含まれている必要があり、次の表の文字列のみが含まれている必要があります。

理由       | 説明             
------------ | -----------
Legacy       | パッケージは保持されなくなりました
CriticalBugs | パッケージにバグがあるため、使用に適さない
Other        | この一覧にない理由により、パッケージは非推奨とされます

既知の`reasons`セットに含まれていない文字列がプロパティに含まれている場合は、無視する必要があります。 文字列では大文字と小文字`legacy`が区別されないため`Legacy`、と同じように処理する必要があります。 配列には順序の制限がないため、任意の順序で文字列を配置できます。 また、既知のセットからのものではない文字列のみがプロパティに含まれている場合は、"その他" の文字列のみが含まれているものとして処理する必要があります。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3/registration3/nuget.server.core/index.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-registration-index.json](./_data/package-registration-index.json)]

この場合、登録インデックスにはインラインで登録ページがあるため、個々のパッケージバージョンに関するメタデータをフェッチするために余分な要求は必要ありません。

## <a name="registration-page"></a>登録ページ

登録ページに登録リーフが含まれています。 登録ページを取得する URL は、前述の`@id` [登録ページオブジェクト](#registration-page-object)のプロパティによって決定されます。

配列が登録インデックスに指定されていない場合、その`@id`値の HTTP GET 要求は、ルートとしてオブジェクトを含む JSON ドキュメントを返します。 `items` オブジェクトには、次のプロパティがあります。

名前   | 種類             | 必須 | メモ
------ | ---------------- | -------- | -----
@id    | string           | 可      | 登録ページの URL
count  | integer          | 可      | ページ内の登録リーフの数
items  | オブジェクトの配列 | 可      | 登録リーフの配列とそれらのメタデータの関連付け
lower  | string           | 可      | ページ内の最小の SemVer 2.0.0 バージョン (包括的)
parent | string           | 可      | 登録インデックスの URL
upper  | string           | 可      | ページ内の最大 SemVer 2.0.0 バージョン (包括)

登録リーフオブジェクトの形状は、[上記](#registration-leaf-object-in-a-page)の登録インデックスと同じです。

## <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3/registration3/ravendb.client/page/1.0.531/1.0.729-unstable.json

## <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-registration-page.json](./_data/package-registration-page.json)]

## <a name="registration-leaf"></a>登録リーフ

登録リーフには、特定のパッケージ ID とバージョンに関する情報が含まれています。 このドキュメントでは、特定のバージョンに関するメタデータを使用できない可能性があります。 パッケージのメタデータは、登録[インデックス](#registration-index)または登録[ページ](#registration-page)(登録インデックスを使用して検出されます) からフェッチする必要があります。

登録リーフをフェッチする URL は、登録インデックスまた`@id`は登録ページの登録リーフオブジェクトのプロパティから取得されます。

登録リーフは、次のプロパティを持つルートオブジェクトを含む JSON ドキュメントです。

名前           | 種類    | 必須 | メモ
-------------- | ------- | -------- | -----
@id            | string  | 可      | 登録リーフの URL
catalogEntry   | string  | Ｘ       | これらのリーフを生成したカタログエントリの URL
listed         | boolean | Ｘ       | 存在しない場合は、一覧として考慮する必要があります
packageContent | string  | Ｘ       | パッケージコンテンツへの URL (. nupkg)
published      | string  | Ｘ       | パッケージが発行されたときの ISO 8601 タイムスタンプを含む文字列
registration   | string  | Ｘ       | 登録インデックスの URL

> [!Note]
> Nuget.org の場合、 `published`パッケージが一覧から削除されると、値は year 1900 に設定されます。

### <a name="sample-request"></a>要求のサンプル

    GET https://api.nuget.org/v3/registration3/nuget.versioning/4.3.0.json

### <a name="sample-response"></a>応答のサンプル

[!code-JSON [package-registration-leaf.json](./_data/package-registration-leaf.json)]
