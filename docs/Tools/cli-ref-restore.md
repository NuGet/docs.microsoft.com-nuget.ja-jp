---
title: "復元コマンドは NuGet CLI |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe restore コマンドのリファレンス"
keywords: "nuget の参照を復元、restore コマンドのパッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2416ad652244e0ea60651147ad74a1513cdb75ff
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/15/2018
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="eed7f-104">restore コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="eed7f-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="eed7f-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="eed7f-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="eed7f-106">ダウンロードし、表示されないすべてのパッケージをインストール、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="eed7f-106">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="eed7f-107">NuGet 4.0 以降および PackageReference 形式に使用する場合は、生成、`<project>.nuget.props`ファイルの場合は、必要に応じて、`obj`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="eed7f-107">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="eed7f-108">(ファイルをソース管理から省略できます)。</span><span class="sxs-lookup"><span data-stu-id="eed7f-108">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="eed7f-109">Mac OSX およびモノラルで CLI を使用して Linux では、パッケージの復元はサポートされていません PackageReference とします。</span><span class="sxs-lookup"><span data-stu-id="eed7f-109">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="eed7f-110">使用法</span><span class="sxs-lookup"><span data-stu-id="eed7f-110">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="eed7f-111">ここで`<projectPath>`ソリューションの場所を指定または`packages.config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="eed7f-111">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="eed7f-112">参照してください[解説](#remarks)下詳細については動作します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-112">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="eed7f-113">オプション</span><span class="sxs-lookup"><span data-stu-id="eed7f-113">Options</span></span>

