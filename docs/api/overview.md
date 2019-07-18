---
title: NuGet API の概要
description: NuGet API には、パッケージをダウンロード、メタデータをフェッチ、新しいパッケージなどの発行に使用できる HTTP エンドポイントのセットです。
author: joelverhagen
ms.author: jver
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: bb15b4decef104f1aefe37fd18f3358181a848af
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637663"
---
# <a name="nuget-api"></a>NuGet API

NuGet API には、パッケージをダウンロード、メタデータをフェッチ、新しいパッケージを発行および公式の NuGet クライアントで使用できるその他のほとんどの操作を実行するために使用する HTTP エンドポイントのセットです。

この API は NuGet の操作を実行します。 Visual Studio、nuget.exe、および .NET CLI、NuGet クライアントによって使用[ `dotnet restore` ](/dotnet/core/tools/dotnet-restore?tabs=netcore2x)、Visual Studio の UI での検索と[ `nuget.exe push`](../tools/cli-ref-push.md)します。

場合によっては、nuget.org が他のパッケージ ソースが適用されていない追加の要件に注意してください。 これらの違いが説明されている、 [nuget.org プロトコル](nuget-protocols.md)します。

単純な列挙型と利用可能な nuget.exe のバージョンのダウンロードでは、次を参照してください。、 [tools.json](tools-json.md)エンドポイント。

## <a name="service-index"></a>サービス インデックス

API のエントリ ポイントは、既知の場所に JSON ドキュメントです。 このドキュメントと呼ばれる、**サービス インデックス**します。 Nuget.org のサービス インデックスの場所は`https://api.nuget.org/v3/index.json`します。

この JSON ドキュメントの一覧を含む*リソース*をさまざまな機能を提供し、さまざまなユース ケースを処理します。

API をサポートしているクライアントでは、それぞれのパッケージ ソースに接続する手段として 1 つ以上のこれらのサービス インデックス URL を受け入れる必要があります。

サービス インデックスの詳細については、[、API リファレンス](service-index.md)を参照してください。

## <a name="versioning"></a>バージョン管理

API は、NuGet の HTTP プロトコルのバージョン 3 です。 このプロトコルは、"V3 API"とも呼ばれます。 これらのリファレンス ドキュメントは単に"API です"とプロトコルのこのバージョンを参照してください。

サービス インデックス スキーマのバージョンが付いて、`version`サービス インデックスのプロパティ。 API のバージョン文字列でのメジャー バージョン番号を持つことが定められて`3`します。 サービス インデックス スキーマには、互換性に影響しない変更が行われるため、バージョン文字列のマイナー バージョンが高くなります。

古いクライアント (nuget.exe など 2.x) V3 API をサポートしていないしかここで説明されていない古い V2 API をサポートします。

NuGet V3 API は、公式の NuGet クライアントのバージョン 2.x で実装されている OData ベースのプロトコルが、V2 API の後継となっているよう名前です。 V3 API は、公式の NuGet クライアントのバージョンが 3.0 で初めてサポートされましたし、まだ最新の主要なプロトコルのバージョンでサポートされていて、NuGet クライアント、4.0 にします。 

改行しないプロトコルの変更には、最初のリリースから、api が加えします。

## <a name="resources-and-schema"></a>リソースとスキーマ

**サービス インデックス**のさまざまなリソースについて説明します。 現在サポートされているリソースのセットは次のとおりです。

リソース名                                                        | 必須 | 説明
-------------------------------------------------------------------- | -------- | -----------
[Catalog](catalog-resource.md)                                       | Ｘ       | パッケージのすべてのイベントの完全なレコードです。
[PackageBaseAddress](package-base-address-resource.md)               | 可      | パッケージ (.nupkg) のコンテンツを取得します。
[PackageDetailsUriTemplate](package-details-template-resource.md)    | Ｘ       | パッケージの詳細の web ページにアクセスする URL を作成します。
[PackagePublish](package-publish-resource.md)                        | 可      | プッシュし削除 (または一覧から削除する) パッケージ。
[RegistrationsBaseUrl](registration-base-url-resource.md)            | 可      | パッケージのメタデータを取得します。
[ReportAbuseUriTemplate](report-abuse-resource.md)                   | Ｘ       | レポートの不正使用の web ページにアクセスする URL を作成します。
[RepositorySignatures](repository-signatures-resource.md)            | Ｘ       | リポジトリに署名するために使用される証明書を取得します。
[SearchAutocompleteService](search-autocomplete-service-resource.md) | Ｘ       | 部分文字列では、パッケージ Id とバージョンを検出します。
[SearchQueryService](search-query-service-resource.md)               | 可      | フィルター処理し、キーワードでパッケージを検索します。
[SymbolPackagePublish](symbol-package-publish-resource.md)           | Ｘ       | シンボル パッケージをプッシュします。

一般に、API リソースによって返されるすべての非バイナリ データは、JSON を使用してシリアル化されます。 サービス インデックス内の各リソースによって返される応答のスキーマは、そのリソースを個別に定義されます。 各リソースの詳細については、上記のトピックを参照してください。

今後、プロトコルの進化に伴って、新しいプロパティは、JSON の応答に追加可能性があります。 将来のあるクライアントは、実装を想定しないでください、応答スキーマは最終的であり、余分なデータを含めることはできません。 実装に対応していないすべてのプロパティを無視する必要があります。

