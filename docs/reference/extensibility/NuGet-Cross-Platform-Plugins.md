---
title: NuGet クロスプラットフォームプラグイン
description: Nuget、dotnet、msbuild.exe、および Visual Studio 用の NuGet クロスプラットフォームプラグイン
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815306"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="40cc2-103">NuGet クロスプラットフォームプラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="40cc2-104">NuGet 4.8 以降では、クロスプラットフォームプラグインのサポートが追加されています。</span><span class="sxs-lookup"><span data-stu-id="40cc2-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="40cc2-105">これは、新しいプラグイン拡張モデルを構築することで実現されました。これは、厳密な一連の操作規則に準拠する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="40cc2-106">プラグインは自己完結型の実行可能ファイルであり、NuGet クライアントは別のプロセスで起動されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="40cc2-107">これは、1回の書き込みで、すべてのプラグインを実行します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="40cc2-108">これは、すべての NuGet クライアントツールで動作します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="40cc2-109">プラグインには、.NET Framework (Nuget.exe、Msbuild.exe、Visual Studio)、または .NET Core (dotnet) のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="40cc2-110">NuGet クライアントとプラグインの間のバージョン付き通信プロトコルが定義されています。</span><span class="sxs-lookup"><span data-stu-id="40cc2-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="40cc2-111">スタートアップハンドシェイク中、2つのプロセスがプロトコルのバージョンをネゴシエートします。</span><span class="sxs-lookup"><span data-stu-id="40cc2-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="40cc2-112">すべての NuGet クライアントツールのシナリオに対応するために、.NET Framework と .NET Core プラグインの両方が必要です。</span><span class="sxs-lookup"><span data-stu-id="40cc2-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="40cc2-113">次に、プラグインのクライアントとフレームワークの組み合わせについて説明します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="40cc2-114">クライアント ツール</span><span class="sxs-lookup"><span data-stu-id="40cc2-114">Client tool</span></span>  | <span data-ttu-id="40cc2-115">Framework</span><span class="sxs-lookup"><span data-stu-id="40cc2-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="40cc2-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40cc2-116">Visual Studio</span></span> | <span data-ttu-id="40cc2-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="40cc2-117">.NET Framework</span></span> |
| <span data-ttu-id="40cc2-118">dotnet</span><span class="sxs-lookup"><span data-stu-id="40cc2-118">dotnet.exe</span></span> | <span data-ttu-id="40cc2-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="40cc2-119">.NET Core</span></span> |
| <span data-ttu-id="40cc2-120">Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="40cc2-120">NuGet.exe</span></span> | <span data-ttu-id="40cc2-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="40cc2-121">.NET Framework</span></span> |
| <span data-ttu-id="40cc2-122">Msbuild.exe</span><span class="sxs-lookup"><span data-stu-id="40cc2-122">MSBuild.exe</span></span> | <span data-ttu-id="40cc2-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="40cc2-123">.NET Framework</span></span> |
| <span data-ttu-id="40cc2-124">Mono での Nuget.exe</span><span class="sxs-lookup"><span data-stu-id="40cc2-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="40cc2-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="40cc2-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="40cc2-126">動作のしくみ</span><span class="sxs-lookup"><span data-stu-id="40cc2-126">How does it work</span></span>

<span data-ttu-id="40cc2-127">高レベルのワークフローは、次のように記述できます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="40cc2-128">NuGet は、使用可能なプラグインを検出します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="40cc2-129">該当する場合、NuGet はプラグインを優先順位に従って繰り返し処理し、1つずつ開始します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="40cc2-130">NuGet は、要求を処理できる最初のプラグインを使用します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="40cc2-131">プラグインは、不要になったときにシャットダウンされます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="40cc2-132">一般的なプラグインの要件</span><span class="sxs-lookup"><span data-stu-id="40cc2-132">General plugin requirements</span></span>

