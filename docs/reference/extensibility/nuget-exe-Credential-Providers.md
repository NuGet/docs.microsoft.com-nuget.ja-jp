---
title: nuget.exe資格情報プロバイダー
description: nuget.exe資格情報プロバイダーはフィードで認証され、特定の規則に従うコマンド ライン実行可能ファイルとして実装されます。
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323831"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="b62ab-103">資格情報プロバイダーを使用nuget.exeの認証</span><span class="sxs-lookup"><span data-stu-id="b62ab-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="b62ab-104">バージョンでは `3.3` 、特定の資格情報プロバイダーに `nuget.exe` 対するサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="b62ab-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="b62ab-105">それ以降、バージョンでは、すべてのコマンド ライン シナリオ (、、) で動作する資格情報プロバイダー `4.8` [](NuGet-Cross-Platform-Authentication-Plugin.md) `nuget.exe` `dotnet.exe` `msbuild.exe` のサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="b62ab-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="b62ab-106">すべての [認証方法の詳細については、「](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) 認証されたフィードからのパッケージの使用」を参照してください。 `nuget.exe`</span><span class="sxs-lookup"><span data-stu-id="b62ab-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="b62ab-107">nuget.exeプロバイダーの検出</span><span class="sxs-lookup"><span data-stu-id="b62ab-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="b62ab-108">nuget.exeプロバイダーは、次の 3 つの方法で使用できます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="b62ab-109">**グローバル:** 資格情報プロバイダーを現在のユーザーのプロファイルで実行のすべてのインスタンスで使用するには、 に `nuget.exe` 追加します `%LocalAppData%\NuGet\CredentialProviders` 。</span><span class="sxs-lookup"><span data-stu-id="b62ab-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="b62ab-110">フォルダーの作成が必要な場合 `CredentialProviders` があります。</span><span class="sxs-lookup"><span data-stu-id="b62ab-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="b62ab-111">資格情報プロバイダーは、フォルダーのルートまたはサブフォルダー `CredentialProviders`  内にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="b62ab-112">資格情報プロバイダーに複数のファイル/アセンブリがある場合は、サブフォルダーを使用してプロバイダーを整理することができます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="b62ab-113">**環境変数から:** 資格情報プロバイダーは、任意の場所に格納し、環境変数をプロバイダーの場所に設定することで `nuget.exe` `%NUGET_CREDENTIALPROVIDERS_PATH%` 、 にアクセスできます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="b62ab-114">複数の場所がある場合、この変数はセミコロンで区切られたリスト (例 `path1;path2` : ) にできます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="b62ab-115">**と共nuget.exe:** nuget.exe資格情報プロバイダーは、 と同じフォルダーに配置できます `nuget.exe` 。</span><span class="sxs-lookup"><span data-stu-id="b62ab-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="b62ab-116">資格情報プロバイダーを読み込むときに、上記の場所を順に検索し、 という名前のファイルを検索し、検出された順序でそれらのファイル `nuget.exe` `credentialprovider*.exe` を読み込めます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="b62ab-117">同じフォルダーに複数の資格情報プロバイダーが存在する場合は、アルファベット順に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="b62ab-118">資格情報プロバイダーnuget.exe作成する</span><span class="sxs-lookup"><span data-stu-id="b62ab-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="b62ab-119">資格情報プロバイダーは、 という形式のコマンド ライン実行可能ファイルです。入力を収集し、必要に応じて資格情報を取得し、適切な終了状態コードと標準出力を返 `CredentialProvider*.exe` します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="b62ab-120">プロバイダーは次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="b62ab-120">A provider must do the following:</span></span>

- <span data-ttu-id="b62ab-121">資格情報の取得を開始する前に、ターゲット URI の資格情報を提供できるかどうかを判断します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="b62ab-122">ない場合は、資格情報を使用しない状態コード 1 を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="b62ab-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="b62ab-123">変更しない `NuGet.Config` (資格情報の設定など)。</span><span class="sxs-lookup"><span data-stu-id="b62ab-123">Not modify `NuGet.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="b62ab-124">NuGet ではプラグインにプロキシ情報が提供されないので、HTTP プロキシ構成を独自に処理します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="b62ab-125">UTF-8 エンコードを使用して、JSON 応答オブジェクト (下記参照) を stdout に書き込み、資格情報またはエラーの詳細 `nuget.exe` を に返します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="b62ab-126">必要に応じて、追加のトレース ログを stderr に出力します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="b62ab-127">詳細レベルでは "通常" または "詳細" なトレースが NuGet によってコンソールにエコーされるので、シークレットを stderr に書き込む必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b62ab-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="b62ab-128">予期しないパラメーターは無視して、将来のバージョンの NuGet との前方互換性を提供する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b62ab-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="b62ab-129">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="b62ab-129">Input parameters</span></span>

