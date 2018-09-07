---
title: NuGet でグローバル パッケージ、キャッシュ、一時フォルダーを管理する方法
description: パッケージをインストール、復元、および更新するときに使用される、コンピューター上に存在するグローバル パッケージ インストール フォルダー、パッケージ キャッシュ、および一時フォルダーを管理する方法
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: c547ae1d46079d040d7c3aa4c7678e70cd199dce
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548014"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a><span data-ttu-id="7823e-103">グローバル パッケージ、キャッシュ、および一時フォルダーを管理する</span><span class="sxs-lookup"><span data-stu-id="7823e-103">Managing the global packages, cache, and temp folders</span></span>

<span data-ttu-id="7823e-104">NuGet では、パッケージのインストール、更新、または復元を行う場合は常に、プロジェクト構造の外にある複数のフォルダーで、以下のようなパッケージとパッケージ情報を管理します。</span><span class="sxs-lookup"><span data-stu-id="7823e-104">Whenever you install, update, or restore a package, NuGet manages packages and package information in several folders outside of your project structure:</span></span>

| <span data-ttu-id="7823e-105">name</span><span class="sxs-lookup"><span data-stu-id="7823e-105">Name</span></span> | <span data-ttu-id="7823e-106">説明および場所 (ユーザーごと)</span><span class="sxs-lookup"><span data-stu-id="7823e-106">Description and Location (per user)</span></span>|
| --- | --- |
| <span data-ttu-id="7823e-107">global&#8209;packages</span><span class="sxs-lookup"><span data-stu-id="7823e-107">global&#8209;packages</span></span> | <span data-ttu-id="7823e-108">"*グローバル パッケージ*" フォルダーは、ダウンロードされた任意のパッケージが NuGet でインストールされる場所です。</span><span class="sxs-lookup"><span data-stu-id="7823e-108">The *global-packages* folder is where NuGet installs any downloaded package.</span></span> <span data-ttu-id="7823e-109">各パッケージは、パッケージ ID とバージョン番号と一致するサブフォルダーに完全に展開されます。</span><span class="sxs-lookup"><span data-stu-id="7823e-109">Each package is fully expanded into a subfolder that matches the package identifier and version number.</span></span> <span data-ttu-id="7823e-110">PackageReference 形式を使用するプロジェクトは常に、このフォルダーから直接パッケージを使用します。</span><span class="sxs-lookup"><span data-stu-id="7823e-110">Projects using the PackageReference format always use packages directly from this folder.</span></span> <span data-ttu-id="7823e-111">`packages.config` を使用する場合、パッケージは "*グローバル パッケージ*" フォルダーにインストールされ、プロジェクトの `packages` フォルダーにコピーされます。</span><span class="sxs-lookup"><span data-stu-id="7823e-111">When using the `packages.config`, packages are installed to the *global-packages* folder, then copied into the project's `packages` folder.</span></span><br/><ul><li><span data-ttu-id="7823e-112">Windows: `%userprofile%\.nuget\packages`</span><span class="sxs-lookup"><span data-stu-id="7823e-112">Windows: `%userprofile%\.nuget\packages`</span></span></li><li><span data-ttu-id="7823e-113">Mac/Linux: `~/.nuget/packages`</span><span class="sxs-lookup"><span data-stu-id="7823e-113">Mac/Linux: `~/.nuget/packages`</span></span></li><li><span data-ttu-id="7823e-114">NUGET_PACKAGES 環境変数、`globalPackagesFolder`または `repositoryPath`[構成設定](../reference/nuget-config-file.md#config-section) (それぞれ、PackageReference および `packages.config` を使用している場合)、あるいは `RestorePackagesPath` MSBuild プロパティ (MSBuild のみ) を使用して、オーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="7823e-114">Override using the NUGET_PACKAGES environment variable, the `globalPackagesFolder` or `repositoryPath` [configuration settings](../reference/nuget-config-file.md#config-section) (when using PackageReference and `packages.config`, respectively), or the `RestorePackagesPath` MSBuild property (MSBuild only).</span></span> <span data-ttu-id="7823e-115">環境変数は、構成設定よりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="7823e-115">The environment variable takes precedence over the configuration setting.</span></span></li></ul> |
| <span data-ttu-id="7823e-116">http&#8209;cache</span><span class="sxs-lookup"><span data-stu-id="7823e-116">http&#8209;cache</span></span> | <span data-ttu-id="7823e-117">Visual Studio パッケージ マネージャー (NuGet 3.x 以降) および `dotnet` ツールでは、ダウンロードしたパッケージのコピーをこのキャッシュに格納し (`.dat` ファイルとして保存)、各パッケージ ソースのサブフォルダーに整理します。</span><span class="sxs-lookup"><span data-stu-id="7823e-117">The Visual Studio Package Manager (NuGet 3.x+) and the `dotnet` tool store copies of downloaded packages in this cache (saved as `.dat` files), organized into subfolders for each package source.</span></span> <span data-ttu-id="7823e-118">パッケージは展開されず、キャッシュには 30 分の有効期限があります。</span><span class="sxs-lookup"><span data-stu-id="7823e-118">Packages are not expanded, and the cache has an expiration time of 30 minutes.</span></span><br/><ul><li><span data-ttu-id="7823e-119">Windows: `%localappdata%\NuGet\v3-cache`</span><span class="sxs-lookup"><span data-stu-id="7823e-119">Windows: `%localappdata%\NuGet\v3-cache`</span></span></li><li><span data-ttu-id="7823e-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span><span class="sxs-lookup"><span data-stu-id="7823e-120">Mac/Linux: `~/.local/share/NuGet/v3-cache`</span></span></li><li><span data-ttu-id="7823e-121">NUGET_HTTP_CACHE_PATH 環境変数を使用してオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="7823e-121">Override using the NUGET_HTTP_CACHE_PATH environment variable.</span></span></li></ul> |
| <span data-ttu-id="7823e-122">temp</span><span class="sxs-lookup"><span data-stu-id="7823e-122">temp</span></span> | <span data-ttu-id="7823e-123">NuGet が、さまざまな操作中に一時ファイルを格納するフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="7823e-123">A folder where NuGet stores temporary files during its various operations.</span></span><br/><li><span data-ttu-id="7823e-124">Windows: `%temp%\NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="7823e-124">Windows: `%temp%\NuGetScratch`</span></span></li><li><span data-ttu-id="7823e-125">Mac/Linux: `/tmp/NuGetScratch`</span><span class="sxs-lookup"><span data-stu-id="7823e-125">Mac/Linux: `/tmp/NuGetScratch`</span></span></li></ul> |
| <span data-ttu-id="7823e-126">plugins-cache **4.8+**</span><span class="sxs-lookup"><span data-stu-id="7823e-126">plugins-cache **4.8+**</span></span> | <span data-ttu-id="7823e-127">NuGet が、操作要求の結果を格納するフォルダーです。</span><span class="sxs-lookup"><span data-stu-id="7823e-127">A folder where NuGet stores the results from the operation claims request.</span></span><br/><ul><li><span data-ttu-id="7823e-128">Windows: `%localappdata%\NuGet\plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="7823e-128">Windows: `%localappdata%\NuGet\plugins-cache`</span></span></li><li><span data-ttu-id="7823e-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span><span class="sxs-lookup"><span data-stu-id="7823e-129">Mac/Linux: `~/.local/share/NuGet/plugins-cache`</span></span></li><li><span data-ttu-id="7823e-130">NUGET_PLUGINS_CACHE_PATH 環境変数を使用してオーバーライドします。</span><span class="sxs-lookup"><span data-stu-id="7823e-130">Override using the NUGET_PLUGINS_CACHE_PATH environment variable.</span></span></li></ul> |

