---
title: nuget の .config ファイルのリファレンス
description: config、bindingRedirects、packageRestore、solution、packageSource の各セクションを含む NuGet.Config ファイル参照。
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 0b052bd03625172f1b941c365cbedf7629809d6f
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825190"
---
# <a name="nugetconfig-reference"></a>nuget の .config リファレンス

NuGet の動作は、[一般的な nuget 構成](../consume-packages/configuring-nuget-behavior.md)で説明されているように、さまざまな `NuGet.Config` または `nuget.config` ファイルの設定によって制御されます。

`nuget.config` は、最上位の `<configuration>` ノードを含む XML ファイルであり、このトピックで説明するセクション要素が含まれます。 各セクションには、0個以上の項目が含まれています。 「[examples config file](#example-config-file)」 (構成ファイルの例) を参照してください。 名前の設定には大文字と小文字の区別があり、値には[環境変数](#using-environment-variables)を使用することができます。

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config セクション

[`nuget config` コマンド](../reference/cli-reference/cli-ref-config.md)を使用して設定できる、さまざまな構成設定が含まれます。

`dependencyVersion` と `repositoryPath` は `packages.config`を使用するプロジェクトにのみ適用されます。 `globalPackagesFolder` は、PackageReference 形式を使用するプロジェクトにのみ適用されます。

| [キー] | Value |
| --- | --- |
| dependencyVersion (`packages.config` のみ) | `-DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `DependencyVersion` 値です。 この値は、NuGet パッケージ マネージャー UI でも使用されます。 値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。 |
| Globalパッケージフォルダー (PackageReference のみを使用するプロジェクト) | 既定のグローバル パッケージ フォルダーの場所です。 既定値は、`%userprofile%\.nuget\packages` (Windows) または `~/.nuget/packages` (Mac/Linux) です。 相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。 この設定は、NUGET_PACKAGES 環境変数によってオーバーライドされます。これは、優先されます。 |
| repositoryPath (`packages.config` のみ) | 既定の `$(Solutiondir)/packages` フォルダーではなく、NuGet パッケージをインストールする場所です。 相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。 この設定は、NUGET_PACKAGES 環境変数によってオーバーライドされます。これは、優先されます。 |
| defaultPushSource | 操作に対してパッケージ ソースが他に見つからない場合に、既定値として使用すべきパッケージ ソースの URL またはパスを識別します。 |
| http_proxy http_proxy.user http_proxy.password no_proxy | パッケージ ソースに接続するときに使用するプロキシ設定です。`http_proxy` の形式は `http://<username>:<password>@<domain>` とする必要があります。 パスワードは暗号化され、手動で追加することはできません。 `no_proxy` の場合、値はドメイン、バイパス、プロキシ サーバーのコンマ区切りのリストとなります。 これらの値に対して http_proxy および no_proxy の環境変数を使用することもできます。 詳細については、「[NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)」 (NuGet プロキシ設定) (skolima.blogspot.com) を参照してください。 |
| signatureValidationMode | パッケージのインストールおよび復元用のパッケージ署名の検証に使用する検証モードを指定します。 値は `accept`、`require`です。 既定値は `accept` です。

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

| [キー] | Value |
| --- | --- |
| スキップ | 自動バインド リダイレクトを省略するかどうかを示すブール値です。 既定値は false です。 |

**例**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>packageRestore セクション

ビルド時のパッケージの復元を制御します。

| [キー] | Value |
| --- | --- |
| が有効 | NuGet で自動復元を実行できるかどうかを示すブール値です。 構成ファイル内にこのキーを設定するのでなく、`True` の値で `EnableNuGetPackageRestore` 環境変数を設定することもできます。 |
| 自動 | ビルド中に欠落しているパッケージの確認を NuGet で行う必要があるかどうかを示すブール値です。 |

**例**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>ソリューション セクション

ソリューションの `packages` フォルダーをソース管理に含めるかどうかを制御します。 このセクションは、ソリューション フォルダー内の `nuget.config` ファイルでのみ機能します。

| [キー] | Value |
| --- | --- |
| disableSourceControlIntegration | ソース管理を使用する場合に、パッケージ フォルダーを無視するかどうかを示すブール値です。 既定値は false です。 |

**例**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>パッケージ ソース セクション

`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource`、`disabledPackageSources`、`trustedSigners` のすべてが連携して、インストール、復元、および更新の操作中に、NuGet がパッケージリポジトリを操作する方法を構成します。

[`nuget sources` コマンド](../reference/cli-reference/cli-ref-sources.md)は、通常、これらの設定を管理するために使用されます。ただし、 [`nuget setapikey` コマンド](../reference/cli-reference/cli-ref-setapikey.md)を使用して管理される `apikeys` と、 [`nuget trusted-signers` コマンド](../reference/cli-reference/cli-ref-trusted-signers.md)を使用して管理される `trustedSigners` は除きます。

ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。

### <a name="packagesources"></a>packageSources

すべての既知のパッケージ ソースの一覧を表示します。 この順序は、復元操作中には無視され、PackageReference 形式を使用するプロジェクトでは無視されます。 NuGet は、`packages.config`を使用したプロジェクトでのインストールおよび更新操作のソースの順序を尊重します。

| [キー] | Value |
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

| [キー] | Value |
| --- | --- |
| username | プレーン テキストで表されるソースのユーザー名です。 |
| のパスワード | ソースの暗号されたパスワードです。 |
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

[`nuget setapikey` コマンド](../reference/cli-reference/cli-ref-setapikey.md)で設定される、API キー認証を使用するソースのキーを格納します。

| [キー] | Value |
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

| [キー] | Value |
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

| [キー] | Value |
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

## <a name="trustedsigners-section"></a>trustedSigners 者セクション

インストールまたは復元中にパッケージを許可するために使用される信頼された署名者を格納します。 ユーザーが `require`に `signatureValidationMode` を設定した場合、この一覧を空にすることはできません。 

このセクションは、 [`nuget trusted-signers` コマンド](../reference/cli-reference/cli-ref-trusted-signers.md)を使用して更新できます。

**[スキーマ]** :

信頼できる署名者には、特定の署名者を識別するすべての証明書を登録する `certificate` 項目のコレクションがあります。 信頼できる署名者は、`Author` または `Repository`のいずれかになります。

また、信頼された*リポジトリ*は、リポジトリの `serviceIndex` (有効な `https` uri である必要があります) を指定します。また、必要に応じて、特定のリポジトリから信頼できるユーザーを制限するために、セミコロンで区切られた `owners` の一覧を指定することもできます。

証明書のフィンガープリントに使用されるサポートされているハッシュアルゴリズムは、`SHA256`、`SHA384`、および `SHA512`です。

`certificate` がとして `allowUntrustedRoot` を指定する場合 `true` 署名の検証の一部として証明書チェーンを構築するときに、指定した証明書を信頼されていないルートにチェーンすることを許可します。

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

## <a name="fallbackpackagefolders-section"></a>fallbackPackageFolders セクション

*(3.5 +)* パッケージがフォールバックフォルダーに存在する場合に作業を行う必要がないように、パッケージをプレインストールする方法を提供します。 フォールバックパッケージフォルダーには、グローバルパッケージフォルダーとまったく同じフォルダーとファイル構造があり*ます。 nupkg*は存在し、すべてのファイルが抽出されます。

この構成の参照ロジックは次のとおりです。

- [グローバルパッケージフォルダー] で、パッケージ/バージョンが既にダウンロードされているかどうかを確認します。

- フォールバックフォルダーでパッケージ/バージョンの一致を確認します。

いずれかの参照が成功した場合、ダウンロードは必要ありません。

一致するものが見つからない場合、NuGet はファイルソースを確認し、次に http ソースを確認してから、パッケージをダウンロードします。

| [キー] | Value |
| --- | --- |
| (フォールバックフォルダーの名前) | フォールバックフォルダーへのパス。 |

**例**:

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>packageManagement セクション

既定のパッケージ管理形式である*app.config*または PackageReference を設定します。 SDK スタイルのプロジェクトは常に PackageReference を使用します。

| [キー] | Value |
| --- | --- |
| 書式 | 既定のパッケージ管理形式を示すブール値。 `1`の場合、format は PackageReference です。 `0`の場合、形式は*app.config*です。 |
| 無効 | 最初のパッケージのインストール時に既定のパッケージ形式を選択するようにプロンプトを表示するかどうかを示すブール値。 `False` プロンプトを非表示にします。 |

**例**:

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
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
