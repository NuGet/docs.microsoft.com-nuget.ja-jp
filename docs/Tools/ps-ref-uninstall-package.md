---
title: "NuGet の Uninstall-package PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 06/01/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールでアンインストール パッケージの PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、アンインストール パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: db7cf9b2282bf40988eee2308c256381c4fd5124
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/20/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="f988b-104">Uninstall-package (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="f988b-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="f988b-105">*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。汎用の PowerShell アンインストール パッケージ コマンドでは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*</span><span class="sxs-lookup"><span data-stu-id="f988b-105">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="f988b-106">必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="f988b-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="f988b-107">コマンドが失敗しない限り、その他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="f988b-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="f988b-108">構文</span><span class="sxs-lookup"><span data-stu-id="f988b-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="f988b-109">コマンドが失敗しない限り、その他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="f988b-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="f988b-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f988b-110">Parameters</span></span>

| <span data-ttu-id="f988b-111">パラメーター</span><span class="sxs-lookup"><span data-stu-id="f988b-111">Parameter</span></span> | <span data-ttu-id="f988b-112">説明</span><span class="sxs-lookup"><span data-stu-id="f988b-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f988b-113">ID</span><span class="sxs-lookup"><span data-stu-id="f988b-113">Id</span></span> | <span data-ttu-id="f988b-114">(必須)アンインストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="f988b-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="f988b-115">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="f988b-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="f988b-116">Version</span><span class="sxs-lookup"><span data-stu-id="f988b-116">Version</span></span> | <span data-ttu-id="f988b-117">をアンインストールするパッケージのバージョン、現在インストールされているバージョンを既定とします。</span><span class="sxs-lookup"><span data-stu-id="f988b-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="f988b-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="f988b-118">RemoveDependencies</span></span> | <span data-ttu-id="f988b-119">パッケージとその未使用の依存関係をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="f988b-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="f988b-120">つまり、すべての依存関係に依存している別のパッケージがある場合は、これはスキップされます。</span><span class="sxs-lookup"><span data-stu-id="f988b-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="f988b-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="f988b-121">ProjectName</span></span> | <span data-ttu-id="f988b-122">既定で、既定のプロジェクト、パッケージをアンインストールするプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="f988b-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="f988b-123">Force</span><span class="sxs-lookup"><span data-stu-id="f988b-123">Force</span></span> | <span data-ttu-id="f988b-124">場合でも、依存している他のパッケージをアンインストールするパッケージを強制します。</span><span class="sxs-lookup"><span data-stu-id="f988b-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="f988b-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="f988b-125">WhatIf</span></span> | <span data-ttu-id="f988b-126">実際には、アンインストールを実行せず、コマンドを実行している場合にどうなるかを示します。</span><span class="sxs-lookup"><span data-stu-id="f988b-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="f988b-127">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="f988b-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="f988b-128">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="f988b-128">Common Parameters</span></span>

<span data-ttu-id="f988b-129">`Uninstall-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="f988b-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="f988b-130">使用例</span><span class="sxs-lookup"><span data-stu-id="f988b-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
