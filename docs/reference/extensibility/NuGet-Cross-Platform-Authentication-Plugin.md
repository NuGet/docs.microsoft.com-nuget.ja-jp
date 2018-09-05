---
title: NuGet のクロス プラットフォーム認証プラグイン
description: NuGet.exe、dotnet.exe、msbuild.exe および Visual Studio の NuGet がプラットフォームの認証プラグインをクロスします。
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 1258ca4b30cb674c3832f12262940729438dd5b0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546635"
---
# <a name="nuget-cross-platform-authentication-plugin"></a><span data-ttu-id="cd361-103">NuGet のクロス プラットフォーム認証プラグイン</span><span class="sxs-lookup"><span data-stu-id="cd361-103">NuGet cross platform authentication plugin</span></span>

<span data-ttu-id="cd361-104">バージョン 4.8 以降、クライアント (NuGet.exe を Visual Studio、dotnet.exe、MSBuild.exe) は、上に構築された認証プラグインを使用できるすべての NuGet で、[クロス プラットフォーム プラグイン NuGet](NuGet-Cross-Platform-Plugins.md)モデル。</span><span class="sxs-lookup"><span data-stu-id="cd361-104">In version 4.8+, all NuGet clients (NuGet.exe, Visual Studio, dotnet.exe and MSBuild.exe) can use an authentication plugin built on top of the [NuGet cross platform plugins](NuGet-Cross-Platform-Plugins.md) model.</span></span>

## <a name="authentication-in-dotnetexe"></a><span data-ttu-id="cd361-105">Dotnet.exe の認証</span><span class="sxs-lookup"><span data-stu-id="cd361-105">Authentication in dotnet.exe</span></span>

<span data-ttu-id="cd361-106">Visual Studio と NuGet.exe は、対話型の既定では。</span><span class="sxs-lookup"><span data-stu-id="cd361-106">Visual Studio and NuGet.exe are by default interactive.</span></span> <span data-ttu-id="cd361-107">NuGet.exe にはようにするためのスイッチが含まれています[非対話型](../../tools/nuget-exe-CLI-Reference.md)します。</span><span class="sxs-lookup"><span data-stu-id="cd361-107">NuGet.exe contains a switch to make it [non interactive](../../tools/nuget-exe-CLI-Reference.md).</span></span>
<span data-ttu-id="cd361-108">さらに、NuGet.exe および Visual Studio のプラグインは、ユーザーに入力を求めます。</span><span class="sxs-lookup"><span data-stu-id="cd361-108">Additionally the NuGet.exe and Visual Studio plugins prompt the user for input.</span></span>
<span data-ttu-id="cd361-109">Dotnet.exe のない入力を求めると、既定値は非対話型です。</span><span class="sxs-lookup"><span data-stu-id="cd361-109">In dotnet.exe there is no prompting and the default is non interactive.</span></span>

<span data-ttu-id="cd361-110">Dotnet.exe での認証メカニズムでは、デバイスのフローです。</span><span class="sxs-lookup"><span data-stu-id="cd361-110">The authentication mechanism in dotnet.exe is device flow.</span></span> <span data-ttu-id="cd361-111">ときに、復元またはパッケージの操作は、操作がブロックと指示する方法を完全な認証ことが、コマンドラインでユーザーに対話的に実行を追加します。</span><span class="sxs-lookup"><span data-stu-id="cd361-111">When the restore or add package operation is run interactively, the operation blocks and instructions to the user how to complete the authentications will be provided on the command line.</span></span>
<span data-ttu-id="cd361-112">ユーザーが認証を完了すると、操作を続行します。</span><span class="sxs-lookup"><span data-stu-id="cd361-112">When the user completes the authentication the operation will continue.</span></span>

<span data-ttu-id="cd361-113">操作を対話型にするために、1 つ渡す必要があります`--interactive`します。</span><span class="sxs-lookup"><span data-stu-id="cd361-113">To make the operation interactive, one should pass `--interactive`.</span></span>
<span data-ttu-id="cd361-114">現在のみ明示的な`dotnet restore`と`dotnet add package`コマンドは、対話型のスイッチをサポートします。</span><span class="sxs-lookup"><span data-stu-id="cd361-114">Currently only the explicit `dotnet restore` and `dotnet add package` commands support an interactive switch.</span></span>
<span data-ttu-id="cd361-115">対話型のスイッチがない`dotnet build`と`dotnet publish`します。</span><span class="sxs-lookup"><span data-stu-id="cd361-115">There is no interactive switch on `dotnet build` and `dotnet publish`.</span></span>

## <a name="authentication-in-msbuild"></a><span data-ttu-id="cd361-116">MSBuild での認証</span><span class="sxs-lookup"><span data-stu-id="cd361-116">Authentication in MSBuild</span></span>

