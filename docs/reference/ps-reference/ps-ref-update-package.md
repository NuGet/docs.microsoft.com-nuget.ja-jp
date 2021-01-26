---
title: NuGet Update-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Update-Package PowerShell コマンドのリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 159817e56d978d6432e989d2027907c0d2445222
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777376"
---
# <a name="update-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="a49f1-103">Update-Package (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="a49f1-103">Update-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a49f1-104">*Windows の Visual Studio の [NuGet パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="a49f1-104">*Available only within the [NuGet Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a49f1-105">パッケージとその依存関係、またはプロジェクト内のすべてのパッケージを新しいバージョンに更新します。</span><span class="sxs-lookup"><span data-stu-id="a49f1-105">Updates a package and its dependencies, or all packages in a project, to a newer version.</span></span>

## <a name="syntax"></a><span data-ttu-id="a49f1-106">構文</span><span class="sxs-lookup"><span data-stu-id="a49f1-106">Syntax</span></span>

```ps
Update-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [-Version <string>]
    [-Safe] [-Source <string>] [-IncludePrerelease] [-Reinstall] [-FileConflictAction]
    [-DependencyVersion] [-ToHighestPatch] [-ToHighestMinor] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="a49f1-107">NuGet 2.8 以降では、を `Update-Package` 使用して、プロジェクト内の既存のパッケージをダウングレードできます。</span><span class="sxs-lookup"><span data-stu-id="a49f1-107">In NuGet 2.8+, `Update-Package` can be used to downgrade an existing package in your project.</span></span> <span data-ttu-id="a49f1-108">たとえば、次のコマンドでは、Microsoft の AspNet. MVC 5.1.0-rc1 がインストールされている場合、それを5.0.0 にダウングレードします。</span><span class="sxs-lookup"><span data-stu-id="a49f1-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Update-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="a49f1-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="a49f1-109">Parameters</span></span>

|  <span data-ttu-id="a49f1-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="a49f1-110">Parameter</span></span> | <span data-ttu-id="a49f1-111">説明</span><span class="sxs-lookup"><span data-stu-id="a49f1-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a49f1-112">Id</span><span class="sxs-lookup"><span data-stu-id="a49f1-112">Id</span></span> | <span data-ttu-id="a49f1-113">更新するパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="a49f1-113">The identifier of the package to update.</span></span> <span data-ttu-id="a49f1-114">省略すると、すべてのパッケージが更新されます。</span><span class="sxs-lookup"><span data-stu-id="a49f1-114">If omitted, updates all packages.</span></span> <span data-ttu-id="a49f1-115">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="a49f1-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="a49f1-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="a49f1-116">IgnoreDependencies</span></span> | <span data-ttu-id="a49f1-117">パッケージの依存関係の更新をスキップします。</span><span class="sxs-lookup"><span data-stu-id="a49f1-117">Skips updating the package's dependencies.</span></span> |
| <span data-ttu-id="a49f1-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="a49f1-118">ProjectName</span></span> | <span data-ttu-id="a49f1-119">更新するパッケージが含まれているプロジェクトの名前。既定ではすべてのプロジェクトになります。</span><span class="sxs-lookup"><span data-stu-id="a49f1-119">The name of the project containing the packages to update, defaulting to all projects.</span></span> |
| <span data-ttu-id="a49f1-120">Version</span><span class="sxs-lookup"><span data-stu-id="a49f1-120">Version</span></span> | <span data-ttu-id="a49f1-121">アップグレードに使用するバージョン。既定では、最新バージョンが使用されます。</span><span class="sxs-lookup"><span data-stu-id="a49f1-121">The version to use for the upgrade, defaulting to the latest version.</span></span> <span data-ttu-id="a49f1-122">NuGet 3.0 以降では、バージョンの値は、 *最低、最高、HighestMinor*、または *HighestPatch* のいずれかである必要があります (これはセーフに相当します)。</span><span class="sxs-lookup"><span data-stu-id="a49f1-122">In NuGet 3.0+, the version value must be one of *Lowest, Highest, HighestMinor*, or *HighestPatch* (equivalent to -Safe).</span></span> |
| <span data-ttu-id="a49f1-123">Safe</span><span class="sxs-lookup"><span data-stu-id="a49f1-123">Safe</span></span> | <span data-ttu-id="a49f1-124">は、現在インストールされているパッケージと同じメジャーバージョンとマイナーバージョンを持つバージョンにのみアップグレードを制限します。</span><span class="sxs-lookup"><span data-stu-id="a49f1-124">Constrains upgrades to only versions with the same Major and Minor version as the currently installed package.</span></span> |
| <span data-ttu-id="a49f1-125">source</span><span class="sxs-lookup"><span data-stu-id="a49f1-125">Source</span></span> | <span data-ttu-id="a49f1-126">検索するパッケージソースの URL またはフォルダーパス。</span><span class="sxs-lookup"><span data-stu-id="a49f1-126">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="a49f1-127">ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="a49f1-127">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="a49f1-128">省略した場合、 `Update-Package` 現在選択されているパッケージソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="a49f1-128">If omitted, `Update-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="a49f1-129">IncludePrerelease リリース</span><span class="sxs-lookup"><span data-stu-id="a49f1-129">IncludePrerelease</span></span> | <span data-ttu-id="a49f1-130">更新プログラムのプレリリースパッケージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a49f1-130">Includes prerelease packages for updates.</span></span> |
| <span data-ttu-id="a49f1-131">再インストール</span><span class="sxs-lookup"><span data-stu-id="a49f1-131">Reinstall</span></span> | <span data-ttu-id="a49f1-132">現在インストールされているバージョンを使用してパッケージを Resintalls します。</span><span class="sxs-lookup"><span data-stu-id="a49f1-132">Resintalls packages using their currently installed versions.</span></span> <span data-ttu-id="a49f1-133">「 [パッケージの再インストールと更新」を](../../consume-packages/reinstalling-and-updating-packages.md)参照してください。</span><span class="sxs-lookup"><span data-stu-id="a49f1-133">See [Reinstalling and updating packages](../../consume-packages/reinstalling-and-updating-packages.md).</span></span> |
| <span data-ttu-id="a49f1-134">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="a49f1-134">FileConflictAction</span></span> | <span data-ttu-id="a49f1-135">プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="a49f1-135">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="a49f1-136">指定できる値は *、Overwrite、Ignore、None、OverwriteAll*、および *ignoreall* (3.0 +) です。</span><span class="sxs-lookup"><span data-stu-id="a49f1-136">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *IgnoreAll* (3.0+).</span></span> |
| <span data-ttu-id="a49f1-137">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="a49f1-137">DependencyVersion</span></span> | <span data-ttu-id="a49f1-138">使用する依存関係パッケージのバージョン。次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="a49f1-138">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="a49f1-139">*最低* (既定): 最も低いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="a49f1-139">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="a49f1-140">*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</span><span class="sxs-lookup"><span data-stu-id="a49f1-140">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="a49f1-141">*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</span><span class="sxs-lookup"><span data-stu-id="a49f1-141">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="a49f1-142">*最高* (パラメーターのない Update-Package の既定値): 最高バージョン</span><span class="sxs-lookup"><span data-stu-id="a49f1-142">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="a49f1-143">ファイルの設定を使用して、既定値を設定でき [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` ます。</span><span class="sxs-lookup"><span data-stu-id="a49f1-143">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="a49f1-144">ToHighestPatch</span><span class="sxs-lookup"><span data-stu-id="a49f1-144">ToHighestPatch</span></span> | <span data-ttu-id="a49f1-145">-Safe と同等です。</span><span class="sxs-lookup"><span data-stu-id="a49f1-145">equivalent to -Safe.</span></span> |
| <span data-ttu-id="a49f1-146">ToHighestMinor</span><span class="sxs-lookup"><span data-stu-id="a49f1-146">ToHighestMinor</span></span> | <span data-ttu-id="a49f1-147">は、現在インストールされているパッケージと同じメジャーバージョンのバージョンにのみアップグレードを制限します。</span><span class="sxs-lookup"><span data-stu-id="a49f1-147">Constrains upgrades to only versions with the same Major version as the currently installed package.</span></span> |
| <span data-ttu-id="a49f1-148">WhatIf</span><span class="sxs-lookup"><span data-stu-id="a49f1-148">WhatIf</span></span> | <span data-ttu-id="a49f1-149">実際に更新を実行せずにコマンドを実行した場合の動作を示します。</span><span class="sxs-lookup"><span data-stu-id="a49f1-149">Shows what would happen when running the command without actually performing the update.</span></span> |

<span data-ttu-id="a49f1-150">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="a49f1-150">None of these parameters accept pipeline input or wildcard characters.</span></span>

### <a name="common-parameters"></a><span data-ttu-id="a49f1-151">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="a49f1-151">Common Parameters</span></span>

<span data-ttu-id="a49f1-152">`Update-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a49f1-152">`Update-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

### <a name="examples"></a><span data-ttu-id="a49f1-153">使用例</span><span class="sxs-lookup"><span data-stu-id="a49f1-153">Examples</span></span>

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
Update-Package Elmah –reinstall 

# Reinstall the Elmah package in just MyProject
Update-Package Elmah -ProjectName MyProject -reinstall

# Reinstall the same version of the original package without touching dependencies.
Update-Package Elmah –reinstall -ignoreDependencies
```
