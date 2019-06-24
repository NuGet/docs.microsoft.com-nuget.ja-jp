---
title: プロジェクトの NuGet Get PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで GetProject PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 849261711fafcadbab38bf6fe99340c4b79e1e21
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550438"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="a5186-103">Get-Project (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="a5186-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a5186-104">*内でのみ使用可能な[NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="a5186-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="a5186-105">既定値または指定されたプロジェクトについての情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="a5186-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="a5186-106">`Get-Project` 具体的には、プロジェクトの Visual Studio DTE (Development Tools Environment) のオブジェクトに参照を返します。</span><span class="sxs-lookup"><span data-stu-id="a5186-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="a5186-107">構文</span><span class="sxs-lookup"><span data-stu-id="a5186-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a5186-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="a5186-108">Parameters</span></span>

| <span data-ttu-id="a5186-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="a5186-109">Parameter</span></span> | <span data-ttu-id="a5186-110">説明</span><span class="sxs-lookup"><span data-stu-id="a5186-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5186-111">Name</span><span class="sxs-lookup"><span data-stu-id="a5186-111">Name</span></span> | <span data-ttu-id="a5186-112">既定では、パッケージ マネージャー コンソールで選択されている既定のプロジェクトを表示するには、プロジェクトに指定します。</span><span class="sxs-lookup"><span data-stu-id="a5186-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="a5186-113">-Name スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="a5186-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="a5186-114">All</span><span class="sxs-lookup"><span data-stu-id="a5186-114">All</span></span> | <span data-ttu-id="a5186-115">このソリューションですべてのプロジェクトの情報を表示します。プロジェクトの順序は決定論的ではありません。</span><span class="sxs-lookup"><span data-stu-id="a5186-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="a5186-116">これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="a5186-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a5186-117">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="a5186-117">Common Parameters</span></span>

<span data-ttu-id="a5186-118">`Get-Project` は次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216) をサポートしています: Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable</span><span class="sxs-lookup"><span data-stu-id="a5186-118">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a5186-119">使用例</span><span class="sxs-lookup"><span data-stu-id="a5186-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```