---
title: NuGet CLI-install コマンド
description: Nuget.exe-install コマンドのリファレンス
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 615f2beca1eb288417f2345fcdf25e323942d300
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="f1bf8-103">Install コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="f1bf8-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="f1bf8-104">**適用されます:** 消費をパッケージ化&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="f1bf8-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="f1bf8-105">ダウンロードし、指定したパッケージ ソースを使用して、現在のフォルダーには、既定のプロジェクトにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="f1bf8-106">プロジェクトのコンテキスト外で直接パッケージをダウンロードするには、ページにアクセスして、パッケージの[nuget.org](https://www.nuget.org)を選択し、**ダウンロード**リンクします。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="f1bf8-107">ソースが指定されていない場合、グローバル構成ファイルに一覧表示`%appdata%\NuGet\NuGet.Config`(Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="f1bf8-108">参照してください[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)の詳細。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-108">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="f1bf8-109">特定のパッケージが指定されていない場合`install`プロジェクトの表示されているすべてのパッケージをインストール`packages.config`ようなファイル[ `restore`](cli-ref-restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="f1bf8-110">`install`コマンドは、プロジェクト ファイルを変更していないまたは`packages.config`; に似ていますが、この方法で`restore`のみにパッケージをディスクに追加、プロジェクトの依存関係を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="f1bf8-111">依存関係を追加するか、Visual Studio で、パッケージ マネージャー UI またはコンソール経由で、プロジェクトを追加または変更`packages.config`いずれかを実行および`install`または`restore`です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-111">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="f1bf8-112">使用法</span><span class="sxs-lookup"><span data-stu-id="f1bf8-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="f1bf8-113">ここで`<packageID>`(最新バージョンを使用) をインストールするパッケージの名前または`<configFilePath>`を識別、`packages.config`ファイルをインストールするパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="f1bf8-114">特定のバージョンを指定することができます、`-Version`オプション。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="f1bf8-115">オプション</span><span class="sxs-lookup"><span data-stu-id="f1bf8-115">Options</span></span>

| <span data-ttu-id="f1bf8-116">オプション</span><span class="sxs-lookup"><span data-stu-id="f1bf8-116">Option</span></span> | <span data-ttu-id="f1bf8-117">説明</span><span class="sxs-lookup"><span data-stu-id="f1bf8-117">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f1bf8-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f1bf8-118">ConfigFile</span></span> | <span data-ttu-id="f1bf8-119">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f1bf8-120">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f1bf8-121">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f1bf8-121">DependencyVersion</span></span> | <span data-ttu-id="f1bf8-122">*(4.4 +)* 既定の依存関係の解決の動作をオーバーライドする特定のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-122">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="f1bf8-123">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="f1bf8-123">DisableParallelProcessing</span></span> | <span data-ttu-id="f1bf8-124">複数のパッケージを並列でインストールを無効にします。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-124">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="f1bf8-125">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="f1bf8-125">ExcludeVersion</span></span> | <span data-ttu-id="f1bf8-126">パッケージ名のみとバージョン番号ではないという名前のフォルダーにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-126">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="f1bf8-127">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="f1bf8-127">FallbackSource</span></span> | <span data-ttu-id="f1bf8-128">*(3.2 +)* プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-128">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="f1bf8-129">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f1bf8-129">ForceEnglishOutput</span></span> | <span data-ttu-id="f1bf8-130">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-130">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f1bf8-131">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="f1bf8-131">Framework</span></span> | <span data-ttu-id="f1bf8-132">*(4.4 +)* ターゲット フレームワークの依存関係を選択するために使用します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-132">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="f1bf8-133">'Any' に指定されていない場合の既定値です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-133">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="f1bf8-134">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="f1bf8-134">Help</span></span> | <span data-ttu-id="f1bf8-135">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-135">Displays help information for the command.</span></span> |
| <span data-ttu-id="f1bf8-136">NoCache</span><span class="sxs-lookup"><span data-stu-id="f1bf8-136">NoCache</span></span> | <span data-ttu-id="f1bf8-137">NuGet がキャッシュされているパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-137">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="f1bf8-138">参照してください[グローバル パッケージとキャッシュ フォルダーの管理](../consume-packages/managing-the-global-packages-and-cache-folders.md)です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-138">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="f1bf8-139">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f1bf8-139">NonInteractive</span></span> | <span data-ttu-id="f1bf8-140">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f1bf8-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="f1bf8-141">OutputDirectory</span></span> | <span data-ttu-id="f1bf8-142">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="f1bf8-143">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="f1bf8-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="f1bf8-144">PackageSaveMode</span></span> | <span data-ttu-id="f1bf8-145">パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="f1bf8-146">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="f1bf8-146">PreRelease</span></span> | <span data-ttu-id="f1bf8-147">インストールするプレリリースのパッケージを使用できます。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="f1bf8-148">このフラグは、使用してパッケージを復元するときに必要ありません`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="f1bf8-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="f1bf8-149">RequireConsent</span></span> | <span data-ttu-id="f1bf8-150">ダウンロードして、パッケージをインストールする前にパッケージを復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="f1bf8-151">詳細については、「[パッケージの復元](../consume-packages/package-restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="f1bf8-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="f1bf8-152">SolutionDirectory</span></span> | <span data-ttu-id="f1bf8-153">パッケージを復元するためのソリューションのルート フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="f1bf8-154">ソース</span><span class="sxs-lookup"><span data-stu-id="f1bf8-154">Source</span></span> | <span data-ttu-id="f1bf8-155">(Url) として使用するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="f1bf8-156">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="f1bf8-157">詳細度</span><span class="sxs-lookup"><span data-stu-id="f1bf8-157">Verbosity</span></span> | <span data-ttu-id="f1bf8-158">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="f1bf8-159">Version</span><span class="sxs-lookup"><span data-stu-id="f1bf8-159">Version</span></span> | <span data-ttu-id="f1bf8-160">インストールするパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="f1bf8-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="f1bf8-161">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f1bf8-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f1bf8-162">使用例</span><span class="sxs-lookup"><span data-stu-id="f1bf8-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
