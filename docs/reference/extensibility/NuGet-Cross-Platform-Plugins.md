---
title: NuGet クロスプラットフォームプラグイン
description: Nuget、dotnet、msbuild.exe、および Visual Studio 用の NuGet クロスプラットフォームプラグイン
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380494"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="c0ccf-103">NuGet クロスプラットフォームプラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="c0ccf-104">NuGet 4.8 以降では、クロスプラットフォームプラグインのサポートが追加されています。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="c0ccf-105">これは、新しいプラグイン拡張モデルを構築することで実現されました。これは、厳密な一連の操作規則に準拠する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="c0ccf-106">プラグインは自己完結型の実行可能ファイルであり、NuGet クライアントは別のプロセスで起動されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="c0ccf-107">これは、1回の書き込みで、すべてのプラグインを実行します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="c0ccf-108">これは、すべての NuGet クライアントツールで動作します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="c0ccf-109">プラグインには、.NET Framework (Nuget.exe、Msbuild.exe、Visual Studio)、または .NET Core (dotnet) のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="c0ccf-110">NuGet クライアントとプラグインの間のバージョン付き通信プロトコルが定義されています。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="c0ccf-111">スタートアップハンドシェイク中、2つのプロセスがプロトコルのバージョンをネゴシエートします。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="c0ccf-112">すべての NuGet クライアントツールのシナリオに対応するために、.NET Framework と .NET Core プラグインの両方が必要です。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="c0ccf-113">次に、プラグインのクライアントとフレームワークの組み合わせについて説明します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="c0ccf-114">クライアント ツール</span><span class="sxs-lookup"><span data-stu-id="c0ccf-114">Client tool</span></span>  | <span data-ttu-id="c0ccf-115">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="c0ccf-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="c0ccf-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c0ccf-116">Visual Studio</span></span> | <span data-ttu-id="c0ccf-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c0ccf-117">.NET Framework</span></span> |
| <span data-ttu-id="c0ccf-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="c0ccf-118">dotnet.exe</span></span> | <span data-ttu-id="c0ccf-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c0ccf-119">.NET Core</span></span> |
| <span data-ttu-id="c0ccf-120">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c0ccf-120">NuGet.exe</span></span> | <span data-ttu-id="c0ccf-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c0ccf-121">.NET Framework</span></span> |
| <span data-ttu-id="c0ccf-122">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="c0ccf-122">MSBuild.exe</span></span> | <span data-ttu-id="c0ccf-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c0ccf-123">.NET Framework</span></span> |
| <span data-ttu-id="c0ccf-124">Mono での Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="c0ccf-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="c0ccf-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c0ccf-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="c0ccf-126">動作のしくみ</span><span class="sxs-lookup"><span data-stu-id="c0ccf-126">How does it work</span></span>

<span data-ttu-id="c0ccf-127">高レベルのワークフローは、次のように記述できます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="c0ccf-128">NuGet は、使用可能なプラグインを検出します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="c0ccf-129">該当する場合、NuGet はプラグインを優先順位に従って繰り返し処理し、1つずつ開始します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="c0ccf-130">NuGet は、要求を処理できる最初のプラグインを使用します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="c0ccf-131">プラグインは、不要になったときにシャットダウンされます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="c0ccf-132">一般的なプラグインの要件</span><span class="sxs-lookup"><span data-stu-id="c0ccf-132">General plugin requirements</span></span>

<span data-ttu-id="c0ccf-133">現在のプロトコルバージョンは*2.0.0*です。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="c0ccf-134">このバージョンでは、次の要件があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="c0ccf-135">Windows と Mono で実行される、信頼された有効な Authenticode 署名アセンブリを用意します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="c0ccf-136">Linux および Mac でのアセンブリの実行には、特別な信頼要件はありません。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="c0ccf-137">関連する問題</span><span class="sxs-lookup"><span data-stu-id="c0ccf-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="c0ccf-138">NuGet クライアントツールの現在のセキュリティコンテキストでのステートレス起動をサポートします。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="c0ccf-139">たとえば、NuGet クライアントツールでは、後で説明するプラグインプロトコルの外部での昇格や追加の初期化は実行されません。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="c0ccf-140">明示的に指定されている場合を除き、非対話型にします。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="c0ccf-141">ネゴシエートされたプラグインプロトコルのバージョンに準拠します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="c0ccf-142">妥当な期間内にすべての要求に応答します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="c0ccf-143">進行中の操作のキャンセル要求を優先します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="c0ccf-144">技術仕様の詳細については、次の仕様を参照してください。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="c0ccf-145">NuGet パッケージのダウンロードプラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="c0ccf-146">NuGet のクロスプラットフォーム認証プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="c0ccf-147">クライアントとプラグインの相互作用</span><span class="sxs-lookup"><span data-stu-id="c0ccf-147">Client - Plugin interaction</span></span>

