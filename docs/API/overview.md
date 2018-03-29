---
title: 概要では、NuGet API |Microsoft ドキュメント
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
ms.technology: ''
description: NuGet API とは、パッケージをダウンロード、メタデータのフェッチなど、新しいパッケージの発行に使用できる HTTP エンドポイントのセットです。
keywords: NuGet V3 API、NuGet V2 API、NuGet JSON、NuGet の登録 API を NuGet API フラット コンテナー、NuGet nupkg API、NuGet メタデータ API、NuGet 検索 API、NuGet プッシュ API、NuGe 公開 API、NuGet は、API を削除、NuGet 非公開 API、NuGet プロトコル
ms.reviewer:
- karann
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7053a971c80a94cf035e8f149c332b36e66a9ea9
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-api"></a><span data-ttu-id="07285-104">NuGet API</span><span class="sxs-lookup"><span data-stu-id="07285-104">NuGet API</span></span>

<span data-ttu-id="07285-105">NuGet API とは、パッケージをダウンロード、メタデータのフェッチ、新しいパッケージを発行および公式 NuGet クライアントで使用できるその他のほとんどの操作を実行するために使用する HTTP エンドポイントのセットです。</span><span class="sxs-lookup"><span data-stu-id="07285-105">The NuGet API is a set of HTTP endpoints that can be used to download packages, fetch metadata, publish new packages, and perform most other operations available in the official NuGet clients.</span></span>

<span data-ttu-id="07285-106">この API は NuGet の操作を実行する Visual Studio、nuget.exe、および .NET CLI で NuGet クライアントによって使用[ `dotnet restore` ](/dotnet/articles/core/preview3/tools/dotnet-restore)、Visual Studio の UI での検索と[ `nuget.exe push`](../tools/cli-ref-push.md)です。</span><span class="sxs-lookup"><span data-stu-id="07285-106">This API is used by the NuGet client in Visual Studio, nuget.exe, and the .NET CLI to perform NuGet operations such as [`dotnet restore`](/dotnet/articles/core/preview3/tools/dotnet-restore), search in the Visual Studio UI, and [`nuget.exe push`](../tools/cli-ref-push.md).</span></span>

<span data-ttu-id="07285-107">場合によっては、nuget.org を他のパッケージ ソースが適用されていない追加の要件がある注意してください。</span><span class="sxs-lookup"><span data-stu-id="07285-107">Note in some cases, nuget.org has additional requirements that are not enforced by other package sources.</span></span> <span data-ttu-id="07285-108">これらの相違点はによって示され、 [nuget.org プロトコル](nuget-protocols.md)です。</span><span class="sxs-lookup"><span data-stu-id="07285-108">These differences are documented by the [nuget.org Protocols](nuget-protocols.md).</span></span>

## <a name="service-index"></a><span data-ttu-id="07285-109">サービスのインデックス</span><span class="sxs-lookup"><span data-stu-id="07285-109">Service index</span></span>

<span data-ttu-id="07285-110">API のエントリ ポイントは、よく知られている場所で JSON ドキュメントです。</span><span class="sxs-lookup"><span data-stu-id="07285-110">The entry point for the API is a JSON document in a well known location.</span></span> <span data-ttu-id="07285-111">このドキュメントと呼ばれる、**サービス インデックス**です。</span><span class="sxs-lookup"><span data-stu-id="07285-111">This document is called the **service index**.</span></span> <span data-ttu-id="07285-112">Nuget.org のサービスのインデックスの位置は`https://api.nuget.org/v3/index.json`します。</span><span class="sxs-lookup"><span data-stu-id="07285-112">The location of the service index for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

<span data-ttu-id="07285-113">この JSON ドキュメントの一覧を含む*リソース*をさまざまな機能を提供し、異なるユース ケースを処理します。</span><span class="sxs-lookup"><span data-stu-id="07285-113">This JSON document contains a list of *resources* which provide different functionality and fulfill different use cases.</span></span>

<span data-ttu-id="07285-114">API をサポートしているクライアントでは、それぞれのパッケージ ソースに接続するための手段としてこれらサービス インデックス URL の 1 つ以上を受け入れる必要があります。</span><span class="sxs-lookup"><span data-stu-id="07285-114">Clients that support the API should accept one or more of these service index URL as the means of connecting to the respective package sources.</span></span>

