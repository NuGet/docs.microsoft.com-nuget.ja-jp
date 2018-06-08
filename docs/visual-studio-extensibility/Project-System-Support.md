---
title: Visual Studio プロジェクト システムの NuGet サポート
description: サードパーティ プロジェクト タイプのために NuGet を Visual Studio プロジェクト システムに統合する
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/09/2017
ms.topic: reference
ms.openlocfilehash: b0937d5c149d79f25a776efac1946c9f42c161e8
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/06/2018
ms.locfileid: "34816905"
---
# <a name="nuget-support-for-the-visual-studio-project-system"></a>Visual Studio プロジェクト システムの NuGet サポート

Visual Studio でサードパーティ プロジェクト タイプをサポートするために、NuGet 3.x+ は[共通プロジェクト システム (CPS)](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/intro.md) を、NuGet 3.2+ は非 CPS プロジェクト システムをサポートしています。

NuGet と統合するためには、プロジェクト システムはこのトピックで説明するすべてのプロジェクト機能に関して独自のサポートを公開する必要があります。

> [!Note]
> パッケージを自分のプロジェクトにインストールする目的で、そのプロジェクトに実際にはない機能を宣言しないでください。 Visual Studio のさまざまな機能とその他の拡張機能は、NuGet クライアント以外のプロジェクト機能に依存します。 自分のプロジェクトの機能を誤って公開すると、これらのコンポーネントに誤作動を引き起こし、ユーザー エクスペリエンスの質が落ちる可能性があります。

## <a name="advertise-project-capabilities"></a>プロジェクトの機能を公開する

NuGet クライアントは、[プロジェクトの機能](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md)に基づいて、プロジェクト タイプと互換性のあるパッケージを判断します。これを次の表にまとめています。

| 機能 | 説明 |
| --- | --- |
| AssemblyReferences | (WinRTReferences とは対照的に) プロジェクトがアセンブリ参照をサポートしていることを示します。 |
| DeclaredSourceItems | プロジェクトが (DNX ではなく) 典型的な MSBuild プロジェクトであることを示します。このプロジェクトでは、プロジェクト自体でソース アイテムが宣言されます。 |
| UserSourceItems|任意のファイルをプロジェクトに追加することがユーザーに許可されることを示します。 |

CPS ベースのプロジェクト システムの場合、このセクションの残りで説明するプロジェクト機能の実装詳細は既に行われています。 「[declaring project capabilities in CPS projects](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/about_project_capabilities.md#how-to-declare-project-capabilities-in-your-project)」 (CPS プロジェクトのプロジェクト機能の宣言) を参照してください。

## <a name="implementing-vsprojectcapabilitiespresencechecker"></a>VsProjectCapabilitiesPresenceChecker を実装する

`VsProjectCapabilitiesPresenceChecker` クラスは、次のように定義される `IVsBooleanSymbolPresenceChecker` インターフェイスを実装する必要があります。

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

このインターフェイスのサンプル実装は次のようになります。

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

必ず、自分のプロジェクト システムで実際にサポートされるものに基づいて設定された `ActualProjectCapabilities` から機能を追加/削除してください。 詳細については、[プロジェクト機能ドキュメント](https://github.com/Microsoft/VSProjectSystem/blob/master/doc/overview/project_capabilities.md)を参照してください。

## <a name="responding-to-queries"></a>クエリに応答する

プロジェクトは、`IVsHierarchy::GetProperty` を介して `VSHPROPID_ProjectCapabilitiesChecker` プロパティをサポートすることでこの機能を宣言します。 これは `Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime.dll` アセンブリで定義される `Microsoft.VisualStudio.Shell.Interop.IVsBooleanSymbolPresenceChecker` のインスタンスを返すはずです。 [その NuGet パッケージ](https://www.nuget.org/packages/Microsoft.VisualStudio.Shell.Interop.14.0.DesignTime)をインストールすることでこのアセンブリを参照します。

たとえば、次の `case` ステートメントを `IVsHierarchy::GetProperty` メソッドの `switch` ステートメントに追加します。

```cs
case __VSHPROPID8.VSHPROPID_ProjectCapabilitiesChecker:
    propVal = new VsProjectCapabilitiesPresenceChecker();
    return VSConstants.S_OK;
```

## <a name="dte-support"></a>DTE サポート

NuGet は、最上位 Visual Studio 自動化インターフェイスである [DTE](/dotnet/api/envdte.dte?view=visualstudiosdk-2017) を呼び出すことで、プロジェクト システムに参照、コンテンツ アイテム、MSBuild インポートを追加させます。 DTE は一連の COM インターフェイスであり、既に実装している場合があります。

プロジェクト タイプが CPS に基づく場合、DTE は自動的に実装されます。
