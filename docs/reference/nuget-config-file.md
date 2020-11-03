---
title: nuget.config ファイル参照
description: config、bindingRedirects、packageRestore、solution、packageSource の各セクションを含む NuGet.Config ファイル参照。
author: karann-msft
ms.author: karann
ms.date: 08/13/2019
ms.topic: reference
ms.openlocfilehash: 371f0d934fcd3c1f111d277131553c1eed0200be
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93238102"
---
# <a name="nugetconfig-reference"></a>nuget.config リファレンス

NuGet の動作は `NuGet.Config` 、 `nuget.config` 「 [一般的な nuget 構成](../consume-packages/configuring-nuget-behavior.md)」で説明されているように、異なるファイルまたはファイルの設定によって制御されます。

`nuget.config` は、最上位の `<configuration>` ノードを含む XML ファイルであり、このトピックで説明するセクション要素が含まれます。 各セクションには、0個以上の項目が含まれています。 「[examples config file](#example-config-file)」 (構成ファイルの例) を参照してください。 名前の設定には大文字と小文字の区別があり、値には[環境変数](#using-environment-variables)を使用することができます。

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config セクション

には、 [ `nuget config` コマンド](../reference/cli-reference/cli-ref-config.md)を使用して設定できるその他の構成設定が含まれています。

`dependencyVersion` および `repositoryPath` は、を使用するプロジェクトにのみ適用さ `packages.config` れます。 `globalPackagesFolder` PackageReference 形式を使用するプロジェクトにのみ適用されます。

| キー | 値 |
| --- | --- |
| dependencyVersion (`packages.config` のみ) | `-DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `DependencyVersion` 値です。 この値は、NuGet パッケージ マネージャー UI でも使用されます。 値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。 |
| Globalパッケージフォルダー (PackageReference のみを使用するプロジェクト) | 既定のグローバル パッケージ フォルダーの場所です。 既定値は、`%userprofile%\.nuget\packages` (Windows) または `~/.nuget/packages` (Mac/Linux) です。 相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。 この設定は、NUGET_PACKAGES 環境変数によってオーバーライドされます。これは、優先されます。 |
| repositoryPath (`packages.config` のみ) | 既定の `$(Solutiondir)/packages` フォルダーではなく、NuGet パッケージをインストールする場所です。 相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。 この設定は、NUGET_PACKAGES 環境変数によってオーバーライドされます。これは、優先されます。 |
| defaultPushSource | 操作に対してパッケージ ソースが他に見つからない場合に、既定値として使用すべきパッケージ ソースの URL またはパスを識別します。 |
| http_proxy http_proxy.user http_proxy.password no_proxy | パッケージ ソースに接続するときに使用するプロキシ設定です。`http_proxy` の形式は `http://<username>:<password>@<domain>` とする必要があります。 パスワードは暗号化され、手動で追加することはできません。 `no_proxy` の場合、値はドメイン、バイパス、プロキシ サーバーのコンマ区切りのリストとなります。 これらの値に対して http_proxy および no_proxy の環境変数を使用することもできます。 詳細については、「[NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)」 (NuGet プロキシ設定) (skolima.blogspot.com) を参照してください。 |
| signatureValidationMode | パッケージのインストールおよび復元用のパッケージ署名の検証に使用する検証モードを指定します。 値は `accept` 、、 `require` です。 既定値は `accept` です。

**例** :

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

**例** :

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

**例** :

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

**例** :

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>パッケージ ソース セクション

`packageSources`、、 `packageSourceCredentials` `apikeys` 、、およびはすべて連携して、 `activePackageSource` `disabledPackageSources` `trustedSigners` インストール、復元、および更新の各操作中に、NuGet がパッケージリポジトリを操作する方法を構成します。

コマンド[ `nuget sources` は](../reference/cli-reference/cli-ref-sources.md)、コマンドを使用して管理され、コマンドを使用して管理される以外は、これらの設定を管理するために一般的に使用され `apikeys` [ `nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md) `trustedSigners` ます。 [ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md)

ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。

### <a name="packagesources"></a>packageSources

すべての既知のパッケージ ソースの一覧を表示します。 この順序は、復元操作中には無視され、PackageReference 形式を使用するプロジェクトでは無視されます。 NuGet は、を使用して、プロジェクトでのインストールおよび更新操作のソースの順序を尊重し `packages.config` ます。

| キー | 値 |
| --- | --- |
| (パッケージ ソースに割り当てる名前) | パッケージ ソースのパスまたは URL です。 |

**例** :

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
必要に応じて、有効な認証の種類をスイッチで指定でき `-validauthenticationtypes` ます。

| キー | 値 |
| --- | --- |
| username | プレーン テキストで表されるソースのユーザー名です。 |
| password | ソースの暗号されたパスワードです。 暗号化されたパスワードは Windows でのみサポートされ、同じコンピューターで、元の暗号化と同じユーザーが使用する場合にのみ、暗号化を解除できます。 |
| cleartextpassword | ソースの暗号化されていないパスワードです。 注: 環境変数はセキュリティを強化するために使用できます。 |
| validauthenticationtypes | このソースに対して有効な認証の種類のコンマ区切りのリスト。 サーバーによって NTLM または Negotiate がアドバタイズされていて、基本メカニズムを使用して資格情報を送信する必要がある場合は、これを `basic` に設定します。たとえば、オンプレミスの Azure DevOps Server で PAT を使用する場合などです。 その他の有効な値には、`negotiate`、`kerberos`、`ntlm`、`digest` などがありますが、これらの値は役に立たない可能性があります。 |

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

暗号化されていないパスワードを環境変数に格納する場合:

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="ClearTextPassword" value="%ContosoPassword%" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="%TestSourcePassword%" />
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

また、有効な認証方法を指定することもできます。

```xml
<packageSourceCredentials>
    <Contoso>
        <add key="Username" value="user@contoso.com" />
        <add key="Password" value="..." />
        <add key="ValidAuthenticationTypes" value="basic" />
    </Contoso>
    <Test_x0020_Source>
        <add key="Username" value="user" />
        <add key="ClearTextPassword" value="hal+9ooo_da!sY" />
        <add key="ValidAuthenticationTypes" value="basic, negotiate" />
    </Test_x0020_Source>
</packageSourceCredentials>
```

### <a name="apikeys"></a>apikeys

[ `nuget setapikey` コマンド](../reference/cli-reference/cli-ref-setapikey.md)で設定された、API キー認証を使用するソースのキーを格納します。

| キー | 値 |
| --- | --- |
| (ソース URL) | 暗号化された API キー。 |

**例** :

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

**例** :

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a>trustedSigners 者セクション

インストールまたは復元中にパッケージを許可するために使用される信頼された署名者を格納します。 ユーザーがに設定した場合、この一覧を空にすることはできません `signatureValidationMode` `require` 。 

このセクションは、 [ `nuget trusted-signers` コマンド](../reference/cli-reference/cli-ref-trusted-signers.md)を使用して更新できます。

**[スキーマ]** :

信頼できる署名者には、 `certificate` 特定の署名者を識別するすべての証明書を登録する項目のコレクションがあります。 信頼できる署名者は、またはのいずれか `Author` `Repository` です。

信頼された *リポジトリ* では、リポジトリのを指定することもできます `serviceIndex` (これは有効な uri である必要があります)。また、必要に応じて、 `https` のセミコロンで区切られた一覧を指定して、 `owners` その特定のリポジトリから信頼できるユーザーをさらに制限することもできます。

証明書のフィンガープリントに使用されるサポートされているハッシュアルゴリズムは `SHA256` 、、 `SHA384` および `SHA512` です。

がを指定した場合、 `certificate` `allowUntrustedRoot` 指定された `true` 証明書は、署名の検証の一部として証明書チェーンを構築するときに、信頼されていないルートにチェーンできます。

**例** :

```xml
<trustedSigners>
    <author name="microsoft">
        <certificate fingerprint="3F9001EA83C560D712C24CF213C3D312CB3BFF51EE89435D3430BD06B5D0EECE" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
    </author>
    <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
        <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        <owners>microsoft;aspnet;nuget</owners>
    </repository>
</trustedSigners>
```

## <a name="fallbackpackagefolders-section"></a>fallbackPackageFolders セクション

*(3.5 +)* パッケージがフォールバックフォルダーに存在する場合に作業を行う必要がないように、パッケージをプレインストールする方法を提供します。 フォールバックパッケージフォルダーには、グローバルパッケージフォルダーとまったく同じフォルダーとファイル構造があり *ます。 nupkg* は存在し、すべてのファイルが抽出されます。

この構成の参照ロジックは次のとおりです。

- [グローバルパッケージフォルダー] で、パッケージ/バージョンが既にダウンロードされているかどうかを確認します。

- フォールバックフォルダーでパッケージ/バージョンの一致を確認します。

いずれかの参照が成功した場合、ダウンロードは必要ありません。

一致するものが見つからない場合、NuGet はファイルソースを確認し、次に http ソースを確認してから、パッケージをダウンロードします。

| キー | 値 |
| --- | --- |
| (フォールバックフォルダーの名前) | フォールバックフォルダーへのパス。 |

**例** :

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a>packageManagement セクション

*packages.config* または PackageReference の既定のパッケージ管理形式を設定します。 SDK スタイルのプロジェクトは常に PackageReference を使用します。

| キー | 値 |
| --- | --- |
| format | 既定のパッケージ管理形式を示すブール値。 `1`の場合、format は PackageReference です。 `0`の場合、format は *packages.config* です。 |
| disabled | 最初のパッケージのインストール時に既定のパッケージ形式を選択するようにプロンプトを表示するかどうかを示すブール値。 `False` プロンプトを非表示にします。 |

**例** :

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a>環境変数の使用

環境変数を `nuget.config` 値 (NuGet 3.4 以降) に使用することで、実行時に設定を適用できます。

たとえば、Windows 上の `HOME` 環境変数を `c:\users\username` に設定すると、構成ファイル内の `%HOME%\NuGetRepository` の値は `c:\users\username\NuGetRepository` に解決されます。

Windows スタイルの環境変数を使用する必要があることに注意してください (開始と終了は%)Mac/Linux でも同様です。 `$HOME/NuGetRepository`構成ファイルでのの保持は解決されません。 Mac/Linux では、の値 `%HOME%/NuGetRepository` はに解決され `/home/myStuff/NuGetRepository` ます。

環境変数が見つからない場合、NuGet は構成ファイルからのリテラル値を使用します。 たとえば、次の `%MY_UNDEFINED_VAR%/NuGetRepository` ように解決されます。 `path/to/current_working_dir/$MY_UNDEFINED_VAR/NuGetRepository`

次の表は、NuGet.Config ファイルの環境 variable 構文とパス区切り記号のサポートを示しています。

### <a name="nugetconfig-environment-variable-support"></a>NuGet.Config 環境変数のサポート

| 構文 | Dir の区切り記号 | Windows nuget.exe | Windows dotnet.exe | Mac nuget.exe (Mono) | Mac dotnet.exe |
|---|---|---|---|---|---|
| `%MY_VAR%` | `/`  | はい | はい | はい | はい |
| `%MY_VAR%` | `\`  | はい | はい | いいえ | いいえ |
| `$MY_VAR` | `/`  | いいえ | いいえ | いいえ | いいえ |
| `$MY_VAR` | `\`  | いいえ | いいえ | いいえ | いいえ |


## <a name="example-config-file"></a>構成ファイルの例

`nuget.config`オプションの設定など、いくつかの設定を示すサンプルファイルを次に示します。

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
    <config>
        <!--
            Used to specify the default location to expand packages.
            See: nuget.exe help install
            See: nuget.exe help update

            In this example, %PACKAGEHOME% is an environment variable.
            This syntax works on Windows/Mac/Linux
        -->
        <add key="repositoryPath" value="%PACKAGEHOME%/External" />

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
            <certificate fingerprint="AA12DA22A49BCE7D5C1AE64CC1F3D892F150DA76140F210ABD2CBFFCA2C18A27" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
        </author>
        <repository name="nuget.org" serviceIndex="https://api.nuget.org/v3/index.json">
            <certificate fingerprint="0E5F38F57DC1BCC806D8494F4F90FBCEDD988B46760709CBEEC6F4219AA6157D" hashAlgorithm="SHA256" allowUntrustedRoot="false" />
            <owners>microsoft;aspnet;nuget</owners>
        </repository>
    </trustedSigners>
</configuration>
```
