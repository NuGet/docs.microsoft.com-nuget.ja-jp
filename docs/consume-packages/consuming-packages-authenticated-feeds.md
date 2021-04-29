---
title: 認証済みフィードからのパッケージの使用
description: すべての NuGet クライアント シナリオでの認証済みフィードからのパッケージの使用
author: nkolev92
ms.author: nikolev
ms.date: 02/28/2020
ms.topic: conceptual
ms.openlocfilehash: e76fefaf4d3c86aa15cf279090c0adb8ed779aab
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901513"
---
# <a name="consuming-packages-from-authenticated-feeds"></a><span data-ttu-id="24ea2-103">認証済みフィードからのパッケージの使用</span><span class="sxs-lookup"><span data-stu-id="24ea2-103">Consuming packages from authenticated feeds</span></span>

<span data-ttu-id="24ea2-104">nuget.org [パブリック フィード](https://api.nuget.org/v3/index.json)に加えて、NuGet クライアントでは、ファイル フィードとプライベート http フィードを操作することができます。</span><span class="sxs-lookup"><span data-stu-id="24ea2-104">In addition to the nuget.org [public feed](https://api.nuget.org/v3/index.json), NuGet clients have the ability to interact with file feeds and private http feeds.</span></span>


<span data-ttu-id="24ea2-105">プライベート http フィードで認証するには、次の 2 つの方法があります。</span><span class="sxs-lookup"><span data-stu-id="24ea2-105">To authenticate with private http feeds, the 2 approaches are:</span></span>

* <span data-ttu-id="24ea2-106">[NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials) で資格情報を追加する</span><span class="sxs-lookup"><span data-stu-id="24ea2-106">Add credentials in the [NuGet.config](../reference/nuget-config-file.md#packagesourcecredentials)</span></span>
* <span data-ttu-id="24ea2-107">使用するクライアントに応じて、多くの拡張モデルのいずれかを使用して認証する</span><span class="sxs-lookup"><span data-stu-id="24ea2-107">Authenticate using one of the many extensibility models depending on the client used.</span></span>

## <a name="nuget-clients-authentication-extensibility"></a><span data-ttu-id="24ea2-108">NuGet クライアントの認証の拡張性</span><span class="sxs-lookup"><span data-stu-id="24ea2-108">NuGet clients' authentication extensibility</span></span>

<span data-ttu-id="24ea2-109">さまざまな NuGet クライアントでは、プライベート フィード プロバイダーそのものが認証を担当します。</span><span class="sxs-lookup"><span data-stu-id="24ea2-109">For the various NuGet clients, the private feed provider itself is responsible for authentication.</span></span>
<span data-ttu-id="24ea2-110">すべての NuGet クライアントには、これをサポートするための拡張メソッドがあります。</span><span class="sxs-lookup"><span data-stu-id="24ea2-110">All NuGet clients have extensibility methods to support this.</span></span> <span data-ttu-id="24ea2-111">これらは、Visual Studio の拡張機能、または NuGet と通信して資格情報を取得できるプラグインのいずれかです。</span><span class="sxs-lookup"><span data-stu-id="24ea2-111">These are either a Visual Studio extension or a plugin that can communicate with NuGet to retrieve credentials.</span></span>

### <a name="visual-studio"></a><span data-ttu-id="24ea2-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="24ea2-112">Visual Studio</span></span>

<span data-ttu-id="24ea2-113">Visual Studio では、フィード プロバイダーが実装して顧客に提供できるインターフェイスが NuGet によって公開されます。</span><span class="sxs-lookup"><span data-stu-id="24ea2-113">In Visual Studio, NuGet exposes an interface that feed providers can implement and provide to their customers.</span></span> <span data-ttu-id="24ea2-114">詳細については、[Visual Studio 資格情報プロバイダーの作成方法](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md)に関するドキュメントを参照してください。</span><span class="sxs-lookup"><span data-stu-id="24ea2-114">For more details, please refer to the documentation on [how to create a Visual Studio credential provider](../reference/extensibility/NuGet-Credential-Providers-for-Visual-Studio.md).</span></span>

#### <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="24ea2-115">Visual Studio 向けの使用可能な NuGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-115">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="24ea2-116">Azure DevOps をサポートするために、Visual Studio に組み込まれている資格情報プロバイダーがあります。</span><span class="sxs-lookup"><span data-stu-id="24ea2-116">There is a credential provider built into Visual Studio to support Azure DevOps.</span></span>


<span data-ttu-id="24ea2-117">利用可能なプラグイン資格情報プロバイダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="24ea2-117">Available plug-in credential providers include:</span></span>

* [<span data-ttu-id="24ea2-118">Visual Studio 向け MyGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-118">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

### <a name="nugetexe"></a><span data-ttu-id="24ea2-119">nuget.exe</span><span class="sxs-lookup"><span data-stu-id="24ea2-119">nuget.exe</span></span>

<span data-ttu-id="24ea2-120">`nuget.exe` では、フィードによる認証のために資格情報が必要な場合に、次の方法でそれらが検索されます。</span><span class="sxs-lookup"><span data-stu-id="24ea2-120">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="24ea2-121">`NuGet.config` ファイル内で資格情報を検索します。</span><span class="sxs-lookup"><span data-stu-id="24ea2-121">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="24ea2-122">V2 プラグイン資格情報プロバイダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="24ea2-122">Use V2 plug-in credential providers</span></span>
1. <span data-ttu-id="24ea2-123">V1 プラグイン資格情報プロバイダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="24ea2-123">Use V1 plug-in credential providers</span></span>
1. <span data-ttu-id="24ea2-124">その後、NuGet がコマンド ラインでユーザーに資格情報の入力を求めます。</span><span class="sxs-lookup"><span data-stu-id="24ea2-124">NuGet then prompts the user for credentials on the command line.</span></span>

#### <a name="nugetexe-and-v2-credential-providers"></a><span data-ttu-id="24ea2-125">nuget.exe と V2 の資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-125">nuget.exe and V2 credential providers</span></span>

<span data-ttu-id="24ea2-126">バージョン `4.8` では、NuGet によって新しい認証プラグイン メカニズムが定義され、これ以降、V2 資格情報プロバイダーと呼ばれています。</span><span class="sxs-lookup"><span data-stu-id="24ea2-126">In version `4.8` NuGet defined a new authentication plugin mechanism, hereafter referred to as V2 credential providers.</span></span>
<span data-ttu-id="24ea2-127">これらのプロバイダーのインストールと検出については、「[NuGet のクロス プラットフォーム プラグイン](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24ea2-127">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="nugetexe-and-v1-credential-providers"></a><span data-ttu-id="24ea2-128">nuget.exe と V1 の資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-128">nuget.exe and V1 credential providers</span></span>

<span data-ttu-id="24ea2-129">バージョン `3.3` では、NuGet で認証プラグインの最初のバージョンが導入されました。</span><span class="sxs-lookup"><span data-stu-id="24ea2-129">In version `3.3` NuGet introduced the first version of authentication plugins.</span></span>
<span data-ttu-id="24ea2-130">これらのプロバイダーのインストールと検出については、[nuget.exe 資格情報プロバイダー](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)に関するセクションを参照してください。</span><span class="sxs-lookup"><span data-stu-id="24ea2-130">For the installation and discovery of those providers refer to [nuget.exe credential providers](../reference/extensibility/nuget-exe-Credential-Providers.md#nugetexe-credential-provider-discovery)</span></span>

#### <a name="available-credential-providers-for-nugetexe"></a><span data-ttu-id="24ea2-131">nuget.exe の利用可能な資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-131">Available credential providers for nuget.exe</span></span>

* <span data-ttu-id="24ea2-132">[Azure DevOps V2 資格情報プロバイダー](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) または [Azure Artifacts 資格情報プロバイダー](https://github.com/microsoft/artifacts-credprovider)</span><span class="sxs-lookup"><span data-stu-id="24ea2-132">[Azure DevOps V2 Credential Providers](/azure/devops/artifacts/nuget/nuget-exe#add-a-feed-to-nuget-482-or-later) or [Azure Artifacts Credential Provider](https://github.com/microsoft/artifacts-credprovider)</span></span>

<span data-ttu-id="24ea2-133">Visual Studio 2017 バージョン 15.9 以降では、Azure DevOps 資格情報プロバイダーが Visual Studio にバンドルされています。</span><span class="sxs-lookup"><span data-stu-id="24ea2-133">With Visual Studio 2017 version 15.9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span>
<span data-ttu-id="24ea2-134">`nuget.exe` がその特定の Visual Studio ツールセットから MSBuild を使用している場合、プラグインは自動的に検出されます。</span><span class="sxs-lookup"><span data-stu-id="24ea2-134">If `nuget.exe` uses MSBuild from that specific Visual Studio toolset, then the plugin will be discovered automatically.</span></span>

### <a name="dotnetexe"></a><span data-ttu-id="24ea2-135">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="24ea2-135">dotnet.exe</span></span>

<span data-ttu-id="24ea2-136">`dotnet.exe` では、フィードによる認証のために資格情報が必要な場合に、次の方法でそれらが検索されます。</span><span class="sxs-lookup"><span data-stu-id="24ea2-136">When `dotnet.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="24ea2-137">`NuGet.config` ファイル内で資格情報を検索します。</span><span class="sxs-lookup"><span data-stu-id="24ea2-137">Look for credentials in `NuGet.config` files.</span></span>
1. <span data-ttu-id="24ea2-138">V2 プラグイン資格情報プロバイダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="24ea2-138">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="24ea2-139">既定では `dotnet.exe` は対話型ではないため、認証をブロックするツールを取得するには、`--interactive` フラグを渡す必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="24ea2-139">By default `dotnet.exe` is not interactive, so you might need to pass an `--interactive` flag to get the tool to block for authentication.</span></span>

#### <a name="dotnetexe-and-v2-credential-providers"></a><span data-ttu-id="24ea2-140">dotnet.exe と V2 の資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-140">dotnet.exe and V2 credential providers</span></span>

<span data-ttu-id="24ea2-141">SDK のバージョン `2.2.100` で、すべてのクライアントで動作する認証プラグイン メカニズムが NuGet によって定義されました。</span><span class="sxs-lookup"><span data-stu-id="24ea2-141">In version `2.2.100` of the SDK, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="24ea2-142">これらのプロバイダーのインストールと検出については、「[NuGet のクロス プラットフォーム プラグイン](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24ea2-142">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-dotnetexe"></a><span data-ttu-id="24ea2-143">dotnet.exe の利用可能な資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-143">Available credential providers for dotnet.exe</span></span>

* [<span data-ttu-id="24ea2-144">Azure Artifacts 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-144">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

### <a name="msbuildexe"></a><span data-ttu-id="24ea2-145">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="24ea2-145">MSBuild.exe</span></span>

<span data-ttu-id="24ea2-146">`MSBuild.exe` では、フィードによる認証のために資格情報が必要な場合に、次の方法でそれらが検索されます。</span><span class="sxs-lookup"><span data-stu-id="24ea2-146">When `MSBuild.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="24ea2-147">`NuGet.config` ファイル内で資格情報を検索します。</span><span class="sxs-lookup"><span data-stu-id="24ea2-147">Look for credentials in `NuGet.config` files</span></span>
1. <span data-ttu-id="24ea2-148">V2 プラグイン資格情報プロバイダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="24ea2-148">Use V2 plug-in credential providers</span></span>

<span data-ttu-id="24ea2-149">既定では `MSBuild.exe` は対話型ではないため、認証をブロックするツールを取得するには、`/p:NuGetInteractive=true` プロパティを設定する必要がある場合があります。</span><span class="sxs-lookup"><span data-stu-id="24ea2-149">By default `MSBuild.exe` is not interactive, so you might need to set the `/p:NuGetInteractive=true` property to get the tool to block for authentication.</span></span>

#### <a name="msbuildexe-and-v2-credential-providers"></a><span data-ttu-id="24ea2-150">MSBuild.exe と V2 の資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-150">MSBuild.exe and V2 credential providers</span></span>

<span data-ttu-id="24ea2-151">Visual Studio 2019 Update 9 で、すべてのクライアントで動作する認証プラグイン メカニズムが NuGet によって定義されました。</span><span class="sxs-lookup"><span data-stu-id="24ea2-151">In Visual Studio 2019 Update 9, NuGet defined an authentication plugin mechanism that works in all clients.</span></span>
<span data-ttu-id="24ea2-152">これらのプロバイダーのインストールと検出については、「[NuGet のクロス プラットフォーム プラグイン](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="24ea2-152">For the installation and discovery of those providers, refer to [NuGet cross platform plugins](../reference/extensibility/NuGet-Cross-Platform-Plugins.md#plugin-installation-and-discovery).</span></span>

#### <a name="available-credential-providers-for-msbuildexe"></a><span data-ttu-id="24ea2-153">MSBuild.exe の利用可能な資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-153">Available credential providers for MSBuild.exe</span></span>

* [<span data-ttu-id="24ea2-154">Azure Artifacts 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="24ea2-154">Azure Artifacts Credential Provider</span></span>](https://github.com/microsoft/artifacts-credprovider)

<span data-ttu-id="24ea2-155">Visual Studio 2017 Update 9 以降では、Azure DevOps 資格情報プロバイダーが Visual Studio にバンドルされています。</span><span class="sxs-lookup"><span data-stu-id="24ea2-155">With Visual Studio 2017 Update 9 and later, the Azure DevOps credential provider is bundled in Visual Studio.</span></span> <span data-ttu-id="24ea2-156">追加の手順は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="24ea2-156">No additional steps are required.</span></span>
