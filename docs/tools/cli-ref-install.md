---
title: NuGet CLI のインストール コマンド
description: Nuget.exe install コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e609b01bc14083ce212f6d4d4c6d3412f0ee316b
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508323"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="82d8d-103">Install コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="82d8d-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="82d8d-104">**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="82d8d-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="82d8d-105">ダウンロードし、既定では、現在のフォルダーを指定したパッケージ ソースを使用して、プロジェクトにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="82d8d-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="82d8d-106">プロジェクトのコンテキスト外で直接パッケージをダウンロードするには、パッケージのページを参照してください。 [nuget.org](https://www.nuget.org)を選択し、**ダウンロード**リンク。</span><span class="sxs-lookup"><span data-stu-id="82d8d-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="82d8d-107">ソースが指定されていない場合、グローバル構成ファイルに一覧表示`%appdata%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) 使用されます。</span><span class="sxs-lookup"><span data-stu-id="82d8d-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="82d8d-108">参照してください[NuGet の構成の動作を](../consume-packages/configuring-nuget-behavior.md)詳細。</span><span class="sxs-lookup"><span data-stu-id="82d8d-108">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="82d8d-109">特定のパッケージが指定されていない場合`install`プロジェクトの一覧にあるすべてのパッケージをインストール`packages.config`ようなファイル[ `restore`](cli-ref-restore.md)します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="82d8d-110">`install`コマンドでは、プロジェクト ファイルは変更しませんまたは`packages.config`; に似ていますが、この方法で`restore`のみにパッケージをディスクに追加しますが、プロジェクトの依存関係を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="82d8d-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="82d8d-111">依存関係を追加するか、Visual Studio でパッケージ マネージャー UI またはコンソールを使用してパッケージを追加または変更`packages.config`いずれかを実行および`install`または`restore`します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="82d8d-112">使用法</span><span class="sxs-lookup"><span data-stu-id="82d8d-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="82d8d-113">場所`<packageID>`(最新バージョンを使用) をインストールするパッケージの名前または`<configFilePath>`を識別、`packages.config`ファイルをインストールするパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="82d8d-114">特定のバージョンを示すことができます、`-Version`オプション。</span><span class="sxs-lookup"><span data-stu-id="82d8d-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="82d8d-115">オプション</span><span class="sxs-lookup"><span data-stu-id="82d8d-115">Options</span></span>

| <span data-ttu-id="82d8d-116">オプション</span><span class="sxs-lookup"><span data-stu-id="82d8d-116">Option</span></span> | <span data-ttu-id="82d8d-117">説明</span><span class="sxs-lookup"><span data-stu-id="82d8d-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="82d8d-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="82d8d-118">ConfigFile</span></span> | <span data-ttu-id="82d8d-119">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="82d8d-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="82d8d-120">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="82d8d-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="82d8d-121">DependencyVersion</span></span> | <span data-ttu-id="82d8d-122">*(4.4 以降)* 次のいずれかの値を使用する依存関係パッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="82d8d-122">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="82d8d-123">*最も低い*(既定値): 最小バージョン</span><span class="sxs-lookup"><span data-stu-id="82d8d-123">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="82d8d-124">*HighestPatch*: 最高レベルの最も大きなを最低軽微な修正プログラムのバージョン</span><span class="sxs-lookup"><span data-stu-id="82d8d-124">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="82d8d-125">*HighestMinor*: 主要な最小のバージョン、マイナー、最高の最高の修正プログラム</span><span class="sxs-lookup"><span data-stu-id="82d8d-125">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="82d8d-126">*最も高い*: 最上位のバージョン</span><span class="sxs-lookup"><span data-stu-id="82d8d-126">*Highest*: the highest version</span></span></li></ul> |
| <span data-ttu-id="82d8d-127">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="82d8d-127">DisableParallelProcessing</span></span> | <span data-ttu-id="82d8d-128">複数のパッケージを並列でインストールを無効にします。</span><span class="sxs-lookup"><span data-stu-id="82d8d-128">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="82d8d-129">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="82d8d-129">ExcludeVersion</span></span> | <span data-ttu-id="82d8d-130">パッケージ名のみとバージョン番号ではないという名前のフォルダーにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="82d8d-130">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="82d8d-131">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="82d8d-131">FallbackSource</span></span> | <span data-ttu-id="82d8d-132">*(3.2 以降)* プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。</span><span class="sxs-lookup"><span data-stu-id="82d8d-132">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="82d8d-133">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="82d8d-133">ForceEnglishOutput</span></span> | <span data-ttu-id="82d8d-134">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-134">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="82d8d-135">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="82d8d-135">Framework</span></span> | <span data-ttu-id="82d8d-136">*(4.4 以降)* ターゲット フレームワークの依存関係を選択するために使用します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-136">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="82d8d-137">'に指定されていない場合の既定値です。</span><span class="sxs-lookup"><span data-stu-id="82d8d-137">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="82d8d-138">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="82d8d-138">Help</span></span> | <span data-ttu-id="82d8d-139">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-139">Displays help information for the command.</span></span> |
| <span data-ttu-id="82d8d-140">NoCache</span><span class="sxs-lookup"><span data-stu-id="82d8d-140">NoCache</span></span> | <span data-ttu-id="82d8d-141">NuGet がキャッシュされたパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="82d8d-141">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="82d8d-142">参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-142">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="82d8d-143">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="82d8d-143">NonInteractive</span></span> | <span data-ttu-id="82d8d-144">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-144">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="82d8d-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="82d8d-145">OutputDirectory</span></span> | <span data-ttu-id="82d8d-146">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-146">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="82d8d-147">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="82d8d-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="82d8d-148">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="82d8d-148">PackageSaveMode</span></span> | <span data-ttu-id="82d8d-149">パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-149">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="82d8d-150">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="82d8d-150">PreRelease</span></span> | <span data-ttu-id="82d8d-151">インストールするプレリリース パッケージを使用できます。</span><span class="sxs-lookup"><span data-stu-id="82d8d-151">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="82d8d-152">このフラグを使用してパッケージを復元するときに必要ありません`packages.config`します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-152">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="82d8d-153">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="82d8d-153">RequireConsent</span></span> | <span data-ttu-id="82d8d-154">ダウンロードして、パッケージをインストールする前にパッケージの復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-154">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="82d8d-155">詳細については、次を参照してください。[パッケージの復元](../consume-packages/package-restore.md)します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-155">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="82d8d-156">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="82d8d-156">SolutionDirectory</span></span> | <span data-ttu-id="82d8d-157">パッケージを復元する対象のソリューションのルート フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-157">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="82d8d-158">ソース</span><span class="sxs-lookup"><span data-stu-id="82d8d-158">Source</span></span> | <span data-ttu-id="82d8d-159">パッケージ ソースの一覧を使用する (Url) として指定します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-159">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="82d8d-160">コマンドを省略すると、構成ファイルで提供されるソースを使用して、参照してください[NuGet の構成の動作を](../consume-packages/configuring-nuget-behavior.md)します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-160">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="82d8d-161">詳細度</span><span class="sxs-lookup"><span data-stu-id="82d8d-161">Verbosity</span></span> | <span data-ttu-id="82d8d-162">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-162">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="82d8d-163">Version</span><span class="sxs-lookup"><span data-stu-id="82d8d-163">Version</span></span> | <span data-ttu-id="82d8d-164">インストールするパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="82d8d-164">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="82d8d-165">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="82d8d-165">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="82d8d-166">使用例</span><span class="sxs-lookup"><span data-stu-id="82d8d-166">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