<span data-ttu-id="c0ccf-148">NuGet クライアントツールとプラグインは、標準ストリーム (stdin、stdout、stderr) を介して JSON と通信します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="c0ccf-149">すべてのデータは、UTF-8 でエンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="c0ccf-150">プラグインは、引数 "-Plugin" を使用して起動されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="c0ccf-151">ユーザーがこの引数を指定せずにプラグインの実行可能ファイルを直接起動した場合、プラグインは、プロトコルハンドシェイクを待機する代わりに、情報メッセージを提供できます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="c0ccf-152">プロトコルハンドシェイクタイムアウトは5秒です。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="c0ccf-153">プラグインは、できるだけ少ない量でセットアップを完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="c0ccf-154">NuGet クライアントツールは、NuGet ソースのサービスインデックスを渡すことによって、プラグインのサポートされている操作に対してクエリを実行します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="c0ccf-155">プラグインでは、サービスインデックスを使用して、サポートされているサービスの種類が存在するかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="c0ccf-156">NuGet クライアントツールとプラグインの間の通信は双方向です。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="c0ccf-157">各要求のタイムアウトは5秒です。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="c0ccf-158">操作の実行時間が長くなることが予想される場合は、要求がタイムアウトしないように、各プロセスが進捗状況メッセージを送信する必要があります。1分の非アクティブな状態では、プラグインはアイドル状態と見なされ、シャットダウンされます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="c0ccf-159">プラグインのインストールと検出</span><span class="sxs-lookup"><span data-stu-id="c0ccf-159">Plugin installation and discovery</span></span>

<span data-ttu-id="c0ccf-160">プラグインは、規則ベースのディレクトリ構造を使用して検出されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="c0ccf-161">CI/CD のシナリオとパワーユーザーは、環境変数を使用して動作をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="c0ccf-162">環境変数を使用する場合、絶対パスのみが許可されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="c0ccf-163">@No__t-0 と `NUGET_NETCORE_PLUGIN_PATHS` は、バージョン5.3 以降の NuGet ツールでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="c0ccf-164">`NUGET_NETFX_PLUGIN_PATHS`-.NET Framework ベースのツール (Nuget.exe/Msbuild.exe/Visual Studio) によって使用されるプラグインを定義します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="c0ccf-165">は `NUGET_PLUGIN_PATHS` よりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="c0ccf-166">(NuGet バージョン5.3 以降のみ)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="c0ccf-167">`NUGET_NETCORE_PLUGIN_PATHS`-.NET Core ベースのツール (dotnet) によって使用されるプラグインを定義します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="c0ccf-168">は `NUGET_PLUGIN_PATHS` よりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="c0ccf-169">(NuGet バージョン5.3 以降のみ)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="c0ccf-170">`NUGET_PLUGIN_PATHS`-その NuGet プロセスに使用されるプラグインを定義し、優先度を保持します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="c0ccf-171">この環境変数が設定されている場合は、規則ベースの検出を上書きします。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="c0ccf-172">フレームワーク固有の変数のいずれかが指定されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="c0ccf-173">@No__t-0 の NuGet ホームの場所。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="c0ccf-174">この場所を上書きすることはできません。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-174">This location cannot be overriden.</span></span> <span data-ttu-id="c0ccf-175">.NET Core と .NET Framework プラグインには、別のルートディレクトリが使用されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="c0ccf-176">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="c0ccf-176">Framework</span></span> | <span data-ttu-id="c0ccf-177">ルート探索場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="c0ccf-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="c0ccf-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="c0ccf-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="c0ccf-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="c0ccf-180">各プラグインは、独自のフォルダーにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="c0ccf-181">プラグインのエントリポイントは、インストールされているフォルダーの名前になります。また、.NET Core の .dll 拡張子と .NET Framework の .exe 拡張子が使用されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="c0ccf-182">現在、プラグインをインストールするためのユーザーストーリーはありません。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="c0ccf-183">これは、必要なファイルを事前に定義された場所に移動するだけの簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="c0ccf-184">サポートされる操作</span><span class="sxs-lookup"><span data-stu-id="c0ccf-184">Supported operations</span></span>

