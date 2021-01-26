---
title: Visual Studio 向け NuGet 資格情報プロバイダー
description: NuGet 資格情報プロバイダーは、Visual Studio 拡張機能で IVsCredentialProvider インターフェイスを実装することによって、フィードで認証を行います。
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2017
ms.topic: conceptual
ms.openlocfilehash: f324f1e27e0d718571525152fcf16b55b900dbaa
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777759"
---
# <a name="authenticating-feeds-in-visual-studio-with-nuget-credential-providers"></a><span data-ttu-id="f6d5d-103">NuGet 資格情報プロバイダーを使用した Visual Studio でのフィードの認証</span><span class="sxs-lookup"><span data-stu-id="f6d5d-103">Authenticating feeds in Visual Studio with NuGet credential providers</span></span>

<span data-ttu-id="f6d5d-104">NuGet Visual Studio 拡張機能3.6 以降では、認証済みのフィードを NuGet で使用できるようにする資格情報プロバイダーがサポートされています。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-104">The NuGet Visual Studio Extension 3.6+ supports credential providers, which enable NuGet to work with authenticated feeds.</span></span>
<span data-ttu-id="f6d5d-105">Visual Studio の NuGet 資格情報プロバイダーをインストールすると、NuGet Visual Studio 拡張機能は、認証されたフィードの資格情報を必要に応じて自動的に取得して更新します。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-105">After you install a NuGet credential provider for Visual Studio, the NuGet Visual Studio extension will automatically acquire and refresh credentials for authenticated feeds as necessary.</span></span>