<span data-ttu-id="40cc2-133">現在のプロトコルバージョンは*2.0.0*です。</span><span class="sxs-lookup"><span data-stu-id="40cc2-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="40cc2-134">このバージョンでは、次の要件があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="40cc2-135">Windows と Mono で実行される、信頼された有効な Authenticode 署名アセンブリを用意します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="40cc2-136">Linux および Mac でのアセンブリの実行には、特別な信頼要件はありません。</span><span class="sxs-lookup"><span data-stu-id="40cc2-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="40cc2-137">関連する問題</span><span class="sxs-lookup"><span data-stu-id="40cc2-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="40cc2-138">NuGet クライアントツールの現在のセキュリティコンテキストでのステートレス起動をサポートします。</span><span class="sxs-lookup"><span data-stu-id="40cc2-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="40cc2-139">たとえば、NuGet クライアントツールでは、後で説明するプラグインプロトコルの外部での昇格や追加の初期化は実行されません。</span><span class="sxs-lookup"><span data-stu-id="40cc2-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="40cc2-140">明示的に指定されている場合を除き、非対話型にします。</span><span class="sxs-lookup"><span data-stu-id="40cc2-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="40cc2-141">ネゴシエートされたプラグインプロトコルのバージョンに準拠します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="40cc2-142">妥当な期間内にすべての要求に応答します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="40cc2-143">進行中の操作のキャンセル要求を優先します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="40cc2-144">技術仕様の詳細については、次の仕様を参照してください。</span><span class="sxs-lookup"><span data-stu-id="40cc2-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="40cc2-145">NuGet パッケージのダウンロードプラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="40cc2-146">NuGet のクロスプラットフォーム認証プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="40cc2-147">クライアントとプラグインの相互作用</span><span class="sxs-lookup"><span data-stu-id="40cc2-147">Client - Plugin interaction</span></span>

<span data-ttu-id="40cc2-148">NuGet クライアントツールとプラグインは、標準ストリーム (stdin、stdout、stderr) を介して JSON と通信します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="40cc2-149">すべてのデータは、UTF-8 でエンコードする必要があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="40cc2-150">プラグインは、引数 "-Plugin" を使用して起動されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="40cc2-151">ユーザーがこの引数を指定せずにプラグインの実行可能ファイルを直接起動した場合、プラグインは、プロトコルハンドシェイクを待機する代わりに、情報メッセージを提供できます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="40cc2-152">プロトコルハンドシェイクタイムアウトは5秒です。</span><span class="sxs-lookup"><span data-stu-id="40cc2-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="40cc2-153">プラグインは、できるだけ少ない量でセットアップを完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="40cc2-154">NuGet クライアントツールは、NuGet ソースのサービスインデックスを渡すことによって、プラグインのサポートされている操作に対してクエリを実行します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="40cc2-155">プラグインでは、サービスインデックスを使用して、サポートされているサービスの種類が存在するかどうかを確認できます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="40cc2-156">NuGet クライアントツールとプラグインの間の通信は双方向です。</span><span class="sxs-lookup"><span data-stu-id="40cc2-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="40cc2-157">各要求のタイムアウトは5秒です。</span><span class="sxs-lookup"><span data-stu-id="40cc2-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="40cc2-158">操作の実行時間が長くなることが予想される場合は、要求がタイムアウトしないように、各プロセスが進捗状況メッセージを送信する必要があります。1分の非アクティブな状態では、プラグインはアイドル状態と見なされ、シャットダウンされます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="40cc2-159">プラグインのインストールと検出</span><span class="sxs-lookup"><span data-stu-id="40cc2-159">Plugin installation and discovery</span></span>

