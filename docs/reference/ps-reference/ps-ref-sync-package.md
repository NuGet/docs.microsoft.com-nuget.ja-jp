---
title: NuGet 同期-パッケージ PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの Sync-Package PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 12a3d5f32056539a75da9e17b15d67e72a8a42c2
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384904"
---
# <a name="sync-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f4467-103">Sync-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="f4467-103">Sync-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f4467-104">*バージョン 3.0 +;Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="f4467-104">*Version 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f4467-105">指定された (または既定の) プロジェクトからインストールされているパッケージのバージョンを取得し、そのバージョンをソリューション内の残りのプロジェクトと同期します。</span><span class="sxs-lookup"><span data-stu-id="f4467-105">Gets the version of installed package from specified (or default) project and synchronizes the version to the rest of projects in the solution.</span></span>

## <a name="syntax"></a><span data-ttu-id="f4467-106">構文</span><span class="sxs-lookup"><span data-stu-id="f4467-106">Syntax</span></span>

```ps
Sync-Package [-Id] <string> [-IgnoreDependencies] [-ProjectName <string>] [[-Version] <string>]
    [[-Source] <string>] [-IncludePrerelease] [-FileConflictAction] [-DependencyVersion]
    [-WhatIf] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f4467-107">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f4467-107">Parameters</span></span>

| <span data-ttu-id="f4467-108">パラメータ</span><span class="sxs-lookup"><span data-stu-id="f4467-108">Parameter</span></span> | <span data-ttu-id="f4467-109">説明</span><span class="sxs-lookup"><span data-stu-id="f4467-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f4467-110">ID</span><span class="sxs-lookup"><span data-stu-id="f4467-110">Id</span></span> | <span data-ttu-id="f4467-111">必要同期するパッケージの識別子。-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="f4467-111">(Required) The identifier of the package to sync. The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f4467-112">IgnoreDependencies</span><span class="sxs-lookup"><span data-stu-id="f4467-112">IgnoreDependencies</span></span> | <span data-ttu-id="f4467-113">依存関係ではなく、このパッケージのみをインストールします。</span><span class="sxs-lookup"><span data-stu-id="f4467-113">Install only this package and not its dependencies.</span></span> |
| <span data-ttu-id="f4467-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f4467-114">ProjectName</span></span> | <span data-ttu-id="f4467-115">パッケージの同期元のプロジェクト。既定のプロジェクトが既定のプロジェクトになります。</span><span class="sxs-lookup"><span data-stu-id="f4467-115">The project to sync the package from, defaulting to the default  project.</span></span> |
| <span data-ttu-id="f4467-116">Version</span><span class="sxs-lookup"><span data-stu-id="f4467-116">Version</span></span> | <span data-ttu-id="f4467-117">同期するパッケージのバージョンです。既定では、現在インストールされているバージョンが対象となります。</span><span class="sxs-lookup"><span data-stu-id="f4467-117">The version of the package to sync, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="f4467-118">Source</span><span class="sxs-lookup"><span data-stu-id="f4467-118">Source</span></span> | <span data-ttu-id="f4467-119">検索するパッケージソースの URL またはフォルダーパス。</span><span class="sxs-lookup"><span data-stu-id="f4467-119">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="f4467-120">ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="f4467-120">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="f4467-121">省略した場合、`Sync-Package` は現在選択されているパッケージソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="f4467-121">If omitted, `Sync-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="f4467-122">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="f4467-122">IncludePrerelease</span></span> | <span data-ttu-id="f4467-123">には、同期のプレリリースパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="f4467-123">Includes prerelease packages in the sync.</span></span> |
| <span data-ttu-id="f4467-124">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="f4467-124">FileConflictAction</span></span> | <span data-ttu-id="f4467-125">プロジェクトによって参照される既存のファイルを上書きまたは無視するように要求されたときに実行するアクション。</span><span class="sxs-lookup"><span data-stu-id="f4467-125">The action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="f4467-126">指定できる値は *、Overwrite、Ignore、None、OverwriteAll*、 *(3.0 +)* *ignoreall*です。</span><span class="sxs-lookup"><span data-stu-id="f4467-126">Possible values are *Overwrite, Ignore, None, OverwriteAll*, and *(3.0+)* *IgnoreAll*.</span></span> |
| <span data-ttu-id="f4467-127">DependencyVersion</span><span class="sxs-lookup"><span data-stu-id="f4467-127">DependencyVersion</span></span> | <span data-ttu-id="f4467-128">使用する依存関係パッケージのバージョン。次のいずれかになります。</span><span class="sxs-lookup"><span data-stu-id="f4467-128">The version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="f4467-129">*最低*(既定): 最も低いバージョンです。</span><span class="sxs-lookup"><span data-stu-id="f4467-129">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="f4467-130">*HighestPatch*: 最も低いメジャー、最低のマイナー、最高のパッチを持つバージョン</span><span class="sxs-lookup"><span data-stu-id="f4467-130">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="f4467-131">*HighestMinor*: 最上位のメジャー、最高のマイナー、最高の修正プログラムが適用されたバージョン</span><span class="sxs-lookup"><span data-stu-id="f4467-131">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="f4467-132">*最高*(更新プログラム-パラメーターなしのパッケージ): 最高バージョン</span><span class="sxs-lookup"><span data-stu-id="f4467-132">*Highest* (default for Update-Package with no parameters): the highest version</span></span></li></ul><span data-ttu-id="f4467-133">`Nuget.Config` ファイルの[`dependencyVersion`](../nuget-config-file.md#config-section)設定を使用して、既定値を設定できます。</span><span class="sxs-lookup"><span data-stu-id="f4467-133">You can set the default value using the [`dependencyVersion`](../nuget-config-file.md#config-section) setting in the `Nuget.Config` file.</span></span> |
| <span data-ttu-id="f4467-134">Whatif</span><span class="sxs-lookup"><span data-stu-id="f4467-134">WhatIf</span></span> | <span data-ttu-id="f4467-135">実際に同期を実行せずにコマンドを実行した場合の動作を示します。</span><span class="sxs-lookup"><span data-stu-id="f4467-135">Shows what would happen when running the command without actually performing the sync.</span></span> |

<span data-ttu-id="f4467-136">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="f4467-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f4467-137">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="f4467-137">Common Parameters</span></span>

<span data-ttu-id="f4467-138">`Sync-Package` 次のサポート[一般的な PowerShell パラメーター](https://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="f4467-138">`Sync-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f4467-139">使用例</span><span class="sxs-lookup"><span data-stu-id="f4467-139">Examples</span></span>

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
