---
title: NuGet のレジスタ TabExpansion PowerShell リファレンス
description: Visual Studio で NuGet パッケージ マネージャー コンソールで登録 TabExpansion PowerShell コマンドのリファレンスです。
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 8adb80af85e2e32fa8c35e5272cf90ff0c0ddcbb
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842480"
---
# <a name="register-tabexpansion-package-manager-console-in-visual-studio"></a><span data-ttu-id="2b687-103">登録 TabExpansion (Visual Studio でパッケージ マネージャー コンソール)</span><span class="sxs-lookup"><span data-stu-id="2b687-103">Register-TabExpansion (Package Manager Console in Visual Studio)</span></span>

<span data-ttu-id="2b687-104">*内でのみ使用可能な[パッケージ マネージャー コンソール](package-manager-console.md)Windows 上の Visual Studio でします。*</span><span class="sxs-lookup"><span data-stu-id="2b687-104">*Available only within the [Package Manager Console](package-manager-console.md) in Visual Studio on Windows.*</span></span>

<span data-ttu-id="2b687-105">展開された値が対象のパラメーターの使用可能なオプションとして表示するコマンドを入力するときにタブを使用する場合など、指定されたコマンドのパラメーターにタブ拡張を登録します。</span><span class="sxs-lookup"><span data-stu-id="2b687-105">Registers a tab expansion for the parameters of the specified command, such that when Tab is used when entering a command, the expanded values appear as available options for the parameter in question.</span></span> <span data-ttu-id="2b687-106">コマンドは、前の展開が上書きされます。</span><span class="sxs-lookup"><span data-stu-id="2b687-106">Any previous expansions for the command are overwritten.</span></span>

## <a name="syntax"></a><span data-ttu-id="2b687-107">構文</span><span class="sxs-lookup"><span data-stu-id="2b687-107">Syntax</span></span>

```ps
Register-TabExpansion [-Name] <String> [-Definition] <Object> [<CommonParameters>]
```

## <a name="parameters"></a><span data-ttu-id="2b687-108">パラメーター</span><span class="sxs-lookup"><span data-stu-id="2b687-108">Parameters</span></span>

| <span data-ttu-id="2b687-109">パラメーター</span><span class="sxs-lookup"><span data-stu-id="2b687-109">Parameter</span></span> | <span data-ttu-id="2b687-110">説明</span><span class="sxs-lookup"><span data-stu-id="2b687-110">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2b687-111">名前</span><span class="sxs-lookup"><span data-stu-id="2b687-111">Name</span></span> | <span data-ttu-id="2b687-112">(必須)拡張を登録するためにコマンド。</span><span class="sxs-lookup"><span data-stu-id="2b687-112">(Required) The command to which to register expansions.</span></span> <span data-ttu-id="2b687-113">-Name スイッチ自体は省略可能です。</span><span class="sxs-lookup"><span data-stu-id="2b687-113">The -Name switch itself is optional.</span></span> |
| <span data-ttu-id="2b687-114">定義</span><span class="sxs-lookup"><span data-stu-id="2b687-114">Definition</span></span> | <span data-ttu-id="2b687-115">(必須)構文の引数を表すオブジェクトです。`@{'<parameter>' = {'<value1>', '<value2>', ...}}`場所`<parameter>`を変更するパラメーターとそれぞれの名前を指定`<value>`固有の展開を提供します。</span><span class="sxs-lookup"><span data-stu-id="2b687-115">(Required) An object describing the argument in the syntax `@{'<parameter>' = {'<value1>', '<value2>', ...}}` where `<parameter>` is the name of the parameter to modify and each `<value>` provides a specific expansion.</span></span> <span data-ttu-id="2b687-116">両方一重引用符と二重引用符が受け入れられます。</span><span class="sxs-lookup"><span data-stu-id="2b687-116">Both single and double quotes are accepted.</span></span> |

<span data-ttu-id="2b687-117">これらのパラメーターには、パイプラインの入力またはワイルドカード文字がそのまま使用します。</span><span class="sxs-lookup"><span data-stu-id="2b687-117">None of these parameters accept pipeline input or wildcard characters.</span></span>

## <a name="common-parameters"></a><span data-ttu-id="2b687-118">共通パラメーター</span><span class="sxs-lookup"><span data-stu-id="2b687-118">Common Parameters</span></span>

<span data-ttu-id="2b687-119">`Register-TabExpansion` 次のサポート[一般的な PowerShell パラメーター](http://go.microsoft.com/fwlink/?LinkID=113216):デバッグ、エラー アクション、ErrorVariable、OutBuffer、OutVariable、PipelineVariable、Verbose、WarningAction、および WarningVariable します。</span><span class="sxs-lookup"><span data-stu-id="2b687-119">`Register-TabExpansion` supports the following [common PowerShell parameters](http://go.microsoft.com/fwlink/?LinkID=113216): Debug, Error Action, ErrorVariable, OutBuffer, OutVariable, PipelineVariable, Verbose, WarningAction, and WarningVariable.</span></span>

## <a name="examples"></a><span data-ttu-id="2b687-120">使用例</span><span class="sxs-lookup"><span data-stu-id="2b687-120">Examples</span></span>

<span data-ttu-id="2b687-121">EventManager、ユーティリティ、および SpecialParser の 3 つのプロジェクト名を含むソリューションを検討してください。</span><span class="sxs-lookup"><span data-stu-id="2b687-121">Consider a solution that contains three projects names EventManager, Utilities, and SpecialParser.</span></span> <span data-ttu-id="2b687-122">開発者が頻繁に使用して、`Update-Package`でこれらの各プロジェクトのさまざまなタイミングでコマンド。</span><span class="sxs-lookup"><span data-stu-id="2b687-122">The developer frequently uses the `Update-Package` command at different times with each of those projects.</span></span> <span data-ttu-id="2b687-123">便利なことを確認します、`Update-Package`コマンドは、展開を自動補完機能を提供する、`-ProjectName`引数たびにプロジェクト名を入力する必要があるので。</span><span class="sxs-lookup"><span data-stu-id="2b687-123">She finds it convenient to have the `Update-Package` command provide auto-completion expansions for the `-ProjectName` argument so she doesn't need to type out a project name each time.</span></span> 

<span data-ttu-id="2b687-124">次のコマンドがの拡張として次に、これら 3 つのプロジェクトの名前を登録、`-ProjectName`パラメーター。</span><span class="sxs-lookup"><span data-stu-id="2b687-124">The following command, then, registers those three project names as an expansion for the `-ProjectName` parameter:</span></span>

```ps
Register-TabExpansion Update-Package @{'ProjectName' = {'EventManager', 'Utilities', 'SpecialParser'}}    
```

<span data-ttu-id="2b687-125">入力できる開発者`Update-Package -ProjectName `、Tab キーを押して、オート コンプリート オプションとして提供される拡張を参照してください。</span><span class="sxs-lookup"><span data-stu-id="2b687-125">The developer can then type `Update-Package -ProjectName `, press Tab, and see the expansions offered as auto-completion options:</span></span>

![登録 TabExpansion の使用例](media/Register-TabExpansion-Example.png)