<span data-ttu-id="07285-115">サービス インデックスに関する詳細については、次を参照してください。[の API リファレンス](service-index.md)です。</span><span class="sxs-lookup"><span data-stu-id="07285-115">For more information about the service index, see [its API reference](service-index.md).</span></span>

## <a name="versioning"></a><span data-ttu-id="07285-116">バージョン管理</span><span class="sxs-lookup"><span data-stu-id="07285-116">Versioning</span></span>

<span data-ttu-id="07285-117">API は、NuGet の HTTP プロトコルのバージョン 3 です。</span><span class="sxs-lookup"><span data-stu-id="07285-117">The API is version 3 of NuGet's HTTP protocol.</span></span> <span data-ttu-id="07285-118">このプロトコルは、"V3 の API です"と呼ばれることがあります。</span><span class="sxs-lookup"><span data-stu-id="07285-118">This protocol is sometimes referred to as "the V3 API."</span></span> <span data-ttu-id="07285-119">これらの参照ドキュメントは単に"API です"としてこのプロトコルのバージョンを参照してください。</span><span class="sxs-lookup"><span data-stu-id="07285-119">These reference documents will refer to this version of the protocol simply as "the API."</span></span>

<span data-ttu-id="07285-120">サービス インデックス スキーマのバージョンがによって示される、`version`サービス インデックスのプロパティにします。</span><span class="sxs-lookup"><span data-stu-id="07285-120">The service index schema version is indicated by the `version` property in the service index.</span></span> <span data-ttu-id="07285-121">この API でのメジャー バージョン番号をバージョン文字列であることが必須で`3`です。</span><span class="sxs-lookup"><span data-stu-id="07285-121">The API mandates that the version string has a major version number of `3`.</span></span> <span data-ttu-id="07285-122">サービス インデックス スキーマに重要ではない変更が加えられると、バージョン文字列のマイナー バージョンが増加します。</span><span class="sxs-lookup"><span data-stu-id="07285-122">As non-breaking changes are made to the service index schema, the version string's minor version will be increased.</span></span>

<span data-ttu-id="07285-123">古いクライアント (nuget.exe など 2.x) をサポートしない V3 API のみがここに記載されていない古い V2 API をサポートします。</span><span class="sxs-lookup"><span data-stu-id="07285-123">Older clients (such as nuget.exe 2.x) do not support the V3 API and only support the older V2 API, which is not documented here.</span></span>

<span data-ttu-id="07285-124">NuGet V3 API というようになっているため、V2 API の後続の公式 NuGet クライアント バージョン 2.x によって実装される OData ベースのプロトコルであった。</span><span class="sxs-lookup"><span data-stu-id="07285-124">The NuGet V3 API is named as such because it's the successor of the V2 API, which was the OData-based protocol implemented by the 2.x version of the official NuGet client.</span></span> <span data-ttu-id="07285-125">V3 API は、公式の NuGet クライアントのバージョンが 3.0 で初めてサポートされましたし、最新バージョンの主要なプロトコルのバージョンは、現在でも NuGet クライアント、4.0 およびします。</span><span class="sxs-lookup"><span data-stu-id="07285-125">The V3 API was first supported by the 3.0 version of the official NuGet client and is still the latest major protocol version supported by the NuGet client, 4.0 and on.</span></span> 

<span data-ttu-id="07285-126">改行しないプロトコルの変更に加えられた、API が最初のリリースです。</span><span class="sxs-lookup"><span data-stu-id="07285-126">Non-breaking protocol changes have been made to the API since it was first release.</span></span>

## <a name="resources-and-schema"></a><span data-ttu-id="07285-127">リソースとスキーマ</span><span class="sxs-lookup"><span data-stu-id="07285-127">Resources and schema</span></span>

<span data-ttu-id="07285-128">**サービス インデックス**さまざまなリソースについて説明します。</span><span class="sxs-lookup"><span data-stu-id="07285-128">The **service index** describes a variety of resources.</span></span> <span data-ttu-id="07285-129">サポートされているリソースの現在のセットは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="07285-129">The current set of supported resources are as follows:</span></span>

