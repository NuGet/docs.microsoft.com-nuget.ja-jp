---
title: NuGet CLI の復元コマンド
description: nuget.exe restore コマンドのリファレンス
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 49fabbd0ef0c1c0c16f13bdf741296575fa72359
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780035"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="97959-103">restore コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="97959-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="97959-104">**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** 2.7 以上</span><span class="sxs-lookup"><span data-stu-id="97959-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="97959-105">フォルダーにないパッケージをダウンロードしてインストールし `packages` ます。</span><span class="sxs-lookup"><span data-stu-id="97959-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="97959-106">NuGet 4.0 + および PackageReference 形式と共に使用すると、必要に応じて `<project>.nuget.props` フォルダー内にファイルが生成され `obj` ます。</span><span class="sxs-lookup"><span data-stu-id="97959-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="97959-107">(ファイルはソース管理から省略できます)。</span><span class="sxs-lookup"><span data-stu-id="97959-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="97959-108">Mono で CLI を使用している Mac OSX と Linux では、パッケージの復元は PackageReference ではサポートされていません。</span><span class="sxs-lookup"><span data-stu-id="97959-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="97959-109">使用方法</span><span class="sxs-lookup"><span data-stu-id="97959-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="97959-110">ここ `<projectPath>` では、ソリューションまたはファイルの場所を指定し `packages.config` ます。</span><span class="sxs-lookup"><span data-stu-id="97959-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="97959-111">動作の詳細については、以下の [解説](#remarks) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97959-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="97959-112">Options</span><span class="sxs-lookup"><span data-stu-id="97959-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="97959-113">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="97959-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="97959-114">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="97959-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="97959-115">*(4.0 以降)* バイナリまたはメタデータを使用してキャッシュを設定せずに、パッケージを直接ダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="97959-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="97959-116">複数のパッケージの並列復元を無効にします。</span><span class="sxs-lookup"><span data-stu-id="97959-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="97959-117">*(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。</span><span class="sxs-lookup"><span data-stu-id="97959-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="97959-118">リストエントリを区切るには、セミコロンを使用します。</span><span class="sxs-lookup"><span data-stu-id="97959-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="97959-119">PackageReference ベースのプロジェクトでは、最後の復元が成功した場合でも、すべての依存関係が強制的に解決されます。</span><span class="sxs-lookup"><span data-stu-id="97959-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="97959-120">このフラグを指定することは、ファイルの削除に似てい `project.assets.json` ます。</span><span class="sxs-lookup"><span data-stu-id="97959-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="97959-121">これは、http キャッシュをバイパスしません。</span><span class="sxs-lookup"><span data-stu-id="97959-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="97959-122">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="97959-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="97959-123">ロック ファイルが既に存在する場合でも、すべての依存関係を再評価するように強制的に復元します。</span><span class="sxs-lookup"><span data-stu-id="97959-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="97959-124">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="97959-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="97959-125">プロジェクトのロック ファイルの書き込み先である出力場所。</span><span class="sxs-lookup"><span data-stu-id="97959-125">Output location where project lock file is written.</span></span> <span data-ttu-id="97959-126">既定値は `PROJECT_ROOT\packages.lock.json` です。</span><span class="sxs-lookup"><span data-stu-id="97959-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="97959-127">プロジェクト ロック ファイルの更新は許可されません。</span><span class="sxs-lookup"><span data-stu-id="97959-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="97959-128">*(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これはよりも優先さ `-MSBuildVersion` れます。</span><span class="sxs-lookup"><span data-stu-id="97959-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="97959-129">*(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="97959-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="97959-130">サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。</span><span class="sxs-lookup"><span data-stu-id="97959-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="97959-131">既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。</span><span class="sxs-lookup"><span data-stu-id="97959-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="97959-132">NuGet がキャッシュされたパッケージを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="97959-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="97959-133">「 [グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="97959-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="97959-134">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="97959-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="97959-135">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="97959-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="97959-136">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="97959-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="97959-137">`packages.config` `PackagesDirectory` またはが使用されている場合を除き、ファイルを使用して復元する場合に必要です `SolutionDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="97959-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="97959-138">パッケージのインストール後に保存するファイルの種類を指定します。、、またはのいずれか `nuspec` `nupkg` `nuspec;nupkg` です。</span><span class="sxs-lookup"><span data-stu-id="97959-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="97959-139">`OutputDirectory` と同じ。</span><span class="sxs-lookup"><span data-stu-id="97959-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="97959-140">`packages.config` `OutputDirectory` またはが使用されている場合を除き、ファイルを使用して復元する場合に必要です `SolutionDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="97959-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="97959-141">プロジェクト間参照を解決するためのタイムアウト (秒)。</span><span class="sxs-lookup"><span data-stu-id="97959-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="97959-142">*(4.0 以降)* UWP および .NET Core プロジェクトのすべての参照プロジェクトを復元します。</span><span class="sxs-lookup"><span data-stu-id="97959-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="97959-143">は、を使用するプロジェクトには適用されません `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="97959-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="97959-144">パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="97959-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="97959-145">詳細については、「 [パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97959-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="97959-146">ソリューションフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="97959-146">Specifies the solution folder.</span></span> <span data-ttu-id="97959-147">ソリューションのパッケージを復元するときには無効です。</span><span class="sxs-lookup"><span data-stu-id="97959-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="97959-148">`packages.config` `PackagesDirectory` またはが使用されている場合を除き、ファイルを使用して復元する場合に必要です `OutputDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="97959-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="97959-149">復元に使用するパッケージソースの一覧を Url として指定します。</span><span class="sxs-lookup"><span data-stu-id="97959-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="97959-150">省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [NuGet の動作の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="97959-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="97959-151">リストエントリを区切るには、セミコロンを使用します。</span><span class="sxs-lookup"><span data-stu-id="97959-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="97959-152">プロジェクト ロック ファイルを生成して復元で使用できるようにします。</span><span class="sxs-lookup"><span data-stu-id="97959-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="97959-153">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="97959-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="97959-154">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="97959-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="97959-155">解説</span><span class="sxs-lookup"><span data-stu-id="97959-155">Remarks</span></span>

<span data-ttu-id="97959-156">Restore コマンドは、次の手順を実行します。</span><span class="sxs-lookup"><span data-stu-id="97959-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="97959-157">Restore コマンドの操作モードを決定します。</span><span class="sxs-lookup"><span data-stu-id="97959-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="97959-158">projectPath ファイルの種類</span><span class="sxs-lookup"><span data-stu-id="97959-158">projectPath file type</span></span> | <span data-ttu-id="97959-159">動作</span><span class="sxs-lookup"><span data-stu-id="97959-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="97959-160">ソリューション (フォルダー)</span><span class="sxs-lookup"><span data-stu-id="97959-160">Solution (folder)</span></span> | <span data-ttu-id="97959-161">NuGet はファイルを検索 `.sln` し、見つかった場合はそれを使用します。それ以外の場合はエラーを返します。</span><span class="sxs-lookup"><span data-stu-id="97959-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="97959-162">`(SolutionDir)\.nuget` は、開始フォルダーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="97959-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="97959-163">`.sln` ファイル</span><span class="sxs-lookup"><span data-stu-id="97959-163">`.sln` file</span></span> | <span data-ttu-id="97959-164">ソリューションによって識別されたパッケージを復元します。が使用されている場合は、エラーが発生 `-SolutionDirectory` します。</span><span class="sxs-lookup"><span data-stu-id="97959-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="97959-165">`$(SolutionDir)\.nuget` は、開始フォルダーとして使用されます。</span><span class="sxs-lookup"><span data-stu-id="97959-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="97959-166">`packages.config` またはプロジェクトファイル</span><span class="sxs-lookup"><span data-stu-id="97959-166">`packages.config` or project file</span></span> | <span data-ttu-id="97959-167">ファイルに一覧表示されているパッケージを復元し、依存関係を解決してインストールします。</span><span class="sxs-lookup"><span data-stu-id="97959-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="97959-168">その他のファイルの種類</span><span class="sxs-lookup"><span data-stu-id="97959-168">Other file type</span></span> | <span data-ttu-id="97959-169">ファイルは上記のファイルと見なされ `.sln` ます。ソリューションでない場合は、NuGet によってエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="97959-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="97959-170">(projectPath が指定されていません)</span><span class="sxs-lookup"><span data-stu-id="97959-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="97959-171">NuGet は、現在のフォルダーにあるソリューションファイルを検索します。</span><span class="sxs-lookup"><span data-stu-id="97959-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="97959-172">1つのファイルが見つかった場合は、そのファイルを使用してパッケージを復元します。複数のソリューションが見つかった場合は、NuGet によってエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="97959-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="97959-173">ソリューションファイルがない場合、NuGet はを検索 `packages.config` し、それを使用してパッケージを復元します。</span><span class="sxs-lookup"><span data-stu-id="97959-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="97959-174">ソリューションまたは `packages.config` ファイルが見つからない場合は、NuGet によってエラーが返されます。</span><span class="sxs-lookup"><span data-stu-id="97959-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="97959-175">次の優先順位を使用して packages フォルダーを特定します (これらのフォルダーが見つからない場合は、NuGet によってエラーが返されます)。</span><span class="sxs-lookup"><span data-stu-id="97959-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="97959-176">で指定されたフォルダー `-PackagesDirectory` 。</span><span class="sxs-lookup"><span data-stu-id="97959-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="97959-177">`repositoryPath`の値`Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="97959-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="97959-178">で指定されたフォルダー `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="97959-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="97959-179">ソリューションのパッケージを復元するとき、NuGet は次のことを行います。</span><span class="sxs-lookup"><span data-stu-id="97959-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="97959-180">ソリューションファイルを読み込みます。</span><span class="sxs-lookup"><span data-stu-id="97959-180">Loads the solution file.</span></span>
    - <span data-ttu-id="97959-181">に一覧表示されているソリューションレベル `$(SolutionDir)\.nuget\packages.config` のパッケージをフォルダーに復元 `packages` します。</span><span class="sxs-lookup"><span data-stu-id="97959-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="97959-182">に一覧表示されているパッケージ `$(ProjectDir)\packages.config` をフォルダーに復元 `packages` します。</span><span class="sxs-lookup"><span data-stu-id="97959-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="97959-183">が指定されている場合を除き、指定したパッケージごとに、並列でパッケージを復元し `-DisableParallelProcessing` ます。</span><span class="sxs-lookup"><span data-stu-id="97959-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="97959-184">使用例</span><span class="sxs-lookup"><span data-stu-id="97959-184">Examples</span></span>

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
