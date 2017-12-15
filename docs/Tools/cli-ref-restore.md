---
title: "復元コマンドは NuGet CLI |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 6ee41020-e548-4e61-b8cd-c82b77ac6af7
description: "Nuget.exe restore コマンドのリファレンス"
keywords: "nuget の参照を復元、restore コマンドのパッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b435a3c2ffe08e3c2f8fc6a4dacb06cf674e4fb9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="2549f-104">restore コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="2549f-104">restore command (NuGet CLI)</span></span>

<span data-ttu-id="2549f-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="2549f-105">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="2549f-106">NuGet 2.7 +: ダウンロードし、表示されないすべてのパッケージをインストール、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="2549f-106">NuGet 2.7+: Downloads and installs any packages missing from the `packages` folder.</span></span>

<span data-ttu-id="2549f-107">NuGet 3.3 + を使用するプロジェクトと`project.json`: が生成されます、`project.lock.json`ファイルと`<project>.nuget.props`ファイル、必要な場合です。</span><span class="sxs-lookup"><span data-stu-id="2549f-107">NuGet 3.3+ with projects using `project.json`: Generates a `project.lock.json` file and a `<project>.nuget.props` file, if needed.</span></span> <span data-ttu-id="2549f-108">(両方のファイルをソース管理から省略できます)。</span><span class="sxs-lookup"><span data-stu-id="2549f-108">(Both files can be omitted from source control.)</span></span>

<span data-ttu-id="2549f-109">NuGet 4.0 以降でプロジェクトをパッケージで参照が含まれますプロジェクト ファイルで直接: 生成、`<project>.nuget.props`ファイルの場合は、必要に応じて、`obj`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="2549f-109">NuGet 4.0+ with project in which package references are included in the project file directly: Generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="2549f-110">(ファイルをソース管理から省略できます)。</span><span class="sxs-lookup"><span data-stu-id="2549f-110">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="2549f-111">Mac OSX およびモノラルで CLI を使用して Linux では、パッケージの復元はサポートされていません PackageReference 形式とします。</span><span class="sxs-lookup"><span data-stu-id="2549f-111">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with the PackageReference format.</span></span>

## <a name="usage"></a><span data-ttu-id="2549f-112">使用方法</span><span class="sxs-lookup"><span data-stu-id="2549f-112">Usage</span></span>

```
nuget restore <projectPath> [options]
```

