---
title: nuget.exe 資格情報プロバイダー
description: nuget.exe 資格情報プロバイダーはフィードで認証され、特定の規則に従うコマンドライン実行可能ファイルとして実装されます。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428301"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="1d8c3-103">Nuget.exe 資格情報プロバイダーを使用したフィードの認証</span><span class="sxs-lookup"><span data-stu-id="1d8c3-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="1d8c3-104">バージョン `3.3` `nuget.exe` 特定の資格情報プロバイダーのサポートが追加されました。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-104">In version `3.3` support was added for `nuget.exe` specific credential providers.</span></span> <span data-ttu-id="1d8c3-105">その後、バージョン `4.8` では、すべてのコマンドラインシナリオ (`nuget.exe`、`dotnet.exe`、`msbuild.exe`) で機能する[資格情報プロバイダーのサポート](NuGet-Cross-Platform-Authentication-Plugin.md)が追加されました。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-105">Since then, in version `4.8` [support for credential providers](NuGet-Cross-Platform-Authentication-Plugin.md) that work across all command line scenarios (`nuget.exe`, `dotnet.exe`, `msbuild.exe`) was added.</span></span>

<span data-ttu-id="1d8c3-106">`nuget.exe` のすべての認証方法の詳細については、「認証された[フィードからのパッケージ](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)の使用」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-106">See [Consuming Packages from authenticated feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) for more details on all authentication approaches for `nuget.exe`</span></span>

## <a name="nugetexe-credential-provider-discovery"></a><span data-ttu-id="1d8c3-107">nuget.exe 資格情報プロバイダーの検出</span><span class="sxs-lookup"><span data-stu-id="1d8c3-107">nuget.exe credential provider discovery</span></span>

<span data-ttu-id="1d8c3-108">nuget.exe 資格情報プロバイダーは、次の3つの方法で使用できます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-108">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="1d8c3-109">**グローバル**: 現在のユーザーのプロファイルで実行 `nuget.exe` のすべてのインスタンスで資格情報プロバイダーを使用できるようにするには、それを `%LocalAppData%\NuGet\CredentialProviders`に追加します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-109">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="1d8c3-110">`CredentialProviders` フォルダーの作成が必要になる場合があります。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-110">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="1d8c3-111">資格情報プロバイダーは、`CredentialProviders` フォルダーのルートまたはサブフォルダー内にインストールできます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-111">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="1d8c3-112">資格情報プロバイダーに複数のファイル/アセンブリがある場合は、サブフォルダーを使用して、プロバイダーを整理したままにすることができます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-112">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="1d8c3-113">**環境変数から**: 資格情報プロバイダーを任意の場所に格納し、`nuget.exe` にアクセスできるようにするには、`%NUGET_CREDENTIALPROVIDERS_PATH%` 環境変数をプロバイダーの場所に設定します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-113">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="1d8c3-114">複数の場所がある場合は、この変数をセミコロンで区切ったリスト (`path1;path2`など) にすることができます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-114">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="1d8c3-115">**Nuget.exe と共**に、nuget.exe 資格情報プロバイダーを `nuget.exe`と同じフォルダーに配置できます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-115">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="1d8c3-116">資格情報プロバイダーを読み込むときに、`nuget.exe` は `credentialprovider*.exe`という名前のファイルについて、上記の場所を順に検索し、見つかった順にそれらのファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-116">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="1d8c3-117">複数の資格情報プロバイダーが同じフォルダーに存在する場合は、アルファベット順に読み込まれます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-117">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="1d8c3-118">Nuget.exe 資格情報プロバイダーを作成する</span><span class="sxs-lookup"><span data-stu-id="1d8c3-118">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="1d8c3-119">資格情報プロバイダーは、`CredentialProvider*.exe`という形式で指定されたコマンドライン実行可能ファイルで、入力を収集し、必要に応じて資格情報を取得して、適切な終了ステータスコードと標準出力を返します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-119">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="1d8c3-120">プロバイダーは次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-120">A provider must do the following:</span></span>

- <span data-ttu-id="1d8c3-121">資格情報の取得を開始する前に、対象の URI の資格情報を提供できるかどうかを判断します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-121">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="1d8c3-122">そうでない場合は、資格情報なしのステータスコード1が返されます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-122">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="1d8c3-123">`Nuget.Config` を変更しません (ここで資格情報を設定するなど)。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-123">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="1d8c3-124">NuGet がプラグインにプロキシ情報を提供しないため、HTTP プロキシの構成を独自に処理します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-124">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="1d8c3-125">UTF-8 エンコーディングを使用して、JSON 応答オブジェクト (下記参照) を stdout に書き込むことによって、資格情報またはエラーの詳細を `nuget.exe` に返します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-125">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="1d8c3-126">必要に応じて、追加のトレースログを stderr に出力します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-126">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="1d8c3-127">詳細レベルの "標準" または "詳細" のトレースが NuGet によってコンソールにエコーされるため、stderr にシークレットを書き出す必要はありません。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-127">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="1d8c3-128">将来のバージョンの NuGet との上位互換性を提供するため、予期しないパラメーターは無視する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-128">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="1d8c3-129">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="1d8c3-129">Input parameters</span></span>