<span data-ttu-id="f6d5d-106">サンプルの実装については [、VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-106">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="f6d5d-107">Visual Studio では、NuGet は内部 `VsCredentialProviderImporter` のを使用します。これはプラグイン資格情報プロバイダーもスキャンします。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-107">Within Visual Studio, NuGet uses an internal `VsCredentialProviderImporter` which also scans for plug-in credential providers.</span></span> <span data-ttu-id="f6d5d-108">これらのプラグイン資格情報プロバイダーは、型の MEF エクスポートとして検出可能である必要があり `IVsCredentialProvider` ます。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-108">These plug-in credential providers must be discoverable as a MEF Export of type `IVsCredentialProvider`.</span></span>

<span data-ttu-id="f6d5d-109">Visual Studio の 4.8 + NuGet 以降では、新しいクロスプラットフォーム認証プラグインもサポートされていますが、パフォーマンス上の理由から推奨される方法ではありません。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-109">Starting with 4.8+ NuGet in Visual Studio supports the new cross platform authentication plugins as well, but they are not the recommended approach for performance reasons.</span></span>

> [!Note]
> <span data-ttu-id="f6d5d-110">Visual Studio の NuGet 資格情報プロバイダーは、通常の Visual Studio 拡張機能としてインストールする必要があり、 [Visual studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) 以降が必要になります。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-110">NuGet credential providers for Visual Studio must be installed as a regular Visual Studio extension and will require [Visual Studio 2017](https://aka.ms/vs/15/release/vs_enterprise.exe) or above.</span></span>
>
> <span data-ttu-id="f6d5d-111">Visual Studio の NuGet 資格情報プロバイダーは、Visual Studio でのみ動作します (dotnet restore または nuget.exe では使用できません)。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-111">NuGet credential providers for Visual Studio work only in Visual Studio (not in dotnet restore or nuget.exe).</span></span> <span data-ttu-id="f6d5d-112">nuget.exe の資格情報プロバイダーについては、「 [nuget.exe 資格情報プロバイダー](nuget-exe-Credential-providers.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-112">For credential providers with nuget.exe, see [nuget.exe Credential Providers](nuget-exe-Credential-providers.md).</span></span>
> <span data-ttu-id="f6d5d-113">Dotnet と msbuild の資格情報プロバイダーについては、「 [NuGet クロスプラットフォームプラグイン](nuget-cross-platform-authentication-plugin.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-113">For credential providers in dotnet and msbuild see [NuGet cross platform plugins](nuget-cross-platform-authentication-plugin.md)</span></span>

## <a name="creating-a-nuget-credential-provider-for-visual-studio"></a><span data-ttu-id="f6d5d-114">Visual Studio の NuGet 資格情報プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="f6d5d-114">Creating a NuGet credential provider for Visual Studio</span></span>

<span data-ttu-id="f6d5d-115">NuGet Visual Studio 拡張機能3.6 以降では、資格情報の取得に使用される内部 CredentialService が実装されています。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-115">The NuGet Visual Studio Extension 3.6+ implements an internal CredentialService that is used to acquire credentials.</span></span> <span data-ttu-id="f6d5d-116">CredentialService には、組み込みおよびプラグインの資格情報プロバイダーの一覧があります。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-116">The CredentialService has a list of built-in and plug-in credential providers.</span></span> <span data-ttu-id="f6d5d-117">各プロバイダーは、資格情報が取得されるまで順番に試行されます。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-117">Each provider is tried sequentially until credentials are acquired.</span></span>

<span data-ttu-id="f6d5d-118">資格情報の取得中、資格情報サービスは次の順序で資格情報プロバイダーを試行し、資格情報が取得されるとすぐに停止します。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-118">During credential acquisition, the credential service will try credential providers in the following order, stopping as soon as credentials are acquired:</span></span>

1. <span data-ttu-id="f6d5d-119">資格情報は、(組み込みのを使用して) NuGet 構成ファイルからフェッチされ `SettingsCredentialProvider` ます。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-119">Credentials will be fetched from NuGet configuration files (using the built-in `SettingsCredentialProvider`).</span></span>
1. <span data-ttu-id="f6d5d-120">パッケージソースが Visual Studio Team Services にある場合は、が `VisualStudioAccountProvider` 使用されます。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-120">If the package source is on Visual Studio Team Services, the `VisualStudioAccountProvider` will be used.</span></span>
1. <span data-ttu-id="f6d5d-121">その他のすべてのプラグイン Visual Studio 資格情報プロバイダーは、順番に試行されます。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-121">All other plug-in Visual Studio credential providers will be tried sequentially.</span></span>
1. <span data-ttu-id="f6d5d-122">すべての NuGet クロスプラットフォーム資格情報プロバイダーを順番に使用してください。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-122">Try to use all NuGet cross platform credential providers sequentially.</span></span>
1. <span data-ttu-id="f6d5d-123">資格情報がまだ取得されていない場合、ユーザーは標準の基本認証ダイアログを使用して資格情報の入力を求められます。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-123">If no credentials have been acquired yet, the user will be prompted for credentials using a standard basic authentication dialog.</span></span>

### <a name="implementing-ivscredentialprovidergetcredentialsasync"></a><span data-ttu-id="f6d5d-124">IVsCredentialProvider を実装しています。 GetCredentialsAsync</span><span class="sxs-lookup"><span data-stu-id="f6d5d-124">Implementing IVsCredentialProvider.GetCredentialsAsync</span></span>

<span data-ttu-id="f6d5d-125">Visual Studio の NuGet 資格情報プロバイダーを作成するには、型を実装するパブリック MEF エクスポートを公開する Visual Studio 拡張機能を作成 `IVsCredentialProvider` し、次に示す原則に従います。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-125">To create a NuGet credential provider for Visual Studio, create a Visual Studio Extension that exposes a public MEF Export implementing the `IVsCredentialProvider` type, and adheres to the principles outlined below.</span></span>

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

<span data-ttu-id="f6d5d-126">サンプルの実装については [、VsCredentialProvider サンプル](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-126">A sample implementation can be found in [the VsCredentialProvider sample](https://github.com/NuGet/Samples/tree/master/VsCredentialProvider).</span></span>

<span data-ttu-id="f6d5d-127">Visual Studio の各 NuGet 資格情報プロバイダーは、次のことを行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-127">Each NuGet credential provider for Visual Studio must:</span></span>

1. <span data-ttu-id="f6d5d-128">資格情報の取得を開始する前に、対象の URI の資格情報を提供できるかどうかを判断します。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-128">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="f6d5d-129">プロバイダーが対象のソースの資格情報を提供できない場合は、を返し `null` ます。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-129">If the provider cannot supply credentials for the targeted source, then it should return `null`.</span></span>
1. <span data-ttu-id="f6d5d-130">プロバイダーが対象 URI の要求を処理するが、資格情報を提供できない場合は、例外をスローする必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-130">If the provider does handle requests for the targeted URI, but cannot supply credentials, an exception should be thrown.</span></span>

<span data-ttu-id="f6d5d-131">Visual Studio のカスタム NuGet 資格情報プロバイダーは、 `IVsCredentialProvider` [VisualStudio パッケージ](https://www.nuget.org/packages/NuGet.VisualStudio/)で使用可能なインターフェイスを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-131">A custom NuGet credential provider for Visual Studio must implement the `IVsCredentialProvider` interface available in the [NuGet.VisualStudio package](https://www.nuget.org/packages/NuGet.VisualStudio/).</span></span>

#### <a name="getcredentialasync"></a><span data-ttu-id="f6d5d-132">GetCredentialAsync</span><span class="sxs-lookup"><span data-stu-id="f6d5d-132">GetCredentialAsync</span></span>

| <span data-ttu-id="f6d5d-133">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="f6d5d-133">Input Parameter</span></span> |<span data-ttu-id="f6d5d-134">説明</span><span class="sxs-lookup"><span data-stu-id="f6d5d-134">Description</span></span>|
| ----------------|-----------|
| <span data-ttu-id="f6d5d-135">Uri uri</span><span class="sxs-lookup"><span data-stu-id="f6d5d-135">Uri uri</span></span> | <span data-ttu-id="f6d5d-136">資格情報が要求されているパッケージソース Uri。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-136">The package source Uri for which credentials are being requested.</span></span>|
| <span data-ttu-id="f6d5d-137">IWebProxy プロキシ</span><span class="sxs-lookup"><span data-stu-id="f6d5d-137">IWebProxy proxy</span></span> | <span data-ttu-id="f6d5d-138">ネットワーク上で通信するときに使用する Web プロキシ。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-138">Web proxy to use when communicating on the network.</span></span> <span data-ttu-id="f6d5d-139">プロキシ認証が構成されていない場合は Null です。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-139">Null if there is no proxy authentication configured.</span></span> |
| <span data-ttu-id="f6d5d-140">bool isProxyRequest</span><span class="sxs-lookup"><span data-stu-id="f6d5d-140">bool isProxyRequest</span></span> | <span data-ttu-id="f6d5d-141">この要求がプロキシ認証資格情報を取得する場合は True。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-141">True if this request is to get proxy authentication credentials.</span></span> <span data-ttu-id="f6d5d-142">実装がプロキシ資格情報の取得に対して有効でない場合は、null が返されます。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-142">If the implementation is not valid for acquiring proxy credentials, then null should be returned.</span></span> |
| <span data-ttu-id="f6d5d-143">bool isRetry</span><span class="sxs-lookup"><span data-stu-id="f6d5d-143">bool isRetry</span></span> | <span data-ttu-id="f6d5d-144">この Uri に対して資格情報が以前に要求されていたが、指定された資格情報が承認済みアクセスを許可していない場合は True。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-144">True if credentials were previously requested for this Uri, but the supplied credentials did not allow authorized access.</span></span> |
| <span data-ttu-id="f6d5d-145">bool 非対話型</span><span class="sxs-lookup"><span data-stu-id="f6d5d-145">bool nonInteractive</span></span> | <span data-ttu-id="f6d5d-146">True の場合、資格情報プロバイダーはすべてのユーザープロンプトを非表示にし、代わりに既定値を使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-146">If true, the credential provider must suppress all user prompts and use default values instead.</span></span> |
| <span data-ttu-id="f6d5d-147">CancellationToken cancellationToken</span><span class="sxs-lookup"><span data-stu-id="f6d5d-147">CancellationToken cancellationToken</span></span> | <span data-ttu-id="f6d5d-148">資格情報を要求している操作が取り消されたかどうかを確認するには、このキャンセルトークンを確認する必要があります。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-148">This cancellation token should be checked to determine if the operation requesting credentials has been cancelled.</span></span> |

<span data-ttu-id="f6d5d-149">**戻り値**: [ `System.Net.ICredentials` インターフェイス](/dotnet/api/system.net.icredentials?view=netstandard-2.0)を実装する資格情報オブジェクト。</span><span class="sxs-lookup"><span data-stu-id="f6d5d-149">**Return value**: A credentials object implementing the [`System.Net.ICredentials` interface](/dotnet/api/system.net.icredentials?view=netstandard-2.0).</span></span>
