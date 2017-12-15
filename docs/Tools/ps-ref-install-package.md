---
title: "NuGet のインストール パッケージの PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 879db0ef-6b72-4a4a-bb68-f9e3a00f64b8
description: "Visual Studio で NuGet パッケージ マネージャー コンソールのインストール パッケージの PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、インストール パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: d51cce6223cd2d89c555ca9d6e936eaadf3757bb
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="install-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="5ca54-104">インストール パッケージ (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="5ca54-104">Install-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="5ca54-105">*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。汎用の PowerShell のインストール パッケージ コマンドでは、次を参照してください。、 [PowerShell PackageManagement 参照](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6)です。*</span><span class="sxs-lookup"><span data-stu-id="5ca54-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Install-Package command, see the [PowerShell PackageManagement reference](https://docs.microsoft.com/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="5ca54-106">プロジェクトにパッケージとその依存関係をインストールします。</span><span class="sxs-lookup"><span data-stu-id="5ca54-106">Installs a package and its dependencies into a project.</span></span>

## <a name="syntax"></a><span data-ttu-id="5ca54-107">構文</span><span class="sxs-lookup"><span data-stu-id="5ca54-107">Syntax</span></span>

```ps
Install-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Source] <string>] 
    [[-Version] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="5ca54-108">NuGet 2.8 + で`Install-Package`プロジェクトで既存のパッケージをダウン グレードできます。</span><span class="sxs-lookup"><span data-stu-id="5ca54-108">In NuGet 2.8+, `Install-Package` can downgrade an existing package in your project.</span></span> <span data-ttu-id="5ca54-109">たとえば、Microsoft.AspNet.MVC 5.1.0-rc1 がインストールされている場合は、次のコマンドはへのダウン グレードに 5.0.0 以降。</span><span class="sxs-lookup"><span data-stu-id="5ca54-109">For example, if you have Microsoft.AspNet.MVC 5.1.0-rc1 installed, the following command would downgrade it to 5.0.0:</span></span>

```ps
Install-Package Microsoft.AspNet.MVC -Version 5.0.0.
```

<span data-ttu-id="5ca54-110">NuGet 2.7 およびそれ以前では、新しいバージョンが既にインストールされていることを示すエラーを説明します。</span><span class="sxs-lookup"><span data-stu-id="5ca54-110">NuGet 2.7 and earlier gives an error saying that a newer version is already installed.</span></span>
  
## <a name="parameters"></a><span data-ttu-id="5ca54-111">パラメーター</span><span class="sxs-lookup"><span data-stu-id="5ca54-111">Parameters</span></span>

| <span data-ttu-id="5ca54-112">パラメーター</span><span class="sxs-lookup"><span data-stu-id="5ca54-112">Parameter</span></span> | <span data-ttu-id="5ca54-113">説明</span><span class="sxs-lookup"><span data-stu-id="5ca54-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5ca54-114">ID</span><span class="sxs-lookup"><span data-stu-id="5ca54-114">Id</span></span> | <span data-ttu-id="5ca54-115">(必須)インストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="5ca54-115">(Required) The identifier of the package to install.</span></span> <span data-ttu-id="5ca54-116">(*3.0 +*) パスまたは URL 識別子を指定できます、`packages.config`ファイルまたは`.nupkg`ファイル。</span><span class="sxs-lookup"><span data-stu-id="5ca54-116">(*3.0+*) The identifier can be a path or URL of a `packages.config` file or a `.nupkg` file.</span></span> <span data-ttu-id="5ca54-117">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="5ca54-117">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="5ca54-118">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="5ca54-118">IgnoreDependencies</span></span> | <span data-ttu-id="5ca54-119">このパッケージのみを依存関係は含めずをインストールします。</span><span class="sxs-lookup"><span data-stu-id="5ca54-119">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="5ca54-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="5ca54-120">ProjectName</span></span> | <span data-ttu-id="5ca54-121">既定で、既定のプロジェクト、パッケージのインストール先のプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="5ca54-121">The project into which to install the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="5ca54-122">ソース</span><span class="sxs-lookup"><span data-stu-id="5ca54-122">Source</span></span> | <span data-ttu-id="5ca54-123">検索するパッケージ ソースの URL またはフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="5ca54-123">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="5ca54-124">ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="5ca54-124">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="5ca54-125">省略した場合、`Install-Package`現在選択されているパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="5ca54-125">If omitted, `Install-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="5ca54-126">Version</span><span class="sxs-lookup"><span data-stu-id="5ca54-126">Version</span></span> | <span data-ttu-id="5ca54-127">バージョンをインストールするパッケージの最新バージョンを既定とします。</span><span class="sxs-lookup"><span data-stu-id="5ca54-127">The version of the package to install, defaulting to the latest version.</span></span> |
| <span data-ttu-id="5ca54-128">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="5ca54-128">IncludePrerelease</span></span> | <span data-ttu-id="5ca54-129">プレリリースのパッケージのインストールを検討します。</span><span class="sxs-lookup"><span data-stu-id="5ca54-129">Considers prerelease packages for the install.</span></span> <span data-ttu-id="5ca54-130">省略した場合は、安定版パッケージのみが考慮されます。</span><span class="sxs-lookup"><span data-stu-id="5ca54-130">If omitted, only stable packages are considered.</span></span> |
| <span data-ttu-id="5ca54-131">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="5ca54-131">FileConflictAction</span></span> | <span data-ttu-id="5ca54-132">上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="5ca54-132">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="5ca54-133">指定できる値は*上書き、Ignore、None、OverwriteAll*、および*(3.0 以降)* *ignoreall です*です。</span><span class="sxs-lookup"><span data-stu-id="5ca54-133">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="5ca54-134">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="5ca54-134">DependencyVersion</span></span> | <span data-ttu-id="5ca54-135">次のいずれかを使用する依存関係パッケージ バージョン:</span><span class="sxs-lookup"><span data-stu-id="5ca54-135">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="5ca54-136">*最小*(既定値): 最小バージョン</span><span class="sxs-lookup"><span data-stu-id="5ca54-136">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="5ca54-137">*HighestPatch*: 最小メジャー、マイナー最小、最高の修正プログラムのバージョン</span><span class="sxs-lookup"><span data-stu-id="5ca54-137">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="5ca54-138">*HighestMinor*: 主要な最小のバージョン、最高のマイナー、最上位の修正プログラム</span><span class="sxs-lookup"><span data-stu-id="5ca54-138">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="5ca54-139">*最も高い*(パラメーターなしで更新プログラム パッケージの既定): 最上位バージョン</span><span class="sxs-lookup"><span data-stu-id="5ca54-139">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="5ca54-140">使用して、既定値を設定することができます、 [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="5ca54-140">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="5ca54-141">WhatIf</span><span class="sxs-lookup"><span data-stu-id="5ca54-141">WhatIf</span></span> | <span data-ttu-id="5ca54-142">実際には、インストールを実行せず、コマンドを実行している場合にどうなるかを示します。</span><span class="sxs-lookup"><span data-stu-id="5ca54-142">Shows what would happen when running the command without actually performing the install.</span></span> |

<span data-ttu-id="5ca54-143">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="5ca54-143">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="5ca54-144">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="5ca54-144">Common Parameters</span></span>

<span data-ttu-id="5ca54-145">`Install-Package`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="5ca54-145">`Install-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="5ca54-146">例</span><span class="sxs-lookup"><span data-stu-id="5ca54-146">Examples</span></span>

```ps
# Installs the latest version of Elmah from the current source into the default project
Install-Package Elmah

# Installs Glimpse 1.0.0 into the MvcApplication1 project
Install-Package Glimpse -Version 1.0.0 -Project MvcApplication1

# Installs Ninject.Mvc3 but not its dependencies from c:\temp\packages
Install-Package Ninject.Mvc3 -IgnoreDependencies -Source c:\temp\packages

# Installs the package listed on the online packages.config into the current project.
Install-package https://raw.githubusercontent.com/json-ld.net/master/src/JsonLD/packages.config

# Installs jquery 1.10.2 package, using the .nupkg file under local path of c:\temp\packages.
Install-package c:\temp\packages\jQuery.1.10.2.nupkg

# Installs the specific online package
Install-package https://az320820.vo.msecnd.net/packages/microsoft.aspnet.mvc.5.2.3.nupkg
```
