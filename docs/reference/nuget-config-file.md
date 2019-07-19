---
title: nuget の .config ファイルのリファレンス
description: config、bindingRedirects、packageRestore、solution、packageSource の各セクションを含む NuGet.Config ファイル参照。
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: b03bb8da0191a679671e5898ac70fff2024d52f2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317220"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="8878a-103">nuget の .config リファレンス</span><span class="sxs-lookup"><span data-stu-id="8878a-103">nuget.config reference</span></span>

<span data-ttu-id="8878a-104">Nuget の動作は、「 `NuGet.Config` [一般的な nuget 構成](../consume-packages/configuring-nuget-behavior.md)」で説明されているように、さまざまなファイルの設定によって制御されます。</span><span class="sxs-lookup"><span data-stu-id="8878a-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8878a-105">`nuget.config` は、最上位の `<configuration>` ノードを含む XML ファイルであり、このトピックで説明するセクション要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="8878a-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="8878a-106">各セクションには、0個以上の項目が含まれています。</span><span class="sxs-lookup"><span data-stu-id="8878a-106">Each section contains zero or more items.</span></span> <span data-ttu-id="8878a-107">「[examples config file](#example-config-file)」 (構成ファイルの例) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8878a-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="8878a-108">名前の設定には大文字と小文字の区別があり、値には[環境変数](#using-environment-variables)を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="8878a-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="8878a-109">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="8878a-109">In this topic:</span></span>