| <span data-ttu-id="1d8c3-130">パラメーター/スイッチ</span><span class="sxs-lookup"><span data-stu-id="1d8c3-130">Parameter/Switch</span></span> |<span data-ttu-id="1d8c3-131">説明</span><span class="sxs-lookup"><span data-stu-id="1d8c3-131">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="1d8c3-132">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="1d8c3-132">Uri {value}</span></span> | <span data-ttu-id="1d8c3-133">資格情報を必要とするパッケージソース URI。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-133">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="1d8c3-134">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1d8c3-134">NonInteractive</span></span> | <span data-ttu-id="1d8c3-135">存在する場合、プロバイダーは対話型プロンプトを発行しません。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-135">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="1d8c3-136">IsRetry</span><span class="sxs-lookup"><span data-stu-id="1d8c3-136">IsRetry</span></span> | <span data-ttu-id="1d8c3-137">存在する場合は、この試行が前回失敗した試行の再試行であることを示します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-137">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="1d8c3-138">通常、プロバイダーはこのフラグを使用して、既存のキャッシュをバイパスし、可能であれば新しい資格情報の入力を求めます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-138">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="1d8c3-139">Verbosity {value}</span><span class="sxs-lookup"><span data-stu-id="1d8c3-139">Verbosity {value}</span></span> | <span data-ttu-id="1d8c3-140">存在する場合は、"normal"、"quiet"、または "detailed" のいずれかの値を指定します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-140">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="1d8c3-141">値が指定されていない場合、は既定で "normal" になります。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-141">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="1d8c3-142">プロバイダーはこれを、標準エラーストリームに出力するオプションのログ記録のレベルを示す値として使用する必要があります。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-142">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="1d8c3-143">終了コード</span><span class="sxs-lookup"><span data-stu-id="1d8c3-143">Exit codes</span></span>

| <span data-ttu-id="1d8c3-144">コード</span><span class="sxs-lookup"><span data-stu-id="1d8c3-144">Code</span></span> |<span data-ttu-id="1d8c3-145">結果</span><span class="sxs-lookup"><span data-stu-id="1d8c3-145">Result</span></span> | <span data-ttu-id="1d8c3-146">説明</span><span class="sxs-lookup"><span data-stu-id="1d8c3-146">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="1d8c3-147">0</span><span class="sxs-lookup"><span data-stu-id="1d8c3-147">0</span></span> | <span data-ttu-id="1d8c3-148">成功</span><span class="sxs-lookup"><span data-stu-id="1d8c3-148">Success</span></span> | <span data-ttu-id="1d8c3-149">資格情報が正常に取得され、stdout に書き込まれました。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-149">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="1d8c3-150">1</span><span class="sxs-lookup"><span data-stu-id="1d8c3-150">1</span></span> | <span data-ttu-id="1d8c3-151">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="1d8c3-151">ProviderNotApplicable</span></span> | <span data-ttu-id="1d8c3-152">現在のプロバイダーは、指定された URI の資格情報を提供しません。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-152">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="1d8c3-153">2</span><span class="sxs-lookup"><span data-stu-id="1d8c3-153">2</span></span> | <span data-ttu-id="1d8c3-154">障害</span><span class="sxs-lookup"><span data-stu-id="1d8c3-154">Failure</span></span> | <span data-ttu-id="1d8c3-155">プロバイダーは、指定された URI の正しいプロバイダーですが、資格情報を提供することはできません。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-155">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="1d8c3-156">この場合、nuget.exe は認証を再試行せず、失敗します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-156">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="1d8c3-157">一般的な例として、ユーザーが対話型ログインをキャンセルした場合があります。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-157">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="1d8c3-158">標準出力</span><span class="sxs-lookup"><span data-stu-id="1d8c3-158">Standard output</span></span>

| <span data-ttu-id="1d8c3-159">プロパティ</span><span class="sxs-lookup"><span data-stu-id="1d8c3-159">Property</span></span> |<span data-ttu-id="1d8c3-160">説明</span><span class="sxs-lookup"><span data-stu-id="1d8c3-160">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="1d8c3-161">ユーザー名</span><span class="sxs-lookup"><span data-stu-id="1d8c3-161">Username</span></span> | <span data-ttu-id="1d8c3-162">認証された要求のユーザー名。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-162">Username for authenticated requests.</span></span>|
| <span data-ttu-id="1d8c3-163">Password</span><span class="sxs-lookup"><span data-stu-id="1d8c3-163">Password</span></span> | <span data-ttu-id="1d8c3-164">認証された要求のパスワード。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-164">Password for authenticated requests.</span></span>|
| <span data-ttu-id="1d8c3-165">Message</span><span class="sxs-lookup"><span data-stu-id="1d8c3-165">Message</span></span> | <span data-ttu-id="1d8c3-166">応答に関するオプションの詳細。失敗した場合に追加の詳細を表示するためにのみ使用されます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-166">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="1d8c3-167">Stdout の例:</span><span class="sxs-lookup"><span data-stu-id="1d8c3-167">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="1d8c3-168">資格情報プロバイダーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="1d8c3-168">Troubleshooting a credential provider</span></span>

<span data-ttu-id="1d8c3-169">現時点では、NuGet はカスタム資格情報プロバイダーをデバッグするための直接的なサポートを提供していません。[問題 4598](https://github.com/NuGet/Home/issues/4598)はこの作業を追跡しています。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-169">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="1d8c3-170">次の操作を行うこともできます。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-170">You can also do the following:</span></span>

- <span data-ttu-id="1d8c3-171">`-verbosity` スイッチを使用して nuget.exe を実行し、詳細な出力を検査します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-171">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="1d8c3-172">適切な場所で `stdout` にデバッグメッセージを追加します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-172">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="1d8c3-173">Nuget.exe 3.3 以降を使用していることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-173">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="1d8c3-174">起動時にデバッガーをアタッチするには、次のコードスニペットを使用します。</span><span class="sxs-lookup"><span data-stu-id="1d8c3-174">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
