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
# <a name="nugetconfig-reference"></a><span data-ttu-id="a0b8c-103">nuget の .config リファレンス</span><span class="sxs-lookup"><span data-stu-id="a0b8c-103">nuget.config reference</span></span>

<span data-ttu-id="a0b8c-104">NuGet の動作は、[一般的な nuget 構成](../consume-packages/configuring-nuget-behavior.md)で説明されているように、さまざまな `NuGet.Config` または `nuget.config` ファイルの設定によって制御されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-104">NuGet behavior is controlled by settings in different `NuGet.Config` or `nuget.config` files as described in [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="a0b8c-105">`nuget.config` は、最上位の `<configuration>` ノードを含む XML ファイルであり、このトピックで説明するセクション要素が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-105">`nuget.config` is an XML file containing a top-level `<configuration>` node, which then contains the section elements described in this topic.</span></span> <span data-ttu-id="a0b8c-106">各セクションには、0個以上の項目が含まれています。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-106">Each section contains zero or more items.</span></span> <span data-ttu-id="a0b8c-107">「[examples config file](#example-config-file)」 (構成ファイルの例) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-107">See the [examples config file](#example-config-file).</span></span> <span data-ttu-id="a0b8c-108">名前の設定には大文字と小文字の区別があり、値には[環境変数](#using-environment-variables)を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-108">Setting names are case-insensitive, and values can use [environment variables](#using-environment-variables).</span></span>

<a name="dependencyVersion"></a>
<a name="globalPackagesFolder"></a>
<a name="repositoryPath"></a>
<a name="proxy-settings"></a>

## <a name="config-section"></a><span data-ttu-id="a0b8c-109">config セクション</span><span class="sxs-lookup"><span data-stu-id="a0b8c-109">config section</span></span>

<span data-ttu-id="a0b8c-110">[`nuget config` コマンド](../reference/cli-reference/cli-ref-config.md)を使用して設定できる、さまざまな構成設定が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-110">Contains miscellaneous configuration settings, which can be set using the [`nuget config` command](../reference/cli-reference/cli-ref-config.md).</span></span>

<span data-ttu-id="a0b8c-111">`dependencyVersion` と `repositoryPath` は `packages.config`を使用するプロジェクトにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-111">`dependencyVersion` and `repositoryPath` apply only to projects using `packages.config`.</span></span> <span data-ttu-id="a0b8c-112">`globalPackagesFolder` は、PackageReference 形式を使用するプロジェクトにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-112">`globalPackagesFolder` applies only to projects using the PackageReference format.</span></span>

| <span data-ttu-id="a0b8c-113">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-113">Key</span></span> | <span data-ttu-id="a0b8c-114">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-114">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-115">dependencyVersion (`packages.config` のみ)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-115">dependencyVersion (`packages.config` only)</span></span> | <span data-ttu-id="a0b8c-116">`-DependencyVersion` スイッチが直接指定されない場合の、パッケージのインストール、復元、および更新における既定の `DependencyVersion` 値です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-116">The default `DependencyVersion` value for package install, restore, and update, when the `-DependencyVersion` switch is not specified directly.</span></span> <span data-ttu-id="a0b8c-117">この値は、NuGet パッケージ マネージャー UI でも使用されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-117">This value is also used by the NuGet Package Manager UI.</span></span> <span data-ttu-id="a0b8c-118">値は `Lowest`、`HighestPatch`、`HighestMinor`、`Highest` となります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-118">Values are `Lowest`, `HighestPatch`, `HighestMinor`, `Highest`.</span></span> |
| <span data-ttu-id="a0b8c-119">Globalパッケージフォルダー (PackageReference のみを使用するプロジェクト)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-119">globalPackagesFolder (projects using PackageReference only)</span></span> | <span data-ttu-id="a0b8c-120">既定のグローバル パッケージ フォルダーの場所です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-120">The location of the default global packages folder.</span></span> <span data-ttu-id="a0b8c-121">既定値は、`%userprofile%\.nuget\packages` (Windows) または `~/.nuget/packages` (Mac/Linux) です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-121">The default is `%userprofile%\.nuget\packages` (Windows) or `~/.nuget/packages` (Mac/Linux).</span></span> <span data-ttu-id="a0b8c-122">相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-122">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="a0b8c-123">この設定は、NUGET_PACKAGES 環境変数によってオーバーライドされます。これは、優先されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-123">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="a0b8c-124">repositoryPath (`packages.config` のみ)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-124">repositoryPath (`packages.config` only)</span></span> | <span data-ttu-id="a0b8c-125">既定の `$(Solutiondir)/packages` フォルダーではなく、NuGet パッケージをインストールする場所です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-125">The location in which to install NuGet packages instead of the default `$(Solutiondir)/packages` folder.</span></span> <span data-ttu-id="a0b8c-126">相対パスは、プロジェクト固有の `nuget.config` ファイルで使用できます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-126">A relative path can be used in project-specific `nuget.config` files.</span></span> <span data-ttu-id="a0b8c-127">この設定は、NUGET_PACKAGES 環境変数によってオーバーライドされます。これは、優先されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-127">This setting is overridden by the NUGET_PACKAGES environment variable, which takes precedence.</span></span> |
| <span data-ttu-id="a0b8c-128">defaultPushSource</span><span class="sxs-lookup"><span data-stu-id="a0b8c-128">defaultPushSource</span></span> | <span data-ttu-id="a0b8c-129">操作に対してパッケージ ソースが他に見つからない場合に、既定値として使用すべきパッケージ ソースの URL またはパスを識別します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-129">Identifies the URL or path of the package source that should be used as the default if no other package sources are found for an operation.</span></span> |
| <span data-ttu-id="a0b8c-130">http_proxy http_proxy.user http_proxy.password no_proxy</span><span class="sxs-lookup"><span data-stu-id="a0b8c-130">http_proxy http_proxy.user http_proxy.password no_proxy</span></span> | <span data-ttu-id="a0b8c-131">パッケージ ソースに接続するときに使用するプロキシ設定です。`http_proxy` の形式は `http://<username>:<password>@<domain>` とする必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-131">Proxy settings to use when connecting to package sources; `http_proxy` should be in the format `http://<username>:<password>@<domain>`.</span></span> <span data-ttu-id="a0b8c-132">パスワードは暗号化され、手動で追加することはできません。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-132">Passwords are encrypted and cannot be added manually.</span></span> <span data-ttu-id="a0b8c-133">`no_proxy` の場合、値はドメイン、バイパス、プロキシ サーバーのコンマ区切りのリストとなります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-133">For `no_proxy`, the value is a comma-separated list of domains the bypass the proxy server.</span></span> <span data-ttu-id="a0b8c-134">これらの値に対して http_proxy および no_proxy の環境変数を使用することもできます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-134">You can alternately use the http_proxy and no_proxy environment variables for those values.</span></span> <span data-ttu-id="a0b8c-135">詳細については、「[NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html)」 (NuGet プロキシ設定) (skolima.blogspot.com) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-135">For additional details, see [NuGet proxy settings](http://skolima.blogspot.com/2012/07/nuget-proxy-settings.html) (skolima.blogspot.com).</span></span> |
| <span data-ttu-id="a0b8c-136">signatureValidationMode</span><span class="sxs-lookup"><span data-stu-id="a0b8c-136">signatureValidationMode</span></span> | <span data-ttu-id="a0b8c-137">パッケージのインストールおよび復元用のパッケージ署名の検証に使用する検証モードを指定します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-137">Specifies the validation mode used to verify package signatures for package install, and restore.</span></span> <span data-ttu-id="a0b8c-138">値は `accept`、`require`です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-138">Values are `accept`, `require`.</span></span> <span data-ttu-id="a0b8c-139">既定値は `accept` です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-139">Defaults to `accept`.</span></span>

<span data-ttu-id="a0b8c-140">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-140">**Example**:</span></span>

```xml
<config>
    <add key="dependencyVersion" value="Highest" />
    <add key="globalPackagesFolder" value="c:\packages" />
    <add key="repositoryPath" value="c:\installed_packages" />
    <add key="http_proxy" value="http://company-squid:3128@contoso.com" />
    <add key="signatureValidationMode" value="require" />
</config>
```

## <a name="bindingredirects-section"></a><span data-ttu-id="a0b8c-141">bindingRedirects セクション</span><span class="sxs-lookup"><span data-stu-id="a0b8c-141">bindingRedirects section</span></span>

<span data-ttu-id="a0b8c-142">パッケージのインストール時に、NuGet で自動バインド リダイレクトを実行するかどうかを構成します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-142">Configures whether NuGet does automatic binding redirects when a package is installed.</span></span>

| <span data-ttu-id="a0b8c-143">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-143">Key</span></span> | <span data-ttu-id="a0b8c-144">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-144">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-145">スキップ</span><span class="sxs-lookup"><span data-stu-id="a0b8c-145">skip</span></span> | <span data-ttu-id="a0b8c-146">自動バインド リダイレクトを省略するかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-146">A Boolean indicating whether to skip automatic binding redirects.</span></span> <span data-ttu-id="a0b8c-147">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-147">The default is false.</span></span> |

<span data-ttu-id="a0b8c-148">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-148">**Example**:</span></span>

```xml
<bindingRedirects>
    <add key="skip" value="True" />
</bindingRedirects>
```

## <a name="packagerestore-section"></a><span data-ttu-id="a0b8c-149">packageRestore セクション</span><span class="sxs-lookup"><span data-stu-id="a0b8c-149">packageRestore section</span></span>

<span data-ttu-id="a0b8c-150">ビルド時のパッケージの復元を制御します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-150">Controls package restore during builds.</span></span>

| <span data-ttu-id="a0b8c-151">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-151">Key</span></span> | <span data-ttu-id="a0b8c-152">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-152">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-153">が有効</span><span class="sxs-lookup"><span data-stu-id="a0b8c-153">enabled</span></span> | <span data-ttu-id="a0b8c-154">NuGet で自動復元を実行できるかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-154">A Boolean indicating whether NuGet can perform automatic restore.</span></span> <span data-ttu-id="a0b8c-155">構成ファイル内にこのキーを設定するのでなく、`True` の値で `EnableNuGetPackageRestore` 環境変数を設定することもできます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-155">You can also set the `EnableNuGetPackageRestore` environment variable with a value of `True` instead of setting this key in the config file.</span></span> |
| <span data-ttu-id="a0b8c-156">自動</span><span class="sxs-lookup"><span data-stu-id="a0b8c-156">automatic</span></span> | <span data-ttu-id="a0b8c-157">ビルド中に欠落しているパッケージの確認を NuGet で行う必要があるかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-157">A Boolean indicating whether NuGet should check for missing packages during a build.</span></span> |

<span data-ttu-id="a0b8c-158">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-158">**Example**:</span></span>

```xml
<packageRestore>
    <add key="enabled" value="true" />
    <add key="automatic" value="true" />
</packageRestore>
```

## <a name="solution-section"></a><span data-ttu-id="a0b8c-159">ソリューション セクション</span><span class="sxs-lookup"><span data-stu-id="a0b8c-159">solution section</span></span>

<span data-ttu-id="a0b8c-160">ソリューションの `packages` フォルダーをソース管理に含めるかどうかを制御します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-160">Controls whether the `packages` folder of a solution is included in source control.</span></span> <span data-ttu-id="a0b8c-161">このセクションは、ソリューション フォルダー内の `nuget.config` ファイルでのみ機能します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-161">This section works only in `nuget.config` files in a solution folder.</span></span>

| <span data-ttu-id="a0b8c-162">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-162">Key</span></span> | <span data-ttu-id="a0b8c-163">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-163">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-164">disableSourceControlIntegration</span><span class="sxs-lookup"><span data-stu-id="a0b8c-164">disableSourceControlIntegration</span></span> | <span data-ttu-id="a0b8c-165">ソース管理を使用する場合に、パッケージ フォルダーを無視するかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-165">A Boolean indicating whether to ignore the packages folder when working with source control.</span></span> <span data-ttu-id="a0b8c-166">既定値は false です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-166">The default value is false.</span></span> |

<span data-ttu-id="a0b8c-167">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-167">**Example**:</span></span>

```xml
<solution>
    <add key="disableSourceControlIntegration" value="true" />
</solution>
```

## <a name="package-source-sections"></a><span data-ttu-id="a0b8c-168">パッケージ ソース セクション</span><span class="sxs-lookup"><span data-stu-id="a0b8c-168">Package source sections</span></span>

<span data-ttu-id="a0b8c-169">`packageSources`、`packageSourceCredentials`、`apikeys`、`activePackageSource`、`disabledPackageSources`、`trustedSigners` のすべてが連携して、インストール、復元、および更新の操作中に、NuGet がパッケージリポジトリを操作する方法を構成します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-169">The `packageSources`, `packageSourceCredentials`, `apikeys`, `activePackageSource`, `disabledPackageSources` and `trustedSigners` all work together to configure how NuGet works with package repositories during install, restore, and update operations.</span></span>

<span data-ttu-id="a0b8c-170">[`nuget sources` コマンド](../reference/cli-reference/cli-ref-sources.md)は、通常、これらの設定を管理するために使用されます。ただし、 [`nuget setapikey` コマンド](../reference/cli-reference/cli-ref-setapikey.md)を使用して管理される `apikeys` と、 [`nuget trusted-signers` コマンド](../reference/cli-reference/cli-ref-trusted-signers.md)を使用して管理される `trustedSigners` は除きます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-170">The [`nuget sources` command](../reference/cli-reference/cli-ref-sources.md) is generally used to manage these settings, except for `apikeys` which is managed using the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md), and `trustedSigners` which is managed using the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="a0b8c-171">ここで、nuget.org のソース URL は `https://api.nuget.org/v3/index.json` となります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-171">Note that the source URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span>

### <a name="packagesources"></a><span data-ttu-id="a0b8c-172">packageSources</span><span class="sxs-lookup"><span data-stu-id="a0b8c-172">packageSources</span></span>

<span data-ttu-id="a0b8c-173">すべての既知のパッケージ ソースの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-173">Lists all known package sources.</span></span> <span data-ttu-id="a0b8c-174">この順序は、復元操作中には無視され、PackageReference 形式を使用するプロジェクトでは無視されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-174">The order is ignored during restore operations and with any project using the PackageReference format.</span></span> <span data-ttu-id="a0b8c-175">NuGet は、`packages.config`を使用したプロジェクトでのインストールおよび更新操作のソースの順序を尊重します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-175">NuGet respects the order of sources for install and update operations with projects using `packages.config`.</span></span>

| <span data-ttu-id="a0b8c-176">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-176">Key</span></span> | <span data-ttu-id="a0b8c-177">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-177">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-178">(パッケージ ソースに割り当てる名前)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-178">(name to assign to the package source)</span></span> | <span data-ttu-id="a0b8c-179">パッケージ ソースのパスまたは URL です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-179">The path or URL of the package source.</span></span> |

<span data-ttu-id="a0b8c-180">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-180">**Example**:</span></span>

```xml
<packageSources>
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" protocolVersion="3" />
    <add key="Contoso" value="https://contoso.com/packages/" />
    <add key="Test Source" value="c:\packages" />
</packageSources>
```

### <a name="packagesourcecredentials"></a><span data-ttu-id="a0b8c-181">packageSourceCredentials</span><span class="sxs-lookup"><span data-stu-id="a0b8c-181">packageSourceCredentials</span></span>

<span data-ttu-id="a0b8c-182">通常、`-username` スイッチおよび `-password` スイッチと `nuget sources` によって指定される、ソースのユーザー名とパスワードを格納します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-182">Stores usernames and passwords for sources, typically specified with the `-username` and `-password` switches with `nuget sources`.</span></span> <span data-ttu-id="a0b8c-183">`-storepasswordincleartext` オプションが使用されていない場合、既定ではパスワードが暗号化されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-183">Passwords are encrypted by default unless the `-storepasswordincleartext` option is also used.</span></span>

| <span data-ttu-id="a0b8c-184">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-184">Key</span></span> | <span data-ttu-id="a0b8c-185">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-185">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-186">username</span><span class="sxs-lookup"><span data-stu-id="a0b8c-186">username</span></span> | <span data-ttu-id="a0b8c-187">プレーン テキストで表されるソースのユーザー名です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-187">The user name for the source in plain text.</span></span> |
| <span data-ttu-id="a0b8c-188">のパスワード</span><span class="sxs-lookup"><span data-stu-id="a0b8c-188">password</span></span> | <span data-ttu-id="a0b8c-189">ソースの暗号されたパスワードです。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-189">The encrypted password for the source.</span></span> |
| <span data-ttu-id="a0b8c-190">cleartextpassword</span><span class="sxs-lookup"><span data-stu-id="a0b8c-190">cleartextpassword</span></span> | <span data-ttu-id="a0b8c-191">ソースの暗号化されていないパスワードです。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-191">The unencrypted password for the source.</span></span> |

<span data-ttu-id="a0b8c-192">**例:**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-192">**Example:**</span></span>

<span data-ttu-id="a0b8c-193">構成ファイル内の `<packageSourceCredentials>` 要素には、適用可能なソース名ごとに子ノードが含まれます (名前内のスペースは `_x0020_` と置換されます)。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-193">In the config file, the `<packageSourceCredentials>` element contains child nodes for each applicable source name (spaces in the name are replaced with `_x0020_`).</span></span> <span data-ttu-id="a0b8c-194">つまり、"Contoso" および "Test Source" という名前のソースの場合は、暗号化されたパスワードを使用するとき、構成ファイルには次の内容が含まれます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-194">That is, for sources named "Contoso" and "Test Source", the config file contains the following when using encrypted passwords:</span></span>

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

<span data-ttu-id="a0b8c-195">暗号化されていないパスワードを使用する場合:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-195">When using unencrypted passwords:</span></span>

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

### <a name="apikeys"></a><span data-ttu-id="a0b8c-196">apikeys</span><span class="sxs-lookup"><span data-stu-id="a0b8c-196">apikeys</span></span>

<span data-ttu-id="a0b8c-197">[`nuget setapikey` コマンド](../reference/cli-reference/cli-ref-setapikey.md)で設定される、API キー認証を使用するソースのキーを格納します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-197">Stores keys for sources that use API key authentication, as set with the [`nuget setapikey` command](../reference/cli-reference/cli-ref-setapikey.md).</span></span>

| <span data-ttu-id="a0b8c-198">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-198">Key</span></span> | <span data-ttu-id="a0b8c-199">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-199">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-200">(ソース URL)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-200">(source URL)</span></span> | <span data-ttu-id="a0b8c-201">暗号化された API キー。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-201">The encrypted API key.</span></span> |

<span data-ttu-id="a0b8c-202">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-202">**Example**:</span></span>

```xml
<apikeys>
    <add key="https://MyRepo/ES/api/v2/package" value="encrypted_api_key" />
</apikeys>
```

### <a name="disabledpackagesources"></a><span data-ttu-id="a0b8c-203">disabledPackageSources</span><span class="sxs-lookup"><span data-stu-id="a0b8c-203">disabledPackageSources</span></span>

<span data-ttu-id="a0b8c-204">現在無効になっているソースを識別します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-204">Identified currently disabled sources.</span></span> <span data-ttu-id="a0b8c-205">空の場合もあります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-205">May be empty.</span></span>

| <span data-ttu-id="a0b8c-206">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-206">Key</span></span> | <span data-ttu-id="a0b8c-207">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-207">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-208">(ソースの名前)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-208">(name of source)</span></span> | <span data-ttu-id="a0b8c-209">ソースが無効になっているかどうかを示すブール値です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-209">A Boolean indicating whether the source is disabled.</span></span> |

<span data-ttu-id="a0b8c-210">**例:**</span><span class="sxs-lookup"><span data-stu-id="a0b8c-210">**Example:**</span></span>

```xml
<disabledPackageSources>
    <add key="Contoso" value="true" />
</disabledPackageSources>

<!-- Empty list -->
<disabledPackageSources />
```

### <a name="activepackagesource"></a><span data-ttu-id="a0b8c-211">activePackageSource</span><span class="sxs-lookup"><span data-stu-id="a0b8c-211">activePackageSource</span></span>

<span data-ttu-id="a0b8c-212">*(2.x のみ。3.x 以降では非推奨とされます)*</span><span class="sxs-lookup"><span data-stu-id="a0b8c-212">*(2.x only; deprecated in 3.x+)*</span></span>

<span data-ttu-id="a0b8c-213">現在アクティブなソースを識別し、すべてのソースの集計を示します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-213">Identifies to the currently active source or indicates the aggregate of all sources.</span></span>

| <span data-ttu-id="a0b8c-214">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-214">Key</span></span> | <span data-ttu-id="a0b8c-215">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-215">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-216">(ソースの名前) または `All`</span><span class="sxs-lookup"><span data-stu-id="a0b8c-216">(name of source) or `All`</span></span> | <span data-ttu-id="a0b8c-217">キーがソースの名前である場合は、ソースのパスまたは URL が値となります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-217">If key is the name of a source, the value is the source path or URL.</span></span> <span data-ttu-id="a0b8c-218">`All` の場合は、値を `(Aggregate source)` にして、無効になっていないすべてのパッケージ ソースを結合する必要があります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-218">If `All`, value should be `(Aggregate source)` to combine all package sources that are not otherwise disabled.</span></span> |

<span data-ttu-id="a0b8c-219">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-219">**Example**:</span></span>

```xml
<activePackageSource>
    <!-- Only one active source-->
    <add key="nuget.org" value="https://api.nuget.org/v3/index.json" />

    <!-- All non-disabled sources are active -->
    <add key="All" value="(Aggregate source)" />
</activePackageSource>
```

## <a name="trustedsigners-section"></a><span data-ttu-id="a0b8c-220">trustedSigners 者セクション</span><span class="sxs-lookup"><span data-stu-id="a0b8c-220">trustedSigners section</span></span>

<span data-ttu-id="a0b8c-221">インストールまたは復元中にパッケージを許可するために使用される信頼された署名者を格納します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-221">Stores trusted signers used to allow package while installing or restoring.</span></span> <span data-ttu-id="a0b8c-222">ユーザーが `require`に `signatureValidationMode` を設定した場合、この一覧を空にすることはできません。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-222">This list cannot be empty when the user sets `signatureValidationMode` to `require`.</span></span> 

<span data-ttu-id="a0b8c-223">このセクションは、 [`nuget trusted-signers` コマンド](../reference/cli-reference/cli-ref-trusted-signers.md)を使用して更新できます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-223">This section can be updated with the [`nuget trusted-signers` command](../reference/cli-reference/cli-ref-trusted-signers.md).</span></span>

<span data-ttu-id="a0b8c-224">**[スキーマ]** :</span><span class="sxs-lookup"><span data-stu-id="a0b8c-224">**Schema**:</span></span>

<span data-ttu-id="a0b8c-225">信頼できる署名者には、特定の署名者を識別するすべての証明書を登録する `certificate` 項目のコレクションがあります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-225">A trusted signer has a collection of `certificate` items that enlist all the certificates that identify a given signer.</span></span> <span data-ttu-id="a0b8c-226">信頼できる署名者は、`Author` または `Repository`のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-226">A trusted signer can be either an `Author` or a `Repository`.</span></span>

<span data-ttu-id="a0b8c-227">また、信頼された*リポジトリ*は、リポジトリの `serviceIndex` (有効な `https` uri である必要があります) を指定します。また、必要に応じて、特定のリポジトリから信頼できるユーザーを制限するために、セミコロンで区切られた `owners` の一覧を指定することもできます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-227">A trusted *repository* also specifies the `serviceIndex` for the repository (which has to be a valid `https` uri) and can optionally specify a semi-colon delimited list of `owners` to restrict even more who is trusted from that specific repository.</span></span>

<span data-ttu-id="a0b8c-228">証明書のフィンガープリントに使用されるサポートされているハッシュアルゴリズムは、`SHA256`、`SHA384`、および `SHA512`です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-228">The supported hash algorithms used for a certificate fingerprint are `SHA256`, `SHA384` and `SHA512`.</span></span>

<span data-ttu-id="a0b8c-229">`certificate` がとして `allowUntrustedRoot` を指定する場合 `true` 署名の検証の一部として証明書チェーンを構築するときに、指定した証明書を信頼されていないルートにチェーンすることを許可します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-229">If a `certificate` specifies `allowUntrustedRoot` as `true` the given certificate is allowed to chain to an untrusted root while building the certificate chain as part of the signature verification.</span></span>

<span data-ttu-id="a0b8c-230">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-230">**Example**:</span></span>

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

## <a name="fallbackpackagefolders-section"></a><span data-ttu-id="a0b8c-231">fallbackPackageFolders セクション</span><span class="sxs-lookup"><span data-stu-id="a0b8c-231">fallbackPackageFolders section</span></span>

<span data-ttu-id="a0b8c-232">*(3.5 +)* パッケージがフォールバックフォルダーに存在する場合に作業を行う必要がないように、パッケージをプレインストールする方法を提供します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-232">*(3.5+)* Provides a way to preinstall packages so that no work needs to be done if the package is found in the fallback folders.</span></span> <span data-ttu-id="a0b8c-233">フォールバックパッケージフォルダーには、グローバルパッケージフォルダーとまったく同じフォルダーとファイル構造があり*ます。 nupkg*は存在し、すべてのファイルが抽出されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-233">Fallback package folders have the exact same folder and file structure as the global package folder: *.nupkg* is present, and all files are extracted.</span></span>

<span data-ttu-id="a0b8c-234">この構成の参照ロジックは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-234">The lookup logic for this configuration is:</span></span>

- <span data-ttu-id="a0b8c-235">[グローバルパッケージフォルダー] で、パッケージ/バージョンが既にダウンロードされているかどうかを確認します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-235">Look in global package folder to see if the package/version is already downloaded.</span></span>

- <span data-ttu-id="a0b8c-236">フォールバックフォルダーでパッケージ/バージョンの一致を確認します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-236">Look in the fallback folders for a package/version match.</span></span>

<span data-ttu-id="a0b8c-237">いずれかの参照が成功した場合、ダウンロードは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-237">If either lookup is successful, then no download is necessary.</span></span>

<span data-ttu-id="a0b8c-238">一致するものが見つからない場合、NuGet はファイルソースを確認し、次に http ソースを確認してから、パッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-238">If a match is not found, then NuGet checks file sources, and then http sources, and then it downloads the packages.</span></span>

| <span data-ttu-id="a0b8c-239">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-239">Key</span></span> | <span data-ttu-id="a0b8c-240">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-240">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-241">(フォールバックフォルダーの名前)</span><span class="sxs-lookup"><span data-stu-id="a0b8c-241">(name of fallback folder)</span></span> | <span data-ttu-id="a0b8c-242">フォールバックフォルダーへのパス。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-242">Path to fallback folder.</span></span> |

<span data-ttu-id="a0b8c-243">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-243">**Example**:</span></span>

```xml
<fallbackPackageFolders>
   <add key="XYZ Offline Packages" value="C:\somePath\someFolder\"/>
</fallbackPackageFolders>
```

## <a name="packagemanagement-section"></a><span data-ttu-id="a0b8c-244">packageManagement セクション</span><span class="sxs-lookup"><span data-stu-id="a0b8c-244">packageManagement section</span></span>

<span data-ttu-id="a0b8c-245">既定のパッケージ管理形式である*app.config*または PackageReference を設定します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-245">Sets the default package management format, either *packages.config* or PackageReference.</span></span> <span data-ttu-id="a0b8c-246">SDK スタイルのプロジェクトは常に PackageReference を使用します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-246">SDK-style projects always use PackageReference.</span></span>

| <span data-ttu-id="a0b8c-247">[キー]</span><span class="sxs-lookup"><span data-stu-id="a0b8c-247">Key</span></span> | <span data-ttu-id="a0b8c-248">Value</span><span class="sxs-lookup"><span data-stu-id="a0b8c-248">Value</span></span> |
| --- | --- |
| <span data-ttu-id="a0b8c-249">書式</span><span class="sxs-lookup"><span data-stu-id="a0b8c-249">format</span></span> | <span data-ttu-id="a0b8c-250">既定のパッケージ管理形式を示すブール値。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-250">A Boolean indicating the default package management format.</span></span> <span data-ttu-id="a0b8c-251">`1`の場合、format は PackageReference です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-251">If `1`, format is PackageReference.</span></span> <span data-ttu-id="a0b8c-252">`0`の場合、形式は*app.config*です。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-252">If `0`, format is *packages.config*.</span></span> |
| <span data-ttu-id="a0b8c-253">無効</span><span class="sxs-lookup"><span data-stu-id="a0b8c-253">disabled</span></span> | <span data-ttu-id="a0b8c-254">最初のパッケージのインストール時に既定のパッケージ形式を選択するようにプロンプトを表示するかどうかを示すブール値。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-254">A Boolean indicating whether to show the prompt to select a default package format on first package install.</span></span> <span data-ttu-id="a0b8c-255">`False` プロンプトを非表示にします。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-255">`False` hides the prompt.</span></span> |

<span data-ttu-id="a0b8c-256">**例**:</span><span class="sxs-lookup"><span data-stu-id="a0b8c-256">**Example**:</span></span>

```xml
<packageManagement>
   <add key="format" value="1" />
   <add key="disabled" value="False" />
</packageManagement>
```

## <a name="using-environment-variables"></a><span data-ttu-id="a0b8c-257">環境変数の使用</span><span class="sxs-lookup"><span data-stu-id="a0b8c-257">Using environment variables</span></span>

<span data-ttu-id="a0b8c-258">環境変数を `nuget.config` 値 (NuGet 3.4 以降) に使用することで、実行時に設定を適用できます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-258">You can use environment variables in `nuget.config` values (NuGet 3.4+) to apply settings at run time.</span></span>

<span data-ttu-id="a0b8c-259">たとえば、Windows 上の `HOME` 環境変数を `c:\users\username` に設定すると、構成ファイル内の `%HOME%\NuGetRepository` の値は `c:\users\username\NuGetRepository` に解決されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-259">For example, if the `HOME` environment variable on Windows is set to `c:\users\username`, then the value of `%HOME%\NuGetRepository` in the configuration file resolves to `c:\users\username\NuGetRepository`.</span></span>

<span data-ttu-id="a0b8c-260">同様に、Mac/Linux 上の `HOME` を `/home/myStuff` に設定すると、構成ファイル内の `%HOME%/NuGetRepository` は `/home/myStuff/NuGetRepository` に解決されます。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-260">Similarly, if `HOME` on Mac/Linux is set to `/home/myStuff`, then `%HOME%/NuGetRepository` in the configuration file resolves to `/home/myStuff/NuGetRepository`.</span></span>

<span data-ttu-id="a0b8c-261">環境変数が見つからない場合、NuGet は構成ファイルからのリテラル値を使用します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-261">If an environment variable is not found, NuGet uses the literal value from the configuration file.</span></span>

## <a name="example-config-file"></a><span data-ttu-id="a0b8c-262">構成ファイルの例</span><span class="sxs-lookup"><span data-stu-id="a0b8c-262">Example config file</span></span>

<span data-ttu-id="a0b8c-263">複数の設定が含まれている `nuget.config` ファイルの例を次に示します。</span><span class="sxs-lookup"><span data-stu-id="a0b8c-263">Below is an example `nuget.config` file that illustrates a number of settings:</span></span>

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