<span data-ttu-id="40cc2-160">プラグインは、規則ベースのディレクトリ構造を使用して検出されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="40cc2-161">CI/CD のシナリオとパワーユーザーは、環境変数を使用して動作をオーバーライドできます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="40cc2-162">`NUGET_NETFX_PLUGIN_PATHS` と`NUGET_NETCORE_PLUGIN_PATHS`は、5.3 以降のバージョンの NuGet ツールでのみ使用できます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="40cc2-163">`NUGET_NETFX_PLUGIN_PATHS`-.NET Framework ベースのツール (Nuget.exe/Msbuild.exe/Visual Studio) によって使用されるプラグインを定義します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="40cc2-164">はより`NUGET_PLUGIN_PATHS`も優先されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="40cc2-165">(NuGet バージョン5.3 以降のみ)</span><span class="sxs-lookup"><span data-stu-id="40cc2-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="40cc2-166">`NUGET_NETCORE_PLUGIN_PATHS`-.NET Core ベースのツール (dotnet) によって使用されるプラグインを定義します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="40cc2-167">はより`NUGET_PLUGIN_PATHS`も優先されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="40cc2-168">(NuGet バージョン5.3 以降のみ)</span><span class="sxs-lookup"><span data-stu-id="40cc2-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="40cc2-169">`NUGET_PLUGIN_PATHS`-その NuGet プロセスに使用されるプラグイン、優先順位予約済みのプラグインを定義します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="40cc2-170">この環境変数が設定されている場合は、規則ベースの検出を上書きします。</span><span class="sxs-lookup"><span data-stu-id="40cc2-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="40cc2-171">フレームワーク固有の変数のいずれかが指定されている場合は無視されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="40cc2-172">ユーザー-場所 (の`%UserProfile%/.nuget/plugins`NuGet ホームの場所)。</span><span class="sxs-lookup"><span data-stu-id="40cc2-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="40cc2-173">この場所を上書きすることはできません。</span><span class="sxs-lookup"><span data-stu-id="40cc2-173">This location cannot be overriden.</span></span> <span data-ttu-id="40cc2-174">.NET Core と .NET Framework プラグインには、別のルートディレクトリが使用されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="40cc2-175">Framework</span><span class="sxs-lookup"><span data-stu-id="40cc2-175">Framework</span></span> | <span data-ttu-id="40cc2-176">ルート探索場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="40cc2-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="40cc2-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="40cc2-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="40cc2-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="40cc2-179">各プラグインは、独自のフォルダーにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="40cc2-180">プラグインのエントリポイントは、インストールされているフォルダーの名前になります。また、.NET Core の .dll 拡張子と .NET Framework の .exe 拡張子が使用されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="40cc2-181">現在、プラグインをインストールするためのユーザーストーリーはありません。</span><span class="sxs-lookup"><span data-stu-id="40cc2-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="40cc2-182">これは、必要なファイルを事前に定義された場所に移動するだけの簡単な方法です。</span><span class="sxs-lookup"><span data-stu-id="40cc2-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="40cc2-183">サポートされる操作</span><span class="sxs-lookup"><span data-stu-id="40cc2-183">Supported operations</span></span>

