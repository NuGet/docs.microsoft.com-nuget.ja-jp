---
title: "nuget.exe 資格情報プロバイダー |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 3cf592de-39f2-4e7f-a597-62635fdcedfa
description: "nuget.exe 資格情報プロバイダーを使用して、フィードを使用認証は、特定の規則に従うコマンドライン実行可能ファイルとして実装されます。"
keywords: "nuget.exe 資格情報プロバイダー、資格情報プロバイダー API をフィードでの認証、ギャラリーでの認証"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 82ab4d6e9be0736e008f5bd27d46e1db166d7bb4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a><span data-ttu-id="8c104-104">Nuget.exe 資格情報プロバイダーを使用したフィードの認証</span><span class="sxs-lookup"><span data-stu-id="8c104-104">Authenticating feeds with nuget.exe credential providers</span></span>

<span data-ttu-id="8c104-105">*NuGet 3.3 +*</span><span class="sxs-lookup"><span data-stu-id="8c104-105">*NuGet 3.3+*</span></span>

<span data-ttu-id="8c104-106">ときに`nuget.exe`フィードとは、認証する資格情報が必要に次のように検索します。</span><span class="sxs-lookup"><span data-stu-id="8c104-106">When `nuget.exe` needs credentials to authenticate with a feed, it looks for them in the following manner:</span></span>

