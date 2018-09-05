---
title: クロス プラットフォームのプラグインの NuGet
description: NuGet.exe、dotnet.exe、msbuild.exe および Visual Studio の NuGet がプラットフォームのプラグインをクロスします。
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548207"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="4fd2e-103">クロス プラットフォームのプラグインの NuGet</span><span class="sxs-lookup"><span data-stu-id="4fd2e-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="4fd2e-104">NuGet 4.8 + でのクロス プラットフォームのプラグインのサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="4fd2e-105">これは、厳密な一連の操作の規則に準拠する必要がありますが、新しいプラグイン拡張モデルを構築することによりで実現されました。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="4fd2e-106">プラグインは、自己完結型の実行可能ファイル (実行可能コードを .NET Core の世界で)、NuGet クライアントを別のプロセスで起動します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="4fd2e-107">これは、変更は、true 書き込み 1 回、プラグインをすべての場所で実行します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="4fd2e-108">すべての NuGet クライアント ツールで動作します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="4fd2e-109">プラグインには、(NuGet.exe、MSBuild.exe と Visual Studio) での .NET Framework または .NET Core (dotnet.exe) のいずれかを指定できます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="4fd2e-110">NuGet クライアントと、プラグインのバージョン管理された通信プロトコルが定義されます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="4fd2e-111">スタートアップのハンドシェイク中には、2 つのプロセスは、プロトコルのバージョンをネゴシエートします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="4fd2e-112">NuGet クライアント ツールのすべてのシナリオを網羅するために .NET Framework と .NET Core のプラグインの両方に 1 つなります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="4fd2e-113">プラグインのクライアント/フレームワークの組み合わせを以下に示します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="4fd2e-114">クライアント ツール</span><span class="sxs-lookup"><span data-stu-id="4fd2e-114">Client tool</span></span>  | <span data-ttu-id="4fd2e-115">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="4fd2e-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="4fd2e-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4fd2e-116">Visual Studio</span></span> | <span data-ttu-id="4fd2e-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fd2e-117">.NET Framework</span></span> |
| <span data-ttu-id="4fd2e-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="4fd2e-118">dotnet.exe</span></span> | <span data-ttu-id="4fd2e-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4fd2e-119">.NET Core</span></span> |
| <span data-ttu-id="4fd2e-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="4fd2e-120">NuGet.exe</span></span> | <span data-ttu-id="4fd2e-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fd2e-121">.NET Framework</span></span> |
| <span data-ttu-id="4fd2e-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="4fd2e-122">MSBuild.exe</span></span> | <span data-ttu-id="4fd2e-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fd2e-123">.NET Framework</span></span> |
| <span data-ttu-id="4fd2e-124">Mono 上で NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="4fd2e-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="4fd2e-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fd2e-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="4fd2e-126">しくみ</span><span class="sxs-lookup"><span data-stu-id="4fd2e-126">How does it work</span></span>

<span data-ttu-id="4fd2e-127">高レベルのワークフローは、次のように記述できます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="4fd2e-128">NuGet では、使用可能なプラグインを検出します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="4fd2e-129">該当する場合、NuGet は優先順位で 1 つずつ開始プラグインを反復処理します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="4fd2e-130">NuGet では、要求を処理できる最初のプラグインを使用します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="4fd2e-131">プラグインは不要になったとき、シャット ダウンをされます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="4fd2e-132">一般的なプラグインの要件</span><span class="sxs-lookup"><span data-stu-id="4fd2e-132">General plugin requirements</span></span>

<span data-ttu-id="4fd2e-133">現在のプロトコルのバージョンは*2.0.0*します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="4fd2e-134">このバージョンは、下の要件は次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="4fd2e-135">信頼された有効な Authenticode 署名のアセンブリがある Windows、Mono で実行されます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="4fd2e-136">Linux および Mac でまだ実行アセンブリの信頼の特別な要件はありません。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="4fd2e-137">関連する問題</span><span class="sxs-lookup"><span data-stu-id="4fd2e-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="4fd2e-138">NuGet クライアント ツールの現在のセキュリティ コンテキストでステートレスな起動をサポートします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="4fd2e-139">たとえば、昇格または後で説明されているプラグインのプロトコルの外部で追加の初期化、NuGet クライアント ツールは実行されません。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="4fd2e-140">明示的に指定しない限り、非対話形式にします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="4fd2e-141">プラグインのネゴシエートされたプロトコルのバージョンに準拠します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="4fd2e-142">妥当な時間内のすべての要求に応答します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="4fd2e-143">任意の実行中の操作の取り消し要求が受け入れられます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="4fd2e-144">技術仕様は次の仕様で詳しく説明します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="4fd2e-145">NuGet パッケージのダウンロードのプラグイン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="4fd2e-146">フォーム認証のプラグイン相互の NuGet</span><span class="sxs-lookup"><span data-stu-id="4fd2e-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="4fd2e-147">クライアントのプラグイン相互作用</span><span class="sxs-lookup"><span data-stu-id="4fd2e-147">Client - Plugin interaction</span></span>

