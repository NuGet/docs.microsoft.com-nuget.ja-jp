---
title: NuGet CLI 更新コマンド
description: Nuget.exe 更新コマンドのリファレンス
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 39e269b10a0cf144d5971d2af9f82a606e0b6904
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817708"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="34c21-103">update コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="34c21-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="34c21-104">**適用されます:** 消費をパッケージ化&bullet;**サポートされているバージョン:** すべて</span><span class="sxs-lookup"><span data-stu-id="34c21-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="34c21-105">プロジェクト内のすべてのパッケージを更新 (を使用して`packages.config`) を使用可能な最新のバージョン。</span><span class="sxs-lookup"><span data-stu-id="34c21-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="34c21-106">実行することをお勧め['restore'](cli-ref-restore.md)実行する前に、`update`です。</span><span class="sxs-lookup"><span data-stu-id="34c21-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="34c21-107">(個々 のパッケージを更新する[ `nuget install` ](cli-ref-install.md)ケースの NuGet が最新バージョンをインストール、バージョン番号を指定することがなくです)。</span><span class="sxs-lookup"><span data-stu-id="34c21-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="34c21-108">注: `update` PackageReference 形式を使用する場合は、Mono (Mac os X または Linux) で、またはを実行している CLI では機能しません。</span><span class="sxs-lookup"><span data-stu-id="34c21-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="34c21-109">`update`コマンドもプロジェクト ファイル内のアセンブリ参照を更新すると、それらの参照が既に提供が存在します。</span><span class="sxs-lookup"><span data-stu-id="34c21-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="34c21-110">新しい参照は、更新されたパッケージに追加されたアセンブリがある場合は、*いない*を追加します。</span><span class="sxs-lookup"><span data-stu-id="34c21-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="34c21-111">新しいパッケージの依存関係も追加のアセンブリ参照がありません。</span><span class="sxs-lookup"><span data-stu-id="34c21-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="34c21-112">更新プログラムの一部としてこれらの操作を含めるには、パッケージ マネージャー UI またはパッケージ マネージャー コンソールを使用して Visual Studio でパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="34c21-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="34c21-113">このコマンドは、nuget.exe 自体の更新にも使用できますを使用して、 *-自己*フラグ。</span><span class="sxs-lookup"><span data-stu-id="34c21-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="34c21-114">使用法</span><span class="sxs-lookup"><span data-stu-id="34c21-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="34c21-115">ここで`<configPath>`いずれかを識別、`packages.config`またはソリューション ファイルがプロジェクトの依存関係を一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="34c21-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="34c21-116">オプション</span><span class="sxs-lookup"><span data-stu-id="34c21-116">Options</span></span>

| <span data-ttu-id="34c21-117">オプション</span><span class="sxs-lookup"><span data-stu-id="34c21-117">Option</span></span> | <span data-ttu-id="34c21-118">説明</span><span class="sxs-lookup"><span data-stu-id="34c21-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="34c21-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="34c21-119">ConfigFile</span></span> | <span data-ttu-id="34c21-120">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="34c21-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="34c21-121">指定しない場合、 `%AppData%\NuGet\NuGet.Config` (Windows) または`~/.nuget/NuGet/NuGet.Config`(Mac または Linux) を使用します。</span><span class="sxs-lookup"><span data-stu-id="34c21-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="34c21-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="34c21-122">FileConflictAction</span></span> | <span data-ttu-id="34c21-123">上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクションを指定します。</span><span class="sxs-lookup"><span data-stu-id="34c21-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="34c21-124">値は*で上書きし、無視する場合に、none*です。</span><span class="sxs-lookup"><span data-stu-id="34c21-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="34c21-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="34c21-125">ForceEnglishOutput</span></span> | <span data-ttu-id="34c21-126">*(3.5 +)* インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="34c21-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="34c21-127">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="34c21-127">Help</span></span> | <span data-ttu-id="34c21-128">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="34c21-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="34c21-129">ID</span><span class="sxs-lookup"><span data-stu-id="34c21-129">Id</span></span> | <span data-ttu-id="34c21-130">パッケージを更新する Id の一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="34c21-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="34c21-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="34c21-131">MSBuildPath</span></span> | <span data-ttu-id="34c21-132">*(4.0 以降)* よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。</span><span class="sxs-lookup"><span data-stu-id="34c21-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="34c21-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="34c21-133">MSBuildVersion</span></span> | <span data-ttu-id="34c21-134">*(3.2 +)* このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="34c21-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="34c21-135">サポートされている値は、4、12、14、15 です。</span><span class="sxs-lookup"><span data-stu-id="34c21-135">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="34c21-136">既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="34c21-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="34c21-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="34c21-137">NonInteractive</span></span> | <span data-ttu-id="34c21-138">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="34c21-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="34c21-139">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="34c21-139">PreRelease</span></span> | <span data-ttu-id="34c21-140">プレリリース バージョンを更新できるようにします。</span><span class="sxs-lookup"><span data-stu-id="34c21-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="34c21-141">このフラグは既にインストールされているプレリリースのパッケージを更新するときに必要ありません。</span><span class="sxs-lookup"><span data-stu-id="34c21-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="34c21-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="34c21-142">RepositoryPath</span></span> | <span data-ttu-id="34c21-143">パッケージがインストールされているローカル フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="34c21-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="34c21-144">セーフ</span><span class="sxs-lookup"><span data-stu-id="34c21-144">Safe</span></span> | <span data-ttu-id="34c21-145">のみを更新する最高のバージョンが同じメジャーおよびマイナー バージョン内で使用できるようにインストールされているパッケージがインストールされるように指定します。</span><span class="sxs-lookup"><span data-stu-id="34c21-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="34c21-146">Self</span><span class="sxs-lookup"><span data-stu-id="34c21-146">Self</span></span> | <span data-ttu-id="34c21-147">Nuget.exe、最新のバージョンに更新です。その他のすべての引数は無視されます。</span><span class="sxs-lookup"><span data-stu-id="34c21-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="34c21-148">ソース</span><span class="sxs-lookup"><span data-stu-id="34c21-148">Source</span></span> | <span data-ttu-id="34c21-149">(Url) として、更新プログラムを使用するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="34c21-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="34c21-150">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../consume-packages/configuring-nuget-behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="34c21-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="34c21-151">詳細度</span><span class="sxs-lookup"><span data-stu-id="34c21-151">Verbosity</span></span> | <span data-ttu-id="34c21-152">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="34c21-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="34c21-153">Version</span><span class="sxs-lookup"><span data-stu-id="34c21-153">Version</span></span> | <span data-ttu-id="34c21-154">1 つのパッケージ ID に使用する場合は、更新するパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="34c21-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="34c21-155">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="34c21-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="34c21-156">使用例</span><span class="sxs-lookup"><span data-stu-id="34c21-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
