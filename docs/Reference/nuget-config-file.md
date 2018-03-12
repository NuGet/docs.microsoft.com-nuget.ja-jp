---
title: "NuGet.Config ファイル参照 | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "config、bindingRedirects、packageRestore、solution、packageSource の各セクションを含む NuGet.Config ファイル参照。"
keywords: "NuGet.Config ファイル、NuGet 構成参照、NuGet 構成オプション"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c76ebcb06adc5e5b862647de6b6f4e19bde87b91
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/08/2018
---
# <a name="nugetconfig-reference"></a>NuGet.Config 参照

NuGet の動作は、「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md)」(NuGet 動作の構成) に記載の各種 `NuGet.Config` ファイルでの設定によって制御されます。

`NuGet.Config` は、最上位の `<configuration>` ノードを含む XML ファイルであり、このトピックで説明するセクション要素が含まれます。 各セクションには、`key` 属性および `value` 属性を持つ 0 個以上の `<add>` 要素が含まれています。 「[examples config file](#example-config-file)」 (構成ファイルの例) を参照してください。 名前の設定には大文字と小文字の区別があり、値には[環境変数](#using-environment-variables)を使用することができます。

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
- [環境変数の使用](#using-environment-variables)
- [構成ファイルの例](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a>config セクション

[`nuget config` コマンド](../tools/cli-ref-config.md)を使用して設定できる、さまざまな構成設定が含まれます。

注: `dependencyVersion` と `repositoryPath` については、`packages.config` を使用するプロジェクトのみに適用されます。 `globalPackagesFolder` PackageReference 形式を使用してプロジェクトにのみ適用されます。

| キー | [値] |
| --- | --- |
| dependencyVersion (`packages.config` のみ) | `-DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `DependencyVersion` 値です。 この値は、NuGet パッケージ マネージャー UI でも使用されます。 値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。 |
| globalPackagesFolder (`packages.config` を使用しないプロジェクト) | 既定のグローバル パッケージ フォルダーの場所です。 既定値は、`%USERPROFILE%\.nuget\packages` (Windows) または `~/.nuget/packages` (Mac/Linux) です。 相対パスは、プロジェクト固有の `Nuget.Config` ファイルで使用できます。 |
| repositoryPath (`packages.config` のみ) | 既定の `$(Solutiondir)/packages` フォルダーではなく、NuGet パッケージをインストールする場所です。 相対パスは、プロジェクト固有の `Nuget.Config` ファイルで使用できます。 |
| defaultPushSource | 操作に対してパッケージ ソースが他に見つからない場合に、既定値として使用すべきパッケージ ソースの URL またはパスを識別します。 |
| http_proxy http_proxy.user http_proxy.password no_proxy | パッケージ ソースに接続するときに使用するプロキシ設定です。`http_proxy` の形式は `http://<username>:<password>@<domain>` とする必要があります。 パスワードは暗号化され、手動で追加することはできません。 `no_proxy` の場合、値はドメイン、バイパス、プロキシ サーバーのコンマ区切りのリストとなります。 これらの値に対して http_proxy および no_proxy の環境変数を使用することもできます。 詳細については、「[NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)」 (NuGet プロキシ設定) (skolima.blogspot.com) を参照してください。 |

**例**:

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\repo" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a>bindingRedirects セクション

パッケージのインストール時に、NuGet で自動バインド リダイレクトを実行するかどうかを構成します。

| キー | [値] |
| --- | --- |
| スキップ | 自動バインド リダイレクトを省略するかどうかを示すブール値です。 既定値は false です。 |

**例**:

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a>packageRestore セクション

*現在のすべてのバージョン (2.7 以降) では無視されます。*

ビルド時のパッケージの復元を制御します。

| キー | [値] |
| --- | --- |
| enabled | NuGet で自動復元を実行できるかどうかを示すブール値です。 構成ファイル内にこのキーを設定するのでなく、`True` の値で `EnableNuGetPackageRestore` 環境変数を設定することもできます。 |
| 自動 | ビルド中に欠落しているパッケージの確認を NuGet で行う必要があるかどうかを示すブール値です。 |

**例**:

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a>ソリューション セクション

ソリューションの `packages` フォルダーをソース管理に含めるかどうかを制御します。 このセクションは、ソリューション フォルダー内の `Nuget.Config` ファイルでのみ機能します。

| キー | [値] |
| --- | --- |
| disableSourceControlIntegration | ソース管理を使用する場合に、パッケージ フォルダーを無視するかどうかを示すブール値です。 既定値は false です。 |

**例**:

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a>パッケージ ソース セクション

`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource`、および `disabledPackageSources` のすべての連携によって、インストール、復元、および更新の操作中にパッケージ リポジトリを NuGet で操作する方法が構成されます。

これらの設定を管理するために、通常は、[`nuget sources` コマンド](../tools/cli-ref-sources.md)が使用されます。ただし、`apikeys` の場合は例外であり、[`nuget setapikey` コマンド](../tools/cli-ref-setapikey.md)によって管理されます。

ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。

### <a name="packagesources"></a>packageSources

すべての既知のパッケージ ソースの一覧を表示します。 復元操作中に、PackageReference 形式を使用して、プロジェクトを使用して、順序は無視されます。 NuGet は、インストールのソースの順序を尊重いたします操作や更新操作を使用して、プロジェクトで`packages.config`です。

| キー | [値] |
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

| キー | [値] |
| --- | --- |
| username | プレーン テキストで表されるソースのユーザー名です。 |
| パスワード | ソースの暗号されたパスワードです。 |
| cleartextpassword | ソースの暗号化されていないパスワードです。 |

**例:**

構成ファイル内の `<packageSourceCredentials>` 要素には、適用可能なソース名ごとに子ノードが含まれます (名前内のスペースは `_x0020+` と置換されます)。 つまり、"Contoso" および "Test Source" という名前のソースの場合は、暗号化されたパスワードを使用するとき、構成ファイルには次の内容が含まれます。

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

| キー | [値] |
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

| キー | [値] |
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

*(2.x のみ。3.x 以降では使用されていない)*

現在アクティブなソースを識別し、すべてのソースの集計を示します。

| キー | [値] |
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

## <a name="using-environment-variables"></a>環境変数の使用

環境変数を `NuGet.Config` 値 (NuGet 3.4 以降) に使用することで、実行時に設定を適用できます。

たとえば、Windows 上の `HOME` 環境変数を `c:\users\username` に設定すると、構成ファイル内の `%HOME%\NuGetRepository` の値は `c:\users\username\NuGetRepository` に解決されます。

同様に、Mac/Linux 上の `HOME` を `/home/myStuff` に設定すると、構成ファイル内の `$HOME/NuGetRepository` は `/home/myStuff/NuGetRepository` に解決されます。

環境変数が見つからない場合、NuGet は構成ファイルからのリテラル値を使用します。

## <a name="example-config-file"></a>構成ファイルの例

複数の設定が含まれている `NuGet.Config` ファイルの例を次に示します。

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
</configuration>
```
