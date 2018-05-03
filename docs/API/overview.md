---
title: NuGet API の概要
description: NuGet API とは、パッケージをダウンロード、メタデータのフェッチなど、新しいパッケージの発行に使用できる HTTP エンドポイントのセットです。
author: joelverhagen
ms.author: jver
manager: skofman
ms.date: 10/26/2017
ms.topic: reference
ms.reviewer: kraigb
ms.openlocfilehash: a638dba005c14bff4b2e668e2d6ca527a67b94a9
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-api"></a>NuGet API

NuGet API とは、パッケージをダウンロード、メタデータのフェッチ、新しいパッケージを発行および公式 NuGet クライアントで使用できるその他のほとんどの操作を実行するために使用する HTTP エンドポイントのセットです。

この API は NuGet の操作を実行する Visual Studio、nuget.exe、および .NET CLI で NuGet クライアントによって使用[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)、Visual Studio の UI での検索と[ `nuget.exe push`](../tools/cli-ref-push.md)です。

場合によっては、nuget.org を他のパッケージ ソースが適用されていない追加の要件がある注意してください。 これらの相違点はによって示され、 [nuget.org プロトコル](nuget-protocols.md)です。

## <a name="service-index"></a>サービスのインデックス

API のエントリ ポイントは、よく知られている場所で JSON ドキュメントです。 このドキュメントと呼ばれる、**サービス インデックス**です。 Nuget.org のサービスのインデックスの位置は`https://api.nuget.org/v3/index.json`します。

この JSON ドキュメントの一覧を含む*リソース*をさまざまな機能を提供し、異なるユース ケースを処理します。

API をサポートしているクライアントでは、それぞれのパッケージ ソースに接続するための手段としてこれらサービス インデックス URL の 1 つ以上を受け入れる必要があります。

サービス インデックスに関する詳細については、次を参照してください。[の API リファレンス](service-index.md)です。

## <a name="versioning"></a>バージョン管理

API は、NuGet の HTTP プロトコルのバージョン 3 です。 このプロトコルは、"V3 の API です"と呼ばれることがあります。 これらの参照ドキュメントは単に"API です"としてこのプロトコルのバージョンを参照してください。

サービス インデックス スキーマのバージョンがによって示される、`version`サービス インデックスのプロパティにします。 この API でのメジャー バージョン番号をバージョン文字列であることが必須で`3`です。 サービス インデックス スキーマに重要ではない変更が加えられると、バージョン文字列のマイナー バージョンが増加します。

古いクライアント (nuget.exe など 2.x) をサポートしない V3 API のみがここに記載されていない古い V2 API をサポートします。

NuGet V3 API というようになっているため、V2 API の後続の公式 NuGet クライアント バージョン 2.x によって実装される OData ベースのプロトコルであった。 V3 API は、公式の NuGet クライアントのバージョンが 3.0 で初めてサポートされましたし、最新バージョンの主要なプロトコルのバージョンは、現在でも NuGet クライアント、4.0 およびします。 

改行しないプロトコルの変更に加えられた、API が最初のリリースです。

## <a name="resources-and-schema"></a>リソースとスキーマ

**サービス インデックス**さまざまなリソースについて説明します。 サポートされているリソースの現在のセットは次のとおりです。

リソース名                                                          | 必須 | 説明
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | 可      | プッシュし削除 (非公開) パッケージ。
[`SearchQueryService`](search-query-service-resource.md)               | 可      | フィルター処理し、キーワードでパッケージを検索します。
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | 可      | パッケージのメタデータを取得します。
[`PackageBaseAddress`](package-base-address-resource.md)               | 可      | パッケージのコンテンツ (これは .nupkg) を取得します。
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | Ｘ       | サブスト リングして、パッケージ Id とバージョンを検出します。
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | Ｘ       | 「不正使用を報告」web ページにアクセスする URL を作成します。
[`Catalog`](catalog-resource.md)                                       | Ｘ       | パッケージのすべてのイベントの完全なレコード。

