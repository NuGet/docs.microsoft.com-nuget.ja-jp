---
title: NuGet のクロス プラットフォーム認証プラグイン
description: Nuget.exe、dotnet、msbuild.exe、および Visual Studio 用の NuGet クロスプラットフォーム認証プラグイン
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317278"
---
# <a name="nuget-cross-platform-authentication-plugin"></a><span data-ttu-id="7aa72-103">NuGet のクロス プラットフォーム認証プラグイン</span><span class="sxs-lookup"><span data-stu-id="7aa72-103">NuGet cross platform authentication plugin</span></span>

<span data-ttu-id="7aa72-104">バージョン4.8 以降では、すべての NuGet クライアント (Nuget.exe、Visual Studio、dotnet、および Msbuild.exe) は、 [nuget クロスプラットフォームプラグイン](NuGet-Cross-Platform-Plugins.md)モデル上に構築された認証プラグインを使用できます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-104">In version 4.8+, all NuGet clients (NuGet.exe, Visual Studio, dotnet.exe and MSBuild.exe) can use an authentication plugin built on top of the [NuGet cross platform plugins](NuGet-Cross-Platform-Plugins.md) model.</span></span>

## <a name="authentication-in-dotnetexe"></a><span data-ttu-id="7aa72-105">Dotnet での認証</span><span class="sxs-lookup"><span data-stu-id="7aa72-105">Authentication in dotnet.exe</span></span>

<span data-ttu-id="7aa72-106">既定では、Visual Studio と Nuget.exe は対話型です。</span><span class="sxs-lookup"><span data-stu-id="7aa72-106">Visual Studio and NuGet.exe are by default interactive.</span></span> <span data-ttu-id="7aa72-107">Nuget.exe には、対話型になら[ない](../nuget-exe-CLI-Reference.md)ようにするスイッチが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7aa72-107">NuGet.exe contains a switch to make it [non interactive](../nuget-exe-CLI-Reference.md).</span></span>
<span data-ttu-id="7aa72-108">さらに、Nuget.exe および Visual Studio プラグインによって、ユーザーに入力を求めるプロンプトが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-108">Additionally the NuGet.exe and Visual Studio plugins prompt the user for input.</span></span>
<span data-ttu-id="7aa72-109">Dotnet では、プロンプトは表示されず、既定値は非対話型です。</span><span class="sxs-lookup"><span data-stu-id="7aa72-109">In dotnet.exe there is no prompting and the default is non interactive.</span></span>

<span data-ttu-id="7aa72-110">Dotnet の認証メカニズムはデバイスフローです。</span><span class="sxs-lookup"><span data-stu-id="7aa72-110">The authentication mechanism in dotnet.exe is device flow.</span></span> <span data-ttu-id="7aa72-111">復元またはパッケージの追加操作を対話的に実行すると、認証を完了するための操作ブロックとユーザーへの指示がコマンドラインに表示されます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-111">When the restore or add package operation is run interactively, the operation blocks and instructions to the user how to complete the authentications will be provided on the command line.</span></span>
<span data-ttu-id="7aa72-112">ユーザーが認証を完了すると、操作は続行されます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-112">When the user completes the authentication the operation will continue.</span></span>

<span data-ttu-id="7aa72-113">操作を対話形式にするには、 `--interactive`1 つを渡す必要があります。</span><span class="sxs-lookup"><span data-stu-id="7aa72-113">To make the operation interactive, one should pass `--interactive`.</span></span>
<span data-ttu-id="7aa72-114">現時点では、 `dotnet restore`明示`dotnet add package`的なコマンドとコマンドのみが対話型スイッチをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="7aa72-114">Currently only the explicit `dotnet restore` and `dotnet add package` commands support an interactive switch.</span></span>
<span data-ttu-id="7aa72-115">`dotnet build` と`dotnet publish`には対話型スイッチがありません。</span><span class="sxs-lookup"><span data-stu-id="7aa72-115">There is no interactive switch on `dotnet build` and `dotnet publish`.</span></span>

## <a name="authentication-in-msbuild"></a><span data-ttu-id="7aa72-116">MSBuild での認証</span><span class="sxs-lookup"><span data-stu-id="7aa72-116">Authentication in MSBuild</span></span>

