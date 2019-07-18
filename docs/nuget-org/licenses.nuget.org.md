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
# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>理由

[ライセンス式](../reference/nuspec.md#license)の導入により、個別のライセンス識別子、例外識別子、またはライセンス式に対する参照テキストを提供する信頼できるサービスを用意する要件が発生しました。
このサービスに対する追加の要件は、古いクライアントに下位互換性を提供するために安全に使用できるよう、リンク切れになりにくい安定した URL スキーマを使用することです。

licenses.nuget.org がその役割を果たします。 Nuget.org では、それを使用して、ライセンス式を使用してライセンスを指定するパッケージにライセンス テキストの参照を提供します。 `nuget pack` または他の[クライアント ツール](../install-nuget-client-tools.md)でのパッキングにより、`license` 要素をサポートしない古いクライアントとの下位互換性を提供するため、licenses.nuget.org を指すように [`licenseUrl`](../reference/nuspec.md#licenseurl) 要素が設定されます。

## <a name="protocol"></a>プロトコル

licenses.nuget.org はユーザーがブラウザーで表示するためのもので、コンピューターが判読できる応答は提供されません。
HTTPS プロトコルを使う必要があり、要求は特定の方法で構築することが想定されています。 `GET` 要求のみがサポートされます。
以下で指定する方法で、入力としてライセンス式またはライセンス例外識別子を受け付けます。 ライセンス式のすべての要素は大文字と小文字が区別されるため、licenses.nuget.org へのすべての入力も大文字と小文字が区別されることに注意してください。

### <a name="license-expressions"></a>ライセンス式

#### <a name="request"></a>要求

ライセンス式は (式が 1 つのライセンスで構成される単純な場合も含めて)、[URL でエンコードされ](https://tools.ietf.org/html/rfc3986#section-2.1)、licenses.nuget.org への要求においてパスとして使用される必要があります。

| ライセンス式 | 使用する URL |
|:---|:---|
| MIT                                                | <https://licenses.nuget.org/MIT> |
| (MIT)                                              | <https://licenses.nuget.org/(MIT)> |
| (LGPL-2.0-only WITH FLTK-exception OR Apache-2.0+) | <https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)> |

サービスでは、nuget.org によって受け入れられるライセンス識別子とライセンス例外識別子のみがサポートされます。サポートされていないライセンス識別子またはライセンス例外識別子が含まれるライセンス式、またはライセンス式の構文に準拠しないライセンス式はすべて、無効と見なされます。

#### <a name="response"></a>応答

licenses.nuget.org は、ステータス コード HTTP 200 の有効なライセンス式が含まれる要求、およびライセンス式の説明が含まれる Web ページに応答します。

* 提供されたライセンス式に 1 つのライセンス識別子が含まれる場合、そのライセンス参照テキストを含む Web ページが返されます
* 提供されたライセンス式が複合ライセンス式である場合、ライセンス式と個別のライセンス参照またはライセンス例外参照へのリンクが含まれる Web ページが返されます。

無効なライセンス式が含まれるすべての要求に対しては、HTTP 404 が応答されます。

### <a name="license-exceptions"></a>ライセンス例外

#### <a name="request"></a>要求

ライセンス例外識別子は、URL でエンコードされ、licenses.nuget.org に対する要求でパスとして使用される必要があります。1 つの要求で指定できるライセンス例外識別子は、1 つのみです。 URL のパス部分には、ライセンス例外識別子以外の文字が存在することはできません。

| ライセンス例外識別子 | 使用する URL |
|:---|:---|
|FLTK-exception            | <https://licenses.nuget.org/FLTK-exception> |
|openvpn-openssl-exception | <https://licenses.nuget.org/openvpn-openssl-exception> |

#### <a name="response"></a>応答

licenses.nuget.org は、既知のライセンス例外識別子が含まれる要求に対し、HTTP 200 応答と、指定されたライセンス例外に対する参照テキストが含まれる Web ページで応答します。

サポートされていないライセンス例外識別子が含まれる要求には、HTTP 404 応答が返ってきます。