---
title: NuGet CLI のインストールコマンド
description: nuget.exe install コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 23856728d07d07183b5aedcd6218a56a444c410b
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623098"
---
# <a name="install-command-nuget-cli"></a><span data-ttu-id="a4b47-103">install コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="a4b47-103">install command (NuGet CLI)</span></span>

<span data-ttu-id="a4b47-104">**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="a4b47-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a4b47-105">パッケージをダウンロードしてプロジェクトにインストールします。指定したパッケージソースを使用して、既定で現在のフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-105">Downloads and installs a package into a project, defaulting to the current folder, using specified package sources.</span></span>

> [!Tip]
> <span data-ttu-id="a4b47-106">プロジェクトのコンテキストの外部でパッケージを直接ダウンロードするには、 [nuget.org](https://www.nuget.org) のパッケージのページにアクセスし、[ **ダウンロード** ] リンクを選択します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-106">To download a package directly outside the context of a project, visit the package's page on [nuget.org](https://www.nuget.org) and select the **Download** link.</span></span>

<span data-ttu-id="a4b47-107">ソースが指定されていない場合は、グローバル構成ファイル `%appdata%\NuGet\NuGet.Config` (Windows) または (Mac/Linux) に記載されているもの `~/.nuget/NuGet/NuGet.Config` が使用されます。</span><span class="sxs-lookup"><span data-stu-id="a4b47-107">If no sources are specified, those listed in the global configuration file, `%appdata%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), are used.</span></span> <span data-ttu-id="a4b47-108">詳細については、「 [一般的な NuGet の構成](../../consume-packages/configuring-nuget-behavior.md) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4b47-108">See [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md) for additional details.</span></span>

<span data-ttu-id="a4b47-109">特定のパッケージが指定されていない場合、は、 `install` プロジェクトのファイルに一覧表示されているすべてのパッケージをインストールして、の `packages.config` ように [`restore`](cli-ref-restore.md) します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-109">If no specific packages are specified, `install` installs all packages listed in the project's `packages.config` file, making it similar to [`restore`](cli-ref-restore.md).</span></span>

<span data-ttu-id="a4b47-110">`install`このコマンドは、プロジェクトファイルまたはを変更しません `packages.config` 。この方法では、 `restore` パッケージをディスクに追加するだけで、プロジェクトの依存関係は変更しないという点でも同様です。</span><span class="sxs-lookup"><span data-stu-id="a4b47-110">The `install` command does not modify a project file or `packages.config`; in this way it's similar to `restore` in that it only adds packages to disk but does not change a project's dependencies.</span></span>

<span data-ttu-id="a4b47-111">依存関係を追加するには、Visual Studio のパッケージマネージャー UI またはコンソールを使用してパッケージを追加するか、 `packages.config` またはを変更して実行し `install` `restore` ます。</span><span class="sxs-lookup"><span data-stu-id="a4b47-111">To add a dependency, either add a package through the Package Manager UI or Console in Visual Studio, or modify `packages.config` and then run either `install` or `restore`.</span></span>

## <a name="usage"></a><span data-ttu-id="a4b47-112">使用法</span><span class="sxs-lookup"><span data-stu-id="a4b47-112">Usage</span></span>

```cli
nuget install <packageID | configFilePath> [options]
```

<span data-ttu-id="a4b47-113">`<packageID>`(最新バージョンを使用して) インストールするパッケージの名前を `<configFilePath>` 指定するか、 `packages.config` インストールするパッケージの一覧を示すファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-113">where `<packageID>` names the package to install (using the latest version), or `<configFilePath>` identifies the `packages.config` file that lists the packages to install.</span></span> <span data-ttu-id="a4b47-114">オプションを使用して特定のバージョンを指定でき `-Version` ます。</span><span class="sxs-lookup"><span data-stu-id="a4b47-114">You can indicate a specific version with the `-Version` option.</span></span>

## <a name="options"></a><span data-ttu-id="a4b47-115">Options</span><span class="sxs-lookup"><span data-stu-id="a4b47-115">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="a4b47-116">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="a4b47-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a4b47-117">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="a4b47-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DependencyVersion`**

  <span data-ttu-id="a4b47-118">*(4.4 以降)* 使用する依存関係パッケージのバージョン。次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="a4b47-118">*(4.4+)* The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="a4b47-119">*最低* (既定): 最も低いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="a4b47-119">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="a4b47-120">*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</span><span class="sxs-lookup"><span data-stu-id="a4b47-120">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="a4b47-121">*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</span><span class="sxs-lookup"><span data-stu-id="a4b47-121">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="a4b47-122">*最高*: 最高バージョン</span><span class="sxs-lookup"><span data-stu-id="a4b47-122">*Highest*: the highest version</span></span></li><li><span data-ttu-id="a4b47-123">*無視*: 依存関係パッケージは使用されません</span><span class="sxs-lookup"><span data-stu-id="a4b47-123">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-DirectDownload`**

  <span data-ttu-id="a4b47-124">メタデータまたはバイナリを含むキャッシュを作成せずに、直接ダウンロードします。</span><span class="sxs-lookup"><span data-stu-id="a4b47-124">Download directly without populating any caches with metadata or binaries.</span></span>

- **`-DisableParallelProcessing`**

  <span data-ttu-id="a4b47-125">複数のパッケージの並列インストールを無効にします。</span><span class="sxs-lookup"><span data-stu-id="a4b47-125">Disables installing multiple packages in parallel.</span></span>

- **`-x|-ExcludeVersion`**

  <span data-ttu-id="a4b47-126">パッケージ名がではなく、パッケージ名だけを持つという名前のフォルダーにパッケージをインストールします。</span><span class="sxs-lookup"><span data-stu-id="a4b47-126">Installs the package to a folder named with only the package name and not the version number.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="a4b47-127">*(3.2 +)* プライマリまたは既定のソースにパッケージが見つからない場合にフォールバックとして使用するパッケージソースの一覧。</span><span class="sxs-lookup"><span data-stu-id="a4b47-127">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="a4b47-128">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-Framework`**

  <span data-ttu-id="a4b47-129">*(4.4 以降)* 依存関係の選択に使用されるターゲットフレームワーク。</span><span class="sxs-lookup"><span data-stu-id="a4b47-129">*(4.4+)* Target framework used for selecting dependencies.</span></span> <span data-ttu-id="a4b47-130">指定しない場合、既定値は ' Any ' になります。</span><span class="sxs-lookup"><span data-stu-id="a4b47-130">Defaults to 'Any' if not specified.</span></span>

- **`-?|-help`**

  <span data-ttu-id="a4b47-131">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-131">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="a4b47-132">NuGet がキャッシュされたパッケージを使用しないようにします。</span><span class="sxs-lookup"><span data-stu-id="a4b47-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="a4b47-133">「 [グローバルパッケージとキャッシュフォルダーの管理」を](../../consume-packages/managing-the-global-packages-and-cache-folders.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4b47-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="a4b47-134">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="a4b47-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="a4b47-135">パッケージがインストールされているフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="a4b47-136">フォルダーが指定されていない場合は、現在のフォルダーが使用されます。</span><span class="sxs-lookup"><span data-stu-id="a4b47-136">If no folder is specified, the current folder is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="a4b47-137">パッケージのインストール後に保存するファイルの種類を指定します。、、またはのいずれか `nuspec` `nupkg` `nuspec;nupkg` です。</span><span class="sxs-lookup"><span data-stu-id="a4b47-137">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="a4b47-138">プレリリースパッケージのインストールを許可します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-138">Allows prerelease packages to be installed.</span></span> <span data-ttu-id="a4b47-139">このフラグは、を使用してパッケージを復元する場合には必要ありません `packages.config` 。</span><span class="sxs-lookup"><span data-stu-id="a4b47-139">This flag is not required when restoring packages with `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="a4b47-140">パッケージをダウンロードしてインストールする前に、パッケージの復元が有効になっていることを確認します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-140">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="a4b47-141">詳細については、「 [パッケージの復元](../../consume-packages/package-restore.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4b47-141">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="a4b47-142">パッケージを復元するソリューションのルートフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-142">Specifies root folder of the solution for which to restore packages.</span></span>

- **`-Source`**

   <span data-ttu-id="a4b47-143">使用するパッケージソースの一覧を Url として指定します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-143">Specifies the list of package sources (as URLs) to use.</span></span> <span data-ttu-id="a4b47-144">省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4b47-144">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="a4b47-145">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="a4b47-145">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="a4b47-146">インストールするパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="a4b47-146">Specifies the version of the package to install.</span></span>

<span data-ttu-id="a4b47-147">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="a4b47-147">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a4b47-148">使用例</span><span class="sxs-lookup"><span data-stu-id="a4b47-148">Examples</span></span>

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
