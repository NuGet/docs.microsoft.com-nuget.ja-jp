---
title: NuGet CLI の更新コマンド
description: nuget.exe update コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 106c4027f03d8e8c1d19545b3ca9b6cd5263830e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236790"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="35d49-103">update コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="35d49-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="35d49-104">**適用対象:** パッケージの使用量が &bullet; **サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="35d49-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="35d49-105">利用できる最も新しいバージョンに (`packages.config` を使用する) プロジェクトのすべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="35d49-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="35d49-106">を実行する前に [' restore '](cli-ref-restore.md) を実行することをお勧め `update` します。</span><span class="sxs-lookup"><span data-stu-id="35d49-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="35d49-107">(個々のパッケージを更新するには、 [`nuget install`](cli-ref-install.md) バージョン番号を指定せずにを使用します。この場合、NuGet は最新バージョンをインストールします)。</span><span class="sxs-lookup"><span data-stu-id="35d49-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="35d49-108">注: `update` は、Mono (MAC OSX または Linux) で実行される CLI、または PackageReference 形式を使用する場合には機能しません。</span><span class="sxs-lookup"><span data-stu-id="35d49-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="35d49-109">`update`また、これらの参照が既に存在する場合は、プロジェクトファイル内のアセンブリ参照も更新されます。</span><span class="sxs-lookup"><span data-stu-id="35d49-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="35d49-110">更新されたパッケージにアセンブリが追加されている場合、新しい参照は追加され *ません* 。</span><span class="sxs-lookup"><span data-stu-id="35d49-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="35d49-111">新しいパッケージの依存関係では、アセンブリ参照も追加されません。</span><span class="sxs-lookup"><span data-stu-id="35d49-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="35d49-112">これらの操作を更新プログラムの一部として含めるには、パッケージマネージャー UI またはパッケージマネージャーコンソールを使用して、Visual Studio でパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="35d49-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="35d49-113">このコマンドは、 *-self* フラグを使用して nuget.exe 自体を更新するためにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="35d49-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="35d49-114">使用</span><span class="sxs-lookup"><span data-stu-id="35d49-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="35d49-115">ここ `<configPath>` `packages.config` では、プロジェクトの依存関係を一覧表示するまたはソリューションファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="35d49-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="35d49-116">オプション</span><span class="sxs-lookup"><span data-stu-id="35d49-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="35d49-117">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="35d49-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="35d49-118">指定されていない場合は、 `%AppData%\NuGet\NuGet.Config` (Windows)、また `~/.nuget/NuGet/NuGet.Config` はまたは `~/.config/NuGet/NuGet.Config` (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="35d49-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="35d49-119">使用する依存関係パッケージのバージョンを指定します。次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="35d49-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="35d49-120">*最低* (既定): 最も低いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="35d49-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="35d49-121">*HighestPatch* : 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</span><span class="sxs-lookup"><span data-stu-id="35d49-121">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="35d49-122">*HighestMinor* : 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</span><span class="sxs-lookup"><span data-stu-id="35d49-122">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="35d49-123">*最高* : 最高バージョン</span><span class="sxs-lookup"><span data-stu-id="35d49-123">*Highest* : the highest version</span></span></li><li><span data-ttu-id="35d49-124">*無視* : 依存関係パッケージは使用されません</span><span class="sxs-lookup"><span data-stu-id="35d49-124">*Ignore* : No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="35d49-125">ターゲットプロジェクトにパッケージのファイルが既に存在する場合の既定のアクションを指定します。</span><span class="sxs-lookup"><span data-stu-id="35d49-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="35d49-126">常にファイルを上書きする場合はに設定し `Overwrite` ます。</span><span class="sxs-lookup"><span data-stu-id="35d49-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="35d49-127">ファイルをスキップするには、に設定し `Ignore` ます。</span><span class="sxs-lookup"><span data-stu-id="35d49-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="35d49-128">`PromptUser`既定では、またはが指定されていない限り、 `OverwriteAll` 他のすべての `IgnoreAll` ファイルに適用されます。</span><span class="sxs-lookup"><span data-stu-id="35d49-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="35d49-129">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="35d49-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="35d49-130">コマンドのヘルプ情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="35d49-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="35d49-131">更新するパッケージ Id の一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="35d49-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="35d49-132">*(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これはよりも優先さ `-MSBuildVersion` れます。</span><span class="sxs-lookup"><span data-stu-id="35d49-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="35d49-133">*(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="35d49-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="35d49-134">サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。</span><span class="sxs-lookup"><span data-stu-id="35d49-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="35d49-135">既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。</span><span class="sxs-lookup"><span data-stu-id="35d49-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="35d49-136">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="35d49-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="35d49-137">プレリリースバージョンに更新できます。</span><span class="sxs-lookup"><span data-stu-id="35d49-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="35d49-138">既にインストールされているプレリリースパッケージを更新する場合、このフラグは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="35d49-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="35d49-139">パッケージがインストールされているローカルフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="35d49-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="35d49-140">インストールされているパッケージと同じメジャーバージョンとマイナーバージョン内で利用可能な最新バージョンの更新プログラムのみをインストールするように指定します。</span><span class="sxs-lookup"><span data-stu-id="35d49-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="35d49-141">最新バージョンに nuget.exe を更新します。その他のすべての引数は無視されます。</span><span class="sxs-lookup"><span data-stu-id="35d49-141">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="35d49-142">更新に使用するパッケージソースの一覧を Url として指定します。</span><span class="sxs-lookup"><span data-stu-id="35d49-142">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="35d49-143">省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="35d49-143">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="35d49-144">出力に表示する詳細の量 `normal` (既定値)、 `quiet` 、またはを指定し `detailed` ます。</span><span class="sxs-lookup"><span data-stu-id="35d49-144">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="35d49-145">1つのパッケージ ID と共に使用する場合は、更新するパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="35d49-145">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="35d49-146">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="35d49-146">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="35d49-147">使用例</span><span class="sxs-lookup"><span data-stu-id="35d49-147">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