| <span data-ttu-id="b62ab-130">パラメーター/スイッチ</span><span class="sxs-lookup"><span data-stu-id="b62ab-130">Parameter/Switch</span></span> |<span data-ttu-id="b62ab-131">説明</span><span class="sxs-lookup"><span data-stu-id="b62ab-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="b62ab-132">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="b62ab-132">Uri {value}</span></span> | <span data-ttu-id="b62ab-133">資格情報を必要とするパッケージ ソース URI。</span><span class="sxs-lookup"><span data-stu-id="b62ab-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="b62ab-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b62ab-134">NonInteractive</span></span> | <span data-ttu-id="b62ab-135">存在する場合、プロバイダーは対話型プロンプトを発行します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="b62ab-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="b62ab-136">IsRetry</span></span> | <span data-ttu-id="b62ab-137">存在する場合は、この試行が以前に失敗した試行の再試行を示します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="b62ab-138">プロバイダーは通常、このフラグを使用して、既存のキャッシュをバイパスし、可能であれば新しい資格情報を要求します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="b62ab-139">詳細度 {value}</span><span class="sxs-lookup"><span data-stu-id="b62ab-139">Verbosity {value}</span></span> | <span data-ttu-id="b62ab-140">存在する場合は、"normal"、"quiet"、または "detailed" のいずれかの値を指定します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="b62ab-141">値が指定されていない場合、既定値は "normal" になります。</span><span class="sxs-lookup"><span data-stu-id="b62ab-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="b62ab-142">プロバイダーは、標準エラー ストリームに出力するオプションのログ記録のレベルを示す値として、これを使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="b62ab-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="b62ab-143">終了コード</span><span class="sxs-lookup"><span data-stu-id="b62ab-143">Exit codes</span></span>

| <span data-ttu-id="b62ab-144">コード</span><span class="sxs-lookup"><span data-stu-id="b62ab-144">Code</span></span> |<span data-ttu-id="b62ab-145">結果</span><span class="sxs-lookup"><span data-stu-id="b62ab-145">Result</span></span> | <span data-ttu-id="b62ab-146">説明</span><span class="sxs-lookup"><span data-stu-id="b62ab-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="b62ab-147">0</span><span class="sxs-lookup"><span data-stu-id="b62ab-147">0</span></span> | <span data-ttu-id="b62ab-148">成功</span><span class="sxs-lookup"><span data-stu-id="b62ab-148">Success</span></span> | <span data-ttu-id="b62ab-149">資格情報が正常に取得され、stdout に書き込まれた。</span><span class="sxs-lookup"><span data-stu-id="b62ab-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="b62ab-150">1</span><span class="sxs-lookup"><span data-stu-id="b62ab-150">1</span></span> | <span data-ttu-id="b62ab-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="b62ab-151">ProviderNotApplicable</span></span> | <span data-ttu-id="b62ab-152">現在のプロバイダーは、指定された URI の資格情報を提供します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="b62ab-153">2</span><span class="sxs-lookup"><span data-stu-id="b62ab-153">2</span></span> | <span data-ttu-id="b62ab-154">障害</span><span class="sxs-lookup"><span data-stu-id="b62ab-154">Failure</span></span> | <span data-ttu-id="b62ab-155">プロバイダーは、指定された URI の正しいプロバイダーですが、資格情報を指定することはできません。</span><span class="sxs-lookup"><span data-stu-id="b62ab-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="b62ab-156">この場合、nuget.exe認証は再試行され、失敗します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="b62ab-157">一般的な例は、ユーザーが対話型ログインを取り消す場合です。</span><span class="sxs-lookup"><span data-stu-id="b62ab-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="b62ab-158">標準出力</span><span class="sxs-lookup"><span data-stu-id="b62ab-158">Standard output</span></span>

| <span data-ttu-id="b62ab-159">プロパティ</span><span class="sxs-lookup"><span data-stu-id="b62ab-159">Property</span></span> |<span data-ttu-id="b62ab-160">Notes</span><span class="sxs-lookup"><span data-stu-id="b62ab-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="b62ab-161">ユーザー名</span><span class="sxs-lookup"><span data-stu-id="b62ab-161">Username</span></span> | <span data-ttu-id="b62ab-162">認証された要求のユーザー名。</span><span class="sxs-lookup"><span data-stu-id="b62ab-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="b62ab-163">Password</span><span class="sxs-lookup"><span data-stu-id="b62ab-163">Password</span></span> | <span data-ttu-id="b62ab-164">認証された要求のパスワード。</span><span class="sxs-lookup"><span data-stu-id="b62ab-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="b62ab-165">Message</span><span class="sxs-lookup"><span data-stu-id="b62ab-165">Message</span></span> | <span data-ttu-id="b62ab-166">応答に関する省略可能な詳細。エラーが発生した場合に追加の詳細を表示するためにのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="b62ab-167">stdout の例:</span><span class="sxs-lookup"><span data-stu-id="b62ab-167">Example stdout:</span></span>

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="b62ab-168">資格情報プロバイダーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="b62ab-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="b62ab-169">現時点では、NuGet では、カスタム資格情報プロバイダーのデバッグを直接サポートする機能はあまり提供されていません。 [問題 4598](https://github.com/NuGet/Home/issues/4598) は、この作業を追跡しています。</span><span class="sxs-lookup"><span data-stu-id="b62ab-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="b62ab-170">次の操作を実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="b62ab-170">You can also do the following:</span></span>

- <span data-ttu-id="b62ab-171">スイッチnuget.exeを実行 `-verbosity` して、詳細な出力を検査します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="b62ab-172">適切な場所にデバッグ `stdout` メッセージを追加します。</span><span class="sxs-lookup"><span data-stu-id="b62ab-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="b62ab-173">3.3 以上のnuget.exeしてください。</span><span class="sxs-lookup"><span data-stu-id="b62ab-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="b62ab-174">次のコード スニペットを使用して、起動時にデバッガーをアタッチします。</span><span class="sxs-lookup"><span data-stu-id="b62ab-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