> [!Note]
> <span data-ttu-id="7823e-131">NuGet 3.5 以前では、"*HTTP キャッシュ*" ではなく、`%localappdata%\NuGet\Cache` にある "*パッケージ キャッシュ*" を使用していました。</span><span class="sxs-lookup"><span data-stu-id="7823e-131">NuGet 3.5 and earlier uses *packages-cache* instead of the *http-cache*, which is located in `%localappdata%\NuGet\Cache`.</span></span>

<span data-ttu-id="7823e-132">キャッシュと "*グローバル パッケージ*" フォルダーを使用することで、NuGet は多くの場合、コンピューター上に既に存在するパッケージのダウンロードを回避して、インストール、更新、および復元処理のパフォーマンスを改善しました。</span><span class="sxs-lookup"><span data-stu-id="7823e-132">By using the cache and *global-packages* folders, NuGet generally avoids downloading packages that already exist on the computer, improving the performance of install, update, and restore operations.</span></span> <span data-ttu-id="7823e-133">また、PackageReference を使用する場合、"*グローバル パッケージ*" フォルダーによって、プロジェクト フォルダー内にダウンロードされたパッケージを保持することを回避できます。プロジェクト フォルダーでは、パッケージがソース コントロールに誤って追加される可能性があります。グローバル パッケージ フォルダーによって、コンピューター ストレージでの NuGet の全体の影響が緩和されます。</span><span class="sxs-lookup"><span data-stu-id="7823e-133">When using PackageReference, the *global-packages* folder also avoids keeping downloaded packages inside project folders, where they might be inadvertently added to source control, and reduces NuGet's overall impact on computer storage.</span></span>

