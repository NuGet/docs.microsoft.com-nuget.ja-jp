---
title: NuGet の登録/タブ拡張の PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの登録タブ拡張 PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 37aed96760e642b03c02bf31fe47a54f0e3cb74a
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/25/2019
ms.locfileid: "75384455"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="214e3-103">登録タブ拡張 (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="214e3-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="214e3-104">*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="214e3-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="214e3-105">指定されたコマンドのパラメーターにタブ拡張を登録します。これにより、コマンドを入力するときに Tab キーを使用すると、対象のパラメーターに使用可能なオプションとして展開値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="214e3-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="214e3-106">コマンドの以前の展開は上書きされます。</span><span class="sxs-lookup"><span data-stu-id="214e3-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="214e3-107">構文</span><span class="sxs-lookup"><span data-stu-id="214e3-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="214e3-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="214e3-108">Parameters</span></span>

| <span data-ttu-id="214e3-109">パラメータ</span><span class="sxs-lookup"><span data-stu-id="214e3-109">Parameter</span></span> | <span data-ttu-id="214e3-110">説明</span><span class="sxs-lookup"><span data-stu-id="214e3-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="214e3-111">[名前]</span><span class="sxs-lookup"><span data-stu-id="214e3-111">Name</span></span> | <span data-ttu-id="214e3-112">必要拡張を登録するコマンド。</span><span class="sxs-lookup"><span data-stu-id="214e3-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="214e3-113">-Name スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="214e3-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="214e3-114">Definition</span><span class="sxs-lookup"><span data-stu-id="214e3-114">Definition</span></span> | <span data-ttu-id="214e3-115">必要`@{'<parameter>' = {'<value1>', '<value2>', ...}}` 構文の引数を記述するオブジェクト。 `<parameter>` は変更するパラメーターの名前であり、各 `<value>` は特定の拡張を提供します。</span><span class="sxs-lookup"><span data-stu-id="214e3-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="214e3-116">単一引用符と二重引用符の両方が受け入れられます。</span><span class="sxs-lookup"><span data-stu-id="214e3-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="214e3-117">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="214e3-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="214e3-118">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="214e3-118">Common Parameters</span></span>

<span data-ttu-id="214e3-119">`Register-TabExpansion` 次のサポート[一般的な PowerShell パラメーター](https://go.microsoft.com/fwlink/?LinkID=113216): Debug、Error Action、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、WarningVariable、します。</span><span class="sxs-lookup"><span data-stu-id="214e3-119">`Register-TabExpansion` supports the following [common PowerShell parameters](https://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="214e3-120">使用例</span><span class="sxs-lookup"><span data-stu-id="214e3-120">Examples</span></span>

<span data-ttu-id="214e3-121">EventManager、Utilities、および特別なパーサーという3つのプロジェクト名が含まれるソリューションについて考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="214e3-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="214e3-122">開発者は、多くの場合、それぞれのプロジェクトで異なるタイミングで `Update-Package` コマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="214e3-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="214e3-123">`Update-Package` コマンドを使用すると、`-ProjectName` 引数に対してオートコンプリートを展開できるので便利です。そのため、毎回プロジェクト名を入力する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="214e3-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="214e3-124">次のコマンドを実行すると、これら3つのプロジェクト名が `-ProjectName` パラメーターの展開として登録されます。</span><span class="sxs-lookup"><span data-stu-id="214e3-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="214e3-125">開発者は `Update-Package -ProjectName `を入力し、Tab キーを押して、オートコンプリートオプションとして提供されている展開を確認できます。</span><span class="sxs-lookup"><span data-stu-id="214e3-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Register TabExpansion の使用例](media/Register-TabExpansion-Example.png)
