---
title: NuGet アンインストール-パッケージ PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの Uninstall-Package PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 06/01/2017
ms.topic: reference
ms.openlocfilehash: 05b7bf0e8abad0904b9e851ea6b7a5317e74229d
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384416"
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="242bd-103">Uninstall-Package (Visual Studio パッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="242bd-103">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="242bd-104">*このトピックでは、Windows 上の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内のコマンドについて説明します。汎用 PowerShell Uninstall-Package コマンドについては、 [Powershell PackageManagement のリファレンス](/powershell/module/packagemanagement/?view=powershell-6)を参照してください。*</span><span class="sxs-lookup"><span data-stu-id="242bd-104">*This topic describes the command within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="242bd-105">プロジェクトからパッケージを削除し、必要に応じて依存関係を削除します。</span><span class="sxs-lookup"><span data-stu-id="242bd-105">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="242bd-106">他のパッケージがこのパッケージに依存している場合、–Force オプションを指定しない限り、コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="242bd-106">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="242bd-107">構文</span><span class="sxs-lookup"><span data-stu-id="242bd-107">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="242bd-108">他のパッケージがこのパッケージに依存している場合、–Force オプションを指定しない限り、コマンドは失敗します。</span><span class="sxs-lookup"><span data-stu-id="242bd-108">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="242bd-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="242bd-109">Parameters</span></span>

| <span data-ttu-id="242bd-110">パラメータ</span><span class="sxs-lookup"><span data-stu-id="242bd-110">Parameter</span></span> | <span data-ttu-id="242bd-111">説明</span><span class="sxs-lookup"><span data-stu-id="242bd-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="242bd-112">ID</span><span class="sxs-lookup"><span data-stu-id="242bd-112">Id</span></span> | <span data-ttu-id="242bd-113">必要アンインストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="242bd-113">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="242bd-114">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="242bd-114">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="242bd-115">Version</span><span class="sxs-lookup"><span data-stu-id="242bd-115">Version</span></span> | <span data-ttu-id="242bd-116">アンインストールするパッケージのバージョン。既定では、現在インストールされているバージョンが対象となります。</span><span class="sxs-lookup"><span data-stu-id="242bd-116">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="242bd-117">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="242bd-117">RemoveDependencies</span></span> | <span data-ttu-id="242bd-118">パッケージとその未使用の依存関係をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="242bd-118">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="242bd-119">つまり、依存関係に依存する別のパッケージがある場合、その依存関係はスキップされます。</span><span class="sxs-lookup"><span data-stu-id="242bd-119">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="242bd-120">ProjectName</span><span class="sxs-lookup"><span data-stu-id="242bd-120">ProjectName</span></span> | <span data-ttu-id="242bd-121">パッケージのアンインストール元のプロジェクト。既定のプロジェクトが既定のプロジェクトになります。</span><span class="sxs-lookup"><span data-stu-id="242bd-121">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="242bd-122">Force</span><span class="sxs-lookup"><span data-stu-id="242bd-122">Force</span></span> | <span data-ttu-id="242bd-123">他のパッケージが依存している場合でも、パッケージを強制的にアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="242bd-123">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="242bd-124">Whatif</span><span class="sxs-lookup"><span data-stu-id="242bd-124">WhatIf</span></span> | <span data-ttu-id="242bd-125">実際にアンインストールを実行せずにコマンドを実行した場合の動作を示します。</span><span class="sxs-lookup"><span data-stu-id="242bd-125">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="242bd-126">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="242bd-126">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="242bd-127">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="242bd-127">Common Parameters</span></span>

<span data-ttu-id="242bd-128">`Uninstall-Package` 次のサポート[一般的な PowerShell パラメーター](https://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="242bd-128">`Uninstall-Package` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="242bd-129">使用例</span><span class="sxs-lookup"><span data-stu-id="242bd-129">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