<span data-ttu-id="7aa72-117">Dotnet と同様に、Msbuild.exe は既定で非対話型になります。 Msbuild.exe の認証メカニズムはデバイスフローです。</span><span class="sxs-lookup"><span data-stu-id="7aa72-117">Similar to dotnet.exe, MSBuild.exe is by default non interactive the MSBuild.exe authentication mechanism is device flow.</span></span>
<span data-ttu-id="7aa72-118">復元を一時停止して認証を待機させるには、 `msbuild -t:restore -p:NuGetInteractive="true"`を使用して restore を呼び出します。</span><span class="sxs-lookup"><span data-stu-id="7aa72-118">To allow the restore to pause and wait for authentication, call restore with `msbuild -t:restore -p:NuGetInteractive="true"`.</span></span>

## <a name="creating-a-cross-platform-authentication-plugin"></a><span data-ttu-id="7aa72-119">クロスプラットフォーム認証プラグインを作成する</span><span class="sxs-lookup"><span data-stu-id="7aa72-119">Creating a cross platform authentication plugin</span></span>

<span data-ttu-id="7aa72-120">サンプルの実装については、「 [Microsoft Credential Provider plugin](https://github.com/Microsoft/artifacts-credprovider)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7aa72-120">A sample implementation can be found in [Microsoft Credential Provider plugin](https://github.com/Microsoft/artifacts-credprovider).</span></span>

<span data-ttu-id="7aa72-121">プラグインは、NuGet クライアントツールによって設定されたセキュリティ要件に準拠していることが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="7aa72-121">It's very important that the plugins conforms to the security requirements set forth by the NuGet client tools.</span></span>
<span data-ttu-id="7aa72-122">プラグインを認証プラグインとして使用するために必要な最小バージョンは*2.0.0*です。</span><span class="sxs-lookup"><span data-stu-id="7aa72-122">The minimum required version for a plugin to be an authentication plugin is *2.0.0*.</span></span>
<span data-ttu-id="7aa72-123">NuGet は、サポートされている操作要求に対して、プラグインとクエリを使用してハンドシェイクを実行します。</span><span class="sxs-lookup"><span data-stu-id="7aa72-123">NuGet will perform the handshake with the plugin and query for the supported operation claims.</span></span>
<span data-ttu-id="7aa72-124">特定のメッセージの詳細については、NuGet クロスプラットフォームプラグイン[プロトコルメッセージ](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7aa72-124">Please refer to the NuGet cross platform plugin [protocol messages](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) for more details about the specific messages.</span></span>

<span data-ttu-id="7aa72-125">NuGet はログレベルを設定し、必要に応じてプロキシ情報をプラグインに提供します。</span><span class="sxs-lookup"><span data-stu-id="7aa72-125">NuGet will set the log level and provide proxy information to the plugin when applicable.</span></span>
<span data-ttu-id="7aa72-126">Nuget コンソールへのログ記録は、NuGet がログレベルをプラグインに設定した後でのみ許容されます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-126">Logging to the NuGet console is only acceptable after NuGet has set the log level to the plugin.</span></span>

- <span data-ttu-id="7aa72-127">.NET Framework プラグインの認証動作</span><span class="sxs-lookup"><span data-stu-id="7aa72-127">.NET Framework plugin authentication behavior</span></span>

<span data-ttu-id="7aa72-128">.NET Framework では、プラグインは、ダイアログの形式でユーザーに入力を求めることができます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-128">In .NET Framework, the plugins are allowed to prompt a user for input, in the form of a dialog.</span></span>

- <span data-ttu-id="7aa72-129">.NET Core プラグインの認証動作</span><span class="sxs-lookup"><span data-stu-id="7aa72-129">.NET Core plugin authentication behavior</span></span>

<span data-ttu-id="7aa72-130">.NET Core では、ダイアログを表示できません。</span><span class="sxs-lookup"><span data-stu-id="7aa72-130">In .NET Core, a dialog cannot be shown.</span></span> <span data-ttu-id="7aa72-131">プラグインは、デバイスフローを使用して認証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7aa72-131">The plugins should use device flow to authenticate.</span></span>
<span data-ttu-id="7aa72-132">プラグインは、ユーザーへの指示と共にログメッセージを NuGet に送信できます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-132">The plugin can send log messages to NuGet with instructions to the user.</span></span>
<span data-ttu-id="7aa72-133">ログレベルがプラグインに設定されている場合は、ログ記録が使用可能であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="7aa72-133">Note that logging is available after the log level has been set to the plugin.</span></span>
<span data-ttu-id="7aa72-134">NuGet は、コマンドラインから対話型の入力を受け取りません。</span><span class="sxs-lookup"><span data-stu-id="7aa72-134">NuGet will not take any interactive input from the command line.</span></span>

<span data-ttu-id="7aa72-135">クライアントが Get 認証資格情報を使用してプラグインを呼び出す場合、プラグインは対話スイッチに準拠し、ダイアログスイッチを尊重する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7aa72-135">When the client calls the plugin with a Get Authentication Credentials, the plugins need to conform to the interactivity switch and respect the dialog switch.</span></span> 

<span data-ttu-id="7aa72-136">次の表は、すべての組み合わせに対してプラグインがどのように動作するかをまとめたものです。</span><span class="sxs-lookup"><span data-stu-id="7aa72-136">The following table summarizes how the plugin should behave for all combinations.</span></span>

| <span data-ttu-id="7aa72-137">IsNonInteractive 型</span><span class="sxs-lookup"><span data-stu-id="7aa72-137">IsNonInteractive</span></span> | <span data-ttu-id="7aa72-138">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="7aa72-138">CanShowDialog</span></span> | <span data-ttu-id="7aa72-139">プラグインの動作</span><span class="sxs-lookup"><span data-stu-id="7aa72-139">Plugin behavior</span></span> |
| ---------------- | ------------- | --------------- |
| <span data-ttu-id="7aa72-140">true</span><span class="sxs-lookup"><span data-stu-id="7aa72-140">true</span></span> | <span data-ttu-id="7aa72-141">true</span><span class="sxs-lookup"><span data-stu-id="7aa72-141">true</span></span> | <span data-ttu-id="7aa72-142">IsNonInteractive スイッチは、ダイアログスイッチよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-142">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="7aa72-143">プラグインは、ダイアログをポップすることが許可されていません。</span><span class="sxs-lookup"><span data-stu-id="7aa72-143">The plugin is not allowed to pop a dialog.</span></span> <span data-ttu-id="7aa72-144">この組み合わせは .NET Framework プラグインに対してのみ有効です。</span><span class="sxs-lookup"><span data-stu-id="7aa72-144">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="7aa72-145">true</span><span class="sxs-lookup"><span data-stu-id="7aa72-145">true</span></span> | <span data-ttu-id="7aa72-146">False</span><span class="sxs-lookup"><span data-stu-id="7aa72-146">false</span></span> | <span data-ttu-id="7aa72-147">IsNonInteractive スイッチは、ダイアログスイッチよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-147">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="7aa72-148">プラグインをブロックすることはできません。</span><span class="sxs-lookup"><span data-stu-id="7aa72-148">The plugin is not allowed to block.</span></span> <span data-ttu-id="7aa72-149">この組み合わせは、.NET Core プラグインに対してのみ有効です。</span><span class="sxs-lookup"><span data-stu-id="7aa72-149">This combination is only valid for .NET Core plugins</span></span> |
| <span data-ttu-id="7aa72-150">False</span><span class="sxs-lookup"><span data-stu-id="7aa72-150">false</span></span> | <span data-ttu-id="7aa72-151">true</span><span class="sxs-lookup"><span data-stu-id="7aa72-151">true</span></span> | <span data-ttu-id="7aa72-152">プラグインにダイアログが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7aa72-152">The plugin should show a dialog.</span></span> <span data-ttu-id="7aa72-153">この組み合わせは .NET Framework プラグインに対してのみ有効です。</span><span class="sxs-lookup"><span data-stu-id="7aa72-153">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="7aa72-154">False</span><span class="sxs-lookup"><span data-stu-id="7aa72-154">false</span></span> | <span data-ttu-id="7aa72-155">False</span><span class="sxs-lookup"><span data-stu-id="7aa72-155">false</span></span> | <span data-ttu-id="7aa72-156">プラグインは、ダイアログを表示しないようにする必要があります。</span><span class="sxs-lookup"><span data-stu-id="7aa72-156">The plugin should/can not show a dialog.</span></span> <span data-ttu-id="7aa72-157">プラグインは、logger 経由で命令メッセージをログに記録することによって、デバイスフローを使用して認証する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7aa72-157">The plugin should use device flow to authenticate by logging an instruction message via the logger.</span></span> <span data-ttu-id="7aa72-158">この組み合わせは、.NET Core プラグインに対してのみ有効です。</span><span class="sxs-lookup"><span data-stu-id="7aa72-158">This combination is only valid for .NET Core plugins</span></span> |

<span data-ttu-id="7aa72-159">プラグインを作成する前に、次の仕様を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7aa72-159">Please refer to the following specs before writing a plugin.</span></span>

- [<span data-ttu-id="7aa72-160">NuGet パッケージのダウンロードプラグイン</span><span class="sxs-lookup"><span data-stu-id="7aa72-160">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="7aa72-161">NuGet のクロスプラットフォーム認証プラグイン</span><span class="sxs-lookup"><span data-stu-id="7aa72-161">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