一般に、API のリソースによって返されるすべての非バイナリ データは、JSON を使用してシリアル化されます。 サービス インデックス内の各リソースによって返された応答スキーマは、そのリソースに対して個別に定義されます。 各リソースに関する詳細については、上記のトピックを参照してください。

> [!Note]
> ときに、ソースを実装しません`SearchAutocompleteService`オートコンプリートの動作が正常に無効にする必要があります。 ときに`ReportAbuseUriTemplate`は実装されていません、nuget.org には、公式の NuGet クライアントがレポートの不正使用の URL (によって追跡される[NuGet/ホーム #4924](https://github.com/NuGet/Home/issues/4924))。 他のクライアントは、単にないレポートの不正使用を URL、ユーザーに表示することもできます。

## <a name="timestamps"></a>タイムスタンプ

API によって返されるすべてのタイムスタンプ (utc) は、それ以外の場合の指定などが使用して[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表現します。 

## <a name="http-methods"></a>HTTP メソッド

動詞   | 使用
------ | -----------
GET    | 通常のデータの取得、読み取り専用操作を実行します。
HEAD、   | 対応する応答ヘッダーをフェッチ`GET`要求します。
PUT    | 存在しないか、存在する場合は更新するリソースを作成します。 一部のリソースでは、更新はサポートされません。
Del | 削除またはリソースを unlists します。

## <a name="http-status-codes"></a>HTTP 状態コード

コード | 説明
---- | -----
200  | 成功した場合、応答本文があるとします。
201  | 成功した場合、リソースが作成されたとします。
202  | 成功した場合、要求が承諾されましたが、何らかの処理はまだ不完全で完了した非同期的に。
204  | 成功した場合、応答本文はありません。
301  | 永続的にリダイレクトします。
302  | 一時的なリダイレクトします。
400  | URL または要求本文パラメーターは無効です。
401  | 指定された資格情報が無効です。
403  | アクションでは、指定された資格情報を指定することはできません。
404  | 要求されたリソースが存在しません。
409  | 要求が既存のリソースと競合しています。
500  | サービスで予期しないエラーが発生しました。
503  | サービスでは、一時的に使用できません。

どの`GET`API エンドポイントに対して行われた要求は、HTTP リダイレクト 301 (302) を返す可能性があります。 クライアントが観察することによってこのようなリダイレクトを適切に処理する必要があります、`Location`ヘッダーと、後続の発行中`GET`です。 ドキュメントに関する特定のエンドポイントがない明示的に呼び出すリダイレクトを使用することがあります。

500 番台の状態コードの場合、クライアントは、適切な再試行メカニズムを実装できます。 公式 NuGet クライアント再試行 3 回の 500 番台の状態コードまたは TCP/DNS エラーが発生するとします。

## <a name="http-request-headers"></a>HTTP 要求ヘッダー

名前                     | 説明
------------------------ | -----------
X-NuGet-ApiKey           | プッシュと削除に必要なを参照してください[`PackagePublish`リソース](package-publish-resource.md)
X-NuGet-Client-Version   | **非推奨**と置き換えられます `X-NuGet-Protocol-Version`
X-NuGet-Protocol-Version | 場合によっては nuget.org にのみ必要なを参照してください[nuget.org プロトコル](NuGet-Protocols.md)
X-NuGet-Session-Id       | *省略可能な*します。 NuGet クライアント v4.7 + 同じ NuGet クライアントのセッションの一部である HTTP 要求を識別します。 `PackageReference`復元操作がありますが完了すると、自動などの他のシナリオの 1 つのセッション id と`packages.config`復元いくつか別のセッション id のコードを組み込む方法のためである可能性があります。

## <a name="authentication"></a>認証

認証は、パッケージ ソースの実装を定義するまでのままです。 Nuget.org、のみの`PackagePublish`リソースには、特殊な API キー ヘッダーを使用して認証が必要です。 参照してください[`PackagePublish`リソース](package-publish-resource.md)詳細についてはします。
