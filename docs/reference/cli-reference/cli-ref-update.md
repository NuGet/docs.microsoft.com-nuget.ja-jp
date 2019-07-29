---
title: NuGet CLI update コマンド
description: Nuget.exe update コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327509"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="5dc1e-103">update コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5dc1e-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="5dc1e-104">**適用対象:** パッケージの&bullet;使用量が**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="5dc1e-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5dc1e-105">利用できる最も新しいバージョンに (`packages.config` を使用する) プロジェクトのすべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="5dc1e-106">を`update`実行する前に[' restore '](cli-ref-restore.md)を実行することをお勧めします。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="5dc1e-107">(個々のパッケージを更新するに[`nuget install`](cli-ref-install.md)は、バージョン番号を指定せずにを使用します。この場合、NuGet は最新バージョンをインストールします)。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="5dc1e-108">注: `update`は、Mono (Mac OSX または Linux) で実行される CLI、または PackageReference 形式を使用する場合には機能しません。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="5dc1e-109">`update`また、これらの参照が既に存在する場合は、プロジェクトファイル内のアセンブリ参照も更新されます。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="5dc1e-110">更新されたパッケージにアセンブリが追加されている場合、新しい参照は追加され*ません*。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="5dc1e-111">新しいパッケージの依存関係では、アセンブリ参照も追加されません。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="5dc1e-112">これらの操作を更新プログラムの一部として含めるには、パッケージマネージャー UI またはパッケージマネージャーコンソールを使用して、Visual Studio でパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="5dc1e-113">このコマンドは、 *-self*フラグを使用して nuget.exe 自体を更新するためにも使用できます。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="5dc1e-114">使用法</span><span class="sxs-lookup"><span data-stu-id="5dc1e-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="5dc1e-115">ここ`<configPath>`では、 `packages.config`プロジェクトの依存関係を一覧表示するまたはソリューションファイルを指定します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="5dc1e-116">オプション</span><span class="sxs-lookup"><span data-stu-id="5dc1e-116">Options</span></span>

| <span data-ttu-id="5dc1e-117">オプション</span><span class="sxs-lookup"><span data-stu-id="5dc1e-117">Option</span></span> | <span data-ttu-id="5dc1e-118">説明</span><span class="sxs-lookup"><span data-stu-id="5dc1e-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5dc1e-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5dc1e-119">ConfigFile</span></span> | <span data-ttu-id="5dc1e-120">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5dc1e-121">指定されて`%AppData%\NuGet\NuGet.Config`いない場合は`~/.nuget/NuGet/NuGet.Config` 、(Windows) または (Mac/Linux) が使用されます。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="5dc1e-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5dc1e-122">FileConflictAction</span></span> | <span data-ttu-id="5dc1e-123">プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクションを指定します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5dc1e-124">値は*overwrite、ignore、none*です。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="5dc1e-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5dc1e-125">ForceEnglishOutput</span></span> | <span data-ttu-id="5dc1e-126">*(3.5 +)* 不変の英語ベースのカルチャを使用して nuget.exe を強制的に実行します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5dc1e-127">Help</span><span class="sxs-lookup"><span data-stu-id="5dc1e-127">Help</span></span> | <span data-ttu-id="5dc1e-128">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="5dc1e-129">ID</span><span class="sxs-lookup"><span data-stu-id="5dc1e-129">Id</span></span> | <span data-ttu-id="5dc1e-130">更新するパッケージ Id の一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="5dc1e-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="5dc1e-131">MSBuildPath</span></span> | <span data-ttu-id="5dc1e-132">*(4.0 以降)* コマンドで使用する MSBuild のパスを指定します。これは`-MSBuildVersion`よりも優先されます。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="5dc1e-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="5dc1e-133">MSBuildVersion</span></span> | <span data-ttu-id="5dc1e-134">*(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="5dc1e-135">サポートされる値は、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="5dc1e-136">既定では、パス内の MSBuild が選択されます。それ以外の場合は、MSBuild のインストールされている最新バージョンが既定値になります。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="5dc1e-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5dc1e-137">NonInteractive</span></span> | <span data-ttu-id="5dc1e-138">ユーザーの入力または確認のプロンプトを表示しません。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5dc1e-139">PreRelease</span><span class="sxs-lookup"><span data-stu-id="5dc1e-139">PreRelease</span></span> | <span data-ttu-id="5dc1e-140">プレリリースバージョンに更新できます。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="5dc1e-141">既にインストールされているプレリリースパッケージを更新する場合、このフラグは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="5dc1e-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="5dc1e-142">RepositoryPath</span></span> | <span data-ttu-id="5dc1e-143">パッケージがインストールされているローカルフォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="5dc1e-144">セーフ</span><span class="sxs-lookup"><span data-stu-id="5dc1e-144">Safe</span></span> | <span data-ttu-id="5dc1e-145">インストールされているパッケージと同じメジャーバージョンとマイナーバージョン内で利用可能な最新バージョンの更新プログラムのみをインストールするように指定します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="5dc1e-146">自身</span><span class="sxs-lookup"><span data-stu-id="5dc1e-146">Self</span></span> | <span data-ttu-id="5dc1e-147">Nuget.exe を最新バージョンに更新します。その他のすべての引数は無視されます。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="5dc1e-148">Source</span><span class="sxs-lookup"><span data-stu-id="5dc1e-148">Source</span></span> | <span data-ttu-id="5dc1e-149">更新に使用するパッケージソースの一覧を Url として指定します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="5dc1e-150">省略した場合、コマンドは構成ファイルで提供されているソースを使用します。「 [Common NuGet](../../consume-packages/configuring-nuget-behavior.md)configuration」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="5dc1e-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="5dc1e-151">Verbosity</span></span> | <span data-ttu-id="5dc1e-152">出力に表示される詳細データの量を指定します:*normal*、*quiet*、*detailed*</span><span class="sxs-lookup"><span data-stu-id="5dc1e-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="5dc1e-153">Version</span><span class="sxs-lookup"><span data-stu-id="5dc1e-153">Version</span></span> | <span data-ttu-id="5dc1e-154">1つのパッケージ ID と共に使用する場合は、更新するパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="5dc1e-155">「[環境変数](cli-ref-environment-variables.md)」も参照してください。</span><span class="sxs-lookup"><span data-stu-id="5dc1e-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5dc1e-156">使用例</span><span class="sxs-lookup"><span data-stu-id="5dc1e-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
