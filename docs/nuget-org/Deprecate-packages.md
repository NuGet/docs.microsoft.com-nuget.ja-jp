---
title: nuget.org でのパッケージの廃止
description: パッケージの廃止プロセスと、クライアントがこの情報を表示する方法の詳細な説明
author: anangaur
ms.author: anangaur
ms.date: 09/23/2019
ms.topic: conceptual
ms.reviewer: karann-msft
ms.openlocfilehash: 70666ddf9cd7bdc448d29d4235e57bc91e2c003e
ms.sourcegitcommit: 60414a17af65237652c1de9926475a74856b91cc
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 11/14/2019
ms.locfileid: "74096880"
---
# <a name="deprecating-packages"></a><span data-ttu-id="f8246-103">パッケージの廃止</span><span class="sxs-lookup"><span data-stu-id="f8246-103">Deprecating packages</span></span>

<span data-ttu-id="f8246-104">パッケージを維持しなくなった場合、またはパッケージのコンシューマーに別のパッケージへの移動を促したい場合は、パッケージを廃止することができます。</span><span class="sxs-lookup"><span data-stu-id="f8246-104">You can deprecate a package if you no longer maintain a package or if would like to encourage your package's consumers to move to another package.</span></span> 

<span data-ttu-id="f8246-105">パッケージの廃止は、以下で説明するように、パッケージを**非公開**にすることとは異なります。</span><span class="sxs-lookup"><span data-stu-id="f8246-105">Package deprecation is different than **unlisting** your package as explained below:</span></span>
* <span data-ttu-id="f8246-106">パッケージを**非公開**にすると、検索結果に表示されなくなるため、検出できません。</span><span class="sxs-lookup"><span data-stu-id="f8246-106">**Unlisting** a package prevents its discovery because it is hidden in search results.</span></span> 
* <span data-ttu-id="f8246-107">パッケージを**廃止**すると、パッケージの既存のコンシューマーが、自分のプロジェクトでそれがインストールされているか、使用されているかを調べることができます。</span><span class="sxs-lookup"><span data-stu-id="f8246-107">**Deprecating** a package lets your package's existing consumers find out if they have it installed or used in their projects.</span></span> <span data-ttu-id="f8246-108">また、廃止の理由や、ユーザー (パッケージの発行元) によって指定された代替の推奨パッケージを知ることもできます。</span><span class="sxs-lookup"><span data-stu-id="f8246-108">It also lets them know the reason for deprecation and an alternate recommended package as specified by you (the package publisher).</span></span> <span data-ttu-id="f8246-109">パッケージを廃止しても、パッケージは非公開になりません。</span><span class="sxs-lookup"><span data-stu-id="f8246-109">Deprecating a package does not unlist the package.</span></span> 

<span data-ttu-id="f8246-110">発行元は、パッケージを非公開にすることも、廃止することもできます。</span><span class="sxs-lookup"><span data-stu-id="f8246-110">As a publisher, you may choose to both unlist as well as deprecate packages.</span></span>

## <a name="deprecation-workflow"></a><span data-ttu-id="f8246-111">廃止のワークフロー</span><span class="sxs-lookup"><span data-stu-id="f8246-111">Deprecation workflow</span></span>
1. <span data-ttu-id="f8246-112">パッケージを廃止するには、 **[パッケージの管理]** に移動して **[廃止]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f8246-112">To deprecate a package, go to **Manage packages** and select **Deprecation**:</span></span>

    ![パッケージの廃止オプションに移動する](media/deprecation-select-option.png)

2. <span data-ttu-id="f8246-114">廃止するバージョンを選択します。</span><span class="sxs-lookup"><span data-stu-id="f8246-114">Select the version you would like to deprecate.</span></span> <span data-ttu-id="f8246-115">すべてのバージョンを廃止する場合は、 **[Select all versions]\(バージョンをすべて選択\)** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="f8246-115">If you want to deprecate all version, choose **Select all versions** option.</span></span>

    ![廃止するパッケージのバージョンを選択する](media/deprecation-select-version.png)

