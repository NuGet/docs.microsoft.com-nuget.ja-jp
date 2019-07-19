---
title: NuGet Open-PackagePage PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで開く-PackagePage PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 0237c23d81000a1d58264cc0ab48c73d819d0e5a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327379"
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="aeff6-103">Open-PackagePage (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="aeff6-103">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="aeff6-104">*3.0 以降では非推奨となりました。Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="aeff6-104">*Deprecated in 3.0+; available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="aeff6-105">指定されたパッケージのプロジェクト、ライセンス、またはレポート不正使用の URL を使用して、既定のブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="aeff6-105">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="aeff6-106">構文</span><span class="sxs-lookup"><span data-stu-id="aeff6-106">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="aeff6-107">パラメーター</span><span class="sxs-lookup"><span data-stu-id="aeff6-107">Parameters</span></span>

| <span data-ttu-id="aeff6-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="aeff6-108">Parameter</span></span> | <span data-ttu-id="aeff6-109">説明</span><span class="sxs-lookup"><span data-stu-id="aeff6-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="aeff6-110">ID</span><span class="sxs-lookup"><span data-stu-id="aeff6-110">Id</span></span> | <span data-ttu-id="aeff6-111">目的のパッケージのパッケージ ID。</span><span class="sxs-lookup"><span data-stu-id="aeff6-111">The package ID of the desired package.</span></span> <span data-ttu-id="aeff6-112">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="aeff6-112">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="aeff6-113">Version</span><span class="sxs-lookup"><span data-stu-id="aeff6-113">Version</span></span> | <span data-ttu-id="aeff6-114">パッケージのバージョン。既定では、最新のバージョンになります。</span><span class="sxs-lookup"><span data-stu-id="aeff6-114">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="aeff6-115">Source</span><span class="sxs-lookup"><span data-stu-id="aeff6-115">Source</span></span> | <span data-ttu-id="aeff6-116">パッケージソース。ソースドロップダウンで選択したソースを既定として選択します。</span><span class="sxs-lookup"><span data-stu-id="aeff6-116">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="aeff6-117">License</span><span class="sxs-lookup"><span data-stu-id="aeff6-117">License</span></span> | <span data-ttu-id="aeff6-118">ブラウザーでパッケージのライセンス URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="aeff6-118">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="aeff6-119">-License も-ReportAbuse も指定されていない場合、ブラウザーはパッケージのプロジェクト URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="aeff6-119">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="aeff6-120">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="aeff6-120">ReportAbuse</span></span> | <span data-ttu-id="aeff6-121">パッケージの不正行為の URL をブラウザーで開きます。</span><span class="sxs-lookup"><span data-stu-id="aeff6-121">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="aeff6-122">-License も-ReportAbuse も指定されていない場合、ブラウザーはパッケージのプロジェクト URL を開きます。</span><span class="sxs-lookup"><span data-stu-id="aeff6-122">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="aeff6-123">PassThru</span><span class="sxs-lookup"><span data-stu-id="aeff6-123">PassThru</span></span> | <span data-ttu-id="aeff6-124">URL が表示されます。ブラウザーを開くことを抑制するには、-WhatIf と共に使用します。</span><span class="sxs-lookup"><span data-stu-id="aeff6-124">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="aeff6-125">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="aeff6-125">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="aeff6-126">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="aeff6-126">Common Parameters</span></span>

<span data-ttu-id="aeff6-127">`Open-PackagePage`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。</span><span class="sxs-lookup"><span data-stu-id="aeff6-127">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="aeff6-128">使用例</span><span class="sxs-lookup"><span data-stu-id="aeff6-128">Examples</span></span>

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