<span data-ttu-id="4fd2e-148">NuGet クライアント ツールとプラグインは、標準ストリーム (stdin、stdout、stderr) 経由での JSON で通信します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="4fd2e-149">すべてのデータは utf-8 エンコードである必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="4fd2e-150">プラグインは、引数で起動されます"-プラグイン"されます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="4fd2e-151">場合に、ユーザーは、この引数を指定せずに実行可能なプラグインを直接起動、プラグインは、プロトコルのハンドシェイクを待つのではなく、情報メッセージを与えることができます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="4fd2e-152">プロトコルのハンドシェイクのタイムアウトは、5 秒です。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="4fd2e-153">プラグインには、可能な容量が不足としてのセットアップを完了する必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="4fd2e-154">NuGet クライアント ツールは、NuGet ソースのサービス インデックスを渡すことで、プラグインのサポートされている操作を照会します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="4fd2e-155">プラグインでは、サービスのインデックスを使用して、サポートされているサービスの種類の存在を確認してください。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="4fd2e-156">NuGet クライアント ツールとプラグイン間の通信は、双方向です。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="4fd2e-157">各要求では、5 秒のタイムアウトがあります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="4fd2e-158">操作に長い時間がかかることになっている場合、対応するプロセスが要求をタイムアウトにならないようにする進行状況メッセージを送信する必要があります。1 分続いた後に、プラグインはアイドル状態と見なされがシャット ダウンします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="4fd2e-159">プラグインのインストールと探索</span><span class="sxs-lookup"><span data-stu-id="4fd2e-159">Plugin installation and discovery</span></span>

<span data-ttu-id="4fd2e-160">規約ベースのディレクトリ構造を使用して、プラグインが検出されます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="4fd2e-161">CI/CD のシナリオおよびパワー ユーザーは、動作をオーバーライドするのに環境変数を使用することができます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="4fd2e-162">`NUGET_PLUGIN_PATHS` -予約済みの優先度、その NuGet プロセスに使用される、プラグインを定義します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="4fd2e-163">この環境変数が設定されている場合は、規則ベースの検出を上書きします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="4fd2e-164">ユーザーの場所の NuGet のホーム場所、`%UserProfile%/.nuget/plugins`します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="4fd2e-165">この場所は、オーバーライドにすることはできません。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-165">This location cannot be overriden.</span></span> <span data-ttu-id="4fd2e-166">別のルート ディレクトリは、.NET Core と .NET Framework のプラグインに使用されます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="4fd2e-167">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="4fd2e-167">Framework</span></span> | <span data-ttu-id="4fd2e-168">ルートの検出場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="4fd2e-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="4fd2e-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="4fd2e-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="4fd2e-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="4fd2e-171">各プラグインは、独自のフォルダーにインストールする必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="4fd2e-172">プラグインのエントリ ポイントは、.NET Core の .dll 拡張子と .NET Framework の拡張子が .exe と、インストールされているフォルダーの名前になります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="4fd2e-173">現在、プラグインをインストールするためのユーザー ストーリーはありません。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="4fd2e-174">必要なファイルを事前に定義された場所に移動するだけになります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="4fd2e-175">サポートされる操作</span><span class="sxs-lookup"><span data-stu-id="4fd2e-175">Supported operations</span></span>

