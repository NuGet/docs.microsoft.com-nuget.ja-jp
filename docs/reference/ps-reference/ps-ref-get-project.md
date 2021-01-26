---
title: NuGet Get-Project PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの GetProject PowerShell コマンドのリファレンス。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 16b3ffc0a375b8027c615020243a7289520715f8
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777470"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="937d0-103">Get-Project (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="937d0-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="937d0-104">*Windows の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="937d0-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="937d0-105">既定のプロジェクトまたは指定されたプロジェクトに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="937d0-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="937d0-106">`Get-Project` 具体的には、プロジェクトの Visual Studio DTE (開発ツール環境) オブジェクトへの指示を返します。</span><span class="sxs-lookup"><span data-stu-id="937d0-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="937d0-107">構文</span><span class="sxs-lookup"><span data-stu-id="937d0-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="937d0-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="937d0-108">Parameters</span></span>

| <span data-ttu-id="937d0-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="937d0-109">Parameter</span></span> | <span data-ttu-id="937d0-110">説明</span><span class="sxs-lookup"><span data-stu-id="937d0-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="937d0-111">名前</span><span class="sxs-lookup"><span data-stu-id="937d0-111">Name</span></span> | <span data-ttu-id="937d0-112">表示するプロジェクトを指定します。既定では、パッケージマネージャーコンソールで選択されている既定のプロジェクトが対象となります。</span><span class="sxs-lookup"><span data-stu-id="937d0-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="937d0-113">-Name スイッチ自体はオプションです。</span><span class="sxs-lookup"><span data-stu-id="937d0-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="937d0-114">すべて</span><span class="sxs-lookup"><span data-stu-id="937d0-114">All</span></span> | <span data-ttu-id="937d0-115">ソリューション内のすべてのプロジェクトの情報を表示します。プロジェクトの順序は決定的ではありません。</span><span class="sxs-lookup"><span data-stu-id="937d0-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="937d0-116">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="937d0-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="937d0-117">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="937d0-117">Common Parameters</span></span>

<span data-ttu-id="937d0-118">`Get-Project` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="937d0-118">`Get-Project` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="937d0-119">使用例</span><span class="sxs-lookup"><span data-stu-id="937d0-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```