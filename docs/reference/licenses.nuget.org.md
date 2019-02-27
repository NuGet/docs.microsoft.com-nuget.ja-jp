# <a name="licensesnugetorg"></a>licenses.nuget.org

## <a name="rationale"></a>理由

導入に伴い、[ライセンス式](nuspec.md#license)が個別のライセンスの識別子、例外識別子、またはライセンスの式の参照のテキストを提供する信頼性の高いサービスが、要件が登場しました。
このサービスに対する追加の要件は安定した古いクライアントの下位互換性を提供する安全に使用できるように、rot のリンクを受けやすくない URL スキーマです。

Licenses.nuget.org では、そのロールが満たされます。 Nuget.org では、これを使用して、ライセンス式を使用して、ライセンスの指定したパッケージのライセンス text のリファレンスを提供します。 `nuget pack` または他のパッキング[クライアント ツール](https://docs.microsoft.com/en-us/nuget/install-nuget-client-tools)設定、 [ `licenseUrl` ](nuspec.md#licenseurl)後方互換性をサポートしない古いバージョンのクライアントで licenses.nuget.org を指す要素、 `license`要素。

## <a name="protocol"></a>プロトコル

Licenses.nuget.org、ブラウザー内のユーザーを表示するものでは、コンピューターが判読できる応答は提供されません。
HTTPS プロトコルを使用して、要求が特定の方法で構築する必要があります。 のみがサポートされます`GET`要求。
式のライセンスまたはライセンス例外識別子は以下で指定した方法で入力として受け入れます。 注意してください、ライセンスの式のすべての要素が大文字小文字を区別、したがって licenses.nuget.org へのすべての入力が同様で大文字小文字を区別します。

### <a name="license-expressions"></a>ライセンスの式

#### <a name="request"></a>要求

ライセンスの式 (式は、1 つのライセンスで構成される場合は、単純なケースを含む) でなければならない[URL でエンコードされた](https://tools.ietf.org/html/rfc3986#section-2.1)licenses.nuget.org への要求で、パスとして使用するとします。

| ライセンスの式 | 使用する URL |
|:---|:---|
MIT                                                | https://licenses.nuget.org/MIT
(MIT)                                              | https://licenses.nuget.org/(MIT)
(LGPL 2.0-専用と FLTK 例外または Apache-2.0+) | https://licenses.nuget.org/(LGPL-2.0-only%20WITH%20FLTK-exception%20OR%20Apache-2.0+)

サービスでは、ライセンスの識別子と nuget.org で受け入れられるライセンス例外識別子のみをサポートします。サポートされていないライセンス識別子またはライセンス例外識別子が含まれている、またはライセンス式の構文に準拠しないが、すべてのライセンス式は無効と見なされます。

#### <a name="response"></a>応答

Licenses.nuget.org はステータス コード HTTP 200 とライセンスの式の説明を含む web ページの有効なライセンス式が含まれる要求に応答します。
* ライセンスの式を指定する場合は、そのライセンス参照テキストを含む web ページが返されます 1 つのライセンスの識別子を含む
* 指定した場合のライセンスがライセンスの複合式、個別のライセンスまたはライセンス例外参照へのリンクを持つライセンス式を含む web ページが返されます。

HTTP 404 応答でライセンスが無効な式の結果が含まれているすべての要求。

### <a name="license-exceptions"></a>ライセンスの例外

#### <a name="request"></a>要求

ライセンス例外識別子 URL でエンコードされ、licenses.nuget.org への要求でパスとして使用されている必要があります。1 つの要求では、1 つのライセンスの例外の識別子のみを指定できます。 URL のパス部分にライセンス例外識別子だけでなく、追加の文字がありません可能性があります。

| ライセンスの例外の識別子 | 使用する URL |
|:---|:---|
FLTK 例外            | https://licenses.nuget.org/FLTK-exception
openvpn-openssl-exception | https://licenses.nuget.org/openvpn-openssl-exception

#### <a name="response"></a>応答

Licenses.nuget.org は、HTTP 200 応答と、指定したライセンスの例外の参照のテキストを含む web ページの既知のライセンス例外識別子を持つ要求に応答します。

ライセンスがサポートされていない例外識別子を含むすべての要求は HTTP 404 応答が発生します。