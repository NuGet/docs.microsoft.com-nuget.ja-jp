---
title: NuGet CLI install コマンド
description: Nuget.exe install コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036943"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="f80b0-103">install コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f80b0-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="f80b0-104">**適用対象:** パッケージ消費 &bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="f80b0-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f80b0-105">パッケージをダウンロードしてプロジェクトにインストールします。指定したパッケージソースを使用して、既定で現在のフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="f80b0-106">プロジェクトのコンテキストの外部でパッケージを直接ダウンロードするには、 [nuget.org](https://www.nuget.org)のパッケージのページにアクセスし、 **[ダウンロード]** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="f80b0-107">ソースが指定されていない場合は、グローバル構成ファイル、`%appdata%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) に記載されているものが使用されます。</span><span class="sxs-lookup"><span data-stu-id="f80b0-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="f80b0-108">詳細については、「[一般的な NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f80b0-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="f80b0-109">特定のパッケージが指定されていない場合は、`install` プロジェクトの `packages.config` ファイルに一覧表示されているすべてのパッケージがインストールされ、 [`restore`](cli-ref-restore.md)のようになります。</span><span class="sxs-lookup"><span data-stu-id="f80b0-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="f80b0-110">`install` コマンドでは、プロジェクトファイルや `packages.config`は変更されません。この方法では、パッケージをディスクに追加するだけで、プロジェクトの依存関係は変更しないという点で `restore` に似ています。</span><span class="sxs-lookup"><span data-stu-id="f80b0-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="f80b0-111">依存関係を追加するには、Visual Studio のパッケージマネージャー UI またはコンソールを使用してパッケージを追加するか、`packages.config` を変更して `install` または `restore`を実行します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="f80b0-112">使用方法</span><span class="sxs-lookup"><span data-stu-id="f80b0-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="f80b0-113">インストールするパッケージの `<packageID>` 名前 (最新バージョンを使用)、または `<configFilePath>` インストールするパッケージの一覧を示す `packages.config` ファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="f80b0-114">`-Version` オプションを使用して特定のバージョンを指定できます。</span><span class="sxs-lookup"><span data-stu-id="f80b0-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="f80b0-115">オプション</span><span class="sxs-lookup"><span data-stu-id="f80b0-115">Options</span></span>

| <span data-ttu-id="f80b0-116">オプション</span><span class="sxs-lookup"><span data-stu-id="f80b0-116">Option</span></span> | <span data-ttu-id="f80b0-117">[説明]</span><span class="sxs-lookup"><span data-stu-id="f80b0-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f80b0-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f80b0-118">ConfigFile</span></span> | <span data-ttu-id="f80b0-119">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="f80b0-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f80b0-120">指定しない場合は、`%AppData%\NuGet\NuGet.Config` (Windows) または `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="f80b0-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f80b0-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f80b0-121">DependencyVersion</span></span> | <span data-ttu-id="f80b0-122">*(4.4 以降)* 使用する依存関係パッケージのバージョン。次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="f80b0-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f80b0-123">*最低*(既定): 最も低いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="f80b0-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f80b0-124">*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</span><span class="sxs-lookup"><span data-stu-id="f80b0-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f80b0-125">*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</span><span class="sxs-lookup"><span data-stu-id="f80b0-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f80b0-126">*最高*: 最高バージョン</span><span class="sxs-lookup"><span data-stu-id="f80b0-126">*Highest*: the highest version</span></span></li><li><span data-ttu-id="f80b0-127">*無視*: 依存関係パッケージは使用されません</span><span class="sxs-lookup"><span data-stu-id="f80b0-127">*Ignore*: No dependency packages will be used</span></span></li></ul> |
| <span data-ttu-id="f80b0-128">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="f80b0-128">DisableParallelProcessing</span></span> | <span data-ttu-id="f80b0-129">複数のパッケージの並列インストールを無効にします。</span><span class="sxs-lookup"><span data-stu-id="f80b0-129">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="f80b0-130">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="f80b0-130">ExcludeVersion</span></span> | <span data-ttu-id="f80b0-131">パッケージ名がではなく、パッケージ名だけを持つという名前のフォルダーにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f80b0-131">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="f80b0-132">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="f80b0-132">FallbackSource</span></span> | <span data-ttu-id="f80b0-133">*(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。</span><span class="sxs-lookup"><span data-stu-id="f80b0-133">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="f80b0-134">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f80b0-134">ForceEnglishOutput</span></span> | <span data-ttu-id="f80b0-135">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-135">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f80b0-136">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="f80b0-136">Framework</span></span> | <span data-ttu-id="f80b0-137">*(4.4 以降)* 依存関係の選択に使用されるターゲットフレームワーク。</span><span class="sxs-lookup"><span data-stu-id="f80b0-137">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="f80b0-138">指定しない場合、既定値は ' Any ' になります。</span><span class="sxs-lookup"><span data-stu-id="f80b0-138">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="f80b0-139">[Help]</span><span class="sxs-lookup"><span data-stu-id="f80b0-139">Help</span></span> | <span data-ttu-id="f80b0-140">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-140">Displays help information for the command.</span></span> |
| <span data-ttu-id="f80b0-141">NoCache</span><span class="sxs-lookup"><span data-stu-id="f80b0-141">NoCache</span></span> | <span data-ttu-id="f80b0-142">NuGet がキャッシュされたパッケージを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="f80b0-142">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="f80b0-143">「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="f80b0-143">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="f80b0-144">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f80b0-144">NonInteractive</span></span> | <span data-ttu-id="f80b0-145">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="f80b0-145">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f80b0-146">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="f80b0-146">OutputDirectory</span></span> | <span data-ttu-id="f80b0-147">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-147">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="f80b0-148">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="f80b0-148">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="f80b0-149">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="f80b0-149">PackageSaveMode</span></span> | <span data-ttu-id="f80b0-150">パッケージのインストール後に保存するファイルの種類を指定します。 `nuspec`、`nupkg`、`nuspec;nupkg`のいずれかです。</span><span class="sxs-lookup"><span data-stu-id="f80b0-150">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="f80b0-151">PreRelease</span><span class="sxs-lookup"><span data-stu-id="f80b0-151">PreRelease</span></span> | <span data-ttu-id="f80b0-152">プレリリースパッケージのインストールを許可します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-152">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="f80b0-153">`packages.config`でパッケージを復元する場合、このフラグは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="f80b0-153">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="f80b0-154">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="f80b0-154">RequireConsent</span></span> | <span data-ttu-id="f80b0-155">パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-155">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="f80b0-156">詳細については、「[パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f80b0-156">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="f80b0-157">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="f80b0-157">SolutionDirectory</span></span> | <span data-ttu-id="f80b0-158">パッケージを復元するソリューションのルートフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-158">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="f80b0-159">[ソース]</span><span class="sxs-lookup"><span data-stu-id="f80b0-159">Source</span></span> | <span data-ttu-id="f80b0-160">使用するパッケージソースの一覧を Url として指定します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-160">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="f80b0-161">省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="f80b0-161">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="f80b0-162">詳細度</span><span class="sxs-lookup"><span data-stu-id="f80b0-162">Verbosity</span></span> | <span data-ttu-id="f80b0-163">出力に表示される詳細の量を指定します (*通常*、*非*表示、*詳細*)。</span><span class="sxs-lookup"><span data-stu-id="f80b0-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="f80b0-164">バージョン</span><span class="sxs-lookup"><span data-stu-id="f80b0-164">Version</span></span> | <span data-ttu-id="f80b0-165">インストールするパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="f80b0-165">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="f80b0-166">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="f80b0-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f80b0-167">例</span><span class="sxs-lookup"><span data-stu-id="f80b0-167">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
