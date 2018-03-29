---
title: NuGet.Config ファイル参照 | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/25/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: config、bindingRedirects、packageRestore、solution、packageSource の各セクションを含む NuGet.Config ファイル参照。
keywords: NuGet.Config ファイル、NuGet 構成参照、NuGet 構成オプション
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: e2a9d4f10ac6af4e5bc7386d4f78e18c2a5752c4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="nugetconfig-reference"></a><span data-ttu-id="4d090-104">NuGet.Config 参照</span><span class="sxs-lookup"><span data-stu-id="4d090-104">NuGet.Config reference</span></span>

<span data-ttu-id="4d090-105">NuGet の動作は、「[Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md)」(NuGet 動作の構成) に記載の各種 `NuGet.Config` ファイルでの設定によって制御されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-105">NuGet behavior is controlled by settings in different `NuGet.Config` files as described in [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="4d090-106">`NuGet.Config` は、最上位の `<configuration>` ノードを含む XML ファイルであり、このトピックで説明するセクション要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4d090-106">`NuGet.Config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="4d090-107">各セクションには、`key` 属性および `value` 属性を持つ 0 個以上の `<add>` 要素が含まれています。</span><span class="sxs-lookup"><span data-stu-id="4d090-107">Each section contains zero or more `<add>` elements with `key` and `value` attributes.</span></span> <span data-ttu-id="4d090-108">「[examples config file](#example-config-file)」 (構成ファイルの例) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4d090-108">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="4d090-109">名前の設定には大文字と小文字の区別があり、値には[環境変数](#using-environment-variables)を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="4d090-109">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<span data-ttu-id="4d090-110">このトピックの内容:</span><span class="sxs-lookup"><span data-stu-id="4d090-110">In this topic:</span></span>

- [<span data-ttu-id="4d090-111">config セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-111">config section</span></span>](#config-section)
- [<span data-ttu-id="4d090-112">bindingRedirects セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-112">bindingRedirects section</span></span>](#bindingredirects-section)
- [<span data-ttu-id="4d090-113">packageRestore セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-113">packageRestore section</span></span>](#packagerestore-section)
- [<span data-ttu-id="4d090-114">solution セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-114">solution section</span></span>](#solution-section)
- <span data-ttu-id="4d090-115">[パッケージ ソース セクション](#package-source-sections):</span><span class="sxs-lookup"><span data-stu-id="4d090-115">[Package source sections](#package-source-sections):</span></span>
  - [<span data-ttu-id="4d090-116">packageSources</span><span class="sxs-lookup"><span data-stu-id="4d090-116">packageSources</span></span>](#packagesources)
  - [<span data-ttu-id="4d090-117">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="4d090-117">packageSourceCredentials</span></span>](#packagesourcecredentials)
  - [<span data-ttu-id="4d090-118">apikeys</span><span class="sxs-lookup"><span data-stu-id="4d090-118">apikeys</span></span>](#apikeys)
  - [<span data-ttu-id="4d090-119">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="4d090-119">disabledPackageSources</span></span>](#disabledpackagesources)
  - [<span data-ttu-id="4d090-120">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="4d090-120">activePackageSource</span></span>](#activepackagesource)
- [<span data-ttu-id="4d090-121">環境変数の使用</span><span class="sxs-lookup"><span data-stu-id="4d090-121">Using environment variables</span></span>](#using-environment-variables)
- [<span data-ttu-id="4d090-122">構成ファイルの例</span><span class="sxs-lookup"><span data-stu-id="4d090-122">Example config file</span></span>](#example-config-file)

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="4d090-123">config セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-123">config section</span></span>

<span data-ttu-id="4d090-124">[`nuget config` コマンド](../tools/cli-ref-config.md)を使用して設定できる、さまざまな構成設定が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4d090-124">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../tools/cli-ref-config.md).</span></span>

<span data-ttu-id="4d090-125">`dependencyVersion` および`repositoryPath`を使用してプロジェクトにのみ適用`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="4d090-125">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="4d090-126">`globalPackagesFolder` PackageReference 形式を使用してプロジェクトにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-126">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="4d090-127">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-127">Key</span></span> | <span data-ttu-id="4d090-128">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-128">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-129">dependencyVersion (`packages.config` のみ)</span><span class="sxs-lookup"><span data-stu-id="4d090-129">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="4d090-130">`-DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `DependencyVersion` 値です。</span><span class="sxs-lookup"><span data-stu-id="4d090-130">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="4d090-131">この値は、NuGet パッケージ マネージャー UI でも使用されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-131">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="4d090-132">値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。</span><span class="sxs-lookup"><span data-stu-id="4d090-132">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="4d090-133">globalPackagesFolder (PackageReference をのみを使用してプロジェクト)</span><span class="sxs-lookup"><span data-stu-id="4d090-133">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="4d090-134">既定のグローバル パッケージ フォルダーの場所です。</span><span class="sxs-lookup"><span data-stu-id="4d090-134">The location of the default global packages folder.</span></span> <span data-ttu-id="4d090-135">既定値は、`%userprofile%\.nuget\packages` (Windows) または `~/.nuget/packages` (Mac/Linux) です。</span><span class="sxs-lookup"><span data-stu-id="4d090-135">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="4d090-136">相対パスは、プロジェクト固有の `Nuget.Config` ファイルで使用できます。</span><span class="sxs-lookup"><span data-stu-id="4d090-136">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="4d090-137">この設定は、優先 NUGET_PACKAGES 環境変数でオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="4d090-137">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="4d090-138">repositoryPath (`packages.config` のみ)</span><span class="sxs-lookup"><span data-stu-id="4d090-138">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="4d090-139">既定の `$(Solutiondir)/packages` フォルダーではなく、NuGet パッケージをインストールする場所です。</span><span class="sxs-lookup"><span data-stu-id="4d090-139">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="4d090-140">相対パスは、プロジェクト固有の `Nuget.Config` ファイルで使用できます。</span><span class="sxs-lookup"><span data-stu-id="4d090-140">A relative path can be used in project-specific `Nuget.Config` files.</span></span> <span data-ttu-id="4d090-141">この設定は、優先 NUGET_PACKAGES 環境変数でオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="4d090-141">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="4d090-142">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="4d090-142">defaultPushSource</span></span> | <span data-ttu-id="4d090-143">操作に対してパッケージ ソースが他に見つからない場合に、既定値として使用すべきパッケージ ソースの URL またはパスを識別します。</span><span class="sxs-lookup"><span data-stu-id="4d090-143">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="4d090-144">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="4d090-144">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="4d090-145">パッケージ ソースに接続するときに使用するプロキシ設定です。`http_proxy` の形式は `http://<username>:<password>@<domain>` とする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d090-145">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="4d090-146">パスワードは暗号化され、手動で追加することはできません。</span><span class="sxs-lookup"><span data-stu-id="4d090-146">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="4d090-147">`no_proxy` の場合、値はドメイン、バイパス、プロキシ サーバーのコンマ区切りのリストとなります。</span><span class="sxs-lookup"><span data-stu-id="4d090-147">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="4d090-148">これらの値に対して http_proxy および no_proxy の環境変数を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="4d090-148">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="4d090-149">詳細については、「[NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)」 (NuGet プロキシ設定) (skolima.blogspot.com) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="4d090-149">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |

