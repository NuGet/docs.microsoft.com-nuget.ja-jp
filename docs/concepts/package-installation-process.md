---
title: パッケージ インストールのしくみ
description: パッケージ インストール プロセスに関する詳細
author: karann-msft
ms.author: karann
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 1ae030c308b14b8884fb608c1683c8c46000b0bd
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036904"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a><span data-ttu-id="896a2-103">NuGet パッケージのインストールのしくみ</span><span class="sxs-lookup"><span data-stu-id="896a2-103">What happens when a NuGet package is installed?</span></span>

<span data-ttu-id="896a2-104">分かりやすく言うと、さまざまな NuGet ツールは通常、プロジェクト ファイルまたは `packages.config` にパッケージへの参照を作成し、次にパッケージの復元を実行することによって効果的にパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="896a2-104">Simply said, the different NuGet tools typically create a reference to a package in the project file or `packages.config`, then perform a package restore, which effectively installs the package.</span></span> <span data-ttu-id="896a2-105">ただし `nuget install` は例外です。この方法では `packages` フォルダーにパッケージを展開するのみで、その他のファイルは変更しません。</span><span class="sxs-lookup"><span data-stu-id="896a2-105">The exception is `nuget install`, which only expands the package into a `packages` folder and does not modify any other files.</span></span>

<span data-ttu-id="896a2-106">一般的なプロセスは次のとおりです。</span><span class="sxs-lookup"><span data-stu-id="896a2-106">The general process is as follows:</span></span>

1. <span data-ttu-id="896a2-107">(`nuget.exe` を除くすべてのツール) プロジェクト ファイルまたは `packages.config` に、パッケージ識別子とバージョンを記録します。</span><span class="sxs-lookup"><span data-stu-id="896a2-107">(All tools except `nuget.exe`) Record the package identifier and version into the project file or `packages.config`.</span></span>

   <span data-ttu-id="896a2-108">インストール ツールが Visual Studio か dotnet CLI の場合は、このツールは最初にパッケージをインストールしようとします。</span><span class="sxs-lookup"><span data-stu-id="896a2-108">If the installation tool is Visual Studio or the dotnet CLI, the tool first attempts to install the package.</span></span> <span data-ttu-id="896a2-109">互換性がない場合、パッケージはプロジェクト ファイルにも `packages.config` にも追加されません。</span><span class="sxs-lookup"><span data-stu-id="896a2-109">If it's incompatible, the package is not added to the project file or `packages.config`.</span></span>

2. <span data-ttu-id="896a2-110">パッケージを取得します。</span><span class="sxs-lookup"><span data-stu-id="896a2-110">Acquire the package:</span></span>
   - <span data-ttu-id="896a2-111">「[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)」で説明されているように、パッケージが "*グローバル パッケージ*" フォルダーにインストール済みかどうかを (正確な識別子とバージョン番号によって) チェックします。</span><span class="sxs-lookup"><span data-stu-id="896a2-111">Check if the package (by exact identifer and version number) is already installed in the *global-packages* folder as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

   - <span data-ttu-id="896a2-112">パッケージが*グローバル パッケージ* フォルダーにない場合、[構成ファイル](../consume-packages/Configuring-NuGet-Behavior.md)でリストされているソースからパッケージの取得を試みます。</span><span class="sxs-lookup"><span data-stu-id="896a2-112">If the package is not in the *global-packages* folder, attempt to retrieve it from the sources listed in the [configuration files](../consume-packages/Configuring-NuGet-Behavior.md).</span></span> <span data-ttu-id="896a2-113">オンライン ソースの場合は、`nuget.exe` コマンドで `-NoCache` を指定するか、`dotnet restore` で `--no-cache` を指定しない限り、最初に HTTP キャッシュからパッケージを取得しようと試みます。</span><span class="sxs-lookup"><span data-stu-id="896a2-113">For online sources, attempt first to retrieve the package from the HTTP cache unless `-NoCache` is specified with `nuget.exe` commands or `--no-cache` is specified with `dotnet restore`.</span></span> <span data-ttu-id="896a2-114">(Visual Studio と `dotnet add package` では常にキャッシュが使用されます。)パッケージがキャッシュから使用された場合、出力に "CACHE" と表示されます。</span><span class="sxs-lookup"><span data-stu-id="896a2-114">(Visual Studio and `dotnet add package` always use the cache.) If a package is used from the cache, "CACHE" appears in the output.</span></span> <span data-ttu-id="896a2-115">キャッシュには 30 分の有効期限があります。</span><span class="sxs-lookup"><span data-stu-id="896a2-115">The cache has an expiration time of 30 minutes.</span></span>

   - <span data-ttu-id="896a2-116">パッケージが HTTP キャッシュにない場合、構成にリストされているソースからパッケージのダウンロードを試みます。</span><span class="sxs-lookup"><span data-stu-id="896a2-116">If the package is not in the HTTP cache, attempt to download it from the sources listed in the configuration.</span></span> <span data-ttu-id="896a2-117">パッケージがダウンロードされると、出力に "GET" および "OK" と表示されます。</span><span class="sxs-lookup"><span data-stu-id="896a2-117">If a package is downloaded, "GET" and "OK" appear in the output.</span></span> <span data-ttu-id="896a2-118">NuGet では、通常の詳細度で http トラフィックが記録されます。</span><span class="sxs-lookup"><span data-stu-id="896a2-118">NuGet logs http traffic on normal verbosity.</span></span>

   - <span data-ttu-id="896a2-119">パッケージがいずれのソースからも正常に取得できない場合は、この時点でインストールが失敗し、[NU1103](../reference/errors-and-warnings/NU1103.md) などのエラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="896a2-119">If the package cannot be successfully acquired from any sources, installation fails at this point with an error such as [NU1103](../reference/errors-and-warnings/NU1103.md).</span></span> <span data-ttu-id="896a2-120">`nuget.exe` コマンドのエラーでは最後にチェックされたソースのみが表示されますが、実際にはいずれのソースからもパッケージをダウンロードできなかったことを意味しています。</span><span class="sxs-lookup"><span data-stu-id="896a2-120">Note that errors from `nuget.exe` commands show only the last source checked, but implies that the package wasn't available from any source.</span></span>

   <span data-ttu-id="896a2-121">パッケージを取得するときに、NuGet の構成でのソースの順序が適用される場合があります。</span><span class="sxs-lookup"><span data-stu-id="896a2-121">When acquiring the package, the order of sources in the NuGet configuration may apply:</span></span>

   - <span data-ttu-id="896a2-122">NuGet では HTTP ソースをチェックする前に、ローカルのフォルダーとネットワーク共有からソースがチェックされます。</span><span class="sxs-lookup"><span data-stu-id="896a2-122">NuGet checks sources local folder and network shares before checking HTTP sources.</span></span>

