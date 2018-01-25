---
title: "NuGet 追加 BindingRedirect PowerShell リファレンス |Microsoft ドキュメント"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Visual Studio で NuGet パッケージ マネージャー コンソールに追加 BindingRedirect PowerShell コマンドのリファレンスです。"
keywords: "NuGet パッケージ マネージャー コンソールで、NuGet Powershell コマンドでは、NuGet Powershell リファレンス、追加 BindingRedirect"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b755970402f29a72b9a10f1a94e4a799e9cb71cf
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/25/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="07efa-104">(Visual Studio でパッケージ マネージャー コンソール) の追加-BindingRedirect</span><span class="sxs-lookup"><span data-stu-id="07efa-104">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="07efa-105">*内でのみ使用可能な[NuGet Package Manager Console](Package-Manager-Console.md) Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="07efa-105">*Available only within the [NuGet Package Manager Console](Package-Manager-Console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="07efa-106">プロジェクトの出力パス内のすべてのアセンブリを調べ、必要に応じて、アプリケーションまたは web 構成ファイルにバインド リダイレクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="07efa-106">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="07efa-107">このコマンドは、パッケージをインストールするときに自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="07efa-107">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="07efa-108">バインディング リダイレクト、および使用する理由の詳細については、「[アセンブリ バージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions).NET のドキュメントにします。</span><span class="sxs-lookup"><span data-stu-id="07efa-108">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="07efa-109">構文</span><span class="sxs-lookup"><span data-stu-id="07efa-109">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="07efa-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="07efa-110">Parameters</span></span>

| <span data-ttu-id="07efa-111">パラメーター</span><span class="sxs-lookup"><span data-stu-id="07efa-111">Parameter</span></span> | <span data-ttu-id="07efa-112">説明</span><span class="sxs-lookup"><span data-stu-id="07efa-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07efa-113">ProjectName</span><span class="sxs-lookup"><span data-stu-id="07efa-113">ProjectName</span></span> | <span data-ttu-id="07efa-114">(必須)バインド リダイレクトを追加するプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="07efa-114">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="07efa-115">-ProjectName スイッチ自体はオプションです。</span><span class="sxs-lookup"><span data-stu-id="07efa-115">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="07efa-116">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="07efa-116">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="07efa-117">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="07efa-117">Common Parameters</span></span>

<span data-ttu-id="07efa-118">`Add-BindingRedirect`次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="07efa-118">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="07efa-119">使用例</span><span class="sxs-lookup"><span data-stu-id="07efa-119">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```