<span data-ttu-id="4d090-150">**例**:</span><span class="sxs-lookup"><span data-stu-id="4d090-150">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="4d090-151">bindingRedirects セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-151">bindingRedirects section</span></span>

<span data-ttu-id="4d090-152">パッケージのインストール時に、NuGet で自動バインド リダイレクトを実行するかどうかを構成します。</span><span class="sxs-lookup"><span data-stu-id="4d090-152">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="4d090-153">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-153">Key</span></span> | <span data-ttu-id="4d090-154">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-154">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-155">スキップ</span><span class="sxs-lookup"><span data-stu-id="4d090-155">skip</span></span> | <span data-ttu-id="4d090-156">自動バインド リダイレクトを省略するかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="4d090-156">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="4d090-157">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="4d090-157">The default is false.</span></span> |

<span data-ttu-id="4d090-158">**例**:</span><span class="sxs-lookup"><span data-stu-id="4d090-158">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="4d090-159">packageRestore セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-159">packageRestore section</span></span>

<span data-ttu-id="4d090-160">ビルド時のパッケージの復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="4d090-160">Controls package restore during builds.</span></span>

| <span data-ttu-id="4d090-161">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-161">Key</span></span> | <span data-ttu-id="4d090-162">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-162">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-163">enabled</span><span class="sxs-lookup"><span data-stu-id="4d090-163">enabled</span></span> | <span data-ttu-id="4d090-164">NuGet で自動復元を実行できるかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="4d090-164">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="4d090-165">構成ファイル内にこのキーを設定するのでなく、`True` の値で `EnableNuGetPackageRestore` 環境変数を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="4d090-165">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="4d090-166">自動</span><span class="sxs-lookup"><span data-stu-id="4d090-166">automatic</span></span> | <span data-ttu-id="4d090-167">ビルド中に欠落しているパッケージの確認を NuGet で行う必要があるかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="4d090-167">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="4d090-168">**例**:</span><span class="sxs-lookup"><span data-stu-id="4d090-168">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="4d090-169">ソリューション セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-169">solution section</span></span>

