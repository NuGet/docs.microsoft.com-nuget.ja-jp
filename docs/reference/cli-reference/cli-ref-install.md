---
title: NuGet CLI install コマンド
description: Nuget.exe install コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327789"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="64900-103">install コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="64900-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="64900-104">**適用対象:** パッケージの&bullet;使用量が**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="64900-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="64900-105">パッケージをダウンロードしてプロジェクトにインストールします。指定したパッケージソースを使用して、既定で現在のフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="64900-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="64900-106">プロジェクトのコンテキストの外部でパッケージを直接ダウンロードするには、 [nuget.org](https://www.nuget.org)のパッケージのページにアクセスし、 **[ダウンロード]** リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="64900-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="64900-107">ソースが指定されていない場合は、グローバル構成ファイル`%appdata%\NuGet\NuGet.Config` (Windows) また`~/.nuget/NuGet/NuGet.Config`は (Mac/Linux) に記載されているものが使用されます。</span><span class="sxs-lookup"><span data-stu-id="64900-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="64900-108">詳細については、「[一般的な NuGet の構成](../../consume-packages/configuring-nuget-behavior.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="64900-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="64900-109">特定のパッケージが指定され`install`ていない場合、は、プロジェクト`packages.config`のファイルに一覧表示さ[`restore`](cli-ref-restore.md)れているすべてのパッケージをインストールして、のようにします。</span><span class="sxs-lookup"><span data-stu-id="64900-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="64900-110">このコマンドは、プロジェクトファイルまたはを`packages.config`変更しません。この`restore`方法では、パッケージをディスクに追加するだけで、プロジェクトの依存関係は変更しないという点でも同様です。 `install`</span><span class="sxs-lookup"><span data-stu-id="64900-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="64900-111">依存関係を追加するには、Visual Studio のパッケージマネージャー UI またはコンソールを使用してパッケージ`packages.config`を追加するか`install` 、 `restore`またはを変更して実行します。</span><span class="sxs-lookup"><span data-stu-id="64900-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="64900-112">使用法</span><span class="sxs-lookup"><span data-stu-id="64900-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="64900-113">(最新バージョンを使用して) インストールするパッケージの`<configFilePath>` `packages.config` 名前を指定するか、インストールするパッケージの一覧を示すファイルを`<packageID>`指定します。</span><span class="sxs-lookup"><span data-stu-id="64900-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="64900-114">`-Version`オプションを使用して特定のバージョンを指定できます。</span><span class="sxs-lookup"><span data-stu-id="64900-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="64900-115">オプション</span><span class="sxs-lookup"><span data-stu-id="64900-115">Options</span></span>

| <span data-ttu-id="64900-116">オプション</span><span class="sxs-lookup"><span data-stu-id="64900-116">Option</span></span> | <span data-ttu-id="64900-117">説明</span><span class="sxs-lookup"><span data-stu-id="64900-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64900-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="64900-118">ConfigFile</span></span> | <span data-ttu-id="64900-119">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="64900-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="64900-120">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="64900-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="64900-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="64900-121">DependencyVersion</span></span> | <span data-ttu-id="64900-122">*(4.4 以降)* 使用する依存関係パッケージのバージョン。次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="64900-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="64900-123">*最低*(既定): 最も低いバージョン</span><span class="sxs-lookup"><span data-stu-id="64900-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="64900-124">*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</span><span class="sxs-lookup"><span data-stu-id="64900-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="64900-125">*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</span><span class="sxs-lookup"><span data-stu-id="64900-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="64900-126">*最高*: 最高バージョン</span><span class="sxs-lookup"><span data-stu-id="64900-126">*Highest*: the highest version</span></span></li></ul> |
| <span data-ttu-id="64900-127">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="64900-127">DisableParallelProcessing</span></span> | <span data-ttu-id="64900-128">複数のパッケージの並列インストールを無効にします。</span><span class="sxs-lookup"><span data-stu-id="64900-128">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="64900-129">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="64900-129">ExcludeVersion</span></span> | <span data-ttu-id="64900-130">パッケージ名がではなく、パッケージ名だけを持つという名前のフォルダーにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="64900-130">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="64900-131">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="64900-131">FallbackSource</span></span> | <span data-ttu-id="64900-132">*(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。</span><span class="sxs-lookup"><span data-stu-id="64900-132">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="64900-133">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="64900-133">ForceEnglishOutput</span></span> | <span data-ttu-id="64900-134">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="64900-134">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="64900-135">Framework</span><span class="sxs-lookup"><span data-stu-id="64900-135">Framework</span></span> | <span data-ttu-id="64900-136">*(4.4 以降)* 依存関係の選択に使用されるターゲットフレームワーク。</span><span class="sxs-lookup"><span data-stu-id="64900-136">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="64900-137">指定しない場合、既定値は ' Any ' になります。</span><span class="sxs-lookup"><span data-stu-id="64900-137">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="64900-138">Help</span><span class="sxs-lookup"><span data-stu-id="64900-138">Help</span></span> | <span data-ttu-id="64900-139">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="64900-139">Displays help information for the command.</span></span> |
| <span data-ttu-id="64900-140">NoCache</span><span class="sxs-lookup"><span data-stu-id="64900-140">NoCache</span></span> | <span data-ttu-id="64900-141">NuGet がキャッシュされたパッケージを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="64900-141">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="64900-142">「[グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="64900-142">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="64900-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="64900-143">NonInteractive</span></span> | <span data-ttu-id="64900-144">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="64900-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="64900-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="64900-145">OutputDirectory</span></span> | <span data-ttu-id="64900-146">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="64900-146">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="64900-147">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="64900-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="64900-148">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="64900-148">PackageSaveMode</span></span> | <span data-ttu-id="64900-149">パッケージのインストール後に保存するファイルの種類を指定し`nuspec`ます`nupkg`。、 `nuspec;nupkg`、またはのいずれかです。</span><span class="sxs-lookup"><span data-stu-id="64900-149">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="64900-150">PreRelease</span><span class="sxs-lookup"><span data-stu-id="64900-150">PreRelease</span></span> | <span data-ttu-id="64900-151">プレリリースパッケージのインストールを許可します。</span><span class="sxs-lookup"><span data-stu-id="64900-151">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="64900-152">このフラグは、を使用してパッケージ`packages.config`を復元する場合には必要ありません。</span><span class="sxs-lookup"><span data-stu-id="64900-152">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="64900-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="64900-153">RequireConsent</span></span> | <span data-ttu-id="64900-154">パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="64900-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="64900-155">詳細については、「[パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="64900-155">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="64900-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="64900-156">SolutionDirectory</span></span> | <span data-ttu-id="64900-157">パッケージを復元するソリューションのルートフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="64900-157">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="64900-158">Source</span><span class="sxs-lookup"><span data-stu-id="64900-158">Source</span></span> | <span data-ttu-id="64900-159">使用するパッケージソースの一覧を Url として指定します。</span><span class="sxs-lookup"><span data-stu-id="64900-159">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="64900-160">省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="64900-160">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="64900-161">Verbosity</span><span class="sxs-lookup"><span data-stu-id="64900-161">Verbosity</span></span> | <span data-ttu-id="64900-162">出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="64900-162">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="64900-163">Version</span><span class="sxs-lookup"><span data-stu-id="64900-163">Version</span></span> | <span data-ttu-id="64900-164">インストールするパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="64900-164">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="64900-165">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="64900-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="64900-166">使用例</span><span class="sxs-lookup"><span data-stu-id="64900-166">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