> [!Note]
> ときに、ソースを実装しません`SearchAutocompleteService`オートコンプリートの動作が正常に無効にする必要があります。 ときに`ReportAbuseUriTemplate`は実装されていません、nuget.org には、公式の NuGet クライアント フォールバック URL の不正使用を報告する (によって追跡される[NuGet ホーム/#4924](https://github.com/NuGet/Home/issues/4924))。 その他のクライアントは、単にユーザーにレポートの URL の不正使用を表示しないように選択できます。

### <a name="undocumented-resources-on-nugetorg"></a>Nuget.org 上のドキュメントに未記載のリソース

Nuget.org V3 サービス インデックスでは、上記に記載されていない一部のリソースを持っています。 いないリソースを文書化するためのいくつかの理由があります。

最初に、nuget.org の実装の詳細として使用されるリソースについて記載はありません。`SearchGalleryQueryService`はこのカテゴリに分類されます。 [NuGetGallery](https://github.com/NuGet/NuGetGallery)一部 V2 を委任するこのリソースを使用して、データベースを使用する代わりに検索のインデックスにクエリを (OData)。 このリソースは、スケーラビリティ上の理由から導入され、外部使用のためのものではありません。

次に、公式のクライアントの RTM バージョンで出荷されていないリソースについて記載はありません。
`PackageDisplayMetadataUriTemplate` `PackageVersionDisplayMetadataUriTemplate`このカテゴリに分類されます。

第 3 に、緊密にあるリソースを文書化していない V2 プロトコルを組み合わせて自体は意図的に文書化します。 `LegacyGallery`リソースは、このカテゴリに分類されます。 このリソースは、対応する V2 ソース URL を指す V3 サービス インデックスを使用します。 このリソースのサポート、`nuget.exe list`します。

リソースがここでは、説明されていない場合*強く*に依存関係を実行しないことをお勧めします。 削除するか、予期しない方法で実装を中断することがこれらの文書化されていないリソースの動作を変更しました可能性があります。

## <a name="timestamps"></a>タイムスタンプ

API によって返されるすべてのタイムスタンプは UTC またはを使用して指定されて[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表現。 

## <a name="http-methods"></a>HTTP メソッド

動詞   | 使用
------ | -----------
GET    | 通常のデータの取得、読み取り専用操作を実行します。
HEAD   | 対応する応答ヘッダーをフェッチ`GET`要求。
PUT    | リソースが存在しないか、存在する場合は更新を作成します。 一部のリソースは更新をサポートしていません。
Del | リソースを一覧から、または削除します。

## <a name="http-status-codes"></a>HTTP 状態コード

コード | 説明
---- | -----
200  | 成功した場合、応答本文があるとします。
201  | 成功して、リソースが作成されました。
202  | 成功すると、要求が受け入れられたがいくつかの作業可能性がありますが不完全で完了して非同期的にできます。
204  | 成功した場合、応答本文はありません。
301  | 永続的にリダイレクトします。
302  | 一時的なリダイレクト。
400  | URL または要求本文にパラメーターが無効です。
401  | 指定された資格情報を使用することはできません。
403  | アクションでは、指定された資格情報を指定することはできません。
404  | 要求されたリソースが存在しません。
409  | 要求が既存のリソースと競合します。
500  | サービスには、予期しないエラーが発生します。
503  | サービスは一時的にご利用いただけません。

すべて`GET`API エンドポイントに対して行われた要求は、HTTP リダイレクト (301 または 302) を返す可能性があります。 クライアントが監視することでこのようなリダイレクトを適切に処理する必要があります、`Location`ヘッダーと、後続の発行`GET`します。 特定のエンドポイントのに関するドキュメントがないを明示的に呼び出すリダイレクトを使用することがあります。

500 レベルの状態コードの場合、クライアントは、妥当な再試行メカニズムを実装できます。 公式 NuGet クライアント再試行 3 回 500 レベルの状態コードまたは TCP/DNS エラーが発生するとします。

## <a name="http-request-headers"></a>HTTP 要求ヘッダー

名前                     | 説明
------------------------ | -----------
X-NuGet-ApiKey           | プッシュと削除に必要なを参照してください[`PackagePublish`リソース](package-publish-resource.md)
X-NuGet-Client-Version   | **非推奨とされます**に置き換え、 `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | 場合によっては nuget.org でのみ必要なを参照してください[nuget.org プロトコル](NuGet-Protocols.md)
X-NuGet-Session-Id       | *省略可能な*します。 NuGet クライアント v4.7 + は、同じ NuGet クライアント セッションの一部である HTTP 要求を識別します。

`X-NuGet-Session-Id`で単一の復元に関連するすべての操作の 1 つの値を持つ`PackageReference`します。 オートコンプリートなどの他のシナリオと`packages.config`コードのファクタリングする方法のため ID の復元がいくつかの異なるセッションである可能性があります。

## <a name="authentication"></a>認証

認証は、パッケージ ソースの実装を定義するまでままです。 Nuget.org のみの場合、`PackagePublish`リソースには、特殊な API キー ヘッダーを使用して認証が必要です。 参照してください[`PackagePublish`リソース](package-publish-resource.md)詳細についてはします。
