---
title: NuGet Get-プロジェクト PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの GetProject PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 3343952535c2d3c822f5cac24cb30c8f5bfa5be3
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384621"
---
# <a name="get-project-package-manager-console-in-visual-studio"></a><span data-ttu-id="f027a-103">Get-Project (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="f027a-103">Get-Project (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f027a-104">*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="f027a-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="f027a-105">既定のプロジェクトまたは指定されたプロジェクトに関する情報を表示します。</span><span class="sxs-lookup"><span data-stu-id="f027a-105">Displays information about the default or specified project.</span></span> <span data-ttu-id="f027a-106">`Get-Project` は、プロジェクトの Visual Studio DTE (開発ツール環境) オブジェクトに対して明示的にを返します。</span><span class="sxs-lookup"><span data-stu-id="f027a-106">`Get-Project` specifically returns a referent to the Visual Studio DTE (Development Tools Environment) object for the project.</span></span>

## <a name="syntax"></a><span data-ttu-id="f027a-107">構文</span><span class="sxs-lookup"><span data-stu-id="f027a-107">Syntax</span></span>

```ps
Get-Project [[-Name] <string>] [-All] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="f027a-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f027a-108">Parameters</span></span>

| <span data-ttu-id="f027a-109">パラメータ</span><span class="sxs-lookup"><span data-stu-id="f027a-109">Parameter</span></span> | <span data-ttu-id="f027a-110">説明</span><span class="sxs-lookup"><span data-stu-id="f027a-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f027a-111">[名前]</span><span class="sxs-lookup"><span data-stu-id="f027a-111">Name</span></span> | <span data-ttu-id="f027a-112">既定では、パッケージ マネージャー コンソールで選択されている既定のプロジェクトを表示するには、プロジェクトに指定します。</span><span class="sxs-lookup"><span data-stu-id="f027a-112">Specifies the project to display, defaulting to the default project selected in the Package Manager Console.</span></span> <span data-ttu-id="f027a-113">-Name スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="f027a-113">The -Name switch is itself optional.</span></span> |
| <span data-ttu-id="f027a-114">すべての</span><span class="sxs-lookup"><span data-stu-id="f027a-114">All</span></span> | <span data-ttu-id="f027a-115">ソリューション内のすべてのプロジェクトの情報を表示します。プロジェクトの順序は決定的ではありません。</span><span class="sxs-lookup"><span data-stu-id="f027a-115">Displays information for every project in the solution; the order of projects is not deterministic.</span></span> |

<span data-ttu-id="f027a-116">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="f027a-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f027a-117">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="f027a-117">Common Parameters</span></span>

<span data-ttu-id="f027a-118">`Get-Project` 次のサポート[一般的な PowerShell パラメーター](https://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="f027a-118">`Get-Project` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f027a-119">使用例</span><span class="sxs-lookup"><span data-stu-id="f027a-119">Examples</span></span>

```ps
# Displays information for the default project
Get-Project

# Displays information for a project in the solution
Get-Project MyProjectName

    # Displays information for all projects in the solution
Get-Project -All
```