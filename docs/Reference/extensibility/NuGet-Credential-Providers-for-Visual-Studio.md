---
title: "Visual Studio の NuGet の資格情報プロバイダー |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 9c7f6d16-f437-47c4-82d4-6c996e0b18ec
description: "NuGet の資格情報プロバイダーは、Visual Studio 拡張機能で IVsCredentialProvider インターフェイスを実装することによって、フィードで認証します。"
keywords: "NuGet の資格情報プロバイダー、フィードでの認証、ギャラリー、NuGet の visual studio 拡張機能での認証"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2b2fac23102865a08509acc1cc3d09f0cd375f26
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="b4a78-104">NuGet の資格情報プロバイダーと Visual Studio でのフィードの認証</span><span class="sxs-lookup"><span data-stu-id="b4a78-104">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="b4a78-105">NuGet Visual Studio 拡張機能、3.6 以降には、認証されているフィードを使用する NuGet を有効にする資格情報プロバイダーがサポートしています。</span><span class="sxs-lookup"><span data-stu-id="b4a78-105">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="b4a78-106">Visual Studio の NuGet の資格情報プロバイダーをインストールした後、NuGet の Visual Studio 拡張機能が自動的に獲得および必要に応じて、フィードの認証された資格情報を更新します。</span><span class="sxs-lookup"><span data-stu-id="b4a78-106">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="b4a78-107">実装のサンプルは含まれて[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-107">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

> [!Note]
> <span data-ttu-id="b4a78-108">Visual Studio の NuGet の資格情報プロバイダーが通常の Visual Studio 拡張機能としてインストールする必要があり、必要になります[Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (現在プレビュー中) またはそれ以降。</span><span class="sxs-lookup"><span data-stu-id="b4a78-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/preview/vs_enterprise) (currently in preview) or above.</span></span>
>
> <span data-ttu-id="b4a78-109">Visual Studio の NuGet の資格情報プロバイダーは、(dotnet 復元や nuget.exe) ではなく Visual Studio でのみ動作します。</span><span class="sxs-lookup"><span data-stu-id="b4a78-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="b4a78-110">Nuget.exe、資格情報プロバイダーを参照してください。 [nuget.exe 資格情報プロバイダー](nuget-exe-Credential-providers.md)です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="b4a78-111">Visual Studio の使用可能な NuGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="b4a78-111">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="b4a78-112">Visual Studio Team Services をサポートするために、Visual Studio の NuGet 拡張機能に組み込まれている資格情報プロバイダーがあります。</span><span class="sxs-lookup"><span data-stu-id="b4a78-112">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="b4a78-113">NuGet の Visual Studio 拡張機能を使用して、内部`VsCredentialProviderImporter`プラグインの資格情報プロバイダーのスキャンが実行します。</span><span class="sxs-lookup"><span data-stu-id="b4a78-113">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="b4a78-114">これらのプラグインの資格情報プロバイダーは、型の MEF エクスポートとして探索可能である必要があります`IVsCredentialProvider`です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-114">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="b4a78-115">使用可能なプラグインの資格情報プロバイダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="b4a78-115">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="b4a78-116">Visual Studio 2017 向け MyGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="b4a78-116">MyGet Credential Provider for Visual Studio 2017</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="b4a78-117">Visual Studio の NuGet 資格情報プロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="b4a78-117">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="b4a78-118">NuGet Visual Studio 拡張機能、3.6 以降では、資格情報の取得に使用される内部 CredentialService を実装します。</span><span class="sxs-lookup"><span data-stu-id="b4a78-118">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="b4a78-119">CredentialService には、組み込みおよびプラグインの資格情報プロバイダーの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="b4a78-119">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="b4a78-120">資格情報を取得するまで、各プロバイダーは順番に試されます。</span><span class="sxs-lookup"><span data-stu-id="b4a78-120">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="b4a78-121">資格情報の取得中に資格情報のサービスは資格情報を取得するとすぐに停止する次の順序で資格情報プロバイダーをしてください。</span><span class="sxs-lookup"><span data-stu-id="b4a78-121">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="b4a78-122">NuGet の構成ファイルから資格情報がフェッチされます (組み込みを使用して`SettingsCredentialProvider`)。</span><span class="sxs-lookup"><span data-stu-id="b4a78-122">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="b4a78-123">パッケージ ソースが Visual Studio Team Services にある場合、`VisualStudioAccountProvider`使用されます。</span><span class="sxs-lookup"><span data-stu-id="b4a78-123">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="b4a78-124">その他のすべてのプラグインの資格情報プロバイダーは順番に試行されます。</span><span class="sxs-lookup"><span data-stu-id="b4a78-124">All other plug-in credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="b4a78-125">資格情報はまだ取得されていない、ユーザーは、標準の基本認証ダイアログを使用する資格情報を求められます。</span><span class="sxs-lookup"><span data-stu-id="b4a78-125">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="b4a78-126">IVsCredentialProvider.GetCredentialsAsync を実装します。</span><span class="sxs-lookup"><span data-stu-id="b4a78-126">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="b4a78-127">Visual Studio の NuGet の資格情報プロバイダーを作成するには、公開するパブリック MEF エクスポートを実装する、Visual Studio 拡張機能を作成、 `IVsCredentialProvider` 「」とは大きく分けて次原則に従います。</span><span class="sxs-lookup"><span data-stu-id="b4a78-127">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="b4a78-128">実装のサンプルは含まれて[VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-128">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="b4a78-129">Visual Studio の各 NuGet 資格情報プロバイダーが必要です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-129">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="b4a78-130">かどうか、資格情報を入力、対象となる URI の資格情報の取得を開始する前に決定します。</span><span class="sxs-lookup"><span data-stu-id="b4a78-130">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="b4a78-131">かどうかは、プロバイダーは、対象のソースの資格情報を提供できません、返すか`null`です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-131">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="b4a78-132">プロバイダーでは、対象となる URI の要求を処理している場合、資格情報を指定することはできません、例外がスローされます。</span><span class="sxs-lookup"><span data-stu-id="b4a78-132">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="b4a78-133">Visual Studio のカスタム NuGet 資格情報プロバイダーを実装する必要があります、`IVsCredentialProvider`インターフェイスで使用できる、 [NuGet.VisualStudio パッケージ](https://www.nuget.org/packages/NuGet.VisualStudio/)です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-133">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="b4a78-134">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="b4a78-134">GetCredentialAsync</span></span>

| <span data-ttu-id="b4a78-135">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="b4a78-135">Input Parameter</span></span> |<span data-ttu-id="b4a78-136">説明</span><span class="sxs-lookup"><span data-stu-id="b4a78-136">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="b4a78-137">Uri の uri</span><span class="sxs-lookup"><span data-stu-id="b4a78-137">Uri uri</span></span> | <span data-ttu-id="b4a78-138">資格情報が要求されているパッケージ ソースの Uri。</span><span class="sxs-lookup"><span data-stu-id="b4a78-138">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="b4a78-139">IWebProxy プロキシ</span><span class="sxs-lookup"><span data-stu-id="b4a78-139">IWebProxy proxy</span></span> | <span data-ttu-id="b4a78-140">ネットワークで通信を行うときに使用する web プロキシです。</span><span class="sxs-lookup"><span data-stu-id="b4a78-140">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="b4a78-141">プロキシ認証の構成が存在しない場合は null です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-141">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="b4a78-142">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="b4a78-142">bool isProxyRequest</span></span> | <span data-ttu-id="b4a78-143">この要求はプロキシ認証の資格情報を取得する場合は true。</span><span class="sxs-lookup"><span data-stu-id="b4a78-143">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="b4a78-144">実装がプロキシ資格情報を取得するために有効でない場合 null を返される必要があります。</span><span class="sxs-lookup"><span data-stu-id="b4a78-144">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="b4a78-145">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="b4a78-145">bool isRetry</span></span> | <span data-ttu-id="b4a78-146">True の場合、資格情報がこの Uri は、以前要求したが、指定された資格情報は、承認されたアクセスを許可しませんでした。</span><span class="sxs-lookup"><span data-stu-id="b4a78-146">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="b4a78-147">非対話型の bool</span><span class="sxs-lookup"><span data-stu-id="b4a78-147">bool nonInteractive</span></span> | <span data-ttu-id="b4a78-148">True の場合、資格情報プロバイダーはすべてのユーザー メッセージを抑制して、既定値の代わりに使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b4a78-148">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="b4a78-149">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="b4a78-149">CancellationToken cancellationToken</span></span> | <span data-ttu-id="b4a78-150">このキャンセル トークンを確認して、操作要求元の資格情報が取り消されましたかどうかを特定する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b4a78-150">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |
  
<span data-ttu-id="b4a78-151">**戻り値**: 資格情報オブジェクトを実装する、 [ `System.Net.ICredentials`インターフェイス](https://msdn.microsoft.com/library/system.net.icredentials.aspx)です。</span><span class="sxs-lookup"><span data-stu-id="b4a78-151">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](https://msdn.microsoft.com/library/system.net.icredentials.aspx).</span></span>
