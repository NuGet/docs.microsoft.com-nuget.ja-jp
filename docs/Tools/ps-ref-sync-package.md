---
title: "NuGet 同期パッケージの PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 1b980b93-fa58-430c-b663-78ce069b1603
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで同期パッケージの PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、Sync パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4dc542714f14f0e6d3e827292f8fce06561fe270
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/14/2017
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7b22a-104">Sync パッケージ (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="7b22a-104">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7b22a-105">*Version 3.0 以降。内でのみ使用可能な[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="7b22a-105">*Version 3.0+; available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7b22a-106">指定した (または既定値) からインストールされているパッケージのバージョンを取得では、プロジェクトし、ソリューション内のプロジェクトの残りの部分をバージョンを同期します。</span><span class="sxs-lookup"><span data-stu-id="7b22a-106">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="7b22a-107">構文</span><span class="sxs-lookup"><span data-stu-id="7b22a-107">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7b22a-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7b22a-108">Parameters</span></span>

| <span data-ttu-id="7b22a-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7b22a-109">Parameter</span></span> | <span data-ttu-id="7b22a-110">説明</span><span class="sxs-lookup"><span data-stu-id="7b22a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7b22a-111">ID</span><span class="sxs-lookup"><span data-stu-id="7b22a-111">Id</span></span> | <span data-ttu-id="7b22a-112">(必須)同期するパッケージの識別子。-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="7b22a-112">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7b22a-113">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="7b22a-113">IgnoreDependencies</span></span> | <span data-ttu-id="7b22a-114">このパッケージのみを依存関係は含めずをインストールします。</span><span class="sxs-lookup"><span data-stu-id="7b22a-114">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="7b22a-115">ProjectName</span><span class="sxs-lookup"><span data-stu-id="7b22a-115">ProjectName</span></span> | <span data-ttu-id="7b22a-116">既定で、既定のプロジェクトから、パッケージを同期するプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="7b22a-116">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="7b22a-117">Version</span><span class="sxs-lookup"><span data-stu-id="7b22a-117">Version</span></span> | <span data-ttu-id="7b22a-118">同期するには、パッケージのバージョン、現在インストールされているバージョンを既定とします。</span><span class="sxs-lookup"><span data-stu-id="7b22a-118">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="7b22a-119">ソース</span><span class="sxs-lookup"><span data-stu-id="7b22a-119">Source</span></span> | <span data-ttu-id="7b22a-120">検索するパッケージ ソースの URL またはフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="7b22a-120">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="7b22a-121">ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="7b22a-121">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="7b22a-122">省略した場合、`Sync-Package`現在選択されているパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="7b22a-122">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="7b22a-123">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="7b22a-123">IncludePrerelease</span></span> | <span data-ttu-id="7b22a-124">同期では、プレリリースのパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="7b22a-124">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="7b22a-125">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="7b22a-125">FileConflictAction</span></span> | <span data-ttu-id="7b22a-126">上書きするか、プロジェクトによって参照されている既存のファイルを無視するように求められたらを実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="7b22a-126">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="7b22a-127">指定できる値は*上書き、Ignore、None、OverwriteAll*、および*(3.0 以降)* *ignoreall です*です。</span><span class="sxs-lookup"><span data-stu-id="7b22a-127">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="7b22a-128">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="7b22a-128">DependencyVersion</span></span> | <span data-ttu-id="7b22a-129">次のいずれかを使用する依存関係パッケージ バージョン:</span><span class="sxs-lookup"><span data-stu-id="7b22a-129">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="7b22a-130">*最小*(既定値): 最小バージョン</span><span class="sxs-lookup"><span data-stu-id="7b22a-130">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="7b22a-131">*HighestPatch*: 最小メジャー、マイナー最小、最高の修正プログラムのバージョン</span><span class="sxs-lookup"><span data-stu-id="7b22a-131">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="7b22a-132">*HighestMinor*: 主要な最小のバージョン、最高のマイナー、最上位の修正プログラム</span><span class="sxs-lookup"><span data-stu-id="7b22a-132">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="7b22a-133">*最も高い*(パラメーターなしで更新プログラム パッケージの既定): 最上位バージョン</span><span class="sxs-lookup"><span data-stu-id="7b22a-133">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="7b22a-134">使用して、既定値を設定することができます、 [ `dependencyVersion` ](../Schema/nuget-config-file.md#config-section)での設定、`Nuget.Config`ファイル。</span><span class="sxs-lookup"><span data-stu-id="7b22a-134">You can set the default value using the [`dependencyVersion`](../Schema/nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="7b22a-135">WhatIf</span><span class="sxs-lookup"><span data-stu-id="7b22a-135">WhatIf</span></span> | <span data-ttu-id="7b22a-136">実際には、同期を実行せず、コマンドを実行している場合にどうなるかを示します。</span><span class="sxs-lookup"><span data-stu-id="7b22a-136">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="7b22a-137">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="7b22a-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7b22a-138">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="7b22a-138">Common Parameters</span></span>

<span data-ttu-id="7b22a-139">`Sync-Package`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="7b22a-139">`Sync-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7b22a-140">例</span><span class="sxs-lookup"><span data-stu-id="7b22a-140">Examples</span></span>

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