3. <span data-ttu-id="896a2-123">「[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)」で説明されているように、パッケージのコピーとその他の情報を "*HTTP キャッシュ*" フォルダーに保存します。</span><span class="sxs-lookup"><span data-stu-id="896a2-123">Save a copy of the package and other information in the *http-cache* folder as described on [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

4. <span data-ttu-id="896a2-124">ダウンロードが完了したら、ユーザーごとの "*グローバル パッケージ*" フォルダーにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="896a2-124">If downloaded, install the package into the per-user *global-packages* folder.</span></span> <span data-ttu-id="896a2-125">NuGet では、パッケージの識別子ごとにサブフォルダーが作成され、次にインストールされるパッケージのバージョンごとにサブフォルダーが作成されます。</span><span class="sxs-lookup"><span data-stu-id="896a2-125">NuGet creates a subfolder for each package identifier, then creates subfolders for each installed version of the package.</span></span>

5. <span data-ttu-id="896a2-126">NuGet では、必要に応じて、パッケージの依存関係がインストールされます。</span><span class="sxs-lookup"><span data-stu-id="896a2-126">NuGet installs package dependencies as required.</span></span> <span data-ttu-id="896a2-127">このプロセスでは、[依存関係の解決](../concepts/dependency-resolution.md)に関するページで説明されているように、パッケージのバージョンが更新される可能性があります。</span><span class="sxs-lookup"><span data-stu-id="896a2-127">This process might update package versions in the process, as described in [Dependency Resolution](../concepts/dependency-resolution.md).</span></span>

6. <span data-ttu-id="896a2-128">その他のプロジェクト ファイルとフォルダーを更新します。</span><span class="sxs-lookup"><span data-stu-id="896a2-128">Update other project files and folders:</span></span>

    - <span data-ttu-id="896a2-129">PackageReference を使用するプロジェクトの場合は、`obj/project.assets.json` に格納されているパッケージの依存関係グラフを更新します。</span><span class="sxs-lookup"><span data-stu-id="896a2-129">For projects using PackageReference, update the package dependency graph stored in `obj/project.assets.json`.</span></span> <span data-ttu-id="896a2-130">パッケージの内容自体はいずれのプロジェクト フォルダーにもコピーされません。</span><span class="sxs-lookup"><span data-stu-id="896a2-130">Package contents themselves are not copied into any project folder.</span></span>
    - <span data-ttu-id="896a2-131">パッケージで[ソースと構成ファイルの変換](../create-packages/source-and-config-file-transformations.md)が使用されている場合は、`app.config` や `web.config` を更新します。</span><span class="sxs-lookup"><span data-stu-id="896a2-131">Update `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>

7. <span data-ttu-id="896a2-132">(Visual Studio のみ) Visual Studio のウィンドウにパッケージの readme ファイルが表示されます (利用可能な場合)。</span><span class="sxs-lookup"><span data-stu-id="896a2-132">(Visual Studio only) Display the package's readme file, if available, in a Visual Studio window.</span></span>

<span data-ttu-id="896a2-133">それでは NuGet パッケージでの生産性の高いコーディングをお楽しみください。</span><span class="sxs-lookup"><span data-stu-id="896a2-133">Enjoy your productive coding with NuGet packages!</span></span>
