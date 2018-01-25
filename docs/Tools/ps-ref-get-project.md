---
title: "プロジェクトの NuGet Get PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで GetProject PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、Get プロジェクト"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cb98498d6cc6245c9e22b00eada097b816160aea
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="1a931-104">Get プロジェクト (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="1a931-104">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="1a931-105">*内でのみ使用可能な[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="1a931-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="1a931-106">既定値または指定したプロジェクトについての情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="1a931-106">Displays information about the default or specified project.</span></span> <span data-ttu-id="1a931-107">`Get-Project`具体的には、プロジェクトの Visual Studio DTE (Development Tools Environment) のオブジェクトに参照を返します。</span><span class="sxs-lookup"><span data-stu-id="1a931-107">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="1a931-108">構文</span><span class="sxs-lookup"><span data-stu-id="1a931-108">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="1a931-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="1a931-109">Parameters</span></span>

| <span data-ttu-id="1a931-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="1a931-110">Parameter</span></span> | <span data-ttu-id="1a931-111">説明</span><span class="sxs-lookup"><span data-stu-id="1a931-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1a931-112">name</span><span class="sxs-lookup"><span data-stu-id="1a931-112">Name</span></span> | <span data-ttu-id="1a931-113">既定のパッケージ マネージャー コンソールで選択された既定のプロジェクトを表示するには、プロジェクトに指定します。</span><span class="sxs-lookup"><span data-stu-id="1a931-113">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="1a931-114">-Name スイッチは、それ自体の省略可能です。</span><span class="sxs-lookup"><span data-stu-id="1a931-114">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="1a931-115">すべて</span><span class="sxs-lookup"><span data-stu-id="1a931-115">All</span></span> | <span data-ttu-id="1a931-116">このソリューションでのすべてのプロジェクトの情報を表示プロジェクトの順序は確定的ではありません。</span><span class="sxs-lookup"><span data-stu-id="1a931-116">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="1a931-117">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="1a931-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="1a931-118">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="1a931-118">Common Parameters</span></span>

<span data-ttu-id="1a931-119">`Get-Project`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="1a931-119">`Get-Project` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="1a931-120">使用例</span><span class="sxs-lookup"><span data-stu-id="1a931-120">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```