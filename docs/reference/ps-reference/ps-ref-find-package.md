---
title: NuGet Find-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Find-Package PowerShell コマンドのリファレンスです。
author: JonDouglas
ms.author: jodou
ms.date: 6/1/2017
ms.topic: reference
ms.openlocfilehash: 83d0d62bbda07d07ea1e3b58e531447e2001b680
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777506"
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="a3505-103">Find-Package (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="a3505-103">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="a3505-104">*バージョン 3.0 +;このトピックでは、Windows 上の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内のコマンドについて説明します。汎用 PowerShell Find-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="a3505-104">*Version 3.0+; this topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="a3505-105">パッケージソースから指定された ID またはキーワードを持つリモートパッケージのセットを取得します。</span><span class="sxs-lookup"><span data-stu-id="a3505-105">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="a3505-106">構文</span><span class="sxs-lookup"><span data-stu-id="a3505-106">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="a3505-107">パラメーター</span><span class="sxs-lookup"><span data-stu-id="a3505-107">Parameters</span></span>

| <span data-ttu-id="a3505-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="a3505-108">Parameter</span></span> | <span data-ttu-id="a3505-109">説明</span><span class="sxs-lookup"><span data-stu-id="a3505-109">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a3505-110">Id &lt; キーワード&gt;</span><span class="sxs-lookup"><span data-stu-id="a3505-110">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="a3505-111">必要パッケージソースの検索時に使用するキーワード。</span><span class="sxs-lookup"><span data-stu-id="a3505-111">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="a3505-112">パッケージ ID がキーワードと一致するパッケージのみを返すには、-"Exactmatch" を使用します。</span><span class="sxs-lookup"><span data-stu-id="a3505-112">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="a3505-113">キーワードが指定されていない場合 `Find-Package` は、ダウンロードによって上位20個のパッケージの一覧が返されます。または、-First で指定した数が返されます。</span><span class="sxs-lookup"><span data-stu-id="a3505-113">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="a3505-114">-Id は省略可能であり、no op であることに注意してください。</span><span class="sxs-lookup"><span data-stu-id="a3505-114">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="a3505-115">source</span><span class="sxs-lookup"><span data-stu-id="a3505-115">Source</span></span> | <span data-ttu-id="a3505-116">検索するパッケージソースの URL またはフォルダーパス。</span><span class="sxs-lookup"><span data-stu-id="a3505-116">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="a3505-117">ローカルフォルダーのパスは、絶対パスでも、現在のフォルダーを基準とした相対パスでもかまいません。</span><span class="sxs-lookup"><span data-stu-id="a3505-117">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="a3505-118">省略した場合、 `Find-Package` 現在選択されているパッケージソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="a3505-118">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="a3505-119">AllVersions</span><span class="sxs-lookup"><span data-stu-id="a3505-119">AllVersions</span></span> | <span data-ttu-id="a3505-120">最新バージョンのみではなく、各パッケージの使用可能なすべてのバージョンを表示します。</span><span class="sxs-lookup"><span data-stu-id="a3505-120">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="a3505-121">First</span><span class="sxs-lookup"><span data-stu-id="a3505-121">First</span></span> | <span data-ttu-id="a3505-122">リストの先頭から取得するパッケージの数。既定値は20です。</span><span class="sxs-lookup"><span data-stu-id="a3505-122">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="a3505-123">スキップ</span><span class="sxs-lookup"><span data-stu-id="a3505-123">Skip</span></span> | <span data-ttu-id="a3505-124">&lt; &gt; 表示されている一覧から最初の int パッケージを除外します。</span><span class="sxs-lookup"><span data-stu-id="a3505-124">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="a3505-125">IncludePrerelease リリース</span><span class="sxs-lookup"><span data-stu-id="a3505-125">IncludePrerelease</span></span> | <span data-ttu-id="a3505-126">結果にプレリリースパッケージが含まれます。</span><span class="sxs-lookup"><span data-stu-id="a3505-126">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="a3505-127">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="a3505-127">ExactMatch</span></span> | <span data-ttu-id="a3505-128">&lt; &gt; 大文字小文字を区別するパッケージ ID としてキーワードを使用するように指定します。</span><span class="sxs-lookup"><span data-stu-id="a3505-128">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="a3505-129">StartWith</span><span class="sxs-lookup"><span data-stu-id="a3505-129">StartWith</span></span> | <span data-ttu-id="a3505-130">パッケージ ID がキーワードで始まるパッケージを返し &lt; &gt; ます。</span><span class="sxs-lookup"><span data-stu-id="a3505-130">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="a3505-131">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="a3505-131">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="a3505-132">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="a3505-132">Common Parameters</span></span>

<span data-ttu-id="a3505-133">`Find-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="a3505-133">`Find-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="a3505-134">使用例</span><span class="sxs-lookup"><span data-stu-id="a3505-134">Examples</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```