<span data-ttu-id="7823e-134">パッケージの取得を求められたら、NuGet は最初に "*グローバル パッケージ*" フォルダー内を調べます。</span><span class="sxs-lookup"><span data-stu-id="7823e-134">When asked to retrieve a package, NuGet first looks in the *global-packages* folder.</span></span> <span data-ttu-id="7823e-135">パッケージの正確なバージョンがここになかった場合、NuGet は HTTP 以外のすべてのパッケージ ソースを確認します。</span><span class="sxs-lookup"><span data-stu-id="7823e-135">If the exact version of package is not there, then NuGet checks all non-HTTP package sources.</span></span> <span data-ttu-id="7823e-136">それでもパッケージが見つからない場合、`--no-cache` を付加した `dotnet.exe` コマンドまたは `-NoCache` を付加した `nuget.exe` コマンドを指定していないかぎり、NuGet は "*HTTP キャッシュ*" でパッケージを探します。</span><span class="sxs-lookup"><span data-stu-id="7823e-136">If the package is still not found, NuGet looks for the package in the *http-cache* unless you specify `--no-cache` with `dotnet.exe` commands or `-NoCache` with `nuget.exe` commands.</span></span> <span data-ttu-id="7823e-137">パッケージがキャッシュになかった場合、またはキャッシュが使用されていない場合、NuGet は HTTP 経由でパッケージを取得します。</span><span class="sxs-lookup"><span data-stu-id="7823e-137">If the package is not in the cache, or the cache isn't used, NuGet then retrieves the package over HTTP .</span></span>

