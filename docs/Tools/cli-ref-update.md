---
title: "NuGet CLI コマンドの更新 |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 61fde945-6983-46a5-8636-da0fada4e641
description: "Nuget.exe 更新コマンドのリファレンス"
keywords: "nuget 参照の更新、更新プログラム パッケージ コマンド"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 654144e93a99a4a4f8d79c0db5660cfb7c6c308e
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="555a3-104">更新コマンド (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="555a3-104">update command (NuGet CLI)</span></span>

<span data-ttu-id="555a3-105">**適用されます:**消費をパッケージ化&bullet;**サポートされているバージョン:**すべて</span><span class="sxs-lookup"><span data-stu-id="555a3-105">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="555a3-106">プロジェクト内のすべてのパッケージを更新 (を使用して`packages.config`) を使用可能な最新のバージョン。</span><span class="sxs-lookup"><span data-stu-id="555a3-106">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="555a3-107">実行することをお勧め['restore'](#restore)実行する前に、`update`です。</span><span class="sxs-lookup"><span data-stu-id="555a3-107">It is recommended to run ['restore'](#restore) before running the `update`.</span></span> <span data-ttu-id="555a3-108">(個々 のパッケージを更新する[ `nuget install` ](cli-ref-install.md)ケースの NuGet が最新バージョンをインストール、バージョン番号を指定することがなくです)。</span><span class="sxs-lookup"><span data-stu-id="555a3-108">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="555a3-109">注: `update` Mono (Mac os X または Linux) で実行している CLI では機能しません。</span><span class="sxs-lookup"><span data-stu-id="555a3-109">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux).</span></span> <span data-ttu-id="555a3-110">コマンドも実行できないを使用してプロジェクト`project.json`または PackageReference 管理形式です。</span><span class="sxs-lookup"><span data-stu-id="555a3-110">The command also does not work with projects using `project.json` or PackageReference management formats.</span></span>

<span data-ttu-id="555a3-111">`update`コマンドもプロジェクト ファイル内のアセンブリ参照を更新すると、それらの参照が既に提供が存在します。</span><span class="sxs-lookup"><span data-stu-id="555a3-111">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="555a3-112">新しい参照は、更新されたパッケージに追加されたアセンブリがある場合は、*いない*を追加します。</span><span class="sxs-lookup"><span data-stu-id="555a3-112">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="555a3-113">新しいパッケージの依存関係も追加のアセンブリ参照がありません。</span><span class="sxs-lookup"><span data-stu-id="555a3-113">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="555a3-114">更新プログラムの一部としてこれらの操作を含めるには、パッケージ マネージャー UI またはパッケージ マネージャー コンソールを使用して Visual Studio でパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="555a3-114">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="555a3-115">このコマンドは、nuget.exe 自体の更新にも使用できますを使用して、 *-自己*フラグ。</span><span class="sxs-lookup"><span data-stu-id="555a3-115">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="555a3-116">使用方法</span><span class="sxs-lookup"><span data-stu-id="555a3-116">Usage</span></span>

```
nuget update <configPath> [options]
```

<span data-ttu-id="555a3-117">ここで`<configPath>`いずれかを識別、`packages.config`またはソリューション ファイルがプロジェクトの依存関係を一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="555a3-117">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="555a3-118">オプション</span><span class="sxs-lookup"><span data-stu-id="555a3-118">Options</span></span>

| <span data-ttu-id="555a3-119">オプション</span><span class="sxs-lookup"><span data-stu-id="555a3-119">Option</span></span> | <span data-ttu-id="555a3-120">説明</span><span class="sxs-lookup"><span data-stu-id="555a3-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="555a3-121">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="555a3-121">ConfigFile</span></span> | <span data-ttu-id="555a3-122">*(2.5 +)* NuGet 構成ファイルを適用します。</span><span class="sxs-lookup"><span data-stu-id="555a3-122">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="555a3-123">指定しない場合、 *%AppData%\NuGet\NuGet.Config*を使用します。</span><span class="sxs-lookup"><span data-stu-id="555a3-123">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="555a3-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="555a3-124">FileConflictAction</span></span> | <span data-ttu-id="555a3-125">*(2.5 +)*上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクションを指定します。</span><span class="sxs-lookup"><span data-stu-id="555a3-125">*(2.5+)* Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="555a3-126">値は*で上書きし、無視する場合に、none*です。</span><span class="sxs-lookup"><span data-stu-id="555a3-126">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="555a3-127">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="555a3-127">ForceEnglishOutput</span></span> | <span data-ttu-id="555a3-128">*(3.5 +)*インバリアント、英語ベースのカルチャを使用して実行する nuget.exe を強制します。</span><span class="sxs-lookup"><span data-stu-id="555a3-128">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="555a3-129">ヘルプ</span><span class="sxs-lookup"><span data-stu-id="555a3-129">Help</span></span> | <span data-ttu-id="555a3-130">ヘルプ コマンドに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="555a3-130">Displays help information for the command.</span></span> |
| <span data-ttu-id="555a3-131">ID</span><span class="sxs-lookup"><span data-stu-id="555a3-131">Id</span></span> | <span data-ttu-id="555a3-132">パッケージを更新する Id の一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="555a3-132">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="555a3-133">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="555a3-133">MSBuildPath</span></span> | <span data-ttu-id="555a3-134">*(4.0 以降)*よりも優先、コマンドで使用する MSBuild のパスを指定`-MSBuildVersion`です。</span><span class="sxs-lookup"><span data-stu-id="555a3-134">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="555a3-135">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="555a3-135">MSBuildVersion</span></span> | <span data-ttu-id="555a3-136">*(3.2 +)*このコマンドで使用する MSBuild のバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="555a3-136">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="555a3-137">サポートされている値は、4、12、14、15 です。</span><span class="sxs-lookup"><span data-stu-id="555a3-137">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="555a3-138">既定では、パスに MSBuild を取得、それ以外の場合、既定値 MSBuild の最上位にインストールされているバージョンです。</span><span class="sxs-lookup"><span data-stu-id="555a3-138">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="555a3-139">非対話型</span><span class="sxs-lookup"><span data-stu-id="555a3-139">NonInteractive</span></span> | <span data-ttu-id="555a3-140">ユーザー入力または確認を要求するプロンプトを抑制します。</span><span class="sxs-lookup"><span data-stu-id="555a3-140">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="555a3-141">プレリリース版</span><span class="sxs-lookup"><span data-stu-id="555a3-141">PreRelease</span></span> | <span data-ttu-id="555a3-142">プレリリース バージョンを更新できるようにします。</span><span class="sxs-lookup"><span data-stu-id="555a3-142">Allows updating to prerelease versions.</span></span> <span data-ttu-id="555a3-143">このフラグは既にインストールされているプレリリースのパッケージを更新するときに必要ありません。</span><span class="sxs-lookup"><span data-stu-id="555a3-143">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="555a3-144">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="555a3-144">RepositoryPath</span></span> | <span data-ttu-id="555a3-145">パッケージがインストールされているローカル フォルダーを指定します。</span><span class="sxs-lookup"><span data-stu-id="555a3-145">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="555a3-146">セーフ</span><span class="sxs-lookup"><span data-stu-id="555a3-146">Safe</span></span> | <span data-ttu-id="555a3-147">のみを更新する最高のバージョンが同じメジャーおよびマイナー バージョン内で使用できるようにインストールされているパッケージがインストールされるように指定します。</span><span class="sxs-lookup"><span data-stu-id="555a3-147">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="555a3-148">Self</span><span class="sxs-lookup"><span data-stu-id="555a3-148">Self</span></span> | <span data-ttu-id="555a3-149">*(1.4 以降)* Nuget.exe、最新のバージョンに更新; 他のすべての引数は無視されます。</span><span class="sxs-lookup"><span data-stu-id="555a3-149">*(1.4+)* Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="555a3-150">ソース</span><span class="sxs-lookup"><span data-stu-id="555a3-150">Source</span></span> | <span data-ttu-id="555a3-151">(Url) として、更新プログラムを使用するパッケージ ソースの一覧を指定します。</span><span class="sxs-lookup"><span data-stu-id="555a3-151">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="555a3-152">コマンドが構成ファイルで提供されるソースを使用する省略するを参照して[構成 NuGet 動作](../Consume-Packages/Configuring-NuGet-Behavior.md)です。</span><span class="sxs-lookup"><span data-stu-id="555a3-152">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../Consume-Packages/Configuring-NuGet-Behavior.md).</span></span> |
| <span data-ttu-id="555a3-153">詳細度</span><span class="sxs-lookup"><span data-stu-id="555a3-153">Verbosity</span></span> | <span data-ttu-id="555a3-154">出力に表示される詳細情報の量を指定します:*通常*、 *quiet*、 *(2.5 以降) の詳細*です。</span><span class="sxs-lookup"><span data-stu-id="555a3-154">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="555a3-155">Version</span><span class="sxs-lookup"><span data-stu-id="555a3-155">Version</span></span> | <span data-ttu-id="555a3-156">1 つのパッケージ ID に使用する場合は、更新するパッケージのバージョンを指定します。</span><span class="sxs-lookup"><span data-stu-id="555a3-156">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="555a3-157">参照してください[環境変数](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="555a3-157">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="555a3-158">例</span><span class="sxs-lookup"><span data-stu-id="555a3-158">Examples</span></span>

```
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
