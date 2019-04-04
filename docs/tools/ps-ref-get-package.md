---
title: NuGet Get-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで Get-package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a28b29614dfe5abdeb24438b3451d96634a120db
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551443"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="04d27-103">Get-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="04d27-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="04d27-104">*このトピックでは、内のコマンドを説明します、 [NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。汎用の Get-package の PowerShell コマンドでは、、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="04d27-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="04d27-105">ローカル リポジトリにインストールされているパッケージの一覧を取得、- ListAvailable スイッチと共に使用する場合は、パッケージ ソースから使用可能なパッケージを一覧表示または更新スイッチを使用すると、利用可能な更新を一覧表示されます。</span><span class="sxs-lookup"><span data-stu-id="04d27-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="04d27-106">構文</span><span class="sxs-lookup"><span data-stu-id="04d27-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="04d27-107">パラメーターなしで`Get-Package`既定のプロジェクトにインストールされているパッケージの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="04d27-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="04d27-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="04d27-108">Parameters</span></span>

| <span data-ttu-id="04d27-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="04d27-109">Parameter</span></span> | <span data-ttu-id="04d27-110">説明</span><span class="sxs-lookup"><span data-stu-id="04d27-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04d27-111">ソース</span><span class="sxs-lookup"><span data-stu-id="04d27-111">Source</span></span> | <span data-ttu-id="04d27-112">パッケージの URL またはフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="04d27-112">The URL or folder path for the package .</span></span> <span data-ttu-id="04d27-113">ローカル フォルダー パスには、absolute、または現在のフォルダーの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="04d27-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="04d27-114">省略した場合、`Get-Package`現在選択されているパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="04d27-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="04d27-115">-ListAvailable で使用する場合は、nuget.org に既定値です。</span><span class="sxs-lookup"><span data-stu-id="04d27-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="04d27-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="04d27-116">ListAvailable</span></span> | <span data-ttu-id="04d27-117">既定では nuget.org をパッケージ ソースから使用可能なパッケージを一覧表示します。-PageSize や最初が指定されていない場合、既定値は 50 のパッケージを示します。</span><span class="sxs-lookup"><span data-stu-id="04d27-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="04d27-118">更新</span><span class="sxs-lookup"><span data-stu-id="04d27-118">Updates</span></span> | <span data-ttu-id="04d27-119">パッケージ、パッケージ ソースから使用可能な更新プログラムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="04d27-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="04d27-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="04d27-120">ProjectName</span></span> | <span data-ttu-id="04d27-121">インストールされているパッケージの取得元のプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="04d27-121">The project from which to get installed packages.</span></span> <span data-ttu-id="04d27-122">省略した場合は、ソリューション全体のプロジェクトをインストールされている返します。</span><span class="sxs-lookup"><span data-stu-id="04d27-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="04d27-123">フィルター</span><span class="sxs-lookup"><span data-stu-id="04d27-123">Filter</span></span> | <span data-ttu-id="04d27-124">パッケージ ID、説明、およびタグに適用して、パッケージの一覧を絞り込むために使用されるフィルター文字列。</span><span class="sxs-lookup"><span data-stu-id="04d27-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="04d27-125">First</span><span class="sxs-lookup"><span data-stu-id="04d27-125">First</span></span> | <span data-ttu-id="04d27-126">リストの先頭から返されるパッケージの数。</span><span class="sxs-lookup"><span data-stu-id="04d27-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="04d27-127">指定しない場合、既定値は 50 です。</span><span class="sxs-lookup"><span data-stu-id="04d27-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="04d27-128">Skip</span><span class="sxs-lookup"><span data-stu-id="04d27-128">Skip</span></span> | <span data-ttu-id="04d27-129">最初の省略&lt;int&gt;表示された一覧からパッケージ。</span><span class="sxs-lookup"><span data-stu-id="04d27-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="04d27-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="04d27-130">AllVersions</span></span> | <span data-ttu-id="04d27-131">最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンが表示されます。</span><span class="sxs-lookup"><span data-stu-id="04d27-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="04d27-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="04d27-132">IncludePrerelease</span></span> | <span data-ttu-id="04d27-133">結果には、プレリリース パッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="04d27-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="04d27-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="04d27-134">PageSize</span></span> | <span data-ttu-id="04d27-135">*(3.0 以降)* 続行を求めるメッセージを渡す前に一覧表示する - ListAvailable (必須)、パッケージの数と使用するとします。</span><span class="sxs-lookup"><span data-stu-id="04d27-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="04d27-136">これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="04d27-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="04d27-137">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="04d27-137">Common Parameters</span></span>

<span data-ttu-id="04d27-138">`Get-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="04d27-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="04d27-139">使用例</span><span class="sxs-lookup"><span data-stu-id="04d27-139">Examples</span></span>

```ps
# Lists the packages installed in the current solution
Get-Package

# Lists the packages installed in a project
Get-Package -ProjectName MyProject

# Lists packages available in the current package source
Get-Package -ListAvailable

# Lists 30 packages at a time from the current source, and prompts to continue if more are available
Get-Package -ListAvailable -PageSize 30

# Lists packages with the Ninject keyword in the current source, up to 50
Get-Package -ListAvailable -Filter Ninject

# List all versions of packages matching the filter "jquery"
Get-Package -ListAvailable -Filter jquery -AllVersions

# Lists packages installed in the solution that have available updates
Get-Package -Updates

# Lists packages installed in a specific project that have available updates
Get-Package -Updates -ProjectName MyProject
```
