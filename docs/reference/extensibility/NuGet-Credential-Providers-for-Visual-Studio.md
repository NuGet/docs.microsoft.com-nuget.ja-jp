---
title: Visual Studio の NuGet の資格情報プロバイダー
description: NuGet の資格情報プロバイダーは、Visual Studio 拡張機能で IVsCredentialProvider インターフェイスを実装することによって、フィードで認証します。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: d4dbcab7c4005efcdc7efe96df3a70e666c558cc
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817845"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="44a13-103">NuGet の資格情報プロバイダーと Visual Studio でのフィードの認証</span><span class="sxs-lookup"><span data-stu-id="44a13-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="44a13-104">NuGet Visual Studio 拡張機能、3.6 以降には、認証されているフィードを使用する NuGet を有効にする資格情報プロバイダーがサポートしています。</span><span class="sxs-lookup"><span data-stu-id="44a13-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="44a13-105">Visual Studio の NuGet の資格情報プロバイダーをインストールした後、NuGet の Visual Studio 拡張機能が自動的に獲得および必要に応じて、フィードの認証された資格情報を更新します。</span><span class="sxs-lookup"><span data-stu-id="44a13-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="44a13-106">実装のサンプルは含まれて[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)です。</span><span class="sxs-lookup"><span data-stu-id="44a13-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="44a13-107">Visual Studio の NuGet の資格情報プロバイダーが通常の Visual Studio 拡張機能としてインストールする必要があり、必要になります[Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (現在プレビュー中) またはそれ以降。</span><span class="sxs-lookup"><span data-stu-id="44a13-107">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="44a13-108">Visual Studio の NuGet の資格情報プロバイダーは、(dotnet 復元や nuget.exe) ではなく Visual Studio でのみ動作します。</span><span class="sxs-lookup"><span data-stu-id="44a13-108">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="44a13-109">Nuget.exe、資格情報プロバイダーを参照してください。 [nuget.exe 資格情報プロバイダー](nuget-exe-Credential-providers.md)です。</span><span class="sxs-lookup"><span data-stu-id="44a13-109">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="44a13-110">Visual Studio の使用可能な NuGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="44a13-110">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="44a13-111">Visual Studio Team Services をサポートするために、Visual Studio の NuGet 拡張機能に組み込まれている資格情報プロバイダーがあります。</span><span class="sxs-lookup"><span data-stu-id="44a13-111">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="44a13-112">NuGet の Visual Studio 拡張機能を使用して、内部`VsCredentialProviderImporter`プラグインの資格情報プロバイダーのスキャンが実行します。</span><span class="sxs-lookup"><span data-stu-id="44a13-112">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="44a13-113">これらのプラグインの資格情報プロバイダーは、型の MEF エクスポートとして探索可能である必要があります`IVsCredentialProvider`です。</span><span class="sxs-lookup"><span data-stu-id="44a13-113">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="44a13-114">使用可能なプラグインの資格情報プロバイダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="44a13-114">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="44a13-115">Visual Studio 2017 向け MyGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="44a13-115">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="44a13-116">Visual Studio の NuGet 資格情報プロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="44a13-116">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="44a13-117">NuGet Visual Studio 拡張機能、3.6 以降では、資格情報の取得に使用される内部 CredentialService を実装します。</span><span class="sxs-lookup"><span data-stu-id="44a13-117">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="44a13-118">CredentialService には、組み込みおよびプラグインの資格情報プロバイダーの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="44a13-118">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="44a13-119">資格情報を取得するまで、各プロバイダーは順番に試されます。</span><span class="sxs-lookup"><span data-stu-id="44a13-119">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="44a13-120">資格情報の取得中に資格情報のサービスは資格情報を取得するとすぐに停止する次の順序で資格情報プロバイダーをしてください。</span><span class="sxs-lookup"><span data-stu-id="44a13-120">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="44a13-121">NuGet の構成ファイルから資格情報がフェッチされます (組み込みを使用して`SettingsCredentialProvider`)。</span><span class="sxs-lookup"><span data-stu-id="44a13-121">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="44a13-122">パッケージ ソースが Visual Studio Team Services にある場合、`VisualStudioAccountProvider`使用されます。</span><span class="sxs-lookup"><span data-stu-id="44a13-122">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="44a13-123">その他のすべてのプラグインの資格情報プロバイダーは順番に試行されます。</span><span class="sxs-lookup"><span data-stu-id="44a13-123">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="44a13-124">資格情報はまだ取得されていない、ユーザーは、標準の基本認証ダイアログを使用する資格情報を求められます。</span><span class="sxs-lookup"><span data-stu-id="44a13-124">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="44a13-125">IVsCredentialProvider.GetCredentialsAsync を実装します。</span><span class="sxs-lookup"><span data-stu-id="44a13-125">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="44a13-126">Visual Studio の NuGet の資格情報プロバイダーを作成するには、公開するパブリック MEF エクスポートを実装する、Visual Studio 拡張機能を作成、 `IVsCredentialProvider` 「」とは大きく分けて次原則に従います。</span><span class="sxs-lookup"><span data-stu-id="44a13-126">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="44a13-127">実装のサンプルは含まれて[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)です。</span><span class="sxs-lookup"><span data-stu-id="44a13-127">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="44a13-128">Visual Studio の各 NuGet 資格情報プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="44a13-128">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="44a13-129">かどうか、資格情報を入力、対象となる URI の資格情報の取得を開始する前に決定します。</span><span class="sxs-lookup"><span data-stu-id="44a13-129">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="44a13-130">かどうかは、プロバイダーは、対象のソースの資格情報を提供できません、返すか`null`です。</span><span class="sxs-lookup"><span data-stu-id="44a13-130">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="44a13-131">プロバイダーでは、対象となる URI の要求を処理している場合、資格情報を指定することはできません、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="44a13-131">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="44a13-132">Visual Studio のカスタム NuGet 資格情報プロバイダーを実装する必要があります、`IVsCredentialProvider`インターフェイスで使用できる、 [NuGet.VisualStudio パッケージ](https://www.nuget.org/packages/NuGet.VisualStudio/)です。</span><span class="sxs-lookup"><span data-stu-id="44a13-132">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="44a13-133">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="44a13-133">GetCredentialAsync</span></span>

