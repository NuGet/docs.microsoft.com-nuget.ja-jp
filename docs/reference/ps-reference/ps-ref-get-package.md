---
title: NuGet Get-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの Get Package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 431e5f292f069ad5eb0c9f7f511d6b06810c8760
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327349"
---
# <a name="get-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7c3ab-103">Get-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="7c3ab-103">Get-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7c3ab-104">*このトピックでは、Windows 上の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内のコマンドについて説明します。汎用 PowerShell のパッケージの取得コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="7c3ab-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Get-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="7c3ab-105">ローカルリポジトリにインストールされているパッケージの一覧を取得し、-ListAvailable スイッチで使用した場合はパッケージソースから利用可能なパッケージを一覧表示します。または、-Update スイッチで使用した場合は、使用可能な更新プログラムを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-105">Retrieves the list of packages installed in the local repository, lists packages available from a package source when used with the -ListAvailable switch, or lists available updates when used with the -Update switch.</span></span>

## <a name="syntax"></a><span data-ttu-id="7c3ab-106">構文</span><span class="sxs-lookup"><span data-stu-id="7c3ab-106">Syntax</span></span>

```ps
Get-Package -Source <string> [-ListAvailable] [-Updates] [-ProjectName <string>]
    [-Filter <string>] [-First <int>] [-Skip <int>] [-AllVersions] [-IncludePrerelease]
    [-PageSize] [<CommonParameters>]
```

<span data-ttu-id="7c3ab-107">パラメーターを使用し`Get-Package`ない場合は、既定のプロジェクトにインストールされているパッケージの一覧が表示されます。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-107">With no parameters, `Get-Package` displays the list of packages installed in the default project.</span></span>

## <a name="parameters"></a><span data-ttu-id="7c3ab-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7c3ab-108">Parameters</span></span>

| <span data-ttu-id="7c3ab-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7c3ab-109">Parameter</span></span> | <span data-ttu-id="7c3ab-110">説明</span><span class="sxs-lookup"><span data-stu-id="7c3ab-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c3ab-111">Source</span><span class="sxs-lookup"><span data-stu-id="7c3ab-111">Source</span></span> | <span data-ttu-id="7c3ab-112">パッケージの URL またはフォルダーパス。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-112">The URL or folder path for the package .</span></span> <span data-ttu-id="7c3ab-113">ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-113">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="7c3ab-114">省略した`Get-Package`場合、現在選択されているパッケージソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-114">If omitted, `Get-Package` searches the currently selected package source.</span></span> <span data-ttu-id="7c3ab-115">-ListAvailable と共に使用すると、既定で nuget.org に設定されます。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-115">When used with -ListAvailable, defaults to nuget.org.</span></span> |
| <span data-ttu-id="7c3ab-116">ListAvailable</span><span class="sxs-lookup"><span data-stu-id="7c3ab-116">ListAvailable</span></span> | <span data-ttu-id="7c3ab-117">パッケージソースから利用可能なパッケージを一覧表示し、既定で nuget.org を使用します。-PageSize と/または-First が指定されていない限り、既定の50パッケージが表示されます。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-117">Lists packages available from a package source, defaulting to nuget.org. Shows a default of 50 packages unless -PageSize and/or -First are specified.</span></span> |
| <span data-ttu-id="7c3ab-118">Updates</span><span class="sxs-lookup"><span data-stu-id="7c3ab-118">Updates</span></span> | <span data-ttu-id="7c3ab-119">パッケージソースから利用可能な更新プログラムが含まれているパッケージを一覧表示します。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-119">Lists packages that have an update available from the package source.</span></span> |
| <span data-ttu-id="7c3ab-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="7c3ab-120">ProjectName</span></span> | <span data-ttu-id="7c3ab-121">インストールされているパッケージの取得元となるプロジェクト。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-121">The project from which to get installed packages.</span></span> <span data-ttu-id="7c3ab-122">省略した場合、ソリューション全体にインストールされているプロジェクトを返します。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-122">If omitted, returns installed projects for the entire solution.</span></span> |
| <span data-ttu-id="7c3ab-123">Filter</span><span class="sxs-lookup"><span data-stu-id="7c3ab-123">Filter</span></span> | <span data-ttu-id="7c3ab-124">パッケージ ID、説明、およびタグに適用してパッケージの一覧を絞り込むために使用されるフィルター文字列。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-124">A filter string used to narrow down the list of packages by applying it to the package ID, description, and tags.</span></span> |
| <span data-ttu-id="7c3ab-125">First</span><span class="sxs-lookup"><span data-stu-id="7c3ab-125">First</span></span> | <span data-ttu-id="7c3ab-126">リストの先頭から取得するパッケージの数。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-126">The number of packages to return from the beginning of the list.</span></span> <span data-ttu-id="7c3ab-127">指定しない場合、の既定値は50です。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-127">If not specified, defaults to 50.</span></span> |
| <span data-ttu-id="7c3ab-128">Skip</span><span class="sxs-lookup"><span data-stu-id="7c3ab-128">Skip</span></span> | <span data-ttu-id="7c3ab-129">表示され&lt;て&gt;いる一覧から最初の int パッケージを除外します。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-129">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="7c3ab-130">AllVersions</span><span class="sxs-lookup"><span data-stu-id="7c3ab-130">AllVersions</span></span> | <span data-ttu-id="7c3ab-131">最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンを表示します。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-131">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="7c3ab-132">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="7c3ab-132">IncludePrerelease</span></span> | <span data-ttu-id="7c3ab-133">結果にプレリリースパッケージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-133">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="7c3ab-134">PageSize</span><span class="sxs-lookup"><span data-stu-id="7c3ab-134">PageSize</span></span> | <span data-ttu-id="7c3ab-135">*(3.0 以降)* -ListAvailable (必須) と共に使用する場合は、続行するように求めるメッセージを表示する前に、一覧表示するパッケージの数。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-135">*(3.0+)* When used with -ListAvailable (required), the number of packages to list before giving a prompt to continue.</span></span> |

<span data-ttu-id="7c3ab-136">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-136">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7c3ab-137">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="7c3ab-137">Common Parameters</span></span>

<span data-ttu-id="7c3ab-138">`Get-Package`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。</span><span class="sxs-lookup"><span data-stu-id="7c3ab-138">`Get-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7c3ab-139">使用例</span><span class="sxs-lookup"><span data-stu-id="7c3ab-139">Examples</span></span>

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
