---
title: "NuGet の更新プログラム パッケージの PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで更新プログラム パッケージの PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、更新プログラム パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 768fdb4d7c785b4f3ed9e70958390676ea965794
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="b9e79-104">更新プログラム パッケージ (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="b9e79-104">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b9e79-105">*内でのみ使用可能な[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="b9e79-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b9e79-106">パッケージとその依存関係またはプロジェクトでは、すべてのパッケージを新しいバージョンに更新されます。</span><span class="sxs-lookup"><span data-stu-id="b9e79-106">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="b9e79-107">構文</span><span class="sxs-lookup"><span data-stu-id="b9e79-107">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="b9e79-108">NuGet 2.8 + で`Update-Package`プロジェクトで既存のパッケージをダウン グレードすることできます。</span><span class="sxs-lookup"><span data-stu-id="b9e79-108">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="b9e79-109">たとえば、Microsoft.AspNet.MVC 5.1.0-rc1 がインストールされている場合は、次のコマンドはへのダウン グレードに 5.0.0 以降。</span><span class="sxs-lookup"><span data-stu-id="b9e79-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="b9e79-110">NuGet 2.7 およびそれ以前では、新しいバージョンが既にインストールされていることを示すエラーを説明します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>

## <a name="parameters"></a><span data-ttu-id="b9e79-111">パラメーター</span><span class="sxs-lookup"><span data-stu-id="b9e79-111">Parameters</span></span>

|  <span data-ttu-id="b9e79-112">パラメーター</span><span class="sxs-lookup"><span data-stu-id="b9e79-112">Parameter</span></span> | <span data-ttu-id="b9e79-113">説明</span><span class="sxs-lookup"><span data-stu-id="b9e79-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b9e79-114">ID</span><span class="sxs-lookup"><span data-stu-id="b9e79-114">Id</span></span> | <span data-ttu-id="b9e79-115">更新するパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="b9e79-115">The identifier of the package to update.</span></span> <span data-ttu-id="b9e79-116">省略した場合は、すべてのパッケージを更新します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-116">If omitted, updates all packages.</span></span> <span data-ttu-id="b9e79-117">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="b9e79-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="b9e79-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="b9e79-118">IgnoreDependencies</span></span> | <span data-ttu-id="b9e79-119">パッケージの依存関係の更新をスキップします。</span><span class="sxs-lookup"><span data-stu-id="b9e79-119">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="b9e79-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="b9e79-120">ProjectName</span></span> | <span data-ttu-id="b9e79-121">プロジェクトを更新するパッケージを含む、すべてのプロジェクトには、既定の名前。</span><span class="sxs-lookup"><span data-stu-id="b9e79-121">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="b9e79-122">Version</span><span class="sxs-lookup"><span data-stu-id="b9e79-122">Version</span></span> | <span data-ttu-id="b9e79-123">アップグレードは、既定で最新バージョンを使用するバージョンです。</span><span class="sxs-lookup"><span data-stu-id="b9e79-123">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="b9e79-124">NuGet 3.0 以降で、バージョンの値はのいずれかのことがあります*Lowest、最高、HighestMinor*、または*HighestPatch* (Safe に相当)。</span><span class="sxs-lookup"><span data-stu-id="b9e79-124">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="b9e79-125">セーフ</span><span class="sxs-lookup"><span data-stu-id="b9e79-125">Safe</span></span> | <span data-ttu-id="b9e79-126">現在インストールされているパッケージと同じメジャーおよびマイナー バージョンの唯一のバージョンにアップグレードするように制約します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-126">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="b9e79-127">ソース</span><span class="sxs-lookup"><span data-stu-id="b9e79-127">Source</span></span> | <span data-ttu-id="b9e79-128">検索するパッケージ ソースの URL またはフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="b9e79-128">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="b9e79-129">ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="b9e79-129">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="b9e79-130">省略した場合、`Uninstall-Package`現在選択されているパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-130">If omitted, `Uninstall-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="b9e79-131">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="b9e79-131">IncludePrerelease</span></span> | <span data-ttu-id="b9e79-132">プレリリースのパッケージ更新プログラムにはが含まれます。</span><span class="sxs-lookup"><span data-stu-id="b9e79-132">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="b9e79-133">再インストール</span><span class="sxs-lookup"><span data-stu-id="b9e79-133">Reinstall</span></span> | <span data-ttu-id="b9e79-134">Resintalls パッケージが、現在インストールされているバージョンを使用します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-134">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="b9e79-135">参照してください[再インストールして、パッケージを更新する](../consume-packages/reinstalling-and-updating-packages.md)です。</span><span class="sxs-lookup"><span data-stu-id="b9e79-135">See [Reinstalling and updating packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="b9e79-136">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="b9e79-136">FileConflictAction</span></span> | <span data-ttu-id="b9e79-137">上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="b9e79-137">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="b9e79-138">指定できる値は*上書き、Ignore、None、OverwriteAll*、および*ignoreall です*(3.0 以降)。</span><span class="sxs-lookup"><span data-stu-id="b9e79-138">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="b9e79-139">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="b9e79-139">DependencyVersion</span></span> | <span data-ttu-id="b9e79-140">次のいずれかを使用する依存関係パッケージ バージョン:</span><span class="sxs-lookup"><span data-stu-id="b9e79-140">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="b9e79-141">*最小*(既定値): 最小バージョン</span><span class="sxs-lookup"><span data-stu-id="b9e79-141">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="b9e79-142">*HighestPatch*: 最小メジャー、マイナー最小、最高の修正プログラムのバージョン</span><span class="sxs-lookup"><span data-stu-id="b9e79-142">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="b9e79-143">*HighestMinor*: 主要な最小のバージョン、最高のマイナー、最上位の修正プログラム</span><span class="sxs-lookup"><span data-stu-id="b9e79-143">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="b9e79-144">*最も高い*(パラメーターなしで更新プログラム パッケージの既定): 最上位バージョン</span><span class="sxs-lookup"><span data-stu-id="b9e79-144">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="b9e79-145">使用して、既定値を設定することができます、 [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="b9e79-145">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="b9e79-146">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="b9e79-146">ToHighestPatch</span></span> | <span data-ttu-id="b9e79-147">現在インストールされているパッケージとマイナー バージョンが同じでバージョンのみへのアップグレードを制約します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-147">Constrains upgrades to only versions with the same Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="b9e79-148">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="b9e79-148">ToHighestMinor</span></span> | <span data-ttu-id="b9e79-149">現在インストールされているパッケージと同じメジャー バージョンのバージョンのみへのアップグレードを制約します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-149">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="b9e79-150">WhatIf</span><span class="sxs-lookup"><span data-stu-id="b9e79-150">WhatIf</span></span> | <span data-ttu-id="b9e79-151">実際には、更新プログラムを実行せず、コマンドを実行している場合にどうなるかを示します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-151">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="b9e79-152">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-152">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="b9e79-153">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="b9e79-153">Common Parameters</span></span>

<span data-ttu-id="b9e79-154">`Update-Package`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="b9e79-154">`Update-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="b9e79-155">使用例</span><span class="sxs-lookup"><span data-stu-id="b9e79-155">Examples</span></span>

```ps
# Updates all packages in every project of the solution
Update-Package

# Updates every package in the MvcApplication1 project
Update-Package -ProjectName MvcApplication1

# Updates the Elmah package in every project to the latest version
Update-Package Elmah

# Updates the Elmah package to version 1.1.0 in every project showing optional -Id usage
Update-Package -Id Elmah -Version 1.1.0

# Updates the Elmah package within the MvcApplication1 project to the highest "safe" version.
# For example, if Elmah version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2,
# and 1.1 are available in the feed, the -Safe parameter updates the package to 1.0.2 instead
# of 1.1 as it would otherwise.
Update-Package Elmah -ProjectName MvcApplication1 -Safe

# Reinstall the same version of the original package, but with the latest version of dependencies
# (subject to version constraints). If this command rolls a dependency back to an earlier version,
# use Update-Package <dependency_name> to reinstall that one dependency without affecting the
# dependent package.
Update-Package ELmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package ELmah –reinstall -ignoreDependencies
```