<span data-ttu-id="07285-130">リソース名</span><span class="sxs-lookup"><span data-stu-id="07285-130">Resource name</span></span>                                                          | <span data-ttu-id="07285-131">必須</span><span class="sxs-lookup"><span data-stu-id="07285-131">Required</span></span> | <span data-ttu-id="07285-132">説明</span><span class="sxs-lookup"><span data-stu-id="07285-132">Description</span></span>
---------------------------------------------------------------------- | -------- | -----------
[`PackagePublish`](package-publish-resource.md)                        | <span data-ttu-id="07285-133">可</span><span class="sxs-lookup"><span data-stu-id="07285-133">yes</span></span>      | <span data-ttu-id="07285-134">プッシュし削除 (非公開) パッケージ。</span><span class="sxs-lookup"><span data-stu-id="07285-134">Push and delete (or unlist) packages.</span></span>
[`SearchQueryService`](search-query-service-resource.md)               | <span data-ttu-id="07285-135">可</span><span class="sxs-lookup"><span data-stu-id="07285-135">yes</span></span>      | <span data-ttu-id="07285-136">フィルター処理し、キーワードでパッケージを検索します。</span><span class="sxs-lookup"><span data-stu-id="07285-136">Filter and search for packages by keyword.</span></span>
[`RegistrationsBaseUrl`](registration-base-url-resource.md)            | <span data-ttu-id="07285-137">可</span><span class="sxs-lookup"><span data-stu-id="07285-137">yes</span></span>      | <span data-ttu-id="07285-138">パッケージのメタデータを取得します。</span><span class="sxs-lookup"><span data-stu-id="07285-138">Get package metadata.</span></span>
[`PackageBaseAddress`](package-base-address-resource.md)               | <span data-ttu-id="07285-139">可</span><span class="sxs-lookup"><span data-stu-id="07285-139">yes</span></span>      | <span data-ttu-id="07285-140">パッケージのコンテンツ (これは .nupkg) を取得します。</span><span class="sxs-lookup"><span data-stu-id="07285-140">Get package content (.nupkg).</span></span>
[`SearchAutocompleteService`](search-autocomplete-service-resource.md) | <span data-ttu-id="07285-141">Ｘ</span><span class="sxs-lookup"><span data-stu-id="07285-141">no</span></span>       | <span data-ttu-id="07285-142">サブスト リングして、パッケージ Id とバージョンを検出します。</span><span class="sxs-lookup"><span data-stu-id="07285-142">Discover package IDs and versions by substring.</span></span>
[`ReportAbuseUriTemplate`](report-abuse-resource.md)                   | <span data-ttu-id="07285-143">Ｘ</span><span class="sxs-lookup"><span data-stu-id="07285-143">no</span></span>       | <span data-ttu-id="07285-144">「不正使用を報告」web ページにアクセスする URL を作成します。</span><span class="sxs-lookup"><span data-stu-id="07285-144">Construct a URL to access a "report abuse" web page.</span></span>
[`Catalog`](catalog-resource.md)                                       | <span data-ttu-id="07285-145">Ｘ</span><span class="sxs-lookup"><span data-stu-id="07285-145">no</span></span>       | <span data-ttu-id="07285-146">パッケージのすべてのイベントの完全なレコード。</span><span class="sxs-lookup"><span data-stu-id="07285-146">Full record of all package events.</span></span>

<span data-ttu-id="07285-147">一般に、API のリソースによって返されるすべての非バイナリ データは、JSON を使用してシリアル化されます。</span><span class="sxs-lookup"><span data-stu-id="07285-147">In general, all non-binary data returned by a API resource are serialized using JSON.</span></span> <span data-ttu-id="07285-148">サービス インデックス内の各リソースによって返された応答スキーマは、そのリソースに対して個別に定義されます。</span><span class="sxs-lookup"><span data-stu-id="07285-148">The response schema returned by each resource in the service index is defined individually for that resource.</span></span> <span data-ttu-id="07285-149">各リソースに関する詳細については、上記のトピックを参照してください。</span><span class="sxs-lookup"><span data-stu-id="07285-149">For more information about each resource, see the topics listed above.</span></span>

