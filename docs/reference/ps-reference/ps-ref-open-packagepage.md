---
title: NuGet Open-PackagePage PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Open-PackagePage PowerShell コマンドのリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d34a91007197f8004e4923deedb1cdb26d662d53
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780406"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="7a9d7-103">Open-PackagePage (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="7a9d7-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7a9d7-104">*3.0 以降では非推奨となりました。Windows の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="7a9d7-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="7a9d7-105">指定されたパッケージのプロジェクト、ライセンス、またはレポート不正使用の URL を使用して、既定のブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="7a9d7-106">構文</span><span class="sxs-lookup"><span data-stu-id="7a9d7-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="7a9d7-107">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7a9d7-107">Parameters</span></span>

| <span data-ttu-id="7a9d7-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7a9d7-108">Parameter</span></span> | <span data-ttu-id="7a9d7-109">説明</span><span class="sxs-lookup"><span data-stu-id="7a9d7-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a9d7-110">Id</span><span class="sxs-lookup"><span data-stu-id="7a9d7-110">Id</span></span> | <span data-ttu-id="7a9d7-111">目的のパッケージのパッケージ ID。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-111">The package ID of the desired package.</span></span> <span data-ttu-id="7a9d7-112">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7a9d7-113">Version</span><span class="sxs-lookup"><span data-stu-id="7a9d7-113">Version</span></span> | <span data-ttu-id="7a9d7-114">パッケージのバージョン。既定では、最新のバージョンになります。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="7a9d7-115">source</span><span class="sxs-lookup"><span data-stu-id="7a9d7-115">Source</span></span> | <span data-ttu-id="7a9d7-116">パッケージソース。ソースドロップダウンで選択したソースを既定として選択します。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="7a9d7-117">ライセンス</span><span class="sxs-lookup"><span data-stu-id="7a9d7-117">License</span></span> | <span data-ttu-id="7a9d7-118">ブラウザーでパッケージのライセンス URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="7a9d7-119">-License も-ReportAbuse も指定されていない場合、ブラウザーはパッケージのプロジェクト URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="7a9d7-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="7a9d7-120">ReportAbuse</span></span> | <span data-ttu-id="7a9d7-121">パッケージの不正行為の URL をブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="7a9d7-122">-License も-ReportAbuse も指定されていない場合、ブラウザーはパッケージのプロジェクト URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="7a9d7-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="7a9d7-123">PassThru</span></span> | <span data-ttu-id="7a9d7-124">URL が表示されます。ブラウザーを開くことを抑制するには、-WhatIf と共に使用します。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="7a9d7-125">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7a9d7-126">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="7a9d7-126">Common Parameters</span></span>

<span data-ttu-id="7a9d7-127">`Open-PackagePage` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="7a9d7-127">`Open-PackagePage` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7a9d7-128">使用例</span><span class="sxs-lookup"><span data-stu-id="7a9d7-128">Examples</span></span>

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