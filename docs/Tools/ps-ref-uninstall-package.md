---
title: "NuGet の Uninstall-package PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 6/1/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: f4f5dc79-8e8e-4012-8986-873a5d9283d9
description: "Visual Studio で NuGet パッケージ マネージャー コンソールでアンインストール パッケージの PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、アンインストール パッケージ"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0899198a354a56615a48a1f7f428674a205f386b
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/05/2018
---
# <a name="uninstall-package-package-manager-console-in-visual-studio"></a><span data-ttu-id="c0814-104">Uninstall-package (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="c0814-104">Uninstall-Package (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="c0814-105">*このトピック内のコマンドをについて説明、 [NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。汎用の PowerShell アンインストール パッケージ コマンドでは、次を参照してください。、 [PowerShell PackageManagement 参照](/powershell/module/packagemanagement/?view=powershell-6)です。*</span><span class="sxs-lookup"><span data-stu-id="c0814-105">*This topic describes the command within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows. For the generic PowerShell Uninstall-Package command, see the [PowerShell PackageManagement reference](/powershell/module/packagemanagement/?view=powershell-6).*</span></span>

<span data-ttu-id="c0814-106">必要に応じてその依存関係を削除する、プロジェクトからパッケージを削除します。</span><span class="sxs-lookup"><span data-stu-id="c0814-106">Removes a package from a project, optionally removing its dependencies.</span></span> <span data-ttu-id="c0814-107">コマンドが失敗しない限り、その他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="c0814-107">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="syntax"></a><span data-ttu-id="c0814-108">構文</span><span class="sxs-lookup"><span data-stu-id="c0814-108">Syntax</span></span>

```ps
Uninstall-Package [-Id] <string> [-RemoveDependencies] [-ProjectName <string>] [-Force]
    [-Version <string>] [-WhatIf] [<CommonParameters>]
```

<span data-ttu-id="c0814-109">コマンドが失敗しない限り、その他のパッケージは、このパッケージに依存している場合、– Force オプションを指定します。</span><span class="sxs-lookup"><span data-stu-id="c0814-109">If other packages depend on this package, the command will fail unless the –Force option is specified.</span></span>

## <a name="parameters"></a><span data-ttu-id="c0814-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c0814-110">Parameters</span></span>

| <span data-ttu-id="c0814-111">パラメーター</span><span class="sxs-lookup"><span data-stu-id="c0814-111">Parameter</span></span> | <span data-ttu-id="c0814-112">説明</span><span class="sxs-lookup"><span data-stu-id="c0814-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="c0814-113">ID</span><span class="sxs-lookup"><span data-stu-id="c0814-113">Id</span></span> | <span data-ttu-id="c0814-114">(必須)アンインストールするパッケージの識別子。</span><span class="sxs-lookup"><span data-stu-id="c0814-114">(Required) The identifier of the package to uninstall.</span></span> <span data-ttu-id="c0814-115">-Id スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="c0814-115">The -Id switch itself is optional.</span></span> |
| <span data-ttu-id="c0814-116">Version</span><span class="sxs-lookup"><span data-stu-id="c0814-116">Version</span></span> | <span data-ttu-id="c0814-117">をアンインストールするパッケージのバージョン、現在インストールされているバージョンを既定とします。</span><span class="sxs-lookup"><span data-stu-id="c0814-117">The version of the package to uninstall, defaulting to the currently installed version.</span></span> |
| <span data-ttu-id="c0814-118">RemoveDependencies</span><span class="sxs-lookup"><span data-stu-id="c0814-118">RemoveDependencies</span></span> | <span data-ttu-id="c0814-119">パッケージとその未使用の依存関係をアンインストールします。</span><span class="sxs-lookup"><span data-stu-id="c0814-119">Uninstall the package and its unused dependencies.</span></span> <span data-ttu-id="c0814-120">つまり、すべての依存関係に依存している別のパッケージがある場合は、これはスキップされます。</span><span class="sxs-lookup"><span data-stu-id="c0814-120">That is, if any dependency has another package that depends on it, it's skipped.</span></span> |
| <span data-ttu-id="c0814-121">ProjectName</span><span class="sxs-lookup"><span data-stu-id="c0814-121">ProjectName</span></span> | <span data-ttu-id="c0814-122">既定で、既定のプロジェクト、パッケージをアンインストールするプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="c0814-122">The project from which to uninstall the package, defaulting to the default project.</span></span> |
| <span data-ttu-id="c0814-123">Force</span><span class="sxs-lookup"><span data-stu-id="c0814-123">Force</span></span> | <span data-ttu-id="c0814-124">場合でも、依存している他のパッケージをアンインストールするパッケージを強制します。</span><span class="sxs-lookup"><span data-stu-id="c0814-124">Forces a package to be uninstalled, even if other packages depend on it.</span></span> |
| <span data-ttu-id="c0814-125">WhatIf</span><span class="sxs-lookup"><span data-stu-id="c0814-125">WhatIf</span></span> | <span data-ttu-id="c0814-126">実際には、アンインストールを実行せず、コマンドを実行している場合にどうなるかを示します。</span><span class="sxs-lookup"><span data-stu-id="c0814-126">Shows what would happen when running the command without actually performing the uninstall.</span></span> |

<span data-ttu-id="c0814-127">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="c0814-127">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="c0814-128">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="c0814-128">Common Parameters</span></span>

<span data-ttu-id="c0814-129">`Uninstall-Package`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="c0814-129">`Uninstall-Package` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="c0814-130">使用例</span><span class="sxs-lookup"><span data-stu-id="c0814-130">Examples</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```
