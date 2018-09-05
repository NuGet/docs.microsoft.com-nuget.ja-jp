---
title: NuGet の Uninstall-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールのアンインストール パッケージの PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: ae60473fbb716b23f40b0605be8aaa8515802315
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551644"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="ec24f-103">Uninstall-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="ec24f-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="ec24f-104">*このトピックでは、内のコマンドを説明します、 [NuGet パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。一般的な PowerShell のアンインストール パッケージ コマンドは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)します。*</span><span class="sxs-lookup"><span data-stu-id="ec24f-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="ec24f-105">必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="ec24f-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="ec24f-106">コマンドが失敗しない限り、他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="ec24f-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="ec24f-107">構文</span><span class="sxs-lookup"><span data-stu-id="ec24f-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="ec24f-108">コマンドが失敗しない限り、他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="ec24f-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="ec24f-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="ec24f-109">Parameters</span></span>

| <span data-ttu-id="ec24f-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="ec24f-110">Parameter</span></span> | <span data-ttu-id="ec24f-111">説明</span><span class="sxs-lookup"><span data-stu-id="ec24f-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec24f-112">ID</span><span class="sxs-lookup"><span data-stu-id="ec24f-112">Id</span></span> | <span data-ttu-id="ec24f-113">(必須)アンインストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="ec24f-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="ec24f-114">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="ec24f-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="ec24f-115">Version</span><span class="sxs-lookup"><span data-stu-id="ec24f-115">Version</span></span> | <span data-ttu-id="ec24f-116">をアンインストールするパッケージのバージョン、現在インストールされているバージョンを既定値します。</span><span class="sxs-lookup"><span data-stu-id="ec24f-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="ec24f-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="ec24f-117">RemoveDependencies</span></span> | <span data-ttu-id="ec24f-118">パッケージとその未使用の依存関係をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="ec24f-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="ec24f-119">すべての依存関係の別のパッケージに依存している場合は、これはスキップされます。</span><span class="sxs-lookup"><span data-stu-id="ec24f-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="ec24f-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="ec24f-120">ProjectName</span></span> | <span data-ttu-id="ec24f-121">既定では、既定のプロジェクト、パッケージをアンインストールするプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="ec24f-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="ec24f-122">Force</span><span class="sxs-lookup"><span data-stu-id="ec24f-122">Force</span></span> | <span data-ttu-id="ec24f-123">場合でも、依存している他のパッケージは、アンインストールするパッケージを強制的にします。</span><span class="sxs-lookup"><span data-stu-id="ec24f-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="ec24f-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="ec24f-124">WhatIf</span></span> | <span data-ttu-id="ec24f-125">実際には、アンインストールを実行せず、コマンドを実行するときに何が起こるかを示します。</span><span class="sxs-lookup"><span data-stu-id="ec24f-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="ec24f-126">これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="ec24f-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="ec24f-127">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="ec24f-127">Common Parameters</span></span>

<span data-ttu-id="ec24f-128">`Uninstall-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="ec24f-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="ec24f-129">使用例</span><span class="sxs-lookup"><span data-stu-id="ec24f-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