| <span data-ttu-id="eed7f-114">オプション</span><span class="sxs-lookup"><span data-stu-id="eed7f-114">Option</span></span> | <span data-ttu-id="eed7f-115">説明</span><span class="sxs-lookup"><span data-stu-id="eed7f-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="eed7f-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="eed7f-116">ConfigFile</span></span> | <span data-ttu-id="eed7f-117">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="eed7f-118">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="eed7f-119">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="eed7f-119">DirectDownload</span></span> | <span data-ttu-id="eed7f-120">*(4.0 以降)*バイナリなどのメタデータ キャッシュの値を設定せず直接パッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="eed7f-120">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="eed7f-121">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="eed7f-121">DisableParallelProcessing</span></span> | <span data-ttu-id="eed7f-122">同時に複数のパッケージの復元を無効にします。</span><span class="sxs-lookup"><span data-stu-id="eed7f-122">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="eed7f-123">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="eed7f-123">FallbackSource</span></span> | <span data-ttu-id="eed7f-124">*(3.2 +)*プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。</span><span class="sxs-lookup"><span data-stu-id="eed7f-124">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="eed7f-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="eed7f-125">ForceEnglishOutput</span></span> | <span data-ttu-id="eed7f-126">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="eed7f-127">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="eed7f-127">Help</span></span> | <span data-ttu-id="eed7f-128">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="eed7f-129">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="eed7f-129">MSBuildPath</span></span> | <span data-ttu-id="eed7f-130">*(4.0 以降)*よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-130">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="eed7f-131">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="eed7f-131">MSBuildVersion</span></span> | <span data-ttu-id="eed7f-132">*(3.2 +)*このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-132">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="eed7f-133">サポートされている値は、4、12、14、15 です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-133">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="eed7f-134">既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="eed7f-134">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="eed7f-135">NoCache</span><span class="sxs-lookup"><span data-stu-id="eed7f-135">NoCache</span></span> | <span data-ttu-id="eed7f-136">NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="eed7f-136">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="eed7f-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="eed7f-137">NonInteractive</span></span> | <span data-ttu-id="eed7f-138">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="eed7f-139">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="eed7f-139">OutputDirectory</span></span> | <span data-ttu-id="eed7f-140">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-140">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="eed7f-141">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="eed7f-141">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="eed7f-142">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="eed7f-142">PackageSaveMode</span></span> | <span data-ttu-id="eed7f-143">パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-143">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="eed7f-144">PackagesDirectory</span><span class="sxs-lookup"><span data-stu-id="eed7f-144">PackagesDirectory</span></span> | <span data-ttu-id="eed7f-145">`OutputDirectory` と同じ。</span><span class="sxs-lookup"><span data-stu-id="eed7f-145">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="eed7f-146">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="eed7f-146">Project2ProjectTimeOut</span></span> | <span data-ttu-id="eed7f-147">タイムアウト (秒) プロジェクト間参照を解決するためです。</span><span class="sxs-lookup"><span data-stu-id="eed7f-147">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="eed7f-148">再帰</span><span class="sxs-lookup"><span data-stu-id="eed7f-148">Recursive</span></span> | <span data-ttu-id="eed7f-149">*(4.0 以降)* UWP と .NET Core プロジェクトのすべての参照プロジェクトを復元します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-149">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="eed7f-150">使用してプロジェクトには適用されません`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-150">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="eed7f-151">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="eed7f-151">RequireConsent</span></span> | <span data-ttu-id="eed7f-152">ダウンロードして、パッケージをインストールする前にパッケージを復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-152">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="eed7f-153">詳細については、「[パッケージの復元](../consume-packages/package-restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-153">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="eed7f-154">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="eed7f-154">SolutionDirectory</span></span> | <span data-ttu-id="eed7f-155">ソリューション フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-155">Specifies the solution folder.</span></span> <span data-ttu-id="eed7f-156">ソリューションのパッケージを復元するときに無効です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-156">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="eed7f-157">ソース</span><span class="sxs-lookup"><span data-stu-id="eed7f-157">Source</span></span> | <span data-ttu-id="eed7f-158">復元操作に使用する (Url) とパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-158">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="eed7f-159">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-159">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="eed7f-160">詳細度</span><span class="sxs-lookup"><span data-stu-id="eed7f-160">Verbosity</span></span> |<span data-ttu-id="eed7f-161">> の出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-161">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="eed7f-162">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="eed7f-162">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="eed7f-163">コメント</span><span class="sxs-lookup"><span data-stu-id="eed7f-163">Remarks</span></span>

<span data-ttu-id="eed7f-164">Restore コマンドでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-164">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="eed7f-165">Restore コマンドの操作モードを決定します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-165">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="eed7f-166">projectPath ファイルの種類</span><span class="sxs-lookup"><span data-stu-id="eed7f-166">projectPath file type</span></span> | <span data-ttu-id="eed7f-167">動作</span><span class="sxs-lookup"><span data-stu-id="eed7f-167">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="eed7f-168">ソリューション (フォルダー)</span><span class="sxs-lookup"><span data-stu-id="eed7f-168">Solution (folder)</span></span> | <span data-ttu-id="eed7f-169">NuGet 検索、`.sln`ファイルとそれ以外の場合はエラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-169">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="eed7f-170">`(SolutionDir)\.nuget` 開始フォルダーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="eed7f-170">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="eed7f-171">`.sln` ファイル</span><span class="sxs-lookup"><span data-stu-id="eed7f-171">`.sln` file</span></span> | <span data-ttu-id="eed7f-172">ソリューションで識別されるパッケージを復元します。エラーは、`-SolutionDirectory`を使用します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-172">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="eed7f-173">`$(SolutionDir)\.nuget` 開始フォルダーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="eed7f-173">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="eed7f-174">`packages.config` またはプロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="eed7f-174">`packages.config` or project file</span></span> | <span data-ttu-id="eed7f-175">解決して、依存関係をインストール ファイルに表示されているパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-175">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="eed7f-176">その他のファイルの種類</span><span class="sxs-lookup"><span data-stu-id="eed7f-176">Other file type</span></span> | <span data-ttu-id="eed7f-177">ファイルがあると見なされます、 `.sln` ; 上記と同じファイルのない場合は、ソリューションでは、NuGet により、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-177">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="eed7f-178">(指定されていない projectPath)</span><span class="sxs-lookup"><span data-stu-id="eed7f-178">(projectPath not specified)</span></span> | <span data-ttu-id="eed7f-179">-NuGet は、現在のフォルダーにソリューション ファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-179">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="eed7f-180">パッケージ; を復元する 1 つが使用される 1 つのファイルが見つかった場合、複数のソリューションが見つからない場合は、NuGet は、エラーを示します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-180">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="eed7f-181">-NuGet 検索ソリューション ファイルが存在しない場合、`packages.config`しパッケージを復元するを使用します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-181">- If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span>
    |<span data-ttu-id="eed7f-182">場合は解決策はありませんか`packages.config`ファイルが見つかると、NuGet は、エラーを示します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-182">- If no solution or `packages.config` file is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="eed7f-183">次の優先順位 (NuGet は、これらのフォルダーが見つからない場合に、エラーを提供) を使用して、パッケージ フォルダーを決定します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-183">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="eed7f-184">指定されたフォルダー`-PackagesDirectory`です。</span><span class="sxs-lookup"><span data-stu-id="eed7f-184">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="eed7f-185">`repositoryPath`で vale `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="eed7f-185">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="eed7f-186">指定されたフォルダー `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="eed7f-186">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="eed7f-187">ソリューションのパッケージを復元するには、NuGet は、次を行います。</span><span class="sxs-lookup"><span data-stu-id="eed7f-187">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="eed7f-188">ソリューション ファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="eed7f-188">Loads the solution file.</span></span>
    - <span data-ttu-id="eed7f-189">表示されているソリューション レベルのパッケージを復元`$(SolutionDir)\.nuget\packages.config`に、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="eed7f-189">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="eed7f-190">表示されているパッケージを復元`$(ProjectDir)\packages.config`に、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="eed7f-190">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="eed7f-191">指定されたパッケージごとに、必要ない限り、並列でパッケージを復元`-DisableParallelProcessing`を指定します。</span><span class="sxs-lookup"><span data-stu-id="eed7f-191">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="eed7f-192">使用例</span><span class="sxs-lookup"><span data-stu-id="eed7f-192">Examples</span></span>

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