<span data-ttu-id="7823e-138">詳細については、[パッケージをインストールする場合のしくみ](ways-to-install-a-package.md#what-happens-when-a-package-is-installed)に関するページをご覧ください。</span><span class="sxs-lookup"><span data-stu-id="7823e-138">For more information, see [What happens when a package is installed](ways-to-install-a-package.md#what-happens-when-a-package-is-installed).</span></span>

## <a name="viewing-folder-locations"></a><span data-ttu-id="7823e-139">フォルダーの場所を表示する</span><span class="sxs-lookup"><span data-stu-id="7823e-139">Viewing folder locations</span></span>

<span data-ttu-id="7823e-140">次のように [nuget locals コマンド](../tools/cli-ref-locals.md)を使用して場所を表示できます。</span><span class="sxs-lookup"><span data-stu-id="7823e-140">You can view locations using the [nuget locals command](../tools/cli-ref-locals.md):</span></span>

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

<span data-ttu-id="7823e-141">典型的な出力は次のとおりです (Windows、"user1" は現在のユーザー名)。</span><span class="sxs-lookup"><span data-stu-id="7823e-141">Typical output (Windows; "user1" is the current username):</span></span>

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

<span data-ttu-id="7823e-142">(`package-cache` は NuGet 2.x で使用され、NuGet 3.5 以前で表示されます。)</span><span class="sxs-lookup"><span data-stu-id="7823e-142">(`package-cache` is used in NuGet 2.x and appears with NuGet 3.5 and earlier.)</span></span>

<span data-ttu-id="7823e-143">次のように [dotnet nuget locals コマンド](/dotnet/core/tools/dotnet-nuget-locals)を使用して、フォルダーの場所を表示することもできます。</span><span class="sxs-lookup"><span data-stu-id="7823e-143">You can also view folder locations using the [dotnet nuget locals command](/dotnet/core/tools/dotnet-nuget-locals):</span></span>

```cli
dotnet nuget locals all --list
```

<span data-ttu-id="7823e-144">典型的な出力は次のとおりです (Mac/Linux、"user1" は現在のユーザー名)。</span><span class="sxs-lookup"><span data-stu-id="7823e-144">Typical output (Mac/Linux; "user1" is the current username):</span></span>

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

<span data-ttu-id="7823e-145">単一フォルダーの場所を表示するには、`all` ではなく、`http-cache`、`global-packages`、`temp`、または `plugins-cache` を使用します。</span><span class="sxs-lookup"><span data-stu-id="7823e-145">To display the location of a single folder, use `http-cache`, `global-packages`, `temp`, or `plugins-cache` instead of `all`.</span></span>

## <a name="clearing-local-folders"></a><span data-ttu-id="7823e-146">ローカル フォルダーをクリアする</span><span class="sxs-lookup"><span data-stu-id="7823e-146">Clearing local folders</span></span>

<span data-ttu-id="7823e-147">パッケージのインストールに関する問題が発生した場合、または、リモート ギャラリーからパッケージをインストールしていることを確認する場合は、フォルダーを指定してクリアする `locals --clear` オプションまたは `locals -clear` (nuget.exe) を使用するか、すべてのフォルダーをクリアする `all` を使用します。</span><span class="sxs-lookup"><span data-stu-id="7823e-147">If you encounter package installation problems or otherwise want to ensure that you're installing packages from a remote gallery, use the `locals --clear` option (dotnet.exe) or `locals -clear` (nuget.exe), specifying the folder to clear, or `all` to clear all folders:</span></span>

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

<span data-ttu-id="7823e-148">現在 Visual Studio で開いているプロジェクトで使用されているパッケージはすべて、"*グローバル パッケージ*" フォルダーからクリアされません。</span><span class="sxs-lookup"><span data-stu-id="7823e-148">Any packages used by projects that are currently open in Visual Studio are not cleared from the *global-packages* folder.</span></span>

<span data-ttu-id="7823e-149">Visual Studio 2017 で、**[ツール]、[NuGet パッケージ マネージャー]、[パッケージ マネージャー設定]** メニュー コマンドを使用して、**[すべての NuGet キャッシュをクリア]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="7823e-149">In Visual Studio 2017, use the **Tools > NuGet Package Manager > Package Manager Settings** menu command, then select **Clear All NuGet Cache(s)**.</span></span> <span data-ttu-id="7823e-150">キャッシュの管理は現在、パッケージ マネージャー コンソール経由では利用できません。</span><span class="sxs-lookup"><span data-stu-id="7823e-150">Managing the cache isn't presently available through the Package Manager Console.</span></span> <span data-ttu-id="7823e-151">Visual Studio 2015 では、代わりに CLI コマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="7823e-151">In Visual Studio 2015, use the CLI commands instead.</span></span>

![キャッシュをクリアするための NuGet オプション コマンド](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a><span data-ttu-id="7823e-153">エラーのトラブルシューティング</span><span class="sxs-lookup"><span data-stu-id="7823e-153">Troubleshooting errors</span></span>

<span data-ttu-id="7823e-154">以下のエラーは、`nuget locals` または `dotnet nuget locals`を使用した場合に発生する可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7823e-154">The following errors can occur when using `nuget locals` or `dotnet nuget locals`:</span></span>

- <span data-ttu-id="7823e-155">"*Error: The process cannot access the file <package> because it is being used by another process*/(エラー: 別のプロセスで使用されているため、プロセスはファイルにアクセスできません/)" または "*ローカル リソースをクリアできませんでした。1 つ以上のファイルを削除できません。*"</span><span class="sxs-lookup"><span data-stu-id="7823e-155">*Error: The process cannot access the file <package> because it is being used by another process* or *Clearing local resources failed: Unable to delete one or more files*</span></span>

    <span data-ttu-id="7823e-156">フォルダーにある 1 つまたは複数のファイルが、別のプロセスで使用中です。たとえば、"*グローバル パッケージ*" フォルダー内のパッケージを参照する Visual Studio プロジェクトが開いています。</span><span class="sxs-lookup"><span data-stu-id="7823e-156">One or more files in the folder are in use by another process; for example, a Visual Studio project is open that refers to packages in the *global-packages* folder.</span></span> <span data-ttu-id="7823e-157">それらのプロセスを閉じて、もう一度やり直してください。</span><span class="sxs-lookup"><span data-stu-id="7823e-157">Close those processes and try again.</span></span>

- <span data-ttu-id="7823e-158">"*Error: Access to the path <path> is denied*/(エラー: パスへのアクセスが拒否されます/)" または "*The directory is not empty*/(ディレクトリが空ではありません/)"</span><span class="sxs-lookup"><span data-stu-id="7823e-158">*Error: Access to the path <path> is denied* or *The directory is not empty*</span></span>

    <span data-ttu-id="7823e-159">キャッシュのファイルを削除するためのアクセス許可がありません。</span><span class="sxs-lookup"><span data-stu-id="7823e-159">You don't have permission to delete files in the cache.</span></span> <span data-ttu-id="7823e-160">可能であれば、フォルダーのアクセス許可を変更して、もう一度やり直してください。</span><span class="sxs-lookup"><span data-stu-id="7823e-160">Change the folder permissions, if possible, and try again.</span></span> <span data-ttu-id="7823e-161">それができない場合は、システム管理者に問い合わせてください。</span><span class="sxs-lookup"><span data-stu-id="7823e-161">Otherwise, contact your system administrator.</span></span>

- <span data-ttu-id="7823e-162">"*エラー: 指定されたパスかファイル名、またはその両方が長すぎます。完全修飾ファイル名は 260 文字未満で指定し、ディレクトリ名は 248 文字未満で指定してください。*"</span><span class="sxs-lookup"><span data-stu-id="7823e-162">*Error: The specified path, file name, or both are too long. The fully qualified file name must be less than 260 characters, and the directory name must be less than 248 characters.*</span></span>

    <span data-ttu-id="7823e-163">フォルダー名を短くして、もう一度やり直してください。</span><span class="sxs-lookup"><span data-stu-id="7823e-163">Shorten the folder names and try again.</span></span>
