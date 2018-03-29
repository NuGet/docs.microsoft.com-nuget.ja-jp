---
title: 復元コマンドは NuGet CLI |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Nuget.exe restore コマンドのリファレンス
keywords: nuget の参照を復元、restore コマンドのパッケージ
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 64f12fdedc8fbfcee15c1dcddc445148f458c030
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="bcf0a-104">restore コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="bcf0a-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="bcf0a-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="bcf0a-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="bcf0a-106">ダウンロードし、表示されないすべてのパッケージをインストール、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="bcf0a-107">NuGet 4.0 以降および PackageReference 形式に使用する場合は、生成、`<project>.nuget.props`ファイルの場合は、必要に応じて、`obj`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="bcf0a-108">(ファイルをソース管理から省略できます)。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="bcf0a-109">Mac OSX およびモノラルで CLI を使用して Linux では、パッケージの復元はサポートされていません PackageReference とします。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="bcf0a-110">使用法</span><span class="sxs-lookup"><span data-stu-id="bcf0a-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="bcf0a-111">ここで`<projectPath>`ソリューションの場所を指定または`packages.config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="bcf0a-112">参照してください[解説](#remarks)下詳細については動作します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="bcf0a-113">オプション</span><span class="sxs-lookup"><span data-stu-id="bcf0a-113">Options</span></span>

| <span data-ttu-id="bcf0a-114">オプション</span><span class="sxs-lookup"><span data-stu-id="bcf0a-114">Option</span></span> | <span data-ttu-id="bcf0a-115">説明</span><span class="sxs-lookup"><span data-stu-id="bcf0a-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="bcf0a-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="bcf0a-116">ConfigFile</span></span> | <span data-ttu-id="bcf0a-117">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="bcf0a-118">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="bcf0a-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="bcf0a-119">DirectDownload</span></span> | <span data-ttu-id="bcf0a-120">*(4.0 以降)*バイナリなどのメタデータ キャッシュの値を設定せず直接パッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="bcf0a-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="bcf0a-121">DisableParallelProcessing</span></span> | <span data-ttu-id="bcf0a-122">同時に複数のパッケージの復元を無効にします。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="bcf0a-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="bcf0a-123">FallbackSource</span></span> | <span data-ttu-id="bcf0a-124">*(3.2 +)*プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="bcf0a-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="bcf0a-125">ForceEnglishOutput</span></span> | <span data-ttu-id="bcf0a-126">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="bcf0a-127">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="bcf0a-127">Help</span></span> | <span data-ttu-id="bcf0a-128">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="bcf0a-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="bcf0a-129">MSBuildPath</span></span> | <span data-ttu-id="bcf0a-130">*(4.0 以降)*よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="bcf0a-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="bcf0a-131">MSBuildVersion</span></span> | <span data-ttu-id="bcf0a-132">*(3.2 +)*このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="bcf0a-133">サポートされている値は、4、12、14、15 です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="bcf0a-134">既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="bcf0a-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="bcf0a-135">NoCache</span></span> | <span data-ttu-id="bcf0a-136">NuGet がキャッシュされているパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-136">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="bcf0a-137">参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-137">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="bcf0a-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="bcf0a-138">NonInteractive</span></span> | <span data-ttu-id="bcf0a-139">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="bcf0a-140">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="bcf0a-140">OutputDirectory</span></span> | <span data-ttu-id="bcf0a-141">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-141">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="bcf0a-142">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-142">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="bcf0a-143">復元するときに必要な`packages.config`ファイル`PackagesDirectory`または`SolutionDirectory`を使用します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-143">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>|
| <span data-ttu-id="bcf0a-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="bcf0a-144">PackageSaveMode</span></span> | <span data-ttu-id="bcf0a-145">パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="bcf0a-146">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="bcf0a-146">PackagesDirectory</span></span> | <span data-ttu-id="bcf0a-147">`OutputDirectory` と同じ。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-147">Same as `OutputDirectory`.</span></span> <span data-ttu-id="bcf0a-148">復元するときに必要な`packages.config`ファイル`OutputDirectory`または`SolutionDirectory`を使用します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-148">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span> |
| <span data-ttu-id="bcf0a-149">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="bcf0a-149">Project2ProjectTimeOut</span></span> | <span data-ttu-id="bcf0a-150">タイムアウト (秒) プロジェクト間参照を解決するためです。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-150">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="bcf0a-151">再帰</span><span class="sxs-lookup"><span data-stu-id="bcf0a-151">Recursive</span></span> | <span data-ttu-id="bcf0a-152">*(4.0 以降)* UWP と .NET Core プロジェクトのすべての参照プロジェクトを復元します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-152">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="bcf0a-153">使用してプロジェクトには適用されません`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-153">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="bcf0a-154">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="bcf0a-154">RequireConsent</span></span> | <span data-ttu-id="bcf0a-155">ダウンロードして、パッケージをインストールする前にパッケージを復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-155">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="bcf0a-156">詳細については、「[パッケージの復元](../consume-packages/package-restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-156">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="bcf0a-157">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="bcf0a-157">SolutionDirectory</span></span> | <span data-ttu-id="bcf0a-158">ソリューション フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-158">Specifies the solution folder.</span></span> <span data-ttu-id="bcf0a-159">ソリューションのパッケージを復元するときに無効です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-159">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="bcf0a-160">復元するときに必要な`packages.config`ファイル`PackagesDirectory`または`OutputDirectory`を使用します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-160">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span> |
| <span data-ttu-id="bcf0a-161">ソース</span><span class="sxs-lookup"><span data-stu-id="bcf0a-161">Source</span></span> | <span data-ttu-id="bcf0a-162">復元操作に使用する (Url) とパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-162">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="bcf0a-163">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-163">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="bcf0a-164">詳細度</span><span class="sxs-lookup"><span data-stu-id="bcf0a-164">Verbosity</span></span> |<span data-ttu-id="bcf0a-165">> の出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-165">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="bcf0a-166">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="bcf0a-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="bcf0a-167">コメント</span><span class="sxs-lookup"><span data-stu-id="bcf0a-167">Remarks</span></span>

<span data-ttu-id="bcf0a-168">Restore コマンドでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-168">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="bcf0a-169">Restore コマンドの操作モードを決定します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-169">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="bcf0a-170">projectPath ファイルの種類</span><span class="sxs-lookup"><span data-stu-id="bcf0a-170">projectPath file type</span></span> | <span data-ttu-id="bcf0a-171">動作</span><span class="sxs-lookup"><span data-stu-id="bcf0a-171">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="bcf0a-172">ソリューション (フォルダー)</span><span class="sxs-lookup"><span data-stu-id="bcf0a-172">Solution (folder)</span></span> | <span data-ttu-id="bcf0a-173">NuGet 検索、`.sln`ファイルとそれ以外の場合はエラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-173">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="bcf0a-174">`(SolutionDir)\.nuget` 開始フォルダーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-174">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="bcf0a-175">`.sln` ファイル</span><span class="sxs-lookup"><span data-stu-id="bcf0a-175">`.sln` file</span></span> | <span data-ttu-id="bcf0a-176">ソリューションで識別されるパッケージを復元します。エラーは、`-SolutionDirectory`を使用します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-176">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="bcf0a-177">`$(SolutionDir)\.nuget` 開始フォルダーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-177">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="bcf0a-178">`packages.config` またはプロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="bcf0a-178">`packages.config` or project file</span></span> | <span data-ttu-id="bcf0a-179">解決して、依存関係をインストール ファイルに表示されているパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-179">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="bcf0a-180">その他のファイルの種類</span><span class="sxs-lookup"><span data-stu-id="bcf0a-180">Other file type</span></span> | <span data-ttu-id="bcf0a-181">ファイルがあると見なされます、 `.sln` ; 上記と同じファイルのない場合は、ソリューションでは、NuGet により、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-181">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="bcf0a-182">(指定されていない projectPath)</span><span class="sxs-lookup"><span data-stu-id="bcf0a-182">(projectPath not specified)</span></span> | <span data-ttu-id="bcf0a-183">-NuGet は、現在のフォルダーにソリューション ファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-183">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="bcf0a-184">パッケージ; を復元する 1 つが使用される 1 つのファイルが見つかった場合、複数のソリューションが見つからない場合は、NuGet は、エラーを示します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-184">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="bcf0a-185">-NuGet 検索ソリューション ファイルが存在しない場合、`packages.config`しパッケージを復元するを使用します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-185">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="bcf0a-186">場合は解決策はありませんか`packages.config`ファイルが見つかると、NuGet は、エラーを示します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-186">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="bcf0a-187">次の優先順位 (NuGet は、これらのフォルダーが見つからない場合に、エラーを提供) を使用して、パッケージ フォルダーを決定します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-187">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="bcf0a-188">指定されたフォルダー`-PackagesDirectory`です。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-188">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="bcf0a-189">`repositoryPath`で vale `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="bcf0a-189">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="bcf0a-190">指定されたフォルダー `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="bcf0a-190">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="bcf0a-191">ソリューションのパッケージを復元するには、NuGet は、次を行います。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-191">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="bcf0a-192">ソリューション ファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-192">Loads the solution file.</span></span>
    - <span data-ttu-id="bcf0a-193">表示されているソリューション レベルのパッケージを復元`$(SolutionDir)\.nuget\packages.config`に、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-193">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="bcf0a-194">表示されているパッケージを復元`$(ProjectDir)\packages.config`に、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-194">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="bcf0a-195">指定されたパッケージごとに、必要ない限り、並列でパッケージを復元`-DisableParallelProcessing`を指定します。</span><span class="sxs-lookup"><span data-stu-id="bcf0a-195">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="bcf0a-196">使用例</span><span class="sxs-lookup"><span data-stu-id="bcf0a-196">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