<span data-ttu-id="4fd2e-176">新しいプラグインのプロトコルの下では、2 つの操作がサポートされています。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="4fd2e-177">操作名</span><span class="sxs-lookup"><span data-stu-id="4fd2e-177">Operation name</span></span> | <span data-ttu-id="4fd2e-178">最小バージョンのプロトコル</span><span class="sxs-lookup"><span data-stu-id="4fd2e-178">Minimum protocol version</span></span> | <span data-ttu-id="4fd2e-179">最小の NuGet クライアント バージョン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="4fd2e-180">パッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-180">Download Package</span></span> | <span data-ttu-id="4fd2e-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="4fd2e-181">1.0.0</span></span> | <span data-ttu-id="4fd2e-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="4fd2e-182">4.3.0</span></span> |
| [<span data-ttu-id="4fd2e-183">認証</span><span class="sxs-lookup"><span data-stu-id="4fd2e-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="4fd2e-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="4fd2e-184">2.0.0</span></span> | <span data-ttu-id="4fd2e-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="4fd2e-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="4fd2e-186">適切なランタイムでプラグインを実行しています。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="4fd2e-187">Dotnet.exe のシナリオでは、NuGet のプラグインは、dotnet.exe の特定のランタイムで実行できる必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="4fd2e-188">互換性のある dotnet.exe/plugin 組み合わせが使用されているかどうかを確認するには、プラグインのプロバイダーとコンシューマーになります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="4fd2e-189">ユーザー場所プラグインと、たとえばで潜在的な問題が発生する可能性が、2.0 ランタイムの下の dotnet.exe 2.1 ランタイム用に記述されたプラグインを使用しようとします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="4fd2e-190">キャッシュ機能</span><span class="sxs-lookup"><span data-stu-id="4fd2e-190">Capabilities caching</span></span>

<span data-ttu-id="4fd2e-191">セキュリティ検証と、プラグインのインスタンス化は、コストのかかるのです。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="4fd2e-192">ダウンロード操作は、平均の NuGet ユーザーの認証プラグインをされている可能性がのみ認証の操作よりもずっと多く頻繁に発生します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="4fd2e-193">エクスペリエンスを向上させるのには、NuGet は指定された要求の操作要求をキャッシュします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="4fd2e-194">このキャッシュは、プラグインのパスをされているプラグインのキーを持つプラグインごと、および、この機能のキャッシュの有効期限は 30 日間。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="4fd2e-195">キャッシュにある`%LocalAppData%/NuGet/plugins-cache`環境変数でオーバーライドされると`NUGET_PLUGINS_CACHE_PATH`します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="4fd2e-196">これをオフにする[キャッシュ](../../consume-packages/managing-the-global-packages-and-cache-folders.md)、ローカル変数に 1 つ実行コマンドを`plugins-cache`オプション。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="4fd2e-197">`all` [ローカル] オプションは、プラグインのキャッシュも削除されますようになりました。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="4fd2e-198">プロトコル メッセージのインデックス</span><span class="sxs-lookup"><span data-stu-id="4fd2e-198">Protocol messages index</span></span>

<span data-ttu-id="4fd2e-199">プロトコル バージョン*1.0.0*メッセージ。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="4fd2e-200">閉じる</span><span class="sxs-lookup"><span data-stu-id="4fd2e-200">Close</span></span>
    * <span data-ttu-id="4fd2e-201">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4fd2e-202">要求にペイロードが含まれません</span><span class="sxs-lookup"><span data-stu-id="4fd2e-202">The request will contain no payload</span></span>
    * <span data-ttu-id="4fd2e-203">応答は発生しません。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-203">No response is expected.</span></span>  <span data-ttu-id="4fd2e-204">適切な応答は、プラグイン プロセスがすぐに終了するからです。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="4fd2e-205">パッケージ ファイルをコピーします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-205">Copy files in package</span></span>
    * <span data-ttu-id="4fd2e-206">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4fd2e-207">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-207">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-208">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-208">the package ID and version</span></span>
        * <span data-ttu-id="4fd2e-209">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-209">the package source repository location</span></span>
        * <span data-ttu-id="4fd2e-210">ターゲット ディレクトリのパス</span><span class="sxs-lookup"><span data-stu-id="4fd2e-210">destination directory path</span></span>
        * <span data-ttu-id="4fd2e-211">デプロイ先のディレクトリ パスにコピーするパッケージ内のファイルの列挙型</span><span class="sxs-lookup"><span data-stu-id="4fd2e-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="4fd2e-212">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-212">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-213">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4fd2e-214">操作が成功した場合は、保存先ディレクトリにコピーしたファイルの完全なパスの列挙型</span><span class="sxs-lookup"><span data-stu-id="4fd2e-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="4fd2e-215">パッケージ ファイルのコピー (.nupkg)</span><span class="sxs-lookup"><span data-stu-id="4fd2e-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="4fd2e-216">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4fd2e-217">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-217">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-218">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-218">the package ID and version</span></span>
        * <span data-ttu-id="4fd2e-219">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-219">the package source repository location</span></span>
        * <span data-ttu-id="4fd2e-220">コピー先のファイル パス</span><span class="sxs-lookup"><span data-stu-id="4fd2e-220">the destination file path</span></span>
    * <span data-ttu-id="4fd2e-221">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-221">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-222">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="4fd2e-223">資格情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-223">Get credentials</span></span>
    * <span data-ttu-id="4fd2e-224">方向の要求: プラグインは NuGet を -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="4fd2e-225">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-225">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-226">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-226">the package source repository location</span></span>
        * <span data-ttu-id="4fd2e-227">現在の資格情報を使用して、パッケージのソース リポジトリから取得した HTTP 状態コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="4fd2e-228">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-228">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-229">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4fd2e-230">使用可能な場合、ユーザー名</span><span class="sxs-lookup"><span data-stu-id="4fd2e-230">a username, if available</span></span>
        * <span data-ttu-id="4fd2e-231">使用可能な場合、パスワード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-231">a password, if available</span></span>

5.  <span data-ttu-id="4fd2e-232">パッケージ内のファイルを取得します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-232">Get files in package</span></span>
    * <span data-ttu-id="4fd2e-233">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4fd2e-234">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-234">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-235">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-235">the package ID and version</span></span>
        * <span data-ttu-id="4fd2e-236">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-236">the package source repository location</span></span>
    * <span data-ttu-id="4fd2e-237">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-237">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-238">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4fd2e-239">操作が成功した場合、パッケージ内のファイル パスの列挙型</span><span class="sxs-lookup"><span data-stu-id="4fd2e-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="4fd2e-240">操作の信頼性情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-240">Get operation claims</span></span> 
    * <span data-ttu-id="4fd2e-241">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4fd2e-242">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-242">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-243">パッケージ ソースのサービス index.json</span><span class="sxs-lookup"><span data-stu-id="4fd2e-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="4fd2e-244">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-244">the package source repository location</span></span>
    * <span data-ttu-id="4fd2e-245">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-245">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-246">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4fd2e-247">サポートされている操作の列挙型 (例:: パッケージのダウンロード)、操作が成功した場合。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="4fd2e-248">プラグインがパッケージ ソースをサポートしていない場合、プラグインがサポートされている操作の空のセットを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="4fd2e-249">このメッセージがバージョンに更新された*2.0.0*します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="4fd2e-250">旧バージョンとの互換性を保つため、クライアントになります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="4fd2e-251">パッケージ ハッシュを取得します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-251">Get package hash</span></span>
    * <span data-ttu-id="4fd2e-252">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4fd2e-253">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-253">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-254">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-254">the package ID and version</span></span>
        * <span data-ttu-id="4fd2e-255">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-255">the package source repository location</span></span>
        * <span data-ttu-id="4fd2e-256">ハッシュ アルゴリズム</span><span class="sxs-lookup"><span data-stu-id="4fd2e-256">the hash algorithm</span></span>
    * <span data-ttu-id="4fd2e-257">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-257">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-258">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4fd2e-259">操作が成功した場合は、要求されたハッシュ アルゴリズムを使用してパッケージ ファイルのハッシュ</span><span class="sxs-lookup"><span data-stu-id="4fd2e-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="4fd2e-260">パッケージのバージョンを取得します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-260">Get package versions</span></span>
    * <span data-ttu-id="4fd2e-261">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4fd2e-262">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-262">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-263">パッケージ ID</span><span class="sxs-lookup"><span data-stu-id="4fd2e-263">the package ID</span></span>
        * <span data-ttu-id="4fd2e-264">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-264">the package source repository location</span></span>
    * <span data-ttu-id="4fd2e-265">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-265">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-266">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4fd2e-267">操作が成功した場合、パッケージのバージョンの列挙型</span><span class="sxs-lookup"><span data-stu-id="4fd2e-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="4fd2e-268">サービス インデックスを取得します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-268">Get service index</span></span>
    * <span data-ttu-id="4fd2e-269">方向の要求: プラグインは NuGet を -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="4fd2e-270">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-270">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-271">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-271">the package source repository location</span></span>
    * <span data-ttu-id="4fd2e-272">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-272">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-273">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4fd2e-274">操作が成功した場合のサービス インデックス</span><span class="sxs-lookup"><span data-stu-id="4fd2e-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="4fd2e-275">ハンドシェイク</span><span class="sxs-lookup"><span data-stu-id="4fd2e-275">Handshake</span></span>
     * <span data-ttu-id="4fd2e-276">方向の要求: NuGet <> - プラグイン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="4fd2e-277">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-277">The request will contain:</span></span>
         * <span data-ttu-id="4fd2e-278">現在のプラグインのプロトコルのバージョン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="4fd2e-279">最小のサポートされているプラグイン プロトコルのバージョン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="4fd2e-280">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-280">A response will contain:</span></span>
         * <span data-ttu-id="4fd2e-281">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="4fd2e-282">操作が成功した場合は、ネゴシエートされたプロトコル バージョン。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="4fd2e-283">プラグインの終了エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="4fd2e-284">初期化します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-284">Initialize</span></span>
     * <span data-ttu-id="4fd2e-285">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4fd2e-286">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-286">The request will contain:</span></span>
         * <span data-ttu-id="4fd2e-287">バージョンの NuGet クライアント ツール</span><span class="sxs-lookup"><span data-stu-id="4fd2e-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="4fd2e-288">NuGet クライアント ツールの有効な言語です。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="4fd2e-289">これは、考慮 ForceEnglishOutput 設定、使用されている場合。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="4fd2e-290">プロトコルの既定値よりも優先される既定の要求のタイムアウト。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="4fd2e-291">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-291">A response will contain:</span></span>
         * <span data-ttu-id="4fd2e-292">操作の結果を示す応答コードを返します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="4fd2e-293">プラグインの終了エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="4fd2e-294">ログ</span><span class="sxs-lookup"><span data-stu-id="4fd2e-294">Log</span></span>
     * <span data-ttu-id="4fd2e-295">方向の要求: プラグインは NuGet を -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="4fd2e-296">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-296">The request will contain:</span></span>
         * <span data-ttu-id="4fd2e-297">要求のログ レベル</span><span class="sxs-lookup"><span data-stu-id="4fd2e-297">the log level for the request</span></span>
         * <span data-ttu-id="4fd2e-298">記録するメッセージ</span><span class="sxs-lookup"><span data-stu-id="4fd2e-298">a message to log</span></span>
     * <span data-ttu-id="4fd2e-299">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-299">A response will contain:</span></span>
         * <span data-ttu-id="4fd2e-300">操作の結果を示す応答コードを返します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="4fd2e-301">NuGet のプロセスの終了時を監視します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="4fd2e-302">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4fd2e-303">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-303">The request will contain:</span></span>
         * <span data-ttu-id="4fd2e-304">NuGet のプロセス ID</span><span class="sxs-lookup"><span data-stu-id="4fd2e-304">the NuGet process ID</span></span>
     * <span data-ttu-id="4fd2e-305">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-305">A response will contain:</span></span>
         * <span data-ttu-id="4fd2e-306">操作の結果を示す応答コードを返します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="4fd2e-307">パッケージをプリフェッチします。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-307">Prefetch package</span></span>
     * <span data-ttu-id="4fd2e-308">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4fd2e-309">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-309">The request will contain:</span></span>
         * <span data-ttu-id="4fd2e-310">パッケージ ID とバージョン</span><span class="sxs-lookup"><span data-stu-id="4fd2e-310">the package ID and version</span></span>
         * <span data-ttu-id="4fd2e-311">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-311">the package source repository location</span></span>
     * <span data-ttu-id="4fd2e-312">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-312">A response will contain:</span></span>
         * <span data-ttu-id="4fd2e-313">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="4fd2e-314">資格情報の設定</span><span class="sxs-lookup"><span data-stu-id="4fd2e-314">Set credentials</span></span>
     * <span data-ttu-id="4fd2e-315">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4fd2e-316">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-316">The request will contain:</span></span>
         * <span data-ttu-id="4fd2e-317">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-317">the package source repository location</span></span>
         * <span data-ttu-id="4fd2e-318">最後既知のパッケージ ソース名、使用可能な場合</span><span class="sxs-lookup"><span data-stu-id="4fd2e-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="4fd2e-319">最後既知のパッケージ ソース パスワード、使用可能な場合</span><span class="sxs-lookup"><span data-stu-id="4fd2e-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="4fd2e-320">使用可能な場合は最後の既知のプロキシ名</span><span class="sxs-lookup"><span data-stu-id="4fd2e-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="4fd2e-321">使用可能な場合は最後の既知のプロキシ パスワード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="4fd2e-322">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-322">A response will contain:</span></span>
         * <span data-ttu-id="4fd2e-323">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="4fd2e-324">ログ レベルの設定</span><span class="sxs-lookup"><span data-stu-id="4fd2e-324">Set log level</span></span>
     * <span data-ttu-id="4fd2e-325">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="4fd2e-326">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-326">The request will contain:</span></span>
         * <span data-ttu-id="4fd2e-327">既定のログ レベル</span><span class="sxs-lookup"><span data-stu-id="4fd2e-327">the default log level</span></span>
     * <span data-ttu-id="4fd2e-328">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-328">A response will contain:</span></span>
         * <span data-ttu-id="4fd2e-329">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="4fd2e-330">プロトコル バージョン*2.0.0*メッセージ</span><span class="sxs-lookup"><span data-stu-id="4fd2e-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="4fd2e-331">操作の信頼性情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-331">Get Operation Claims</span></span>

* <span data-ttu-id="4fd2e-332">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="4fd2e-333">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-333">The request will contain:</span></span>
        * <span data-ttu-id="4fd2e-334">パッケージ ソースのサービス index.json</span><span class="sxs-lookup"><span data-stu-id="4fd2e-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="4fd2e-335">パッケージ ソースのリポジトリ場所</span><span class="sxs-lookup"><span data-stu-id="4fd2e-335">the package source repository location</span></span>
    * <span data-ttu-id="4fd2e-336">応答が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-336">A response will contain:</span></span>
        * <span data-ttu-id="4fd2e-337">操作の結果を示す応答コード</span><span class="sxs-lookup"><span data-stu-id="4fd2e-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="4fd2e-338">操作が成功した場合、サポートされている操作の列挙型。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="4fd2e-339">プラグインがパッケージ ソースをサポートしていない場合、プラグインがサポートされている操作の空のセットを返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="4fd2e-340">サービス インデックスとパッケージ ソースが null の場合、このプラグインは、認証で応答できます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="4fd2e-341">認証の資格情報を取得します。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="4fd2e-342">方向の要求: NuGet プラグインを -></span><span class="sxs-lookup"><span data-stu-id="4fd2e-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="4fd2e-343">要求が含まれます。</span><span class="sxs-lookup"><span data-stu-id="4fd2e-343">The request will contain:</span></span>
    * <span data-ttu-id="4fd2e-344">URI</span><span class="sxs-lookup"><span data-stu-id="4fd2e-344">Uri</span></span>
    * <span data-ttu-id="4fd2e-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="4fd2e-345">isRetry</span></span>
    * <span data-ttu-id="4fd2e-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="4fd2e-346">NonInteractive</span></span>
    * <span data-ttu-id="4fd2e-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="4fd2e-347">CanShowDialog</span></span>
* <span data-ttu-id="4fd2e-348">応答には</span><span class="sxs-lookup"><span data-stu-id="4fd2e-348">A response will contain</span></span>
    * <span data-ttu-id="4fd2e-349">[ユーザー名]</span><span class="sxs-lookup"><span data-stu-id="4fd2e-349">Username</span></span>
    * <span data-ttu-id="4fd2e-350">[Password]</span><span class="sxs-lookup"><span data-stu-id="4fd2e-350">Password</span></span>
    * <span data-ttu-id="4fd2e-351">メッセージ</span><span class="sxs-lookup"><span data-stu-id="4fd2e-351">Message</span></span>
    * <span data-ttu-id="4fd2e-352">認証の種類の一覧</span><span class="sxs-lookup"><span data-stu-id="4fd2e-352">List of Auth Types</span></span>
    * <span data-ttu-id="4fd2e-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="4fd2e-353">MessageResponseCode</span></span>