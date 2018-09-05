---
title: nuget.exe 資格情報プロバイダー
description: nuget.exe 資格情報プロバイダーは、フィードで認証し、特定の規則に従うコマンドライン実行可能ファイルとして実装されます。
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550190"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="54219-103">Nuget.exe 資格情報プロバイダーでフィードの認証</span><span class="sxs-lookup"><span data-stu-id="54219-103">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="54219-104">*NuGet 3.3 以降*</span><span class="sxs-lookup"><span data-stu-id="54219-104">*NuGet 3.3+*</span></span>

<span data-ttu-id="54219-105">ときに`nuget.exe`フィードで認証する資格情報が必要で、次のように見えます。</span><span class="sxs-lookup"><span data-stu-id="54219-105">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="54219-106">NuGet は最初に資格情報で`Nuget.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="54219-106">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="54219-107">NuGet は、以下の順序に従って、プラグインの資格情報プロバイダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="54219-107">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="54219-108">(例であり、 [Visual Studio Team Services の資格情報プロバイダー](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider))。</span><span class="sxs-lookup"><span data-stu-id="54219-108">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="54219-109">NuGet は、そのコマンドラインで資格情報のユーザーを求めます。</span><span class="sxs-lookup"><span data-stu-id="54219-109">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="54219-110">ここで説明されている資格情報プロバイダーの機能でのみ注`nuget.exe`'dotnet restore' または Visual Studio ではなく、します。</span><span class="sxs-lookup"><span data-stu-id="54219-110">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="54219-111">Visual Studio を使用した資格情報プロバイダーは、次を参照してください[nuget.exe for Visual Studio の資格情報プロバイダー。](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="54219-111">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="54219-112">nuget.exe 資格情報プロバイダーは、3 つの方法で使用できます。</span><span class="sxs-lookup"><span data-stu-id="54219-112">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="54219-113">**グローバルに**: 資格情報プロバイダーのすべてのインスタンスを使用できるように`nuget.exe`を追加してください。 現在のユーザーのプロファイルの下で実行`%LocalAppData%\NuGet\CredentialProviders`します。</span><span class="sxs-lookup"><span data-stu-id="54219-113">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="54219-114">作成する必要があります、`CredentialProviders`フォルダー。</span><span class="sxs-lookup"><span data-stu-id="54219-114">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="54219-115">ルートにある資格情報プロバイダーをインストールすることができます、`CredentialProviders`フォルダーまたはサブフォルダー内。</span><span class="sxs-lookup"><span data-stu-id="54219-115">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="54219-116">資格情報プロバイダーに複数のファイル/アセンブリがある場合は、構成プロバイダーを保持するサブフォルダーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="54219-116">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="54219-117">**環境変数から**: 資格情報プロバイダーを任意の場所に格納しにアクセスできるように`nuget.exe`を設定して、`%NUGET_CREDENTIALPROVIDERS_PATH%`プロバイダーの場所を環境変数。</span><span class="sxs-lookup"><span data-stu-id="54219-117">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="54219-118">この変数は、セミコロンで区切ったリストを指定できます (たとえば、 `path1;path2`) 複数の場所がある場合。</span><span class="sxs-lookup"><span data-stu-id="54219-118">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="54219-119">**Nuget.exe と共に**: nuget.exe 資格情報プロバイダーと同じフォルダーに配置できる`nuget.exe`します。</span><span class="sxs-lookup"><span data-stu-id="54219-119">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="54219-120">資格情報のプロバイダーの読み込み時に`nuget.exe`という名前のファイルの順序で上記の場所を検索`credentialprovider*.exe`、後に記載してある順序でこれらのファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="54219-120">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="54219-121">複数の資格情報プロバイダーは、同じフォルダーに存在する場合は、アルファベット順に読み込まれています。</span><span class="sxs-lookup"><span data-stu-id="54219-121">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="54219-122">Nuget.exe 資格情報プロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="54219-122">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="54219-123">資格情報プロバイダーは、コマンドライン実行可能ファイル形式で名前`CredentialProvider*.exe`入力を収集、必要に応じて、資格情報を取得して、適切な終了ステータス コードと標準出力を返します。</span><span class="sxs-lookup"><span data-stu-id="54219-123">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="54219-124">プロバイダーでは、次の操作を行う必要があります。</span><span class="sxs-lookup"><span data-stu-id="54219-124">A provider must do the following:</span></span>

- <span data-ttu-id="54219-125">かどうかを対象となる URI の資格情報が提供資格情報の取得を開始する前に決定します。</span><span class="sxs-lookup"><span data-stu-id="54219-125">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="54219-126">必要でない場合は、状態コードを資格情報なしの 1 を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="54219-126">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="54219-127">変更しない`Nuget.Config`(など、資格情報の設定があります)。</span><span class="sxs-lookup"><span data-stu-id="54219-127">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="54219-128">としての独自の NuGet のハンドル HTTP プロキシの構成では、プラグインにプロキシ情報は提供されません。</span><span class="sxs-lookup"><span data-stu-id="54219-128">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="54219-129">資格情報またはエラーの詳細を返す`nuget.exe`標準出力に utf-8 エンコードを使用して JSON 応答オブジェクト (下記参照) を記述しています。</span><span class="sxs-lookup"><span data-stu-id="54219-129">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="54219-130">必要に応じて stderr に別のトレース ログを出力します。</span><span class="sxs-lookup"><span data-stu-id="54219-130">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="54219-131">シークレットする必要がありますこれまでに書き込まれません stderr、"normal"または「詳細」の詳細レベルでこのようなトレースは、コンソールにエコー NuGet ではあるためです。</span><span class="sxs-lookup"><span data-stu-id="54219-131">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="54219-132">NuGet の将来のバージョンと上位互換性を提供する、予期しないパラメーターを無視する必要があります。</span><span class="sxs-lookup"><span data-stu-id="54219-132">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="54219-133">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="54219-133">Input parameters</span></span>

| <span data-ttu-id="54219-134">パラメーターまたはスイッチ</span><span class="sxs-lookup"><span data-stu-id="54219-134">Parameter/Switch</span></span> |<span data-ttu-id="54219-135">説明</span><span class="sxs-lookup"><span data-stu-id="54219-135">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="54219-136">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="54219-136">Uri {value}</span></span> | <span data-ttu-id="54219-137">パッケージはソース URI が必要な資格情報です。</span><span class="sxs-lookup"><span data-stu-id="54219-137">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="54219-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="54219-138">NonInteractive</span></span> | <span data-ttu-id="54219-139">存在する場合、プロバイダーは対話型のプロンプトを発行しません。</span><span class="sxs-lookup"><span data-stu-id="54219-139">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="54219-140">IsRetry</span><span class="sxs-lookup"><span data-stu-id="54219-140">IsRetry</span></span> | <span data-ttu-id="54219-141">存在する場合、この試行が以前に失敗した試行の再試行をことを示します。</span><span class="sxs-lookup"><span data-stu-id="54219-141">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="54219-142">通常、プロバイダーではこのフラグを使用して、任意の既存のキャッシュをバイパスして、可能であれば新しい資格情報を要求できるようにします。</span><span class="sxs-lookup"><span data-stu-id="54219-142">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="54219-143">詳細度 {value}</span><span class="sxs-lookup"><span data-stu-id="54219-143">Verbosity {value}</span></span> | <span data-ttu-id="54219-144">存在する場合、次の値のいずれか:"normal"、「サイレント」または「詳細」。</span><span class="sxs-lookup"><span data-stu-id="54219-144">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="54219-145">値が指定されていない場合は、"normal"を既定値です。</span><span class="sxs-lookup"><span data-stu-id="54219-145">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="54219-146">プロバイダーはこれを使用しての省略可能なログ レベルを示す値として標準エラー ストリームに出力します。</span><span class="sxs-lookup"><span data-stu-id="54219-146">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="54219-147">終了コード</span><span class="sxs-lookup"><span data-stu-id="54219-147">Exit codes</span></span>

| <span data-ttu-id="54219-148">コード</span><span class="sxs-lookup"><span data-stu-id="54219-148">Code</span></span> |<span data-ttu-id="54219-149">結果</span><span class="sxs-lookup"><span data-stu-id="54219-149">Result</span></span> | <span data-ttu-id="54219-150">説明</span><span class="sxs-lookup"><span data-stu-id="54219-150">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="54219-151">0</span><span class="sxs-lookup"><span data-stu-id="54219-151">0</span></span> | <span data-ttu-id="54219-152">成功</span><span class="sxs-lookup"><span data-stu-id="54219-152">Success</span></span> | <span data-ttu-id="54219-153">資格情報が正常に取得された、stdout に書き込まれました。</span><span class="sxs-lookup"><span data-stu-id="54219-153">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="54219-154">1</span><span class="sxs-lookup"><span data-stu-id="54219-154">1</span></span> | <span data-ttu-id="54219-155">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="54219-155">ProviderNotApplicable</span></span> | <span data-ttu-id="54219-156">現在のプロバイダーでは、指定された uri の資格情報は提供されません。</span><span class="sxs-lookup"><span data-stu-id="54219-156">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="54219-157">2</span><span class="sxs-lookup"><span data-stu-id="54219-157">2</span></span> | <span data-ttu-id="54219-158">失敗</span><span class="sxs-lookup"><span data-stu-id="54219-158">Failure</span></span> | <span data-ttu-id="54219-159">プロバイダーが、指定された uri では、適切なプロバイダーが資格情報を提供することはできません。</span><span class="sxs-lookup"><span data-stu-id="54219-159">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="54219-160">この場合は、nuget.exe が認証を再試行しません、失敗します。</span><span class="sxs-lookup"><span data-stu-id="54219-160">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="54219-161">典型的な例は、ユーザーが対話型ログインをキャンセルするとします。</span><span class="sxs-lookup"><span data-stu-id="54219-161">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="54219-162">標準出力</span><span class="sxs-lookup"><span data-stu-id="54219-162">Standard output</span></span>

| <span data-ttu-id="54219-163">プロパティ</span><span class="sxs-lookup"><span data-stu-id="54219-163">Property</span></span> |<span data-ttu-id="54219-164">メモ</span><span class="sxs-lookup"><span data-stu-id="54219-164">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="54219-165">[ユーザー名]</span><span class="sxs-lookup"><span data-stu-id="54219-165">Username</span></span> | <span data-ttu-id="54219-166">認証された要求のユーザー名。</span><span class="sxs-lookup"><span data-stu-id="54219-166">Username for authenticated requests.</span></span>|
| <span data-ttu-id="54219-167">[Password]</span><span class="sxs-lookup"><span data-stu-id="54219-167">Password</span></span> | <span data-ttu-id="54219-168">認証された要求のパスワードです。</span><span class="sxs-lookup"><span data-stu-id="54219-168">Password for authenticated requests.</span></span>|
| <span data-ttu-id="54219-169">メッセージ</span><span class="sxs-lookup"><span data-stu-id="54219-169">Message</span></span> | <span data-ttu-id="54219-170">障害発生時の追加の詳細を表示するためだけに使用される、応答詳細を省略します。</span><span class="sxs-lookup"><span data-stu-id="54219-170">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="54219-171">例の標準出力:</span><span class="sxs-lookup"><span data-stu-id="54219-171">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="54219-172">資格情報プロバイダーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="54219-172">Troubleshooting a credential provider</span></span>

<span data-ttu-id="54219-173">現時点では、NuGet は、カスタム資格情報プロバイダーをデバッグするため多くダイレクトのサポートを提供しません[発行 4598](https://github.com/NuGet/Home/issues/4598)がこの作業を追跡します。</span><span class="sxs-lookup"><span data-stu-id="54219-173">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="54219-174">次の操作を実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="54219-174">You can also do the following:</span></span>

- <span data-ttu-id="54219-175">Nuget.exe の実行、`-verbosity`に詳しい出力を検査するスイッチ。</span><span class="sxs-lookup"><span data-stu-id="54219-175">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="54219-176">デバッグ メッセージを追加`stdout`適切な場所にします。</span><span class="sxs-lookup"><span data-stu-id="54219-176">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="54219-177">3.3 またはそれ以降の nuget.exe を使用していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="54219-177">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="54219-178">このコード スニペットにより、起動時にデバッガーをアタッチするには。</span><span class="sxs-lookup"><span data-stu-id="54219-178">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="54219-179">詳細については、[サポート リクエストを nuget.org 送信](https://www.nuget.org/policies/Contact)します。</span><span class="sxs-lookup"><span data-stu-id="54219-179">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
