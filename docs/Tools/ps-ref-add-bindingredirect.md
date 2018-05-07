---
title: NuGet 追加 BindingRedirect PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールに追加 BindingRedirect PowerShell コマンドのリファレンスです。
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 7f1f2ef23e54ee48b577a2796b7f7b5f4c7eb284
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/26/2018
---
# <a name="add-bindingredirect-package-manager-console-in-visual-studio"></a><span data-ttu-id="379ed-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span><span class="sxs-lookup"><span data-stu-id="379ed-103">Add-BindingRedirect (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="379ed-104">*内でのみ使用可能な[NuGet Package Manager Console](package-manager-console.md) Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="379ed-104">*Available only within the [NuGet Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="379ed-105">プロジェクトの出力パス内のすべてのアセンブリを調べ、必要に応じて、アプリケーションまたは web 構成ファイルにバインド リダイレクトを追加します。</span><span class="sxs-lookup"><span data-stu-id="379ed-105">Examines all assemblies within the output path for a project and adds binding redirects to the application or web configuration file where necessary.</span></span> <span data-ttu-id="379ed-106">このコマンドは、パッケージをインストールするときに自動的に実行されます。</span><span class="sxs-lookup"><span data-stu-id="379ed-106">This command is run automatically when installing a package.</span></span>

<span data-ttu-id="379ed-107">バインディング リダイレクト、および使用する理由の詳細については、「[アセンブリ バージョンのリダイレクト](/dotnet/framework/configure-apps/redirect-assembly-versions).NET のドキュメントにします。</span><span class="sxs-lookup"><span data-stu-id="379ed-107">For details on binding redirects and why they are used, see [Redirecting Assembly Versions](/dotnet/framework/configure-apps/redirect-assembly-versions) in the .NET documentation.</span></span>

## <a name="syntax"></a><span data-ttu-id="379ed-108">構文</span><span class="sxs-lookup"><span data-stu-id="379ed-108">Syntax</span></span>

```ps
Add-BindingRedirect [-ProjectName] <string> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="379ed-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="379ed-109">Parameters</span></span>

| <span data-ttu-id="379ed-110">パラメーター</span><span class="sxs-lookup"><span data-stu-id="379ed-110">Parameter</span></span> | <span data-ttu-id="379ed-111">説明</span><span class="sxs-lookup"><span data-stu-id="379ed-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="379ed-112">ProjectName</span><span class="sxs-lookup"><span data-stu-id="379ed-112">ProjectName</span></span> | <span data-ttu-id="379ed-113">(必須)バインド リダイレクトを追加するプロジェクトです。</span><span class="sxs-lookup"><span data-stu-id="379ed-113">(Required) The project to which to add binding redirects.</span></span> <span data-ttu-id="379ed-114">-ProjectName スイッチ自体はオプションです。</span><span class="sxs-lookup"><span data-stu-id="379ed-114">The -ProjectName switch itself is optional.</span></span> |

<span data-ttu-id="379ed-115">これらのパラメーターのいずれもには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="379ed-115">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="379ed-116">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="379ed-116">Common Parameters</span></span>

<span data-ttu-id="379ed-117">`Add-BindingRedirect` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216): デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="379ed-117">`Add-BindingRedirect` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="379ed-118">使用例</span><span class="sxs-lookup"><span data-stu-id="379ed-118">Examples</span></span>

```ps
Add-BindingRedirect MyProject

Add-BindingRedirect -ProjectName MyProject
```