<span data-ttu-id="c0ccf-185">新しいプラグインプロトコルでは、2つの操作がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="c0ccf-186">操作名</span><span class="sxs-lookup"><span data-stu-id="c0ccf-186">Operation name</span></span> | <span data-ttu-id="c0ccf-187">最小プロトコルバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-187">Minimum protocol version</span></span> | <span data-ttu-id="c0ccf-188">最小 NuGet クライアントバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="c0ccf-189">パッケージのダウンロード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-189">Download Package</span></span> | <span data-ttu-id="c0ccf-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="c0ccf-190">1.0.0</span></span> | <span data-ttu-id="c0ccf-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="c0ccf-191">4.3.0</span></span> |
| [<span data-ttu-id="c0ccf-192">認証</span><span class="sxs-lookup"><span data-stu-id="c0ccf-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="c0ccf-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="c0ccf-193">2.0.0</span></span> | <span data-ttu-id="c0ccf-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="c0ccf-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="c0ccf-195">正しいランタイムでのプラグインの実行</span><span class="sxs-lookup"><span data-stu-id="c0ccf-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="c0ccf-196">Dotnet シナリオの NuGet の場合、プラグインは dotnet の特定のランタイムで実行できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="c0ccf-197">プラグインプロバイダーとコンシューマーが、互換性のある dotnet とプラグインの組み合わせが使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="c0ccf-198">ユーザー場所プラグインでは、たとえば、2.0 ランタイムの下にある dotnet が2.1 ランタイム用に記述されたプラグインを使用しようとすると、問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="c0ccf-199">機能のキャッシュ</span><span class="sxs-lookup"><span data-stu-id="c0ccf-199">Capabilities caching</span></span>

<span data-ttu-id="c0ccf-200">プラグインのセキュリティ検証とインスタンス化はコストがかかります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="c0ccf-201">ダウンロード操作は認証操作よりも頻繁に行われますが、平均の NuGet ユーザーは認証プラグインを持つ可能性があるだけです。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="c0ccf-202">エクスペリエンスを向上させるために、NuGet は指定された要求の操作要求をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="c0ccf-203">このキャッシュはプラグインごとに、プラグインキーはプラグインパス、この機能キャッシュの有効期限は30日です。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="c0ccf-204">キャッシュは @no__t 0 にあり、環境変数 `NUGET_PLUGINS_CACHE_PATH` でオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="c0ccf-205">この[キャッシュ](../../consume-packages/managing-the-global-packages-and-cache-folders.md)をクリアするには、`plugins-cache` オプションを指定してローカルコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="c0ccf-206">@No__t-0 ローカルオプションでは、プラグインキャッシュも削除されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="c0ccf-207">プロトコルメッセージのインデックス</span><span class="sxs-lookup"><span data-stu-id="c0ccf-207">Protocol messages index</span></span>

<span data-ttu-id="c0ccf-208">プロトコルバージョン*1.0.0*メッセージ:</span><span class="sxs-lookup"><span data-stu-id="c0ccf-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="c0ccf-209">閉じる</span><span class="sxs-lookup"><span data-stu-id="c0ccf-209">Close</span></span>
    * <span data-ttu-id="c0ccf-210">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c0ccf-211">要求にペイロードが含まれていません</span><span class="sxs-lookup"><span data-stu-id="c0ccf-211">The request will contain no payload</span></span>
    * <span data-ttu-id="c0ccf-212">応答は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-212">No response is expected.</span></span>  <span data-ttu-id="c0ccf-213">適切な応答は、プラグインプロセスがすぐに終了するためです。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="c0ccf-214">パッケージ内のファイルをコピーする</span><span class="sxs-lookup"><span data-stu-id="c0ccf-214">Copy files in package</span></span>
    * <span data-ttu-id="c0ccf-215">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c0ccf-216">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-216">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-217">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-217">the package ID and version</span></span>
        * <span data-ttu-id="c0ccf-218">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-218">the package source repository location</span></span>
        * <span data-ttu-id="c0ccf-219">宛先ディレクトリのパス</span><span class="sxs-lookup"><span data-stu-id="c0ccf-219">destination directory path</span></span>
        * <span data-ttu-id="c0ccf-220">コピー先のディレクトリパスにコピーするパッケージ内のファイルの列挙</span><span class="sxs-lookup"><span data-stu-id="c0ccf-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="c0ccf-221">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-221">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-222">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c0ccf-223">操作が成功した場合にコピー先ディレクトリにコピーされたファイルの完全パスを列挙可能</span><span class="sxs-lookup"><span data-stu-id="c0ccf-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="c0ccf-224">パッケージファイルのコピー (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="c0ccf-225">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c0ccf-226">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-226">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-227">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-227">the package ID and version</span></span>
        * <span data-ttu-id="c0ccf-228">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-228">the package source repository location</span></span>
        * <span data-ttu-id="c0ccf-229">コピー先のファイルパス</span><span class="sxs-lookup"><span data-stu-id="c0ccf-229">the destination file path</span></span>
    * <span data-ttu-id="c0ccf-230">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-230">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-231">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="c0ccf-232">資格情報の取得</span><span class="sxs-lookup"><span data-stu-id="c0ccf-232">Get credentials</span></span>
    * <span data-ttu-id="c0ccf-233">要求方向: プラグイン-> NuGet</span><span class="sxs-lookup"><span data-stu-id="c0ccf-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="c0ccf-234">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-234">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-235">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-235">the package source repository location</span></span>
        * <span data-ttu-id="c0ccf-236">現在の資格情報を使用してパッケージソースリポジトリから取得した HTTP ステータスコード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="c0ccf-237">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-237">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-238">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c0ccf-239">ユーザー名 (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-239">a username, if available</span></span>
        * <span data-ttu-id="c0ccf-240">パスワード (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-240">a password, if available</span></span>

5.  <span data-ttu-id="c0ccf-241">パッケージ内のファイルを取得する</span><span class="sxs-lookup"><span data-stu-id="c0ccf-241">Get files in package</span></span>
    * <span data-ttu-id="c0ccf-242">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c0ccf-243">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-243">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-244">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-244">the package ID and version</span></span>
        * <span data-ttu-id="c0ccf-245">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-245">the package source repository location</span></span>
    * <span data-ttu-id="c0ccf-246">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-246">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-247">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c0ccf-248">操作が成功した場合のパッケージ内のファイルパスの列挙。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="c0ccf-249">操作要求の取得</span><span class="sxs-lookup"><span data-stu-id="c0ccf-249">Get operation claims</span></span> 
    * <span data-ttu-id="c0ccf-250">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c0ccf-251">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-251">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-252">パッケージソースのサービスインデックス。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="c0ccf-253">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-253">the package source repository location</span></span>
    * <span data-ttu-id="c0ccf-254">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-254">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-255">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c0ccf-256">操作が成功した場合の、サポートされている操作 (例: パッケージのダウンロード) の列挙。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="c0ccf-257">プラグインでパッケージソースがサポートされていない場合、プラグインはサポートされている操作の空のセットを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="c0ccf-258">このメッセージは、バージョン*2.0.0*で更新されました。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="c0ccf-259">旧バージョンとの互換性を維持するために、クライアント上にあります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="c0ccf-260">パッケージハッシュの取得</span><span class="sxs-lookup"><span data-stu-id="c0ccf-260">Get package hash</span></span>
    * <span data-ttu-id="c0ccf-261">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c0ccf-262">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-262">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-263">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-263">the package ID and version</span></span>
        * <span data-ttu-id="c0ccf-264">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-264">the package source repository location</span></span>
        * <span data-ttu-id="c0ccf-265">ハッシュアルゴリズム</span><span class="sxs-lookup"><span data-stu-id="c0ccf-265">the hash algorithm</span></span>
    * <span data-ttu-id="c0ccf-266">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-266">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-267">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c0ccf-268">操作が成功した場合は、要求されたハッシュアルゴリズムを使用したパッケージファイルハッシュ</span><span class="sxs-lookup"><span data-stu-id="c0ccf-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="c0ccf-269">パッケージのバージョンを取得する</span><span class="sxs-lookup"><span data-stu-id="c0ccf-269">Get package versions</span></span>
    * <span data-ttu-id="c0ccf-270">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c0ccf-271">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-271">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-272">パッケージ ID</span><span class="sxs-lookup"><span data-stu-id="c0ccf-272">the package ID</span></span>
        * <span data-ttu-id="c0ccf-273">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-273">the package source repository location</span></span>
    * <span data-ttu-id="c0ccf-274">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-274">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-275">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c0ccf-276">操作が成功した場合のパッケージバージョンの列挙可能な</span><span class="sxs-lookup"><span data-stu-id="c0ccf-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="c0ccf-277">サービスインデックスの取得</span><span class="sxs-lookup"><span data-stu-id="c0ccf-277">Get service index</span></span>
    * <span data-ttu-id="c0ccf-278">要求方向: プラグイン-> NuGet</span><span class="sxs-lookup"><span data-stu-id="c0ccf-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="c0ccf-279">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-279">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-280">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-280">the package source repository location</span></span>
    * <span data-ttu-id="c0ccf-281">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-281">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-282">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c0ccf-283">操作が成功した場合のサービスインデックス</span><span class="sxs-lookup"><span data-stu-id="c0ccf-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="c0ccf-284">ハンドシェイク</span><span class="sxs-lookup"><span data-stu-id="c0ccf-284">Handshake</span></span>
     * <span data-ttu-id="c0ccf-285">要求方向: NuGet <-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="c0ccf-286">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-286">The request will contain:</span></span>
         * <span data-ttu-id="c0ccf-287">現在のプラグインプロトコルのバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="c0ccf-288">サポートされている最小プラグインプロトコルバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="c0ccf-289">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-289">A response will contain:</span></span>
         * <span data-ttu-id="c0ccf-290">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="c0ccf-291">操作が成功した場合は、ネゴシエートされたプロトコルバージョン。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="c0ccf-292">エラーが発生すると、プラグインが終了します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="c0ccf-293">Initialize</span><span class="sxs-lookup"><span data-stu-id="c0ccf-293">Initialize</span></span>
     * <span data-ttu-id="c0ccf-294">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c0ccf-295">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-295">The request will contain:</span></span>
         * <span data-ttu-id="c0ccf-296">NuGet クライアントツールのバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="c0ccf-297">NuGet クライアントツールの有効な言語です。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="c0ccf-298">これにより、ForceEnglishOutput 設定が使用されている場合、そのことが考慮されます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="c0ccf-299">既定の要求タイムアウト (プロトコルの既定値よりも優先されます)。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="c0ccf-300">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-300">A response will contain:</span></span>
         * <span data-ttu-id="c0ccf-301">操作の結果を示す応答コード。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="c0ccf-302">エラーが発生すると、プラグインが終了します。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="c0ccf-303">ログ</span><span class="sxs-lookup"><span data-stu-id="c0ccf-303">Log</span></span>
     * <span data-ttu-id="c0ccf-304">要求方向: プラグイン-> NuGet</span><span class="sxs-lookup"><span data-stu-id="c0ccf-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="c0ccf-305">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-305">The request will contain:</span></span>
         * <span data-ttu-id="c0ccf-306">要求のログレベル</span><span class="sxs-lookup"><span data-stu-id="c0ccf-306">the log level for the request</span></span>
         * <span data-ttu-id="c0ccf-307">ログに記録するメッセージ</span><span class="sxs-lookup"><span data-stu-id="c0ccf-307">a message to log</span></span>
     * <span data-ttu-id="c0ccf-308">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-308">A response will contain:</span></span>
         * <span data-ttu-id="c0ccf-309">操作の結果を示す応答コード。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="c0ccf-310">NuGet プロセス終了の監視</span><span class="sxs-lookup"><span data-stu-id="c0ccf-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="c0ccf-311">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c0ccf-312">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-312">The request will contain:</span></span>
         * <span data-ttu-id="c0ccf-313">NuGet プロセス ID</span><span class="sxs-lookup"><span data-stu-id="c0ccf-313">the NuGet process ID</span></span>
     * <span data-ttu-id="c0ccf-314">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-314">A response will contain:</span></span>
         * <span data-ttu-id="c0ccf-315">操作の結果を示す応答コード。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="c0ccf-316">プリフェッチパッケージ</span><span class="sxs-lookup"><span data-stu-id="c0ccf-316">Prefetch package</span></span>
     * <span data-ttu-id="c0ccf-317">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c0ccf-318">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-318">The request will contain:</span></span>
         * <span data-ttu-id="c0ccf-319">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-319">the package ID and version</span></span>
         * <span data-ttu-id="c0ccf-320">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-320">the package source repository location</span></span>
     * <span data-ttu-id="c0ccf-321">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-321">A response will contain:</span></span>
         * <span data-ttu-id="c0ccf-322">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="c0ccf-323">資格情報の設定</span><span class="sxs-lookup"><span data-stu-id="c0ccf-323">Set credentials</span></span>
     * <span data-ttu-id="c0ccf-324">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c0ccf-325">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-325">The request will contain:</span></span>
         * <span data-ttu-id="c0ccf-326">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-326">the package source repository location</span></span>
         * <span data-ttu-id="c0ccf-327">最後に認識されたパッケージソースのユーザー名 (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="c0ccf-328">最後に認識されたパッケージソースパスワード (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="c0ccf-329">最後の既知のプロキシユーザー名 (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="c0ccf-330">最後に確認されたプロキシパスワード (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="c0ccf-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="c0ccf-331">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-331">A response will contain:</span></span>
         * <span data-ttu-id="c0ccf-332">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="c0ccf-333">ログレベルの設定</span><span class="sxs-lookup"><span data-stu-id="c0ccf-333">Set log level</span></span>
     * <span data-ttu-id="c0ccf-334">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="c0ccf-335">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-335">The request will contain:</span></span>
         * <span data-ttu-id="c0ccf-336">既定のログレベル</span><span class="sxs-lookup"><span data-stu-id="c0ccf-336">the default log level</span></span>
     * <span data-ttu-id="c0ccf-337">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-337">A response will contain:</span></span>
         * <span data-ttu-id="c0ccf-338">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="c0ccf-339">プロトコルバージョン*2.0.0*メッセージ</span><span class="sxs-lookup"><span data-stu-id="c0ccf-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="c0ccf-340">操作要求の取得</span><span class="sxs-lookup"><span data-stu-id="c0ccf-340">Get Operation Claims</span></span>

* <span data-ttu-id="c0ccf-341">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="c0ccf-342">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-342">The request will contain:</span></span>
        * <span data-ttu-id="c0ccf-343">パッケージソースのサービスインデックス。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="c0ccf-344">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="c0ccf-344">the package source repository location</span></span>
    * <span data-ttu-id="c0ccf-345">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-345">A response will contain:</span></span>
        * <span data-ttu-id="c0ccf-346">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="c0ccf-347">操作が成功した場合の、サポートされている操作の列挙体。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="c0ccf-348">プラグインでパッケージソースがサポートされていない場合、プラグインはサポートされている操作の空のセットを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="c0ccf-349">サービスインデックスとパッケージソースが null の場合、プラグインは認証を使用して応答できます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="c0ccf-350">認証資格情報の取得</span><span class="sxs-lookup"><span data-stu-id="c0ccf-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="c0ccf-351">要求方向: NuGet > プラグイン</span><span class="sxs-lookup"><span data-stu-id="c0ccf-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="c0ccf-352">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-352">The request will contain:</span></span>
    * <span data-ttu-id="c0ccf-353">URI</span><span class="sxs-lookup"><span data-stu-id="c0ccf-353">Uri</span></span>
    * <span data-ttu-id="c0ccf-354">isRetry</span><span class="sxs-lookup"><span data-stu-id="c0ccf-354">isRetry</span></span>
    * <span data-ttu-id="c0ccf-355">非対話型</span><span class="sxs-lookup"><span data-stu-id="c0ccf-355">NonInteractive</span></span>
    * <span data-ttu-id="c0ccf-356">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="c0ccf-356">CanShowDialog</span></span>
* <span data-ttu-id="c0ccf-357">応答にはが含まれます。</span><span class="sxs-lookup"><span data-stu-id="c0ccf-357">A response will contain</span></span>
    * <span data-ttu-id="c0ccf-358">ユーザー名</span><span class="sxs-lookup"><span data-stu-id="c0ccf-358">Username</span></span>
    * <span data-ttu-id="c0ccf-359">パスワード</span><span class="sxs-lookup"><span data-stu-id="c0ccf-359">Password</span></span>
    * <span data-ttu-id="c0ccf-360">[メッセージ]</span><span class="sxs-lookup"><span data-stu-id="c0ccf-360">Message</span></span>
    * <span data-ttu-id="c0ccf-361">認証の種類の一覧</span><span class="sxs-lookup"><span data-stu-id="c0ccf-361">List of Auth Types</span></span>
    * <span data-ttu-id="c0ccf-362">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="c0ccf-362">MessageResponseCode</span></span>
