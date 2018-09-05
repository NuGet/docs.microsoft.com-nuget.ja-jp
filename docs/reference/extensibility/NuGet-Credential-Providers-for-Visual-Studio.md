---
title: Visual Studio 向け NuGet 資格情報プロバイダー
description: NuGet 資格情報プロバイダーは、Visual Studio 拡張機能で IVsCredentialProvider インターフェイスを実装することによって、フィードで認証します。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: abe009fee5863c55a188f4d7c71ed0924dd067ff
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547955"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="42751-103">NuGet 資格情報プロバイダーでフィードを Visual Studio での認証</span><span class="sxs-lookup"><span data-stu-id="42751-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="42751-104">NuGet Visual Studio Extension 3.6 以降では、資格情報プロバイダーは、認証されたフィードを使用する NuGet を有効にするサポートしています。</span><span class="sxs-lookup"><span data-stu-id="42751-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="42751-105">Visual Studio 向け NuGet 資格情報プロバイダーをインストールした後、Visual Studio の NuGet 拡張機能が自動的に獲得および必要に応じて、認証されたフィードの資格情報を更新します。</span><span class="sxs-lookup"><span data-stu-id="42751-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="42751-106">実装のサンプルが記載[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)します。</span><span class="sxs-lookup"><span data-stu-id="42751-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="42751-107">4.8 + 以降、Visual Studio の NuGet が新しいクロス プラットフォーム認証プラグインを同様に、サポートしていますが、パフォーマンス上の理由から推奨されるアプローチではありません。</span><span class="sxs-lookup"><span data-stu-id="42751-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="42751-108">Visual Studio 向け NuGet 資格情報プロバイダーを選択し、通常 Visual Studio 拡張機能としてインストールする必要がありますが必要になります[Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe)以降。</span><span class="sxs-lookup"><span data-stu-id="42751-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="42751-109">Visual Studio 向け NuGet 資格情報プロバイダーは、(dotnet 復元または nuget.exe) ではなく Visual Studio でのみ動作します。</span><span class="sxs-lookup"><span data-stu-id="42751-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="42751-110">Nuget.exe 資格情報プロバイダーは、次を参照してください。 [nuget.exe 資格情報プロバイダー](nuget-exe-Credential-providers.md)します。</span><span class="sxs-lookup"><span data-stu-id="42751-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="42751-111">資格情報プロバイダーでは、dotnet と msbuild を参照してください[NuGet クロス プラットフォームのプラグイン](nuget-cross-platform-authentication-plugin.md)</span><span class="sxs-lookup"><span data-stu-id="42751-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="42751-112">Visual Studio 用の利用可能な NuGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="42751-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="42751-113">Visual Studio Team Services をサポートするために、Visual Studio の NuGet 拡張機能に組み込まれている資格情報プロバイダーがあります。</span><span class="sxs-lookup"><span data-stu-id="42751-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="42751-114">Visual Studio の NuGet 拡張機能を使用して内部`VsCredentialProviderImporter`もプラグインの資格情報プロバイダーがスキャンします。</span><span class="sxs-lookup"><span data-stu-id="42751-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="42751-115">これらのプラグインの資格情報プロバイダーは、型の MEF エクスポートとして検出可能である必要があります`IVsCredentialProvider`します。</span><span class="sxs-lookup"><span data-stu-id="42751-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="42751-116">使用可能なプラグインの資格情報プロバイダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="42751-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="42751-117">Visual Studio 2017 向け MyGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="42751-117">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="42751-118">Visual Studio 向け NuGet 資格情報プロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="42751-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="42751-119">NuGet Visual Studio Extension 3.6 以降では、資格情報を取得するために使用される内部の CredentialService を実装します。</span><span class="sxs-lookup"><span data-stu-id="42751-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="42751-120">CredentialService には、組み込みおよびプラグインの資格情報プロバイダーの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="42751-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="42751-121">各プロバイダーが資格情報を取得するまで順番に試されます。</span><span class="sxs-lookup"><span data-stu-id="42751-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="42751-122">資格情報の取得中に資格情報サービスに資格情報が取得されるとすぐに停止する次の順序で資格情報プロバイダーは試してください。</span><span class="sxs-lookup"><span data-stu-id="42751-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="42751-123">NuGet 構成ファイルから資格情報がフェッチされます (組み込みの`SettingsCredentialProvider`)。</span><span class="sxs-lookup"><span data-stu-id="42751-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="42751-124">Visual Studio Team Services では、パッケージ ソースがある場合、`VisualStudioAccountProvider`使用されます。</span><span class="sxs-lookup"><span data-stu-id="42751-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="42751-125">プラグインしている他の Visual Studio の資格情報プロバイダーは順番に試行されます。</span><span class="sxs-lookup"><span data-stu-id="42751-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="42751-126">順番にクロス プラットフォームの資格情報プロバイダーのすべての NuGet を使用してください。</span><span class="sxs-lookup"><span data-stu-id="42751-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="42751-127">資格情報はまだ取得されていない場合、ユーザーは標準の基本認証ダイアログを使用して資格情報を求めます。</span><span class="sxs-lookup"><span data-stu-id="42751-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="42751-128">IVsCredentialProvider.GetCredentialsAsync を実装します。</span><span class="sxs-lookup"><span data-stu-id="42751-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="42751-129">Visual Studio 向け NuGet 資格情報プロバイダーを作成するには、公開するパブリック MEF エクスポートを実装する Visual Studio 拡張機能を作成、`IVsCredentialProvider`以下に示す原則に準拠している型します。</span><span class="sxs-lookup"><span data-stu-id="42751-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

