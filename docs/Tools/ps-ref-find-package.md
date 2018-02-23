---
title: "NuGet Find-package PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールで Find-package PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、Find-package"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 4303421c5f11177f3e5fc051a450934df47ab117
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="find-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ef307-104">Find-package (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="ef307-104">Find-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ef307-105">*Version 3.0 以降。このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。一般的な PowerShell Find-package コマンドは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*</span><span class="sxs-lookup"><span data-stu-id="ef307-105">*Version 3.0+; this topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Find-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ef307-106">パッケージ ソースから指定された ID またはキーワードに一致するリモート パッケージのセットを取得します。</span><span class="sxs-lookup"><span data-stu-id="ef307-106">Gets the set of remote packages with specified ID or keywords from the package source.</span></span>

## <a name="syntax"></a><span data-ttu-id="ef307-107">構文</span><span class="sxs-lookup"><span data-stu-id="ef307-107">Syntax</span></span>

```ps
Find-Package [-Id] <keywords> -Source <string> [-AllVersions] [-First [<int>]]
    [-Skip <int>] [-IncludePrerelease] [-ExactMatch] [-StartWith] [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="ef307-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="ef307-108">Parameters</span></span>

| <span data-ttu-id="ef307-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="ef307-109">Parameter</span></span> | <span data-ttu-id="ef307-110">説明</span><span class="sxs-lookup"><span data-stu-id="ef307-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ef307-111">Id&lt;キーワード&gt;</span><span class="sxs-lookup"><span data-stu-id="ef307-111">Id &lt;keywords&gt;</span></span> | <span data-ttu-id="ef307-112">(必須)パッケージ ソースの検索に使用するキーワードです。</span><span class="sxs-lookup"><span data-stu-id="ef307-112">(Required) Keywords to use when searching the package source.</span></span> <span data-ttu-id="ef307-113">ExactMatch-を使用して、パッケージ ID を持つが、キーワードと一致するパッケージのみを返します。</span><span class="sxs-lookup"><span data-stu-id="ef307-113">Use -ExactMatch to return only those packages whose package ID matches the keywords.</span></span> <span data-ttu-id="ef307-114">キーワードが指定されていない場合`Find-Package`によって指定される最初のダウンロード、または番号によって上位 20 のパッケージの一覧を返します。</span><span class="sxs-lookup"><span data-stu-id="ef307-114">If no keywords are given, `Find-Package` returns a list of the top 20 packages by downloads, or the number specified by -First.</span></span> <span data-ttu-id="ef307-115">-Id が省略可能なため、no-op に注意してください。</span><span class="sxs-lookup"><span data-stu-id="ef307-115">Note that -Id is optional and a no-op.</span></span> |
| <span data-ttu-id="ef307-116">ソース</span><span class="sxs-lookup"><span data-stu-id="ef307-116">Source</span></span> | <span data-ttu-id="ef307-117">検索するパッケージ ソースの URL またはフォルダーのパス。</span><span class="sxs-lookup"><span data-stu-id="ef307-117">The URL or folder path for the package source to search.</span></span> <span data-ttu-id="ef307-118">ローカル フォルダー パスには、絶対パス、または現在のフォルダーの相対パスを指定できます。</span><span class="sxs-lookup"><span data-stu-id="ef307-118">Local folder paths can be absolute, or relative to the current folder.</span></span> <span data-ttu-id="ef307-119">省略した場合、`Find-Package`現在選択されているパッケージ ソースを検索します。</span><span class="sxs-lookup"><span data-stu-id="ef307-119">If omitted, `Find-Package` searches the currently selected package source.</span></span> |
| <span data-ttu-id="ef307-120">AllVersions</span><span class="sxs-lookup"><span data-stu-id="ef307-120">AllVersions</span></span> | <span data-ttu-id="ef307-121">最新バージョンのみではなく、各パッケージのすべての利用可能なバージョンを表示します。</span><span class="sxs-lookup"><span data-stu-id="ef307-121">Displays all available versions of each package instead of only the latest version.</span></span> |
| <span data-ttu-id="ef307-122">First</span><span class="sxs-lookup"><span data-stu-id="ef307-122">First</span></span> | <span data-ttu-id="ef307-123">リストの先頭から返されるパッケージの数既定値は 20 です。</span><span class="sxs-lookup"><span data-stu-id="ef307-123">The number of packages to return from the beginning of the list; the default is 20.</span></span> |
| <span data-ttu-id="ef307-124">Skip</span><span class="sxs-lookup"><span data-stu-id="ef307-124">Skip</span></span> | <span data-ttu-id="ef307-125">最初の省略&lt;int&gt;表示される一覧からパッケージです。</span><span class="sxs-lookup"><span data-stu-id="ef307-125">Omits the first &lt;int&gt; packages from the displayed list.</span></span>  |
| <span data-ttu-id="ef307-126">IncludePrerelease</span><span class="sxs-lookup"><span data-stu-id="ef307-126">IncludePrerelease</span></span> | <span data-ttu-id="ef307-127">結果にリリース前のパッケージが含まれています。</span><span class="sxs-lookup"><span data-stu-id="ef307-127">Includes prerelease packages in the results.</span></span> |
| <span data-ttu-id="ef307-128">ExactMatch</span><span class="sxs-lookup"><span data-stu-id="ef307-128">ExactMatch</span></span> | <span data-ttu-id="ef307-129">使用する指定された&lt;キーワード&gt;大文字小文字を区別パッケージ ID と</span><span class="sxs-lookup"><span data-stu-id="ef307-129">Specified to use &lt;keywords&gt; as a case-sensitive package ID.</span></span> |
| <span data-ttu-id="ef307-130">始める</span><span class="sxs-lookup"><span data-stu-id="ef307-130">StartWith</span></span> | <span data-ttu-id="ef307-131">返します。 パッケージがパッケージ ID が始まる&lt;キーワード&gt;です。</span><span class="sxs-lookup"><span data-stu-id="ef307-131">Returns packages whose package ID begins with &lt;keywords&gt;.</span></span> |

<span data-ttu-id="ef307-132">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="ef307-132">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ef307-133">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="ef307-133">Common Parameters</span></span>

<span data-ttu-id="ef307-134">`Find-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="ef307-134">`Find-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ef307-135">使用例</span><span class="sxs-lookup"><span data-stu-id="ef307-135">Examples</span></span>

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
