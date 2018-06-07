---
title: NuGet の Uninstall-package PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールでアンインストール パッケージの PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 860a58c359c9b723564a70f83aee4eee5cebf16d
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818868"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="6b7be-103">Uninstall-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="6b7be-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="6b7be-104">*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。汎用の PowerShell アンインストール パッケージ コマンドでは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*</span><span class="sxs-lookup"><span data-stu-id="6b7be-104">*This topic describes the command within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="6b7be-105">必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="6b7be-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="6b7be-106">コマンドが失敗しない限り、その他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7be-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="6b7be-107">構文</span><span class="sxs-lookup"><span data-stu-id="6b7be-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="6b7be-108">コマンドが失敗しない限り、その他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="6b7be-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="6b7be-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="6b7be-109">Parameters</span></span>

| <span data-ttu-id="6b7be-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="6b7be-110">Parameter</span></span> | <span data-ttu-id="6b7be-111">説明</span><span class="sxs-lookup"><span data-stu-id="6b7be-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6b7be-112">ID</span><span class="sxs-lookup"><span data-stu-id="6b7be-112">Id</span></span> | <span data-ttu-id="6b7be-113">(必須)アンインストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="6b7be-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="6b7be-114">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="6b7be-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="6b7be-115">Version</span><span class="sxs-lookup"><span data-stu-id="6b7be-115">Version</span></span> | <span data-ttu-id="6b7be-116">をアンインストールするパッケージのバージョン、現在インストールされているバージョンを既定とします。</span><span class="sxs-lookup"><span data-stu-id="6b7be-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="6b7be-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="6b7be-117">RemoveDependencies</span></span> | <span data-ttu-id="6b7be-118">パッケージとその未使用の依存関係をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="6b7be-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="6b7be-119">つまり、すべての依存関係に依存している別のパッケージがある場合は、これはスキップされます。</span><span class="sxs-lookup"><span data-stu-id="6b7be-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="6b7be-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="6b7be-120">ProjectName</span></span> | <span data-ttu-id="6b7be-121">既定で、既定のプロジェクト、パッケージをアンインストールするプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="6b7be-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="6b7be-122">Force</span><span class="sxs-lookup"><span data-stu-id="6b7be-122">Force</span></span> | <span data-ttu-id="6b7be-123">場合でも、依存している他のパッケージをアンインストールするパッケージを強制します。</span><span class="sxs-lookup"><span data-stu-id="6b7be-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="6b7be-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="6b7be-124">WhatIf</span></span> | <span data-ttu-id="6b7be-125">実際には、アンインストールを実行せず、コマンドを実行している場合にどうなるかを示します。</span><span class="sxs-lookup"><span data-stu-id="6b7be-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="6b7be-126">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="6b7be-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="6b7be-127">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="6b7be-127">Common Parameters</span></span>

<span data-ttu-id="6b7be-128">`Uninstall-Package` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="6b7be-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="6b7be-129">使用例</span><span class="sxs-lookup"><span data-stu-id="6b7be-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