| <span data-ttu-id="44a13-134">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="44a13-134">Input Parameter</span></span> |<span data-ttu-id="44a13-135">説明</span><span class="sxs-lookup"><span data-stu-id="44a13-135">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="44a13-136">Uri の uri</span><span class="sxs-lookup"><span data-stu-id="44a13-136">Uri uri</span></span> | <span data-ttu-id="44a13-137">資格情報が要求されているパッケージ ソースの Uri。</span><span class="sxs-lookup"><span data-stu-id="44a13-137">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="44a13-138">IWebProxy プロキシ</span><span class="sxs-lookup"><span data-stu-id="44a13-138">IWebProxy proxy</span></span> | <span data-ttu-id="44a13-139">ネットワークで通信を行うときに使用する web プロキシです。</span><span class="sxs-lookup"><span data-stu-id="44a13-139">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="44a13-140">プロキシ認証の構成が存在しない場合は null です。</span><span class="sxs-lookup"><span data-stu-id="44a13-140">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="44a13-141">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="44a13-141">bool isProxyRequest</span></span> | <span data-ttu-id="44a13-142">この要求はプロキシ認証の資格情報を取得する場合は true。</span><span class="sxs-lookup"><span data-stu-id="44a13-142">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="44a13-143">実装がプロキシ資格情報を取得するために有効でない場合 null を返される必要があります。</span><span class="sxs-lookup"><span data-stu-id="44a13-143">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="44a13-144">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="44a13-144">bool isRetry</span></span> | <span data-ttu-id="44a13-145">True の場合、資格情報がこの Uri は、以前要求したが、指定された資格情報は、承認されたアクセスを許可しませんでした。</span><span class="sxs-lookup"><span data-stu-id="44a13-145">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="44a13-146">非対話型の bool</span><span class="sxs-lookup"><span data-stu-id="44a13-146">bool nonInteractive</span></span> | <span data-ttu-id="44a13-147">True の場合、資格情報プロバイダーはすべてのユーザー メッセージを抑制して、既定値の代わりに使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44a13-147">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="44a13-148">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="44a13-148">CancellationToken cancellationToken</span></span> | <span data-ttu-id="44a13-149">このキャンセル トークンを確認して、操作要求元の資格情報が取り消されましたかどうかを特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="44a13-149">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="44a13-150">**戻り値**: 資格情報オブジェクトを実装する、 [ `System.Net.ICredentials`インターフェイス](/dotnet/api/system.net.icredentials?view=netstandard-2.0)です。</span><span class="sxs-lookup"><span data-stu-id="44a13-150">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
