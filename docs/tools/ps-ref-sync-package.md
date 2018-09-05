---
title: NuGet の同期パッケージ PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで同期パッケージの PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8119664b1bafe9238b12b1819cc46dc1ee7bdd00
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547995"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="1643b-103">Sync-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="1643b-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1643b-104">*バージョン 3.0 以降。内でのみ使用可能な[NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="1643b-104">*Version 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1643b-105">指定した (または既定値) からインストールされているパッケージのバージョンを取得しますはプロジェクトし、ソリューション内のプロジェクトの他のバージョンを同期します。</span><span class="sxs-lookup"><span data-stu-id="1643b-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="1643b-106">構文</span><span class="sxs-lookup"><span data-stu-id="1643b-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1643b-107">パラメーター</span><span class="sxs-lookup"><span data-stu-id="1643b-107">Parameters</span></span>

| <span data-ttu-id="1643b-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="1643b-108">Parameter</span></span> | <span data-ttu-id="1643b-109">説明</span><span class="sxs-lookup"><span data-stu-id="1643b-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1643b-110">ID</span><span class="sxs-lookup"><span data-stu-id="1643b-110">Id</span></span> | <span data-ttu-id="1643b-111">(必須)同期するパッケージの識別子です。-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="1643b-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="1643b-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="1643b-112">IgnoreDependencies</span></span> | <span data-ttu-id="1643b-113">このパッケージのみとその依存関係のないをインストールします。</span><span class="sxs-lookup"><span data-stu-id="1643b-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="1643b-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="1643b-114">ProjectName</span></span> | <span data-ttu-id="1643b-115">既定では、既定のプロジェクトから、パッケージを同期するプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="1643b-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="1643b-116">Version</span><span class="sxs-lookup"><span data-stu-id="1643b-116">Version</span></span> | <span data-ttu-id="1643b-117">同期するには、パッケージのバージョン、現在インストールされているバージョンを既定値します。</span><span class="sxs-lookup"><span data-stu-id="1643b-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="1643b-118">ソース</span><span class="sxs-lookup"><span data-stu-id="1643b-118">Source</span></span> | <span data-ttu-id="1643b-119">検索するパッケージ ソースの URL またはフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="1643b-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="1643b-120">ローカル フォルダー パスには、absolute、または現在のフォルダーの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="1643b-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="1643b-121">省略した場合、`Sync-Package`現在選択されているパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="1643b-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="1643b-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="1643b-122">IncludePrerelease</span></span> | <span data-ttu-id="1643b-123">同期では、プレリリース パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="1643b-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="1643b-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="1643b-124">FileConflictAction</span></span> | <span data-ttu-id="1643b-125">上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められる場合に実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="1643b-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="1643b-126">指定できる値は*上書き、Ignore、None、OverwriteAll*、および *(3.0 +)* *ignoreall です*します。</span><span class="sxs-lookup"><span data-stu-id="1643b-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="1643b-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="1643b-127">DependencyVersion</span></span> | <span data-ttu-id="1643b-128">次のいずれかの値を使用する依存関係パッケージのバージョン:</span><span class="sxs-lookup"><span data-stu-id="1643b-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="1643b-129">*最も低い*(既定値): 最小バージョン</span><span class="sxs-lookup"><span data-stu-id="1643b-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="1643b-130">*HighestPatch*: 最高レベルの最も大きなを最低軽微な修正プログラムのバージョン</span><span class="sxs-lookup"><span data-stu-id="1643b-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="1643b-131">*HighestMinor*: 主要な最小のバージョン、マイナー、最高の最高の修正プログラム</span><span class="sxs-lookup"><span data-stu-id="1643b-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="1643b-132">*最も高い*(パラメーターなしの更新プログラム パッケージの既定): 最上位のバージョン</span><span class="sxs-lookup"><span data-stu-id="1643b-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="1643b-133">使用して、既定値を設定することができます、 [ `dependencyVersion` ](../reference/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="1643b-133">You can set the default value using the [`dependencyVersion`](../reference/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="1643b-134">WhatIf</span><span class="sxs-lookup"><span data-stu-id="1643b-134">WhatIf</span></span> | <span data-ttu-id="1643b-135">実際には、同期を実行することがなく、コマンドを実行するときに何が起こるかを示します。</span><span class="sxs-lookup"><span data-stu-id="1643b-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="1643b-136">これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="1643b-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1643b-137">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="1643b-137">Common Parameters</span></span>

<span data-ttu-id="1643b-138">`Sync-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="1643b-138">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1643b-139">使用例</span><span class="sxs-lookup"><span data-stu-id="1643b-139">Examples</span></span>

```ps
# Sync the Elmah package installed in the default project into the other projects in the solution
Sync-Package Elmah

# Sync the Elmah package installed in the ClassLibrary1 project into other projects in the solution
Sync-Package Elmah -ProjectName ClassLibrary1

# Sync Microsoft.Aspnet.package but not its dependencies into the other projects in the solution
Sync-Package Microsoft.Aspnet.Mvc -IgnoreDependencies

# Sync jQuery.Validation and install the highest version of jQuery (a dependency) from the package source    
Sync-Package jQuery.Validation -DependencyVersion highest
```
