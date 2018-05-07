---
title: NuGet 開く PackagePage PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで開く PackagePage PowerShell コマンドのリファレンスです。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: df4bea390105a7e3fc5d2abd476f2908d92bbcf8
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="42160-103">Open-PackagePage (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="42160-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="42160-104">*3.0 +; で使用されていません内でのみ使用可能な[NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="42160-104">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="42160-105">プロジェクト、ライセンス、または指定したパッケージの不正使用を URL のレポートで既定のブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="42160-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="42160-106">構文</span><span class="sxs-lookup"><span data-stu-id="42160-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="42160-107">パラメーター</span><span class="sxs-lookup"><span data-stu-id="42160-107">Parameters</span></span>

| <span data-ttu-id="42160-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="42160-108">Parameter</span></span> | <span data-ttu-id="42160-109">説明</span><span class="sxs-lookup"><span data-stu-id="42160-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="42160-110">ID</span><span class="sxs-lookup"><span data-stu-id="42160-110">Id</span></span> | <span data-ttu-id="42160-111">目的のパッケージのパッケージ ID。</span><span class="sxs-lookup"><span data-stu-id="42160-111">The package ID of the desired package.</span></span> <span data-ttu-id="42160-112">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="42160-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="42160-113">Version</span><span class="sxs-lookup"><span data-stu-id="42160-113">Version</span></span> | <span data-ttu-id="42160-114">既定の最新バージョンに、パッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="42160-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="42160-115">ソース</span><span class="sxs-lookup"><span data-stu-id="42160-115">Source</span></span> | <span data-ttu-id="42160-116">パッケージ ソースは、ソース ドロップダウンで選択したソースを既定とします。</span><span class="sxs-lookup"><span data-stu-id="42160-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="42160-117">ライセンス</span><span class="sxs-lookup"><span data-stu-id="42160-117">License</span></span> | <span data-ttu-id="42160-118">パッケージのライセンス URL をブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="42160-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="42160-119">-ライセンスも - ReportAbuse が指定されている、パッケージのプロジェクトの URL をブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="42160-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="42160-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="42160-120">ReportAbuse</span></span> | <span data-ttu-id="42160-121">パッケージの不正使用を URL にレポートをブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="42160-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="42160-122">-ライセンスも - ReportAbuse が指定されている、パッケージのプロジェクトの URL をブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="42160-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="42160-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="42160-123">PassThru</span></span> | <span data-ttu-id="42160-124">URL を表示します。-whatif を使用して、抑制する状況、ブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="42160-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="42160-125">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="42160-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="42160-126">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="42160-126">Common Parameters</span></span>

<span data-ttu-id="42160-127">`Open-PackagePage` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="42160-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="42160-128">使用例</span><span class="sxs-lookup"><span data-stu-id="42160-128">Examples</span></span>

```ps
# Opens a browser with the Ninject package's project page
Open-PackagePage Ninject

# Opens a browser with the Ninject package's license page
Open-PackagePage Ninject -License

# Opens a browser with the Ninject package's report abuse page  
Open-PackagePage Ninject -ReportAbuse

# Assigns the license URL to the variable, $url, without launching the browser
$url = Open-PackagePage Ninject -License -PassThru -WhatIf
```