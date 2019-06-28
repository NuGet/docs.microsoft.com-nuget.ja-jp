---
title: NuGet CLI の更新コマンド
description: Nuget.exe の update コマンドのリファレンス
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425916"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="69c5a-103">update コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="69c5a-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="69c5a-104">**適用対象:** 消費をパッケージ化&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="69c5a-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="69c5a-105">プロジェクト内のすべてのパッケージの更新 (を使用して`packages.config`) を使用可能な最新のバージョン。</span><span class="sxs-lookup"><span data-stu-id="69c5a-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="69c5a-106">実行することをお勧め['restore'](cli-ref-restore.md)実行する前に、`update`します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="69c5a-107">(個々 のパッケージを更新する[ `nuget install` ](cli-ref-install.md)大文字と小文字の NuGet が最新バージョンをインストールするバージョン番号を指定することがなく)。</span><span class="sxs-lookup"><span data-stu-id="69c5a-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="69c5a-108">注: `update` PackageReference 形式を使用する場合は、Mono (Mac OSX または Linux) で、またはを実行して、CLI では機能しません。</span><span class="sxs-lookup"><span data-stu-id="69c5a-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="69c5a-109">`update`コマンドはプロジェクト ファイル内のアセンブリ参照を更新することも、存在するものを参照して既に提供します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="69c5a-110">新しい参照は、更新されたパッケージに追加されたアセンブリがある場合は、*いない*を追加します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="69c5a-111">新しいパッケージの依存関係は、追加のアセンブリ参照も必要はありません。</span><span class="sxs-lookup"><span data-stu-id="69c5a-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="69c5a-112">更新プログラムの一部としてこれらの操作を含めるには、パッケージ マネージャー UI またはパッケージ マネージャー コンソールを使用して Visual Studio でパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="69c5a-113">このコマンドが nuget.exe 自体を更新することもできますを使用して、 *-セルフ*フラグ。</span><span class="sxs-lookup"><span data-stu-id="69c5a-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="69c5a-114">使用法</span><span class="sxs-lookup"><span data-stu-id="69c5a-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="69c5a-115">場所`<configPath>`いずれかを識別、`packages.config`またはソリューション ファイルをプロジェクトの依存関係を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="69c5a-116">オプション</span><span class="sxs-lookup"><span data-stu-id="69c5a-116">Options</span></span>

| <span data-ttu-id="69c5a-117">オプション</span><span class="sxs-lookup"><span data-stu-id="69c5a-117">Option</span></span> | <span data-ttu-id="69c5a-118">説明</span><span class="sxs-lookup"><span data-stu-id="69c5a-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="69c5a-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="69c5a-119">ConfigFile</span></span> | <span data-ttu-id="69c5a-120">適用する NuGet 構成ファイル。</span><span class="sxs-lookup"><span data-stu-id="69c5a-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="69c5a-121">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac/linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="69c5a-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="69c5a-122">FileConflictAction</span></span> | <span data-ttu-id="69c5a-123">上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められる場合に実行するアクションを指定します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="69c5a-124">値は*で上書きし、無視する場合に、none*します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="69c5a-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="69c5a-125">ForceEnglishOutput</span></span> | <span data-ttu-id="69c5a-126">*(3.5 以降)* インバリアントの英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="69c5a-127">Help</span><span class="sxs-lookup"><span data-stu-id="69c5a-127">Help</span></span> | <span data-ttu-id="69c5a-128">ヘルプのコマンドの情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="69c5a-129">ID</span><span class="sxs-lookup"><span data-stu-id="69c5a-129">Id</span></span> | <span data-ttu-id="69c5a-130">パッケージを更新する Id の一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="69c5a-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="69c5a-131">MSBuildPath</span></span> | <span data-ttu-id="69c5a-132">*(4.0 以降)* よりも優先、コマンドで使用する MSBuild のパスを示す`-MSBuildVersion`します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="69c5a-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="69c5a-133">MSBuildVersion</span></span> | <span data-ttu-id="69c5a-134">*(3.2 以降)* このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="69c5a-135">サポートされている値とは、4、12、14、15.1、15.3、15.4、15.5、15.6、15.7、15.8、15.9 です。</span><span class="sxs-lookup"><span data-stu-id="69c5a-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="69c5a-136">パスに MSBuild が取得される、既定でそれ以外の場合、既定値 MSBuild の最上位のインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="69c5a-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="69c5a-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="69c5a-137">NonInteractive</span></span> | <span data-ttu-id="69c5a-138">ユーザー入力や確認のプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="69c5a-139">PreRelease</span><span class="sxs-lookup"><span data-stu-id="69c5a-139">PreRelease</span></span> | <span data-ttu-id="69c5a-140">プレリリース バージョンに更新を許可します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="69c5a-141">既にインストールされているプレリリースのパッケージを更新するときに、このフラグは必要ありません。</span><span class="sxs-lookup"><span data-stu-id="69c5a-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="69c5a-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="69c5a-142">RepositoryPath</span></span> | <span data-ttu-id="69c5a-143">パッケージがインストールされているローカル フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="69c5a-144">Safe</span><span class="sxs-lookup"><span data-stu-id="69c5a-144">Safe</span></span> | <span data-ttu-id="69c5a-145">のみを更新する同じメジャーおよびマイナーのバージョン内で使用可能な最上位バージョンにインストールされているパッケージはインストールされているを指定します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="69c5a-146">self</span><span class="sxs-lookup"><span data-stu-id="69c5a-146">Self</span></span> | <span data-ttu-id="69c5a-147">Nuget.exe を最新のバージョンに更新します。その他のすべての引数は無視されます。</span><span class="sxs-lookup"><span data-stu-id="69c5a-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="69c5a-148">Source</span><span class="sxs-lookup"><span data-stu-id="69c5a-148">Source</span></span> | <span data-ttu-id="69c5a-149">(Url) として、更新に使用するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="69c5a-150">コマンドを省略すると、構成ファイルで提供されるソースを使用して、参照してください[一般的な NuGet 構成](../consume-packages/configuring-nuget-behavior.md)します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="69c5a-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="69c5a-151">Verbosity</span></span> | <span data-ttu-id="69c5a-152">出力に表示される詳細データの量を指定します:*通常*、 *quiet*、*詳細*</span><span class="sxs-lookup"><span data-stu-id="69c5a-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="69c5a-153">Version</span><span class="sxs-lookup"><span data-stu-id="69c5a-153">Version</span></span> | <span data-ttu-id="69c5a-154">1 つのパッケージ ID と共に使用すると、更新するパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="69c5a-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="69c5a-155">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="69c5a-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="69c5a-156">使用例</span><span class="sxs-lookup"><span data-stu-id="69c5a-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
