---
title: licenses.nuget.org
author: agr
ms.date: 02/22/2019
ms.openlocfilehash: 717cf8c47335c620410be71300b07de82799e1d3
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427117"
---
# <a name="licensesnugetorg"></a><span data-ttu-id="eaebc-102">licenses.nuget.org</span><span class="sxs-lookup"><span data-stu-id="eaebc-102">licenses.nuget.org</span></span>

## <a name="rationale"></a><span data-ttu-id="eaebc-103">理由</span><span class="sxs-lookup"><span data-stu-id="eaebc-103">Rationale</span></span>

<span data-ttu-id="eaebc-104">[ライセンス式](../reference/nuspec.md#license)の導入により、個別のライセンス識別子、例外識別子、またはライセンス式に対する参照テキストを提供する信頼できるサービスを用意する要件が発生しました。</span><span class="sxs-lookup"><span data-stu-id="eaebc-104">With the introduction of the [license expressions](../reference/nuspec.md#license), a requirement emerged to have a reliable service that would provide a reference text for individual license identifiers, exception identifiers or license expressions.</span></span>
<span data-ttu-id="eaebc-105">このサービスに対する追加の要件は、古いクライアントに下位互換性を提供するために安全に使用できるよう、リンク切れになりにくい安定した URL スキーマを使用することです。</span><span class="sxs-lookup"><span data-stu-id="eaebc-105">An additional requirement for this service is to have a stable URL schema, that is not susceptible to link rot, so that we can safely use it to provide backwards compatibility for older clients.</span></span>

<span data-ttu-id="eaebc-106">licenses.nuget.org がその役割を果たします。</span><span class="sxs-lookup"><span data-stu-id="eaebc-106">Licenses.nuget.org fulfills that role.</span></span> <span data-ttu-id="eaebc-107">Nuget.org では、それを使用して、ライセンス式を使用してライセンスを指定するパッケージにライセンス テキストの参照を提供します。</span><span class="sxs-lookup"><span data-stu-id="eaebc-107">Nuget.org uses it to provide the license text reference for packages that specify their license using a license expression.</span></span> <span data-ttu-id="eaebc-108">`nuget pack` または他の[クライアント ツール](../install-nuget-client-tools.md)でのパッキングにより、`license` 要素をサポートしない古いクライアントとの下位互換性を提供するため、licenses.nuget.org を指すように [`licenseUrl`](../reference/nuspec.md#licenseurl) 要素が設定されます。</span><span class="sxs-lookup"><span data-stu-id="eaebc-108">`nuget pack` or packing with other [client tools](../install-nuget-client-tools.md) set the [`licenseUrl`](../reference/nuspec.md#licenseurl) element to point to licenses.nuget.org to provide backwards compatibility with older clients that don't support the `license` element.</span></span>

## <a name="protocol"></a><span data-ttu-id="eaebc-109">プロトコル</span><span class="sxs-lookup"><span data-stu-id="eaebc-109">Protocol</span></span>

<span data-ttu-id="eaebc-110">licenses.nuget.org はユーザーがブラウザーで表示するためのもので、コンピューターが判読できる応答は提供されません。</span><span class="sxs-lookup"><span data-stu-id="eaebc-110">Licenses.nuget.org is intended to be viewed by people in their browsers, no machine-readable responses are provided.</span></span>
<span data-ttu-id="eaebc-111">HTTPS プロトコルを使う必要があり、要求は特定の方法で構築することが想定されています。</span><span class="sxs-lookup"><span data-stu-id="eaebc-111">HTTPS protocol must be used and requests are expected to be constructed in a certain way.</span></span> <span data-ttu-id="eaebc-112">`GET` 要求のみがサポートされます。</span><span class="sxs-lookup"><span data-stu-id="eaebc-112">It only supports `GET` requests.</span></span>
<span data-ttu-id="eaebc-113">以下で指定する方法で、入力としてライセンス式またはライセンス例外識別子を受け付けます。</span><span class="sxs-lookup"><span data-stu-id="eaebc-113">It accepts license expressions or license exception identifiers as an input in a way specified below.</span></span> <span data-ttu-id="eaebc-114">ライセンス式のすべての要素は大文字と小文字が区別されるため、licenses.nuget.org へのすべての入力も大文字と小文字が区別されることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="eaebc-114">Please note, that all elements of license expressions are case sensitive, and therefore all input to licenses.nuget.org is case sensitive as well.</span></span>

### <a name="license-expressions"></a><span data-ttu-id="eaebc-115">ライセンス式</span><span class="sxs-lookup"><span data-stu-id="eaebc-115">License expressions</span></span>

#### <a name="request"></a><span data-ttu-id="eaebc-116">要求</span><span class="sxs-lookup"><span data-stu-id="eaebc-116">Request</span></span>

<span data-ttu-id="eaebc-117">ライセンス式は (式が 1 つのライセンスで構成される単純な場合も含めて)、[URL でエンコードされ](https://tools.ietf.org/html/rfc3986#section-2.1)、licenses.nuget.org への要求においてパスとして使用される必要があります。</span><span class="sxs-lookup"><span data-stu-id="eaebc-117">License expressions (including the trivial cases when expression consists of a single license) have to be [URL-encoded](https://tools.ietf.org/html/rfc3986#section-2.1) and used as a path in the request to licenses.nuget.org.</span></span>

| <span data-ttu-id="eaebc-118">ライセンス式</span><span class="sxs-lookup"><span data-stu-id="eaebc-118">License expression</span></span> | <span data-ttu-id="eaebc-119">使用する URL</span><span class="sxs-lookup"><span data-stu-id="eaebc-119">URL to use</span></span> |
|:---|:---|
| <span data-ttu-id="eaebc-120">MIT</span><span class="sxs-lookup"><span data-stu-id="eaebc-120">MIT</span></span>                                                | <https://licenses.nuget.org/MIT> |
| <span data-ttu-id="eaebc-121">(MIT)</span><span class="sxs-lookup"><span data-stu-id="eaebc-121">(MIT)</span></span>                                              | <https://licenses.nuget.org/(MIT)> |
| <span data-ttu-id="eaebc-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span><span class="sxs-lookup"><span data-stu-id="eaebc-122">(LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+)</span></span> | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

<span data-ttu-id="eaebc-123">サービスでは、nuget.org によって受け入れられるライセンス識別子とライセンス例外識別子のみがサポートされます。サポートされていないライセンス識別子またはライセンス例外識別子が含まれるライセンス式、またはライセンス式の構文に準拠しないライセンス式はすべて、無効と見なされます。</span><span class="sxs-lookup"><span data-stu-id="eaebc-123">The service supports only license identifiers and license exception identifiers that are accepted by nuget.org. All license expressions that contain unsupported license identifiers or license exception identifiers or that does not conform to license expression syntax are considered invalid.</span></span>

#### <a name="response"></a><span data-ttu-id="eaebc-124">応答</span><span class="sxs-lookup"><span data-stu-id="eaebc-124">Response</span></span>

<span data-ttu-id="eaebc-125">licenses.nuget.org は、ステータス コード HTTP 200 の有効なライセンス式が含まれる要求、およびライセンス式の説明が含まれる Web ページに応答します。</span><span class="sxs-lookup"><span data-stu-id="eaebc-125">Licenses.nuget.org responds to requests containing valid license expressions with an HTTP 200 status code and a web page containing a description of the license expression:</span></span>

* <span data-ttu-id="eaebc-126">提供されたライセンス式に 1 つのライセンス識別子が含まれる場合、そのライセンス参照テキストを含む Web ページが返されます</span><span class="sxs-lookup"><span data-stu-id="eaebc-126">if supplied license expression contains a single license identifier a web page is returned that contains that license reference text;</span></span>
* <span data-ttu-id="eaebc-127">提供されたライセンス式が複合ライセンス式である場合、ライセンス式と個別のライセンス参照またはライセンス例外参照へのリンクが含まれる Web ページが返されます。</span><span class="sxs-lookup"><span data-stu-id="eaebc-127">if supplied license expression is a composite license expression, a web page is returned that contains the license expression with links to individual license or license exception references.</span></span>

<span data-ttu-id="eaebc-128">無効なライセンス式が含まれるすべての要求に対しては、HTTP 404 が応答されます。</span><span class="sxs-lookup"><span data-stu-id="eaebc-128">Any requests that contain an invalid license expression result in an HTTP 404 response.</span></span>

### <a name="license-exceptions"></a><span data-ttu-id="eaebc-129">ライセンス例外</span><span class="sxs-lookup"><span data-stu-id="eaebc-129">License exceptions</span></span>

#### <a name="request"></a><span data-ttu-id="eaebc-130">要求</span><span class="sxs-lookup"><span data-stu-id="eaebc-130">Request</span></span>

<span data-ttu-id="eaebc-131">ライセンス例外識別子は、URL でエンコードされ、licenses.nuget.org に対する要求でパスとして使用される必要があります。1 つの要求で指定できるライセンス例外識別子は、1 つのみです。</span><span class="sxs-lookup"><span data-stu-id="eaebc-131">License exception identifiers must be URL-encoded and used as a path in the request to licenses.nuget.org. Only a single license exception identifier can be supplied in a single request.</span></span> <span data-ttu-id="eaebc-132">URL のパス部分には、ライセンス例外識別子以外の文字が存在することはできません。</span><span class="sxs-lookup"><span data-stu-id="eaebc-132">No additional characters besides license exception identifier may present in the path portion of the URL.</span></span>

| <span data-ttu-id="eaebc-133">ライセンス例外識別子</span><span class="sxs-lookup"><span data-stu-id="eaebc-133">License exception identifier</span></span> | <span data-ttu-id="eaebc-134">使用する URL</span><span class="sxs-lookup"><span data-stu-id="eaebc-134">URL to use</span></span> |
|:---|:---|
|<span data-ttu-id="eaebc-135">FLTK-exception</span><span class="sxs-lookup"><span data-stu-id="eaebc-135">FLTK-exception</span></span>            | <https://licenses.nuget.org/FLTK-exception> |
|<span data-ttu-id="eaebc-136">openvpn-openssl-exception</span><span class="sxs-lookup"><span data-stu-id="eaebc-136">openvpn-openssl-exception</span></span> | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a><span data-ttu-id="eaebc-137">応答</span><span class="sxs-lookup"><span data-stu-id="eaebc-137">Response</span></span>

<span data-ttu-id="eaebc-138">licenses.nuget.org は、既知のライセンス例外識別子が含まれる要求に対し、HTTP 200 応答と、指定されたライセンス例外に対する参照テキストが含まれる Web ページで応答します。</span><span class="sxs-lookup"><span data-stu-id="eaebc-138">Licenses.nuget.org responds to a request with a known license exception identifier with a HTTP 200 response and a web page containing the reference text for the specified license exception.</span></span>

<span data-ttu-id="eaebc-139">サポートされていないライセンス例外識別子が含まれる要求には、HTTP 404 応答が返ってきます。</span><span class="sxs-lookup"><span data-stu-id="eaebc-139">Any request containing an unsupported license exception identifier results in an HTTP 404 response.</span></span>