> [!Note]
> <span data-ttu-id="07285-150">ときに、ソースを実装しません`SearchAutocompleteService`オートコンプリートの動作が正常に無効にする必要があります。</span><span class="sxs-lookup"><span data-stu-id="07285-150">When a source does not implement `SearchAutocompleteService` any autocomplete behavior should be disabled gracefully.</span></span> <span data-ttu-id="07285-151">ときに`ReportAbuseUriTemplate`は実装されていません、nuget.org には、公式の NuGet クライアントがレポートの不正使用の URL (によって追跡される[NuGet/ホーム #4924](https://github.com/NuGet/Home/issues/4924))。</span><span class="sxs-lookup"><span data-stu-id="07285-151">When `ReportAbuseUriTemplate` is not implemented, the official NuGet client falls back to nuget.org's report abuse URL (tracked by [NuGet/Home#4924](https://github.com/NuGet/Home/issues/4924)).</span></span> <span data-ttu-id="07285-152">他のクライアントは、単にないレポートの不正使用を URL、ユーザーに表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="07285-152">Other clients may opt to simply not show a report abuse URL to the user.</span></span>

## <a name="timestamps"></a><span data-ttu-id="07285-153">タイムスタンプ</span><span class="sxs-lookup"><span data-stu-id="07285-153">Timestamps</span></span>

<span data-ttu-id="07285-154">API によって返されるすべてのタイムスタンプ (utc) は、それ以外の場合の指定などが使用して[ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html)表現します。</span><span class="sxs-lookup"><span data-stu-id="07285-154">All timestamps returned by the API are UTC or are otherwise specified using [ISO 8601](https://www.iso.org/iso-8601-date-and-time-format.html) representation.</span></span> 

## <a name="http-methods"></a><span data-ttu-id="07285-155">HTTP メソッド</span><span class="sxs-lookup"><span data-stu-id="07285-155">HTTP methods</span></span>

<span data-ttu-id="07285-156">動詞</span><span class="sxs-lookup"><span data-stu-id="07285-156">Verb</span></span>   | <span data-ttu-id="07285-157">使用</span><span class="sxs-lookup"><span data-stu-id="07285-157">Use</span></span>
------ | -----------
<span data-ttu-id="07285-158">GET</span><span class="sxs-lookup"><span data-stu-id="07285-158">GET</span></span>    | <span data-ttu-id="07285-159">通常のデータの取得、読み取り専用操作を実行します。</span><span class="sxs-lookup"><span data-stu-id="07285-159">Performs a read-only operation, typically retrieving data.</span></span>
<span data-ttu-id="07285-160">HEAD、</span><span class="sxs-lookup"><span data-stu-id="07285-160">HEAD</span></span>   | <span data-ttu-id="07285-161">対応する応答ヘッダーをフェッチ`GET`要求します。</span><span class="sxs-lookup"><span data-stu-id="07285-161">Fetches the response headers for the corresponding `GET` request.</span></span>
<span data-ttu-id="07285-162">PUT</span><span class="sxs-lookup"><span data-stu-id="07285-162">PUT</span></span>    | <span data-ttu-id="07285-163">存在しないか、存在する場合は更新するリソースを作成します。</span><span class="sxs-lookup"><span data-stu-id="07285-163">Creates a resource that doesn't exist or, if it does exist, updates it.</span></span> <span data-ttu-id="07285-164">一部のリソースでは、更新はサポートされません。</span><span class="sxs-lookup"><span data-stu-id="07285-164">Some resources may not support update.</span></span>
<span data-ttu-id="07285-165">Del</span><span class="sxs-lookup"><span data-stu-id="07285-165">DELETE</span></span> | <span data-ttu-id="07285-166">削除またはリソースを unlists します。</span><span class="sxs-lookup"><span data-stu-id="07285-166">Deletes or unlists a resource.</span></span>

## <a name="http-status-codes"></a><span data-ttu-id="07285-167">HTTP 状態コード</span><span class="sxs-lookup"><span data-stu-id="07285-167">HTTP status codes</span></span>

<span data-ttu-id="07285-168">コード</span><span class="sxs-lookup"><span data-stu-id="07285-168">Code</span></span> | <span data-ttu-id="07285-169">説明</span><span class="sxs-lookup"><span data-stu-id="07285-169">Description</span></span>
---- | -----
<span data-ttu-id="07285-170">200</span><span class="sxs-lookup"><span data-stu-id="07285-170">200</span></span>  | <span data-ttu-id="07285-171">成功した場合、応答本文があるとします。</span><span class="sxs-lookup"><span data-stu-id="07285-171">Success, and there is a response body.</span></span>
<span data-ttu-id="07285-172">201</span><span class="sxs-lookup"><span data-stu-id="07285-172">201</span></span>  | <span data-ttu-id="07285-173">成功した場合、リソースが作成されたとします。</span><span class="sxs-lookup"><span data-stu-id="07285-173">Success, and the resource was created.</span></span>
<span data-ttu-id="07285-174">202</span><span class="sxs-lookup"><span data-stu-id="07285-174">202</span></span>  | <span data-ttu-id="07285-175">成功した場合、要求が承諾されましたが、何らかの処理はまだ不完全で完了した非同期的に。</span><span class="sxs-lookup"><span data-stu-id="07285-175">Success, the request has been accepted but some work may still be incomplete and completed asynchronously.</span></span>
<span data-ttu-id="07285-176">204</span><span class="sxs-lookup"><span data-stu-id="07285-176">204</span></span>  | <span data-ttu-id="07285-177">成功した場合、応答本文はありません。</span><span class="sxs-lookup"><span data-stu-id="07285-177">Success, but there is no response body.</span></span>
<span data-ttu-id="07285-178">301</span><span class="sxs-lookup"><span data-stu-id="07285-178">301</span></span>  | <span data-ttu-id="07285-179">永続的にリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="07285-179">A permanent redirect.</span></span>
<span data-ttu-id="07285-180">302</span><span class="sxs-lookup"><span data-stu-id="07285-180">302</span></span>  | <span data-ttu-id="07285-181">一時的なリダイレクトします。</span><span class="sxs-lookup"><span data-stu-id="07285-181">A temporary redirect.</span></span>
<span data-ttu-id="07285-182">400</span><span class="sxs-lookup"><span data-stu-id="07285-182">400</span></span>  | <span data-ttu-id="07285-183">URL または要求本文パラメーターは無効です。</span><span class="sxs-lookup"><span data-stu-id="07285-183">The parameters in the URL or in the request body aren't valid.</span></span>
<span data-ttu-id="07285-184">401</span><span class="sxs-lookup"><span data-stu-id="07285-184">401</span></span>  | <span data-ttu-id="07285-185">指定された資格情報が無効です。</span><span class="sxs-lookup"><span data-stu-id="07285-185">The provided credentials are invalid.</span></span>
<span data-ttu-id="07285-186">403</span><span class="sxs-lookup"><span data-stu-id="07285-186">403</span></span>  | <span data-ttu-id="07285-187">アクションでは、指定された資格情報を指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="07285-187">The action is not allowed given the provided credentials.</span></span>
<span data-ttu-id="07285-188">404</span><span class="sxs-lookup"><span data-stu-id="07285-188">404</span></span>  | <span data-ttu-id="07285-189">要求されたリソースが存在しません。</span><span class="sxs-lookup"><span data-stu-id="07285-189">The requested resource doesn't exist.</span></span>
<span data-ttu-id="07285-190">409</span><span class="sxs-lookup"><span data-stu-id="07285-190">409</span></span>  | <span data-ttu-id="07285-191">要求が既存のリソースと競合しています。</span><span class="sxs-lookup"><span data-stu-id="07285-191">The request conflicts with an existing resource.</span></span>
<span data-ttu-id="07285-192">500</span><span class="sxs-lookup"><span data-stu-id="07285-192">500</span></span>  | <span data-ttu-id="07285-193">サービスで予期しないエラーが発生しました。</span><span class="sxs-lookup"><span data-stu-id="07285-193">The service has encountered an unexpected error.</span></span>
<span data-ttu-id="07285-194">503</span><span class="sxs-lookup"><span data-stu-id="07285-194">503</span></span>  | <span data-ttu-id="07285-195">サービスでは、一時的に使用できません。</span><span class="sxs-lookup"><span data-stu-id="07285-195">The service is temporarily unavailable.</span></span>

<span data-ttu-id="07285-196">どの`GET`API エンドポイントに対して行われた要求は、HTTP リダイレクト 301 (302) を返す可能性があります。</span><span class="sxs-lookup"><span data-stu-id="07285-196">Any `GET` request made to a API endpoint may return an HTTP redirect (301 or 302).</span></span> <span data-ttu-id="07285-197">クライアントが観察することによってこのようなリダイレクトを適切に処理する必要があります、`Location`ヘッダーと、後続の発行中`GET`です。</span><span class="sxs-lookup"><span data-stu-id="07285-197">Clients should gracefully handle such redirects by observing the `Location` header and issueing a subsequent `GET`.</span></span> <span data-ttu-id="07285-198">ドキュメントに関する特定のエンドポイントがない明示的に呼び出すリダイレクトを使用することがあります。</span><span class="sxs-lookup"><span data-stu-id="07285-198">Documentation concerning specific endpoints will not explicitly call out where redirects may be used.</span></span>

<span data-ttu-id="07285-199">500 番台の状態コードの場合、クライアントは、適切な再試行メカニズムを実装できます。</span><span class="sxs-lookup"><span data-stu-id="07285-199">In the case of a 500-level status code, the client can implement a reasonable retry mechanism.</span></span> <span data-ttu-id="07285-200">公式 NuGet クライアント再試行 3 回の 500 番台の状態コードまたは TCP/DNS エラーが発生するとします。</span><span class="sxs-lookup"><span data-stu-id="07285-200">The official NuGet client retries three times when encountering any 500-level status code or TCP/DNS error.</span></span>

## <a name="http-request-headers"></a><span data-ttu-id="07285-201">HTTP 要求ヘッダー</span><span class="sxs-lookup"><span data-stu-id="07285-201">HTTP request headers</span></span>

<span data-ttu-id="07285-202">名前</span><span class="sxs-lookup"><span data-stu-id="07285-202">Name</span></span>                     | <span data-ttu-id="07285-203">説明</span><span class="sxs-lookup"><span data-stu-id="07285-203">Description</span></span>
------------------------ | -----------
<span data-ttu-id="07285-204">X-NuGet-ApiKey</span><span class="sxs-lookup"><span data-stu-id="07285-204">X-NuGet-ApiKey</span></span>           | <span data-ttu-id="07285-205">プッシュと削除に必要なを参照してください[`PackagePublish`リソース](package-publish-resource.md)</span><span class="sxs-lookup"><span data-stu-id="07285-205">Required for push and delete, see [`PackagePublish` resource](package-publish-resource.md)</span></span>
<span data-ttu-id="07285-206">X-NuGet-Client-Version</span><span class="sxs-lookup"><span data-stu-id="07285-206">X-NuGet-Client-Version</span></span>   | <span data-ttu-id="07285-207">**非推奨**と置き換えられます `X-NuGet-Protocol-Version`</span><span class="sxs-lookup"><span data-stu-id="07285-207">**Deprecated** and replaced by `X-NuGet-Protocol-Version`</span></span>
<span data-ttu-id="07285-208">X-NuGet-Protocol-Version</span><span class="sxs-lookup"><span data-stu-id="07285-208">X-NuGet-Protocol-Version</span></span> | <span data-ttu-id="07285-209">場合によっては nuget.org にのみ必要なを参照してください[nuget.org プロトコル](NuGet-Protocols.md)</span><span class="sxs-lookup"><span data-stu-id="07285-209">Required in certain cases only on nuget.org, see [nuget.org protocols](NuGet-Protocols.md)</span></span>
<span data-ttu-id="07285-210">X-NuGet-Session-Id</span><span class="sxs-lookup"><span data-stu-id="07285-210">X-NuGet-Session-Id</span></span>       | <span data-ttu-id="07285-211">*省略可能な*します。</span><span class="sxs-lookup"><span data-stu-id="07285-211">*Optional*.</span></span> <span data-ttu-id="07285-212">NuGet クライアント v4.7 + 同じ NuGet クライアントのセッションの一部である HTTP 要求を識別します。</span><span class="sxs-lookup"><span data-stu-id="07285-212">NuGet clients v4.7+ identify HTTP requests that are part of the same NuGet client session.</span></span> <span data-ttu-id="07285-213">`PackageReference`復元操作がありますが完了すると、自動などの他のシナリオの 1 つのセッション id と`packages.config`復元いくつか別のセッション id のコードを組み込む方法のためである可能性があります。</span><span class="sxs-lookup"><span data-stu-id="07285-213">For `PackageReference` restore operations there is a single session id, for other scenarios such as auto complete, and `packages.config` restore there may be several different session id's due to how the code is factored.</span></span>

## <a name="authentication"></a><span data-ttu-id="07285-214">認証</span><span class="sxs-lookup"><span data-stu-id="07285-214">Authentication</span></span>

<span data-ttu-id="07285-215">認証は、パッケージ ソースの実装を定義するまでのままです。</span><span class="sxs-lookup"><span data-stu-id="07285-215">Authentication is left up to the package source implementation to define.</span></span> <span data-ttu-id="07285-216">Nuget.org、のみの`PackagePublish`リソースには、特殊な API キー ヘッダーを使用して認証が必要です。</span><span class="sxs-lookup"><span data-stu-id="07285-216">For nuget.org, only the `PackagePublish` resource requires authentication via a special API key header.</span></span> <span data-ttu-id="07285-217">参照してください[`PackagePublish`リソース](package-publish-resource.md)詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="07285-217">See [`PackagePublish` resource](package-publish-resource.md) for details.</span></span>
