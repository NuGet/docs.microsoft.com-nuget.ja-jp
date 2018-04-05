---
title: Visual Studio プロジェクト システムの NuGet サポート | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/09/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: サードパーティ プロジェクト タイプのために NuGet を Visual Studio プロジェクト システムに統合する
keywords: Visual Studio の NuGet, カスタム プロジェクト タイプ, Visual Studio プロジェクト
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0ffebfc9e403315482d3781a00a0a6896fd04f0c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/28/2018
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a><span data-ttu-id="7a58f-104">Visual Studio プロジェクト システムの NuGet サポート</span><span class="sxs-lookup"><span data-stu-id="7a58f-104">NuGet support for the Visual Studio project system</span></span>

<span data-ttu-id="7a58f-105">Visual Studio でサードパーティ プロジェクト タイプをサポートするために、NuGet 3.x+ は[共通プロジェクト システム (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) を、NuGet 3.2+ は非 CPS プロジェクト システムをサポートしています。</span><span class="sxs-lookup"><span data-stu-id="7a58f-105">To support third-party project types in Visual Studio, NuGet 3.x+ supports the [Common Project System (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md), and NuGet 3.2+ supports non-CPS project systems as well.</span></span>

<span data-ttu-id="7a58f-106">NuGet と統合するためには、プロジェクト システムはこのトピックで説明するすべてのプロジェクト機能に関して独自のサポートを公開する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7a58f-106">To integrate with NuGet, a project system must advertise its own support for all the project capabilities described in this topic.</span></span>

> [!Note]
> <span data-ttu-id="7a58f-107">パッケージを自分のプロジェクトにインストールする目的で、そのプロジェクトに実際にはない機能を宣言しないでください。</span><span class="sxs-lookup"><span data-stu-id="7a58f-107">Don't declare capabilities that your project does not actually have for the sake of enabling packages to install in your project.</span></span> <span data-ttu-id="7a58f-108">Visual Studio のさまざまな機能とその他の拡張機能は、NuGet クライアント以外のプロジェクト機能に依存します。</span><span class="sxs-lookup"><span data-stu-id="7a58f-108">Many features of Visual Studio and other extensions depend on project capabilities besides the NuGet client.</span></span> <span data-ttu-id="7a58f-109">自分のプロジェクトの機能を誤って公開すると、これらのコンポーネントに誤作動を引き起こし、ユーザー エクスペリエンスの質が落ちる可能性があります。</span><span class="sxs-lookup"><span data-stu-id="7a58f-109">Falsely advertising capabilities of your project can lead these components to malfunction and your users' experience to degrade.</span></span>

## <a name="advertise-project-capabilities"></a><span data-ttu-id="7a58f-110">プロジェクトの機能を公開する</span><span class="sxs-lookup"><span data-stu-id="7a58f-110">Advertise project capabilities</span></span>

<span data-ttu-id="7a58f-111">NuGet クライアントは、[プロジェクトの機能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)に基づいて、プロジェクト タイプと互換性のあるパッケージを判断します。これを次の表にまとめています。</span><span class="sxs-lookup"><span data-stu-id="7a58f-111">The NuGet client determines which packages are compatible with your project type based on the [project's capabilities](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md), as described in the following table.</span></span>

| <span data-ttu-id="7a58f-112">機能</span><span class="sxs-lookup"><span data-stu-id="7a58f-112">Capability</span></span> | <span data-ttu-id="7a58f-113">説明</span><span class="sxs-lookup"><span data-stu-id="7a58f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7a58f-114">AssemblyReferences</span><span class="sxs-lookup"><span data-stu-id="7a58f-114">AssemblyReferences</span></span> | <span data-ttu-id="7a58f-115">(WinRTReferences とは対照的に) プロジェクトがアセンブリ参照をサポートしていることを示します。</span><span class="sxs-lookup"><span data-stu-id="7a58f-115">Indicates that the project supports assembly references (distinct from WinRTReferences).</span></span> |
| <span data-ttu-id="7a58f-116">DeclaredSourceItems</span><span class="sxs-lookup"><span data-stu-id="7a58f-116">DeclaredSourceItems</span></span> | <span data-ttu-id="7a58f-117">プロジェクトが (DNX ではなく) 典型的な MSBuild プロジェクトであることを示します。このプロジェクトでは、プロジェクト自体でソース アイテムが宣言されます。</span><span class="sxs-lookup"><span data-stu-id="7a58f-117">Indicates that the project is a typical MSBuild project (not DNX) in that it declares source items in the project itself.</span></span> |
| <span data-ttu-id="7a58f-118">UserSourceItems</span><span class="sxs-lookup"><span data-stu-id="7a58f-118">UserSourceItems</span></span>|<span data-ttu-id="7a58f-119">任意のファイルをプロジェクトに追加することがユーザーに許可されることを示します。</span><span class="sxs-lookup"><span data-stu-id="7a58f-119">Indicates that the user is allowed to add arbitrary files to their project.</span></span> |

<span data-ttu-id="7a58f-120">CPS ベースのプロジェクト システムの場合、このセクションの残りで説明するプロジェクト機能の実装詳細は既に行われています。</span><span class="sxs-lookup"><span data-stu-id="7a58f-120">For CPS-based project systems, the implementation details for project capabilities described in the rest of this section have been done for you.</span></span> <span data-ttu-id="7a58f-121">「[declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)」 (CPS プロジェクトのプロジェクト機能の宣言) を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7a58f-121">See [declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project).</span></span>

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a><span data-ttu-id="7a58f-122">VsProjectCapabilitiesPresenceChecker を実装する</span><span class="sxs-lookup"><span data-stu-id="7a58f-122">Implementing VsProjectCapabilitiesPresenceChecker</span></span>

<span data-ttu-id="7a58f-123">`VsProjectCapabilitiesPresenceChecker` クラスは、次のように定義される `IVsBooleanSymbolPresenceChecker` インターフェイスを実装する必要があります。</span><span class="sxs-lookup"><span data-stu-id="7a58f-123">The `VsProjectCapabilitiesPresenceChecker` class must implement the `IVsBooleanSymbolPresenceChecker` interface, which is defined as follows:</span></span>

```cs
public interface IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// Checks whether the symbols defined may have changed since the last time
    /// this method was called.
    /// </summary>
    /// <param name="versionObject">
    /// The response version object assigned at the last call.
    /// May be null to get the initial version.
    /// At the conclusion of this method call, the reference may be changed so that on a subsequent call
    /// we know what version was last observed. The caller should treat this value as an opaque object,
    /// and should not assume any significance from whether the pointer changed or not.
    /// </param>
    /// <returns>
    /// <c>true</c> if the symbols defined may have changed since the last call to this method
    /// or if <paramref name="versionObject"/> was <c>null</c> upon entering this method.
    /// <c>false</c> if the responses would all be the same.
    /// </returns>
    bool HasChangedSince(ref object versionObject);

    /// <summary>
    /// Checks for the presence of a given symbol.
    /// </summary>
    /// <param name="symbol">The symbol to check for.</param>
    /// <returns><c>true</c> if the symbol is present; <c>false</c> otherwise.</returns>
    bool IsSymbolPresent(string symbol);
}
```

<span data-ttu-id="7a58f-124">このインターフェイスのサンプル実装は次のようになります。</span><span class="sxs-lookup"><span data-stu-id="7a58f-124">A sample implementation of this interface would then be:</span></span>

```cs
class VsProjectCapabilitiesPresenceChecker : IVsBooleanSymbolPresenceChecker
{
    /// <summary>
    /// The set of capabilities this project system actually has.
    /// This should be kept current, and honestly reflect what the project can do.
    /// </summary>
    private static readonly HashSet<string> ActualProjectCapabilities = new HashSet<string>(StringComparer.OrdinalIgnoreCase)
        {
            "AssemblyReferences",
            "DeclaredSourceItems",
            "UserSourceItems",
        };

    public bool HasChangedSince(ref object versionObject)
    {
        // If your project capabilities do not change over time while the project is open,
        // you may simply `return false;` from your `HasChangedSince` method.
        return false;
    }

    public bool IsSymbolPresent(string symbol)
    {
        return ActualProjectCapabilities.Contains(symbol);
    }
}
```

<span data-ttu-id="7a58f-125">必ず、自分のプロジェクト システムで実際にサポートされるものに基づいて設定された `ActualProjectCapabilities` から機能を追加/削除してください。</span><span class="sxs-lookup"><span data-stu-id="7a58f-125">Remember to add/remove capabilities from the `ActualProjectCapabilities` set based on what your project system actually supports.</span></span> <span data-ttu-id="7a58f-126">詳細については、[プロジェクト機能ドキュメント](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)を参照してください。</span><span class="sxs-lookup"><span data-stu-id="7a58f-126">See the [project capabilities documentation](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md) for full descriptions.</span></span>

## <a name="responding-to-queries"></a><span data-ttu-id="7a58f-127">クエリに応答する</span><span class="sxs-lookup"><span data-stu-id="7a58f-127">Responding to queries</span></span>

<span data-ttu-id="7a58f-128">プロジェクトは、`IVsHierarchy::GetProperty` を介して `VSHPROPID_ProjectCapabilitiesChecker` プロパティをサポートすることでこの機能を宣言します。</span><span class="sxs-lookup"><span data-stu-id="7a58f-128">A project declares this capability by supporting the  `VSHPROPID_ProjectCapabilitiesChecker` property through the `IVsHierarchy::GetProperty`.</span></span> <span data-ttu-id="7a58f-129">これは `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` アセンブリで定義される `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` のインスタンスを返すはずです。</span><span class="sxs-lookup"><span data-stu-id="7a58f-129">It should return an instance of `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker`, which is defined in the `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` assembly.</span></span> <span data-ttu-id="7a58f-130">[その NuGet パッケージ](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)をインストールすることでこのアセンブリを参照します。</span><span class="sxs-lookup"><span data-stu-id="7a58f-130">Reference this assembly by installing [its NuGet package](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime).</span></span>

<span data-ttu-id="7a58f-131">たとえば、次の `case` ステートメントを `IVsHierarchy::GetProperty` メソッドの `switch` ステートメントに追加します。</span><span class="sxs-lookup"><span data-stu-id="7a58f-131">For example, you might add the following `case` statement to your `IVsHierarchy::GetProperty` method's `switch` statement:</span></span>

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a><span data-ttu-id="7a58f-132">DTE サポート</span><span class="sxs-lookup"><span data-stu-id="7a58f-132">DTE Support</span></span>

<span data-ttu-id="7a58f-133">NuGet は、最上位 Visual Studio 自動化インターフェイスである [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017) を呼び出すことで、プロジェクト システムに参照、コンテンツ アイテム、MSBuild インポートを追加させます。</span><span class="sxs-lookup"><span data-stu-id="7a58f-133">NuGet drives the project system to add references, content items, and MSBuild imports by calling into [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017), which is the top-level Visual Studio automation interface.</span></span> <span data-ttu-id="7a58f-134">DTE は一連の COM インターフェイスであり、既に実装している場合があります。</span><span class="sxs-lookup"><span data-stu-id="7a58f-134">DTE is a set of COM interfaces that you may already implement.</span></span>

<span data-ttu-id="7a58f-135">プロジェクト タイプが CPS に基づく場合、DTE は自動的に実装されます。</span><span class="sxs-lookup"><span data-stu-id="7a58f-135">If your project type is based on CPS, DTE is implemented for you.</span></span>