1. <span data-ttu-id="8c104-107">NuGet は、資格情報に最初に`Nuget.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="8c104-107">NuGet first looks for credentials in `Nuget.Config` files.</span></span>
1. <span data-ttu-id="8c104-108">NuGet は、以下の順序に従って、プラグインの資格情報プロバイダーを使用します。</span><span class="sxs-lookup"><span data-stu-id="8c104-108">NuGet then uses plug-in credential providers, subject to the order given below.</span></span> <span data-ttu-id="8c104-109">(例、および、 [Visual Studio Team Services 資格情報プロバイダー](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider))。</span><span class="sxs-lookup"><span data-stu-id="8c104-109">(And example is the [Visual Studio Team Services Credential Provider](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)</span></span>
1. <span data-ttu-id="8c104-110">NuGet し、コマンドラインで資格情報をユーザーに求めます。</span><span class="sxs-lookup"><span data-stu-id="8c104-110">NuGet then prompts the user for credentials on the command line.</span></span>

<span data-ttu-id="8c104-111">ここで説明されている資格情報プロバイダーの機能でのみ注`nuget.exe`'dotnet restore' または Visual Studio ではなく、します。</span><span class="sxs-lookup"><span data-stu-id="8c104-111">Note that the credential providers described here work only in `nuget.exe` and not in 'dotnet restore' or Visual Studio.</span></span> <span data-ttu-id="8c104-112">Visual Studio での資格情報プロバイダーは、次を参照してください[nuget.exe for Visual Studio の資格情報プロバイダー。](nuget-credential-providers-for-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="8c104-112">For credential providers with Visual Studio, see [nuget.exe Credential Providers for Visual Studio](nuget-credential-providers-for-visual-studio.md)</span></span>

<span data-ttu-id="8c104-113">nuget.exe 資格情報プロバイダーは、3 つの方法で使用できます。</span><span class="sxs-lookup"><span data-stu-id="8c104-113">nuget.exe credential providers can be used in 3 ways:</span></span>

- <span data-ttu-id="8c104-114">**グローバル**: 資格情報プロバイダーのすべてのインスタンスに使用できるようにする`nuget.exe`に追加して、現在のユーザーのプロファイルの下で実行`%LocalAppData%\NuGet\CredentialProviders`です。</span><span class="sxs-lookup"><span data-stu-id="8c104-114">**Globally**: to make a credential provider available to all instances of `nuget.exe` run under the current user's profile, add it to `%LocalAppData%\NuGet\CredentialProviders`.</span></span> <span data-ttu-id="8c104-115">作成する必要があります、`CredentialProviders`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="8c104-115">You may need to create the `CredentialProviders` folder.</span></span> <span data-ttu-id="8c104-116">ルートにある資格情報プロバイダーをインストールすることができます、`CredentialProviders`フォルダーまたはサブフォルダー内にあります。</span><span class="sxs-lookup"><span data-stu-id="8c104-116">Credential providers can be installed at the root of the `CredentialProviders`  folder or within a subfolder.</span></span> <span data-ttu-id="8c104-117">資格情報プロバイダーに複数のファイルまたはアセンブリがある場合は、構成プロバイダーを保持するサブフォルダーを使用できます。</span><span class="sxs-lookup"><span data-stu-id="8c104-117">If a credential provider has multiple files/assemblies, you can use subfolders to keep the providers organized.</span></span>

- <span data-ttu-id="8c104-118">**環境変数から**: 資格情報プロバイダーを任意の場所に格納し、アクセスできるように`nuget.exe`を設定して、`%NUGET_CREDENTIALPROVIDERS_PATH%`プロバイダーの場所を環境変数。</span><span class="sxs-lookup"><span data-stu-id="8c104-118">**From an environment variable**: Credential providers can be stored anywhere and made accessible to `nuget.exe` by setting the `%NUGET_CREDENTIALPROVIDERS_PATH%` environment variable to the provider location.</span></span> <span data-ttu-id="8c104-119">この変数は、セミコロンで区切ったリストを指定できます (たとえば、 `path1;path2`) 複数の場所がある場合。</span><span class="sxs-lookup"><span data-stu-id="8c104-119">This variable can be a semicolon-separated list (for example, `path1;path2`) if you have multiple locations.</span></span>

- <span data-ttu-id="8c104-120">**Nuget.exe と共に**: nuget.exe 資格情報プロバイダーと同じフォルダーに配置できる`nuget.exe`です。</span><span class="sxs-lookup"><span data-stu-id="8c104-120">**Alongside nuget.exe**: nuget.exe credential providers can be placed in the same folder as `nuget.exe`.</span></span>

<span data-ttu-id="8c104-121">資格情報プロバイダーを読み込むときに`nuget.exe`という名前のファイルの順序で、上記の場所が検索`credentialprovider*.exe`、見つかったいる順序でそれらのファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="8c104-121">When loading credential providers, `nuget.exe` searches the above locations, in order, for any file named `credentialprovider*.exe`, then loads those files in the order they're found.</span></span> <span data-ttu-id="8c104-122">複数の資格情報プロバイダーは、同じフォルダーに存在する場合は、アルファベット順に読み込まれています。</span><span class="sxs-lookup"><span data-stu-id="8c104-122">If multiple credential providers exist in the same folder, they're loaded in alphabetical order.</span></span>

## <a name="creating-a-nugetexe-credential-provider"></a><span data-ttu-id="8c104-123">Nuget.exe 資格情報プロバイダーを作成します。</span><span class="sxs-lookup"><span data-stu-id="8c104-123">Creating a nuget.exe credential provider</span></span>

<span data-ttu-id="8c104-124">資格情報プロバイダーは、コマンドラインの実行可能ファイル形式で名前付き`CredentialProvider*.exe`入力の収集、必要に応じて、資格情報を取得して、適切な終了ステータス コードと標準出力を返します。</span><span class="sxs-lookup"><span data-stu-id="8c104-124">A credential provider is a command-line executable, named in the form `CredentialProvider*.exe`, that gathers inputs, acquires credentials as appropriate, and then returns the appropriate exit status code and standard output.</span></span>

<span data-ttu-id="8c104-125">プロバイダーでは、次の操作を行います必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c104-125">A provider must do the following:</span></span>

- <span data-ttu-id="8c104-126">かどうか、資格情報を入力、対象となる URI の資格情報の取得を開始する前に決定します。</span><span class="sxs-lookup"><span data-stu-id="8c104-126">Determine whether it can provide credentials for the targeted URI before initiating credential acquisition.</span></span> <span data-ttu-id="8c104-127">それ以外の場合は、状態コード資格情報を持たない 1 を返す必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c104-127">If not, it should return status code 1 with no credentials.</span></span>
- <span data-ttu-id="8c104-128">変更しない`Nuget.Config`(など、資格情報の設定があります)。</span><span class="sxs-lookup"><span data-stu-id="8c104-128">Not modify `Nuget.Config` (such as setting credentials there).</span></span>
- <span data-ttu-id="8c104-129">としての独自の NuGet のハンドル HTTP プロキシの構成は、プラグインをプロキシ情報を提供しません。</span><span class="sxs-lookup"><span data-stu-id="8c104-129">Handle HTTP proxy configuration on its own, as NuGet does not provide proxy information to the plugin.</span></span>
- <span data-ttu-id="8c104-130">資格情報またはエラーの詳細を返す`nuget.exe`を標準出力に utf-8 エンコードを使用して JSON 応答オブジェクト (下記参照) を記述します。</span><span class="sxs-lookup"><span data-stu-id="8c104-130">Return credentials or error details to `nuget.exe` by writing a JSON response object (see below) to stdout, using UTF-8 encoding.</span></span>
- <span data-ttu-id="8c104-131">必要に応じて stderr への追加のトレース ログを出力します。</span><span class="sxs-lookup"><span data-stu-id="8c104-131">Optionally emit additional trace logging to stderr.</span></span> <span data-ttu-id="8c104-132">シークレットこれまでに書き込むかない stderr、"normal"または「詳細」の詳細レベルでこれらのトレースは、NuGet によって、コンソールにエコーためです。</span><span class="sxs-lookup"><span data-stu-id="8c104-132">No secrets should ever be written to stderr, since at verbosity levels "normal" or "detailed" such traces are echoed by NuGet to the console.</span></span>
- <span data-ttu-id="8c104-133">NuGet の将来のバージョンとの上位互換性を提供する、予期しないパラメーターを無視する必要があります。</span><span class="sxs-lookup"><span data-stu-id="8c104-133">Unexpected parameters should be ignored, providing forward compatibility with future versions of NuGet.</span></span>

### <a name="input-parameters"></a><span data-ttu-id="8c104-134">入力パラメーター</span><span class="sxs-lookup"><span data-stu-id="8c104-134">Input parameters</span></span>

| <span data-ttu-id="8c104-135">パラメーターまたはスイッチ</span><span class="sxs-lookup"><span data-stu-id="8c104-135">Parameter/Switch</span></span> |<span data-ttu-id="8c104-136">説明</span><span class="sxs-lookup"><span data-stu-id="8c104-136">Description</span></span>|
|----------------|-----------|
| <span data-ttu-id="8c104-137">Uri {value}</span><span class="sxs-lookup"><span data-stu-id="8c104-137">Uri {value}</span></span> | <span data-ttu-id="8c104-138">パッケージ ソース URI が必要な資格情報。</span><span class="sxs-lookup"><span data-stu-id="8c104-138">The package source URI requiring credentials.</span></span>|
| <span data-ttu-id="8c104-139">非対話型</span><span class="sxs-lookup"><span data-stu-id="8c104-139">NonInteractive</span></span> | <span data-ttu-id="8c104-140">存在する場合、プロバイダーは対話型のプロンプトを発行しません。</span><span class="sxs-lookup"><span data-stu-id="8c104-140">If present, provider does not issue interactive prompts.</span></span> |
| <span data-ttu-id="8c104-141">IsRetry</span><span class="sxs-lookup"><span data-stu-id="8c104-141">IsRetry</span></span> | <span data-ttu-id="8c104-142">存在する場合、この試行が以前に失敗した試行の再試行ことを示します。</span><span class="sxs-lookup"><span data-stu-id="8c104-142">If present, indicates that this attempt is a retry of a previously failed attempt.</span></span> <span data-ttu-id="8c104-143">プロバイダーは、このフラグを使用して通常、任意の既存のキャッシュをバイパスし、可能であれば新しい資格情報の入力を求めることを確認してください。</span><span class="sxs-lookup"><span data-stu-id="8c104-143">Providers typically use this flag to ensure that they bypass any existing cache and prompt for new credentials if possible.</span></span>|
| <span data-ttu-id="8c104-144">詳細度 {value}</span><span class="sxs-lookup"><span data-stu-id="8c104-144">Verbosity {value}</span></span> | <span data-ttu-id="8c104-145">存在する場合、次の値のいずれかの:"normal"、「サイレント」または「詳細」です。</span><span class="sxs-lookup"><span data-stu-id="8c104-145">If present, one of the following values: "normal", "quiet", or "detailed".</span></span> <span data-ttu-id="8c104-146">値が指定されていない場合は、"normal"に既定値です。</span><span class="sxs-lookup"><span data-stu-id="8c104-146">If no value is supplied, defaults to "normal".</span></span> <span data-ttu-id="8c104-147">プロバイダーとして使用してくださいこれの省略可能なログ レベルを示す値を標準エラー ストリームに出力します。</span><span class="sxs-lookup"><span data-stu-id="8c104-147">Providers should use this as an indication of the level of optional logging to emit to the standard error stream.</span></span> |

### <a name="exit-codes"></a><span data-ttu-id="8c104-148">終了コード</span><span class="sxs-lookup"><span data-stu-id="8c104-148">Exit codes</span></span>

| <span data-ttu-id="8c104-149">コード</span><span class="sxs-lookup"><span data-stu-id="8c104-149">Code</span></span> |<span data-ttu-id="8c104-150">結果</span><span class="sxs-lookup"><span data-stu-id="8c104-150">Result</span></span> | <span data-ttu-id="8c104-151">説明</span><span class="sxs-lookup"><span data-stu-id="8c104-151">Description</span></span> |
|----------------|-----------|-----------|
| <span data-ttu-id="8c104-152">0</span><span class="sxs-lookup"><span data-stu-id="8c104-152">0</span></span> | <span data-ttu-id="8c104-153">成功</span><span class="sxs-lookup"><span data-stu-id="8c104-153">Success</span></span> | <span data-ttu-id="8c104-154">資格情報は、正常に取得された、stdout に書き込まれています。</span><span class="sxs-lookup"><span data-stu-id="8c104-154">Credentials were successfully acquired and have been written to stdout.</span></span>|
| <span data-ttu-id="8c104-155">1</span><span class="sxs-lookup"><span data-stu-id="8c104-155">1</span></span> | <span data-ttu-id="8c104-156">ProviderNotApplicable</span><span class="sxs-lookup"><span data-stu-id="8c104-156">ProviderNotApplicable</span></span> | <span data-ttu-id="8c104-157">現在のプロバイダーは、指定された URI の資格情報を提供していません。</span><span class="sxs-lookup"><span data-stu-id="8c104-157">The current provider does not provide credentials for the given URI.</span></span>|
| <span data-ttu-id="8c104-158">2</span><span class="sxs-lookup"><span data-stu-id="8c104-158">2</span></span> | <span data-ttu-id="8c104-159">失敗</span><span class="sxs-lookup"><span data-stu-id="8c104-159">Failure</span></span> | <span data-ttu-id="8c104-160">プロバイダーは、適切なプロバイダー、指定された uri が、資格情報を提供することはできません。</span><span class="sxs-lookup"><span data-stu-id="8c104-160">The provider is the correct provider for the given URI, but cannot provide credentials.</span></span> <span data-ttu-id="8c104-161">この場合、nuget.exe は認証実行は再試行されませんしは失敗します。</span><span class="sxs-lookup"><span data-stu-id="8c104-161">In this case, nuget.exe will not retry authentication and will fail.</span></span> <span data-ttu-id="8c104-162">典型的な例は、ユーザーが対話型ログインをキャンセルするとします。</span><span class="sxs-lookup"><span data-stu-id="8c104-162">A typical example is when a user cancels an interactive login.</span></span> |

### <a name="standard-output"></a><span data-ttu-id="8c104-163">標準出力</span><span class="sxs-lookup"><span data-stu-id="8c104-163">Standard output</span></span>

| <span data-ttu-id="8c104-164">プロパティ</span><span class="sxs-lookup"><span data-stu-id="8c104-164">Property</span></span> |<span data-ttu-id="8c104-165">メモ</span><span class="sxs-lookup"><span data-stu-id="8c104-165">Notes</span></span>|
|----------------|-----------|
| <span data-ttu-id="8c104-166">ユーザー名</span><span class="sxs-lookup"><span data-stu-id="8c104-166">Username</span></span> | <span data-ttu-id="8c104-167">認証された要求のユーザー名。</span><span class="sxs-lookup"><span data-stu-id="8c104-167">Username for authenticated requests.</span></span>|
| <span data-ttu-id="8c104-168">パスワード</span><span class="sxs-lookup"><span data-stu-id="8c104-168">Password</span></span> | <span data-ttu-id="8c104-169">認証された要求のパスワードです。</span><span class="sxs-lookup"><span data-stu-id="8c104-169">Password for authenticated requests.</span></span>|
| <span data-ttu-id="8c104-170">メッセージ</span><span class="sxs-lookup"><span data-stu-id="8c104-170">Message</span></span> | <span data-ttu-id="8c104-171">失敗した場合の詳細を表示するためだけに使用される、応答の省略可能な詳細はします。</span><span class="sxs-lookup"><span data-stu-id="8c104-171">Optional details about the response, used only to show additional details in failure cases.</span></span> |

<span data-ttu-id="8c104-172">例の標準出力:</span><span class="sxs-lookup"><span data-stu-id="8c104-172">Example stdout:</span></span>

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a><span data-ttu-id="8c104-173">資格情報プロバイダーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="8c104-173">Troubleshooting a credential provider</span></span>

<span data-ttu-id="8c104-174">現時点では、NuGet は、カスタム資格情報のプロバイダーのデバッグの程度を直接サポートを提供しません[発行 4598](https://github.com/NuGet/Home/issues/4598)がこの作業を追跡します。</span><span class="sxs-lookup"><span data-stu-id="8c104-174">At present, NuGet doesn't provide much direct support for debugging custom credential providers; [issue 4598](https://github.com/NuGet/Home/issues/4598) is tracking this work.</span></span>

<span data-ttu-id="8c104-175">次の操作を実行することもできます。</span><span class="sxs-lookup"><span data-stu-id="8c104-175">You can also do the following:</span></span>

- <span data-ttu-id="8c104-176">Nuget.exe での実行、`-verbosity`に詳しい出力を検査するスイッチです。</span><span class="sxs-lookup"><span data-stu-id="8c104-176">Run nuget.exe with the `-verbosity` switch to inspect detailed output.</span></span>
- <span data-ttu-id="8c104-177">デバッグ メッセージを追加`stdout`適切な場所にします。</span><span class="sxs-lookup"><span data-stu-id="8c104-177">Add debug messages to `stdout` in appropriate places.</span></span>
- <span data-ttu-id="8c104-178">Nuget.exe 3.3 またはそれ以降を使用していることを確認します。</span><span class="sxs-lookup"><span data-stu-id="8c104-178">Be sure that you're using nuget.exe 3.3 or higher.</span></span>
- <span data-ttu-id="8c104-179">このコード スニペットの起動時にデバッガーをアタッチします。</span><span class="sxs-lookup"><span data-stu-id="8c104-179">Attach debugger on startup with this code snippet:</span></span>

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

<span data-ttu-id="8c104-180">詳細については、[要求を送信するサポート、nuget.org](https://www.nuget.org/policies/Contact)です。</span><span class="sxs-lookup"><span data-stu-id="8c104-180">For further help, [submit a support request a nuget.org](https://www.nuget.org/policies/Contact).</span></span>
