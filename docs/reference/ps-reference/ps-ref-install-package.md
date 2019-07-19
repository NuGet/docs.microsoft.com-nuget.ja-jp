---
title: NuGet インストール-パッケージ PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでのインストールパッケージ PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 1899662049735189ab4dcb728df5d56afdc5f7c5
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327339"
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="dc7c0-103">Install-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="dc7c0-103">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="dc7c0-104">*このトピックでは、Windows 上の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内のコマンドについて説明します。汎用 PowerShell のインストールパッケージコマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="dc7c0-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="dc7c0-105">パッケージとその依存関係をプロジェクトにインストールします。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-105">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="dc7c0-106">構文</span><span class="sxs-lookup"><span data-stu-id="dc7c0-106">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="dc7c0-107">NuGet 2.8 以降では`Install-Package` 、はプロジェクト内の既存のパッケージをダウングレードできます。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-107">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="dc7c0-108">たとえば、次のコマンドでは、Microsoft の AspNet. MVC 5.1.0-rc1 がインストールされている場合、それを5.0.0 にダウングレードします。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-108">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

## <a name="parameters"></a><span data-ttu-id="dc7c0-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="dc7c0-109">Parameters</span></span>

| <span data-ttu-id="dc7c0-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="dc7c0-110">Parameter</span></span> | <span data-ttu-id="dc7c0-111">説明</span><span class="sxs-lookup"><span data-stu-id="dc7c0-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dc7c0-112">ID</span><span class="sxs-lookup"><span data-stu-id="dc7c0-112">Id</span></span> | <span data-ttu-id="dc7c0-113">必要インストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-113">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="dc7c0-114">(*3.0 以降*)識別子には、 `packages.config`ファイル`.nupkg`またはファイルのパスまたは URL を指定できます。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-114">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="dc7c0-115">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="dc7c0-116">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="dc7c0-116">IgnoreDependencies</span></span> | <span data-ttu-id="dc7c0-117">依存関係ではなく、このパッケージのみをインストールします。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-117">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="dc7c0-118">ProjectName</span><span class="sxs-lookup"><span data-stu-id="dc7c0-118">ProjectName</span></span> | <span data-ttu-id="dc7c0-119">パッケージのインストール先となるプロジェクト。既定のプロジェクトが既定のプロジェクトになります。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-119">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="dc7c0-120">Source</span><span class="sxs-lookup"><span data-stu-id="dc7c0-120">Source</span></span> | <span data-ttu-id="dc7c0-121">検索するパッケージソースの URL またはフォルダーパス。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-121">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="dc7c0-122">ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-122">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="dc7c0-123">省略した`Install-Package`場合、現在選択されているパッケージソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-123">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="dc7c0-124">Version</span><span class="sxs-lookup"><span data-stu-id="dc7c0-124">Version</span></span> | <span data-ttu-id="dc7c0-125">インストールするパッケージのバージョン。既定では、最新バージョンが対象となります。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-125">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="dc7c0-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="dc7c0-126">IncludePrerelease</span></span> | <span data-ttu-id="dc7c0-127">インストールのプレリリースパッケージを検討します。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-127">Considers prerelease packages for the install.</span></span> <span data-ttu-id="dc7c0-128">省略した場合、安定したパッケージだけが考慮されます。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-128">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="dc7c0-129">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="dc7c0-129">FileConflictAction</span></span> | <span data-ttu-id="dc7c0-130">プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-130">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="dc7c0-131">指定できる値は *、Overwrite、Ignore、None、OverwriteAll*、 *(3.0 +)* *ignoreall*です。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-131">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="dc7c0-132">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="dc7c0-132">DependencyVersion</span></span> | <span data-ttu-id="dc7c0-133">使用する依存関係パッケージのバージョン。次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-133">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="dc7c0-134">*最低*(既定): 最も低いバージョン</span><span class="sxs-lookup"><span data-stu-id="dc7c0-134">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="dc7c0-135">*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</span><span class="sxs-lookup"><span data-stu-id="dc7c0-135">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="dc7c0-136">*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</span><span class="sxs-lookup"><span data-stu-id="dc7c0-136">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="dc7c0-137">*最高*(パラメーターのない更新プログラム-パッケージの既定値): 最高のバージョン</span><span class="sxs-lookup"><span data-stu-id="dc7c0-137">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="dc7c0-138">`Nuget.Config`ファイルの[`dependencyVersion`](../nuget-config-file.md#config-section)設定を使用して、既定値を設定できます。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-138">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="dc7c0-139">WhatIf</span><span class="sxs-lookup"><span data-stu-id="dc7c0-139">WhatIf</span></span> | <span data-ttu-id="dc7c0-140">実際にインストールを実行せずにコマンドを実行した場合の動作を示します。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-140">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="dc7c0-141">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-141">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="dc7c0-142">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="dc7c0-142">Common Parameters</span></span>

<span data-ttu-id="dc7c0-143">`Install-Package`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。</span><span class="sxs-lookup"><span data-stu-id="dc7c0-143">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="dc7c0-144">使用例</span><span class="sxs-lookup"><span data-stu-id="dc7c0-144">Examples</span></span>

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