- [<span data-ttu-id="8878a-110">config セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-110">config section</span></span>](#config-section)
- [<span data-ttu-id="8878a-111">bindingRedirects セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="8878a-112">packageRestore セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="8878a-113">solution セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="8878a-114">[パッケージ ソース セクション](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="8878a-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="8878a-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="8878a-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="8878a-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8878a-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="8878a-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="8878a-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="8878a-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8878a-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="8878a-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8878a-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="8878a-120">trustedSigners 者セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="8878a-121">環境変数の使用</span><span class="sxs-lookup"><span data-stu-id="8878a-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="8878a-122">構成ファイルの例</span><span class="sxs-lookup"><span data-stu-id="8878a-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="8878a-123">config セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-123">config section</span></span>

<span data-ttu-id="8878a-124">[`nuget config` コマンド](../reference/cli-reference/cli-ref-config.md)を使用して設定できる、さまざまな構成設定が含まれます。</span><span class="sxs-lookup"><span data-stu-id="8878a-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="8878a-125">`dependencyVersion`および`repositoryPath`は、を使用`packages.config`するプロジェクトにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="8878a-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="8878a-126">`globalPackagesFolder`PackageReference 形式を使用するプロジェクトにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="8878a-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="8878a-127">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-127">Key</span></span> | <span data-ttu-id="8878a-128">値</span><span class="sxs-lookup"><span data-stu-id="8878a-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-129">dependencyVersion (`packages.config` のみ)</span><span class="sxs-lookup"><span data-stu-id="8878a-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="8878a-130">`-DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `DependencyVersion` 値です。</span><span class="sxs-lookup"><span data-stu-id="8878a-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="8878a-131">この値は、NuGet パッケージ マネージャー UI でも使用されます。</span><span class="sxs-lookup"><span data-stu-id="8878a-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="8878a-132">値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。</span><span class="sxs-lookup"><span data-stu-id="8878a-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="8878a-133">Globalパッケージフォルダー (PackageReference のみを使用するプロジェクト)</span><span class="sxs-lookup"><span data-stu-id="8878a-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="8878a-134">既定のグローバル パッケージ フォルダーの場所です。</span><span class="sxs-lookup"><span data-stu-id="8878a-134">The location of the default global packages folder.</span></span> <span data-ttu-id="8878a-135">既定値は、`%userprofile%\.nuget\packages` (Windows) または `~/.nuget/packages` (Mac/Linux) です。</span><span class="sxs-lookup"><span data-stu-id="8878a-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="8878a-136">相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。</span><span class="sxs-lookup"><span data-stu-id="8878a-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="8878a-137">この設定は、優先される NUGET_PACKAGES 環境変数によってオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="8878a-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="8878a-138">repositoryPath (`packages.config` のみ)</span><span class="sxs-lookup"><span data-stu-id="8878a-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="8878a-139">既定の `$(Solutiondir)/packages` フォルダーではなく、NuGet パッケージをインストールする場所です。</span><span class="sxs-lookup"><span data-stu-id="8878a-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="8878a-140">相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。</span><span class="sxs-lookup"><span data-stu-id="8878a-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="8878a-141">この設定は、優先される NUGET_PACKAGES 環境変数によってオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="8878a-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="8878a-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="8878a-142">defaultPushSource</span></span> | <span data-ttu-id="8878a-143">操作に対してパッケージ ソースが他に見つからない場合に、既定値として使用すべきパッケージ ソースの URL またはパスを識別します。</span><span class="sxs-lookup"><span data-stu-id="8878a-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="8878a-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="8878a-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="8878a-145">パッケージ ソースに接続するときに使用するプロキシ設定です。`http_proxy` の形式は `http://<username>:<password>@<domain>` とする必要があります。</span><span class="sxs-lookup"><span data-stu-id="8878a-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="8878a-146">パスワードは暗号化され、手動で追加することはできません。</span><span class="sxs-lookup"><span data-stu-id="8878a-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="8878a-147">`no_proxy` の場合、値はドメイン、バイパス、プロキシ サーバーのコンマ区切りのリストとなります。</span><span class="sxs-lookup"><span data-stu-id="8878a-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="8878a-148">これらの値に対して http_proxy および no_proxy の環境変数を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="8878a-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="8878a-149">詳細については、「[NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)」 (NuGet プロキシ設定) (skolima.blogspot.com) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="8878a-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="8878a-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="8878a-150">signatureValidationMode</span></span> | <span data-ttu-id="8878a-151">パッケージのインストールおよび復元用のパッケージ署名の検証に使用する検証モードを指定します。</span><span class="sxs-lookup"><span data-stu-id="8878a-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="8878a-152">値は`accept`、 `require`、です。</span><span class="sxs-lookup"><span data-stu-id="8878a-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="8878a-153">既定値は `accept` です。</span><span class="sxs-lookup"><span data-stu-id="8878a-153">Defaults to `accept`.</span></span>

<span data-ttu-id="8878a-154">**例**:</span><span class="sxs-lookup"><span data-stu-id="8878a-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="8878a-155">bindingRedirects セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-155">bindingRedirects section</span></span>

<span data-ttu-id="8878a-156">パッケージのインストール時に、NuGet で自動バインド リダイレクトを実行するかどうかを構成します。</span><span class="sxs-lookup"><span data-stu-id="8878a-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="8878a-157">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-157">Key</span></span> | <span data-ttu-id="8878a-158">値</span><span class="sxs-lookup"><span data-stu-id="8878a-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-159">skip</span><span class="sxs-lookup"><span data-stu-id="8878a-159">skip</span></span> | <span data-ttu-id="8878a-160">自動バインド リダイレクトを省略するかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="8878a-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="8878a-161">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="8878a-161">The default is false.</span></span> |

<span data-ttu-id="8878a-162">**例**:</span><span class="sxs-lookup"><span data-stu-id="8878a-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="8878a-163">packageRestore セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-163">packageRestore section</span></span>

<span data-ttu-id="8878a-164">ビルド時のパッケージの復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="8878a-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="8878a-165">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-165">Key</span></span> | <span data-ttu-id="8878a-166">値</span><span class="sxs-lookup"><span data-stu-id="8878a-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-167">enabled</span><span class="sxs-lookup"><span data-stu-id="8878a-167">enabled</span></span> | <span data-ttu-id="8878a-168">NuGet で自動復元を実行できるかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="8878a-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="8878a-169">構成ファイル内にこのキーを設定するのでなく、`True` の値で `EnableNuGetPackageRestore` 環境変数を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="8878a-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="8878a-170">automatic</span><span class="sxs-lookup"><span data-stu-id="8878a-170">automatic</span></span> | <span data-ttu-id="8878a-171">ビルド中に欠落しているパッケージの確認を NuGet で行う必要があるかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="8878a-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="8878a-172">**例**:</span><span class="sxs-lookup"><span data-stu-id="8878a-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="8878a-173">ソリューション セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-173">solution section</span></span>

<span data-ttu-id="8878a-174">ソリューションの `packages` フォルダーをソース管理に含めるかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="8878a-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="8878a-175">このセクションは、ソリューション フォルダー内の `nuget.config` ファイルでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="8878a-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="8878a-176">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-176">Key</span></span> | <span data-ttu-id="8878a-177">値</span><span class="sxs-lookup"><span data-stu-id="8878a-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="8878a-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="8878a-179">ソース管理を使用する場合に、パッケージ フォルダーを無視するかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="8878a-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="8878a-180">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="8878a-180">The default value is false.</span></span> |

<span data-ttu-id="8878a-181">**例**:</span><span class="sxs-lookup"><span data-stu-id="8878a-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="8878a-182">パッケージ ソース セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-182">Package source sections</span></span>

<span data-ttu-id="8878a-183">`packageSources` 、`packageSourceCredentials`、 、`disabledPackageSources` 、およびは`trustedSigners`すべて連携して、インストール、復元、および更新の各操作中に、NuGet がパッケージリポジトリを操作する方法を構成します。 `activePackageSource` `apikeys`</span><span class="sxs-lookup"><span data-stu-id="8878a-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="8878a-184">[ `nuget trusted-signers` ](../reference/cli-reference/cli-ref-trusted-signers.md) [コマンドは`nuget setapikey` ](../reference/cli-reference/cli-ref-setapikey.md)、コマンドを使用`trustedSigners`して管理され、 `apikeys`コマンドを使用して管理される以外は、これらの設定を管理するために一般的に使用されます。 [ `nuget sources` ](../reference/cli-reference/cli-ref-sources.md)</span><span class="sxs-lookup"><span data-stu-id="8878a-184">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="8878a-185">ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。</span><span class="sxs-lookup"><span data-stu-id="8878a-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="8878a-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="8878a-186">packageSources</span></span>

<span data-ttu-id="8878a-187">すべての既知のパッケージ ソースの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="8878a-187">Lists all known package sources.</span></span> <span data-ttu-id="8878a-188">この順序は、復元操作中には無視され、PackageReference 形式を使用するプロジェクトでは無視されます。</span><span class="sxs-lookup"><span data-stu-id="8878a-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="8878a-189">NuGet は、を使用して`packages.config`、プロジェクトでのインストールおよび更新操作のソースの順序を尊重します。</span><span class="sxs-lookup"><span data-stu-id="8878a-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="8878a-190">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-190">Key</span></span> | <span data-ttu-id="8878a-191">値</span><span class="sxs-lookup"><span data-stu-id="8878a-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-192">(パッケージ ソースに割り当てる名前)</span><span class="sxs-lookup"><span data-stu-id="8878a-192">(name to assign to the package source)</span></span> | <span data-ttu-id="8878a-193">パッケージ ソースのパスまたは URL です。</span><span class="sxs-lookup"><span data-stu-id="8878a-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="8878a-194">**例**:</span><span class="sxs-lookup"><span data-stu-id="8878a-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="8878a-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="8878a-195">packageSourceCredentials</span></span>

<span data-ttu-id="8878a-196">通常、`-username` スイッチおよび `-password` スイッチと `nuget sources` によって指定される、ソースのユーザー名とパスワードを格納します。</span><span class="sxs-lookup"><span data-stu-id="8878a-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="8878a-197">`-storepasswordincleartext` オプションが使用されていない場合、既定ではパスワードが暗号化されます。</span><span class="sxs-lookup"><span data-stu-id="8878a-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="8878a-198">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-198">Key</span></span> | <span data-ttu-id="8878a-199">値</span><span class="sxs-lookup"><span data-stu-id="8878a-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-200">username</span><span class="sxs-lookup"><span data-stu-id="8878a-200">username</span></span> | <span data-ttu-id="8878a-201">プレーン テキストで表されるソースのユーザー名です。</span><span class="sxs-lookup"><span data-stu-id="8878a-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="8878a-202">password</span><span class="sxs-lookup"><span data-stu-id="8878a-202">password</span></span> | <span data-ttu-id="8878a-203">ソースの暗号されたパスワードです。</span><span class="sxs-lookup"><span data-stu-id="8878a-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="8878a-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="8878a-204">cleartextpassword</span></span> | <span data-ttu-id="8878a-205">ソースの暗号化されていないパスワードです。</span><span class="sxs-lookup"><span data-stu-id="8878a-205">The unencrypted password for the source.</span></span> |

<span data-ttu-id="8878a-206">**例:**</span><span class="sxs-lookup"><span data-stu-id="8878a-206">**Example:**</span></span>

<span data-ttu-id="8878a-207">構成ファイル内の `<packageSourceCredentials>` 要素には、適用可能なソース名ごとに子ノードが含まれます (名前内のスペースは `_x0020_` と置換されます)。</span><span class="sxs-lookup"><span data-stu-id="8878a-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="8878a-208">つまり、"Contoso" および "Test Source" という名前のソースの場合は、暗号化されたパスワードを使用するとき、構成ファイルには次の内容が含まれます。</span><span class="sxs-lookup"><span data-stu-id="8878a-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="8878a-209">暗号化されていないパスワードを使用する場合:</span><span class="sxs-lookup"><span data-stu-id="8878a-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="8878a-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="8878a-210">apikeys</span></span>

<span data-ttu-id="8878a-211">[`nuget setapikey` コマンド](../reference/cli-reference/cli-ref-setapikey.md)で設定される、API キー認証を使用するソースのキーを格納します。</span><span class="sxs-lookup"><span data-stu-id="8878a-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="8878a-212">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-212">Key</span></span> | <span data-ttu-id="8878a-213">値</span><span class="sxs-lookup"><span data-stu-id="8878a-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-214">(ソース URL)</span><span class="sxs-lookup"><span data-stu-id="8878a-214">(source URL)</span></span> | <span data-ttu-id="8878a-215">暗号化された API キー。</span><span class="sxs-lookup"><span data-stu-id="8878a-215">The encrypted API key.</span></span> |

<span data-ttu-id="8878a-216">**例**:</span><span class="sxs-lookup"><span data-stu-id="8878a-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="8878a-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="8878a-217">disabledPackageSources</span></span>

<span data-ttu-id="8878a-218">現在無効になっているソースを識別します。</span><span class="sxs-lookup"><span data-stu-id="8878a-218">Identified currently disabled sources.</span></span> <span data-ttu-id="8878a-219">空の場合もあります。</span><span class="sxs-lookup"><span data-stu-id="8878a-219">May be empty.</span></span>

| <span data-ttu-id="8878a-220">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-220">Key</span></span> | <span data-ttu-id="8878a-221">値</span><span class="sxs-lookup"><span data-stu-id="8878a-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-222">(ソースの名前)</span><span class="sxs-lookup"><span data-stu-id="8878a-222">(name of source)</span></span> | <span data-ttu-id="8878a-223">ソースが無効になっているかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="8878a-223">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="8878a-224">**例:**</span><span class="sxs-lookup"><span data-stu-id="8878a-224">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="8878a-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="8878a-225">activePackageSource</span></span>

<span data-ttu-id="8878a-226">*(2.x のみ。3.x 以降では非推奨とされます)*</span><span class="sxs-lookup"><span data-stu-id="8878a-226">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="8878a-227">現在アクティブなソースを識別し、すべてのソースの集計を示します。</span><span class="sxs-lookup"><span data-stu-id="8878a-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="8878a-228">キー</span><span class="sxs-lookup"><span data-stu-id="8878a-228">Key</span></span> | <span data-ttu-id="8878a-229">値</span><span class="sxs-lookup"><span data-stu-id="8878a-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="8878a-230">(ソースの名前) または `All`</span><span class="sxs-lookup"><span data-stu-id="8878a-230">(name of source) or `All`</span></span> | <span data-ttu-id="8878a-231">キーがソースの名前である場合は、ソースのパスまたは URL が値となります。</span><span class="sxs-lookup"><span data-stu-id="8878a-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="8878a-232">`All` の場合は、値を `(Aggregate source)` にして、無効になっていないすべてのパッケージ ソースを結合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8878a-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="8878a-233">**例**:</span><span class="sxs-lookup"><span data-stu-id="8878a-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="8878a-234">trustedSigners 者セクション</span><span class="sxs-lookup"><span data-stu-id="8878a-234">trustedSigners section</span></span>

<span data-ttu-id="8878a-235">インストールまたは復元中にパッケージを許可するために使用される信頼された署名者を格納します。</span><span class="sxs-lookup"><span data-stu-id="8878a-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="8878a-236">ユーザーがに設定`signatureValidationMode`した場合、この一覧を`require`空にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="8878a-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="8878a-237">このセクションは、 [ `nuget trusted-signers`コマンド](../reference/cli-reference/cli-ref-trusted-signers.md)を使用して更新できます。</span><span class="sxs-lookup"><span data-stu-id="8878a-237">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="8878a-238">**スキーマ**:</span><span class="sxs-lookup"><span data-stu-id="8878a-238">**Schema**:</span></span>

<span data-ttu-id="8878a-239">信頼できる署名者には、 `certificate`特定の署名者を識別するすべての証明書を登録する項目のコレクションがあります。</span><span class="sxs-lookup"><span data-stu-id="8878a-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="8878a-240">信頼できる署名者は、 `Author`またはの`Repository`いずれかです。</span><span class="sxs-lookup"><span data-stu-id="8878a-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="8878a-241">信頼された*リポジトリ*で`serviceIndex`は、リポジトリのを指定することもでき`https`ます (これは有効な uri である必要があります`owners` )。また、必要に応じて、をセミコロンで区切ったリストを指定して、その特定のによって信頼できるユーザーをさらに制限することもできます。・.</span><span class="sxs-lookup"><span data-stu-id="8878a-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="8878a-242">証明書のフィンガープリントに使用されるサポート`SHA256`さ`SHA384`れ`SHA512`ているハッシュアルゴリズムは、、およびです。</span><span class="sxs-lookup"><span data-stu-id="8878a-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="8878a-243">がを`allowUntrustedRoot` `true`指定した場合、指定された証明書は、署名の検証の一部として証明書チェーンを構築するときに、信頼されていないルートにチェーンできます。 `certificate`</span><span class="sxs-lookup"><span data-stu-id="8878a-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="8878a-244">**例**:</span><span class="sxs-lookup"><span data-stu-id="8878a-244">**Example**:</span></span>

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

## <a name="using-environment-variables"></a><span data-ttu-id="8878a-245">環境変数の使用</span><span class="sxs-lookup"><span data-stu-id="8878a-245">Using environment variables</span></span>

<span data-ttu-id="8878a-246">環境変数を `nuget.config` 値 (NuGet 3.4 以降) に使用することで、実行時に設定を適用できます。</span><span class="sxs-lookup"><span data-stu-id="8878a-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="8878a-247">たとえば、Windows 上の `HOME` 環境変数を `c:\users\username` に設定すると、構成ファイル内の `%HOME%\NuGetRepository` の値は `c:\users\username\NuGetRepository` に解決されます。</span><span class="sxs-lookup"><span data-stu-id="8878a-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="8878a-248">同様に、Mac/Linux 上の `HOME` を `/home/myStuff` に設定すると、構成ファイル内の `%HOME%/NuGetRepository` は `/home/myStuff/NuGetRepository` に解決されます。</span><span class="sxs-lookup"><span data-stu-id="8878a-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="8878a-249">環境変数が見つからない場合、NuGet は構成ファイルからのリテラル値を使用します。</span><span class="sxs-lookup"><span data-stu-id="8878a-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="8878a-250">構成ファイルの例</span><span class="sxs-lookup"><span data-stu-id="8878a-250">Example config file</span></span>

<span data-ttu-id="8878a-251">複数の設定が含まれている `nuget.config` ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="8878a-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
