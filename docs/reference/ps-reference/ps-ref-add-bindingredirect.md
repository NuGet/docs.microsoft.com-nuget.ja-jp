---
title: NuGet BindingRedirect PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの BindingRedirect PowerShell コマンドのリファレンス。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: d3d156cf882229260e8cf55f8ece2804aec36dc9
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384985"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="83d2a-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="83d2a-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="83d2a-104">*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="83d2a-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="83d2a-105">プロジェクトの出力パス内のすべてのアセンブリを調べ、必要に応じて、アプリケーションまたは web 構成ファイルにバインドリダイレクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="83d2a-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="83d2a-106">このコマンドは、パッケージのインストール時に自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="83d2a-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="83d2a-107">バインディングリダイレクトとその使用理由の詳細については、.NET ドキュメントの「[アセンブリバージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="83d2a-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="83d2a-108">構文</span><span class="sxs-lookup"><span data-stu-id="83d2a-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="83d2a-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="83d2a-109">Parameters</span></span>

| <span data-ttu-id="83d2a-110">パラメータ</span><span class="sxs-lookup"><span data-stu-id="83d2a-110">Parameter</span></span> | <span data-ttu-id="83d2a-111">説明</span><span class="sxs-lookup"><span data-stu-id="83d2a-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="83d2a-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="83d2a-112">ProjectName</span></span> | <span data-ttu-id="83d2a-113">必要バインドリダイレクトを追加するプロジェクト。</span><span class="sxs-lookup"><span data-stu-id="83d2a-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="83d2a-114">-ProjectName スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="83d2a-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="83d2a-115">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="83d2a-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="83d2a-116">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="83d2a-116">Common Parameters</span></span>

<span data-ttu-id="83d2a-117">`Add-BindingRedirect` 次のサポート[一般的な PowerShell パラメーター](https://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="83d2a-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="83d2a-118">使用例</span><span class="sxs-lookup"><span data-stu-id="83d2a-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```