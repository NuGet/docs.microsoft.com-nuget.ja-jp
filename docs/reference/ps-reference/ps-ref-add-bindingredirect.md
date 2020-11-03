---
title: NuGet Add-BindingRedirect PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールで Add-BindingRedirect PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 382ba9b179428c70e3eb16db86a363e095207d61
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237258"
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="d4b2a-103">Add-BindingRedirect (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="d4b2a-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="d4b2a-104">*Windows の Visual Studio の [パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md) 内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="d4b2a-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="d4b2a-105">プロジェクトの出力パス内のすべてのアセンブリを調べ、必要に応じて、アプリケーションまたは web 構成ファイルにバインドリダイレクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="d4b2a-106">このコマンドは、パッケージのインストール時に自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-106">This command is run automatically when installing a package.</span></span>

> [!NOTE]
> <span data-ttu-id="d4b2a-107">これは、packages.config ファイルを使用するシナリオにのみ適用されます。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-107">This only applies to scenarios using a packages.config file.</span></span> <span data-ttu-id="d4b2a-108">詳細については、「 [NuGet packages.config ファイルリファレンス](~/reference/packages-config.md)」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-108">For more information, see [NuGet packages.config file reference](~/reference/packages-config.md).</span></span>

<span data-ttu-id="d4b2a-109">バインディングリダイレクトとその使用理由の詳細については、.NET ドキュメントの「 [アセンブリバージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions) 」を参照してください。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-109">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="d4b2a-110">構文</span><span class="sxs-lookup"><span data-stu-id="d4b2a-110">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="d4b2a-111">パラメーター</span><span class="sxs-lookup"><span data-stu-id="d4b2a-111">Parameters</span></span>

| <span data-ttu-id="d4b2a-112">パラメーター</span><span class="sxs-lookup"><span data-stu-id="d4b2a-112">Parameter</span></span> | <span data-ttu-id="d4b2a-113">説明</span><span class="sxs-lookup"><span data-stu-id="d4b2a-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d4b2a-114">ProjectName</span><span class="sxs-lookup"><span data-stu-id="d4b2a-114">ProjectName</span></span> | <span data-ttu-id="d4b2a-115">必要バインドリダイレクトを追加するプロジェクト。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-115">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="d4b2a-116">-ProjectName スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-116">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="d4b2a-117">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="d4b2a-118">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="d4b2a-118">Common Parameters</span></span>

<span data-ttu-id="d4b2a-119">`Add-BindingRedirect` は、Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数の [一般的な PowerShell パラメーター](/powershell/module/microsoft.powershell.core/about/about_commonparameters)をサポートしています。</span><span class="sxs-lookup"><span data-stu-id="d4b2a-119">`Add-BindingRedirect` supports the following [common PowerShell parameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="d4b2a-120">使用例</span><span class="sxs-lookup"><span data-stu-id="d4b2a-120">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```