<span data-ttu-id="cd361-117">Dotnet.exe と同様に、MSBuild.exe が既定で非対話型 MSBuild.exe の認証メカニズムはデバイスのフローです。</span><span class="sxs-lookup"><span data-stu-id="cd361-117">Similar to dotnet.exe, MSBuild.exe is by default non interactive the MSBuild.exe authentication mechanism is device flow.</span></span>
<span data-ttu-id="cd361-118">一時停止し、認証を待つ復元できるように、復元を呼び出す`msbuild /t:restore /p:NuGetInteractive="true"`します。</span><span class="sxs-lookup"><span data-stu-id="cd361-118">To allow the restore to pause and wait for authentication, call restore with `msbuild /t:restore /p:NuGetInteractive="true"`.</span></span>

## <a name="creating-a-cross-platform-authentication-plugin"></a><span data-ttu-id="cd361-119">クロス プラットフォーム認証プラグインを作成します。</span><span class="sxs-lookup"><span data-stu-id="cd361-119">Creating a cross platform authentication plugin</span></span>

<span data-ttu-id="cd361-120">実装のサンプルが記載[MSCredProvider プラグイン](https://github.com/Microsoft/mscredprovider)します。</span><span class="sxs-lookup"><span data-stu-id="cd361-120">A sample implementation can be found in [MSCredProvider plugin](https://github.com/Microsoft/mscredprovider).</span></span>

<span data-ttu-id="cd361-121">プラグインは、NuGet クライアント ツールによって設定されたセキュリティ要件に準拠していることが非常に重要です。</span><span class="sxs-lookup"><span data-stu-id="cd361-121">It's very important that the plugins conforms to the security requirements set forth by the NuGet client tools.</span></span>
<span data-ttu-id="cd361-122">最低限必要な認証プラグインを使用するプラグイン バージョンは*2.0.0*します。</span><span class="sxs-lookup"><span data-stu-id="cd361-122">The minimum required version for a plugin to be an authentication plugin is *2.0.0*.</span></span>
<span data-ttu-id="cd361-123">NuGet はサポートされている操作の信頼性情報と、プラグインとクエリのハンドシェイクを実行します。</span><span class="sxs-lookup"><span data-stu-id="cd361-123">NuGet will perform the handshake with the plugin and query for the supported operation claims.</span></span>
<span data-ttu-id="cd361-124">クロス プラットフォームのプラグインの NuGet を参照してください[プロトコル メッセージ](NuGet-Cross-Platform-Plugins.md#protocol-messages-index)特定のメッセージの詳細についてはします。</span><span class="sxs-lookup"><span data-stu-id="cd361-124">Please refer to the NuGet cross platform plugin [protocol messages](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) for more details about the specific messages.</span></span>

<span data-ttu-id="cd361-125">NuGet はログ レベルを設定し、該当する場合、プラグインにプロキシ情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="cd361-125">NuGet will set the log level and provide proxy information to the plugin when applicable.</span></span>
<span data-ttu-id="cd361-126">NuGet へのログ記録コンソールはのみ許容可能な NuGet がプラグインにログ レベルを設定後します。</span><span class="sxs-lookup"><span data-stu-id="cd361-126">Logging to the NuGet console is only acceptable after NuGet has set the log level to the plugin.</span></span>

- <span data-ttu-id="cd361-127">.NET framework プラグインの認証の動作</span><span class="sxs-lookup"><span data-stu-id="cd361-127">.NET Framework plugin authentication behavior</span></span>

<span data-ttu-id="cd361-128">.NET framework、プラグインは、ダイアログ ボックスの形式での入力をユーザーに求めるが許可されます。</span><span class="sxs-lookup"><span data-stu-id="cd361-128">In .NET Framework, the plugins are allowed to prompt a user for input, in the form of a dialog.</span></span>

- <span data-ttu-id="cd361-129">.NET core プラグインの認証の動作</span><span class="sxs-lookup"><span data-stu-id="cd361-129">.NET Core plugin authentication behavior</span></span>

<span data-ttu-id="cd361-130">.NET Core では、ダイアログを表示することはできません。</span><span class="sxs-lookup"><span data-stu-id="cd361-130">In .NET Core, a dialog cannot be shown.</span></span> <span data-ttu-id="cd361-131">プラグインは、認証にデバイスのフローを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd361-131">The plugins should use device flow to authenticate.</span></span>
<span data-ttu-id="cd361-132">プラグインは、ユーザーに指示を NuGet にログ メッセージを送信できます。</span><span class="sxs-lookup"><span data-stu-id="cd361-132">The plugin can send log messages to NuGet with instructions to the user.</span></span>
<span data-ttu-id="cd361-133">ログ レベルが、プラグインを設定した後のログ記録が使用できることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="cd361-133">Note that logging is available after the log level has been set to the plugin.</span></span>
<span data-ttu-id="cd361-134">NuGet では、コマンドラインから対話型の入力は実行されません。</span><span class="sxs-lookup"><span data-stu-id="cd361-134">NuGet will not take any interactive input from the command line.</span></span>

<span data-ttu-id="cd361-135">クライアントが取得の認証資格情報を使ってプラグインを呼び出すと、プラグインは対話機能のスイッチに準拠しているし、ダイアログのスイッチを尊重する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd361-135">When the client calls the plugin with a Get Authentication Credentials, the plugins need to conform to the interactivity switch and respect the dialog switch.</span></span> 

<span data-ttu-id="cd361-136">次の表では、すべての組み合わせに対して、プラグインの動作方法を示します。</span><span class="sxs-lookup"><span data-stu-id="cd361-136">The following table summarizes how the plugin should behave for all combinations.</span></span>

| <span data-ttu-id="cd361-137">IsNonInteractive</span><span class="sxs-lookup"><span data-stu-id="cd361-137">IsNonInteractive</span></span> | <span data-ttu-id="cd361-138">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="cd361-138">CanShowDialog</span></span> | <span data-ttu-id="cd361-139">プラグインの動作</span><span class="sxs-lookup"><span data-stu-id="cd361-139">Plugin behavior</span></span> |
| ---------------- | ------------- | --------------- |
| <span data-ttu-id="cd361-140">true</span><span class="sxs-lookup"><span data-stu-id="cd361-140">true</span></span> | <span data-ttu-id="cd361-141">true</span><span class="sxs-lookup"><span data-stu-id="cd361-141">true</span></span> | <span data-ttu-id="cd361-142">IsNonInteractive スイッチは、ダイアログのスイッチよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="cd361-142">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="cd361-143">ダイアログ ボックスをポップアップ表示には、プラグインすることはできません。</span><span class="sxs-lookup"><span data-stu-id="cd361-143">The plugin is not allowed to pop a dialog.</span></span> <span data-ttu-id="cd361-144">この組み合わせは .NET Framework のプラグインの有効なのみ</span><span class="sxs-lookup"><span data-stu-id="cd361-144">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="cd361-145">true</span><span class="sxs-lookup"><span data-stu-id="cd361-145">true</span></span> | <span data-ttu-id="cd361-146">False</span><span class="sxs-lookup"><span data-stu-id="cd361-146">false</span></span> | <span data-ttu-id="cd361-147">IsNonInteractive スイッチは、ダイアログのスイッチよりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="cd361-147">The IsNonInteractive switch takes precedence over the dialog switch.</span></span> <span data-ttu-id="cd361-148">ブロックには、プラグインすることはできません。</span><span class="sxs-lookup"><span data-stu-id="cd361-148">The plugin is not allowed to block.</span></span> <span data-ttu-id="cd361-149">この組み合わせは、.NET コア プラグインの有効なのみ</span><span class="sxs-lookup"><span data-stu-id="cd361-149">This combination is only valid for .NET Core plugins</span></span> |
| <span data-ttu-id="cd361-150">False</span><span class="sxs-lookup"><span data-stu-id="cd361-150">false</span></span> | <span data-ttu-id="cd361-151">true</span><span class="sxs-lookup"><span data-stu-id="cd361-151">true</span></span> | <span data-ttu-id="cd361-152">プラグインは、ダイアログ ボックスを表示する必要があります。</span><span class="sxs-lookup"><span data-stu-id="cd361-152">The plugin should show a dialog.</span></span> <span data-ttu-id="cd361-153">この組み合わせは .NET Framework のプラグインの有効なのみ</span><span class="sxs-lookup"><span data-stu-id="cd361-153">This combination is only valid for .NET Framework plugins</span></span> |
| <span data-ttu-id="cd361-154">False</span><span class="sxs-lookup"><span data-stu-id="cd361-154">false</span></span> | <span data-ttu-id="cd361-155">False</span><span class="sxs-lookup"><span data-stu-id="cd361-155">false</span></span> | <span data-ttu-id="cd361-156">プラグインする必要があります/ことに、ダイアログを表示されません。</span><span class="sxs-lookup"><span data-stu-id="cd361-156">The plugin should/can not show a dialog.</span></span> <span data-ttu-id="cd361-157">プラグインは、命令メッセージ ロガーを使用してログに記録して認証するデバイスのフローを使用してください。</span><span class="sxs-lookup"><span data-stu-id="cd361-157">The plugin should use device flow to authenticate by logging an instruction message via the logger.</span></span> <span data-ttu-id="cd361-158">この組み合わせは、.NET コア プラグインの有効なのみ</span><span class="sxs-lookup"><span data-stu-id="cd361-158">This combination is only valid for .NET Core plugins</span></span> |

<span data-ttu-id="cd361-159">プラグインを記述する前に、次の仕様を参照してください。</span><span class="sxs-lookup"><span data-stu-id="cd361-159">Please refer to the following specs before writing a plugin.</span></span>

- [<span data-ttu-id="cd361-160">NuGet パッケージのダウンロードのプラグイン</span><span class="sxs-lookup"><span data-stu-id="cd361-160">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="cd361-161">フォーム認証のプラグイン相互の NuGet</span><span class="sxs-lookup"><span data-stu-id="cd361-161">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