<span data-ttu-id="2549f-113">ここで`<projectPath>`、ソリューションの場所を指定します、`packages.config`ファイル、または`project.json`ファイル。</span><span class="sxs-lookup"><span data-stu-id="2549f-113">where `<projectPath>` specifies the location of a solution, a `packages.config` file, or a `project.json` file.</span></span> <span data-ttu-id="2549f-114">参照してください[解説](#remarks)下詳細については動作します。</span><span class="sxs-lookup"><span data-stu-id="2549f-114">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="2549f-115">オプション</span><span class="sxs-lookup"><span data-stu-id="2549f-115">Options</span></span>

| <span data-ttu-id="2549f-116">オプション</span><span class="sxs-lookup"><span data-stu-id="2549f-116">Option</span></span> | <span data-ttu-id="2549f-117">説明</span><span class="sxs-lookup"><span data-stu-id="2549f-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2549f-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2549f-118">ConfigFile</span></span> | <span data-ttu-id="2549f-119">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="2549f-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2549f-120">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="2549f-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="2549f-121">DirectDownload</span><span class="sxs-lookup"><span data-stu-id="2549f-121">DirectDownload</span></span> | <span data-ttu-id="2549f-122">*(4.0 以降)*バイナリなどのメタデータ キャッシュの値を設定せず直接パッケージをダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="2549f-122">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span> |
| <span data-ttu-id="2549f-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="2549f-123">DisableParallelProcessing</span></span> | <span data-ttu-id="2549f-124">同時に複数のパッケージの復元を無効にします。</span><span class="sxs-lookup"><span data-stu-id="2549f-124">Disables restoring multiple packages in parallel.</span></span> |
| <span data-ttu-id="2549f-125">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="2549f-125">FallbackSource</span></span> | <span data-ttu-id="2549f-126">*(3.2 +)*プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。</span><span class="sxs-lookup"><span data-stu-id="2549f-126">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="2549f-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2549f-127">ForceEnglishOutput</span></span> | <span data-ttu-id="2549f-128">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="2549f-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2549f-129">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="2549f-129">Help</span></span> | <span data-ttu-id="2549f-130">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="2549f-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="2549f-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="2549f-131">MSBuildPath</span></span> | <span data-ttu-id="2549f-132">*(4.0 以降)*よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。</span><span class="sxs-lookup"><span data-stu-id="2549f-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="2549f-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="2549f-133">MSBuildVersion</span></span> | <span data-ttu-id="2549f-134">*(3.2 +)*このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="2549f-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="2549f-135">サポートされている値は、4、12、14、15 です。</span><span class="sxs-lookup"><span data-stu-id="2549f-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="2549f-136">既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="2549f-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="2549f-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="2549f-137">NoCache</span></span> | <span data-ttu-id="2549f-138">NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="2549f-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="2549f-139">非対話型</span><span class="sxs-lookup"><span data-stu-id="2549f-139">NonInteractive</span></span> | <span data-ttu-id="2549f-140">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="2549f-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2549f-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="2549f-141">OutputDirectory</span></span> | <span data-ttu-id="2549f-142">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="2549f-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="2549f-143">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="2549f-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="2549f-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="2549f-144">PackageSaveMode</span></span> | <span data-ttu-id="2549f-145">パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`です。</span><span class="sxs-lookup"><span data-stu-id="2549f-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="2549f-146">パッケージファイル</span><span class="sxs-lookup"><span data-stu-id="2549f-146">PackagesDirectory</span></span> | <span data-ttu-id="2549f-147">`OutputDirectory` と同じ。</span><span class="sxs-lookup"><span data-stu-id="2549f-147">Same as `OutputDirectory`.</span></span> |
| <span data-ttu-id="2549f-148">Project2ProjectTimeOut</span><span class="sxs-lookup"><span data-stu-id="2549f-148">Project2ProjectTimeOut</span></span> | <span data-ttu-id="2549f-149">タイムアウト (秒) プロジェクト間参照を解決するためです。</span><span class="sxs-lookup"><span data-stu-id="2549f-149">Timeout in seconds for resolving project-to-project references.</span></span> |
| <span data-ttu-id="2549f-150">再帰</span><span class="sxs-lookup"><span data-stu-id="2549f-150">Recursive</span></span> | <span data-ttu-id="2549f-151">*(4.0 以降)* UWP と .NET Core プロジェクトのすべての参照プロジェクトを復元します。</span><span class="sxs-lookup"><span data-stu-id="2549f-151">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="2549f-152">使用してプロジェクトには適用されません`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="2549f-152">Does not apply to projects using `packages.config`.</span></span> |
| <span data-ttu-id="2549f-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="2549f-153">RequireConsent</span></span> | <span data-ttu-id="2549f-154">ダウンロードして、パッケージをインストールする前にパッケージを復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="2549f-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="2549f-155">詳細については、「[パッケージの復元](../consume-packages/package-restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="2549f-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="2549f-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="2549f-156">SolutionDirectory</span></span> | <span data-ttu-id="2549f-157">ソリューション フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="2549f-157">Specifies the solution folder.</span></span> <span data-ttu-id="2549f-158">ソリューションのパッケージを復元するときに無効です。</span><span class="sxs-lookup"><span data-stu-id="2549f-158">Not valid when restoring packages for a solution.</span></span> |
| <span data-ttu-id="2549f-159">ソース</span><span class="sxs-lookup"><span data-stu-id="2549f-159">Source</span></span> | <span data-ttu-id="2549f-160">復元操作に使用する (Url) とパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="2549f-160">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="2549f-161">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../Consume-Packages/Configuring-NuGet-Behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="2549f-161">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="2549f-162">詳細度</span><span class="sxs-lookup"><span data-stu-id="2549f-162">Verbosity</span></span> |<span data-ttu-id="2549f-163">> の出力に表示される詳細データの量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="2549f-163">>Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="2549f-164">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2549f-164">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="2549f-165">コメント</span><span class="sxs-lookup"><span data-stu-id="2549f-165">Remarks</span></span>

<span data-ttu-id="2549f-166">Restore コマンドでは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="2549f-166">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="2549f-167">Restore コマンドの操作モードを決定します。</span><span class="sxs-lookup"><span data-stu-id="2549f-167">Determine the operation mode of the restore command.</span></span>
    <span data-ttu-id="2549f-168">projectPath ファイルの種類</span><span class="sxs-lookup"><span data-stu-id="2549f-168">projectPath file type</span></span> | <span data-ttu-id="2549f-169">動作</span><span class="sxs-lookup"><span data-stu-id="2549f-169">Behavior</span></span>
    | --- | --- |
    <span data-ttu-id="2549f-170">ソリューション (フォルダー)</span><span class="sxs-lookup"><span data-stu-id="2549f-170">Solution (folder)</span></span> | <span data-ttu-id="2549f-171">NuGet 検索、`.sln`ファイルとそれ以外の場合はエラーを使用します。</span><span class="sxs-lookup"><span data-stu-id="2549f-171">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="2549f-172">`(SolutionDir)\.nuget`開始フォルダーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="2549f-172">`(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="2549f-173">`.sln`ファイル</span><span class="sxs-lookup"><span data-stu-id="2549f-173">`.sln` file</span></span> | <span data-ttu-id="2549f-174">ソリューションで識別されるパッケージを復元します。エラーは、`-SolutionDirectory`を使用します。</span><span class="sxs-lookup"><span data-stu-id="2549f-174">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="2549f-175">`$(SolutionDir)\.nuget`開始フォルダーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="2549f-175">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span>
    <span data-ttu-id="2549f-176">`packages.config`、 `project.json`、またはプロジェクト ファイル</span><span class="sxs-lookup"><span data-stu-id="2549f-176">`packages.config`, `project.json`, or project file</span></span> | <span data-ttu-id="2549f-177">解決して、依存関係をインストール ファイルに表示されているパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="2549f-177">Restore packages listed in the file, resolving and installing dependencies.</span></span>
    <span data-ttu-id="2549f-178">その他のファイルの種類</span><span class="sxs-lookup"><span data-stu-id="2549f-178">Other file type</span></span> | <span data-ttu-id="2549f-179">ファイルがあると見なされます、 `.sln` ; 上記と同じファイルのない場合は、ソリューションでは、NuGet により、エラーが発生します。</span><span class="sxs-lookup"><span data-stu-id="2549f-179">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span>
    <span data-ttu-id="2549f-180">(指定されていない projectPath)</span><span class="sxs-lookup"><span data-stu-id="2549f-180">(projectPath not specified)</span></span> | <span data-ttu-id="2549f-181">-NuGet は、現在のフォルダーにソリューション ファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="2549f-181">- NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="2549f-182">パッケージ; を復元する 1 つが使用される 1 つのファイルが見つかった場合、複数のソリューションが見つからない場合は、NuGet は、エラーを示します。</span><span class="sxs-lookup"><span data-stu-id="2549f-182">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span>
    |<span data-ttu-id="2549f-183">-NuGet 検索ソリューション ファイルが存在しない場合、`packages.config`または`project.json`しパッケージを復元するを使用します。</span><span class="sxs-lookup"><span data-stu-id="2549f-183">- If there are no solution files, NuGet looks for a `packages.config` or `project.json` and uses that to restore packages.</span></span>
    |<span data-ttu-id="2549f-184">-場合ないソリューション ファイル`packages.config`、または`project.json`が見つかると、NuGet は、エラーを示します。</span><span class="sxs-lookup"><span data-stu-id="2549f-184">- If no solution file, `packages.config`, or `project.json` is found, NuGet gives an error.</span></span>

1. <span data-ttu-id="2549f-185">次の優先順位 (NuGet は、これらのフォルダーが見つからない場合に、エラーを提供) を使用して、パッケージ フォルダーを決定します。</span><span class="sxs-lookup"><span data-stu-id="2549f-185">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="2549f-186">`%userprofile%\.nuget\packages`値`project.json`です。</span><span class="sxs-lookup"><span data-stu-id="2549f-186">The `%userprofile%\.nuget\packages` value in `project.json`.</span></span>
    - <span data-ttu-id="2549f-187">指定されたフォルダー`-PackagesDirectory`です。</span><span class="sxs-lookup"><span data-stu-id="2549f-187">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="2549f-188">`repositoryPath`で vale`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="2549f-188">The `repositoryPath` vale in `Nuget.Config`</span></span>
    - <span data-ttu-id="2549f-189">指定されたフォルダー`-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="2549f-189">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

1. <span data-ttu-id="2549f-190">ソリューションのパッケージを復元するには、NuGet は、次を行います。</span><span class="sxs-lookup"><span data-stu-id="2549f-190">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="2549f-191">ソリューション ファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="2549f-191">Loads the solution file.</span></span>
    - <span data-ttu-id="2549f-192">表示されているソリューション レベルのパッケージを復元`$(SolutionDir)\.nuget\packages.config`に、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="2549f-192">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="2549f-193">表示されているパッケージを復元`$(ProjectDir)\packages.config`に、`packages`フォルダーです。</span><span class="sxs-lookup"><span data-stu-id="2549f-193">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="2549f-194">指定されたパッケージごとに、必要ない限り、並列でパッケージを復元`-DisableParallelProcessing`を指定します。</span><span class="sxs-lookup"><span data-stu-id="2549f-194">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="2549f-195">例</span><span class="sxs-lookup"><span data-stu-id="2549f-195">Examples</span></span>

```
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
