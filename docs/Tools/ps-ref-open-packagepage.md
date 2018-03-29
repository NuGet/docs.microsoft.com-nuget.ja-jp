---
title: NuGet 開く PackagePage PowerShell リファレンス |Microsoft ドキュメント
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Visual Studio で NuGet パッケージ マネージャー コンソールで開く PackagePage PowerShell コマンドのリファレンスです。
keywords: NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、開く PackagePage
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 5e0955e58daacf381666c676c8fcf22c698e9db6
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="open-packagepage-package-manager-console-in-visual-studio"></a><span data-ttu-id="c6360-104">開く PackagePage (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="c6360-104">Open-PackagePage (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c6360-105">*3.0 +; で使用されていません内でのみ使用可能な[NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="c6360-105">*Deprecated in 3.0+; available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="c6360-106">プロジェクト、ライセンス、または指定したパッケージの不正使用を URL のレポートで既定のブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="c6360-106">Launches the default browser with the project, license, or report abuse URL for the specified package.</span></span>

## <a name="syntax"></a><span data-ttu-id="c6360-107">構文</span><span class="sxs-lookup"><span data-stu-id="c6360-107">Syntax</span></span>

```ps
Open-PackagePage [-Id] <string> [-Version] [-Source] [-License] [-ReportAbuse]
    [-PassThru] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="c6360-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c6360-108">Parameters</span></span>

| <span data-ttu-id="c6360-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c6360-109">Parameter</span></span> | <span data-ttu-id="c6360-110">説明</span><span class="sxs-lookup"><span data-stu-id="c6360-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c6360-111">ID</span><span class="sxs-lookup"><span data-stu-id="c6360-111">Id</span></span> | <span data-ttu-id="c6360-112">目的のパッケージのパッケージ ID。</span><span class="sxs-lookup"><span data-stu-id="c6360-112">The package ID of the desired package.</span></span> <span data-ttu-id="c6360-113">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="c6360-113">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c6360-114">Version</span><span class="sxs-lookup"><span data-stu-id="c6360-114">Version</span></span> | <span data-ttu-id="c6360-115">既定の最新バージョンに、パッケージのバージョン。</span><span class="sxs-lookup"><span data-stu-id="c6360-115">The version of the package, defaulting to the latest version.</span></span> |
| <span data-ttu-id="c6360-116">ソース</span><span class="sxs-lookup"><span data-stu-id="c6360-116">Source</span></span> | <span data-ttu-id="c6360-117">パッケージ ソースは、ソース ドロップダウンで選択したソースを既定とします。</span><span class="sxs-lookup"><span data-stu-id="c6360-117">The package source, defaulting to the selected source in the source drop-down.</span></span> |
| <span data-ttu-id="c6360-118">ライセンス</span><span class="sxs-lookup"><span data-stu-id="c6360-118">License</span></span> | <span data-ttu-id="c6360-119">パッケージのライセンス URL をブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="c6360-119">Opens the browser to the package's License URL.</span></span> <span data-ttu-id="c6360-120">-ライセンスも - ReportAbuse が指定されている、パッケージのプロジェクトの URL をブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="c6360-120">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="c6360-121">ReportAbuse</span><span class="sxs-lookup"><span data-stu-id="c6360-121">ReportAbuse</span></span> | <span data-ttu-id="c6360-122">パッケージの不正使用を URL にレポートをブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="c6360-122">Opens the browser to the package's Report Abuse URL.</span></span> <span data-ttu-id="c6360-123">-ライセンスも - ReportAbuse が指定されている、パッケージのプロジェクトの URL をブラウザーが開きます。</span><span class="sxs-lookup"><span data-stu-id="c6360-123">If neither -License nor -ReportAbuse is specified, the browser opens the package's Project URL.</span></span> |
| <span data-ttu-id="c6360-124">PassThru</span><span class="sxs-lookup"><span data-stu-id="c6360-124">PassThru</span></span> | <span data-ttu-id="c6360-125">URL を表示します。-whatif を使用して、抑制する状況、ブラウザーを起動します。</span><span class="sxs-lookup"><span data-stu-id="c6360-125">Displays the URL; use with -WhatIf to suppress opening the browser.</span></span> |

<span data-ttu-id="c6360-126">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="c6360-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c6360-127">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="c6360-127">Common Parameters</span></span>

<span data-ttu-id="c6360-128">`Open-PackagePage` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="c6360-128">`Open-PackagePage` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c6360-129">使用例</span><span class="sxs-lookup"><span data-stu-id="c6360-129">Examples</span></span>

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