---
title: Visual Studio 向け NuGet 資格情報プロバイダー
description: NuGet 資格情報プロバイダーは、Visual Studio 拡張機能で IVsCredentialProvider インターフェイスを実装することによって、フィードで認証を行います。
author: karann-msft
ms.author: karann
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: 4e781a2462871bceeb1c7f02220320daabdab98a
ms.sourcegitcommit: a0807671386782021acb7588741390e6f07e94e1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/05/2019
ms.locfileid: "70384429"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="2c138-103">NuGet 資格情報プロバイダーを使用した Visual Studio でのフィードの認証</span><span class="sxs-lookup"><span data-stu-id="2c138-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="2c138-104">NuGet Visual Studio 拡張機能3.6 以降では、認証済みのフィードを NuGet で使用できるようにする資格情報プロバイダーがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="2c138-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="2c138-105">Visual Studio の NuGet 資格情報プロバイダーをインストールすると、NuGet Visual Studio 拡張機能は、認証されたフィードの資格情報を必要に応じて自動的に取得して更新します。</span><span class="sxs-lookup"><span data-stu-id="2c138-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="2c138-106">サンプルの実装については[、VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2c138-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="2c138-107">Visual Studio の 4.8 + NuGet 以降では、新しいクロスプラットフォーム認証プラグインもサポートされていますが、パフォーマンス上の理由から推奨される方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="2c138-107">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="2c138-108">Visual Studio の NuGet 資格情報プロバイダーは、通常の Visual Studio 拡張機能としてインストールする必要があり、 [Visual studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe)以降が必要になります。</span><span class="sxs-lookup"><span data-stu-id="2c138-108">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](http://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="2c138-109">Visual Studio の NuGet 資格情報プロバイダーは、(dotnet restore または nuget.exe ではなく) Visual Studio でのみ動作します。</span><span class="sxs-lookup"><span data-stu-id="2c138-109">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="2c138-110">Nuget.exe の資格情報プロバイダーについては、「 [Nuget.exe 資格情報プロバイダー](nuget-exe-Credential-providers.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2c138-110">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="2c138-111">Dotnet と msbuild の資格情報プロバイダーについては、「 [NuGet クロスプラットフォームプラグイン](nuget-cross-platform-authentication-plugin.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2c138-111">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="available-nuget-credential-providers-for-visual-studio"></a><span data-ttu-id="2c138-112">Visual Studio の利用可能な NuGet 資格情報プロバイダー</span><span class="sxs-lookup"><span data-stu-id="2c138-112">Available NuGet credential providers for Visual Studio</span></span>

<span data-ttu-id="2c138-113">Visual Studio Team Services をサポートするために、Visual Studio NuGet 拡張機能に組み込まれている資格情報プロバイダーがあります。</span><span class="sxs-lookup"><span data-stu-id="2c138-113">There is a credential provider built into the Visual Studio NuGet extension to support Visual Studio Team Services.</span></span>

<span data-ttu-id="2c138-114">NuGet Visual Studio 拡張機能は内部`VsCredentialProviderImporter`を使用します。これはプラグイン資格情報プロバイダーもスキャンします。</span><span class="sxs-lookup"><span data-stu-id="2c138-114">The NuGet Visual Studio Extension uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="2c138-115">これらのプラグイン資格情報プロバイダーは、型`IVsCredentialProvider`の MEF エクスポートとして検出可能である必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c138-115">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="2c138-116">利用可能なプラグイン資格情報プロバイダーは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="2c138-116">Available plug-in credential providers include:</span></span>

- [<span data-ttu-id="2c138-117">Visual Studio の MyGet Credential Provider</span><span class="sxs-lookup"><span data-stu-id="2c138-117">MyGet Credential Provider for Visual Studio</span></span>](http://docs.myget.org/docs/reference/credential-provider-for-visual-studio)

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="2c138-118">Visual Studio の NuGet 資格情報プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="2c138-118">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="2c138-119">NuGet Visual Studio 拡張機能3.6 以降では、資格情報の取得に使用される内部 CredentialService が実装されています。</span><span class="sxs-lookup"><span data-stu-id="2c138-119">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="2c138-120">CredentialService には、組み込みおよびプラグインの資格情報プロバイダーの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="2c138-120">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="2c138-121">各プロバイダーは、資格情報が取得されるまで順番に試行されます。</span><span class="sxs-lookup"><span data-stu-id="2c138-121">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="2c138-122">資格情報の取得中、資格情報サービスは次の順序で資格情報プロバイダーを試行し、資格情報が取得されるとすぐに停止します。</span><span class="sxs-lookup"><span data-stu-id="2c138-122">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="2c138-123">資格情報は、(組み込み`SettingsCredentialProvider`のを使用して) NuGet 構成ファイルからフェッチされます。</span><span class="sxs-lookup"><span data-stu-id="2c138-123">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="2c138-124">パッケージソースが Visual Studio Team Services にある場合は、 `VisualStudioAccountProvider`が使用されます。</span><span class="sxs-lookup"><span data-stu-id="2c138-124">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="2c138-125">その他のすべてのプラグイン Visual Studio 資格情報プロバイダーは、順番に試行されます。</span><span class="sxs-lookup"><span data-stu-id="2c138-125">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="2c138-126">すべての NuGet クロスプラットフォーム資格情報プロバイダーを順番に使用してください。</span><span class="sxs-lookup"><span data-stu-id="2c138-126">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="2c138-127">資格情報がまだ取得されていない場合、ユーザーは標準の基本認証ダイアログを使用して資格情報の入力を求められます。</span><span class="sxs-lookup"><span data-stu-id="2c138-127">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="2c138-128">IVsCredentialProvider を実装しています。 GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="2c138-128">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="2c138-129">Visual studio の NuGet 資格情報プロバイダーを作成するには、 `IVsCredentialProvider`型を実装するパブリック MEF エクスポートを公開する visual studio 拡張機能を作成し、次に示す原則に従います。</span><span class="sxs-lookup"><span data-stu-id="2c138-129">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="2c138-130">サンプルの実装については[、VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2c138-130">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="2c138-131">Visual Studio の各 NuGet 資格情報プロバイダーは、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c138-131">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="2c138-132">資格情報の取得を開始する前に、対象の URI の資格情報を提供できるかどうかを判断します。</span><span class="sxs-lookup"><span data-stu-id="2c138-132">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="2c138-133">プロバイダーが対象のソースの資格情報を提供できない場合は、 `null`を返します。</span><span class="sxs-lookup"><span data-stu-id="2c138-133">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="2c138-134">プロバイダーが対象 URI の要求を処理するが、資格情報を提供できない場合は、例外をスローする必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c138-134">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="2c138-135">Visual Studio のカスタム nuget 資格情報プロバイダーは、 `IVsCredentialProvider` [VisualStudio パッケージ](https://www.nuget.org/packages/NuGet.VisualStudio/)で使用可能なインターフェイスを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c138-135">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="2c138-136">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="2c138-136">GetCredentialAsync</span></span>

| <span data-ttu-id="2c138-137">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="2c138-137">Input Parameter</span></span> |<span data-ttu-id="2c138-138">説明</span><span class="sxs-lookup"><span data-stu-id="2c138-138">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="2c138-139">Uri uri</span><span class="sxs-lookup"><span data-stu-id="2c138-139">Uri uri</span></span> | <span data-ttu-id="2c138-140">資格情報が要求されているパッケージソース Uri。</span><span class="sxs-lookup"><span data-stu-id="2c138-140">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="2c138-141">IWebProxy プロキシ</span><span class="sxs-lookup"><span data-stu-id="2c138-141">IWebProxy proxy</span></span> | <span data-ttu-id="2c138-142">ネットワーク上で通信するときに使用する Web プロキシ。</span><span class="sxs-lookup"><span data-stu-id="2c138-142">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="2c138-143">プロキシ認証が構成されていない場合は Null です。</span><span class="sxs-lookup"><span data-stu-id="2c138-143">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="2c138-144">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="2c138-144">bool isProxyRequest</span></span> | <span data-ttu-id="2c138-145">この要求がプロキシ認証資格情報を取得する場合は True。</span><span class="sxs-lookup"><span data-stu-id="2c138-145">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="2c138-146">実装がプロキシ資格情報の取得に対して有効でない場合は、null が返されます。</span><span class="sxs-lookup"><span data-stu-id="2c138-146">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="2c138-147">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="2c138-147">bool isRetry</span></span> | <span data-ttu-id="2c138-148">この Uri に対して資格情報が以前に要求されていたが、指定された資格情報が承認済みアクセスを許可していない場合は True。</span><span class="sxs-lookup"><span data-stu-id="2c138-148">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="2c138-149">bool 非対話型</span><span class="sxs-lookup"><span data-stu-id="2c138-149">bool nonInteractive</span></span> | <span data-ttu-id="2c138-150">True の場合、資格情報プロバイダーはすべてのユーザープロンプトを非表示にし、代わりに既定値を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c138-150">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="2c138-151">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="2c138-151">CancellationToken cancellationToken</span></span> | <span data-ttu-id="2c138-152">資格情報を要求している操作が取り消されたかどうかを確認するには、このキャンセルトークンを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="2c138-152">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="2c138-153">**戻り値**:[ `System.Net.ICredentials`インターフェイス](/dotnet/api/system.net.icredentials?view=netstandard-2.0)を実装する資格情報オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="2c138-153">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
