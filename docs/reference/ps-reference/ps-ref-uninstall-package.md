---
title: NuGet Uninstall-Package PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Uninstall-Package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: d164176355e32e5bbe0a017fc2b291cbc9ef326a
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237128"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="7f323-103">Uninstall-Package (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="7f323-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="7f323-104">*このトピックでは、Windows 上の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内のコマンドについて説明します。汎用 PowerShell Uninstall-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="7f323-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="7f323-105">プロジェクトからパッケージを削除し、必要に応じて依存関係を削除します。</span><span class="sxs-lookup"><span data-stu-id="7f323-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="7f323-106">他のパッケージがこのパッケージに依存している場合、–Force オプションを指定しない限り、コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="7f323-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="7f323-107">構文</span><span class="sxs-lookup"><span data-stu-id="7f323-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="7f323-108">他のパッケージがこのパッケージに依存している場合、–Force オプションを指定しない限り、コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="7f323-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="7f323-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7f323-109">Parameters</span></span>

| <span data-ttu-id="7f323-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="7f323-110">Parameter</span></span> | <span data-ttu-id="7f323-111">説明</span><span class="sxs-lookup"><span data-stu-id="7f323-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7f323-112">Id</span><span class="sxs-lookup"><span data-stu-id="7f323-112">Id</span></span> | <span data-ttu-id="7f323-113">必要アンインストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="7f323-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="7f323-114">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="7f323-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="7f323-115">Version</span><span class="sxs-lookup"><span data-stu-id="7f323-115">Version</span></span> | <span data-ttu-id="7f323-116">アンインストールするパッケージのバージョン。既定では、現在インストールされているバージョンが対象となります。</span><span class="sxs-lookup"><span data-stu-id="7f323-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="7f323-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="7f323-117">RemoveDependencies</span></span> | <span data-ttu-id="7f323-118">パッケージとその未使用の依存関係をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="7f323-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="7f323-119">つまり、依存関係に依存する別のパッケージがある場合、その依存関係はスキップされます。</span><span class="sxs-lookup"><span data-stu-id="7f323-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="7f323-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="7f323-120">ProjectName</span></span> | <span data-ttu-id="7f323-121">パッケージのアンインストール元のプロジェクト。既定のプロジェクトが既定のプロジェクトになります。</span><span class="sxs-lookup"><span data-stu-id="7f323-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="7f323-122">Force</span><span class="sxs-lookup"><span data-stu-id="7f323-122">Force</span></span> | <span data-ttu-id="7f323-123">他のパッケージが依存している場合でも、パッケージを強制的にアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="7f323-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="7f323-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="7f323-124">WhatIf</span></span> | <span data-ttu-id="7f323-125">実際にアンインストールを実行せずにコマンドを実行した場合の動作を示します。</span><span class="sxs-lookup"><span data-stu-id="7f323-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="7f323-126">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="7f323-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="7f323-127">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="7f323-127">Common Parameters</span></span>

<span data-ttu-id="7f323-128">`Uninstall-Package` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="7f323-128">`Uninstall-Package` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="7f323-129">使用例</span><span class="sxs-lookup"><span data-stu-id="7f323-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```