<span data-ttu-id="40cc2-184">新しいプラグインプロトコルでは、2つの操作がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="40cc2-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="40cc2-185">操作名</span><span class="sxs-lookup"><span data-stu-id="40cc2-185">Operation name</span></span> | <span data-ttu-id="40cc2-186">最小プロトコルバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-186">Minimum protocol version</span></span> | <span data-ttu-id="40cc2-187">最小 NuGet クライアントバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="40cc2-188">パッケージのダウンロード</span><span class="sxs-lookup"><span data-stu-id="40cc2-188">Download Package</span></span> | <span data-ttu-id="40cc2-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="40cc2-189">1.0.0</span></span> | <span data-ttu-id="40cc2-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="40cc2-190">4.3.0</span></span> |
| [<span data-ttu-id="40cc2-191">認証</span><span class="sxs-lookup"><span data-stu-id="40cc2-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="40cc2-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="40cc2-192">2.0.0</span></span> | <span data-ttu-id="40cc2-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="40cc2-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="40cc2-194">正しいランタイムでのプラグインの実行</span><span class="sxs-lookup"><span data-stu-id="40cc2-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="40cc2-195">Dotnet シナリオの NuGet の場合、プラグインは dotnet の特定のランタイムで実行できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="40cc2-196">プラグインプロバイダーとコンシューマーが、互換性のある dotnet とプラグインの組み合わせが使用されていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="40cc2-197">ユーザー場所プラグインでは、たとえば、2.0 ランタイムの下にある dotnet が2.1 ランタイム用に記述されたプラグインを使用しようとすると、問題が発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="40cc2-198">機能のキャッシュ</span><span class="sxs-lookup"><span data-stu-id="40cc2-198">Capabilities caching</span></span>

<span data-ttu-id="40cc2-199">プラグインのセキュリティ検証とインスタンス化はコストがかかります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="40cc2-200">ダウンロード操作は認証操作よりも頻繁に行われますが、平均の NuGet ユーザーは認証プラグインを持つ可能性があるだけです。</span><span class="sxs-lookup"><span data-stu-id="40cc2-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="40cc2-201">エクスペリエンスを向上させるために、NuGet は指定された要求の操作要求をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="40cc2-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="40cc2-202">このキャッシュはプラグインごとに、プラグインキーはプラグインパス、この機能キャッシュの有効期限は30日です。</span><span class="sxs-lookup"><span data-stu-id="40cc2-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="40cc2-203">キャッシュはに`%LocalAppData%/NuGet/plugins-cache`あり、環境変数`NUGET_PLUGINS_CACHE_PATH`でオーバーライドされます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="40cc2-204">この[キャッシュ](../../consume-packages/managing-the-global-packages-and-cache-folders.md)をクリアするには、 `plugins-cache`オプションを指定してローカルコマンドを実行します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="40cc2-205">[ `all`ローカル] オプションでは、プラグインキャッシュも削除されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="40cc2-206">プロトコルメッセージのインデックス</span><span class="sxs-lookup"><span data-stu-id="40cc2-206">Protocol messages index</span></span>

<span data-ttu-id="40cc2-207">プロトコルバージョン*1.0.0*メッセージ:</span><span class="sxs-lookup"><span data-stu-id="40cc2-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="40cc2-208">閉じる</span><span class="sxs-lookup"><span data-stu-id="40cc2-208">Close</span></span>
    * <span data-ttu-id="40cc2-209">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="40cc2-210">要求にペイロードが含まれていません</span><span class="sxs-lookup"><span data-stu-id="40cc2-210">The request will contain no payload</span></span>
    * <span data-ttu-id="40cc2-211">応答は必要ありません。</span><span class="sxs-lookup"><span data-stu-id="40cc2-211">No response is expected.</span></span>  <span data-ttu-id="40cc2-212">適切な応答は、プラグインプロセスがすぐに終了するためです。</span><span class="sxs-lookup"><span data-stu-id="40cc2-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="40cc2-213">パッケージ内のファイルをコピーする</span><span class="sxs-lookup"><span data-stu-id="40cc2-213">Copy files in package</span></span>
    * <span data-ttu-id="40cc2-214">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="40cc2-215">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-215">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-216">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-216">the package ID and version</span></span>
        * <span data-ttu-id="40cc2-217">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-217">the package source repository location</span></span>
        * <span data-ttu-id="40cc2-218">宛先ディレクトリのパス</span><span class="sxs-lookup"><span data-stu-id="40cc2-218">destination directory path</span></span>
        * <span data-ttu-id="40cc2-219">コピー先のディレクトリパスにコピーするパッケージ内のファイルの列挙</span><span class="sxs-lookup"><span data-stu-id="40cc2-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="40cc2-220">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-220">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-221">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="40cc2-222">操作が成功した場合にコピー先ディレクトリにコピーされたファイルの完全パスを列挙可能</span><span class="sxs-lookup"><span data-stu-id="40cc2-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="40cc2-223">パッケージファイルのコピー (. nupkg)</span><span class="sxs-lookup"><span data-stu-id="40cc2-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="40cc2-224">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="40cc2-225">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-225">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-226">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-226">the package ID and version</span></span>
        * <span data-ttu-id="40cc2-227">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-227">the package source repository location</span></span>
        * <span data-ttu-id="40cc2-228">コピー先のファイルパス</span><span class="sxs-lookup"><span data-stu-id="40cc2-228">the destination file path</span></span>
    * <span data-ttu-id="40cc2-229">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-229">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-230">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="40cc2-231">資格情報の取得</span><span class="sxs-lookup"><span data-stu-id="40cc2-231">Get credentials</span></span>
    * <span data-ttu-id="40cc2-232">要求方向: プラグイン-> NuGet</span><span class="sxs-lookup"><span data-stu-id="40cc2-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="40cc2-233">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-233">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-234">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-234">the package source repository location</span></span>
        * <span data-ttu-id="40cc2-235">現在の資格情報を使用してパッケージソースリポジトリから取得した HTTP ステータスコード</span><span class="sxs-lookup"><span data-stu-id="40cc2-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="40cc2-236">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-236">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-237">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="40cc2-238">ユーザー名 (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="40cc2-238">a username, if available</span></span>
        * <span data-ttu-id="40cc2-239">パスワード (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="40cc2-239">a password, if available</span></span>

5.  <span data-ttu-id="40cc2-240">パッケージ内のファイルを取得する</span><span class="sxs-lookup"><span data-stu-id="40cc2-240">Get files in package</span></span>
    * <span data-ttu-id="40cc2-241">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="40cc2-242">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-242">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-243">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-243">the package ID and version</span></span>
        * <span data-ttu-id="40cc2-244">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-244">the package source repository location</span></span>
    * <span data-ttu-id="40cc2-245">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-245">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-246">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="40cc2-247">操作が成功した場合のパッケージ内のファイルパスの列挙。</span><span class="sxs-lookup"><span data-stu-id="40cc2-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="40cc2-248">操作要求の取得</span><span class="sxs-lookup"><span data-stu-id="40cc2-248">Get operation claims</span></span> 
    * <span data-ttu-id="40cc2-249">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="40cc2-250">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-250">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-251">パッケージソースのサービスインデックス。</span><span class="sxs-lookup"><span data-stu-id="40cc2-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="40cc2-252">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-252">the package source repository location</span></span>
    * <span data-ttu-id="40cc2-253">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-253">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-254">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="40cc2-255">操作が成功した場合の、サポートされている操作 (例: パッケージのダウンロード) の列挙。</span><span class="sxs-lookup"><span data-stu-id="40cc2-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="40cc2-256">プラグインでパッケージソースがサポートされていない場合、プラグインはサポートされている操作の空のセットを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="40cc2-257">このメッセージは、バージョン*2.0.0*で更新されました。</span><span class="sxs-lookup"><span data-stu-id="40cc2-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="40cc2-258">旧バージョンとの互換性を維持するために、クライアント上にあります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="40cc2-259">パッケージハッシュの取得</span><span class="sxs-lookup"><span data-stu-id="40cc2-259">Get package hash</span></span>
    * <span data-ttu-id="40cc2-260">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="40cc2-261">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-261">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-262">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-262">the package ID and version</span></span>
        * <span data-ttu-id="40cc2-263">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-263">the package source repository location</span></span>
        * <span data-ttu-id="40cc2-264">ハッシュアルゴリズム</span><span class="sxs-lookup"><span data-stu-id="40cc2-264">the hash algorithm</span></span>
    * <span data-ttu-id="40cc2-265">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-265">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-266">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="40cc2-267">操作が成功した場合は、要求されたハッシュアルゴリズムを使用したパッケージファイルハッシュ</span><span class="sxs-lookup"><span data-stu-id="40cc2-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="40cc2-268">パッケージのバージョンを取得する</span><span class="sxs-lookup"><span data-stu-id="40cc2-268">Get package versions</span></span>
    * <span data-ttu-id="40cc2-269">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="40cc2-270">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-270">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-271">パッケージ ID</span><span class="sxs-lookup"><span data-stu-id="40cc2-271">the package ID</span></span>
        * <span data-ttu-id="40cc2-272">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-272">the package source repository location</span></span>
    * <span data-ttu-id="40cc2-273">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-273">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-274">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="40cc2-275">操作が成功した場合のパッケージバージョンの列挙可能な</span><span class="sxs-lookup"><span data-stu-id="40cc2-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="40cc2-276">サービスインデックスの取得</span><span class="sxs-lookup"><span data-stu-id="40cc2-276">Get service index</span></span>
    * <span data-ttu-id="40cc2-277">要求方向: プラグイン-> NuGet</span><span class="sxs-lookup"><span data-stu-id="40cc2-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="40cc2-278">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-278">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-279">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-279">the package source repository location</span></span>
    * <span data-ttu-id="40cc2-280">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-280">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-281">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="40cc2-282">操作が成功した場合のサービスインデックス</span><span class="sxs-lookup"><span data-stu-id="40cc2-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="40cc2-283">ハンドシェイク</span><span class="sxs-lookup"><span data-stu-id="40cc2-283">Handshake</span></span>
     * <span data-ttu-id="40cc2-284">要求方向:NuGet <-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="40cc2-285">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-285">The request will contain:</span></span>
         * <span data-ttu-id="40cc2-286">現在のプラグインプロトコルのバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="40cc2-287">サポートされている最小プラグインプロトコルバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="40cc2-288">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-288">A response will contain:</span></span>
         * <span data-ttu-id="40cc2-289">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="40cc2-290">操作が成功した場合は、ネゴシエートされたプロトコルバージョン。</span><span class="sxs-lookup"><span data-stu-id="40cc2-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="40cc2-291">エラーが発生すると、プラグインが終了します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="40cc2-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="40cc2-292">Initialize</span></span>
     * <span data-ttu-id="40cc2-293">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="40cc2-294">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-294">The request will contain:</span></span>
         * <span data-ttu-id="40cc2-295">NuGet クライアントツールのバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="40cc2-296">NuGet クライアントツールの有効な言語です。</span><span class="sxs-lookup"><span data-stu-id="40cc2-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="40cc2-297">これにより、ForceEnglishOutput 設定が使用されている場合、そのことが考慮されます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="40cc2-298">既定の要求タイムアウト (プロトコルの既定値よりも優先されます)。</span><span class="sxs-lookup"><span data-stu-id="40cc2-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="40cc2-299">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-299">A response will contain:</span></span>
         * <span data-ttu-id="40cc2-300">操作の結果を示す応答コード。</span><span class="sxs-lookup"><span data-stu-id="40cc2-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="40cc2-301">エラーが発生すると、プラグインが終了します。</span><span class="sxs-lookup"><span data-stu-id="40cc2-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="40cc2-302">Log</span><span class="sxs-lookup"><span data-stu-id="40cc2-302">Log</span></span>
     * <span data-ttu-id="40cc2-303">要求方向: プラグイン-> NuGet</span><span class="sxs-lookup"><span data-stu-id="40cc2-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="40cc2-304">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-304">The request will contain:</span></span>
         * <span data-ttu-id="40cc2-305">要求のログレベル</span><span class="sxs-lookup"><span data-stu-id="40cc2-305">the log level for the request</span></span>
         * <span data-ttu-id="40cc2-306">ログに記録するメッセージ</span><span class="sxs-lookup"><span data-stu-id="40cc2-306">a message to log</span></span>
     * <span data-ttu-id="40cc2-307">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-307">A response will contain:</span></span>
         * <span data-ttu-id="40cc2-308">操作の結果を示す応答コード。</span><span class="sxs-lookup"><span data-stu-id="40cc2-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="40cc2-309">NuGet プロセス終了の監視</span><span class="sxs-lookup"><span data-stu-id="40cc2-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="40cc2-310">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="40cc2-311">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-311">The request will contain:</span></span>
         * <span data-ttu-id="40cc2-312">NuGet プロセス ID</span><span class="sxs-lookup"><span data-stu-id="40cc2-312">the NuGet process ID</span></span>
     * <span data-ttu-id="40cc2-313">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-313">A response will contain:</span></span>
         * <span data-ttu-id="40cc2-314">操作の結果を示す応答コード。</span><span class="sxs-lookup"><span data-stu-id="40cc2-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="40cc2-315">プリフェッチパッケージ</span><span class="sxs-lookup"><span data-stu-id="40cc2-315">Prefetch package</span></span>
     * <span data-ttu-id="40cc2-316">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="40cc2-317">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-317">The request will contain:</span></span>
         * <span data-ttu-id="40cc2-318">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="40cc2-318">the package ID and version</span></span>
         * <span data-ttu-id="40cc2-319">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-319">the package source repository location</span></span>
     * <span data-ttu-id="40cc2-320">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-320">A response will contain:</span></span>
         * <span data-ttu-id="40cc2-321">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="40cc2-322">資格情報の設定</span><span class="sxs-lookup"><span data-stu-id="40cc2-322">Set credentials</span></span>
     * <span data-ttu-id="40cc2-323">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="40cc2-324">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-324">The request will contain:</span></span>
         * <span data-ttu-id="40cc2-325">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-325">the package source repository location</span></span>
         * <span data-ttu-id="40cc2-326">最後に認識されたパッケージソースのユーザー名 (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="40cc2-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="40cc2-327">最後に認識されたパッケージソースパスワード (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="40cc2-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="40cc2-328">最後の既知のプロキシユーザー名 (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="40cc2-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="40cc2-329">最後に確認されたプロキシパスワード (使用可能な場合)</span><span class="sxs-lookup"><span data-stu-id="40cc2-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="40cc2-330">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-330">A response will contain:</span></span>
         * <span data-ttu-id="40cc2-331">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="40cc2-332">ログレベルの設定</span><span class="sxs-lookup"><span data-stu-id="40cc2-332">Set log level</span></span>
     * <span data-ttu-id="40cc2-333">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="40cc2-334">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-334">The request will contain:</span></span>
         * <span data-ttu-id="40cc2-335">既定のログレベル</span><span class="sxs-lookup"><span data-stu-id="40cc2-335">the default log level</span></span>
     * <span data-ttu-id="40cc2-336">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-336">A response will contain:</span></span>
         * <span data-ttu-id="40cc2-337">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="40cc2-338">プロトコルバージョン*2.0.0*メッセージ</span><span class="sxs-lookup"><span data-stu-id="40cc2-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="40cc2-339">操作要求の取得</span><span class="sxs-lookup"><span data-stu-id="40cc2-339">Get Operation Claims</span></span>

* <span data-ttu-id="40cc2-340">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="40cc2-341">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-341">The request will contain:</span></span>
        * <span data-ttu-id="40cc2-342">パッケージソースのサービスインデックス。</span><span class="sxs-lookup"><span data-stu-id="40cc2-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="40cc2-343">パッケージソースリポジトリの場所</span><span class="sxs-lookup"><span data-stu-id="40cc2-343">the package source repository location</span></span>
    * <span data-ttu-id="40cc2-344">応答には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-344">A response will contain:</span></span>
        * <span data-ttu-id="40cc2-345">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="40cc2-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="40cc2-346">操作が成功した場合の、サポートされている操作の列挙体。</span><span class="sxs-lookup"><span data-stu-id="40cc2-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="40cc2-347">プラグインでパッケージソースがサポートされていない場合、プラグインはサポートされている操作の空のセットを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="40cc2-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="40cc2-348">サービスインデックスとパッケージソースが null の場合、プラグインは認証を使用して応答できます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="40cc2-349">認証資格情報の取得</span><span class="sxs-lookup"><span data-stu-id="40cc2-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="40cc2-350">要求方向:NuGet-> プラグイン</span><span class="sxs-lookup"><span data-stu-id="40cc2-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="40cc2-351">要求には次のものが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-351">The request will contain:</span></span>
    * <span data-ttu-id="40cc2-352">URI</span><span class="sxs-lookup"><span data-stu-id="40cc2-352">Uri</span></span>
    * <span data-ttu-id="40cc2-353">isRetry</span><span class="sxs-lookup"><span data-stu-id="40cc2-353">isRetry</span></span>
    * <span data-ttu-id="40cc2-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="40cc2-354">NonInteractive</span></span>
    * <span data-ttu-id="40cc2-355">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="40cc2-355">CanShowDialog</span></span>
* <span data-ttu-id="40cc2-356">応答にはが含まれます。</span><span class="sxs-lookup"><span data-stu-id="40cc2-356">A response will contain</span></span>
    * <span data-ttu-id="40cc2-357">Username</span><span class="sxs-lookup"><span data-stu-id="40cc2-357">Username</span></span>
    * <span data-ttu-id="40cc2-358">Password</span><span class="sxs-lookup"><span data-stu-id="40cc2-358">Password</span></span>
    * <span data-ttu-id="40cc2-359">Message</span><span class="sxs-lookup"><span data-stu-id="40cc2-359">Message</span></span>
    * <span data-ttu-id="40cc2-360">認証の種類の一覧</span><span class="sxs-lookup"><span data-stu-id="40cc2-360">List of Auth Types</span></span>
    * <span data-ttu-id="40cc2-361">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="40cc2-361">MessageResponseCode</span></span>
