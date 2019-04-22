---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 4a40cc1f7d333e8d35a721f3eed2e6b9365faf7b
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/18/2019
ms.locfileid: "58921560"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="0c37b-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="0c37b-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="0c37b-103">理由</span><span class="sxs-lookup"><span data-stu-id="0c37b-103">Rationale</span></span>

<span data-ttu-id="0c37b-104">導入に伴い、[ライセンス式](nuspec.md#license)、個別のライセンスの識別子、例外識別子、またはライセンスの式の参照のテキストを提供する信頼性の高いサービスが、要件が登場しました。</span><span class="sxs-lookup"><span data-stu-id="0c37b-104">With the introduction of the [license expressions](nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="0c37b-105">このサービスに対する追加の要件は安定した古いクライアントの下位互換性を提供する安全に使用できるように、rot のリンクを受けやすくない URL スキーマです。</span><span class="sxs-lookup"><span data-stu-id="0c37b-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="0c37b-106">Licenses.nuget.org では、そのロールが満たされます。</span><span class="sxs-lookup"><span data-stu-id="0c37b-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="0c37b-107">Nuget.org では、これを使用して、ライセンス式を使用して、ライセンスの指定したパッケージのライセンス text のリファレンスを提供します。</span><span class="sxs-lookup"><span data-stu-id="0c37b-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="0c37b-108">`nuget pack` または他のパッキング[クライアント ツール](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools)設定、 [ `licenseUrl` ](nuspec.md#licenseurl)後方互換性をサポートしない古いバージョンのクライアントで licenses.nuget.org を指す要素、 `license`要素。</span><span class="sxs-lookup"><span data-stu-id="0c37b-108">`nuget pack` or packing with other [client tools](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools) set the [`licenseUrl`](nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="0c37b-109">プロトコル</span><span class="sxs-lookup"><span data-stu-id="0c37b-109">Protocol</span></span>

<span data-ttu-id="0c37b-110">Licenses.nuget.org、ブラウザー内のユーザーを表示するものでは、コンピューターが判読できる応答は提供されません。</span><span class="sxs-lookup"><span data-stu-id="0c37b-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="0c37b-111">HTTPS プロトコルを使用して、要求が特定の方法で構築する必要があります。</span><span class="sxs-lookup"><span data-stu-id="0c37b-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="0c37b-112">のみがサポートされます`GET`要求。</span><span class="sxs-lookup"><span data-stu-id="0c37b-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="0c37b-113">式のライセンスまたはライセンス例外識別子は以下で指定した方法で入力として受け入れます。</span><span class="sxs-lookup"><span data-stu-id="0c37b-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="0c37b-114">注意してください、ライセンスの式のすべての要素が大文字小文字を区別、したがって licenses.nuget.org へのすべての入力が同様で大文字小文字を区別します。</span><span class="sxs-lookup"><span data-stu-id="0c37b-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="0c37b-115">ライセンスの式</span><span class="sxs-lookup"><span data-stu-id="0c37b-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="0c37b-116">要求</span><span class="sxs-lookup"><span data-stu-id="0c37b-116">Request</span></span>

<span data-ttu-id="0c37b-117">ライセンスの式 (式は、1 つのライセンスで構成される場合は、単純なケースを含む) でなければならない[URL でエンコードされた](https://tools.ietf.org/html/rfc3986#section-2.1)licenses.nuget.org への要求で、パスとして使用するとします。</span><span class="sxs-lookup"><span data-stu-id="0c37b-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="0c37b-118">ライセンスの式</span><span class="sxs-lookup"><span data-stu-id="0c37b-118">License expression</span></span> | <span data-ttu-id="0c37b-119">使用する URL</span><span class="sxs-lookup"><span data-stu-id="0c37b-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="0c37b-120">MIT</span><span class="sxs-lookup"><span data-stu-id="0c37b-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="0c37b-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="0c37b-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="0c37b-122">(LGPL 2.0-専用と FLTK 例外または Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="0c37b-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="0c37b-123">サービスでは、ライセンスの識別子と nuget.org で受け入れられるライセンス例外識別子のみをサポートします。サポートされていないライセンス識別子またはライセンス例外識別子が含まれている、またはライセンス式の構文に準拠しないが、すべてのライセンス式は無効と見なされます。</span><span class="sxs-lookup"><span data-stu-id="0c37b-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="0c37b-124">応答</span><span class="sxs-lookup"><span data-stu-id="0c37b-124">Response</span></span>

<span data-ttu-id="0c37b-125">Licenses.nuget.org はステータス コード HTTP 200 とライセンスの式の説明を含む web ページの有効なライセンス式が含まれる要求に応答します。</span><span class="sxs-lookup"><span data-stu-id="0c37b-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="0c37b-126">ライセンスの式を指定する場合は、そのライセンス参照テキストを含む web ページが返されます 1 つのライセンスの識別子を含む</span><span class="sxs-lookup"><span data-stu-id="0c37b-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="0c37b-127">指定した場合のライセンスがライセンスの複合式、個別のライセンスまたはライセンス例外参照へのリンクを持つライセンス式を含む web ページが返されます。</span><span class="sxs-lookup"><span data-stu-id="0c37b-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="0c37b-128">HTTP 404 応答でライセンスが無効な式の結果が含まれているすべての要求。</span><span class="sxs-lookup"><span data-stu-id="0c37b-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="0c37b-129">ライセンスの例外</span><span class="sxs-lookup"><span data-stu-id="0c37b-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="0c37b-130">要求</span><span class="sxs-lookup"><span data-stu-id="0c37b-130">Request</span></span>

<span data-ttu-id="0c37b-131">ライセンス例外識別子 URL でエンコードされ、licenses.nuget.org への要求でパスとして使用されている必要があります。1 つの要求では、1 つのライセンスの例外の識別子のみを指定できます。</span><span class="sxs-lookup"><span data-stu-id="0c37b-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="0c37b-132">URL のパス部分にライセンス例外識別子だけでなく、追加の文字がありません可能性があります。</span><span class="sxs-lookup"><span data-stu-id="0c37b-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="0c37b-133">ライセンスの例外の識別子</span><span class="sxs-lookup"><span data-stu-id="0c37b-133">License exception identifier</span></span> | <span data-ttu-id="0c37b-134">使用する URL</span><span class="sxs-lookup"><span data-stu-id="0c37b-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="0c37b-135">FLTK 例外</span><span class="sxs-lookup"><span data-stu-id="0c37b-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="0c37b-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="0c37b-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="0c37b-137">応答</span><span class="sxs-lookup"><span data-stu-id="0c37b-137">Response</span></span>

<span data-ttu-id="0c37b-138">Licenses.nuget.org は、HTTP 200 応答と、指定したライセンスの例外の参照のテキストを含む web ページの既知のライセンス例外識別子を持つ要求に応答します。</span><span class="sxs-lookup"><span data-stu-id="0c37b-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="0c37b-139">ライセンスがサポートされていない例外識別子を含むすべての要求は HTTP 404 応答が発生します。</span><span class="sxs-lookup"><span data-stu-id="0c37b-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>