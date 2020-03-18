---
title: nuget の .config ファイルのリファレンス
description: config、bindingRedirects、packageRestore、solution、packageSource の各セクションを含む NuGet.Config ファイル参照。
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: cd321084c46709e3d1d22872c37485edacd33afa
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428403"
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

| Key | 値 |
| --- | --- |
| dependencyVersion (`packages.config` のみ) | `DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `-DependencyVersion` 値です。 この値は、NuGet パッケージ マネージャー UI でも使用されます。 値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。 |
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

| Key | 値 |
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

| Key | 値 |
| --- | --- |
| enabled | NuGet で自動復元を実行できるかどうかを示すブール値です。 構成ファイル内にこのキーを設定するのでなく、`EnableNuGetPackageRestore` の値で `True` 環境変数を設定することもできます。 |
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

| Key | 値 |
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

| Key | 値 |
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

> [!Tip]
> 指定されたノードに `<clear />` が存在すると、そのノードより前に定義された構成値は無視されます。 [詳細については、「設定の適用方法](../consume-packages/configuring-nuget-behavior.md#how-settings-are-applied)」を参照してください。

### <a name="packagesourcecredentials"></a>packageSourceCredentials

通常、`-username` スイッチおよび `-password` スイッチと `nuget sources` によって指定される、ソースのユーザー名とパスワードを格納します。 `-storepasswordincleartext` オプションが使用されていない場合、既定ではパスワードが暗号化されます。

| Key | 値 |
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

[`nuget setapikey` コマンド](../reference/cli-reference/cli-ref-setapikey.md)で設定される、API キー認証を使用するソースのキーを格納します。

| Key | 値 |
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

| Key | 値 |
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

| Key | 値 |
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

| Key | 値 |
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

| Key | 値 |
| --- | --- |
| format | 既定のパッケージ管理形式を示すブール値。 `1`の場合、format は PackageReference です。 `0`の場合、形式は*app.config*です。 |
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

Windows スタイルの環境変数を使用する必要があることに注意してください (開始と終了は%)Mac/Linux でも同様です。 構成ファイルに `$HOME/NuGetRepository` があると、解決されません。 Mac/Linux では、`%HOME%\NuGetRepository` の値が `/home/myStuff/NuGetRepository`に解決されます。

環境変数が見つからない場合、NuGet は構成ファイルからのリテラル値を使用します。

## <a name="example-config-file"></a>構成ファイルの例

オプションの設定など、いくつかの設定を示す `nuget.config` ファイルの例を次に示します。

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
