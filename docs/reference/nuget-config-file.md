---
title: nuget.config ファイル参照
description: config、bindingRedirects、packageRestore、solution、packageSource の各セクションを含む NuGet.Config ファイル参照。
author: karann-msft
ms.author: karann
ms.date: 10/25/2017
ms.topic: reference
ms.openlocfilehash: d7c943c1f13edf782dabe4afee9d19a1a42bd42a
ms.sourcegitcommit: 9f94e00428d83aef4a7a87db679129eff7720c59
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/03/2019
ms.locfileid: "58911089"
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="520c9-103">nuget.config reference</span><span class="sxs-lookup"><span data-stu-id="520c9-103">nuget.config reference</span></span>

<span data-ttu-id="520c9-104">NuGet の動作は、「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md)」(NuGet 動作の構成) に記載の各種 `NuGet.Config` ファイルでの設定によって制御されます。</span><span class="sxs-lookup"><span data-stu-id="520c9-104">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

`nuget.config` <span data-ttu-id="520c9-105">最上位を含む XML ファイルは、`<configuration>`ノードで、このトピックで説明するセクションの要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="520c9-105">is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="520c9-106">各セクションには、0 個以上の項目が含まれています。</span><span class="sxs-lookup"><span data-stu-id="520c9-106">Each section contains zero or more items.</span></span> <span data-ttu-id="520c9-107">「[examples config file](#example-config-file)」 (構成ファイルの例) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="520c9-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="520c9-108">名前の設定には大文字と小文字の区別があり、値には[環境変数](#using-environment-variables)を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="520c9-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="520c9-109">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="520c9-109">In this topic:</span></span>

- [<span data-ttu-id="520c9-110">config セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-110">config section</span></span>](#config-section)
- [<span data-ttu-id="520c9-111">bindingRedirects セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-111">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="520c9-112">packageRestore セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-112">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="520c9-113">ソリューション セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-113">solution section</span></span>](#solution-section)
- <span data-ttu-id="520c9-114">[パッケージ ソース セクション](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="520c9-114">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="520c9-115">packageSources</span><span class="sxs-lookup"><span data-stu-id="520c9-115">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="520c9-116">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="520c9-116">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="520c9-117">apikeys</span><span class="sxs-lookup"><span data-stu-id="520c9-117">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="520c9-118">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="520c9-118">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="520c9-119">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="520c9-119">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="520c9-120">trustedSigners セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-120">trustedSigners section</span></span>](#trustedsigners-section)
- [<span data-ttu-id="520c9-121">環境変数の使用</span><span class="sxs-lookup"><span data-stu-id="520c9-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="520c9-122">構成ファイルの例</span><span class="sxs-lookup"><span data-stu-id="520c9-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="520c9-123">config セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-123">config section</span></span>

<span data-ttu-id="520c9-124">[`nuget config` コマンド](../tools/cli-ref-config.md)を使用して設定できる、さまざまな構成設定が含まれます。</span><span class="sxs-lookup"><span data-stu-id="520c9-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

`dependencyVersion` <span data-ttu-id="520c9-125">`repositoryPath`を使用してプロジェクトにのみ適用`packages.config`します。</span><span class="sxs-lookup"><span data-stu-id="520c9-125">and `repositoryPath` apply only to projects using `packages.config`.</span></span> `globalPackagesFolder` <span data-ttu-id="520c9-126">PackageReference 形式を使用してプロジェクトにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="520c9-126">applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="520c9-127">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-127">Key</span></span> | <span data-ttu-id="520c9-128">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-129">dependencyVersion (`packages.config` のみ)</span><span class="sxs-lookup"><span data-stu-id="520c9-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="520c9-130">`-DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `DependencyVersion` 値です。</span><span class="sxs-lookup"><span data-stu-id="520c9-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="520c9-131">この値は、NuGet パッケージ マネージャー UI でも使用されます。</span><span class="sxs-lookup"><span data-stu-id="520c9-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="520c9-132">値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。</span><span class="sxs-lookup"><span data-stu-id="520c9-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="520c9-133">globalPackagesFolder (プロジェクトは PackageReference をのみを使用して)</span><span class="sxs-lookup"><span data-stu-id="520c9-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="520c9-134">既定のグローバル パッケージ フォルダーの場所です。</span><span class="sxs-lookup"><span data-stu-id="520c9-134">The location of the default global packages folder.</span></span> <span data-ttu-id="520c9-135">既定値は、`%userprofile%\.nuget\packages` (Windows) または `~/.nuget/packages` (Mac/Linux) です。</span><span class="sxs-lookup"><span data-stu-id="520c9-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="520c9-136">相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。</span><span class="sxs-lookup"><span data-stu-id="520c9-136">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="520c9-137">この設定は、優先 NUGET_PACKAGES 環境変数によってオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="520c9-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="520c9-138">repositoryPath (`packages.config` のみ)</span><span class="sxs-lookup"><span data-stu-id="520c9-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="520c9-139">既定の `$(Solutiondir)/packages` フォルダーではなく、NuGet パッケージをインストールする場所です。</span><span class="sxs-lookup"><span data-stu-id="520c9-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="520c9-140">相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。</span><span class="sxs-lookup"><span data-stu-id="520c9-140">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="520c9-141">この設定は、優先 NUGET_PACKAGES 環境変数によってオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="520c9-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="520c9-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="520c9-142">defaultPushSource</span></span> | <span data-ttu-id="520c9-143">操作に対してパッケージ ソースが他に見つからない場合に、既定値として使用すべきパッケージ ソースの URL またはパスを識別します。</span><span class="sxs-lookup"><span data-stu-id="520c9-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="520c9-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="520c9-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="520c9-145">パッケージ ソースに接続するときに使用するプロキシ設定です。`http_proxy` の形式は `http://<username>:<password>@<domain>` とする必要があります。</span><span class="sxs-lookup"><span data-stu-id="520c9-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="520c9-146">パスワードは暗号化され、手動で追加することはできません。</span><span class="sxs-lookup"><span data-stu-id="520c9-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="520c9-147">`no_proxy` の場合、値はドメイン、バイパス、プロキシ サーバーのコンマ区切りのリストとなります。</span><span class="sxs-lookup"><span data-stu-id="520c9-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="520c9-148">これらの値に対して http_proxy および no_proxy の環境変数を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="520c9-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="520c9-149">詳細については、「[NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)」 (NuGet プロキシ設定) (skolima.blogspot.com) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="520c9-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="520c9-150">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="520c9-150">signatureValidationMode</span></span> | <span data-ttu-id="520c9-151">パッケージのインストール パッケージの署名を確認し、復元に使用される検証モードを指定します。</span><span class="sxs-lookup"><span data-stu-id="520c9-151">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="520c9-152">値は`accept`、`require`します。</span><span class="sxs-lookup"><span data-stu-id="520c9-152">Values are `accept`, `require`.</span></span> <span data-ttu-id="520c9-153">既定値は `accept` です。</span><span class="sxs-lookup"><span data-stu-id="520c9-153">Defaults to `accept`.</span></span>

<span data-ttu-id="520c9-154">**例**:</span><span class="sxs-lookup"><span data-stu-id="520c9-154">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="520c9-155">bindingRedirects セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-155">bindingRedirects section</span></span>

<span data-ttu-id="520c9-156">パッケージのインストール時に、NuGet で自動バインド リダイレクトを実行するかどうかを構成します。</span><span class="sxs-lookup"><span data-stu-id="520c9-156">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="520c9-157">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-157">Key</span></span> | <span data-ttu-id="520c9-158">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-158">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-159">スキップ</span><span class="sxs-lookup"><span data-stu-id="520c9-159">skip</span></span> | <span data-ttu-id="520c9-160">自動バインド リダイレクトを省略するかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="520c9-160">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="520c9-161">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="520c9-161">The default is false.</span></span> |

<span data-ttu-id="520c9-162">**例**:</span><span class="sxs-lookup"><span data-stu-id="520c9-162">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="520c9-163">packageRestore セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-163">packageRestore section</span></span>

<span data-ttu-id="520c9-164">ビルド時のパッケージの復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="520c9-164">Controls package restore during builds.</span></span>

| <span data-ttu-id="520c9-165">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-165">Key</span></span> | <span data-ttu-id="520c9-166">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-166">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-167">enabled</span><span class="sxs-lookup"><span data-stu-id="520c9-167">enabled</span></span> | <span data-ttu-id="520c9-168">NuGet で自動復元を実行できるかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="520c9-168">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="520c9-169">構成ファイル内にこのキーを設定するのでなく、`True` の値で `EnableNuGetPackageRestore` 環境変数を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="520c9-169">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="520c9-170">自動</span><span class="sxs-lookup"><span data-stu-id="520c9-170">automatic</span></span> | <span data-ttu-id="520c9-171">ビルド中に欠落しているパッケージの確認を NuGet で行う必要があるかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="520c9-171">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="520c9-172">**例**:</span><span class="sxs-lookup"><span data-stu-id="520c9-172">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="520c9-173">ソリューション セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-173">solution section</span></span>

<span data-ttu-id="520c9-174">ソリューションの `packages` フォルダーをソース管理に含めるかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="520c9-174">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="520c9-175">このセクションは、ソリューション フォルダー内の `nuget.config` ファイルでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="520c9-175">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="520c9-176">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-176">Key</span></span> | <span data-ttu-id="520c9-177">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-178">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="520c9-178">disableSourceControlIntegration</span></span> | <span data-ttu-id="520c9-179">ソース管理を使用する場合に、パッケージ フォルダーを無視するかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="520c9-179">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="520c9-180">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="520c9-180">The default value is false.</span></span> |

<span data-ttu-id="520c9-181">**例**:</span><span class="sxs-lookup"><span data-stu-id="520c9-181">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="520c9-182">パッケージ ソース セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-182">Package source sections</span></span>

<span data-ttu-id="520c9-183">`packageSources`、 `packageSourceCredentials`、 `apikeys`、 `activePackageSource`、`disabledPackageSources`と`trustedSigners`パッケージ リポジトリとインストール、復元、および更新操作中に NuGet の動作を構成するすべての作業です。</span><span class="sxs-lookup"><span data-stu-id="520c9-183">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="520c9-184">[ `nuget sources`コマンド](../tools/cli-ref-sources.md)を除き、これらの設定を管理するために使用が一般的に`apikeys`を使用して管理される、 [ `nuget setapikey`コマンド](../tools/cli-ref-setapikey.md)、および`trustedSigners`管理されます。使用して、 [ `nuget trusted-signers`コマンド](../tools/cli-ref-trusted-signers.md)します。</span><span class="sxs-lookup"><span data-stu-id="520c9-184">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="520c9-185">ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。</span><span class="sxs-lookup"><span data-stu-id="520c9-185">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="520c9-186">packageSources</span><span class="sxs-lookup"><span data-stu-id="520c9-186">packageSources</span></span>

<span data-ttu-id="520c9-187">すべての既知のパッケージ ソースの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="520c9-187">Lists all known package sources.</span></span> <span data-ttu-id="520c9-188">PackageReference 形式を使用して任意のプロジェクトと復元操作中に、順序は無視されます。</span><span class="sxs-lookup"><span data-stu-id="520c9-188">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="520c9-189">NuGet のインストール ソースの順序を尊重する操作や更新操作を使用するプロジェクトで`packages.config`します。</span><span class="sxs-lookup"><span data-stu-id="520c9-189">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="520c9-190">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-190">Key</span></span> | <span data-ttu-id="520c9-191">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-191">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-192">(パッケージ ソースに割り当てる名前)</span><span class="sxs-lookup"><span data-stu-id="520c9-192">(name to assign to the package source)</span></span> | <span data-ttu-id="520c9-193">パッケージ ソースのパスまたは URL です。</span><span class="sxs-lookup"><span data-stu-id="520c9-193">The path or URL of the package source.</span></span> |

<span data-ttu-id="520c9-194">**例**:</span><span class="sxs-lookup"><span data-stu-id="520c9-194">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="520c9-195">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="520c9-195">packageSourceCredentials</span></span>

<span data-ttu-id="520c9-196">通常、`-username` スイッチおよび `-password` スイッチと `nuget sources` によって指定される、ソースのユーザー名とパスワードを格納します。</span><span class="sxs-lookup"><span data-stu-id="520c9-196">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="520c9-197">`-storepasswordincleartext` オプションが使用されていない場合、既定ではパスワードが暗号化されます。</span><span class="sxs-lookup"><span data-stu-id="520c9-197">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="520c9-198">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-198">Key</span></span> | <span data-ttu-id="520c9-199">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-200">username</span><span class="sxs-lookup"><span data-stu-id="520c9-200">username</span></span> | <span data-ttu-id="520c9-201">プレーン テキストで表されるソースのユーザー名です。</span><span class="sxs-lookup"><span data-stu-id="520c9-201">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="520c9-202">パスワード</span><span class="sxs-lookup"><span data-stu-id="520c9-202">password</span></span> | <span data-ttu-id="520c9-203">ソースの暗号されたパスワードです。</span><span class="sxs-lookup"><span data-stu-id="520c9-203">The encrypted password for the source.</span></span> |
| <span data-ttu-id="520c9-204">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="520c9-204">cleartextpassword</span></span> | <span data-ttu-id="520c9-205">ソースの暗号化されていないパスワードです。</span><span class="sxs-lookup"><span data-stu-id="520c9-205">The unencrypted password for the source.</span></span> |

**<span data-ttu-id="520c9-206">例:</span><span class="sxs-lookup"><span data-stu-id="520c9-206">Example:</span></span>**

<span data-ttu-id="520c9-207">構成ファイル内の `<packageSourceCredentials>` 要素には、適用可能なソース名ごとに子ノードが含まれます (名前内のスペースは `_x0020_` と置換されます)。</span><span class="sxs-lookup"><span data-stu-id="520c9-207">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="520c9-208">つまり、"Contoso" および "Test Source" という名前のソースの場合は、暗号化されたパスワードを使用するとき、構成ファイルには次の内容が含まれます。</span><span class="sxs-lookup"><span data-stu-id="520c9-208">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="520c9-209">暗号化されていないパスワードを使用する場合:</span><span class="sxs-lookup"><span data-stu-id="520c9-209">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="520c9-210">apikeys</span><span class="sxs-lookup"><span data-stu-id="520c9-210">apikeys</span></span>

<span data-ttu-id="520c9-211">[`nuget setapikey` コマンド](../tools/cli-ref-setapikey.md)で設定される、API キー認証を使用するソースのキーを格納します。</span><span class="sxs-lookup"><span data-stu-id="520c9-211">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="520c9-212">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-212">Key</span></span> | <span data-ttu-id="520c9-213">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-213">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-214">(ソース URL)</span><span class="sxs-lookup"><span data-stu-id="520c9-214">(source URL)</span></span> | <span data-ttu-id="520c9-215">暗号化された API キー。</span><span class="sxs-lookup"><span data-stu-id="520c9-215">The encrypted API key.</span></span> |

<span data-ttu-id="520c9-216">**例**:</span><span class="sxs-lookup"><span data-stu-id="520c9-216">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="520c9-217">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="520c9-217">disabledPackageSources</span></span>

<span data-ttu-id="520c9-218">現在無効になっているソースを識別します。</span><span class="sxs-lookup"><span data-stu-id="520c9-218">Identified currently disabled sources.</span></span> <span data-ttu-id="520c9-219">空の場合もあります。</span><span class="sxs-lookup"><span data-stu-id="520c9-219">May be empty.</span></span>

| <span data-ttu-id="520c9-220">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-220">Key</span></span> | <span data-ttu-id="520c9-221">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-221">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-222">(ソースの名前)</span><span class="sxs-lookup"><span data-stu-id="520c9-222">(name of source)</span></span> | <span data-ttu-id="520c9-223">ソースが無効になっているかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="520c9-223">A Boolean indicating whether the source is disabled.</span></span> |

**<span data-ttu-id="520c9-224">例:</span><span class="sxs-lookup"><span data-stu-id="520c9-224">Example:</span></span>**

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="520c9-225">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="520c9-225">activePackageSource</span></span>

*<span data-ttu-id="520c9-226">(2.x のみ。 3.x 以降のでは非推奨)</span><span class="sxs-lookup"><span data-stu-id="520c9-226">(2.x only; deprecated in 3.x+)</span></span>*

<span data-ttu-id="520c9-227">現在アクティブなソースを識別し、すべてのソースの集計を示します。</span><span class="sxs-lookup"><span data-stu-id="520c9-227">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="520c9-228">キー</span><span class="sxs-lookup"><span data-stu-id="520c9-228">Key</span></span> | <span data-ttu-id="520c9-229">[値]</span><span class="sxs-lookup"><span data-stu-id="520c9-229">Value</span></span> |
| --- | --- |
| <span data-ttu-id="520c9-230">(ソースの名前) または</span><span class="sxs-lookup"><span data-stu-id="520c9-230">(name of source) or</span></span> `All` | <span data-ttu-id="520c9-231">キーがソースの名前である場合は、ソースのパスまたは URL が値となります。</span><span class="sxs-lookup"><span data-stu-id="520c9-231">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="520c9-232">`All` の場合は、値を `(Aggregate source)` にして、無効になっていないすべてのパッケージ ソースを結合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="520c9-232">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="520c9-233">**例**:</span><span class="sxs-lookup"><span data-stu-id="520c9-233">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```
## <a name="trustedsigners-section"></a><span data-ttu-id="520c9-234">trustedSigners セクション</span><span class="sxs-lookup"><span data-stu-id="520c9-234">trustedSigners section</span></span>

<span data-ttu-id="520c9-235">ストアには、パッケージをインストールまたは復元中に許可するために使用する署名者が信頼されています。</span><span class="sxs-lookup"><span data-stu-id="520c9-235">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="520c9-236">ユーザーを設定するとこの一覧を空にすることはできません`signatureValidationMode`に`require`します。</span><span class="sxs-lookup"><span data-stu-id="520c9-236">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="520c9-237">このセクションを更新するためには、 [ `nuget trusted-signers`コマンド](../tools/cli-ref-trusted-signers.md)します。</span><span class="sxs-lookup"><span data-stu-id="520c9-237">This section can be updated with the [`nuget trusted-signers` command](../tools/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="520c9-238">**スキーマ**:</span><span class="sxs-lookup"><span data-stu-id="520c9-238">**Schema**:</span></span>

<span data-ttu-id="520c9-239">信頼できる署名者のコレクションがある`certificate`項目を指定した署名者を識別するすべての証明書を登録します。</span><span class="sxs-lookup"><span data-stu-id="520c9-239">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="520c9-240">信頼できる署名者には、いずれかを指定できる、`Author`または`Repository`します。</span><span class="sxs-lookup"><span data-stu-id="520c9-240">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="520c9-241">信頼された*リポジトリ*も指定します、`serviceIndex`リポジトリの (は有効なある`https`uri) のセミコロンで区切られたリストを必要に応じて指定できますと`owners`者が信頼されているさらを制限するにはその特定のリポジトリ。</span><span class="sxs-lookup"><span data-stu-id="520c9-241">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="520c9-242">証明書フィンガー プリントを使用するサポートされているハッシュ アルゴリズム`SHA256`、`SHA384`と`SHA512`します。</span><span class="sxs-lookup"><span data-stu-id="520c9-242">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="520c9-243">場合、`certificate`指定`allowUntrustedRoot`として`true`特定の証明書が信頼されていないルートにチェーン署名の検証の一部として証明書チェーンの構築中に許可されました。</span><span class="sxs-lookup"><span data-stu-id="520c9-243">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="520c9-244">**例**:</span><span class="sxs-lookup"><span data-stu-id="520c9-244">**Example**:</span></span>

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

## <a name="using-environment-variables"></a><span data-ttu-id="520c9-245">環境変数の使用</span><span class="sxs-lookup"><span data-stu-id="520c9-245">Using environment variables</span></span>

<span data-ttu-id="520c9-246">環境変数を `nuget.config` 値 (NuGet 3.4 以降) に使用することで、実行時に設定を適用できます。</span><span class="sxs-lookup"><span data-stu-id="520c9-246">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="520c9-247">たとえば、Windows 上の `HOME` 環境変数を `c:\users\username` に設定すると、構成ファイル内の `%HOME%\NuGetRepository` の値は `c:\users\username\NuGetRepository` に解決されます。</span><span class="sxs-lookup"><span data-stu-id="520c9-247">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="520c9-248">同様に、Mac/Linux 上の `HOME` を `/home/myStuff` に設定すると、構成ファイル内の `%HOME%/NuGetRepository` は `/home/myStuff/NuGetRepository` に解決されます。</span><span class="sxs-lookup"><span data-stu-id="520c9-248">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="520c9-249">環境変数が見つからない場合、NuGet は構成ファイルからのリテラル値を使用します。</span><span class="sxs-lookup"><span data-stu-id="520c9-249">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="520c9-250">構成ファイルの例</span><span class="sxs-lookup"><span data-stu-id="520c9-250">Example config file</span></span>

<span data-ttu-id="520c9-251">複数の設定が含まれている `nuget.config` ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="520c9-251">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