```cs
public interface IVsCredentialProvider
{
    Task<ICredentials> GetCredentialsAsync(
        Uri uri,
        IWebProxy proxy,
        bool isProxyRequest,
        bool isRetry,
        bool nonInteractive,
        CancellationToken cancellationToken);
}
```

<span data-ttu-id="42751-130">実装のサンプルが記載[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)します。</span><span class="sxs-lookup"><span data-stu-id="42751-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="42751-131">Visual Studio の各 NuGet 資格情報プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="42751-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="42751-132">かどうかを対象となる URI の資格情報が提供資格情報の取得を開始する前に決定します。</span><span class="sxs-lookup"><span data-stu-id="42751-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="42751-133">返されます場合、プロバイダーは、対象のソースの資格情報を提供できません`null`します。</span><span class="sxs-lookup"><span data-stu-id="42751-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="42751-134">場合は、プロバイダーは、対象となる URI の要求を処理するには、資格情報を指定することはできません、例外がスローする必要があります。</span><span class="sxs-lookup"><span data-stu-id="42751-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="42751-135">Visual Studio 向けカスタム NuGet 資格情報プロバイダーを実装する必要があります、`IVsCredentialProvider`インターフェイスで使用できる、 [NuGet.VisualStudio パッケージ](https://www.nuget.org/packages/NuGet.VisualStudio/)します。</span><span class="sxs-lookup"><span data-stu-id="42751-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="42751-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="42751-136">GetCredentialAsync</span></span>

| <span data-ttu-id="42751-137">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="42751-137">Input Parameter</span></span> |<span data-ttu-id="42751-138">説明</span><span class="sxs-lookup"><span data-stu-id="42751-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="42751-139">Uri の uri</span><span class="sxs-lookup"><span data-stu-id="42751-139">Uri uri</span></span> | <span data-ttu-id="42751-140">資格情報が要求されているパッケージのソース Uri。</span><span class="sxs-lookup"><span data-stu-id="42751-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="42751-141">IWebProxy プロキシ</span><span class="sxs-lookup"><span data-stu-id="42751-141">IWebProxy proxy</span></span> | <span data-ttu-id="42751-142">Web プロキシ、ネットワークで通信を行うときに使用します。</span><span class="sxs-lookup"><span data-stu-id="42751-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="42751-143">プロキシ認証の構成が存在しない場合は null です。</span><span class="sxs-lookup"><span data-stu-id="42751-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="42751-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="42751-144">bool isProxyRequest</span></span> | <span data-ttu-id="42751-145">この要求は、プロキシ認証の資格情報を取得する場合は true。</span><span class="sxs-lookup"><span data-stu-id="42751-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="42751-146">実装がプロキシの資格情報を取得するために有効でない場合は null が返されます。</span><span class="sxs-lookup"><span data-stu-id="42751-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="42751-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="42751-147">bool isRetry</span></span> | <span data-ttu-id="42751-148">True の場合、以前に資格情報が、この Uri の要求が、指定された資格情報は、承認されたアクセスを許可しませんでした。</span><span class="sxs-lookup"><span data-stu-id="42751-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="42751-149">非対話型の bool</span><span class="sxs-lookup"><span data-stu-id="42751-149">bool nonInteractive</span></span> | <span data-ttu-id="42751-150">True の場合、資格情報プロバイダーはすべてのユーザー メッセージを非表示し、既定値の代わりに使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42751-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="42751-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="42751-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="42751-152">このキャンセル トークンをチェックして、操作要求元の資格情報が取り消されましたかどうかを判断する必要があります。</span><span class="sxs-lookup"><span data-stu-id="42751-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="42751-153">**値を返す**: 実装する資格情報オブジェクト、 [ `System.Net.ICredentials`インターフェイス](/dotnet/api/system.net.icredentials?view=netstandard-2.0)します。</span><span class="sxs-lookup"><span data-stu-id="42751-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