3. <span data-ttu-id="f8246-117">廃止の理由を選択します。</span><span class="sxs-lookup"><span data-stu-id="f8246-117">Choose a reason for deprecation.</span></span> <span data-ttu-id="f8246-118">パッケージが維持されなくなった場合は、 **[レガシ]** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="f8246-118">If the package is no longer maintained, choose the **Legacy** option.</span></span> <span data-ttu-id="f8246-119">特定のバージョンに重大なバグがある場合は、 **[has critical bugs]\(重大なバグあり\)** オプションを選択します。</span><span class="sxs-lookup"><span data-stu-id="f8246-119">If the specific version has a critical bug, choose the **has critical bugs** option.</span></span> <span data-ttu-id="f8246-120">その他の理由については、 **[その他]** を選択します。</span><span class="sxs-lookup"><span data-stu-id="f8246-120">For any other reason, select **Other**.</span></span> <span data-ttu-id="f8246-121">代替の推奨パッケージ (およびバージョン) とカスタム メッセージを所有者に対していつでも指定できます。</span><span class="sxs-lookup"><span data-stu-id="f8246-121">You can always specify an alternate recommended package (and version) and a custom message to the owners.</span></span> 

    ![理由、代替の推奨パッケージ、カスタム メッセージを選択する](media/deprecation-save.png)

> [!Note]
> <span data-ttu-id="f8246-123">カスタム メッセージは nuget.org にのみ表示され、クライアントには表示されません。</span><span class="sxs-lookup"><span data-stu-id="f8246-123">Custom message is only shown on nuget.org but not from the clients.</span></span> <span data-ttu-id="f8246-124">現時点では、`dotnet.exe` や NuGet パッケージ マネージャーなどのクライアントにはカスタム メッセージが表示されません。</span><span class="sxs-lookup"><span data-stu-id="f8246-124">Currently, clients such as `dotnet.exe` and the NuGet Package Manager do not show the custom message.</span></span>

## <a name="client-experience-for-deprecated-packages"></a><span data-ttu-id="f8246-125">非推奨のパッケージのクライアント エクスペリエンス</span><span class="sxs-lookup"><span data-stu-id="f8246-125">Client experience for deprecated packages</span></span>
<span data-ttu-id="f8246-126">パッケージが非推奨になると、そのコンシューマーには次の方法で通知されます (使用しているクライアントによって異なります)。</span><span class="sxs-lookup"><span data-stu-id="f8246-126">Once a package has been deprecated, its consumers are notified about it in the following ways (depending upon the client used).</span></span>

### <a name="visual-studio"></a><span data-ttu-id="f8246-127">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f8246-127">Visual Studio</span></span> 
<span data-ttu-id="f8246-128">*Visual Studio 2019 バージョン 16.3 以降に適用*</span><span class="sxs-lookup"><span data-stu-id="f8246-128">*Available starting in Visual Studio 2019 version 16.3*</span></span>

<span data-ttu-id="f8246-129">Visual Studio では `Installed` タブに非推奨のパッケージの使用に関する警告が表示されます。その後、パッケージとその廃止情報 (非推奨とされた理由、代わりに使用する代替パッケージ (存在する場合)) に関する警告が表示されます。</span><span class="sxs-lookup"><span data-stu-id="f8246-129">Visual Studio warns about a deprecated package's usage on the `Installed` tab. It will show a warning for the package and its deprecation information (including the reason it was deprecated and the alternate package to use instead, if present).</span></span>

   ![Visual Studio のパッケージ マネージャーの [Installed] タブに表示された非推奨のパッケージ](media/deprecation-vs.png)

### <a name="dotnetexe"></a><span data-ttu-id="f8246-131">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="f8246-131">dotnet.exe</span></span>
<span data-ttu-id="f8246-132">*.NET SDK 3.0 以降に適用*</span><span class="sxs-lookup"><span data-stu-id="f8246-132">*Available starting with .NET SDK 3.0*</span></span>

<span data-ttu-id="f8246-133">dotnet.exe を使用する場合は、ソリューションまたはプロジェクト フォルダーに対して `dotnet list package --deprecated` コマンドを実行すると、非推奨のパッケージの一覧と廃止情報を取得できます。</span><span class="sxs-lookup"><span data-stu-id="f8246-133">If you use dotnet.exe, you can run the command `dotnet list package --deprecated` on the solution or project folder to get a list of deprecated packages along with the deprecation information:</span></span>

```
> dotnet list package --deprecated

The following sources were used:
   https://api.nuget.org/v3/index.json

Project `My.Test.Project` has the following deprecated packages
   [netcoreapp3.0]:
   Top-level Package      Resolved   Reason(s)   Alternative
   > My.Sample.Lib        6.0.0      Legacy      My.Awesome.Package

```
