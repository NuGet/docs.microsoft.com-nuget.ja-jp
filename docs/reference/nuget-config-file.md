---
title: nuget.config ファイル参照
description: config、bindingRedirects、packageRestore、solution、packageSource の各セクションを含む NuGet.Config ファイル参照。
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: 2eceb6e94a353cb29b83aea114c6cea2acbac266
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426145"
---
# <a name="nugetconfig-reference"></a>nuget.config reference

NuGet の動作が異なる設定によって制御される`NuGet.Config`ファイル」の説明に従って[一般的な NuGet 構成](../consume-packages/configuring-nuget-behavior.md)します。

`nuget.config` は、最上位の `<configuration>` ノードを含む XML ファイルであり、このトピックで説明するセクション要素が含まれます。 各セクションには、0 個以上の項目が含まれています。 「[examples config file](#example-config-file)」 (構成ファイルの例) を参照してください。 名前の設定には大文字と小文字の区別があり、値には[環境変数](#using-environment-variables)を使用することができます。

このトピックの内容:

- [config セクション](#config-section)
- [bindingRedirects セクション](#bindingredirects-section)
- [packageRestore セクション](#packagerestore-section)
- [solution セクション](#solution-section)
- [パッケージ ソース セクション](#package-source-sections):
  - [packageSources](#packagesources)
  - [packageSourceCredentials](#packagesourcecredentials)
  - [apikeys](#apikeys)
  - [disabledPackageSources](#disabledpackagesources)
  - [activePackageSource](#activepackagesource)
- [trustedSigners セクション](#trustedsigners-section)
- [環境変数の使用](#using-environment-variables)
- [構成ファイルの例](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config セクション

[`nuget config` コマンド](../tools/cli-ref-config.md)を使用して設定できる、さまざまな構成設定が含まれます。

`dependencyVersion` `repositoryPath`を使用してプロジェクトにのみ適用`packages.config`します。 `globalPackagesFolder` PackageReference 形式を使用してプロジェクトにのみ適用されます。

| キー | 値 |
| --- | --- |
| dependencyVersion (`packages.config` のみ) | `-DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `DependencyVersion` 値です。 この値は、NuGet パッケージ マネージャー UI でも使用されます。 値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。 |
| globalPackagesFolder (プロジェクトは PackageReference をのみを使用して) | 既定のグローバル パッケージ フォルダーの場所です。 既定値は、`%userprofile%\.nuget\packages` (Windows) または `~/.nuget/packages` (Mac/Linux) です。 相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。 この設定は、優先 NUGET_PACKAGES 環境変数によってオーバーライドされます。 |
| repositoryPath (`packages.config` のみ) | 既定の `$(Solutiondir)/packages` フォルダーではなく、NuGet パッケージをインストールする場所です。 相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。 この設定は、優先 NUGET_PACKAGES 環境変数によってオーバーライドされます。 |
| defaultPushSource | 操作に対してパッケージ ソースが他に見つからない場合に、既定値として使用すべきパッケージ ソースの URL またはパスを識別します。 |
| http_proxy http_proxy.user http_proxy.password no_proxy | パッケージ ソースに接続するときに使用するプロキシ設定です。`http_proxy` の形式は `http://<username>:<password>@<domain>` とする必要があります。 パスワードは暗号化され、手動で追加することはできません。 `no_proxy` の場合、値はドメイン、バイパス、プロキシ サーバーのコンマ区切りのリストとなります。 これらの値に対して http_proxy および no_proxy の環境変数を使用することもできます。 詳細については、「[NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)」 (NuGet プロキシ設定) (skolima.blogspot.com) を参照してください。 |
| signatureValidationMode | パッケージのインストール パッケージの署名を確認し、復元に使用される検証モードを指定します。 値は`accept`、`require`します。 既定値は `accept` です。

**例**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a>bindingRedirects セクション

パッケージのインストール時に、NuGet で自動バインド リダイレクトを実行するかどうかを構成します。

| キー | 値 |
| --- | --- |
| skip | 自動バインド リダイレクトを省略するかどうかを示すブール値です。 既定値は false です。 |

**例**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>packageRestore セクション

ビルド時のパッケージの復元を制御します。

| キー | 値 |
| --- | --- |
| enabled | NuGet で自動復元を実行できるかどうかを示すブール値です。 構成ファイル内にこのキーを設定するのでなく、`True` の値で `EnableNuGetPackageRestore` 環境変数を設定することもできます。 |
| automatic | ビルド中に欠落しているパッケージの確認を NuGet で行う必要があるかどうかを示すブール値です。 |

**例**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>ソリューション セクション

ソリューションの `packages` フォルダーをソース管理に含めるかどうかを制御します。 このセクションは、ソリューション フォルダー内の `nuget.config` ファイルでのみ機能します。

| キー | 値 |
| --- | --- |
| disableSourceControlIntegration | ソース管理を使用する場合に、パッケージ フォルダーを無視するかどうかを示すブール値です。 既定値は false です。 |

**例**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>パッケージ ソース セクション

`packageSources`、 `packageSourceCredentials`、 `apikeys`、 `activePackageSource`、`disabledPackageSources`と`trustedSigners`パッケージ リポジトリとインストール、復元、および更新操作中に NuGet の動作を構成するすべての作業です。

[ `nuget sources`コマンド](../tools/cli-ref-sources.md)を除き、これらの設定を管理するために使用が一般的に`apikeys`を使用して管理される、 [ `nuget setapikey`コマンド](../tools/cli-ref-setapikey.md)、および`trustedSigners`管理されます。使用して、 [ `nuget trusted-signers`コマンド](../tools/cli-ref-trusted-signers.md)します。

ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。

### <a name="packagesources"></a>packageSources

すべての既知のパッケージ ソースの一覧を表示します。 PackageReference 形式を使用して任意のプロジェクトと復元操作中に、順序は無視されます。 NuGet のインストール ソースの順序を尊重する操作や更新操作を使用するプロジェクトで`packages.config`します。

| キー | 値 |
| --- | --- |
| (パッケージ ソースに割り当てる名前) | パッケージ ソースのパスまたは URL です。 |

**例**:

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a>packageSourceCredentials

通常、`-username` スイッチおよび `-password` スイッチと `nuget sources` によって指定される、ソースのユーザー名とパスワードを格納します。 `-storepasswordincleartext` オプションが使用されていない場合、既定ではパスワードが暗号化されます。

| キー | 値 |
| --- | --- |
| username | プレーン テキストで表されるソースのユーザー名です。 |
| password | ソースの暗号されたパスワードです。 |
| cleartextpassword | ソースの暗号化されていないパスワードです。 |

**例:**

構成ファイル内の `<packageSourceCredentials>` 要素には、適用可能なソース名ごとに子ノードが含まれます (名前内のスペースは `_x0020_` と置換されます)。 つまり、"Contoso" および "Test Source" という名前のソースの場合は、暗号化されたパスワードを使用するとき、構成ファイルには次の内容が含まれます。

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="Password" value="..." />
    </Test_x0020_Source>
</packageSourceCredentials>
```

暗号化されていないパスワードを使用する場合:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="33f!!lloppa" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

[`nuget setapikey` コマンド](../tools/cli-ref-setapikey.md)で設定される、API キー認証を使用するソースのキーを格納します。

| キー | 値 |
| --- | --- |
| (ソース URL) | 暗号化された API キー。 |

**例**:

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a>disabledPackageSources

現在無効になっているソースを識別します。 空の場合もあります。

| キー | 値 |
| --- | --- |
| (ソースの名前) | ソースが無効になっているかどうかを示すブール値です。 |

**例:**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a>activePackageSource

*(2.x のみ。3.x 以降では非推奨とされます)*

現在アクティブなソースを識別し、すべてのソースの集計を示します。

| キー | 値 |
| --- | --- |
| (ソースの名前) または `All` | キーがソースの名前である場合は、ソースのパスまたは URL が値となります。 `All` の場合は、値を `(Aggregate source)` にして、無効になっていないすべてのパッケージ ソースを結合する必要があります。 |

**例**:

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a>trustedSigners セクション

ストアには、パッケージをインストールまたは復元中に許可するために使用する署名者が信頼されています。 ユーザーを設定するとこの一覧を空にすることはできません`signatureValidationMode`に`require`します。 

このセクションを更新するためには、 [ `nuget trusted-signers`コマンド](../tools/cli-ref-trusted-signers.md)します。

**スキーマ**:

信頼できる署名者のコレクションがある`certificate`項目を指定した署名者を識別するすべての証明書を登録します。 信頼できる署名者には、いずれかを指定できる、`Author`または`Repository`します。

信頼された*リポジトリ*も指定します、`serviceIndex`リポジトリの (は有効なある`https`uri) のセミコロンで区切られたリストを必要に応じて指定できますと`owners`者が信頼されているさらを制限するにはその特定のリポジトリ。

証明書フィンガー プリントを使用するサポートされているハッシュ アルゴリズム`SHA256`、`SHA384`と`SHA512`します。

場合、`certificate`指定`allowUntrustedRoot`として`true`特定の証明書が信頼されていないルートにチェーン署名の検証の一部として証明書チェーンの構築中に許可されました。

**例**:

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="using-environment-variables"></a>環境変数の使用

環境変数を `nuget.config` 値 (NuGet 3.4 以降) に使用することで、実行時に設定を適用できます。

たとえば、Windows 上の `HOME` 環境変数を `c:\users\username` に設定すると、構成ファイル内の `%HOME%\NuGetRepository` の値は `c:\users\username\NuGetRepository` に解決されます。

同様に、Mac/Linux 上の `HOME` を `/home/myStuff` に設定すると、構成ファイル内の `%HOME%/NuGetRepository` は `/home/myStuff/NuGetRepository` に解決されます。

環境変数が見つからない場合、NuGet は構成ファイルからのリテラル値を使用します。

## <a name="example-config-file"></a>構成ファイルの例

複数の設定が含まれている `nuget.config` ファイルの例を次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable. On Mac/Linux,
            use $PACKAGE_HOME/External as the value.
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%\External" />

        <!--
            Used to specify default source for the push command.
            See: nuget.exe help push
        -->

        <add key="defaultPushSource" value="https://MyRepo/ES/api/v2/package" />

        <!-- Proxy settings -->
        <add key="http_proxy" value="host" />
        <add key="http_proxy.user" value="username" />
        <add key="http_proxy.password" value="encrypted_password" />
    </config>

    <packageRestore>
        <!-- Allow NuGet to download missing packages -->
        <add key="enabled" value="True" />

        <!-- Automatically check for missing packages during build in Visual Studio -->
        <add key="automatic" value="True" />
    </packageRestore>

    <!--
        Used to specify the default Sources for list, install and update.
        See: nuget.exe help list
        See: nuget.exe help install
        See: nuget.exe help update
    -->
    <packageSources>
        <add key="NuGet official package source" value="https://api.nuget.org/v3/index.json" />
        <add key="MyRepo - ES" value="https://MyRepo/ES/nuget" />
    </packageSources>

    <!-- Used to store credentials -->
    <packageSourceCredentials />

    <!-- Used to disable package sources  -->
    <disabledPackageSources />

    <!--
        Used to specify default API key associated with sources.
        See: nuget.exe help setApiKey
        See: nuget.exe help push
        See: nuget.exe help mirror
    -->
    <apikeys>
        <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
    </apikeys>

    <!--
        Used to specify trusted signers to allow during signature verification.
        See: nuget.exe help trusted-signers
    -->
    <trustedSigners>
        <author name="microsoft">
            <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
