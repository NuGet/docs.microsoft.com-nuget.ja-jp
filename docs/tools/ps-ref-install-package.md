---
title: NuGet のインストール パッケージの PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで Install-package の PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: e7ddf9ad97cbb4ec9cfc8b01f366511239f41416
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546027"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c0c73-103">Install-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="c0c73-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c0c73-104">*このトピックでは、内のコマンドを説明します、 [NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。一般的な PowerShell のインストール パッケージ コマンドは、、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="c0c73-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="c0c73-105">プロジェクトにパッケージとその依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="c0c73-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="c0c73-106">構文</span><span class="sxs-lookup"><span data-stu-id="c0c73-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="c0c73-107">NuGet 2.8 以降で`Install-Package`プロジェクトに既存のパッケージをダウン グレードできます。</span><span class="sxs-lookup"><span data-stu-id="c0c73-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="c0c73-108">たとえば、Microsoft.AspNet.MVC 5.1.0-rc1 がインストールされている場合は、次のコマンドはダウン グレード 5.0.0。</span><span class="sxs-lookup"><span data-stu-id="c0c73-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="c0c73-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c0c73-109">Parameters</span></span>

| <span data-ttu-id="c0c73-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c0c73-110">Parameter</span></span> | <span data-ttu-id="c0c73-111">説明</span><span class="sxs-lookup"><span data-stu-id="c0c73-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0c73-112">ID</span><span class="sxs-lookup"><span data-stu-id="c0c73-112">Id</span></span> | <span data-ttu-id="c0c73-113">(必須)インストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="c0c73-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="c0c73-114">(*3.0 +* ) 識別子は、パスまたは URL の`packages.config`ファイルまたは`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="c0c73-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="c0c73-115">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="c0c73-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c0c73-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="c0c73-116">IgnoreDependencies</span></span> | <span data-ttu-id="c0c73-117">このパッケージのみとその依存関係のないをインストールします。</span><span class="sxs-lookup"><span data-stu-id="c0c73-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="c0c73-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c0c73-118">ProjectName</span></span> | <span data-ttu-id="c0c73-119">既定では、既定のプロジェクト、パッケージをインストールするプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="c0c73-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="c0c73-120">source</span><span class="sxs-lookup"><span data-stu-id="c0c73-120">Source</span></span> | <span data-ttu-id="c0c73-121">検索するパッケージ ソースの URL またはフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="c0c73-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="c0c73-122">ローカル フォルダー パスには、absolute、または現在のフォルダーの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="c0c73-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="c0c73-123">省略した場合、`Install-Package`現在選択されているパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="c0c73-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="c0c73-124">Version</span><span class="sxs-lookup"><span data-stu-id="c0c73-124">Version</span></span> | <span data-ttu-id="c0c73-125">バージョンをインストールするパッケージの既定の最新バージョンになります。</span><span class="sxs-lookup"><span data-stu-id="c0c73-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="c0c73-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="c0c73-126">IncludePrerelease</span></span> | <span data-ttu-id="c0c73-127">プレリリース パッケージのインストールを検討します。</span><span class="sxs-lookup"><span data-stu-id="c0c73-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="c0c73-128">省略した場合は、安定版パッケージのみが考慮されます。</span><span class="sxs-lookup"><span data-stu-id="c0c73-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="c0c73-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="c0c73-129">FileConflictAction</span></span> | <span data-ttu-id="c0c73-130">上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められる場合に実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="c0c73-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="c0c73-131">指定できる値は*上書き、Ignore、None、OverwriteAll*、および *(3.0 +)* *ignoreall です*します。</span><span class="sxs-lookup"><span data-stu-id="c0c73-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="c0c73-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="c0c73-132">DependencyVersion</span></span> | <span data-ttu-id="c0c73-133">次のいずれかの値を使用する依存関係パッケージのバージョン:</span><span class="sxs-lookup"><span data-stu-id="c0c73-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="c0c73-134">*最も低い*(既定値): 最小バージョン</span><span class="sxs-lookup"><span data-stu-id="c0c73-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="c0c73-135">*HighestPatch*: 最高レベルの最も大きなを最低軽微な修正プログラムのバージョン</span><span class="sxs-lookup"><span data-stu-id="c0c73-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="c0c73-136">*HighestMinor*: 主要な最小のバージョン、マイナー、最高の最高の修正プログラム</span><span class="sxs-lookup"><span data-stu-id="c0c73-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="c0c73-137">*最も高い*(パラメーターなしの更新プログラム パッケージの既定): 最上位のバージョン</span><span class="sxs-lookup"><span data-stu-id="c0c73-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="c0c73-138">使用して、既定値を設定することができます、 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="c0c73-138">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="c0c73-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="c0c73-139">WhatIf</span></span> | <span data-ttu-id="c0c73-140">実際には、インストールを実行せず、コマンドを実行するときに何が起こるかを示します。</span><span class="sxs-lookup"><span data-stu-id="c0c73-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="c0c73-141">これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="c0c73-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c0c73-142">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="c0c73-142">Common Parameters</span></span>

<span data-ttu-id="c0c73-143">`Install-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="c0c73-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c0c73-144">使用例</span><span class="sxs-lookup"><span data-stu-id="c0c73-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
