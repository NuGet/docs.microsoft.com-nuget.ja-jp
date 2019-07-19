---
title: NuGet の登録/タブ拡張の PowerShell リファレンス
description: Visual Studio の NuGet パッケージマネージャーコンソールでの登録タブ拡張 PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 14cda695677e1052c78169fda097b72b460a9d43
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327299"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="b31e8-103">登録タブ拡張 (Visual Studio のパッケージマネージャーコンソール)</span><span class="sxs-lookup"><span data-stu-id="b31e8-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="b31e8-104">*Windows の Visual Studio の[パッケージマネージャーコンソール](../../consume-packages/install-use-packages-powershell.md)内でのみ使用できます。*</span><span class="sxs-lookup"><span data-stu-id="b31e8-104">*Available only within the [Package Manager Console](../../consume-packages/install-use-packages-powershell.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="b31e8-105">指定されたコマンドのパラメーターにタブ拡張を登録します。これにより、コマンドを入力するときに Tab キーを使用すると、対象のパラメーターに使用可能なオプションとして展開値が表示されます。</span><span class="sxs-lookup"><span data-stu-id="b31e8-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="b31e8-106">コマンドの以前の展開は上書きされます。</span><span class="sxs-lookup"><span data-stu-id="b31e8-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="b31e8-107">構文</span><span class="sxs-lookup"><span data-stu-id="b31e8-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="b31e8-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="b31e8-108">Parameters</span></span>

| <span data-ttu-id="b31e8-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="b31e8-109">Parameter</span></span> | <span data-ttu-id="b31e8-110">説明</span><span class="sxs-lookup"><span data-stu-id="b31e8-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b31e8-111">名前</span><span class="sxs-lookup"><span data-stu-id="b31e8-111">Name</span></span> | <span data-ttu-id="b31e8-112">必要拡張を登録するコマンド。</span><span class="sxs-lookup"><span data-stu-id="b31e8-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="b31e8-113">-Name スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="b31e8-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="b31e8-114">定義</span><span class="sxs-lookup"><span data-stu-id="b31e8-114">Definition</span></span> | <span data-ttu-id="b31e8-115">必要構文`@{'<parameter>' = {'<value1>', '<value2>', ...}}`の引数を記述するオブジェクト。ここ`<parameter>`で、は変更するパラメーターの名前であり`<value>` 、それぞれに特定の展開が用意されています。</span><span class="sxs-lookup"><span data-stu-id="b31e8-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="b31e8-116">単一引用符と二重引用符の両方が受け入れられます。</span><span class="sxs-lookup"><span data-stu-id="b31e8-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="b31e8-117">これらのパラメーターでは、パイプラインの入力やワイルドカード文字を受け入れません。</span><span class="sxs-lookup"><span data-stu-id="b31e8-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="b31e8-118">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="b31e8-118">Common Parameters</span></span>

<span data-ttu-id="b31e8-119">`Register-TabExpansion`では、次の[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216)がサポートされています。Debug、Error Action、ErrorVariable、OutBuffer、Outbuffer、PipelineVariable、Verbose、Warnings Action、および Warnings 変数。</span><span class="sxs-lookup"><span data-stu-id="b31e8-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="b31e8-120">使用例</span><span class="sxs-lookup"><span data-stu-id="b31e8-120">Examples</span></span>

<span data-ttu-id="b31e8-121">EventManager、Utilities、および特別なパーサーという3つのプロジェクト名が含まれるソリューションについて考えてみましょう。</span><span class="sxs-lookup"><span data-stu-id="b31e8-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="b31e8-122">開発者は、多く`Update-Package`の場合、各プロジェクトで異なるタイミングでコマンドを使用します。</span><span class="sxs-lookup"><span data-stu-id="b31e8-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="b31e8-123">この`Update-Package`コマンドを使用すると、 `-ProjectName`引数のオートコンプリートを展開できるので便利です。そのため、毎回プロジェクト名を入力する必要はありません。</span><span class="sxs-lookup"><span data-stu-id="b31e8-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="b31e8-124">次のコマンドを実行すると、これら3つのプロジェクト名が`-ProjectName`パラメーターの展開として登録されます。</span><span class="sxs-lookup"><span data-stu-id="b31e8-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="b31e8-125">開発者は、「 `Update-Package -ProjectName `」と入力し、tab キーを押して、オートコンプリートオプションとして提供されている展開を確認できます。</span><span class="sxs-lookup"><span data-stu-id="b31e8-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![Register TabExpansion の使用例](media/Register-TabExpansion-Example.png)
