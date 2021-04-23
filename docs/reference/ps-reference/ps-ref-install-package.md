---
title: NuGet Install-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Install-Package PowerShell コマンドのリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ad551b8701cfc2061f7721fb050ed9b5a4fede32
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901695"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f6423-103">Install-Package (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="f6423-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f6423-104">*このトピックでは、Windows 上の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内のコマンドについて説明します。汎用 PowerShell Install-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="f6423-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement).*</span></span>

<span data-ttu-id="f6423-105">パッケージとその依存関係をプロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="f6423-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="f6423-106">構文</span><span class="sxs-lookup"><span data-stu-id="f6423-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f6423-107">NuGet 2.8 以降では、は `Install-Package` プロジェクト内の既存のパッケージをダウングレードできます。</span><span class="sxs-lookup"><span data-stu-id="f6423-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="f6423-108">たとえば、次のコマンドでは、Microsoft の AspNet. MVC 5.1.0-rc1 がインストールされている場合、それを5.0.0 にダウングレードします。</span><span class="sxs-lookup"><span data-stu-id="f6423-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="f6423-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f6423-109">Parameters</span></span>

| <span data-ttu-id="f6423-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f6423-110">Parameter</span></span> | <span data-ttu-id="f6423-111">説明</span><span class="sxs-lookup"><span data-stu-id="f6423-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6423-112">Id</span><span class="sxs-lookup"><span data-stu-id="f6423-112">Id</span></span> | <span data-ttu-id="f6423-113">必要インストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="f6423-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="f6423-114">(*3.0 以降*)識別子には、ファイルまたはファイルのパスまたは URL を指定でき `packages.config` `.nupkg` ます。</span><span class="sxs-lookup"><span data-stu-id="f6423-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="f6423-115">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="f6423-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f6423-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="f6423-116">IgnoreDependencies</span></span> | <span data-ttu-id="f6423-117">依存関係ではなく、このパッケージのみをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f6423-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="f6423-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f6423-118">ProjectName</span></span> | <span data-ttu-id="f6423-119">パッケージのインストール先となるプロジェクト。既定のプロジェクトが既定のプロジェクトになります。</span><span class="sxs-lookup"><span data-stu-id="f6423-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="f6423-120">source</span><span class="sxs-lookup"><span data-stu-id="f6423-120">Source</span></span> | <span data-ttu-id="f6423-121">検索するパッケージソースの URL またはフォルダーパス。</span><span class="sxs-lookup"><span data-stu-id="f6423-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f6423-122">ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="f6423-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f6423-123">省略した場合、 `Install-Package` 現在選択されているパッケージソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="f6423-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f6423-124">Version</span><span class="sxs-lookup"><span data-stu-id="f6423-124">Version</span></span> | <span data-ttu-id="f6423-125">インストールするパッケージのバージョン。既定では、最新バージョンが対象となります。</span><span class="sxs-lookup"><span data-stu-id="f6423-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="f6423-126">IncludePrerelease リリース</span><span class="sxs-lookup"><span data-stu-id="f6423-126">IncludePrerelease</span></span> | <span data-ttu-id="f6423-127">インストールのプレリリースパッケージを検討します。</span><span class="sxs-lookup"><span data-stu-id="f6423-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="f6423-128">省略した場合、安定版パッケージのみが考慮されます。</span><span class="sxs-lookup"><span data-stu-id="f6423-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="f6423-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f6423-129">FileConflictAction</span></span> | <span data-ttu-id="f6423-130">プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="f6423-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f6423-131">指定できる値は *、Overwrite、Ignore、None、OverwriteAll*、 *(3.0 +)* *ignoreall* です。</span><span class="sxs-lookup"><span data-stu-id="f6423-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="f6423-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f6423-132">DependencyVersion</span></span> | <span data-ttu-id="f6423-133">使用する依存関係パッケージのバージョン。次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="f6423-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f6423-134">*最低* (既定): 最も低いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="f6423-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f6423-135">*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</span><span class="sxs-lookup"><span data-stu-id="f6423-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f6423-136">*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</span><span class="sxs-lookup"><span data-stu-id="f6423-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f6423-137">*最高* (パラメーターのない Update-Package の既定値): 最高バージョン</span><span class="sxs-lookup"><span data-stu-id="f6423-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f6423-138">ファイルの設定を使用して、既定値を設定でき [`dependencyVersion`](../nuget-config-file.md#config-section) `Nuget.Config` ます。</span><span class="sxs-lookup"><span data-stu-id="f6423-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f6423-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f6423-139">WhatIf</span></span> | <span data-ttu-id="f6423-140">実際にインストールを実行せずにコマンドを実行した場合の動作を示します。</span><span class="sxs-lookup"><span data-stu-id="f6423-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="f6423-141">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="f6423-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f6423-142">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="f6423-142">Common Parameters</span></span>

<span data-ttu-id="f6423-143">`Install-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="f6423-143">`Install-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f6423-144">使用例</span><span class="sxs-lookup"><span data-stu-id="f6423-144">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project
# Note: the URL must end with "packages.config"
Install-Package https://raw.githubusercontent.com/linked-data-dotnet/json-ld.net/master/.nuget/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages
Install-Package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
# Note: the URL must end with ".nupkg"
Install-Package https://globalcdn.nuget.org/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```