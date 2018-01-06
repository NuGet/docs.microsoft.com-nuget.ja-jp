---
title: "NuGet パッケージの PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 42476008-64b3-480e-a966-98b2fa38b681
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで Get-package PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、Get-package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 632936fe4dd9736f7c3740a2f763173dc725424a
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="0024a-104">Get-package (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="0024a-104">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="0024a-105">*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。一般的な PowerShell Get-package コマンドは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*</span><span class="sxs-lookup"><span data-stu-id="0024a-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="0024a-106">ローカル リポジトリにインストールされているパッケージの一覧を取得、-listavailable スイッチで使用する場合は、パッケージ ソースから使用可能なパッケージを一覧表示または更新スイッチを使用すると、利用可能な更新を一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="0024a-106">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="0024a-107">構文</span><span class="sxs-lookup"><span data-stu-id="0024a-107">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="0024a-108">パラメーターなしで`Get-Package`既定のプロジェクトにインストールされているパッケージの一覧を表示します。</span><span class="sxs-lookup"><span data-stu-id="0024a-108">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="0024a-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="0024a-109">Parameters</span></span>

| <span data-ttu-id="0024a-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="0024a-110">Parameter</span></span> | <span data-ttu-id="0024a-111">説明</span><span class="sxs-lookup"><span data-stu-id="0024a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0024a-112">ソース</span><span class="sxs-lookup"><span data-stu-id="0024a-112">Source</span></span> | <span data-ttu-id="0024a-113">パッケージの URL またはフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="0024a-113">The URL or folder path for the package .</span></span> <span data-ttu-id="0024a-114">ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="0024a-114">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="0024a-115">省略した場合、`Get-Package`現在選択されているパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="0024a-115">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="0024a-116">-Listavailable で使用する場合は、nuget.org を既定値です。</span><span class="sxs-lookup"><span data-stu-id="0024a-116">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="0024a-117">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="0024a-117">ListAvailable</span></span> | <span data-ttu-id="0024a-118">既定で nuget.org、パッケージ ソースから使用可能なパッケージを一覧表示します。-PageSize や最初が指定されていない限り、既定値は 50 のパッケージを示しています。</span><span class="sxs-lookup"><span data-stu-id="0024a-118">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="0024a-119">更新</span><span class="sxs-lookup"><span data-stu-id="0024a-119">Updates</span></span> | <span data-ttu-id="0024a-120">パッケージ ソースで更新が提供されているパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="0024a-120">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="0024a-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="0024a-121">ProjectName</span></span> | <span data-ttu-id="0024a-122">インストールされているパッケージの取得元のプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="0024a-122">The project from which to get installed packages.</span></span> <span data-ttu-id="0024a-123">省略した場合、ソリューション全体に対してプロジェクトがインストールを返します。</span><span class="sxs-lookup"><span data-stu-id="0024a-123">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="0024a-124">フィルター</span><span class="sxs-lookup"><span data-stu-id="0024a-124">Filter</span></span> | <span data-ttu-id="0024a-125">パッケージ ID、説明、およびタグを適用して、パッケージの一覧を絞り込むためのフィルター文字列。</span><span class="sxs-lookup"><span data-stu-id="0024a-125">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="0024a-126">First</span><span class="sxs-lookup"><span data-stu-id="0024a-126">First</span></span> | <span data-ttu-id="0024a-127">リストの先頭から返されるパッケージの数。</span><span class="sxs-lookup"><span data-stu-id="0024a-127">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="0024a-128">指定しない場合、既定値は 50 です。</span><span class="sxs-lookup"><span data-stu-id="0024a-128">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="0024a-129">Skip</span><span class="sxs-lookup"><span data-stu-id="0024a-129">Skip</span></span> | <span data-ttu-id="0024a-130">最初の省略&lt;int&gt;表示される一覧からパッケージです。</span><span class="sxs-lookup"><span data-stu-id="0024a-130">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="0024a-131">AllVersions</span><span class="sxs-lookup"><span data-stu-id="0024a-131">AllVersions</span></span> | <span data-ttu-id="0024a-132">最新バージョンのみではなく、各パッケージのすべての利用可能なバージョンを表示します。</span><span class="sxs-lookup"><span data-stu-id="0024a-132">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="0024a-133">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="0024a-133">IncludePrerelease</span></span> | <span data-ttu-id="0024a-134">結果にリリース前のパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="0024a-134">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="0024a-135">PageSize</span><span class="sxs-lookup"><span data-stu-id="0024a-135">PageSize</span></span> | <span data-ttu-id="0024a-136">*(3.0 +)* -Listavailable と共に使用 (必須)、パッケージの数を続行するためのプロンプトを許可する前に一覧表示するときにします。</span><span class="sxs-lookup"><span data-stu-id="0024a-136">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="0024a-137">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="0024a-137">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="0024a-138">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="0024a-138">Common Parameters</span></span>

<span data-ttu-id="0024a-139">`Get-Package`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="0024a-139">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="0024a-140">使用例</span><span class="sxs-lookup"><span data-stu-id="0024a-140">Examples</span></span>

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