<span data-ttu-id="4d090-170">ソリューションの `packages` フォルダーをソース管理に含めるかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="4d090-170">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="4d090-171">このセクションは、ソリューション フォルダー内の `Nuget.Config` ファイルでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="4d090-171">This section works only in `Nuget.Config` files in a solution folder.</span></span>

| <span data-ttu-id="4d090-172">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-172">Key</span></span> | <span data-ttu-id="4d090-173">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-173">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-174">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="4d090-174">disableSourceControlIntegration</span></span> | <span data-ttu-id="4d090-175">ソース管理を使用する場合に、パッケージ フォルダーを無視するかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="4d090-175">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="4d090-176">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="4d090-176">The default value is false.</span></span> |

<span data-ttu-id="4d090-177">**例**:</span><span class="sxs-lookup"><span data-stu-id="4d090-177">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="4d090-178">パッケージ ソース セクション</span><span class="sxs-lookup"><span data-stu-id="4d090-178">Package source sections</span></span>

<span data-ttu-id="4d090-179">`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource`、および `disabledPackageSources` のすべての連携によって、インストール、復元、および更新の操作中にパッケージ リポジトリを NuGet で操作する方法が構成されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-179">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, and `disabledPackageSources` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="4d090-180">これらの設定を管理するために、通常は、[`nuget sources` コマンド](../tools/cli-ref-sources.md)が使用されます。ただし、`apikeys` の場合は例外であり、[`nuget setapikey` コマンド](../tools/cli-ref-setapikey.md)によって管理されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-180">The [`nuget sources` command](../tools/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

<span data-ttu-id="4d090-181">ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。</span><span class="sxs-lookup"><span data-stu-id="4d090-181">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="4d090-182">packageSources</span><span class="sxs-lookup"><span data-stu-id="4d090-182">packageSources</span></span>

<span data-ttu-id="4d090-183">すべての既知のパッケージ ソースの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="4d090-183">Lists all known package sources.</span></span> <span data-ttu-id="4d090-184">復元操作中に、PackageReference 形式を使用して、プロジェクトを使用して、順序は無視されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-184">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="4d090-185">NuGet は、インストールのソースの順序を尊重いたします操作や更新操作を使用して、プロジェクトで`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="4d090-185">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="4d090-186">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-186">Key</span></span> | <span data-ttu-id="4d090-187">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-187">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-188">(パッケージ ソースに割り当てる名前)</span><span class="sxs-lookup"><span data-stu-id="4d090-188">(name to assign to the package source)</span></span> | <span data-ttu-id="4d090-189">パッケージ ソースのパスまたは URL です。</span><span class="sxs-lookup"><span data-stu-id="4d090-189">The path or URL of the package source.</span></span> |

<span data-ttu-id="4d090-190">**例**:</span><span class="sxs-lookup"><span data-stu-id="4d090-190">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="4d090-191">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="4d090-191">packageSourceCredentials</span></span>

<span data-ttu-id="4d090-192">通常、`-username` スイッチおよび `-password` スイッチと `nuget sources` によって指定される、ソースのユーザー名とパスワードを格納します。</span><span class="sxs-lookup"><span data-stu-id="4d090-192">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="4d090-193">`-storepasswordincleartext` オプションが使用されていない場合、既定ではパスワードが暗号化されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-193">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="4d090-194">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-194">Key</span></span> | <span data-ttu-id="4d090-195">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-195">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-196">username</span><span class="sxs-lookup"><span data-stu-id="4d090-196">username</span></span> | <span data-ttu-id="4d090-197">プレーン テキストで表されるソースのユーザー名です。</span><span class="sxs-lookup"><span data-stu-id="4d090-197">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="4d090-198">パスワード</span><span class="sxs-lookup"><span data-stu-id="4d090-198">password</span></span> | <span data-ttu-id="4d090-199">ソースの暗号されたパスワードです。</span><span class="sxs-lookup"><span data-stu-id="4d090-199">The encrypted password for the source.</span></span> |
| <span data-ttu-id="4d090-200">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="4d090-200">cleartextpassword</span></span> | <span data-ttu-id="4d090-201">ソースの暗号化されていないパスワードです。</span><span class="sxs-lookup"><span data-stu-id="4d090-201">The unencrypted password for the source.</span></span> |

<span data-ttu-id="4d090-202">**例:**</span><span class="sxs-lookup"><span data-stu-id="4d090-202">**Example:**</span></span>

<span data-ttu-id="4d090-203">構成ファイル内の `<packageSourceCredentials>` 要素には、適用可能なソース名ごとに子ノードが含まれます (名前内のスペースは `_x0020_` と置換されます)。</span><span class="sxs-lookup"><span data-stu-id="4d090-203">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="4d090-204">つまり、"Contoso" および "Test Source" という名前のソースの場合は、暗号化されたパスワードを使用するとき、構成ファイルには次の内容が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4d090-204">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="4d090-205">暗号化されていないパスワードを使用する場合:</span><span class="sxs-lookup"><span data-stu-id="4d090-205">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="4d090-206">apikeys</span><span class="sxs-lookup"><span data-stu-id="4d090-206">apikeys</span></span>

<span data-ttu-id="4d090-207">[`nuget setapikey` コマンド](../tools/cli-ref-setapikey.md)で設定される、API キー認証を使用するソースのキーを格納します。</span><span class="sxs-lookup"><span data-stu-id="4d090-207">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../tools/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="4d090-208">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-208">Key</span></span> | <span data-ttu-id="4d090-209">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-209">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-210">(ソース URL)</span><span class="sxs-lookup"><span data-stu-id="4d090-210">(source URL)</span></span> | <span data-ttu-id="4d090-211">暗号化された API キー。</span><span class="sxs-lookup"><span data-stu-id="4d090-211">The encrypted API key.</span></span> |

<span data-ttu-id="4d090-212">**例**:</span><span class="sxs-lookup"><span data-stu-id="4d090-212">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="4d090-213">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="4d090-213">disabledPackageSources</span></span>

<span data-ttu-id="4d090-214">現在無効になっているソースを識別します。</span><span class="sxs-lookup"><span data-stu-id="4d090-214">Identified currently disabled sources.</span></span> <span data-ttu-id="4d090-215">空の場合もあります。</span><span class="sxs-lookup"><span data-stu-id="4d090-215">May be empty.</span></span>

| <span data-ttu-id="4d090-216">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-216">Key</span></span> | <span data-ttu-id="4d090-217">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-217">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-218">(ソースの名前)</span><span class="sxs-lookup"><span data-stu-id="4d090-218">(name of source)</span></span> | <span data-ttu-id="4d090-219">ソースが無効になっているかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="4d090-219">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="4d090-220">**例:**</span><span class="sxs-lookup"><span data-stu-id="4d090-220">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="4d090-221">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="4d090-221">activePackageSource</span></span>

<span data-ttu-id="4d090-222">*(2.x のみ。3.x 以降では使用されていない)*</span><span class="sxs-lookup"><span data-stu-id="4d090-222">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="4d090-223">現在アクティブなソースを識別し、すべてのソースの集計を示します。</span><span class="sxs-lookup"><span data-stu-id="4d090-223">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="4d090-224">キー</span><span class="sxs-lookup"><span data-stu-id="4d090-224">Key</span></span> | <span data-ttu-id="4d090-225">[値]</span><span class="sxs-lookup"><span data-stu-id="4d090-225">Value</span></span> |
| --- | --- |
| <span data-ttu-id="4d090-226">(ソースの名前) または `All`</span><span class="sxs-lookup"><span data-stu-id="4d090-226">(name of source) or `All`</span></span> | <span data-ttu-id="4d090-227">キーがソースの名前である場合は、ソースのパスまたは URL が値となります。</span><span class="sxs-lookup"><span data-stu-id="4d090-227">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="4d090-228">`All` の場合は、値を `(Aggregate source)` にして、無効になっていないすべてのパッケージ ソースを結合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4d090-228">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="4d090-229">**例**:</span><span class="sxs-lookup"><span data-stu-id="4d090-229">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="using-environment-variables"></a><span data-ttu-id="4d090-230">環境変数の使用</span><span class="sxs-lookup"><span data-stu-id="4d090-230">Using environment variables</span></span>

<span data-ttu-id="4d090-231">環境変数を `NuGet.Config` 値 (NuGet 3.4 以降) に使用することで、実行時に設定を適用できます。</span><span class="sxs-lookup"><span data-stu-id="4d090-231">You can use environment variables in `NuGet.Config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="4d090-232">たとえば、Windows 上の `HOME` 環境変数を `c:\users\username` に設定すると、構成ファイル内の `%HOME%\NuGetRepository` の値は `c:\users\username\NuGetRepository` に解決されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-232">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="4d090-233">同様に、Mac/Linux 上の `HOME` を `/home/myStuff` に設定すると、構成ファイル内の `$HOME/NuGetRepository` は `/home/myStuff/NuGetRepository` に解決されます。</span><span class="sxs-lookup"><span data-stu-id="4d090-233">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `$HOME/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="4d090-234">環境変数が見つからない場合、NuGet は構成ファイルからのリテラル値を使用します。</span><span class="sxs-lookup"><span data-stu-id="4d090-234">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="4d090-235">構成ファイルの例</span><span class="sxs-lookup"><span data-stu-id="4d090-235">Example config file</span></span>

<span data-ttu-id="4d090-236">複数の設定が含まれている `NuGet.Config` ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="4d090-236">Below is an example `NuGet.Config` file that illustrates a number of settings:</span></span>

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
