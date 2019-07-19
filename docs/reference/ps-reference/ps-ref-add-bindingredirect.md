---
title: NuGet BindingRedirect PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの BindingRedirect PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b1e88d32deb3ff34833ef22a9cbb8cad3f0d4354
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327459"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="938e4-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="938e4-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="938e4-104">*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="938e4-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="938e4-105">プロジェクトの出力パス内のすべてのアセンブリを調べ、必要に応じて、アプリケーションまたは web 構成ファイルにバインドリダイレクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="938e4-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="938e4-106">このコマンドは、パッケージのインストール時に自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="938e4-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="938e4-107">バインディングリダイレクトとその使用理由の詳細については、.NET ドキュメントの「[アセンブリバージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="938e4-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="938e4-108">構文</span><span class="sxs-lookup"><span data-stu-id="938e4-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="938e4-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="938e4-109">Parameters</span></span>

| <span data-ttu-id="938e4-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="938e4-110">Parameter</span></span> | <span data-ttu-id="938e4-111">説明</span><span class="sxs-lookup"><span data-stu-id="938e4-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="938e4-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="938e4-112">ProjectName</span></span> | <span data-ttu-id="938e4-113">必要バインドリダイレクトを追加するプロジェクト。</span><span class="sxs-lookup"><span data-stu-id="938e4-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="938e4-114">-ProjectName スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="938e4-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="938e4-115">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="938e4-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="938e4-116">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="938e4-116">Common Parameters</span></span>

<span data-ttu-id="938e4-117">`Add-BindingRedirect`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。</span><span class="sxs-lookup"><span data-stu-id="938e4-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="938e4-118">使用例</span><span class="sxs-lookup"><span data-stu-id="938e4-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```