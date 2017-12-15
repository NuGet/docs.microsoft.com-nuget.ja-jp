---
title: "NuGet CLI コマンドをインストールする |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Nuget.exe-install コマンドのリファレンス"
keywords: "nuget の参照をパッケージのコマンドをインストールします。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="77bdf-104">コマンド (NuGet CLI) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="77bdf-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="77bdf-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="77bdf-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="77bdf-106">ダウンロードし、指定したパッケージ ソースを使用して、現在のフォルダーには、既定のプロジェクトにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="77bdf-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="77bdf-107">プロジェクトのコンテキスト外で直接パッケージをダウンロードするには、ページにアクセスして、パッケージの[nuget.org](https://www.nuget.org)を選択し、**ダウンロード**リンクします。</span><span class="sxs-lookup"><span data-stu-id="77bdf-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span> 

<span data-ttu-id="77bdf-108">ソースが指定されていない場合、グローバル構成ファイルに一覧表示`%APPDATA%\NuGet\NuGet.Config`、使用されます。</span><span class="sxs-lookup"><span data-stu-id="77bdf-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="77bdf-109">参照してください[NuGet の動作を構成する](../consume-packages/configuring-nuget-behavior.md)さらに詳細です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-109">See [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="77bdf-110">特定のパッケージが指定されていない場合`install`プロジェクトの表示されているすべてのパッケージをインストール`packages.config`ようなファイル[ `restore`](#restore)です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](#restore).</span></span> <span data-ttu-id="77bdf-111">(、`install`コマンドでは機能しません`project.json`)。</span><span class="sxs-lookup"><span data-stu-id="77bdf-111">(The `install` command does not work with `project.json`.)</span></span>

<span data-ttu-id="77bdf-112">`install`コマンドは、プロジェクト ファイルを変更していないまたは`packages.config`; に似ていますが、この方法で`restore`のみにパッケージをディスクに追加、プロジェクトの依存関係を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="77bdf-112">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="77bdf-113">依存関係を追加するか、Visual Studio で、パッケージ マネージャー UI またはコンソール経由で、プロジェクトを追加または変更`packages.config`いずれかを実行および`install`または`restore`です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-113">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span> <span data-ttu-id="77bdf-114">使用してプロジェクトの`project.json`、そのファイルを変更して実行し、`restore`です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-114">For projects using `project.json`, you can modify that file and then run `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="77bdf-115">使用方法</span><span class="sxs-lookup"><span data-stu-id="77bdf-115">Usage</span></span>

```
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="77bdf-116">ここで`<packageID>`(最新バージョンを使用) をインストールするパッケージの名前または`<configFilePath>`を識別、`packages.config`ファイルをインストールするパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-116">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="77bdf-117">特定のバージョンを指定することができます、`-Version`オプション。</span><span class="sxs-lookup"><span data-stu-id="77bdf-117">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="77bdf-118">オプション</span><span class="sxs-lookup"><span data-stu-id="77bdf-118">Options</span></span>

| <span data-ttu-id="77bdf-119">オプション</span><span class="sxs-lookup"><span data-stu-id="77bdf-119">Option</span></span> | <span data-ttu-id="77bdf-120">説明</span><span class="sxs-lookup"><span data-stu-id="77bdf-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="77bdf-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="77bdf-121">ConfigFile</span></span> | <span data-ttu-id="77bdf-122">*(2.5 +)* NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="77bdf-123">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="77bdf-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="77bdf-124">DisableParallelProcessing</span></span> | <span data-ttu-id="77bdf-125">複数のパッケージを並列でインストールを無効にします。</span><span class="sxs-lookup"><span data-stu-id="77bdf-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="77bdf-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="77bdf-126">ExcludeVersion</span></span> | <span data-ttu-id="77bdf-127">パッケージ名のみとバージョン番号ではないという名前のフォルダーにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="77bdf-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="77bdf-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="77bdf-128">FallbackSource</span></span> | <span data-ttu-id="77bdf-129">*(3.2 +)*プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。</span><span class="sxs-lookup"><span data-stu-id="77bdf-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="77bdf-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="77bdf-130">ForceEnglishOutput</span></span> | <span data-ttu-id="77bdf-131">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="77bdf-132">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="77bdf-132">Framework</span></span> | <span data-ttu-id="77bdf-133">*(4.4 +)*ターゲット フレームワークの依存関係を選択するために使用します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="77bdf-134">'Any' に指定されていない場合の既定値です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="77bdf-135">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="77bdf-135">Help</span></span> | <span data-ttu-id="77bdf-136">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="77bdf-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="77bdf-137">NoCache</span></span> | <span data-ttu-id="77bdf-138">NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="77bdf-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="77bdf-139">非対話型</span><span class="sxs-lookup"><span data-stu-id="77bdf-139">NonInteractive</span></span> | <span data-ttu-id="77bdf-140">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="77bdf-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="77bdf-141">OutputDirectory</span></span> | <span data-ttu-id="77bdf-142">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="77bdf-143">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="77bdf-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="77bdf-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="77bdf-144">PackageSaveMode</span></span> | <span data-ttu-id="77bdf-145">パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="77bdf-146">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="77bdf-146">PreRelease</span></span> | <span data-ttu-id="77bdf-147">インストールするプレリリースのパッケージを使用できます。</span><span class="sxs-lookup"><span data-stu-id="77bdf-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="77bdf-148">このフラグは、使用してパッケージを復元するときに必要ありません`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="77bdf-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="77bdf-149">RequireConsent</span></span> | <span data-ttu-id="77bdf-150">ダウンロードして、パッケージをインストールする前にパッケージを復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="77bdf-151">詳細については、「[パッケージの復元](../consume-packages/package-restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="77bdf-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="77bdf-152">SolutionDirectory</span></span> | <span data-ttu-id="77bdf-153">パッケージを復元するためのソリューションのルート フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="77bdf-154">ソース</span><span class="sxs-lookup"><span data-stu-id="77bdf-154">Source</span></span> | <span data-ttu-id="77bdf-155">(Url) として使用するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="77bdf-156">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../Consume-Packages/Configuring-NuGet-Behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="77bdf-157">詳細度</span><span class="sxs-lookup"><span data-stu-id="77bdf-157">Verbosity</span></span> | <span data-ttu-id="77bdf-158">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="77bdf-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="77bdf-159">Version</span><span class="sxs-lookup"><span data-stu-id="77bdf-159">Version</span></span> | <span data-ttu-id="77bdf-160">インストールするパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="77bdf-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="77bdf-161">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="77bdf-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="77bdf-162">例</span><span class="sxs-lookup"><span data-stu-id="77bdf-162">Examples</span></span>

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
