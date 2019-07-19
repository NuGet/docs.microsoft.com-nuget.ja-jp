---
title: NuGet アンインストール-パッケージ PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの Uninstall-Package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 5c963588d28cab42e5fb6a43b31a17e26e49d0d2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327279"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="4024b-103">Uninstall-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="4024b-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="4024b-104">*このトピックでは、Windows 上の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内のコマンドについて説明します。汎用 PowerShell Uninstall-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="4024b-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="4024b-105">プロジェクトからパッケージを削除し、必要に応じて依存関係を削除します。</span><span class="sxs-lookup"><span data-stu-id="4024b-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="4024b-106">他のパッケージがこのパッケージに依存している場合、– Force オプションを指定しない限り、コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="4024b-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="4024b-107">構文</span><span class="sxs-lookup"><span data-stu-id="4024b-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="4024b-108">他のパッケージがこのパッケージに依存している場合、– Force オプションを指定しない限り、コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="4024b-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="4024b-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="4024b-109">Parameters</span></span>

| <span data-ttu-id="4024b-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="4024b-110">Parameter</span></span> | <span data-ttu-id="4024b-111">説明</span><span class="sxs-lookup"><span data-stu-id="4024b-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4024b-112">ID</span><span class="sxs-lookup"><span data-stu-id="4024b-112">Id</span></span> | <span data-ttu-id="4024b-113">必要アンインストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="4024b-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="4024b-114">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="4024b-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="4024b-115">Version</span><span class="sxs-lookup"><span data-stu-id="4024b-115">Version</span></span> | <span data-ttu-id="4024b-116">アンインストールするパッケージのバージョン。既定では、現在インストールされているバージョンが対象となります。</span><span class="sxs-lookup"><span data-stu-id="4024b-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="4024b-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="4024b-117">RemoveDependencies</span></span> | <span data-ttu-id="4024b-118">パッケージとその未使用の依存関係をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="4024b-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="4024b-119">つまり、依存関係に依存する別のパッケージがある場合、その依存関係はスキップされます。</span><span class="sxs-lookup"><span data-stu-id="4024b-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="4024b-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="4024b-120">ProjectName</span></span> | <span data-ttu-id="4024b-121">パッケージのアンインストール元のプロジェクト。既定のプロジェクトが既定のプロジェクトになります。</span><span class="sxs-lookup"><span data-stu-id="4024b-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="4024b-122">必ず</span><span class="sxs-lookup"><span data-stu-id="4024b-122">Force</span></span> | <span data-ttu-id="4024b-123">他のパッケージが依存している場合でも、パッケージを強制的にアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="4024b-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="4024b-124">WhatIf</span><span class="sxs-lookup"><span data-stu-id="4024b-124">WhatIf</span></span> | <span data-ttu-id="4024b-125">実際にアンインストールを実行せずにコマンドを実行した場合の動作を示します。</span><span class="sxs-lookup"><span data-stu-id="4024b-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="4024b-126">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="4024b-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="4024b-127">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="4024b-127">Common Parameters</span></span>

<span data-ttu-id="4024b-128">`Uninstall-Package`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。</span><span class="sxs-lookup"><span data-stu-id="4024b-128">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="4024b-129">使用例</span><span class="sxs-lookup"><span data-stu-id="4024b-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
