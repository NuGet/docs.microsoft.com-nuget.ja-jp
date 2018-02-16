---
title: "NuGet CLI コマンドをインストールする |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe-install コマンドのリファレンス"
keywords: "nuget の参照をパッケージのコマンドをインストールします。"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e824b08486704371eebefb964f86315d82fc222
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/14/2018
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="798ec-104">コマンド (NuGet CLI) をインストールします。</span><span class="sxs-lookup"><span data-stu-id="798ec-104">install command (NuGet CLI)</span></span>

<span data-ttu-id="798ec-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="798ec-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="798ec-106">ダウンロードし、指定したパッケージ ソースを使用して、現在のフォルダーには、既定のプロジェクトにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="798ec-106">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="798ec-107">プロジェクトのコンテキスト外で直接パッケージをダウンロードするには、ページにアクセスして、パッケージの[nuget.org](https://www.nuget.org)を選択し、**ダウンロード**リンクします。</span><span class="sxs-lookup"><span data-stu-id="798ec-107">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="798ec-108">ソースが指定されていない場合、グローバル構成ファイルに一覧表示`%APPDATA%\NuGet\NuGet.Config`、使用されます。</span><span class="sxs-lookup"><span data-stu-id="798ec-108">If no sources are specified, those listed in the global configuration file, `%APPDATA%\NuGet\NuGet.Config`, are used.</span></span> <span data-ttu-id="798ec-109">参照してください[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)の詳細。</span><span class="sxs-lookup"><span data-stu-id="798ec-109">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="798ec-110">特定のパッケージが指定されていない場合`install`プロジェクトの表示されているすべてのパッケージをインストール`packages.config`ようなファイル[ `restore`](cli-ref-restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="798ec-110">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="798ec-111">`install`コマンドは、プロジェクト ファイルを変更していないまたは`packages.config`; に似ていますが、この方法で`restore`のみにパッケージをディスクに追加、プロジェクトの依存関係を変更することはできません。</span><span class="sxs-lookup"><span data-stu-id="798ec-111">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="798ec-112">依存関係を追加するか、Visual Studio で、パッケージ マネージャー UI またはコンソール経由で、プロジェクトを追加または変更`packages.config`いずれかを実行および`install`または`restore`です。</span><span class="sxs-lookup"><span data-stu-id="798ec-112">To add a dependency, either add a project through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="798ec-113">使用法</span><span class="sxs-lookup"><span data-stu-id="798ec-113">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="798ec-114">ここで`<packageID>`(最新バージョンを使用) をインストールするパッケージの名前または`<configFilePath>`を識別、`packages.config`ファイルをインストールするパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="798ec-114">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="798ec-115">特定のバージョンを指定することができます、`-Version`オプション。</span><span class="sxs-lookup"><span data-stu-id="798ec-115">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="798ec-116">オプション</span><span class="sxs-lookup"><span data-stu-id="798ec-116">Options</span></span>

| <span data-ttu-id="798ec-117">オプション</span><span class="sxs-lookup"><span data-stu-id="798ec-117">Option</span></span> | <span data-ttu-id="798ec-118">説明</span><span class="sxs-lookup"><span data-stu-id="798ec-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="798ec-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="798ec-119">ConfigFile</span></span> | <span data-ttu-id="798ec-120">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="798ec-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="798ec-121">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="798ec-121">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="798ec-122">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="798ec-122">DependencyVersion</span></span> | <span data-ttu-id="798ec-123">*(4.4 +)*既定の依存関係の解決の動作をオーバーライドする特定のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="798ec-123">*(4.4+)* Specifies a specific version, overriding the default dependency resolution behavior.</span></span> |
| <span data-ttu-id="798ec-124">DisableParallelProcessing</span><span class="sxs-lookup"><span data-stu-id="798ec-124">DisableParallelProcessing</span></span> | <span data-ttu-id="798ec-125">複数のパッケージを並列でインストールを無効にします。</span><span class="sxs-lookup"><span data-stu-id="798ec-125">Disables installing multiple packages in parallel.</span></span> |
| <span data-ttu-id="798ec-126">ExcludeVersion</span><span class="sxs-lookup"><span data-stu-id="798ec-126">ExcludeVersion</span></span> | <span data-ttu-id="798ec-127">パッケージ名のみとバージョン番号ではないという名前のフォルダーにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="798ec-127">Installs the package to a folder named with only the package name and not the version number.</span></span> |
| <span data-ttu-id="798ec-128">FallbackSource</span><span class="sxs-lookup"><span data-stu-id="798ec-128">FallbackSource</span></span> | <span data-ttu-id="798ec-129">*(3.2 +)*プライマリで、パッケージが見つからない場合に、フォールバックとして使用するパッケージ ソースの一覧または既定のソース。</span><span class="sxs-lookup"><span data-stu-id="798ec-129">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> |
| <span data-ttu-id="798ec-130">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="798ec-130">ForceEnglishOutput</span></span> | <span data-ttu-id="798ec-131">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="798ec-131">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="798ec-132">フレームワーク</span><span class="sxs-lookup"><span data-stu-id="798ec-132">Framework</span></span> | <span data-ttu-id="798ec-133">*(4.4 +)*ターゲット フレームワークの依存関係を選択するために使用します。</span><span class="sxs-lookup"><span data-stu-id="798ec-133">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="798ec-134">'Any' に指定されていない場合の既定値です。</span><span class="sxs-lookup"><span data-stu-id="798ec-134">Defaults to 'Any' if not specified.</span></span> |
| <span data-ttu-id="798ec-135">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="798ec-135">Help</span></span> | <span data-ttu-id="798ec-136">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="798ec-136">Displays help information for the command.</span></span> |
| <span data-ttu-id="798ec-137">NoCache</span><span class="sxs-lookup"><span data-stu-id="798ec-137">NoCache</span></span> | <span data-ttu-id="798ec-138">NuGet がローカル コンピューターのキャッシュからパッケージを使用するを防ぎます。</span><span class="sxs-lookup"><span data-stu-id="798ec-138">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="798ec-139">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="798ec-139">NonInteractive</span></span> | <span data-ttu-id="798ec-140">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="798ec-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="798ec-141">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="798ec-141">OutputDirectory</span></span> | <span data-ttu-id="798ec-142">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="798ec-142">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="798ec-143">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="798ec-143">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="798ec-144">PackageSaveMode</span><span class="sxs-lookup"><span data-stu-id="798ec-144">PackageSaveMode</span></span> | <span data-ttu-id="798ec-145">パッケージのインストール後に保存するファイルの種類を指定します: のいずれかの`nuspec`、 `nupkg`、または`nuspec;nupkg`です。</span><span class="sxs-lookup"><span data-stu-id="798ec-145">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span> |
| <span data-ttu-id="798ec-146">PreRelease</span><span class="sxs-lookup"><span data-stu-id="798ec-146">PreRelease</span></span> | <span data-ttu-id="798ec-147">インストールするプレリリースのパッケージを使用できます。</span><span class="sxs-lookup"><span data-stu-id="798ec-147">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="798ec-148">このフラグは、使用してパッケージを復元するときに必要ありません`packages.config`です。</span><span class="sxs-lookup"><span data-stu-id="798ec-148">This flag is not required when restoring packages with `packages.config`.</span></span> |
| <span data-ttu-id="798ec-149">RequireConsent</span><span class="sxs-lookup"><span data-stu-id="798ec-149">RequireConsent</span></span> | <span data-ttu-id="798ec-150">ダウンロードして、パッケージをインストールする前にパッケージを復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="798ec-150">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="798ec-151">詳細については、「[パッケージの復元](../consume-packages/package-restore.md)です。</span><span class="sxs-lookup"><span data-stu-id="798ec-151">For details, see [Package Restore](../consume-packages/package-restore.md).</span></span> |
| <span data-ttu-id="798ec-152">SolutionDirectory</span><span class="sxs-lookup"><span data-stu-id="798ec-152">SolutionDirectory</span></span> | <span data-ttu-id="798ec-153">パッケージを復元するためのソリューションのルート フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="798ec-153">Specifies root folder of the solution for which to restore packages.</span></span> |
| <span data-ttu-id="798ec-154">ソース</span><span class="sxs-lookup"><span data-stu-id="798ec-154">Source</span></span> | <span data-ttu-id="798ec-155">(Url) として使用するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="798ec-155">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="798ec-156">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="798ec-156">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="798ec-157">詳細度</span><span class="sxs-lookup"><span data-stu-id="798ec-157">Verbosity</span></span> | <span data-ttu-id="798ec-158">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="798ec-158">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="798ec-159">Version</span><span class="sxs-lookup"><span data-stu-id="798ec-159">Version</span></span> | <span data-ttu-id="798ec-160">インストールするパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="798ec-160">Specifies the version of the package to install.</span></span> |

<span data-ttu-id="798ec-161">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="798ec-161">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="798ec-162">使用例</span><span class="sxs-lookup"><span data-stu-id="798ec-162">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
