---
title: "NuGet CLI コマンドの更新 |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Nuget.exe 更新コマンドのリファレンス"
keywords: "nuget 参照の更新、更新プログラム パッケージ コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 891ce1f27102b16125c93e7a66ebd29f6fc626db
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="894b1-104">更新コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="894b1-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="894b1-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="894b1-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="894b1-106">プロジェクト内のすべてのパッケージを更新 (を使用して`packages.config`) を使用可能な最新のバージョン。</span><span class="sxs-lookup"><span data-stu-id="894b1-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="894b1-107">実行することをお勧め['restore'](cli-ref-restore.md)実行する前に、`update`です。</span><span class="sxs-lookup"><span data-stu-id="894b1-107">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="894b1-108">(個々 のパッケージを更新する[ `nuget install` ](cli-ref-install.md)ケースの NuGet が最新バージョンをインストール、バージョン番号を指定することがなくです)。</span><span class="sxs-lookup"><span data-stu-id="894b1-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="894b1-109">注: `update` PackageReference 形式を使用する場合は、Mono (Mac os X または Linux) で、またはを実行している CLI では機能しません。</span><span class="sxs-lookup"><span data-stu-id="894b1-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="894b1-110">`update`コマンドもプロジェクト ファイル内のアセンブリ参照を更新すると、それらの参照が既に提供が存在します。</span><span class="sxs-lookup"><span data-stu-id="894b1-110">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="894b1-111">新しい参照は、更新されたパッケージに追加されたアセンブリがある場合は、*いない*を追加します。</span><span class="sxs-lookup"><span data-stu-id="894b1-111">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="894b1-112">新しいパッケージの依存関係も追加のアセンブリ参照がありません。</span><span class="sxs-lookup"><span data-stu-id="894b1-112">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="894b1-113">更新プログラムの一部としてこれらの操作を含めるには、パッケージ マネージャー UI またはパッケージ マネージャー コンソールを使用して Visual Studio でパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="894b1-113">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="894b1-114">このコマンドは、nuget.exe 自体の更新にも使用できますを使用して、 *-自己*フラグ。</span><span class="sxs-lookup"><span data-stu-id="894b1-114">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="894b1-115">使用法</span><span class="sxs-lookup"><span data-stu-id="894b1-115">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="894b1-116">ここで`<configPath>`いずれかを識別、`packages.config`またはソリューション ファイルがプロジェクトの依存関係を一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="894b1-116">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="894b1-117">オプション</span><span class="sxs-lookup"><span data-stu-id="894b1-117">Options</span></span>

| <span data-ttu-id="894b1-118">オプション</span><span class="sxs-lookup"><span data-stu-id="894b1-118">Option</span></span> | <span data-ttu-id="894b1-119">説明</span><span class="sxs-lookup"><span data-stu-id="894b1-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="894b1-120">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="894b1-120">ConfigFile</span></span> | <span data-ttu-id="894b1-121">NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="894b1-121">The NuGet configuration file to apply.</span></span> <span data-ttu-id="894b1-122">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="894b1-122">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="894b1-123">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="894b1-123">FileConflictAction</span></span> | <span data-ttu-id="894b1-124">上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクションを指定します。</span><span class="sxs-lookup"><span data-stu-id="894b1-124">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="894b1-125">値は*で上書きし、無視する場合に、none*です。</span><span class="sxs-lookup"><span data-stu-id="894b1-125">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="894b1-126">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="894b1-126">ForceEnglishOutput</span></span> | <span data-ttu-id="894b1-127">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="894b1-127">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="894b1-128">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="894b1-128">Help</span></span> | <span data-ttu-id="894b1-129">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="894b1-129">Displays help information for the command.</span></span> |
| <span data-ttu-id="894b1-130">ID</span><span class="sxs-lookup"><span data-stu-id="894b1-130">Id</span></span> | <span data-ttu-id="894b1-131">パッケージを更新する Id の一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="894b1-131">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="894b1-132">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="894b1-132">MSBuildPath</span></span> | <span data-ttu-id="894b1-133">*(4.0 以降)*よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。</span><span class="sxs-lookup"><span data-stu-id="894b1-133">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="894b1-134">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="894b1-134">MSBuildVersion</span></span> | <span data-ttu-id="894b1-135">*(3.2 +)*このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="894b1-135">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="894b1-136">サポートされている値は、4、12、14、15 です。</span><span class="sxs-lookup"><span data-stu-id="894b1-136">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="894b1-137">既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="894b1-137">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="894b1-138">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="894b1-138">NonInteractive</span></span> | <span data-ttu-id="894b1-139">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="894b1-139">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="894b1-140">PreRelease</span><span class="sxs-lookup"><span data-stu-id="894b1-140">PreRelease</span></span> | <span data-ttu-id="894b1-141">プレリリース バージョンを更新できるようにします。</span><span class="sxs-lookup"><span data-stu-id="894b1-141">Allows updating to prerelease versions.</span></span> <span data-ttu-id="894b1-142">このフラグは既にインストールされているプレリリースのパッケージを更新するときに必要ありません。</span><span class="sxs-lookup"><span data-stu-id="894b1-142">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="894b1-143">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="894b1-143">RepositoryPath</span></span> | <span data-ttu-id="894b1-144">パッケージがインストールされているローカル フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="894b1-144">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="894b1-145">セーフ</span><span class="sxs-lookup"><span data-stu-id="894b1-145">Safe</span></span> | <span data-ttu-id="894b1-146">のみを更新する最高のバージョンが同じメジャーおよびマイナー バージョン内で使用できるようにインストールされているパッケージがインストールされるように指定します。</span><span class="sxs-lookup"><span data-stu-id="894b1-146">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="894b1-147">Self</span><span class="sxs-lookup"><span data-stu-id="894b1-147">Self</span></span> | <span data-ttu-id="894b1-148">Nuget.exe、最新のバージョンに更新です。その他のすべての引数は無視されます。</span><span class="sxs-lookup"><span data-stu-id="894b1-148">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="894b1-149">ソース</span><span class="sxs-lookup"><span data-stu-id="894b1-149">Source</span></span> | <span data-ttu-id="894b1-150">(Url) として、更新プログラムを使用するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="894b1-150">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="894b1-151">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../Consume-Packages/Configuring-NuGet-Behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="894b1-151">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="894b1-152">詳細度</span><span class="sxs-lookup"><span data-stu-id="894b1-152">Verbosity</span></span> | <span data-ttu-id="894b1-153">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、*詳細*です。</span><span class="sxs-lookup"><span data-stu-id="894b1-153">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="894b1-154">Version</span><span class="sxs-lookup"><span data-stu-id="894b1-154">Version</span></span> | <span data-ttu-id="894b1-155">1 つのパッケージ ID に使用する場合は、更新するパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="894b1-155">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="894b1-156">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="894b1-156">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="894b1-157">使用例</span><span class="sxs-lookup"><span data-stu-id="894b1-157">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
